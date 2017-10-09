

## <a name="generate-hello-certificate-signing-request-file"></a><span data-ttu-id="01d57-101">Generar archivo de solicitud de firma de certificado de hello</span><span class="sxs-lookup"><span data-stu-id="01d57-101">Generate hello Certificate Signing Request file</span></span>
<span data-ttu-id="01d57-102">Hola servicio de notificación de inserción de Apple (APNS) utiliza certificados tooauthenticate las notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="01d57-102">hello Apple Push Notification Service (APNS) uses certificates tooauthenticate your push notifications.</span></span> <span data-ttu-id="01d57-103">Siga estos toosend instrucciones toocreate Hola inserción necesario certificado y recibir notificaciones.</span><span class="sxs-lookup"><span data-stu-id="01d57-103">Follow these instructions toocreate hello necessary push certificate toosend and receive notifications.</span></span> <span data-ttu-id="01d57-104">Para obtener más información sobre estos conceptos, vea oficial de hello [servicio de notificaciones Push de Apple](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentación.</span><span class="sxs-lookup"><span data-stu-id="01d57-104">For more information on these concepts see hello official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="01d57-105">Generar archivo de solicitud de firma de certificado (CSR) hello, que es utilizado por toogenerate de Apple un certificado firmado de inserción.</span><span class="sxs-lookup"><span data-stu-id="01d57-105">Generate hello Certificate Signing Request (CSR) file, which is used by Apple toogenerate a signed push certificate.</span></span>

1. <span data-ttu-id="01d57-106">En el equipo Mac, ejecute hello herramienta de acceso a llaves.</span><span class="sxs-lookup"><span data-stu-id="01d57-106">On your Mac, run hello Keychain Access tool.</span></span> <span data-ttu-id="01d57-107">Se puede abrir desde hello **utilidades** carpeta o hello **otros** carpeta en el panel de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="01d57-107">It can be opened from hello **Utilities** folder or hello **Other** folder on hello launch pad.</span></span>
2. <span data-ttu-id="01d57-108">Haga clic en **Keychain Access** (Acceso a llaves), expanda **Certificate Assistant**, (Asistente para certificados) y, a continuación, haga clic en **Request a Certificate from a Certificate Authority...** (Solicitar un certificado de una entidad de certificación...).</span><span class="sxs-lookup"><span data-stu-id="01d57-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="01d57-109">Seleccione el **dirección de correo electrónico del usuario** y **nombre común** , asegúrese de que **guardar toodisk** está seleccionada y, a continuación, haga clic en **continuar**.</span><span class="sxs-lookup"><span data-stu-id="01d57-109">Select your **User Email Address** and **Common Name** , make sure that **Saved toodisk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="01d57-110">Deje hello **dirección de correo electrónico de la entidad emisora de certificados** campo en blanco, ya que no es necesario.</span><span class="sxs-lookup"><span data-stu-id="01d57-110">Leave hello **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="01d57-111">Escriba un nombre para el archivo de solicitud de firma de certificado (CSR) hello en **Guardar como**, Seleccionar ubicación de hello en **donde**, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="01d57-111">Type a name for hello Certificate Signing Request (CSR) file in **Save As**, select hello location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="01d57-112">Esto ahorra archivo CSR de hello en ubicación de hello seleccionado; ubicación predeterminada de Hello es Hola escritorio.</span><span class="sxs-lookup"><span data-stu-id="01d57-112">This saves hello CSR file in hello selected location; hello default location is in hello Desktop.</span></span> <span data-ttu-id="01d57-113">Recuerde ubicación Hola elegido para este archivo.</span><span class="sxs-lookup"><span data-stu-id="01d57-113">Remember hello location chosen for this file.</span></span>

<span data-ttu-id="01d57-114">A continuación, registre la aplicación con Apple, habilitará las notificaciones de inserción y cargar este toocreate CSR exportado un certificado de inserción.</span><span class="sxs-lookup"><span data-stu-id="01d57-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR toocreate a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="01d57-115">Registro de la aplicación para notificaciones push</span><span class="sxs-lookup"><span data-stu-id="01d57-115">Register your app for push notifications</span></span>
<span data-ttu-id="01d57-116">aplicación de iOS de la tooan de notificaciones de inserción con toobe toosend capaz de, debe registrar la aplicación con Apple y también se registran para notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="01d57-116">toobe able toosend push notifications tooan iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="01d57-117">Si todavía no ha registrado su aplicación, vaya a toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de aprovisionamiento de iOS</a> en hello Centro para desarrolladores de Apple, debe iniciar sesión con su identificador de Apple, haga clic en **identificadores**, a continuación, haga clic en **Id. de aplicaciones** y por último, haga clic en hello  **+**  firmar tooregister una nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="01d57-117">If you have not already registered your app, navigate toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at hello Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on hello **+** sign tooregister a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="01d57-118">Actualizar Hola después de tres campos de la nueva aplicación y, a continuación, haga clic en **continuar**:</span><span class="sxs-lookup"><span data-stu-id="01d57-118">Update hello following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="01d57-119">**Nombre**: escriba un nombre descriptivo para la aplicación hello **nombre** campo hello **descripción del Id. de aplicación** sección.</span><span class="sxs-lookup"><span data-stu-id="01d57-119">**Name**: Type a descriptive name for your app in hello **Name** field in hello **App ID Description** section.</span></span>
   * <span data-ttu-id="01d57-120">**Agrupar identificador**: en hello **explícita Id. de aplicación** sección, especifique un **identificador de paquete** en forma de hello `<Organization Identifier>.<Product Name>` como se mencionó en hello [distribución de aplicaciones Guía de](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="01d57-120">**Bundle Identifier**: Under hello **Explicit App ID** section, enter a **Bundle Identifier** in hello form `<Organization Identifier>.<Product Name>` as mentioned in hello [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="01d57-121">Hola *identificador de la organización* y *Product Name* usar debe coincidir con identificador de la organización de Hola y el nombre de producto que se utilizará al crear el proyecto de XCode.</span><span class="sxs-lookup"><span data-stu-id="01d57-121">hello *Organization Identifier* and *Product Name* you use must match hello organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="01d57-122">En hello screeshot siguiente *NotificationHubs* se utiliza como un identificador de organización y *GetStarted* se usa como nombre de producto de Hola.</span><span class="sxs-lookup"><span data-stu-id="01d57-122">In hello screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as hello product name.</span></span> <span data-ttu-id="01d57-123">Asegurarse de que esto coincide con los valores de hello que va a utilizar en el proyecto de XCode le permitirá toouse Hola correcto perfil de publicación con XCode.</span><span class="sxs-lookup"><span data-stu-id="01d57-123">Making sure this matches hello values you will use in your XCode project will allow you toouse hello correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="01d57-124">**Notificaciones de inserción**: Hola de comprobación **notificaciones Push** opción Hola **servicios de aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="01d57-124">**Push Notifications**: Check hello **Push Notifications** option in hello **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="01d57-125">Esto genera el identificador de la aplicación y solicita información de hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="01d57-125">This generates your App ID and requests you tooconfirm hello information.</span></span> <span data-ttu-id="01d57-126">Haga clic en **registrar** tooconfirm Hola nuevo identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="01d57-126">Click **Register** tooconfirm hello new App ID.</span></span>
     
      <span data-ttu-id="01d57-127">Una vez que pulses **registrar**, verá hello **completar registro** pantalla, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="01d57-127">Once you click **Register**, you will see hello **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="01d57-128">Haga clic en **Done**(Listo).</span><span class="sxs-lookup"><span data-stu-id="01d57-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="01d57-129">Hola centro de desarrollo en identificadores de aplicación, busque Hola Id. de aplicación que acaba de crear y haga clic en su fila.</span><span class="sxs-lookup"><span data-stu-id="01d57-129">In hello Developer Center, under App IDs, locate hello app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="01d57-130">Al hacer clic en el identificador de la aplicación hello mostrará detalles de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="01d57-130">Clicking on hello app ID will display hello app details.</span></span> <span data-ttu-id="01d57-131">Haga clic en hello **editar** situado en la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="01d57-131">Click hello **Edit** button at hello bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="01d57-132">Desplácese toohello inferior de la pantalla de bienvenida y haga clic en hello **Create Certificate...**  botón en la sección de hello **certificado SSL de inserción de desarrollo**.</span><span class="sxs-lookup"><span data-stu-id="01d57-132">Scroll toohello bottom of hello screen, and click hello **Create Certificate...** button under hello section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="01d57-133">Esto muestra el Asistente "Agregar certificado de iOS" de Hola.</span><span class="sxs-lookup"><span data-stu-id="01d57-133">This displays hello "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="01d57-134">Este tutorial usa un certificado de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="01d57-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="01d57-135">Hola mismo proceso se usa al registrar un certificado de producción.</span><span class="sxs-lookup"><span data-stu-id="01d57-135">hello same process is used when registering a production certificate.</span></span> <span data-ttu-id="01d57-136">Siempre que se asegure de que usas Hola mismo tipo de certificado al enviar notificaciones.</span><span class="sxs-lookup"><span data-stu-id="01d57-136">Just make sure that you use hello same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="01d57-137">Haga clic en **Elegir archivo**, busque la ubicación de toohello donde guardó el archivo CSR hello que creó en la primera tarea de Hola y luego haga clic en **generar**.</span><span class="sxs-lookup"><span data-stu-id="01d57-137">Click **Choose File**, browse toohello location where you saved hello CSR file that you created in hello first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="01d57-138">Después de crea el certificado de hello portal hello, haga clic en hello **descargar** y haga clic en **realiza**.</span><span class="sxs-lookup"><span data-stu-id="01d57-138">After hello certificate is created by hello portal, click hello **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="01d57-139">Esto descarga el certificado de Hola y lo guarda tooyour equipo en la carpeta de descargas.</span><span class="sxs-lookup"><span data-stu-id="01d57-139">This downloads hello certificate and saves it tooyour computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="01d57-140">De forma predeterminada, Hola descargó el archivo se denomina un certificado de desarrollo **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="01d57-140">By default, hello downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="01d57-141">Haga doble clic en el certificado de inserción descargado hello **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="01d57-141">Double-click hello downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="01d57-142">Esto instala un nuevo certificado Hola Hola llaves, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="01d57-142">This installs hello new certificate in hello Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="01d57-143">nombre de Hello en el certificado puede ser diferente, pero estará prefijado con **servicios de inserción del desarrollo de Apple iOS:**.</span><span class="sxs-lookup"><span data-stu-id="01d57-143">hello name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="01d57-144">En acceso a llaveros, haga clic en nuevo certificado de inserción de Hola que creó en hello **certificados** categoría.</span><span class="sxs-lookup"><span data-stu-id="01d57-144">In Keychain Access, right-click hello new push certificate that you created in hello **Certificates** category.</span></span> <span data-ttu-id="01d57-145">Haga clic en **exportar**, el nombre de archivo hello, seleccione hello **. p12** dar formato y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="01d57-145">Click **Export**, name hello file, select hello **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="01d57-146">Tome nota del nombre de archivo de Hola y ubicación del certificado exportado. p12 de Hola.</span><span class="sxs-lookup"><span data-stu-id="01d57-146">Make a note of hello file name and location of hello exported .p12 certificate.</span></span> <span data-ttu-id="01d57-147">Será tooenable usa la autenticación con APNS.</span><span class="sxs-lookup"><span data-stu-id="01d57-147">It will be used tooenable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="01d57-148">Con este tutorial se crea un archivo QuickStart.p12.</span><span class="sxs-lookup"><span data-stu-id="01d57-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="01d57-149">El nombre del archivo y la ubicación pueden ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="01d57-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a><span data-ttu-id="01d57-150">Crear un perfil de aprovisionamiento para la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="01d57-150">Create a provisioning profile for hello app</span></span>
1. <span data-ttu-id="01d57-151">Nuevo en hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de aprovisionamiento de iOS</a>, seleccione **perfiles de aprovisionamiento**, seleccione **todos los**y, a continuación, haga clic en hello  **+**  botón toocreate un nuevo perfil.</span><span class="sxs-lookup"><span data-stu-id="01d57-151">Back in hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click hello **+** button toocreate a new profile.</span></span> <span data-ttu-id="01d57-152">Esto inicia hello **Agregar perfil Provisiong iOS** Asistente</span><span class="sxs-lookup"><span data-stu-id="01d57-152">This launches hello **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="01d57-153">Seleccione **desarrollo de aplicaciones de iOS** en **desarrollo** como tipo de perfil de hello provisiong y haga clic en **continuar**.</span><span class="sxs-lookup"><span data-stu-id="01d57-153">Select **iOS App Development** under **Development** as hello provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="01d57-154">A continuación, seleccione el identificador de la aplicación hello que acaba de crear desde hello **Id. de aplicación** lista desplegable y haga clic en **continuar**</span><span class="sxs-lookup"><span data-stu-id="01d57-154">Next, select hello app ID you just created from hello **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="01d57-155">Hola **seleccionar certificados** pantalla, seleccione el certificado de desarrollo habitual utilizado para la firma de código y haga clic en **continuar**.</span><span class="sxs-lookup"><span data-stu-id="01d57-155">In hello **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="01d57-156">Esto no es certificado de inserción de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="01d57-156">This is not hello push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="01d57-157">A continuación, seleccione hello **dispositivos** toouse para probar y haga clic en **continuar**</span><span class="sxs-lookup"><span data-stu-id="01d57-157">Next, select hello **Devices** toouse for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="01d57-158">Por último, elija un nombre para el perfil de hello en **nombre de perfil**, haga clic en **generar**.</span><span class="sxs-lookup"><span data-stu-id="01d57-158">Finally, pick a name for hello profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="01d57-159">Cuando se crea el nuevo perfil de aprovisionamiento de hello, haga clic en toodownload e instalar en su equipo de desarrollo de Xcode.</span><span class="sxs-lookup"><span data-stu-id="01d57-159">When hello new provisioning profile is created click toodownload it and install it on your Xcode development machine.</span></span> <span data-ttu-id="01d57-160">A continuación, haga clic en **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="01d57-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
