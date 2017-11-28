
1. <span data-ttu-id="de656-101">En la vista Solución (o **Explorador de soluciones** en Visual Studio), haga clic en la carpeta **Componentes**, en **Obtener más componentes...**, busque el componente **Google Cloud Messaging Client** y agréguelo al proyecto.</span><span class="sxs-lookup"><span data-stu-id="de656-101">In the Solution view (or **Solution Explorer** in Visual Studio), right-click the **Components** folder, click  **Get More Components...**, search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>
2. <span data-ttu-id="de656-102">Abra el archivo de proyecto ToDoActivity.cs y agregue la siguiente instrucción using a la clase:</span><span class="sxs-lookup"><span data-stu-id="de656-102">Open the ToDoActivity.cs project file and add the following using statement to the class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="de656-103">En la clase **ToDoActivity** , agregue el siguiente código nuevo:</span><span class="sxs-lookup"><span data-stu-id="de656-103">In the **ToDoActivity** class, add the following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return the current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return the Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="de656-104">Esto le permite tener acceso a la instancia de cliente de Servicios móviles desde el proceso del servicio del controlador de inserciones.</span><span class="sxs-lookup"><span data-stu-id="de656-104">This enables you to access the mobile client instance from the push handler service process.</span></span>
4. <span data-ttu-id="de656-105">Agregue el código siguiente al método **OnCreate** después de crear **MobileServiceClient**:</span><span class="sxs-lookup"><span data-stu-id="de656-105">Add the following code to the **OnCreate** method, after the **MobileServiceClient** is created:</span></span>
   
       // Set the current instance of TodoActivity.
       instance = this;
   
       // Make sure the GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register the app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="de656-106">Ahora la **ToDoActivity** estará preparada para agregar notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="de656-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

