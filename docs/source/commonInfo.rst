.. _commonInfo:

Common Info
=====

.. contents::
   :local:

.. _cullPointInfo:

Cullpoint Info
-------------------

The cull point is the point of origin for the surrounding entities (by default, it's a child in the camera). The :ref:`state <cullPointStates>` of the surrounding entities varies depending on the distance to the culling point (:ref:`example <cullPointExamples>`).
You can change the distances in the :ref:`cull config <cullConfig>`.

.. _cullPointStates:

States
~~~~~~~~~~~~

* **Culled** : entity is far away (by default, the entity is destroyed or disabled).
* **CloseToCamera** : entity enabled but with limited or modified functionality for better performance.
* **InVisionOfCamera** : entity fully enabled.

Scene Streaming
-------------------

How To Use
~~~~~~~~~~~~