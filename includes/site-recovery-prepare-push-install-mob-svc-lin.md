### <a name="prepare-for-a-push-installation-on-a-linux-server"></a>Preparación de una instalación de inserción en un servidor Linux

1. Asegúrese de que hay conectividad de red entre el equipo de Linux de Hola y un servidor de procesos de Hola.
2. Crear una cuenta de que ese servidor de procesos de hello puede usar el equipo de Hola de tooaccess. Hola cuenta debe ser un **raíz** usuario Hola servidor de origen Linux. (Use esta cuenta solo para la instalación de inserción de Hola y para las actualizaciones).
3. Compruebe el archivo/etc/hosts hello en origen Hola Linux servidor tiene las entradas que se asignan direcciones de tooIP de nombre de host local de hello asociadas con todos los adaptadores de red.
4. Instalar paquetes de openssh, el servidor de openssh y openssl de más recientes hello en equipo Hola que desea tooreplicate.
5. Asegúrese de que Secure Shell (SSH) está habilitado y se ejecuta en el puerto 22.
6. Habilitar la autenticación de SFTP subsistema y una contraseña en el archivo de hello sshd_config:
  1.  Inicie sesión como usuario **raíz**.
  2.  En Hola archivo/etcetera/ssh/archivo sshd_config, buscar Hola de línea que comienza con **PasswordAuthentication**.
  3.  Quite el comentario de línea de Hola y Hola valor demasiado**Sí**.
  4.  Línea de Hola de búsqueda que comienza con **subsistema** y quite el comentario de línea de saludo.

     ![Linux](./media/site-recovery-prepare-push-install-mob-svc-lin/mobility2.png)
  5. Reinicie hello **sshd** servicio.

7. Agregar cuenta de hello que creó en CSPSConfigtool.
    1.  Inicie sesión en el servidor de configuración de tooyour.
    2.  Abra **cspsconfigtool.exe**. (Está disponible como un acceso directo en el escritorio de Hola y de carpeta de hello %ProgramData%\home\svsystems\bin.)
    3.  En hello **administrar cuentas de** , haga clic en **Agregar cuenta**.
    4.  Agregar cuenta de hello que ha creado. 
    5.  Escriba las credenciales de Hola que utilizan cuando se habilita la replicación para un equipo.
