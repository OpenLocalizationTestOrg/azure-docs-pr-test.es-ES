
1. <span data-ttu-id="b6dbb-101">Hola vista soluciones (o **el Explorador de soluciones** en Visual Studio), contextual hello **componentes** carpeta, haga clic en **obtener más componentes de...** , busque hello **el cliente de mensajería de nube de Google** componentes y agregue el proyecto de toohello.</span><span class="sxs-lookup"><span data-stu-id="b6dbb-101">In hello Solution view (or **Solution Explorer** in Visual Studio), right-click hello **Components** folder, click  **Get More Components...**, search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>
2. <span data-ttu-id="b6dbb-102">Abrir archivo de proyecto de hello ToDoActivity.cs y agregue Hola siguiente mediante la clase toohello de instrucción:</span><span class="sxs-lookup"><span data-stu-id="b6dbb-102">Open hello ToDoActivity.cs project file and add hello following using statement toohello class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="b6dbb-103">Hola **ToDoActivity** clase, agregue Hola siguiendo el nuevo código:</span><span class="sxs-lookup"><span data-stu-id="b6dbb-103">In hello **ToDoActivity** class, add hello following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return hello current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return hello Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="b6dbb-104">Esto le permite la instancia de cliente móvil tooaccess Hola de proceso del servicio de controlador de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6dbb-104">This enables you tooaccess hello mobile client instance from hello push handler service process.</span></span>
4. <span data-ttu-id="b6dbb-105">Agregar Hola después código toohello **OnCreate** método después de hello **MobileServiceClient** se crea:</span><span class="sxs-lookup"><span data-stu-id="b6dbb-105">Add hello following code toohello **OnCreate** method, after hello **MobileServiceClient** is created:</span></span>
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="b6dbb-106">Ahora la **ToDoActivity** estará preparada para agregar notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="b6dbb-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

