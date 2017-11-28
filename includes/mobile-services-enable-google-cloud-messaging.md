
1. <span data-ttu-id="81cb8-101">Navegue a la [consola de Google Cloud](https://console.developers.google.com/project)e inicie sesión con las credenciales de su cuenta de Google+.</span><span class="sxs-lookup"><span data-stu-id="81cb8-101">Navigate to the [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="81cb8-102">Haga clic en **Create Project** (Crear proyecto), escriba un nombre de proyecto y luego haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="81cb8-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="81cb8-103">Si se solicita, ejecute la comprobación de SMS y haga clic de nuevo en **Crear** .</span><span class="sxs-lookup"><span data-stu-id="81cb8-103">If requested, carry out the SMS Verification, and click **Create** again.</span></span>
   
    ![Creación de un proyecto](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="81cb8-105">Escriba el **nombre del nuevo proyecto** y haga clic en **Create project** (Crear proyecto).</span><span class="sxs-lookup"><span data-stu-id="81cb8-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="81cb8-106">Haga clic en el botón **Utilities and More** (Utilidades y más) y después en **Project Information** (Información del proyecto).</span><span class="sxs-lookup"><span data-stu-id="81cb8-106">Click the **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="81cb8-107">Anote el **número de proyecto**.</span><span class="sxs-lookup"><span data-stu-id="81cb8-107">Make a note of the **Project Number**.</span></span> <span data-ttu-id="81cb8-108">Lo necesitará para establecer este valor como la variable `SenderId` en la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="81cb8-108">You will need to set this value as the `SenderId` variable in the client app.</span></span>
   
    ![Utilidades y mucho más](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="81cb8-110">En el panel de proyecto, en **Mobile APIs** (API móviles), haga clic en **Google Cloud Messaging** (Servicio de mensajería en la nube de Google) y, después, en la página siguiente, haga clic en **Enable API** (Habilitar API) y acepte los términos del servicio.</span><span class="sxs-lookup"><span data-stu-id="81cb8-110">In the project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on the next page click **Enable API** and accept the terms of service.</span></span> 
   
    ![Habilitación de GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Habilitación de GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="81cb8-113">En el panel de proyecto, haga clic en **Credentials** > **Create Credential** > **API Key** (Credenciales > Crear credencial > Clave de API).</span><span class="sxs-lookup"><span data-stu-id="81cb8-113">In the project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="81cb8-114">En **Create a new key** (Crear una nueva clave), haga clic en **Server key** (Clave de servidor), escriba un nombre para la clave y haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="81cb8-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="81cb8-115">Anote el valor de **API KEY** (Clave de API).</span><span class="sxs-lookup"><span data-stu-id="81cb8-115">Make a note of the **API KEY** value.</span></span>
   
    <span data-ttu-id="81cb8-116">Usará este valor de clave de API para permitir que Azure lleve a cabo la autenticación con GCM y envíe notificaciones de inserción en nombre de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="81cb8-116">You will use this API key value to enable Azure to authenticate with GCM and send push notifications on behalf of your app.</span></span>

