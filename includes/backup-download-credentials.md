## <a name="using-vault-credentials-tooauthenticate-with-hello-azure-backup-service"></a>Uso de tooauthenticate de credenciales de almacén con hello servicio de copia de seguridad de Azure
servidor local de Hello (cliente de Windows o servidor de Windows Server o el Administrador de protección de datos) es necesario toobe autenticado con un almacén de copia de seguridad antes de pueda respaldar tooAzure de datos. autenticación de Hola se logra mediante "del almacén de credenciales". concepto de Hola de las credenciales de almacén es similar toohello concepto de un archivo de "configuración de publicación" que se usa en Azure PowerShell.

### <a name="what-is-hello-vault-credential-file"></a>¿Qué es el archivo de credenciales de almacén de hello?
archivo de credenciales de almacén de Hello es un certificado generado por el portal de Hola para cada almacén de copia de seguridad. portal de Hello, a continuación, carga hello toohello clave pública Access Control Service (ACS). clave privada de Hello del certificado de Hola estará disponible toohello usuario como parte del flujo de trabajo de Hola que se proporciona como una entrada en el flujo de trabajo de registro de hello máquina. Esto autentica Hola máquina toosend una copia de seguridad tooan identificado almacén Hola servicio copia de seguridad de Azure.

las credenciales del almacén Hola se utilizan solo durante el flujo de trabajo de registro de hello. Es tooensure de responsabilidad del usuario de Hola que hello las credenciales de almacén archivo no se ve comprometido. Si se encuentra en manos de Hola de cualquier usuario no autorizado, archivo de credenciales de almacén de hello puede ser usado tooregister otras máquinas en Hola mismo almacén. Sin embargo, como datos de copia de seguridad de Hola se cifran con una frase de contraseña que pertenece al cliente de toohello, los datos de copia de seguridad existentes no pueden estar en peligro. toomitigate este problema, las credenciales de almacén se establecen tooexpire en 48 horas. Puede descargar las credenciales de almacén de Hola de un almacén de copia de seguridad de cualquier número de veces: pero solo Hola archivo más reciente almacén credencial sigue intacta durante el flujo de trabajo de registro de hello.

### <a name="download-hello-vault-credential-file"></a>Descargar archivo de credenciales de almacén de Hola
archivo de credenciales de almacén de Hola se descarga a través de un canal seguro de hello portal de Azure. Hola servicio de copia de seguridad de Azure no es consciente de clave privada de hello del certificado de Hola y clave privada de hello no se conserva en el portal de Hola o servicio Hola. Usar hello siguiendo los pasos toodownload Hola almacén credencial archivo tooa equipo local.

1. Inicie sesión en toohello [Portal de administración](https://manage.windowsazure.com/)
2. Haga clic en **servicios de recuperación de** en el panel de navegación izquierdo de Hola y almacén de copia de seguridad de hello select que ha creado. Haga clic en el icono tooget toohello vista inicio rápido de almacén de copia de seguridad de Hola de hello en la nube.
   
   ![Vista rápida](./media/backup-download-credentials/quickview.png)
3. En la página de inicio rápido de hello, haga clic en **descargar credenciales de almacén**. portal de Hello genera el archivo de credenciales de almacén de hello, que están disponible para su descarga.
   
   ![Descargar](./media/backup-download-credentials/downloadvc.png)
4. portal de Hello generará una credencial de almacén mediante una combinación de nombre de almacén de Hola y Hola fecha actual. Haga clic en **guardar** toodownload Hola almacén credenciales toohello cuenta local descargas de carpeta o seleccione Guardar como de hello Guardar menú toospecify una ubicación para las credenciales de almacén de Hola.

### <a name="note"></a>Nota:
* Asegúrese de que las credenciales de almacén de Hola se guarda en una ubicación que se puede acceder desde el equipo. Si se almacena en un recurso compartido de archivo/SMB, busque los permisos de acceso de Hola.
* archivo de credenciales de almacén de Hola se utiliza solo durante el flujo de trabajo de registro de hello.
* archivo de credenciales de almacén de Hello expira después de 48 horas y puede descargarse desde el portal de Hola.
* Toohello copia de seguridad de Azure, consulte [preguntas más frecuentes sobre](../articles/backup/backup-azure-backup-faq.md) si tiene alguna pregunta en el flujo de trabajo de Hola.

