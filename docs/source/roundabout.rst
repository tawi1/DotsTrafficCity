.. _roadSegmentCreatorRoundabout:

Roundabout
----------

The `Roundabout` component works in tandem with the :ref:`RoadSegmentCreator <roadSegmentCreator>` to automatically generate complex circular intersections. The tool supports two primary workflows: creating a standard roundabout from scratch using purely inspector-defined metrics, or generating a custom roundabout fitted directly onto the existing traffic nodes of approaching roads.

Method 1. Inspector Only Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This method is ideal for creating a standalone roundabout "from scratch" in an empty area of the scene, where you manually define the dimensions and the number of connection points.

#. Create a :ref:`RoadSegment <roadSegment>`.
#. In the `RoadSegmentCreator` component, select **Roundabout** as the road segment type (the `Roundabout` script component will be attached automatically).
#. In the **Current Generation Type** dropdown, select ``InspectorOnly``.
#. Configure the base parameters of the roundabout in the Inspector:
   
   * **Entrance Node Count**: The number of entry/exit roads connecting to the roundabout (ranges from 3 to 10).
   * **Outer Radius**: The distance from the center to the entrance/exit nodes.
   * **Inner Radius**: The radius of the inner central island.
   * **Inner Lane Count** & **Lane Width**: The number and width of the lanes inside the circle.

#. Press the `Create` button to generate the road layout.
#. If you need to fine-tune the layout, you can manually move elements directly in the Scene View using Gizmos handles by selecting the appropriate **Active Handle** mode.

Method 2. Custom Mode (Based on Existing Roads)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This method allows you to seamlessly integrate a roundabout into your current road network. Instead of creating a standalone asset and trying to snap it manually, the tool uses the final :ref:`Traffic Nodes <trafficNode>` of the straight roads that approach the intersection as anchor points.

#. Create a :ref:`RoadSegment <roadSegment>` and set its road segment type to **Roundabout** via the `RoadSegmentCreator`.
#. Set the **Current Generation Type** parameter to ``Custom`` in the `Roundabout` component.
#. Enable the **Show Buttons** option in the editor to display node selection overlay elements in the Scene View.
#. Look at the Scene View: each available traffic node will have a **"T"** button floating above it. Simply click the **"T"** button on the final nodes of the approaching roads to automatically add them to the selection (the button label changes to **"T-"** once selected, allowing you to remove the node just as easily).
#. Choose how the center of the circle should be defined via the **Center Type** option:
   
   * ``Current``: The current transform position of the `Roundabout` object is used as the center.
   * ``Calculate``: The system automatically calculates the geometric intersection center based on the perpendiculars and directions of the approaching roads.

#. Enable the **Calculate Radius** option to let the system automatically compute the ideal inner and outer circle radii based on the distance to the closest selected node.
#. Enable the **Merge Nodes** option. This ensures that the newly generated roundabout entry and exit paths will automatically snap and stitch onto your pre-existing traffic nodes.
#. Press the `Create` button. The system will automatically sort the nodes clockwise to prevent any path overlaps or intersection conflicts, and seamlessly link the approaching streets into the loop.

Advanced Geometry & Customization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once a roundabout is generated (especially useful for tweaking the layout in ``Custom`` mode), you can utilize advanced parameters to deform and fine-tune its geometry:

* **Position Fine-Tuning**: Adjust the ``Additive Circular Position`` and ``Additive Offset`` parameters for individual entry points to slide them along the circle's perimeter or shift their precise distance from the center.
* **Roundabout Types**:
  
  * ``SingleInnerNode``: Generates one inner node per circle segment.
  * ``DoubleInnerNodes``: Generates two inner nodes per segment, providing a smoother and more natural curvature for vehicle paths.

* **Pedestrian Ring Settings**:
  By enabling the ``Generate Outer Pedestrian Ring`` option, the tool automatically constructs a continuous sidewalk loop around the outer radius, linking existing crosswalks together into a unified pedestrian network.