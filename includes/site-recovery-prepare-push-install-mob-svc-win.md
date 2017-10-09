### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a>Preparación de una instalación de inserción en un equipo Windows

1. Asegúrese de que hay conectividad de red entre el equipo con Windows hello y servidor de procesos de Hola.
2. Crear una cuenta de que ese servidor de procesos de hello puede usar el equipo de Hola de tooaccess. cuenta de Hello debe tener derechos de administrador (local o dominio). (Use esta cuenta solo para la instalación de inserción de Hola y para las actualizaciones del agente).

   > [!NOTE]
   > Si no está utilizando una cuenta de dominio, deshabilite control de acceso de usuarios remotos en el equipo local de Hola. toodisable control de acceso de usuario remoto, en la clave del registro de hello HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, agregue un nuevo valor DWORD: **LocalAccountTokenFilterPolicy**. Establecer valor de hello demasiado**1**. toodo en un comando de símbolo del sistema, ejecute el siguiente comando de hello:  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. Firewall de Windows en el equipo de hello desea tooprotect, seleccione **permitir que una aplicación o una característica a través del Firewall**. Habilite **Compartir archivos e impresoras** e **Instrumental de administración de Windows (WMI)**. Para los equipos que pertenecen tooa dominio, puede configurar Hola firewall mediante el uso de un objeto de directiva de grupo (GPO).

   ![Configuración de firewall](./media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. Agregar cuenta de hello que creó en CSPSConfigtool.
    1.  Inicie sesión en el servidor de configuración de tooyour.
    2.  Abra **cspsconfigtool.exe**. (Está disponible como un acceso directo en el escritorio de Hola y de carpeta de hello %ProgramData%\home\svsystems\bin.)
    3.  En hello **administrar cuentas de** ficha, seleccione **Agregar cuenta**.
    4.  Agregar cuenta de hello que ha creado.
    5.  Escriba las credenciales de Hola que utilizan cuando se habilita la replicación para un equipo.
