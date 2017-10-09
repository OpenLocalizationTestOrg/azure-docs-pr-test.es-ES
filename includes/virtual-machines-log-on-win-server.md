1. Al hacer clic en **Conectar** se crea y descarga un archivo de Protocolo de escritorio remoto (archivo .rdp). Haga clic en **abiertos** toouse este archivo.
2. Recibirá una advertencia que .rdp hello es de un publicador desconocido. Esto es normal. En la ventana de escritorio remoto de hello, haga clic en **conectar** toocontinue.
   
    ![Captura de pantalla de una advertencia sobre un editor desconocido.](./media/virtual-machines-log-on-win-server/rdp-warn.png)
3. Hola **Windows Security** ventana, escriba las credenciales de Hola para una cuenta en la máquina virtual de hello y, a continuación, haga clic en **Aceptar**.
   
     **Cuenta local** -suele ser cuenta local Hola nombre de usuario y la contraseña que especificó cuando creó Hola máquina virtual. En este caso, el dominio de hello es el nombre de Hola de máquina virtual de Hola y se escribe como *vmname*&#92; *nombre de usuario*.  
   
    **VM Unidos a un dominio** : si Hola VM pertenece tooa dominio, escriba el nombre de usuario de hello en formato de hello *dominio*&#92; *Nombre de usuario*. cuenta de Hello también debe tooeither ser en hello administradores de grupo o se le haya concedido privilegios de acceso remoto toohello máquina virtual.
   
    **Controlador de dominio** : si hello VM es un controlador de dominio, escriba el nombre de usuario de hello y una contraseña de una cuenta de administrador de dominio para ese dominio.
4. Haga clic en **Sí** tooverify Hola identidad de máquina virtual de Hola y finalizar la sesión.
   
   ![Captura de pantalla muestra un mensaje acerca de la verificación de identidad de Hola de hello máquina virtual.](./media/virtual-machines-log-on-win-server/cert-warning.png)

