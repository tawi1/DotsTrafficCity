************
Scene Handle
************

Bootstrap
============

* To start the scene automatically on the `Build` application, tick the `Auto-bootstrap` option in the `CityEntryPoint` (in the `Editor`, the scene loads by default).

	.. image:: /images/core/CityEntryPoint.png
	`CityEntryPoint.`
		
	.. image:: /images/core/CityEntryPoint2.png
	`SceneBootstrap.`
	
* If you want to start with code, assign `CityEntryPoint` to your script & use follow method, example:

	..  code-block:: r
	
		[SerializeField] private SceneBootstrapBase sceneBootstrapBase;
		
		private void StartInit()
		{
			sceneBootstrapBase.StartInitilization();
		}

Scene Unload
============

* Before you unload the main scene, you should manually unload the entity subscene.
* Assign `EntityWorldService` to your script.

	.. image:: /images/core/EntityWorldService.png
	
* You can use this sample code:


	..  code-block:: r
	
		[SerializeField] private EntityWorldService entityWorldService;
		
		private void Dispose()
		{
			entityWorldService.DisposeWorld();
		}