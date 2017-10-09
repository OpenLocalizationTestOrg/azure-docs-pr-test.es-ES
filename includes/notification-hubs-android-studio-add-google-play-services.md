1. <span data-ttu-id="b6e5e-101">Hola abrir Administrador de Android SDK, haga clic en el icono de hello en la barra de herramientas de Hola de Android Studio o haciendo clic en **herramientas** -> **Android** -> **SDK Manager**en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6e5e-101">Open hello Android SDK Manager by clicking hello icon on hello toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on hello menu.</span></span> <span data-ttu-id="b6e5e-102">Busque la versión de destino de Hola de hello SDK de Android que se usa en el proyecto, ábralo haciendo clic en **mostrar detalles del paquete**y elija **Google APIs**, si no está ya instalado.</span><span class="sxs-lookup"><span data-stu-id="b6e5e-102">Locate hello target version of hello Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="b6e5e-103">Haga clic en hello **herramientas de SDK** ficha. Si no ha instalado todavía el servicio Google Play, haga clic en **Google Play Services** (Servicios de Google Play), tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="b6e5e-103">Click hello **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="b6e5e-104">A continuación, haga clic en **aplicar** tooinstall.</span><span class="sxs-lookup"><span data-stu-id="b6e5e-104">Then click **Apply** tooinstall.</span></span> 
   
    <span data-ttu-id="b6e5e-105">Tenga en cuenta Hola SDK ruta de acceso, para su uso en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="b6e5e-105">Note hello SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="b6e5e-106">Abra hello **build.gradle** archivo en el directorio de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="b6e5e-106">Open hello **build.gradle** file in hello app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="b6e5e-107">Agregue esta línea en *dependencias*:</span><span class="sxs-lookup"><span data-stu-id="b6e5e-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="b6e5e-108">Haga clic en hello **proyecto de la sincronización con archivos de Gradle** icono en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6e5e-108">Click hello **Sync Project with Gradle Files** icon in hello tool bar.</span></span>
6. <span data-ttu-id="b6e5e-109">Abra **AndroidManifest.xml** y agregue este toohello etiqueta *aplicación* etiqueta.</span><span class="sxs-lookup"><span data-stu-id="b6e5e-109">Open **AndroidManifest.xml** and add this tag toohello *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

