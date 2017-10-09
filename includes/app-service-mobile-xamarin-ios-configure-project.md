#### <a name="configure-hello-ios-project-in-xamarin-studio"></a>Configurar proyecto de iOS de hello en Xamarin Studio
1. En Xamarin.Studio, abra **Info.plist**, actualización hello y **identificador de paquete** con hello agrupar Id. que creó anteriormente con el nuevo identificador de aplicación.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. Desplácese hacia abajo demasiado**modos en segundo plano**. Seleccione hello **habilitar modos en segundo plano** hello y cuadro **notificaciones remotas** cuadro.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. Haga doble clic en el proyecto en hello solución Panel tooopen **Project Options**.
4. En **generar**, elija **agrupación de firma de iOS**y seleccione Hola identidad correspondiente y perfil de aprovisionamiento acaba de configurar para este proyecto.

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   Esto garantiza que ese proyecto hello usa el nuevo perfil de Hola de firma de código. Para hello oficial Xamarin de aprovisionamiento de dispositivos documentación, vea [aprovisionamiento de dispositivos de Xamarin].

#### <a name="configure-hello-ios-project-in-visual-studio"></a>Configurar el proyecto de iOS de hello en Visual Studio
1. En Visual Studio, haga clic en proyecto de hello y, a continuación, haga clic en **propiedades**.
2. En las páginas de propiedades de hello, haga clic en hello **iOS aplicación** ficha y actualización hello **identificador** con el Id. de Hola que creó anteriormente.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. Hola **agrupación de firma de iOS** ficha identidad correspondiente seleccione hello y aprovisionamiento de configuración de perfil solo para este proyecto.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    Esto garantiza que ese proyecto hello usa el nuevo perfil de Hola de firma de código. Para hello oficial Xamarin de aprovisionamiento de dispositivos documentación, vea [aprovisionamiento de dispositivos de Xamarin].
4. Haga doble clic en Info.plist tooopen y, a continuación, habilitar **RemoteNotifications** en **modos en segundo plano**.

[aprovisionamiento de dispositivos de Xamarin]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
