
### <a name="update-manifest-file-tooenable-notifications"></a>Archivo de manifiesto tooenable notificaciones de actualización
Copiar recursos de mensajería en la aplicación Hola a continuación en su Manifest.xml entre hello `<application>` y `</application>` etiquetas.

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

### <a name="specify-an-icon-for-notifications"></a>Especificación de un icono para las notificaciones
Hola pegar siguiente fragmento XML en su Manifest.xml entre hello `<application>` y `</application>` etiquetas.

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

Esto define icono Hola que aparece tanto en el sistema y las notificaciones de la aplicación. Es opcional para las notificaciones en aplicación y obligatorio para las notificaciones del sistema. Android rechazará las notificaciones del sistema con iconos no válidos.

Asegúrese de que se usa un icono que existe en uno de hello **pueden dibujar** carpetas (como ``engagement_close.png``). **mipmap** no se admite.

> [!NOTE]
> No debe usar hello **selector** icono. Tiene una resolución distinta y suele ser en carpetas de asignación MIP hello, que no es compatible.
> 
> 

Para las aplicaciones reales, puede usar un icono adecuado para notificaciones según las [directrices de diseño de Android](http://developer.android.com/design/patterns/notifications.html).

> [!TIP]
> toobe toouse seguro correcta resoluciones de icono, puede mirar [estos ejemplos](https://www.google.com/design/icons).
> Desplácese hacia abajo toohello **notificación** sección, haga clic en un icono y, a continuación, haga clic en `PNGS` conjunto puede dibujar del icono de hello toodownload. Puede ver las carpetas que puede dibujar con qué toouse de resolución para cada versión del icono de Hola.
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a>Habilitar las notificaciones de inserción de aplicación tooreceive GCM
1. Pegue el siguiente de hello en su Manifest.xml entre hello `<application>` y `</application>` etiquetas después de reemplazar hello **Id. de remitente** obtenido de la consola de proyecto Firebase. Hola \n es deliberado por lo tanto, asegúrese de que terminar proyecto Hola número con él.
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. Pegue el código de hello siguiente en su Manifest.xml entre hello `<application>` y `</application>` etiquetas. Reemplace el nombre del paquete de hello <Your package name>.
   
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
3. Agregar Hola último conjunto de permisos que están resaltados antes de hello `<application>` etiqueta. Reemplace `<Your package name>` por su nombre de paquete real de saludo de la aplicación.
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

