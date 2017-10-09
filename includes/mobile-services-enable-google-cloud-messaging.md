
1. Navegue toohello [consola en la nube de Google](https://console.developers.google.com/project), inicie sesión con sus credenciales de cuenta de Google. 
2. Haga clic en **Create Project** (Crear proyecto), escriba un nombre de proyecto y luego haga clic en **Create** (Crear). Si se solicita, realizar Hola verificación por SMS y haga clic en **crear** nuevo.
   
    ![Creación de un proyecto](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     Escriba el **nombre del nuevo proyecto** y haga clic en **Create project** (Crear proyecto).
3. Haga clic en hello **utilidades y mucho más** botón y, a continuación, haga clic en **información del proyecto**. Tome nota de hello **proyecto número**. Necesitará tooset este valor como hello `SenderId` variable en la aplicación de cliente de hello.
   
    ![Utilidades y mucho más](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. En hello proyecto del panel, en **las API de Mobile**, haga clic en **Google Cloud Messaging**, haga clic en la página siguiente de hello **habilitar la API** y acepte los términos de hello del servicio. 
   
    ![Habilitación de GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Habilitación de GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. En el panel de proyecto de hello, haga clic en **credenciales** > **Create Credential** > **clave de API**. 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. En **Create a new key** (Crear una nueva clave), haga clic en **Server key** (Clave de servidor), escriba un nombre para la clave y haga clic en **Create** (Crear).
7. Tome nota de hello **clave de API** valor.
   
    Utilizará este tooenable de valor de clave de API tooauthenticate Azure con GCM y enviar notificaciones de inserción en el nombre de la aplicación.

