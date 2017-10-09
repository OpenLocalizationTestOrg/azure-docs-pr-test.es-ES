> [!IMPORTANT]
> tooreceive notificaciones de inserción de Mobile Engagement, necesita tooenable `Silent Remote Notifications` en la aplicación. Necesitará tooadd Hola valor remoto notificación toohello UIBackgroundModes matriz en el archivo Info.plist.
> 
> 

1. Abra `info.plist` archivo de proyecto de Hola
2. Haga clic en el elemento superior de hello en lista de hello (`Information Property List`) y agregue una nueva fila
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. Hola escriba nueva fila`Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. Haga clic en la fila de hello flecha izquierda tooexpand Hola
5. Agregar Hola sigue valor toohello elemento 0`App downloads content in response toopush notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. Una vez cambiar hello, info.plist Hola XML debe contener Hola después de la clave y valor:
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. Si está usando **Xcode 7+** e **iOS 9+**:
   
   * Habilite **Notificaciones push** en Destinos > Su nombre de destino > Capacidades.

