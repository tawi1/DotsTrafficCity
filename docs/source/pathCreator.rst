.. _pathCreator:

Path Creator
=====

`Path Creator` is a tool for quickly creating :ref:`paths <path>` between :ref:`traffic nodes <trafficNode>`.

How To Use
------------

#. Open the tool from the `Unity` toolbar:

	`Spirit604/CityEditor/Window/Path Creator`
	
	.. image:: /images/road/trafficNode/pathCreator/OpenExample.png
	
#. Select the :ref:`source traffic node <trafficNode>` and :ref:`target traffic node <trafficNode>` in the scene (:ref:`example <pathCreatorExamples>`).
#. Customize new :ref:`path settings <pathCreatorPathSettings>`.
#. Select the desired `Connection Mode Type` (:ref:`connection settings <pathCreatorConnectionSettings>`).
#. Customize `Source` & `Target` :ref:`connection side <trafficNodeConnectionInfo>`, so that the path is positioned correctly (:ref:`example <pathCreatorExamples>`) (:ref:`connection settings <pathCreatorConnectionSettings>`).
#. Click the `Create` button.
#. :ref:`Customize <pathCustomize>` the created :ref:`paths <path>`.

Settings
------------

Node Settings
~~~~~~~~~~~~ 

	.. image:: /images/road/trafficNode/pathCreator/NodeSettings.png
	
| **Source Traffic Node** : source :ref:`traffic node <trafficNode>`.
| **Target Traffic Node** : target :ref:`traffic node <trafficNode>`.

.. _pathCreatorPathSettings:

Path Settings
~~~~~~~~~~~~ 

	.. image:: /images/road/trafficNode/pathCreator/PathSettings.png
	
| :ref:`Path settings <pathSettings>`.
| **Select after create** : the path will be selected in the inspector after creation.
	
Visual Settings
~~~~~~~~~~~~ 

	.. image:: /images/road/trafficNode/pathCreator/VisualSettings.png
	
**Show preview dotted line:** on/off connection line in the scene.
	* **Show path direction** : on/off arrows of the connection line.
	* **Arrow spacing** : arrow spacing.
	
| **Show forbidden path** : on/off display of forbidden connection line.
| **Show overriden path** : on/off display of overriden connection line (if disabled preview color will be taken).
| **Font color** : font color of traffic node index gizmos.
| **Preview connection color** : preview connection line color.
| **Forbidden connection color** : forbidden connection line color.
| **Overriden connection color** : overriden connection line color.

.. _pathCreatorConnectionSettings:

Connection Settings
~~~~~~~~~~~~ 

	.. image:: /images/road/trafficNode/pathCreator/ConnectionSettings.png
	
**Connection mode type:** 
	* **Single connect** : only 1 :ref:`path <path>` is created.
	* **Direction connect** : :ref:`paths <path>` of all lanes are created.
	
**Connection type:** 
	* **Create only if not exist** : :ref:`path <path>` will be created only if the :ref:`path <path>` has not been created before.
	* **Allow override** : :ref:`path <path>` will be overwritten if created earlier.
	
| **Auto detect side** : when selecting nodes, the selected :ref:`sides <trafficNodeConnectionInfo>` will be automatically detected
| **Connect same side** : target :ref:`side <trafficNodeConnectionInfo>` will be the same as source :ref:`side <trafficNodeConnectionInfo>`.

**Source connection type** : 
	* **Default side** : selected :ref:`right side <trafficNodeConnectionInfo>` point in the source :ref:`traffic node <trafficNode>`.
	* **External side** : selected :ref:`left side <trafficNodeConnectionInfo>` point in the source :ref:`traffic node <trafficNode>`.
	
**Target connection type** : 
	* **Default side** : selected :ref:`right side <trafficNodeConnectionInfo>` point in the target :ref:`traffic node <trafficNode>`.
	* **External side** : selected :ref:`left side <trafficNodeConnectionInfo>` point in the target :ref:`traffic node <trafficNode>`.
	
**Single connect setting** :
	* **Connect same index** : target index will be the same as source index.
	* **Source lane index** : source lane index.
	* **Target lane index** : connected lane index.
	
Buttons
~~~~~~~~~~~~ 

	.. image:: /images/road/trafficNode/pathCreator/Buttons.png
	
| **Swap nodes** : swap source and target node.
| **Create** : create available paths.

.. _pathCreatorExamples:

Examples
------------ 

	.. image:: /images/road/trafficNode/pathCreator/Example1.png
	`Connection available example (allow override path enabled, show overriden path disabled).`
	
	.. image:: /images/road/trafficNode/pathCreator/Example2.png	
	`Connection available example (allow override path enabled, show overriden path enabled).`
	
	.. image:: /images/road/trafficNode/pathCreator/Example3.png
	`Connection forbidden example.`