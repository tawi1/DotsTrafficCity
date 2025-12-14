.. _pedestrianApi:

API
----------------

Node Hash Map System
~~~~~~~~~~~~

Used to find the nearest entity node.

How To Use
""""""""""""""

	..  code-block:: r
	
		private void Awake()
		{
			NodeHashMapSystem.Register();
		}
		
		public Entity GetClosestNode(Vector3 position, out Vector3 nodePosition)
		{
			return NodeHashMapSystem.GetClosestNode(position, out nodePosition);
		}
		
Custom Spawn
~~~~~~~~~~~~

Spawn a pedestrian in a custom position using user code.


	..  code-block:: r
	
		private EntityQuery pedestrianSettingsQuery;
		private EntityQuery prefabContainerQuery;

		private EntityManager EntityManager => World.DefaultGameObjectInjectionWorld.EntityManager;

		private void Start()
		{
			pedestrianSettingsQuery = EntityManager.CreateEntityQuery(ComponentType.ReadOnly<PedestrianSettingsReference>());
			prefabContainerQuery = EntityManager.CreateEntityQuery(ComponentType.ReadOnly<PedestrianEntityPrefabContainer>());
			NodeHashMapSystem.Register();
		}

		public void SpawnExampleMethod(Vector3 spawnPosition, Quaternion spawnRotation, Vector3 destination)
		{
			var commandBuffer = new EntityCommandBuffer(Unity.Collections.Allocator.Temp);
			uint seed = MathUtilMethods.GetRandomSeed();

			var pedestrianSettings = pedestrianSettingsQuery.GetSingleton<PedestrianSettingsReference>().Config;
			var prefabContainer = prefabContainerQuery.GetSingletonBuffer<PedestrianEntityPrefabContainer>();

			var rnd = new Unity.Mathematics.Random(seed);

			var entityPrefab = prefabContainer.GetRandomPrefab(rnd, out var skinIndex);

			Entity destinationNode = NodeHashMapSystem.GetClosestNode(destination, out destination);

			Spawn(
				ref commandBuffer,
				in pedestrianSettings,
				seed,
				entityPrefab,
				skinIndex,
				spawnPosition,
				spawnRotation,
				destinationNode,
				destination);

			commandBuffer.Playback(EntityManager);
			commandBuffer.Dispose();
		}

		private static Entity Spawn(
				 ref EntityCommandBuffer commandBuffer,
				 in BlobAssetReference<PedestrianSettings> pedestrianSettings,
				 uint seed,
				 Entity entityPrefab,
				 int skinIndex,
				 Vector3 spawnPosition,
				 Quaternion spawnRotation,
				 Entity destinationEntity,
				 float3 destination)
		{
			var pedestrianEntity = commandBuffer.Instantiate(entityPrefab);

			var destinationComponent = new DestinationComponent()
			{
				Value = destination,
				PreviousDestination = destination,
				DestinationNode = destinationEntity,
				PreviuosDestinationNode = destinationEntity,
			};

			var spawnParams = new SpawnParams()
			{
				DestinationComponent = destinationComponent,
				RigidTransform = new RigidTransform(spawnRotation, spawnPosition),
				Seed = seed,
				SkinIndex = skinIndex
			};

			PedestrianInitUtils.Initialize(ref commandBuffer, pedestrianEntity, in spawnParams, in pedestrianSettings);

			return pedestrianEntity;
		}