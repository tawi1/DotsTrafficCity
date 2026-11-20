.. _astar:

Aron's A* Pathfinding project
=============================

A* solution can be used for `Traffic` & `Pedestrian` navigation as an alternative to the built-in A* solution.

How To Use
----------

#. Buy & download, import the following asset plugin:

	`A* Pathfinding Project Pro <https://assetstore.unity.com/packages/tools/behavior-ai/a-pathfinding-project-pro-87744>`_

Getting Started
---------------

#. Create a new gameobject & add the `AstarPath` component.
#. Add 2 `Point Graphs` to the `AstarPath` component (if you are going to navigate for either traffic or pedestrians only, create just 1 graph).

	.. image:: /images/integration/astar2.png
	
#. Create a new gameobject & add `AstarPedestrianPathService` for pedestrians & `AstarTrafficPathService` for traffic.

	.. image:: /images/integration/astar1.png
	
#. The next step is to create a graph for a runtime or static scene.
#. To retrieve traffic or pedestrians, read the :ref:`Traffic entity selection <trafficEntitySelection>` or :ref:`Pedestrian entity selection <pedestrianEntitySelection>`.
#. To get entity nodes on the scenes, read the `TrafficNodeSelector` & `PedestrianNodeSelector` examples.
#. After you have added service & graph, use this code:

	..  code-block:: csharp
	
		public class StartPathServiceExample : MonoBehaviour
		{
		// Reference to pedestrian or traffic path service
		[SerializeField] private EntityCustomPathServiceBase pathService;
		
		public void StartPath(Entity entity, Entity endNode)
		{
			pathService.SetFollowPath(entity, endNode);
		}
		}

Static Graph
------------

Used for static scenes created in the `Editor`.

#. Add components `AstarPedestrianStaticGraph` & `AstarTrafficStaticGraph` & assign these references to corresponding services, making sure local graph indexes are different for both graphs & matched with `AstarPath` (e.g. 0 index for pedestrian & 1 index for traffic).

Runtime Graph
-------------

Used for tile-based run-time generated scenes with `RuntimeRoadManager`.

#. Create a new gameobject & add a `RuntimeRoadManager` component & you can use :ref:`Runtime Road <runtimeRoad>` for demo.
#. Add components `AstarPedestrianRuntimeGraphModifier` & `AstarTrafficRuntimeGraphModifier` & assign these references to corresponding services, making sure local graph indexes are different for both graphs & matched with `AstarPath` (e.g. 0 index for pedestrian & 1 index for traffic).
#. Make sure that you have assigned `RuntimeRoadManager` to these graphs.
#. For a quick start follow these steps *[optional]*:
	#. Open a `RuntimeTileRoad Demo` scene.
	#. Disable built-in path services & add created path services to corresponding path selectors.
	#. Example for pedestrian:
	
		.. image:: /images/integration/astar3.png
		
	#. Do the same for traffic.

Runtime Graph (Custom)
----------------------

Used for spline-based / custom run-time generated scenes with `RuntimeRoadManagerCustom`.

#. Create a new gameobject & add a `RuntimeRoadManagerCustom` component.
#. Add components `AstarPedestrianRuntimeCustomGraphModifier` & `AstarTrafficRuntimeCustomGraphModifier` & assign these references to corresponding services, making sure local graph indexes are different for both graphs & matched with `AstarPath` (e.g. 0 index for pedestrian & 1 index for traffic).
#. Make sure that you have assigned `RuntimeRoadManagerCustom` to these modifiers.

Performance Optimization (Authoring)
------------------------------------

By default, `allowStructuralChanges` is enabled on `AstarPedestrianPathService` & `AstarTrafficPathService`. This mode adds & removes pathfinding components at runtime and is suitable for infrequent pathfinding on a small number of entities.

If you plan to search paths frequently or for a large number of entities, avoid runtime structural changes by baking the required components directly onto your entity prefabs:

#. Disable `allowStructuralChanges` on `AstarPedestrianPathService` and/or `AstarTrafficPathService`.
#. Add the corresponding authoring components to your entity prefabs:

	* **Pedestrians:** `PedestrianPathfindingAuthoring` & `AstarAgentAuthoring`
	* **Traffic:** `TrafficPathfindingAuthoring` & `AstarAgentAuthoring`

.. note::
	When `allowStructuralChanges` is disabled, all entities requesting a path must have these authoring components on their prefabs; otherwise, the service will log an error & fall back to structural changes.