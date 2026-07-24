.. _customRuntimeSegment:

Custom Runtime Segment Generation
=================================

Overview
--------

The **DOTS Traffic City** framework provides a flexible pipeline for generating road network topology completely at runtime. Instead of relying purely on pre-baked authoring assets in the Unity Editor, you can programmatically construct straight road segments, build complex crossroads, and link pedestrian paths on the fly.

This approach is ideal for procedural city generation, dynamic map chunk loading, or custom runtime road creation tools.

Key Components & Utilities
---------------------------

* **RuntimeGenerationUtils**: A static helper class containing low-level path calculations, Bezier curve evaluations, straight segment math, and automated crossroad topology generation.
* **RuntimeGenerationPool**: A zero-allocation object pool used to pop and recycle ``RuntimeSegmentCustom``, ``TrafficNodeData``, and ``PathData`` instances during runtime operations.
* **RuntimeRoadManagerCustom**: The runtime manager responsible for registering generated road segments into the live DOTS simulation world.

Generating Auto Crossroads
---------------------------

The framework provides automated crossroad generation via ``RuntimeGenerationUtils.GenerateAutoCrossroad()``. There are two primary workflows for generating an intersection segment:

1. Standard Crossroad Setup
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Construct a single ``RuntimeSegmentCustom`` object, attach boundary traffic nodes to it, and pass it into the generator:

.. code-block:: csharp

    // Generate internal paths, lane connections, U-turns, and crosswalks
    RuntimeGenerationUtils.GenerateAutoCrossroad(newSegment, generationSettings);

2. Stitching Existing Connected Straight Roads
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can also stitch together an intersection from existing straight road segments whose endpoint nodes already meet at the junction center:

.. code-block:: csharp

    // Collect boundary nodes from straight roads pointing to the junction
    List<TrafficNodeData> connectedStraightRoadNodes = GetConnectedEndpointNodes();

    // Generate the crossroad by connecting existing boundary nodes
    RuntimeSegmentCustom newIntersection = RuntimeGenerationUtils.GenerateAutoCrossroad(
        connectedStraightRoadNodes, 
        baseLightContainer, 
        generationSettings, 
        areExistsNodes: true
    );

    // Add the newly created intersection segment to your segment list
    newSegments.Add(newIntersection);

.. note::
   Setting ``areExistsNodes: true`` tells the utility to reuse the boundary transformations and configuration of existing nodes rather than instantiating new ones. This ensures seamless lane stitching between pre-existing straight roads and the new crossroad.

Sample Scene: Runtime Generation
--------------------------------

The framework includes a dedicated sample scene demonstrating dynamic road segment generation from raw data and intersection creation at runtime:

* **Location**: ``Spirit604/DotsCity/Samples/RuntimeGenerationSample/RuntimeGenerationSample.unity``
* **Script**: ``RuntimeGenerationSample.cs``

.. note::
   **Demonstration Notice**: The road creators (``RoadSegmentCreator``) and scene objects present in this sample scene are used **strictly as data containers** to extract raw parameters (such as waypoint positions, lane widths, and connection rules) for API demonstration purposes. 
   
   You are **not limited** to using these editor components. The runtime generation API is entirely decoupled from scene MonoBehaviours, allowing you to feed your own custom data sources (e.g., procedural grid generators, tilemap databases, external JSON files, or network streams) directly into ``RuntimeGenerationUtils``.

How the Sample Works
~~~~~~~~~~~~~~~~~~~~

1. **Initialization & Pooling Warmup**:
   On ``Start()``, the sample initializes the ``RuntimeGenerationPool`` and calls ``RuntimeGenerationUtils.Warmup()`` to pre-allocate internal collection capacities, eliminating garbage collector allocations during road generation.

2. **Parsing Raw Road Data**:
   The sample iterates over a list of reference editor road objects purely to read their underlying structural data (lane count, width, speed limits, pedestrian spacing) as an input source.

3. **Processing Straight Roads vs. Crossroads**:
   
   * **Straight Roads**: Evaluates middle waypoint positions, pops nodes from the pool, and calls ``RuntimeGenerationUtils.GenerateStraightSegment()`` to build multi-lane geometry and lateral pedestrian paths.
   * **Crossroads**: Assigns shared traffic light containers and automatically computes turns, Bezier curves, and pedestrian links via ``RuntimeGenerationUtils.GenerateAutoCrossroad()``.

4. **Registering with Simulation World**:
   Once segments are generated, they are registered synchronously with the DOTS world using ``runtimeRoadManagerCustom.AddSegmentsSync(newSegments)``.

5. **Traffic Light & Frame Binding**:
   Upon completion of segment addition, physical traffic light MonoBehaviours in the scene are bound to their respective crossroad IDs via ``RegisterTrafficLights()``.

Best Practices
--------------

* **Use Custom Data Sources**: Feel free to replace the sample's scene road references with your own custom runtime data structures or procedural algorithms.
* **Use Object Pooling**: Always use ``RuntimeGenerationPool.Instance.PopSegment()`` and ``PopTrafficNode()`` instead of instantiating new objects directly to prevent GC spikes during runtime generation.
* **Recycle Removed Segments**: When tearing down chunks or removing road segments, return them to the pool using ``runtimeGenerationPool.RecycleSegment(segment)``.
* **Pre-allocate with Warmup**: Call ``RuntimeGenerationUtils.Warmup()`` during game startup or scene loading to ensure zero-allocation performance when constructing road networks dynamically.