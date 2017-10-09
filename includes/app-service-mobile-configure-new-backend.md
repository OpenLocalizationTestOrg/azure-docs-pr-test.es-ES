
1. Haga clic en hello **servicios de aplicaciones** botón, seleccione el back-end de aplicaciones móviles, seleccione **inicio rápido**y, a continuación, seleccione la plataforma de cliente (iOS, Android, Xamarin, Cordova).

    ![Azure Portal con inicio rápido de Mobile Apps resaltado][quickstart]

2. Si no hay configurada una conexión de base de datos, cree uno mediante acciones Hola siguientes:

    ![Portal de Azure con aplicaciones de Mobile Connect toodatabase][connect]

    a. Cree una nueva instancia y un nuevo servidor de SQL Database.

    ![Azure Portal con Mobile Apps: creación de una nueva base de datos y un nuevo servidor][server]

    b. Espere hasta que la conexión de datos de Hola se creó correctamente.

    ![Notificación de Azure Portal de la creación correcta de conexión de datos][notification]

    c. La conexión de datos debe haberse creado correctamente.

    ![Notificación de Azure Portal: "Ya tiene una conexión de datos"][already-connection]

3. En **2. Crear una API de tabla**, seleccione Node.js para **Lenguaje de back-end**. 
 
4. Acepte la confirmación de hello y, a continuación, seleccione **TodoItem crear tabla**.  
    Esta acción crea una nueva tabla de elementos pendientes en la base de datos. 

    >[!IMPORTANT]
    > Cambiar un tooNode.js de back-end existente, sobrescribe todo el contenido. toocreate un back-end de .NET en su lugar, vea [trabajar con servidor hello back-end de .NET SDK para aplicaciones móviles][instructions].

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
