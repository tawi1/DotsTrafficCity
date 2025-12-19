.. _trafficApi:

API
----------------

Section is progress.

Path HashMap System
~~~~~~~~~~~~

Used to find the nearest path of the road to a given position.

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

		public class TrafficSpawnExample : MonoBehaviour
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
			var pathIndex = PathHashMapSystem.GetClosestPath(spawnPosition);
			var graph = GetRoadGraph();
			var entityGraph = GetEntityGraph();

			var sourceNodeEntity = entityGraph.TryToGetSourceNode(pathIndex);
			var targetNodeEntity = entityGraph.TryToGetConnectedNode(pathIndex);

			TrafficSpawnParams trafficSpawnParams = TrafficSpawnUtils.GetSpawnParams(in graph, sourceNodeEntity, targetNodeEntity, carModel, pathIndex, spawnPosition, TrafficCustomInitType.UserCallback);
			trafficSpawnerSystem.Spawn(trafficSpawnParams, true);
		}

		private void TrafficSpawnerCallbackSystem_OnSpawn(Entity entity)
		{
			Debug.Log($"Spawned {entity.Index}");
		}
		}
		
		
Density
~~~~~~~~~~~~

Change the density of traffic at runtime.

	..  code-block:: r

		using Spirit604.Attributes;
		using Spirit604.DotsCity.Simulation.Traffic.Authoring;
		using Spirit604.Extensions;
		using System;
		using System.Linq;
		using UnityEngine;

		public class TrafficDensityChanger : MonoBehaviour
		{
			[SerializeField] private TrafficSettings trafficSettings;
			[SerializeField] private TrafficSpawnerSettingsAuthoring trafficSpawnerSettingsAuthoring;
			[SerializeField] private int count = 20;

			public void SetCountRuntime(int count)
			{
				if (count < 0)
					throw new ArgumentException("Count should be greater than zero");

				trafficSpawnerSettingsAuthoring.ChangeDensity(count);
			}

			public void SetCountEditor(int count)
			{
				if (count < 0)
					throw new ArgumentException("Count should be greater than zero");

				trafficSettings.TrafficSpawnerConfig.PreferableCount = count;
				EditorSaver.SetObjectDirty(trafficSettings.TrafficSpawnerConfig);
			}

			[Button]
			private void SetCountFromInspector()
			{
				SetCountRuntime(count);
			}

		#if UNITY_EDITOR
			private void Reset()
			{
				trafficSettings = ObjectUtils.FindObjectsOfType<TrafficSettings>().Where(a => !a.gameObject.scene.isSubScene).FirstOrDefault();
				trafficSpawnerSettingsAuthoring = ObjectUtils.FindObjectsOfType<TrafficSpawnerSettingsAuthoring>().Where(a => !a.gameObject.scene.isSubScene).FirstOrDefault();
				EditorSaver.SetObjectDirty(this);
			}
		#endif
		}