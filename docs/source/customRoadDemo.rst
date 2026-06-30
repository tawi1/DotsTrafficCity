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

2. **Explore Sample Scene**: Open the ``Runtime CustomRoad Demo`` scene to review a basic implementation bridge.

	.. note::
		**Architectural Separation (Sample vs Production):**
		The classes ``RoadBase``, ``SplineRoad``, ``IntersectionRoad``, and the helper methods inside ``RoadSceneUtils`` are editor-time utilities provided **strictly as samples**. They illustrate how to extract node placement from Unity Splines. 

   In a production environment, you do not need these helper classes; instead, you populate the low-level data structures (``RuntimeSegmentCustom``, ``TrafficNodeData``, ``PathData``) directly from your game loop logic (e.g., procedural grids, server states, or save files).

How to Use: Step-by-Step Graph Initialization
---------------------------------------------

Follow these steps sequentially to generate a functional road layout directly via code.

Step 1: Instantiating the Root Runtime Segment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Every localized section of a road or an intersection must be encapsulated by a ``RuntimeSegmentCustom`` container. This tracking block manages the life cycle of its underlying paths and nodes.

.. code-block:: csharp

   // Define the physical center point of the road area
   Vector3 segmentCenter = new Vector3(50f, 0f, 17.5f);
   RuntimeSegmentCustom customSegment = new RuntimeSegmentCustom(segmentCenter);

Step 2: Designing Traffic Control Nodes (Segment Sides)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A ``TrafficNodeData`` represents a specific outer side (boundary) of a segment containing its own set of paths. The paths of this node enter the segment for the right lanes. The number of nodes depends entirely on the layout shape:
* **Straight Road**: Requires exactly **2 nodes** (an entry side and an exit side).
* **Intersection**: Requires **3 or more nodes** (one node for each approaching crossroad side).

	.. attention::
		**The Traffic Node Rotation Rule:**
		To align with the internal traffic navigation matrix, the rotation of an entry boundary node must look **backwards (oriented in the opposite direction)** relative to the track's path direction. Instead of hardcoding angles, this rotation should always be derived dynamically from the direction vector of the path's starting waypoints. Exit nodes face the natural forward path direction.

Setup the boundary structures dynamically based on your path direction. In this example, the straight road ends at ``(50f, 0f, 35f)``, which acts as the entry boundary for the next intersection segment:

.. code-block:: csharp

   Vector3 startPos = new Vector3(50f, 0f, 0f);
   Vector3 nextPos = new Vector3(50f, 0f, 5f); // Next waypoint to determine path direction
   Vector3 endPos = new Vector3(50f, 0f, 35f);  // Exact position where it connects to the intersection

   // Calculate the forward direction of the track path
   Vector3 pathDirection = Vector3.Normalize(nextPos - startPos);

   // Entry node rotation MUST look backwards from the forward path direction
   Quaternion entryRotation = Quaternion.LookRotation(-pathDirection);

   // Exit node rotation faces the natural forward path direction
   Quaternion exitRotation = Quaternion.LookRotation(pathDirection);

   // 1. Configure the Entry side node (Node Index 0)
   TrafficNodeData entryNode = new TrafficNodeData()
   {
       Owner = customSegment,
       Position = startPos,
       Rotation = entryRotation, // Derived dynamically from path direction
       LaneCountData = new Vector2Int(1, 1), // X: 1 Forward Lane, Y: 1 Backward Lane
       LaneWidth = 4.0f,
       NodeType = TrafficNodeType.Default,
       LocalNodeIndex = 0
   };

   // 2. Configure the Exit side node (Node Index 1 - enters the intersection)
   TrafficNodeData exitNode = new TrafficNodeData()
   {
       Owner = customSegment,
       Position = endPos,
       Rotation = exitRotation, // Facing forward
       LaneCountData = new Vector2Int(1, 1),
       LaneWidth = 4.0f,
       NodeType = TrafficNodeType.Default,
       LocalNodeIndex = 1
   };

   // Register nodes into the segment container
   customSegment.Nodes.Add(entryNode);
   customSegment.Nodes.Add(exitNode);

Step 3: Creating Two-Way Path Data (Right & Left Side Lanes)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Paths describe the precise trajectories vehicles follow between lane indexes of different nodes inside the segment. For a standard straight road, we create **two distinct paths** (one for the right-hand traffic going forward, and one for the left-hand lane going backward).

* **Speed limits** are processed internally using the Metric System (**meters per second**). Use the built-in abstraction helper ``SetSpeedLimitByKmh()`` to convert traditional values automatically.

.. code-block:: csharp

   // --- PATH 1: FORWARD PATH (Right side lane, from Entry Node 0 to Exit Node 1) ---
   PathData forwardPath = new PathData()
   {
       SourceLaneIndex = 0,      // Start lane index on the entry node
       ConnectedLaneIndex = 0,   // Target lane index on the destination node
       ConnectedNodeIndex = 1,   // The local array index of the destination node (exitNode)
       LocalPathIndex = 0
   };
   forwardPath.SetSpeedLimitByKmh(60f);

   // Right lane positions (shifted right by half of a lane width, e.g., 2 meters)
   Vector3 laneOffset = Quaternion.LookRotation(pathDirection) * Vector3.right * 2.0f;
   forwardPath.Waypoints.Add(startPos + laneOffset);
   forwardPath.Waypoints.Add(nextPos + laneOffset);
   forwardPath.Waypoints.Add(endPos + laneOffset);


   // --- PATH 2: BACKWARD PATH (Left side lane, from Exit Node 1 to Entry Node 0) ---
   PathData backwardPath = new PathData()
   {
       SourceLaneIndex = 0,      // Start lane index on the exit node (acting as entry for return path)
       ConnectedLaneIndex = 0,   // Target lane index on the entry node destination
       ConnectedNodeIndex = 0,   // The local array index of the destination node (entryNode)
       LocalPathIndex = 1
   };
   backwardPath.SetSpeedLimitByKmh(60f);

   // Left lane positions going in reverse direction (shifted left relative to forward path direction)
   backwardPath.Waypoints.Add(endPos - laneOffset);
   backwardPath.Waypoints.Add(nextPos - laneOffset);
   backwardPath.Waypoints.Add(startPos - laneOffset);


   // Bind both paths to the segment
   customSegment.AllPaths.Add(forwardPath);
   customSegment.AllPaths.Add(backwardPath);

Step 4: Adding Optional Pedestrian Infrastructure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If AI pedestrians are supported, sidewalk and crosswalk points are allocated by assigning standalone ``PedestrianNodeData`` structures within the same segment.

.. code-block:: csharp

   PedestrianNodeData sidewalkNode = new PedestrianNodeData()
   {
       Owner = customSegment,
       Position = new Vector3(54f, 0f, 17.5f), // Physical placement next to the roadway
       PedestrianNodeType = PedestrianNodeType.Default,
       NodeShapeType = NodeShapeType.Circle,
       ChanceToSpawn = 1.0f,
       Weight = 1.0f
   };

   customSegment.PedestrianNodes.Add(sidewalkNode);

Step 5: Submitting the Segment to the System Manager
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once the dataset within your ``RuntimeSegmentCustom`` instance is complete, invoke the synchronization pipeline of the system manager to build and inject Entity Component System (ECS) elements.

.. code-block:: csharp

   // Wrap your segment into an iterable list
   List<RuntimeSegmentCustom> segmentsToRegister = new List<RuntimeSegmentCustom> { customSegment };

   // Submit for instant integration
   roadManager.AddSegmentsSync(segmentsToRegister);

	.. note::
		**Node Stitched/Connections (v1.5.1+):**
		If **Auto Connect Nodes** is activated inside your ``RuntimeRoadManagerCustom`` settings, the system automatically checks external node proximities and stitches connections over cross-segment borders, removing the need for manual connection loops.

Procedural Example: Connecting a Straight Road to a 4-Way Intersection
-----------------------------------------------------------------------

This example demonstrates how to programmatically initialize a complex junction entity—a classic **4-Way X-Intersection**—where its southern boundary node seamlessly connects to the straight road created above by sharing the exact same position:

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

       // Configure 4 TrafficNodeData segment sides.
       // Notice that entry nodes are inverted (LookRotation(-dir)) according to the architectural rule.
       TrafficNodeData southNode = new TrafficNodeData() {
           Owner = intersectionSegment, Position = southPos, Rotation = Quaternion.LookRotation(-dirFromSouth),
           LaneCountData = new Vector2Int(1, 1), LaneWidth = 4.0f, LocalNodeIndex = 0
       };
       TrafficNodeData northNode = new TrafficNodeData() {
           Owner = intersectionSegment, Position = northPos, Rotation = Quaternion.LookRotation(dirFromSouth),
           LaneCountData = new Vector2Int(1, 1), LaneWidth = 4.0f, LocalNodeIndex = 1
       };
       TrafficNodeData westNode = new TrafficNodeData() {
           Owner = intersectionSegment, Position = westPos, Rotation = Quaternion.LookRotation(-dirFromWest),
           LaneCountData = new Vector2Int(1, 1), LaneWidth = 4.0f, LocalNodeIndex = 2
       };
       TrafficNodeData eastNode = new TrafficNodeData() {
           Owner = intersectionSegment, Position = eastPos, Rotation = Quaternion.LookRotation(dirFromWest),
           LaneCountData = new Vector2Int(1, 1), LaneWidth = 4.0f, LocalNodeIndex = 3
       };

       intersectionSegment.Nodes.Add(southNode); // LocalIndex 0
       intersectionSegment.Nodes.Add(northNode); // LocalIndex 1
       intersectionSegment.Nodes.Add(westNode);  // LocalIndex 2
       intersectionSegment.Nodes.Add(eastNode);  // LocalIndex 3

       // 2. Populate a RIGHT-TURN path (from South Side (0) to East Side (3))
       PathData southToEastPath = new PathData()
       {
           SourceLaneIndex = 0,
           ConnectedLaneIndex = 0,
           ConnectedNodeIndex = 3, // Array index of eastNode in Nodes list
           Priority = -5,           // Right turns typically get secondary cross priority
           LocalPathIndex = 0
       };
       southToEastPath.SetSpeedLimitByKmh(30f); // Slower speed limit for tight intersection curve

       // Shape the turn trajectory curve via a midpoint waypoint
       southToEastPath.Waypoints.Add(southPos);
       southToEastPath.Waypoints.Add(new Vector3(45f, 0f, 45f)); // Curve midpoint
       southToEastPath.Waypoints.Add(eastPos);

       intersectionSegment.AllPaths.Add(southToEastPath);

       // 3. Register the newly created intersection block into the runtime engine
       roadManager.AddSegmentsSync(new List<RuntimeSegmentCustom> { intersectionSegment });
   }

How to Dynamically Remove Segments
----------------------------------

To tear down a road grid or clear memory blocks during runtime execution, pass the active segment handles back to the clean-up registry loop.

.. code-block:: csharp

   // Unlinks the graph data from spatial hashes and safely unloads running entity references
   runtimeRoadManagerCustom.RemoveSegments(segmentsToRemove);

	.. warning::
		The provided code samples are for **demonstration purposes only** and are not fully functional for production use. They are designed to illustrate the API structure and data flow. You should implement your own robust error handling, edge-case management, and performance optimizations tailored to your specific project needs.

API Reference
-------------

Core Runtime Structures
~~~~~~~~~~~~~~~~~~~~~~~

``RuntimeSegmentCustom``
  The primary structural tracking entity containing all physical lane nodes, walkway links, and traffic behaviors for a specific area.
  
  * ``public List<TrafficNodeData> Nodes``: Grid of entry/exit boundaries (segment sides).
  * ``public List<PathData> AllPaths``: Track vectors mapped out within this block.
  * ``public List<PedestrianNodeData> PedestrianNodes``: Localized navigation graph markers for pedestrian simulation.

``TrafficNodeData``
  A low-level metadata block mapping out lane parameters across boundaries (segment sides).
  
  * ``public Vector2Int LaneCountData``: Vector tracking configurations where ``X`` controls forward capacity (entry lanes) and ``Y`` controls backward lanes (exit lanes).
  * ``public float LaneWidth``: Sets space width requirements per vehicle.
  * ``public Quaternion Rotation``: Direction orientation tracker. Must look backwards on entry nodes (calculated dynamically based on path direction vectors).

``PathData``
  Low-level mathematical structure housing positions tracking real-time vehicle routes.
  
  * ``public List<Vector3> Waypoints``: Coordinate lists shaping out lane trajectories.
  * ``public void SetSpeedLimitByKmh(float speedLimitKmh)``: Sets and scales target velocities appropriately to matching internal physics architectures (KM/H to M/S).

Manager Interaction Methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use these operational methods inside ``RuntimeRoadManagerCustom`` to affect changes over the entire live simulation grid:

* ``AddSegmentsSync(List<RuntimeSegmentCustom> segments)``: Blocks execution flow temporarily while constructing entities instantly. Use this for quick map adjustments.
* ``AddSegments(List<RuntimeSegmentCustom> segments)``: Asynchronous initialization routine. Recommended for vast chunks or heavily threaded procedural loading patterns to prevent frame drops.
* ``RemoveSegments(List<RuntimeSegmentCustom> segments)``: Immediately updates internal spatial hash indexes, ensuring traffic paths detour around deleted tracks seamlessly.