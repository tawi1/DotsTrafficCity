.. _faq:

FAQ
=====

The section will be updated with the most frequently asked questions.

Known Issues
-------------------

.. _physicsFreeze:

`Unity.Physics <https://docs.unity3d.com/Packages/com.unity.physics@1.0/manual/index.html>`_ package spikes by `BuildPhysicsWorld <https://forum.unity.com/threads/in-49838-1-0-11-massive-performance-spike.1467863/>`_ & `SolveAndIntegrate <https://forum.unity.com/threads/in-49838-1-0-11-massive-performance-spike.1467863/>`_ systems on mobile devices.
~~~~~~~~~~~~

Temporary fix until official `Unity` release
^^^^^^^^^^^^^^^^^^^^^^

#. Close the `Unity` project.
#. Delete `Unity.Entities` & `Unity.Physics` packages from the `ProjectFolder/Library/PackageCache/` path.
#. Download fork packages `Unity.Entities <https://github.com/tertle/com.unity.entities>`_ & `Unity.Physics <https://github.com/tertle/com.unity.physics>`_ by `tertle <https://github.com/tertle>`_ to `ProjectFolder/Packages/` path.
#. Open the project, if it fails, close `Unity`, clear the library folder & open again.

Leak Detected : Persistent allocates 3 individual allocations.
~~~~~~~~~~~~

Editor-related memory leaks.

Common Questions
-------------------

.. _gitFix:

No 'git' executable was found
~~~~~~~~~~~~

How to fix
^^^^^^^^^^^^^^^^^^^^^^

#. Download & install `git <https://git-scm.com/download/>`_.
#. Make sure the system variable `PATH <https://www.java.com/en/download/help/path.html>`_ contains the git install path.
#. Reboot your PC.

.. _nunitFix:

error CS0006: Metadata file 'nunit.framework.dll' could not be found
~~~~~~~~~~~~

How to fix
^^^^^^^^^^^^^^^^^^^^^^

#. Restart the editor.
#. If the error is still appears, delete the `Library` folder from the project folder.