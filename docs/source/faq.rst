.. _faq:

FAQ
=====

The section will be updated with the most frequently asked questions.

Common Questions
-------------------

Issues
-------------------

I changed my preset, but the changes were not applied to the scene?
~~~~~~~~~~~~

Try reopen the subscene by toggling the checkbox on & off.

.. only:: builder_html

	.. image:: /images/faq/SceneReopen.gif

Errors
-------------------

.. _gitFix:

No 'git' executable was found
~~~~~~~~~~~~

How to fix
^^^^^^^^^^^^^^^^^^^^^^

#. Download & install `git <https://git-scm.com/download/>`_.
#. Make sure the system variable `PATH <https://www.java.com/en/download/help/path.html>`_ contains the git install path.
#. Reboot your PC.

ChunkDataUtility.cs(1412,60): error CS0117
~~~~~~~~~~~~

#. Update the Unity app to 2022.3.19 or higher.

.. _nunitFix:

error CS0006: Metadata file 'nunit.framework.dll' could not be found
~~~~~~~~~~~~

How to fix
^^^^^^^^^^^^^^^^^^^^^^

#. Restart the editor.
#. If the error is still appears, delete the `Library` folder from the project folder.