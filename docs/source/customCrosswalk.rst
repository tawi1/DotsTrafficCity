.. _customCrosswalk:

Custom Crosswalk
----------------

Allows placing a crosswalk in an arbitrary position without using :ref:`trafficNode` and :ref:`roadSegment`.

How To Use
~~~~~~~~~~

* Place pedestrian nodes where the crosswalk will be.
* Connect them with each other and other non-crosswalk nodes.

	.. image:: /images/road/pedestrianNode/customCrosswalk1.png
	
* Set ``Node type`` to ``Crosswalk node`` (the node color will change to cyan after changing the type).

	.. image:: /images/road/pedestrianNode/customCrosswalk2.png
	
* Add the ``PedestrianCrosswalkNodeAuthoring`` component to both nodes.
* Select one node of the crosswalk and select traffic paths where vehicles drive by clicking "+" in the scene view.

	.. image:: /images/road/pedestrianNode/customCrosswalk3.png
	
* Repeat this step for the second node.
* Adjust parameters in :ref:`PedestrianCrosswalkConfigAuthoring <customCrosswalkConfig>` if needed.
* Traffic will now react to pedestrians moving on that crosswalk.

.. note::
   Pedestrians evaluate approaching vehicles before crossing. If a vehicle's calculated braking distance is greater than its distance to the crosswalk (meaning the vehicle cannot stop in time due to its speed and will hit the pedestrian), the pedestrian will wait and avoid entering the crosswalk.

.. _customCrosswalkConfig:

Crosswalk Config
~~~~~~~~~~~~~~~~

The ``PedestrianCrosswalkConfigAuthoring`` component configures pedestrian behavior near crosswalks based on approaching traffic:

* **Min Speed** — Minimum vehicle speed in km/h to be considered a potential hazard. Vehicles moving slower than this speed are ignored by pedestrians.
* **Braking Rate** — Multiplier used to calculate the vehicle's safe braking distance (``braking distance = vehicle speed * braking rate``). If an approaching vehicle is closer than this calculated braking distance, the pedestrian determines the vehicle cannot stop in time and will pause/wait to avoid getting hit.
* **Distance From Crosswalk** — Distance threshold from the previous pedestrian node. Once the pedestrian walks beyond this distance, the crosswalk tracking system stops checking for traffic.
* **Idle Action** — The action state assigned to the pedestrian (e.g., waiting) when stopping for oncoming vehicles.