
### <a name="update-manifest-file-tooenable-notifications"></a><span data-ttu-id="beeaa-101">Archivo de manifiesto tooenable notificaciones de actualización</span><span class="sxs-lookup"><span data-stu-id="beeaa-101">Update manifest file tooenable notifications</span></span>
<span data-ttu-id="beeaa-102">Copiar recursos de mensajería en la aplicación Hola a continuación en su Manifest.xml entre hello `<application>` y `</application>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="beeaa-102">Copy hello in-app messaging resources below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
        </receiver>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
        </receiver>

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="beeaa-103">Especificación de un icono para las notificaciones</span><span class="sxs-lookup"><span data-stu-id="beeaa-103">Specify an icon for notifications</span></span>
<span data-ttu-id="beeaa-104">Hola pegar siguiente fragmento XML en su Manifest.xml entre hello `<application>` y `</application>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="beeaa-104">Paste hello following XML snippet in your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="beeaa-105">Esto define icono Hola que aparece tanto en el sistema y las notificaciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="beeaa-105">This defines hello icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="beeaa-106">Es opcional para las notificaciones en aplicación y obligatorio para las notificaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="beeaa-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="beeaa-107">Android rechazará las notificaciones del sistema con iconos no válidos.</span><span class="sxs-lookup"><span data-stu-id="beeaa-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="beeaa-108">Asegúrese de que se usa un icono que existe en uno de hello **pueden dibujar** carpetas (como ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="beeaa-108">Make sure you are using an icon that exists in one of hello **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="beeaa-109">**mipmap** no se admite.</span><span class="sxs-lookup"><span data-stu-id="beeaa-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="beeaa-110">No debe usar hello **selector** icono.</span><span class="sxs-lookup"><span data-stu-id="beeaa-110">You should not use hello **launcher** icon.</span></span> <span data-ttu-id="beeaa-111">Tiene una resolución distinta y suele ser en carpetas de asignación MIP hello, que no es compatible.</span><span class="sxs-lookup"><span data-stu-id="beeaa-111">It has a different resolution and is usually in hello mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="beeaa-112">Para las aplicaciones reales, puede usar un icono adecuado para notificaciones según las [directrices de diseño de Android](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="beeaa-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="beeaa-113">toobe toouse seguro correcta resoluciones de icono, puede mirar [estos ejemplos](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="beeaa-113">toobe sure toouse correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="beeaa-114">Desplácese hacia abajo toohello **notificación** sección, haga clic en un icono y, a continuación, haga clic en `PNGS` conjunto puede dibujar del icono de hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="beeaa-114">Scroll down toohello **Notification** section, click an icon, and then click `PNGS` toodownload hello icon drawable set.</span></span> <span data-ttu-id="beeaa-115">Puede ver las carpetas que puede dibujar con qué toouse de resolución para cada versión del icono de Hola.</span><span class="sxs-lookup"><span data-stu-id="beeaa-115">You can see what drawable folders with which resolution toouse for each version of hello icon.</span></span>
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a><span data-ttu-id="beeaa-116">Habilitar las notificaciones de inserción de aplicación tooreceive GCM</span><span class="sxs-lookup"><span data-stu-id="beeaa-116">Enable your app tooreceive GCM push notifications</span></span>
1. <span data-ttu-id="beeaa-117">Pegue el siguiente de hello en su Manifest.xml entre hello `<application>` y `</application>` etiquetas después de reemplazar hello **Id. de remitente** obtenido de la consola de proyecto Firebase.</span><span class="sxs-lookup"><span data-stu-id="beeaa-117">Paste hello following into your Manifest.xml between hello `<application>` and `</application>` tags after replacing hello **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="beeaa-118">Hola \n es deliberado por lo tanto, asegúrese de que terminar proyecto Hola número con él.</span><span class="sxs-lookup"><span data-stu-id="beeaa-118">hello \n is intentional so make sure that you end hello project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="beeaa-119">Pegue el código de hello siguiente en su Manifest.xml entre hello `<application>` y `</application>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="beeaa-119">Paste hello code below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span> <span data-ttu-id="beeaa-120">Reemplace el nombre del paquete de hello <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="beeaa-120">Replace hello package name <Your package name>.</span></span>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. <span data-ttu-id="beeaa-121">Agregar Hola último conjunto de permisos que están resaltados antes de hello `<application>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="beeaa-121">Add hello last set of permissions that are highlighted before hello `<application>` tag.</span></span> <span data-ttu-id="beeaa-122">Reemplace `<Your package name>` por su nombre de paquete real de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="beeaa-122">Replace `<Your package name>` by hello actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

