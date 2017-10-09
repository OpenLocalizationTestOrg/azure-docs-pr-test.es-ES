#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall MPIO en el host de Hola
1. Abra el Administrador del servidor en el host de Windows Server. De forma predeterminada, el administrador del servidor se inicia cuando un miembro del grupo de administradores de hello inicia sesión tooa equipo que ejecuta Windows Server 2012 R2 o Windows Server 2012. Hola, administrador del servidor ya no está abierto, haga clic en **Inicio > Administrador del servidor**.
   
    ![Administrador del servidor](./media/storsimple-install-mpio-windows-server/IC740997.png)
2. Haga clic en **Administrador del servidor > Panel > Agregar roles y características**. Esto inicia hello **agregar Roles y características** asistente.
   
    ![Asistente para agregar roles y características 1](./media/storsimple-install-mpio-windows-server/IC740998.png)
3. Hola **agregar Roles y características** asistente, Hola siguientes:
   
   * En hello **antes de comenzar** página, haga clic en **siguiente**.
   * En hello **Seleccionar tipo de instalación** , acepte la configuración predeterminada de Hola de **basada en roles o basada en características** instalación. Haga clic en **Siguiente**.
     
       ![Asistente para agregar roles y características 2](./media/storsimple-install-mpio-windows-server/IC740999.png)
   * En hello **Seleccionar servidor de destino** página, elija **seleccione un servidor de grupo de servidores de hello**. El servidor host debería detectarse automáticamente. Haga clic en **Siguiente**.
   * En hello **seleccionar roles de servidor** página, haga clic en **siguiente**.
   * En hello **seleccionar características** , seleccione **E/S de múltiples rutas**y haga clic en **siguiente**.
     
       ![Asistente para agregar roles y características 5](./media/storsimple-install-mpio-windows-server/IC741000.png)
   * En hello **Confirmar selecciones de instalación** página, confirme la selección de hello y, a continuación, seleccione **reinicie el servidor de destino Hola automáticamente si es necesario**, tal y como se muestra a continuación. Haga clic en **Instalar**.
     
       ![Asistente para agregar roles y características 8](./media/storsimple-install-mpio-windows-server/IC741001.png)
   * Se le notificará cuando se completa la instalación de Hola. Haga clic en **cerrar** Asistente de hello tooclose.
     
       ![Asistente para agregar roles y características 9](./media/storsimple-install-mpio-windows-server/IC741002.png)

