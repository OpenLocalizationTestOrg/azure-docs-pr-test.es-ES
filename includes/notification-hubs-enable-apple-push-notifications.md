

## <a name="generate-hello-certificate-signing-request-file"></a>Generar archivo de solicitud de firma de certificado de hello
Hola servicio de notificación de inserción de Apple (APNS) utiliza certificados tooauthenticate las notificaciones de inserción. Siga estos toosend instrucciones toocreate Hola inserción necesario certificado y recibir notificaciones. Para obtener más información sobre estos conceptos, vea oficial de hello [servicio de notificaciones Push de Apple](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentación.

Generar archivo de solicitud de firma de certificado (CSR) hello, que es utilizado por toogenerate de Apple un certificado firmado de inserción.

1. En el equipo Mac, ejecute hello herramienta de acceso a llaves. Se puede abrir desde hello **utilidades** carpeta o hello **otros** carpeta en el panel de inicio de Hola.
2. Haga clic en **Keychain Access** (Acceso a llaves), expanda **Certificate Assistant**, (Asistente para certificados) y, a continuación, haga clic en **Request a Certificate from a Certificate Authority...** (Solicitar un certificado de una entidad de certificación...).
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. Seleccione el **dirección de correo electrónico del usuario** y **nombre común** , asegúrese de que **guardar toodisk** está seleccionada y, a continuación, haga clic en **continuar**. Deje hello **dirección de correo electrónico de la entidad emisora de certificados** campo en blanco, ya que no es necesario.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. Escriba un nombre para el archivo de solicitud de firma de certificado (CSR) hello en **Guardar como**, Seleccionar ubicación de hello en **donde**, a continuación, haga clic en **guardar**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      Esto ahorra archivo CSR de hello en ubicación de hello seleccionado; ubicación predeterminada de Hello es Hola escritorio. Recuerde ubicación Hola elegido para este archivo.

A continuación, registre la aplicación con Apple, habilitará las notificaciones de inserción y cargar este toocreate CSR exportado un certificado de inserción.

## <a name="register-your-app-for-push-notifications"></a>Registro de la aplicación para notificaciones push
aplicación de iOS de la tooan de notificaciones de inserción con toobe toosend capaz de, debe registrar la aplicación con Apple y también se registran para notificaciones de inserción.  

1. Si todavía no ha registrado su aplicación, vaya a toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de aprovisionamiento de iOS</a> en hello Centro para desarrolladores de Apple, debe iniciar sesión con su identificador de Apple, haga clic en **identificadores**, a continuación, haga clic en **Id. de aplicaciones** y por último, haga clic en hello  **+**  firmar tooregister una nueva aplicación.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. Actualizar Hola después de tres campos de la nueva aplicación y, a continuación, haga clic en **continuar**:
   
   * **Nombre**: escriba un nombre descriptivo para la aplicación hello **nombre** campo hello **descripción del Id. de aplicación** sección.
   * **Agrupar identificador**: en hello **explícita Id. de aplicación** sección, especifique un **identificador de paquete** en forma de hello `<Organization Identifier>.<Product Name>` como se mencionó en hello [distribución de aplicaciones Guía de](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8). Hola *identificador de la organización* y *Product Name* usar debe coincidir con identificador de la organización de Hola y el nombre de producto que se utilizará al crear el proyecto de XCode. En hello screeshot siguiente *NotificationHubs* se utiliza como un identificador de organización y *GetStarted* se usa como nombre de producto de Hola. Asegurarse de que esto coincide con los valores de hello que va a utilizar en el proyecto de XCode le permitirá toouse Hola correcto perfil de publicación con XCode. 
   * **Notificaciones de inserción**: Hola de comprobación **notificaciones Push** opción Hola **servicios de aplicaciones** sección.
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      Esto genera el identificador de la aplicación y solicita información de hello tooconfirm. Haga clic en **registrar** tooconfirm Hola nuevo identificador de aplicación.
     
      Una vez que pulses **registrar**, verá hello **completar registro** pantalla, tal y como se muestra a continuación. Haga clic en **Done**(Listo).
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. Hola centro de desarrollo en identificadores de aplicación, busque Hola Id. de aplicación que acaba de crear y haga clic en su fila.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      Al hacer clic en el identificador de la aplicación hello mostrará detalles de la aplicación hello. Haga clic en hello **editar** situado en la parte inferior de Hola.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. Desplácese toohello inferior de la pantalla de bienvenida y haga clic en hello **Create Certificate...**  botón en la sección de hello **certificado SSL de inserción de desarrollo**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      Esto muestra el Asistente "Agregar certificado de iOS" de Hola.
   
   > [!NOTE]
   > Este tutorial usa un certificado de desarrollo. Hola mismo proceso se usa al registrar un certificado de producción. Siempre que se asegure de que usas Hola mismo tipo de certificado al enviar notificaciones.
   > 
   > 
3. Haga clic en **Elegir archivo**, busque la ubicación de toohello donde guardó el archivo CSR hello que creó en la primera tarea de Hola y luego haga clic en **generar**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. Después de crea el certificado de hello portal hello, haga clic en hello **descargar** y haga clic en **realiza**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      Esto descarga el certificado de Hola y lo guarda tooyour equipo en la carpeta de descargas.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > De forma predeterminada, Hola descargó el archivo se denomina un certificado de desarrollo **aps_development.cer**.
   > 
   > 
5. Haga doble clic en el certificado de inserción descargado hello **aps_development.cer**.
   
      Esto instala un nuevo certificado Hola Hola llaves, tal y como se muestra a continuación:
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > nombre de Hello en el certificado puede ser diferente, pero estará prefijado con **servicios de inserción del desarrollo de Apple iOS:**.
   > 
   > 
6. En acceso a llaveros, haga clic en nuevo certificado de inserción de Hola que creó en hello **certificados** categoría. Haga clic en **exportar**, el nombre de archivo hello, seleccione hello **. p12** dar formato y, a continuación, haga clic en **guardar**.
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    Tome nota del nombre de archivo de Hola y ubicación del certificado exportado. p12 de Hola. Será tooenable usa la autenticación con APNS.
   
   > [!NOTE]
   > Con este tutorial se crea un archivo QuickStart.p12. El nombre del archivo y la ubicación pueden ser diferentes.
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a>Crear un perfil de aprovisionamiento para la aplicación hello
1. Nuevo en hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de aprovisionamiento de iOS</a>, seleccione **perfiles de aprovisionamiento**, seleccione **todos los**y, a continuación, haga clic en hello  **+**  botón toocreate un nuevo perfil. Esto inicia hello **Agregar perfil Provisiong iOS** Asistente
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. Seleccione **desarrollo de aplicaciones de iOS** en **desarrollo** como tipo de perfil de hello provisiong y haga clic en **continuar**. 
3. A continuación, seleccione el identificador de la aplicación hello que acaba de crear desde hello **Id. de aplicación** lista desplegable y haga clic en **continuar**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. Hola **seleccionar certificados** pantalla, seleccione el certificado de desarrollo habitual utilizado para la firma de código y haga clic en **continuar**. Esto no es certificado de inserción de Hola que acaba de crear.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. A continuación, seleccione hello **dispositivos** toouse para probar y haga clic en **continuar**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. Por último, elija un nombre para el perfil de hello en **nombre de perfil**, haga clic en **generar**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. Cuando se crea el nuevo perfil de aprovisionamiento de hello, haga clic en toodownload e instalar en su equipo de desarrollo de Xcode. A continuación, haga clic en **Hecho**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
