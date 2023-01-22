.. _sound:

************
Sound
************

`FMOD <https://www.fmod.com/docs/2.02/studio/welcome-to-fmod-studio.html>`_ is used for all sounds in the project.

Installation
------------

#. Download `FMOD <https://assetstore.unity.com/packages/tools/audio/fmod-for-unity-161631>`_ plugin from the `Asset Store`.
#. Sign up & download `FMOD Studio <https://www.fmod.com/download>`_ software from the official site (`official guide <https://www.fmod.com/docs/2.02/unity/user-guide.html>`_).

	.. image:: /images/sound/FMODstudio-download.png
		
#. Add `FMOD` scripting define to the project.
#. Open `FMOD` settings.

	.. image:: /images/sound/FMOD-toolbar-settings.png
	
#. By default, project path: `FMOD` project path `DotsCity/FMOD/fmodproject/fmodproject.fspro`, make sure that the `FMOD` project path is set correctly.

	.. image:: /images/sound/FMOD-settings.png

How To Use
------------

#. Open `FMOD studio` installed on your computer.

	.. image:: /images/sound/FMOD-Studio-mainwindow.png
	
#. Open `Bank` bookmark.

	.. image:: /images/sound/FMOD-Studio-bankwindow.png
	
#. If you do not have an existing bank or need to set up a new one, right-click in the window and press `New Bank`.
#. In the bookmark `Events` - create or open exist folder.

	.. image:: /images/sound/FMOD-Studio-eventswindow.png
	
#. Right-click on the created folder and press `Create Event`, rename created event.

	.. image:: /images/sound/FMOD-Studio-NewEventExample.png
	
#. Right-click `Add Timeline Sheet` in the created event.

	.. image:: /images/sound/FMOD-Studio-NewTimelineExample.png
	.. image:: /images/sound/FMOD-Studio-NewTimelineExample2.png
	
#. Drag and drop the desired sound to the timeline.

	.. image:: /images/sound/FMOD-Studio-DragNDropTimelineExample.png
	
#. `Customize <https://www.fmod.com/docs/2.02/studio/authoring-events.html>`_  your sound.
#. Assign selected `FMOD event` to the `Bank`.

	.. image:: /images/sound/FMOD-Studio-AssignToBankExample.png
	
#. Build `FMOD` project.

	.. image:: /images/sound/FMOD-Studio-BuildExample.png
	
#. Create :ref:`Sound Data <soundData>` in the `Unity` project.

	.. image:: /images/sound/SoundDataCreation.png
	
#. Enter trigger name `event:/Vehicle/TestExample`.

	.. image:: /images/sound/SoundDataExample2.png
	
	.. note:: Sound ID is created automatically.
	
#. Press `Add To Service` button to add sound to the :ref:`FMOD sound service <fmodSoundService>`.	

	.. image:: /images/sound/FMOD-SoundServiceAddedExample.png
	
#. Now, we can trigger the sound from the :ref:`code <soundCodeExample>`.	

.. _soundData:

Sound Data
------------

Contains data about the `FMOD` sound.

How To Create
~~~~~~~~~~~~

In project context menu select:

	`Spirit604/City/Sound/Sound Data`

	.. image:: /images/sound/SoundDataCreation.png
	
Settings
~~~~~~~~~~~~

	.. image:: /images/sound/SoundDataExample.png
	
| **Id** : immutable ID, by which sounds are triggered in `DOTS traffic city` (ID is created automatically).
| **Name** : `event name <https://www.fmod.com/docs/2.02/studio/glossary.html#event>`_  of the sound.
| **Parameters** : event `parameters <https://www.fmod.com/docs/2.02/studio/glossary.html#parameter>`_ .

.. _fmodSoundService:

FMOD Sound Service
------------

Contains data on all :ref:`sounds <soundData>` in the `Unity` project.

	.. image:: /images/sound/FMOD-SoundServiceExample.png
	
	.. warning:: If you do not add :ref:`sound <soundData>` to the service, it cannot be activated from the code.
	
.. _soundCodeExample:

Code Examples
------------

.. _soundCodeHowToCreate:

How To Create
~~~~~~~~~~~~

EntityManager methods
""""""""""""""

..  code-block:: r

	SoundExtension.CreateSoundEntity(ref this EntityManager entityManager, int soundId, float volume = 1f, bool oneShot = false)
	// Creating a default sound entity.
	
..  code-block:: r

	SoundExtension.CreateTrackedSoundEntity(ref this EntityManager entityManager, int soundId, Entity parentEntity, float volume = 1f, bool oneShot = false)
	// Creation of a sound entity that follows a given entity.
	
..  code-block:: r

	SoundExtension.CreateChildSoundEntity(ref this EntityManager entityManager, int soundId, Entity parentEntity, float volume = 1f, bool oneShot = false)
	// Creation of a sound entity that will be a child of a given entity.
	
CommandBuffer methods
""""""""""""""

Burst compatible methods.

..  code-block:: r

	SoundExtension.CreateSoundEntity(ref this EntityCommandBuffer commandBuffer, EntityArchetype soundEntityArchetype, int soundId, float volume = 1f, bool oneShot = false)
	// Creating a default sound entity.
	
..  code-block:: r

	SoundExtension.CreateSoundEntity(ref this EntityCommandBuffer commandBuffer, EntityArchetype soundEntityArchetype, int soundId, float3 position, float volume = 1f, bool oneShot = false)
	// Create a sound entity at a specific position.
	
.. _soundArchetypeExample:

Create Archetype methods
""""""""""""""
	
..  code-block:: r

	SoundExtension.GetSoundArchetype(EntityManager entityManager, bool force = false)
	// Default sound archetype.

..  code-block:: r	

	SoundExtension.GetSoundOneShotArchetype(EntityManager entityManager)
	// OneShot sound archetype.
	
Params
""""""""""""""
            
* soundId : id of sound taken from :ref:`sound data <soundData>`.
* soundEntityArchetype : sound :ref:`archetype <soundArchetypeExample>`.
* position : initial position of the sound.
* volume : volume of the sound (0..1 range).
* oneShot : sound is played once and then destroyed.
	
How To Play
~~~~~~~~~~~~

..  code-block:: r
	
	public partial class PlayAndStopSoundExampleSystem : SystemBase
	{
		protected override void OnUpdate()
		{
			//get world sounds
			var sounds = GetComponentLookup<FMODSound>(true);
			
			Entities
			.WithBurst()
			.WithReadOnly(sounds)
			.ForEach((
				Entity entity
				in SoundHolder soundHolder) =>
			{
				bool shouldPlay = true; //some play condition
				Entity soundEntity = soundHolder.Entity //some sound entity container component 
				
                FMODSound fmodSound = sounds[soundEntity];

                if (shouldPlay)
                {
                    fmodSound.Event.start();
                }
                else
                {
                    fmodSound.Event.stop(FMOD.Studio.STOP_MODE.ALLOWFADEOUT);
                }
					
			}).Schedule();
		}
	}
	
How To Destroy
~~~~~~~~~~~~

Add `PooledEventTag` component to the `sound` entity.

How To Loop
~~~~~~~~~~~~

#. Create :ref:`Sound entity <soundCodeHowToCreate>`.
#. Add `LoopSoundData` component (assign `Duration` value).