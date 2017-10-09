
1. Hola vista soluciones (o **el Explorador de soluciones** en Visual Studio), contextual hello **componentes** carpeta, haga clic en **obtener más componentes de...** , busque hello **el cliente de mensajería de nube de Google** componentes y agregue el proyecto de toohello.
2. Abrir archivo de proyecto de hello ToDoActivity.cs y agregue Hola siguiente mediante la clase toohello de instrucción:
   
        using Gcm.Client;
3. Hola **ToDoActivity** clase, agregue Hola siguiendo el nuevo código: 
   
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
   
    Esto le permite la instancia de cliente móvil tooaccess Hola de proceso del servicio de controlador de inserción de Hola.
4. Agregar Hola después código toohello **OnCreate** método después de hello **MobileServiceClient** se crea:
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

Ahora la **ToDoActivity** estará preparada para agregar notificaciones de inserción.

