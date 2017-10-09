
1. <span data-ttu-id="f7771-101">Navegue toohello [consola en la nube de Google](https://console.developers.google.com/project), inicie sesión con sus credenciales de cuenta de Google.</span><span class="sxs-lookup"><span data-stu-id="f7771-101">Navigate toohello [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="f7771-102">Haga clic en **Create Project** (Crear proyecto), escriba un nombre de proyecto y luego haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="f7771-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="f7771-103">Si se solicita, realizar Hola verificación por SMS y haga clic en **crear** nuevo.</span><span class="sxs-lookup"><span data-stu-id="f7771-103">If requested, carry out hello SMS Verification, and click **Create** again.</span></span>
   
    ![Creación de un proyecto](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="f7771-105">Escriba el **nombre del nuevo proyecto** y haga clic en **Create project** (Crear proyecto).</span><span class="sxs-lookup"><span data-stu-id="f7771-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="f7771-106">Haga clic en hello **utilidades y mucho más** botón y, a continuación, haga clic en **información del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="f7771-106">Click hello **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="f7771-107">Tome nota de hello **proyecto número**.</span><span class="sxs-lookup"><span data-stu-id="f7771-107">Make a note of hello **Project Number**.</span></span> <span data-ttu-id="f7771-108">Necesitará tooset este valor como hello `SenderId` variable en la aplicación de cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="f7771-108">You will need tooset this value as hello `SenderId` variable in hello client app.</span></span>
   
    ![Utilidades y mucho más](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="f7771-110">En hello proyecto del panel, en **las API de Mobile**, haga clic en **Google Cloud Messaging**, haga clic en la página siguiente de hello **habilitar la API** y acepte los términos de hello del servicio.</span><span class="sxs-lookup"><span data-stu-id="f7771-110">In hello project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on hello next page click **Enable API** and accept hello terms of service.</span></span> 
   
    ![Habilitación de GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Habilitación de GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="f7771-113">En el panel de proyecto de hello, haga clic en **credenciales** > **Create Credential** > **clave de API**.</span><span class="sxs-lookup"><span data-stu-id="f7771-113">In hello project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="f7771-114">En **Create a new key** (Crear una nueva clave), haga clic en **Server key** (Clave de servidor), escriba un nombre para la clave y haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="f7771-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="f7771-115">Tome nota de hello **clave de API** valor.</span><span class="sxs-lookup"><span data-stu-id="f7771-115">Make a note of hello **API KEY** value.</span></span>
   
    <span data-ttu-id="f7771-116">Utilizará este tooenable de valor de clave de API tooauthenticate Azure con GCM y enviar notificaciones de inserción en el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f7771-116">You will use this API key value tooenable Azure tooauthenticate with GCM and send push notifications on behalf of your app.</span></span>

