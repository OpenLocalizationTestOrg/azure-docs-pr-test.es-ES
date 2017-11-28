
### <a name="update-manifest-file-to-enable-notifications"></a><span data-ttu-id="02ec3-101">Actualización del archivo de manifiesto para habilitar las notificaciones</span><span class="sxs-lookup"><span data-stu-id="02ec3-101">Update manifest file to enable notifications</span></span>
<span data-ttu-id="02ec3-102">Copie los siguientes recursos de mensajería en aplicación en Manifest.xml, entre las etiquetas `<application>` y `</application>`.</span><span class="sxs-lookup"><span data-stu-id="02ec3-102">Copy the in-app messaging resources below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

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

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="02ec3-103">Especificación de un icono para las notificaciones</span><span class="sxs-lookup"><span data-stu-id="02ec3-103">Specify an icon for notifications</span></span>
<span data-ttu-id="02ec3-104">Pegue el siguiente fragmento XML en su Manifest.xml entre las etiquetas `<application>` y `</application>`.</span><span class="sxs-lookup"><span data-stu-id="02ec3-104">Paste the following XML snippet in your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="02ec3-105">Esto define el icono que se muestra tanto en el sistema como en las notificaciones en aplicación.</span><span class="sxs-lookup"><span data-stu-id="02ec3-105">This defines the icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="02ec3-106">Es opcional para las notificaciones en aplicación y obligatorio para las notificaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="02ec3-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="02ec3-107">Android rechazará las notificaciones del sistema con iconos no válidos.</span><span class="sxs-lookup"><span data-stu-id="02ec3-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="02ec3-108">Asegúrese de que está usando un icono que se encuentra en una de las carpetas de recursos **dibujables** (como ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="02ec3-108">Make sure you are using an icon that exists in one of the **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="02ec3-109">**mipmap** no se admite.</span><span class="sxs-lookup"><span data-stu-id="02ec3-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="02ec3-110">No debería usar el icono del **iniciador** .</span><span class="sxs-lookup"><span data-stu-id="02ec3-110">You should not use the **launcher** icon.</span></span> <span data-ttu-id="02ec3-111">Tiene una resolución diferente y normalmente está en las carpetas mipmap, que no se admiten.</span><span class="sxs-lookup"><span data-stu-id="02ec3-111">It has a different resolution and is usually in the mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="02ec3-112">Para las aplicaciones reales, puede usar un icono adecuado para notificaciones según las [directrices de diseño de Android](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="02ec3-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="02ec3-113">Para asegurarse de usar las resoluciones de icono correctas, consulte [estos ejemplos](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="02ec3-113">To be sure to use correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="02ec3-114">Desplácese hasta la sección **Notificación**, haga clic en un icono y luego haga clic en `PNGS` para descargar el conjunto de iconos dibujables.</span><span class="sxs-lookup"><span data-stu-id="02ec3-114">Scroll down to the **Notification** section, click an icon, and then click `PNGS` to download the icon drawable set.</span></span> <span data-ttu-id="02ec3-115">Puede ver qué carpetas de recursos dibujables usar con qué resolución para cada versión del icono.</span><span class="sxs-lookup"><span data-stu-id="02ec3-115">You can see what drawable folders with which resolution to use for each version of the icon.</span></span>
> 
> 

### <a name="enable-your-app-to-receive-gcm-push-notifications"></a><span data-ttu-id="02ec3-116">Habilitar la aplicación para recibir notificaciones de inserción de GCM</span><span class="sxs-lookup"><span data-stu-id="02ec3-116">Enable your app to receive GCM push notifications</span></span>
1. <span data-ttu-id="02ec3-117">Pegue lo siguiente entre las etiquetas `<application>` y `</application>` del archivo Manifest.xml después de reemplazar el **identificador de remitente** obtenido en la consola del proyecto Firebase.</span><span class="sxs-lookup"><span data-stu-id="02ec3-117">Paste the following into your Manifest.xml between the `<application>` and `</application>` tags after replacing the **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="02ec3-118">\n se introduce de manera intencionada para asegurarse de finalizar el número de proyecto con él.</span><span class="sxs-lookup"><span data-stu-id="02ec3-118">The \n is intentional so make sure that you end the project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="02ec3-119">Pegue el código siguiente en su Manifest.xml entre las etiquetas `<application>` y `</application>`.</span><span class="sxs-lookup"><span data-stu-id="02ec3-119">Paste the code below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span> <span data-ttu-id="02ec3-120">Reemplace el nombre del paquete <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="02ec3-120">Replace the package name <Your package name>.</span></span>
   
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
3. <span data-ttu-id="02ec3-121">Agregue el último conjunto de permisos resaltados antes de la etiqueta `<application>` .</span><span class="sxs-lookup"><span data-stu-id="02ec3-121">Add the last set of permissions that are highlighted before the `<application>` tag.</span></span> <span data-ttu-id="02ec3-122">Reemplace `<Your package name>` por el nombre real del paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="02ec3-122">Replace `<Your package name>` by the actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

