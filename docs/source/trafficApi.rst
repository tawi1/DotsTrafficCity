.. _trafficApi:

API
----------------

Section is progress.

Path HashMap System
~~~~~~~~~~~~

Used to find the nearest path.

How To Use
""""""""""""""

	..  code-block:: r
	
		private void Awake()
		{
			PathHashMapSystem.Register();
		}
		
		public int GetClosestPath(Vector3 position)
		{
			return PathHashMapSystem.GetClosestPath(position);
		}
		
User Spawn
~~~~~~~~~~~~

Spawn a traffic car in a custom position using user code.


	..  code-block:: r
	
		using Spirit604.DotsCity.Simulation.Level.Streaming;
		using Spirit604.DotsCity.Simulation.Road;
		using Spirit604.DotsCity.Simulation.Traffic;
		using Unity.Entities;
		using UnityEngine;

		public class SpawnExample1 : MonoBehaviour
		{
		private EntityQuery pedestrianSettingsQuery;
		private EntityQuery prefabContainerQuery;
		private EntityQuery graphQuery;
		private EntityQuery entityGraphQuery;
		private TrafficSpawnerSystem trafficSpawnerSystem;

		public PathGraphSystem.Singleton GetRoadGraph() => graphQuery.GetSingleton<PathGraphSystem.Singleton>();

		public TrafficNodeResolverSystem.RuntimePathDataRef GetEntityGraph() => entityGraphQuery.GetSingleton<TrafficNodeResolverSystem.RuntimePathDataRef>();

		private EntityManager EntityManager => World.DefaultGameObjectInjectionWorld.EntityManager;

		private void Start()
		{
			graphQuery = EntityManager.CreateEntityQuery(ComponentType.ReadOnly<PathGraphSystem.Singleton>());
			entityGraphQuery = EntityManager.CreateEntityQuery(ComponentType.ReadOnly<TrafficNodeResolverSystem.RuntimePathDataRef>());
			trafficSpawnerSystem = World.DefaultGameObjectInjectionWorld.GetOrCreateSystemManaged<TrafficSpawnerSystem>();
			PathHashMapSystem.Register();
			var spawnerCallback = TrafficSpawnerCallbackSystem.RegisterSystem();
			spawnerCallback.OnSpawn += TrafficSpawnerCallbackSystem_OnSpawn;
		}

		public void Spawn(Vector3 spawnPosition, int carModel)
		{
			var path = PathHashMapSystem.GetClosestPath(spawnPosition);
			var graph = GetRoadGraph();
			var entityGraph = GetEntityGraph();

			var sourceNodeEntity = entityGraph.TryToGetSourceNode(path);

			TrafficSpawnParams trafficSpawnParams = TrafficSpawnUtils.GetSpawnParams(in graph, EntityManager, sourceNodeEntity, carModel, TrafficCustomInitType.UserCallback);
			trafficSpawnerSystem.Spawn(trafficSpawnParams, true);
		}

		private void TrafficSpawnerCallbackSystem_OnSpawn(Entity entity)
		{
			Debug.Log($"Spawned {entity.Index}");
		}
		}