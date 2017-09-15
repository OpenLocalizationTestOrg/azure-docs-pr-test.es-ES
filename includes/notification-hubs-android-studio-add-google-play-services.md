1. <span data-ttu-id="d4be3-101">Abra el Administrador de SDK de Android haciendo clic en el icono de la barra de herramientas de Android Studio o haciendo clic en **Herramientas** -> **Android** -> **SDK Manager** en el menú.</span><span class="sxs-lookup"><span data-stu-id="d4be3-101">Open the Android SDK Manager by clicking the icon on the toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on the menu.</span></span> <span data-ttu-id="d4be3-102">Busque la versión de destino del SDK de Android que se usa en su proyecto, ábrala, para lo que debe hacer clic en **Show Package Details** (Mostrar detalles de paquete) y elija **Google APIs** (API de Google), en caso de que no esté instalado.</span><span class="sxs-lookup"><span data-stu-id="d4be3-102">Locate the target version of the Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="d4be3-103">Haga clic en la pestaña **SDK Tools** (Herramientas del SDK).</span><span class="sxs-lookup"><span data-stu-id="d4be3-103">Click the **SDK Tools** tab.</span></span> <span data-ttu-id="d4be3-104">Si no ha instalado todavía el servicio Google Play, haga clic en **Google Play Services** (Servicios de Google Play), tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="d4be3-104">If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="d4be3-105">A continuación, haga clic en **Apply** (Aplicar) para instalarlo.</span><span class="sxs-lookup"><span data-stu-id="d4be3-105">Then click **Apply** to install.</span></span> 
   
    <span data-ttu-id="d4be3-106">Tome nota de la ruta de acceso del SDK para usarla en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="d4be3-106">Note the SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="d4be3-107">Abra el archivo **build.gradle** en el directorio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d4be3-107">Open the **build.gradle** file in the app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="d4be3-108">Agregue esta línea en *dependencias*:</span><span class="sxs-lookup"><span data-stu-id="d4be3-108">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="d4be3-109">Haga clic en el botón **Sincronizar proyecto con archivos de Gradle** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="d4be3-109">Click the **Sync Project with Gradle Files** icon in the tool bar.</span></span>
6. <span data-ttu-id="d4be3-110">Abra **AndroidManifest.xml** y agregue esta etiqueta a la etiqueta *application* .</span><span class="sxs-lookup"><span data-stu-id="d4be3-110">Open **AndroidManifest.xml** and add this tag to the *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

