1. Hola abrir Administrador de Android SDK, haga clic en el icono de hello en la barra de herramientas de Hola de Android Studio o haciendo clic en **herramientas** -> **Android** -> **SDK Manager**en el menú de Hola. Busque la versión de destino de Hola de hello SDK de Android que se usa en el proyecto, ábralo haciendo clic en **mostrar detalles del paquete**y elija **Google APIs**, si no está ya instalado.
2. Haga clic en hello **herramientas de SDK** ficha. Si no ha instalado todavía el servicio Google Play, haga clic en **Google Play Services** (Servicios de Google Play), tal como se muestra a continuación. A continuación, haga clic en **aplicar** tooinstall. 
   
    Tenga en cuenta Hola SDK ruta de acceso, para su uso en un paso posterior. 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. Abra hello **build.gradle** archivo en el directorio de aplicación Hola.
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. Agregue esta línea en *dependencias*: 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. Haga clic en hello **proyecto de la sincronización con archivos de Gradle** icono en la barra de herramientas de Hola.
6. Abra **AndroidManifest.xml** y agregue este toohello etiqueta *aplicación* etiqueta.
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

