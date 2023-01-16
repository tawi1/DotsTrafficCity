.. _trafficNodePathCreator:

TrafficNode Path Creator
=====

`TrafficNode Path Creator` is a tool for quickly creating :ref:`paths <path>` between :ref:`traffic nodes <trafficNode>`.

How To Use
------------

#. Open tool in the Unity toolbar:

	`Spirit604/CityEditor/Window/TrafficNode Path Creator`
	
	.. image:: /images/road/trafficNode/trafficNodePathCreator/OpenExample.png
	
#. Select the :ref:`source traffic node <trafficNode>` and :ref:`target traffic node <trafficNode>` on the scene (:ref:`example <trafficNodePathCreatorExamples>`).
#. Customize new :ref:`path settings <trafficNodePathCreatorPathSettings>`.
#. Select desired `Connection Mode Type` (:ref:`connection settings <trafficNodePathCreatorConnectionSettings>`).
#. Customize `source` & `target` :ref:`connection side <trafficNodeConnectionInfo>`, so that the path is positioned correctly (:ref:`example <trafficNodePathCreatorExamples>`) (:ref:`connection settings <trafficNodePathCreatorConnectionSettings>`).
#. Click `Create` button.
#. :ref:`Customize <pathCustomize>` created :ref:`paths <path>`.

Settings
------------

Node Settings
~~~~~~~~~~~~ 

	.. image:: /images/road/trafficNode/trafficNodePathCreator/NodeSettings.png
	
| **Source Traffic Node** : source :ref:`traffic node <trafficNode>`.
| **Target Traffic Node** : target :ref:`traffic node <trafficNode>`.

.. _trafficNodePathCreatorPathSettings:

Path Settings
~~~~~~~~~~~~ 

	.. image:: /images/road/trafficNode/trafficNodePathCreator/PathSettings.png
	
| :ref:`Path settings <pathSettings>`.
| **Select after create** : the path will be selected in the inspector after creation.
	
Visual Settings
~~~~~~~~~~~~ 

	.. image:: /images/road/trafficNode/trafficNodePathCreator/VisualSettings.png
	
**Show preview dotted line:** on/off connection line on the scene.
	* **Show path direction** : on/off arrows of the connection line.
	* **Arrow spacing** : arrow spacing.
| **Show forbidden path** : on/off display of forbidden connection line.
| **Show overriden path** : on/off display of overriden connection line (if disabled preview color will be taken).
| **Font color** : font color of traffic node index gizmos.
| **Preview connection color** : preview connection line color.
| **Forbidden connection color** : forbidden connection line color.
| **Overriden connection color** : overriden connection line color.

.. _trafficNodePathCreatorConnectionSettings:

Connection Settings
~~~~~~~~~~~~ 

	.. image:: /images/road/trafficNode/trafficNodePathCreator/ConnectionSettings.png
	
**Connection mode type:** 
	* **Single connect** : only 1 path is created.
	* **Direction connect** : paths of all lanes are created.
**Connection type:** 
	* **Create only if not exist** : path will be created only if the path has not been created before.
	* **Allow override** : path will be overwritten if created earlier.
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

	.. image:: /images/road/trafficNode/trafficNodePathCreator/Buttons.png
	
| **Swap nodes** : swap source and target node.
| **Create** : create available paths.

.. _trafficNodePathCreatorExamples:

Examples
------------ 

	.. image:: /images/road/trafficNode/trafficNodePathCreator/Example1.png
	`Connection available example (allow override path enabled, show overriden path disabled).`
	
	.. image:: /images/road/trafficNode/trafficNodePathCreator/Example2.png	
	`Connection available example (allow override path enabled, show overriden path enabled).`
	
	.. image:: /images/road/trafficNode/trafficNodePathCreator/Example3.png
	`Connection forbidden example.`