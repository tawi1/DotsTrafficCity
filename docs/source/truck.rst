.. _truck:

Truck with Trailer
==================

This guide explains how to set up and configure a truck with a trailer for Mono and DOTS workflows.

How to Create
-------------

1. Drag and drop your truck with trailer FBX prefab into the scene.
2. Unpack the prefab.
3. Add the ``TruckPrefabHelper`` component to the root GameObject.
4. Assign the truck and trailer references in ``TruckPrefabHelper``.
5. Create a new child GameObject under the trailer to serve as an anchor, then assign it to the ``TruckPrefabHelper`` component.
6. Adjust the position of the anchor where the truck and trailer connect.
7. Adjust **Split Entity Length** in ``TruckPrefabHelper`` to subdivide the trailer into multiple sub-entities if it is too long.
8. Save the resulting GameObject as a new prefab (refer to the ``Truck2`` prefab for an example).
9. Open the :ref:`Car Prefab Creator <carPrefabCreator>` tool.
10. Clear the **Prefabs** field, then drag and drop the created prefab into it.
11. Click **Scan**.
12. In the **Save** tab, configure the target architecture:

    * **For Mono:**

      * **Entity type:** ``Hybrid entity mono physics``
      * **Controller type:** ``Arcade truck with trailer``

    * **For DOTS:**

      * **Entity type:** ``Pure entity custom physics``
      * **Controller type:** ``Truck with trailer``

13. Click **Create**.

Suspension Setup (DOTS)
-----------------------

To adjust the suspension length, stiffness, damping, or other physical parameters for a DOTS truck and trailer:

1. Open the ``Custom Vehicle test scene``.
2. Drag and drop the created DOTS truck prefab (which includes the trailer as a child object) into the active SubScene.
3. Remove the ``TrafficCarEntityAuthoring`` component from the child trailer instance in the scene (do NOT remove it from the source prefab asset).
4. Tweak the suspension parameters in the inspector while in Play mode to find the desired feel.