## <a name="download-install-and-register-hello-azure-backup-agent"></a>Descargar, instalar y registrar el agente de copia de seguridad de Azure Hola
Después de crear el almacén de copia de seguridad de Azure hello, debe instalarse un agente en cada uno de los equipos de Windows (Windows Server, el cliente de Windows, servidor de System Center Data Protection Manager o equipo del servidor de copia de seguridad de Azure) que permite realizar copias de seguridad de datos y aplicaciones tooAzure.

1. Inicie sesión en toohello [Portal de administración](https://manage.windowsazure.com/)
2. Haga clic en **servicios de recuperación**, a continuación, seleccione almacén de copia de seguridad de Hola que desea tooregister con un servidor. aparece la página de inicio rápido de Hola para ese almacén de copia de seguridad.
   
    ![Inicio rápido](./media/backup-install-agent/quickstart.png)
3. En la página de inicio rápido de hello, haga clic en hello **cliente para Windows Server, System Center Data Protection Manager o Windows** opción **descargar agente**. Haga clic en **guardar** toocopy se toohello de equipo local.
   
    ![Guardar agente](./media/backup-install-agent/agent.png)
4. Una vez instalado el agente de hello, haga doble clic en instalación de hello MARSAgentInstaller.exe toolaunch de agente de copia de seguridad de Azure Hola. Elija la carpeta de instalación de Hola y carpeta temporal requerido para el agente de Hola. ubicación de caché de Hello especificada debe tener espacio libre que es al menos del 5% de datos de copia de seguridad de saludo.
5. Si utiliza un toohello de tooconnect de servidor proxy internet Hola **configuración de Proxy** pantalla, escriba los detalles del servidor proxy Hola. Si usa a un proxy autenticado, escriba los detalles de nombre y la contraseña del usuario de hello en esta pantalla.
6. agente de copia de seguridad de Azure Hola instala .NET Framework 4.5 y Windows PowerShell (si aún no está disponible) toocomplete Hola instalación.
7. Una vez instalado el agente de hello, haga clic en hello **continuar tooRegistration** toocontinue botón con el flujo de trabajo de Hola.
   
   ![Registro](./media/backup-install-agent/register.png)
8. En la pantalla de credenciales de almacén de hello, examinar tooand archivo de credenciales de almacén de hello select que se descargó anteriormente.
   
    ![Credenciales de almacén](./media/backup-install-agent/vc.png)
   
    archivo de credenciales de almacén de Hello es válido únicamente para los 48 horas (después de descargarlo desde el portal de hello). Si se produce algún error en esta pantalla (por ejemplo "las credenciales del almacén archivo ha caducado"), inicio de sesión toohello portal de Azure y descargar credenciales de almacén de hello archivo nuevo.
   
    Asegúrese de que ese archivo de credenciales de almacén de hello está disponible en una ubicación que se puede acceder mediante la aplicación de instalación de Hola. Si se producen errores relacionados de acceso, las credenciales de almacén de copia hello tooa ubicación temporal en esta máquina del archivo y vuelva a intentar la operación de Hola.
   
    Si se produce un error de credencial de almacén no es válido (por ejemplo "no válido las credenciales del almacén") archivo hello está dañado o no tienen credenciales más recientes de hello asociados con el servicio de recuperación de Hola. Vuelva a intentar la operación de hello después de descargar un nuevo archivo de credenciales de almacén desde el portal de Hola. Normalmente, este error aparece si hace clic en un usuario de hello en hello **descarga las credenciales del almacén** opción Hola portal de Azure, en una sucesión rápida. En este caso, solo Hola segundo almacén credencial archivo es válido.
9. Hola **configuración de cifrado** pantalla, puede generar una frase de contraseña o proporcione una frase de contraseña (mínimo de 16 caracteres). Recuerde la frase de contraseña de toosave hello en una ubicación segura.
   
    ![Cifrado](./media/backup-install-agent/encryption.png)
   
   > [!WARNING]
   > Si hello frase de contraseña se pierde u olvida; Microsoft no puede ayudar en la recuperación de datos de copia de seguridad de Hola. usuario final de Hello posee Hola frase de contraseña y Microsoft no tiene visibilidad en la frase de contraseña de hello usada por el usuario final de Hola. Guarde el archivo de hello en una ubicación segura ya que es necesario durante una operación de recuperación.
   > 
   > 
10. Una vez que pulses hello **finalizar** botón, hello máquina se ha registrado correctamente toohello almacén y si ahora está listo toostart copia de seguridad tooMicrosoft Azure.
11. Cuando se utiliza la copia de seguridad de Microsoft Azure independiente puede modificar la configuración de hello especificado durante el flujo de trabajo de registro de hello, haga clic en hello **cambiar las propiedades de** opción en el complemento de mmc de copia de seguridad de Azure Hola.
    
    ![Cambiar propiedades](./media/backup-install-agent/change.png)
    
    O bien, al usar el Administrador de protección de datos, puede modificar la configuración de hello especificado durante el flujo de trabajo de registro de hello haciendo clic en hello **configurar** opción seleccionando **Online** en hello **Administración** ficha.
    
    ![Configurar Copia de seguridad de Azure](./media/backup-install-agent/configure.png)

