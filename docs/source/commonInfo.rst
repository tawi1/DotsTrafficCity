.. _commonInfo:

Common Info
=====

.. contents::
   :local:

.. _cullPointInfo:

Cullpoint Info
-------------------

.. _cullPointStates:

States
~~~~~~~~~~~~

The state is selected on the basis of the distance to the cull point. You can change the distances in the :ref:`cull config <cullConfig>` (:ref:`example <cullPointExamples>`).

* **Culled** : object is far away (by default, the entity is destroyed or disabled).
* **CloseToCamera** : entity enabled but with limited or modified functionality for better performance.
* **InVisionOfCamera** : entity fully enabled.

Scene Streaming
-------------------

How To Use
~~~~~~~~~~~~