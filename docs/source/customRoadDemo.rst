.. _customRoadDemo:

Custom Road Demo
================

This guide provides a comprehensive step-by-step walkthrough on how to utilize the Runtime Road API to dynamically construct, register, and destroy traffic networks during gameplay.

Installation & Setup
--------------------

1. **Enable Scripting Define**: Open your project settings via **Project Settings -> Player -> Scripting Compile Symbols** and add the ``RUNTIME_ROAD`` directive. This symbol ensures all runtime simulation dependencies are included during compilation.

.. image:: /images/road/runtimeRoad/runtimeRoadInstall.png
   :alt: Runtime Road Installation Setup
   :align: center

2. **Architectural Note: Sample vs. Production Code**
   
   It is important to distinguish between demonstration samples and production-ready components:

   * **Production-Ready**: You should directly manipulate the low-level data structures (``RuntimeSegmentCustom``, ``TrafficNodeData``, ``PathData``) and the ``RuntimeRoadManagerCustom`` manager. These are pure data structures or ECS-compatible components fully intended for procedural run-time generation.
   * **Demonstration Only**: The classes ``RoadBase``, ``SplineRoad``, and ``IntersectionRoad`` are provided **strictly as samples**. They are intended to demonstrate how to extract data from Unity Splines and are not intended for use in production run-time environments.

   **Disclaimer**: The code examples in this guide are for **demonstration purposes only**. They are not fully functional for production use and do not include necessary error handling or performance optimizations. Please use them as a conceptual starting point to build your own robust implementation.

How to Use: Step-by-Step Graph Initialization
---------------------------------------------

Follow these steps sequentially to generate a functional road layout directly via code.

Step 1: Instantiating the Root Runtime Segment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Every localized section of a road or an intersection must be encapsulated by a ``RuntimeSegmentCustom`` container. This tracking block manages the life cycle of its underlying paths, traffic nodes, and pedestrian nodes.

.. code-block:: csharp

   // Define the physical center point of the road area
   Vector3 segmentCenter = new Vector3(50f, 0f, 17.5f);
   RuntimeSegmentCustom customSegment = new RuntimeSegmentCustom(segmentCenter);

Step 2: Designing Traffic Control Nodes and Associated Paths
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A ``TrafficNodeData`` represents a specific outer side (boundary) of a segment containing its own set of paths. The paths of this node enter the segment for the right lanes.
* **Straight Road**: Requires exactly **2 nodes** (an entry side and an exit side).
* **Intersection**: Requires **3 or more nodes** (one node for each approaching crossroad side).

Rather than manually adding nodes and paths directly into internal segment collections, always populate the ``TrafficNodeData`` first, prepare its outgoing ``PathData`` list, and then register them using the structured execution loop of ``AddNodeData``.

.. important::
   **The Traffic Node Rotation Rule:**
   To align with the internal traffic navigation matrix, the rotation of an entry boundary node must look **backwards (oriented in the opposite direction)** relative to the track's path direction. Exit nodes face the natural forward path direction.

.. image:: /images/road/runtimeRoad/runtimeRoadRotation.png
   :alt: Entry and Exit Node Rotation Constraint Diagram
   :align: center

Setup the boundary structures dynamically based on your path direction. In this example, the straight road ends at ``(50f, 0f, 35f)``, which acts as the entry boundary for the next intersection segment:

.. code-block:: csharp

   Vector3 startPos = new Vector3(50f, 0f, 0f);
   Vector3 nextPos = new Vector3(50f, 0f, 5f); // Next waypoint to determine path direction
   Vector3 endPos = new Vector3(50f, 0f, 35f);  // Exact position where it connects to the intersection

   // Calculate the forward direction of the track path
   Vector3 pathDirection = Vector3.Normalize(nextPos - startPos);
   Vector3 laneOffset = Quaternion.LookRotation(pathDirection) * Vector3.right * 2.0f;

   // ==========================================
   // 1. CONSTRUCT ENTRY NODE AND ITS PATHS (Index 0)
   // ==========================================
   TrafficNodeData entryNode = new TrafficNodeData()
   {
       Position = startPos,
       Rotation = Quaternion.LookRotation(-pathDirection), // Facing backward
       LaneCount = 1,
       LaneWidth = 4.0f,
   };

   // Create Forward Path (Right side lane, from Entry Node 0 to Exit Node 1)
   PathData forwardPath = new PathData()
   {
       SourceLaneIndex = 0,
       ConnectedLaneIndex = 0,
       ConnectedNodeIndex = 1, // Targets local node index 1 (the exitNode)
   };
   forwardPath.SetSpeedLimitByKmh(60f);
   forwardPath.Waypoints.Add(startPos + laneOffset);
   forwardPath.Waypoints.Add(nextPos + laneOffset);
   forwardPath.Waypoints.Add(endPos + laneOffset);

   List<PathData> entryNodePaths = new List<PathData> { forwardPath };

   // Safe atomic processing and index generation through the root container
   customSegment.AddNodeData(entryNode, entryNodePaths, registerNode: true);


   // ==========================================
   // 2. CONSTRUCT EXIT NODE AND ITS PATHS (Index 1)
   // ==========================================
   TrafficNodeData exitNode = new TrafficNodeData()
   {
       Position = endPos,
       Rotation = Quaternion.LookRotation(pathDirection), // Facing forward
       LaneCount = 1,
       LaneWidth = 4.0f,
   };

   // Create Backward Path (Left side lane, from Exit Node 1 back to Entry Node 0)
   PathData backwardPath = new PathData()
   {
       SourceLaneIndex = 0,
       ConnectedLaneIndex = 0,
       ConnectedNodeIndex = 0, // Targets local node index 0 (the entryNode)
   };
   backwardPath.SetSpeedLimitByKmh(60f);
   backwardPath.Waypoints.Add(endPos - laneOffset);
   backwardPath.Waypoints.Add(nextPos - laneOffset);
   backwardPath.Waypoints.Add(startPos - laneOffset);

   List<PathData> exitNodePaths = new List<PathData> { backwardPath };

   // Complete registration for the straight road segment
   customSegment.AddNodeData(exitNode, exitNodePaths, registerNode: true);

Step 3: Designing Pedestrian Navigation Nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pedestrian simulation tracks are defined using sequences of coordinates. To add pedestrian paths or crosswalks to your segment, avoid manual node initialization. Instead, simply pass your list of ``Vector3`` positions directly into the official ``AddPedestrianNodes`` API method.

* **Regular Sidewalks**: Pass a sequential list of positions representing sidewalk coordinates. The ``crosswalk`` optional parameter defaults to ``false``.
* **Pedestrian Crosswalks**: To construct a functioning crosswalk link, supply a list containing **exactly 2 positions** representing opposite sides of the traffic lanes, and you **must set the crosswalk parameter to true**.

.. important::
   **Automatic Crosswalk Stitching:**
   When a segment is compiled, the system **automatically stitches and links the outer end bounds of regular sidewalk tracks to the nearest crosswalk crossing nodes**, dynamically weaving them into a unified simulation mesh.

Here is an example of isolating this logic into clean, reusable helper methods:

.. code-block:: csharp

   // Method to build and register a standard sidewalk path from a list of positions
   public void AddSidewalkPath(RuntimeSegmentCustom segment, List<Vector3> positions)
   {
       // Forward the vector list directly to the official segment API method (crosswalk is false by default)
       segment.AddPedestrianNodes(positions);
   }

   // Method to create a dedicated road crosswalk link from exactly 2 positions
   public void AddCrosswalkLink(RuntimeSegmentCustom segment, List<Vector3> crossingPoints)
   {
       if (crossingPoints == null || crossingPoints.Count != 2)
       {
           Debug.LogError("A crosswalk requires exactly 2 boundary vector positions.");
           return;
       }

       // CRITICAL: For crosswalk generation, the crosswalk optional flag must be set to true
       segment.AddPedestrianNodes(crossingPoints, crosswalk: true);
   }

Procedural Example: Connecting a Straight Road to a 4-Way Intersection
-----------------------------------------------------------------------

This example demonstrates how to programmatically initialize a complex junction entity—a classic **4-Way X-Intersection**—where its southern boundary node seamlessly connects to the straight road created above by sharing the exact same position:

.. note::
   **Intersection Paths Simplification:**
   In a production environment, **every approaching node inside an intersection must contain its own set of internal paths** mapping out all allowed directions (e.g., left turns, right turns, straight movement). To keep this demonstration clear and prevent cluttered code, we will only map out a single right-turn path for the South Node, while the remaining nodes will be registered with empty path lists.

.. code-block:: csharp

   public void CreateProceduralIntersection(RuntimeRoadManagerCustom roadManager)
   {
       // 1. Instantiate the root intersection runtime segment
       Vector3 intersectionCenter = new Vector3(50f, 0f, 50f);
       RuntimeSegmentCustom intersectionSegment = new RuntimeSegmentCustom(intersectionCenter);

       // Physical centers of the 4 approaching sides (nodes)
       // Note: southPos is identical to the endPos of the straight road segment!
       Vector3 southPos = new Vector3(50f, 0f, 35f); 
       Vector3 northPos = new Vector3(50f, 0f, 65f);
       Vector3 westPos  = new Vector3(35f, 0f, 50f);
       Vector3 eastPos  = new Vector3(65f, 0f, 50f);

       // Calculate path direction vectors entering toward the intersection center
       Vector3 dirFromSouth = Vector3.Normalize(intersectionCenter - southPos);
       Vector3 dirFromWest  = Vector3.Normalize(intersectionCenter - westPos);

       // ==========================================
       // SOUTH NODE DATA SETUP (Local Index 0)
       // ==========================================
       TrafficNodeData southNode = new TrafficNodeData() {
           Position = southPos, Rotation = Quaternion.LookRotation(-dirFromSouth),
           LaneCount = 1, LaneWidth = 4.0f
       };

       // Populate a RIGHT-TURN path (from South Side (0) to East Side (3))
       PathData southToEastPath = new PathData()
       {
           Priority = -1,           // Secondary crossing priority constraints
       };
       southToEastPath.SetSpeedLimitByKmh(30f);
       southToEastPath.Waypoints.Add(southPos);
       southToEastPath.Waypoints.Add(new Vector3(45f, 0f, 45f)); // Curve midpoint
       southToEastPath.Waypoints.Add(eastPos);

       List<PathData> southNodePaths = new List<PathData> { southToEastPath };
       intersectionSegment.AddNodeData(southNode, southNodePaths, registerNode: true);

       // ==========================================
       // REMAINING INTERSECTION NODES SETUP
       // ==========================================
       TrafficNodeData northNode = new TrafficNodeData() {
           Position = northPos, Rotation = Quaternion.LookRotation(dirFromSouth),
           LaneCount = 1, LaneWidth = 4.0f
       };
       intersectionSegment.AddNodeData(northNode, new List<PathData>(), registerNode: true); // Local Index 1

       TrafficNodeData westNode = new TrafficNodeData() {
           Position = westPos, Rotation = Quaternion.LookRotation(-dirFromWest),
           LaneCount = 1, LaneWidth = 4.0f
       };
       intersectionSegment.AddNodeData(westNode, new List<PathData>(), registerNode: true);  // Local Index 2

       TrafficNodeData eastNode = new TrafficNodeData() {
           Position = eastPos, Rotation = Quaternion.LookRotation(dirFromWest),
           LaneCount = 1, LaneWidth = 4.0f
       };
       intersectionSegment.AddNodeData(eastNode, new List<PathData>(), registerNode: true);  // Local Index 3

       // 2. Automatically generate traffic light signaling configuration for the intersection
       intersectionSegment.AddTrafficLights();

       // 3. Register the newly created intersection block into the runtime engine
       roadManager.AddSegmentsSync(new List<RuntimeSegmentCustom> { intersectionSegment });
   }

Step 4: Configuring Traffic Lights and Signaling Phases
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before sending a segment to the manager, you must define its traffic light behavior if it acts as an intersection. You can configure signaling phases using one of the following approaches:

* **Automatic Generation**: Call the official ``AddTrafficLights()`` method on your segment. The system will analyze angles and positions of the registered traffic nodes, then automatically assign valid synchronized ``LightIndex`` IDs across the boundaries.
* **Manual Setup**: Manually assign the ``LightIndex`` property on each ``TrafficNodeData`` instance to map specific boundaries to custom traffic light phase queues or external controllers.

.. note::
   If you want the intersection to act as an unregulated crossing governed entirely by path priorities without traffic signals, set the ``ForceDisableLight`` property to ``true``.

.. code-block:: csharp

   // Approach A: Automatic calculation of signaling phases based on node positions
   customSegment.AddTrafficLights();

   // Approach B: Manual phase indexing per traffic node boundary
   // entryNode.LightIndex = 0;
   // exitNode.LightIndex = 1;

Step 5: Submitting the Segment to the System Manager
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once the dataset within your ``RuntimeSegmentCustom`` instance is complete, invoke the synchronization pipeline of the system manager to build and inject Entity Component System (ECS) elements.

.. code-block:: csharp

   // Wrap your segment into an iterable list
   List<RuntimeSegmentCustom> segmentsToRegister = new List<RuntimeSegmentCustom> { customSegment };

   // Submit for instant integration
   roadManager.AddSegmentsSync(segmentsToRegister);

.. important::
   **Automatic Node Stitching & Merging:**
   When different road segments connect, their boundary ``TrafficNodeData`` points **automatically stitch and merge together if they share the exact same spatial position** (or fall within internal proximity thresholds). The manager dynamically calculates cross-segment linkages over these borders, discarding the need to create manual external stitching logic loops during procedural network generation.

How to Dynamically Remove Segments
----------------------------------

To tear down a road grid or clear memory blocks during runtime execution, pass the active segment handles back to the clean-up registry loop.

.. code-block:: csharp

   // Unlinks the graph data from spatial hashes and safely unloads running entity references
   runtimeRoadManagerCustom.RemoveSegments(segmentsToRemove);


API Reference
-------------

Core Runtime Structures
~~~~~~~~~~~~~~~~~~~~~~~

``RuntimeSegmentCustom``
  The primary structural tracking entity containing all physical lane nodes, walkway links, and traffic behaviors for a specific area.
  
  * ``public void AddNodeData(TrafficNodeData node, List<PathData> nodePaths, bool registerNode = true)``: Registers a traffic node and its associated paths into the segment, automatically assigning sequential internal path tracking IDs.
  * ``public void AddPedestrianNodes(List<Vector3> positions, bool crosswalk = false)``: Official runtime API method to register pedestrian path networks directly from raw vector coordinate lists. Set ``crosswalk`` to ``true`` when creating specialized crossing routes.
  * ``public void AddTrafficLights()``: Analyzes registered node configurations and positions to automatically calculate and assign synchronized traffic light signaling phase indexes.
  * ``public bool ForceDisableLight { get; set; }``: When enabled, forces the segment to operate without traffic lights, relying purely on path crossing priorities.
  * ``public List<TrafficNodeData> Nodes``: Grid of entry/exit boundaries (segment sides).
  * ``public List<PathData> AllPaths``: Track vectors mapped out within this block.
  * ``public List<PedestrianNodeData> PedestrianNodes``: Localized navigation graph markers for pedestrian simulation.

``TrafficNodeData``
  A low-level metadata block mapping out lane parameters across boundaries (segment sides).
  
  * ``public RuntimeSegmentCustom Owner``: Reference to the parent runtime segment structure that holds this node.
  * ``public TrafficNodeData ConnectedExternalNode``: Reference to an adjacent segment's external node that this boundary node is stitched to.
  * ``public PedestrianNodeData CrosswalkNodeLeft``: Left-side boundary pedestrian node allocated for a crosswalk crossing.
  * ``public PedestrianNodeData CrosswalkNodeRight``: Right-side boundary pedestrian node allocated for a crosswalk crossing.
  * ``public TrafficNodeType NodeType``: Defines the structural node style constraint (e.g., Default, DestroyVehicle, etc.).
  * ``public Vector3 Position``: Spatial world position coordinates of this segment boundary side.
  * ``public Quaternion Rotation``: Direction orientation tracker. Must look backwards on entry nodes.
  * ``public Vector2Int LaneCountData``: Vector tracking configurations where ``X`` controls forward capacity (entry lanes) and ``Y`` controls backward lanes (exit lanes).
  * ``public float LaneWidth``: Sets space width requirements per vehicle (Defaults to 4.0).
  * ``public float Offset``: Side positioning offset shift value from standard path origin curves.
  * ``public float DividerWidth``: Physical center width separating left and right traffic lane rows.
  * ``public bool IsOneWay``: Toggles whether the route operates exclusively as a one-way path network.
  * ``public bool IsEndOfOneWay``: Designates if this node acts as the final terminal exit of a one-way road layout.
  * ``public bool AddPedestrianNodes``: Flag tracking whether regular sidewalk node structures should auto-generate here (Defaults to true).
  * ``public bool AddCrosswalk``: Toggles the auto-generation of pedestrian crosswalk markings across lanes (Defaults to true).
  * ``public float CrosswalkOffset``: Linear positioning displacement adjustment for the crosswalk link.
  * ``public int LightIndex``: Identifies the traffic light group/phase assigned to this specific boundary node. Can be assigned manually or generated automatically via ``AddTrafficLights()``. Defaults to ``-1`` (no traffic light).
  * ``public float ChanceToSpawn``: Density probability weight influencing vehicle background generation loops.
  * ``public float Weight``: Relative path selection preference modifier for traffic routing AI calculations.
  * ``public float CustomAchieveDistance``: Custom stopping distance accuracy tolerance value for paths intersecting near this boundary.
  * ``public int LocalNodeIndex { get; set; }``: The index position assigned to this unique node within its parent segment.
  * ``public int CrosswalkIndex``: Internal sequence tracker for crosswalk entity instances.
  * ``public bool InverseCrosswalk``: Property to mirror or flip crosswalk vector alignment.
  * ``public int MinLocalPathIndex { get; set; }``: Flat bounding helper representing the lowest localized index slice assigned to this node's tracks.
  * ``public int MaxLocalPathIndex { get; set; }``: Flat bounding helper representing the upper localized index boundary assigned to this node's tracks.

``PathData``
  Low-level mathematical structure housing positions tracking real-time vehicle routes. Refers directly to **PathData.cs**.
  
  * ``public List<Vector3> Waypoints``: Coordinate lists shaping out lane trajectories.
  * ``public int GlobalPathIndex``: A unique, absolute simulation path ID assigned automatically by the pipeline.
  * ``public int SourceLaneIndex``: The original source index track of the lane (if -1, it auto-detects based on layout).
  * ``public int ConnectedLaneIndex``: The target lane row index on the destination boundary side.
  * ``public int ConnectedNodeIndex``: Local index targeting the specific destination traffic node inside the segment.
  * ``public bool External``: Flag marking if this path forms a cross-boundary connection linking outward to a separate road segment.
  * ``public int LocalPathIndex { get; set; }``: The sequential sequence tracker assigned automatically by the parent runtime segment.
  * ``public float SpeedLimit``: Raw target maximum vehicle traversal speed limits tracked in meters per second (M/S).
  * ``public int Priority``: Crossing intersection priority ranking configuration (Higher values gain right-of-way).
  * ``public int TrafficGroup``: Mask filter group determining types of vehicles permitted to traverse this path lane.
  * ``public void SetSpeedLimitByKmh(float speedLimitKmh)``: Sets and scales target velocities appropriately to matching internal physics architectures (KM/H to M/S).

``PedestrianNodeData``
  Localized navigation graph markers managing civilian simulation walking path blocks. Refers directly to **PedestrianNodeData_2.cs**.
  
  * ``public int RuntimeID``: Absolute unique tracker ID assigned dynamically by the manager at network initialization.
  * ``public RuntimeSegmentCustom Owner``: Link reference to the parent custom runtime segment containing this walker node.
  * ``public PedestrianNodeData Previous``: Link node reference back to the previous coordinate step along the current sidewalk chain.
  * ``public PedestrianNodeData Next``: Link node reference targeting the subsequent coordinate node step forward along the sidewalk chain.
  * ``public List<PedestrianNodeData> CustomConnectedNodes``: Connection matrix managing non-standard pathway logic links (e.g., doorway pathways or branching side-alleys).
  * ``public Vector3 Position``: Exact 3D world space coordinates locating this specific pedestrian junction marker.
  * ``public int ConnectedNodeIndex``: Structural connection index marker pointing towards neighboring target traffic nodes.
  * ``public int LightIndex``: Maps the node to a specific pedestrian crosswalk light signaling step phase. Defaults to ``-1``.
  * ``public PedestrianNodeType PedestrianNodeType``: Defines behavioral mode attributes assigned to the node (e.g., Default, Crosswalk, etc.).
  * ``public NodeShapeType NodeShapeType``: Form shape layout style for target reaching mechanics (e.g., Circle, Square bounding).
  * ``public bool CanSpawnInView``: Toggles whether fresh pedestrian agents can spawn on this node inside active camera viewing fields.
  * ``public float ChanceToSpawn``: AI traffic density distribution weight configuration.
  * ``public float Weight``: Pathfinding cost weight modifier used during long-distance walking route calculations.
  * ``public float CustomAchieveDistance``: Specific reaching threshold overriding default proximity target arrival checks.
  * ``public float Width``: Area space sizing width parameter assigned to the pedestrian track node.
  * ``public float Height``: Area space sizing height parameter assigned to the pedestrian track node.
  * ``public bool HasMovementRandomOffset``: Enables chaotic walk variance drift distributions preventing pedestrians from walking in a single thin line.

Manager Interaction Methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~

``RuntimeRoadManagerCustom``
  The main runtime engine manager coordinating initialization, stitching, lifecycle tracking, and destruction of entities within the ECS world.

  **Properties & Fields**
  
  * ``public bool InProgress { get; }``: Returns true if there is an active asynchronous construction or processing batch currently executing.

  **Public Methods**

  * ``public void AddSegmentsSync(List<RuntimeSegmentCustom> segments)``: Blocks execution flow temporarily while constructing and stitching entities instantly within the simulation grid. Use this for immediate runtime map generation or small updates.
  * ``public void AddSegments(List<RuntimeSegmentCustom> segments)``: Starts a background asynchronous initialization routine for the submitted list. Highly recommended for vast chunks or heavily threaded procedural environments to prevent frame rate drops.
  * ``public void AddSegmentsAsync(List<RuntimeSegmentCustom> segments, Action<List<RuntimeSegmentCustom>> onResult = null, int addSegmentPerIteration = 20)``: Spawns a Coroutine task that incrementally initializes a fixed batch of segments (``addSegmentPerIteration``) per frame, triggering an optional callback complete loop (``onResult``) when done.
  * ``public async Task AddSegmentsAsyncTask(List<RuntimeSegmentCustom> segments)``: A fully async/await compatible asynchronous wrapper task that completes when all requested segments have successfully processed and loaded into the active world state.
  * ``public void CreateCustomRuntimeNodes(List<PedestrianNodeData> pedestrianNodes)``: Low-level initialization loop that processes a collection of pedestrian nodes, pre-calculating boundaries, checking crosswalk links, and registering them within the simulation grid. **Note:** This method requires the ``runtimePedestrianNodes`` feature flag to be enabled in the manager's Inspector.
  * ``public void CreateCustomRuntimeNode(PedestrianNodeData pedestrianNode)``: Low-level method to initialize a single pedestrian node. It generates its runtime tracking ID, sets up connections with neighboring nodes, and prepares its position data for the pedestrian simulation hash grid. **Note:** This method requires the ``runtimePedestrianNodes`` feature flag to be enabled in the manager's Inspector.
  * ``public void RemoveSegments(List<RuntimeSegmentCustom> segments)``: Immediately removes and cleans up the specified list of road segments. It clears spatial hash index positions, removes tracking data from neighbor nodes, and unloads any live simulation entities safely.