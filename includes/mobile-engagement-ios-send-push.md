### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a>Conceder acceso tooyour insertar certificado tooMobile interacción
tooallow Mobile Engagement toosend notificaciones de inserción en su nombre, debe toogrant que tener acceso tooyour certificado. Esto se realiza mediante la configuración y especificar el certificado en el portal de interacción móvil Hola. Asegúrese de obtener el certificado. p12, tal y como se explica en la [documentación de Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

1. Navegue tooyour portal de interacción móvil. Asegúrese de se encuentra en hello correcto y, a continuación, haga clic en hello **implique** situado en la parte inferior de hello:
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. Haga clic en hello **configuración** página en el Portal de interacción. Desde allí, haga clic en hello **inserción nativa** sección tooupload su certificado p12:
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. Elija el certificado p12, cárguelo y escriba la contraseña:
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a>Enviar una aplicación de tooyour de notificación
Se creará una campaña de notificación de inserción simple que se va a enviar una aplicación de tooour de inserción:

1. Navegue toohello **alcanzar** ficha en el portal de interacción móvil.
2. Haga clic en **nuevo anuncio** toocreate la campaña de inserción
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. El programa de instalación primeros campos de saludo de la campaña:
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * Proporcione un **Nombre** para la campaña. 
   * Seleccione hello **hora de entrega** como **fuera de la aplicación solo**: se trata de hello Apple push notificación tipo simple que incorpora algún texto.
   * En el texto de la notificación de hello, escriba Hola primera **título** cuál es la primera línea de Hola de inserción de Hola.
   * A continuación, escriba su **mensaje** que será la segunda línea de Hola
4. Desplácese hacia abajo y, en hello seleccione sección contenido **solo notificación**
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. Ha terminado la campaña más básica de Hola de configuración. Ahora, desplácese hacia abajo y haga clic en **crear** botón toosave la campaña de notificación de inserción. 
6. Por último - haga clic en **activar** toosend notificación de inserción. 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. Podrá recibir una notificación de hello en el dispositivo iOS en Centro de notificaciones de hello como Hola siguiente:
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. Si tienes un Apple Watch emparejado con este dispositivo iOS verá notificación hello en su Apple Watch:
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

