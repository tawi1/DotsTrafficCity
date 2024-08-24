.. _sound:

************
Sound
************

Built-in
============

By default is used for all sounds in the project (if :ref:`FMOD <fmod>` is not installed).

How To Use
------------

#. Create :ref:`Sound Data <soundData>` in the `Unity` project.

	.. image:: /images/sound/SoundDataCreation.png
	
#. Assign your desired `AudioClip <https://docs.unity3d.com/ScriptReference/AudioClip.html>`_.

	.. image:: /images/sound/SoundDataBuiltin.png
	
	.. note:: Sound ID is created automatically.
	
#. Press `Add To Container` button to add sound to the :ref:`Sound container <soundContainer>`.	

	.. image:: /images/sound/FMOD-SoundServiceAddedExample.png
	
#. Now, we can trigger the sound using the code examples below.	

Code Examples
------------

MonoBehaviour
~~~~~~~~~~~~

..  code-block:: r

    public class ExampleSoundBehaviour : MonoBehaviour
    {
        [SerializeField] private SoundData exampleSoundData;
		
		private void PlaySound()
		{
			SoundManager.Instance.PlayOneShot(exampleSoundData, transform.position);
		}
	}
	
Jobs
~~~~~~~~~~~~

If you want to create sound in Job, :ref:`read here <soundCodeExample>`.

.. _fmodSound:

FMOD
============

`FMOD <https://www.fmod.com/docs/2.02/studio/welcome-to-fmod-studio.html>`_ is used for all sounds in the project (if `FMOD` installed).

Installation
------------

#. Download the `FMOD <https://assetstore.unity.com/packages/tools/audio/fmod-for-unity-161631>`_ plugin from the `Asset Store`.
#. Add the `FMOD` scripting define to the project.
#. Select the project `FMOD` path in the window that appears on the `Linking` tab (by default `DotsCity/FMOD/fmodproject/fmodproject.fspro`).

	.. image:: /images/sound/FMOD-setup.png
	
#. `Sign up <https://www.fmod.com/profile/register>`_ & download the `FMOD Studio <https://www.fmod.com/download>`_ software from the official site (`official guide <https://www.fmod.com/docs/2.02/unity/user-guide.html>`_) **[optional step, required if you want to add & edit sounds]**.

	.. image:: /images/sound/FMODstudio-download.png

#. Open `FMOD` settings.

	.. image:: /images/sound/FMOD-toolbar-settings.png
	
#. By default, project path: `FMOD` project path `DotsCity/FMOD/fmodproject/fmodproject.fspro`, make sure that the `FMOD` project path is set correctly.

	.. image:: /images/sound/FMOD-settings.png

How To Use
------------

#. Open `FMOD Studio` installed on your computer.

	.. image:: /images/sound/FMOD-Studio-mainwindow.png
	
#. Open `Bank` bookmark.

	.. image:: /images/sound/FMOD-Studio-bankwindow.png
	
#. If you do not have an existing bank or need to create a new one, right-click in the window and press `New Bank`.
#. In the bookmark `Events` - Create or open exist folder.

	.. image:: /images/sound/FMOD-Studio-eventswindow.png
	
#. Right-click on the created folder and press `Create Event`, rename created event.

	.. image:: /images/sound/FMOD-Studio-NewEventExample.png
	
#. Right-click on `Add Timeline Sheet` in the created event.

	.. image:: /images/sound/FMOD-Studio-NewTimelineExample.png
	.. image:: /images/sound/FMOD-Studio-NewTimelineExample2.png
	
#. Drag and drop the desired sound into the timeline.

	.. image:: /images/sound/FMOD-Studio-DragNDropTimelineExample.png
	
#. `Customize <https://www.fmod.com/docs/2.02/studio/authoring-events.html>`_  your sound.
#. Assign the selected `FMOD event` to the `Bank`.

	.. image:: /images/sound/FMOD-Studio-AssignToBankExample.png
	
#. Build `FMOD` project.

	.. image:: /images/sound/FMOD-Studio-BuildExample.png
	
#. Create :ref:`Sound Data <soundData>` in the `Unity` project.

	.. image:: /images/sound/SoundDataCreation.png
	
#. Enter trigger name `event:/Vehicle/TestExample`.

	.. image:: /images/sound/SoundDataExample2.png
	
	.. note:: Sound ID is created automatically.
	
#. Press `Add To Container` button to add sound to the :ref:`Sound container <soundContainer>`.	

	.. image:: /images/sound/FMOD-SoundServiceAddedExample.png
	
#. Now, we can trigger the sound from the :ref:`code <soundCodeExample>`.	

Data
============

.. _soundData:

Sound Data
------------

Contains data about the sound.

How To Create
~~~~~~~~~~~~

Select from the project context menu:

	`Spirit604/City/Sound/Sound Data`

	.. image:: /images/sound/SoundDataCreation.png
	
Settings
~~~~~~~~~~~~

Built-in
""""""""""""""

	.. image:: /images/sound/SoundDataBuiltin.png
	
| **Id** : immutable ID, by which sounds are triggered in `DOTS traffic city` (ID is created automatically).
| **Loop** : on/off sound looping.
| **Clip volume** : volume of the audio clip.
| **Random sound** : on/off random sound.
| **Audio clip** : reference to `AudioClip <https://docs.unity3d.com/ScriptReference/AudioClip.html>`_ .

FMOD
""""""""""""""

	.. image:: /images/sound/SoundDataExample.png
	
| **Id** : immutable ID, by which sounds are triggered in `DOTS traffic city` (ID is created automatically).
| **Name** : `event name <https://www.fmod.com/docs/2.02/studio/glossary.html#event>`_  of the sound.
| **Parameters** : event `parameters <https://www.fmod.com/docs/2.02/studio/glossary.html#parameter>`_ .

.. _soundContainer:

Sound Data Container
------------

Contains data on all :ref:`sounds <soundData>` in the `Unity` project.

	.. image:: /images/sound/FMOD-SoundServiceExample.png
	
	.. warning:: If you do not add :ref:`sound <soundData>` to the service, it cannot be activated from the code.
	
.. _soundCodeExample:

Code Examples
============

.. _soundType:

Sound Types
------------

* **Default** : default sound entity.
* **One Shot** : entity played once & destroyed afterwards.
* **Tracking** : entity tracks target entity.
* **Tracking Vehicle** : entity tracks target vehicle entity.
* **Tracking And Loop** : entity tracks target entity & loop playback.

.. _soundCodeHowToCreate:

How To Create
------------

EntityManager methods
~~~~~~~~~~~~

..  code-block:: r

	SoundExtension.CreateSoundEntity(ref this EntityManager entityManager, int soundId, float volume = 1f)
	// Creating a default sound entity.
	
..  code-block:: r

	SoundExtension.CreateTrackedSoundEntity(ref this EntityManager entityManager, int soundId, Entity parentEntity, float volume = 1f)
	// Creation of a sound entity that follows a given entity.
	
..  code-block:: r

	SoundExtension.CreateChildSoundEntity(ref this EntityManager entityManager, int soundId, Entity parentEntity, float volume = 1f)
	// Creation of a sound entity that will be a child of a given entity.
	
CommandBuffer methods
~~~~~~~~~~~~

Burst compatible methods.

..  code-block:: r

	SoundExtension.CreateSoundEntity(ref this EntityCommandBuffer commandBuffer, Entity soundPrefabEntity, int soundId, float volume = 1f)
	// Creating a default sound entity.
	
..  code-block:: r

	SoundExtension.CreateSoundEntity(ref this EntityCommandBuffer commandBuffer, Entity soundPrefabEntity, int soundId, float3 position, float volume = 1f)
	// Create a sound entity at a specific position.
	
.. _soundPrefabExample:

Create prefab query method
~~~~~~~~~~~~
	
..  code-block:: r

	SoundExtension.GetSoundQuery(EntityManager entityManager, SoundType soundType)
	// Get `EntityQuery` with the selected `Sound type`.
	
Create sound example
~~~~~~~~~~~~

..  code-block:: r

    public partial class ExampleSoundSystem : SystemBase
    {
        private EntityQuery soundPrefabQuery;

        protected override void OnCreate()
        {
            soundPrefabQuery = SoundExtension.GetSoundQuery(EntityManager, SoundType.Default);
        }
		
		protected override void OnUpdate()
		{
			var commandBuffer = ...
			var soundPrefabEntity = soundPrefabQuery.GetSingletonEntity();
			
			// Pass 'commandBuffer' & 'soundPrefabEntity' into the IJobEntity or Entities.ForEach
			// commandBuffer.CreateSoundEntity(soundPrefabEntity, soundId, position);
			// 'soundId' can be taken from 'SoundData'
		}
	
Params
~~~~~~~~~~~~
            
* soundId : id of sound taken from :ref:`sound data <soundData>`.
* soundPrefabEntity : sound :ref:`prefab entity <soundPrefabExample>` taken from :ref:`EntityQuery <soundPrefabExample>`.
* position : initial position of the sound.
* volume : volume of the sound (0..1 range).
	
How To Play
------------

..  code-block:: r
	
	public partial class PlayAndStopSoundExampleSystem : SystemBase
	{
	protected override void OnUpdate()
	{
	
	// Get world sounds
	var sounds = GetComponentLookup<SoundEventComponent>(false);
	
	Entities
	.WithBurst()
	.ForEach((
		Entity entity
		in SoundHolder soundHolder) =>
	{
		// Some play condition
		bool shouldPlay = true; 
		
		// Some sound entity container component 
		Entity soundEntity = soundHolder.Entity 
		
		SoundEventComponent soundEvent = sounds[soundEntity];
		
		if (shouldPlay)
		{
			soundEvent.SetEvent(SoundEventType.Play);
		}
		else
		{
			soundEvent.SetEvent(SoundEventType.StopFadeout);
		}
		
		sounds[soundEntity] = soundEvent;
			
	}).Schedule();
	}
	}
	
How To Destroy
------------

Enable the `PooledEventTag` component in the `sound` entity.

How To Loop
------------

#. Create a :ref:`Sound entity <soundCodeHowToCreate>`.
#. Add a `LoopSoundData` component (assign a `Duration` value).