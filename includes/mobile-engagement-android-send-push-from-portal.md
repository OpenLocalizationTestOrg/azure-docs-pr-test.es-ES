### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>GRANT Mobile Engagement acceso tooyour clave de API GCM
notificaciones de inserción de tooallow Mobile Engagement toosend en su nombre, debe toogrant que tener acceso tooyour clave de API. Esto se realiza mediante la configuración y escribir la clave en el portal de interacción móvil Hola.

1. En el Portal clásico de Azure, asegúrese de que está en la aplicación de hello se usa para este proyecto y, a continuación, haga clic en hello **implique** situado en la parte inferior de hello:
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. A continuación, haga clic en hello **configuración** -> **inserción nativa** sección tooenter su clave de GCM:
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. Haga clic en hello **editar** icono delante del **clave de API** en hello **configuración GCM** sección tal y como se muestra a continuación:
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. En el menú emergente de hello, Hola GCM servidor clave que obtuvo antes de pegar y, a continuación, haga clic en **Aceptar**.
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a>Enviar una aplicación de tooyour de notificación
Se va a crear una campaña de notificación de inserción simple que envía una aplicación de tooour de notificación de inserción.

1. Navegue toohello **ALCANZAR** ficha en el portal de interacción móvil.
2. Haga clic en **nuevo anuncio** toocreate la campaña de notificación de inserción.
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. Configurar el primer campo de saludo de la campaña a través de hello pasos:
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    a. Asigne un nombre a la campaña.
   
    b. Seleccione hello **tipo de entrega** como *notificación del sistema -> Simple*: se trata de tipo de notificación de inserción de Android simple de Hola que ofrece un título y una pequeña línea de texto.
   
    c. Seleccione **hora de entrega** como *cualquier momento* tooallow Hola aplicación tooreceive una notificación si se inicia la aplicación hello, o no.
   
    d. Hola Hola de tipo de texto de notificación **título** que estará en negrita en la inserción de Hola.
   
    e. Luego escriba su **mensaje**
4. Desplácese hacia abajo y en hello **contenido** sección, seleccione **solo notificación**.
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. Ha terminado la posible de campaña más básica de configuración Hola. Ahora, desplácese hacia abajo en nuevo y haga clic en hello **crear** botón toosave la campaña.
6. Último paso: haga clic en **activar** tooactivate las notificaciones de inserción de toosend de campaña.
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

