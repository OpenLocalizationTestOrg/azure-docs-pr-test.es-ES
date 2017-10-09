
1. En el Explorador de soluciones de Visual Studio, haga clic en proyecto de aplicación de tienda Windows hello y haga clic en **almacén** > **asociar aplicación con hello almacén**.

    ![Asociar aplicación con la Tienda Windows](./media/app-service-mobile-register-wns/notification-hub-associate-win8-app.png)
2. En el Asistente de hello, haga clic en **siguiente**e inicie sesión con su cuenta de Microsoft. Escriba el nombre de la aplicación en **Reserve un nuevo nombre de aplicación** y después haga clic en **Reservar**.
3. Después de registro de una aplicación Hola es Hola se creó correctamente, seleccione Nuevo nombre de aplicación, haga clic en **siguiente**y, a continuación, haga clic en **asociar**. Esto agrega manifiesto de aplicación Hola necesario tienda Windows registro información toohello.
4. Repita los pasos 1 y 3 para el proyecto de aplicación de tienda de Windows Phone de hello mediante el uso de Hola mismo registro que creó anteriormente para la aplicación de la tienda de Windows hello.  
5. Examinar toohello [centro de desarrollo de Windows](https://dev.windows.com/en-us/overview)e inicie sesión con su cuenta de Microsoft. Haga clic en nuevo registro de aplicación hello en **mis aplicaciones**y, a continuación, expanda **servicios** > **notificaciones de inserción**.
6. En hello **notificaciones de inserción** página, haga clic en **sitio de los servicios de Live** en **servicios de notificación de inserción de Windows (WNS) y aplicaciones móviles de Microsoft Azure**. Tome nota de los valores de hello de hello **SID del paquete** hello y *actual* valor en **secreto de aplicación**. 

    ![Configuración de la aplicación en el Centro para desarrolladores de Hola](./media/app-service-mobile-register-wns/mobile-services-win8-app-push-auth.png)

   > [!IMPORTANT]
   > secreto de aplicación Hola y el SID del paquete son credenciales de seguridad importantes. No los comparta con nadie ni los distribuya con su aplicación.
   >
   >
