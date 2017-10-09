
1. Hola **conexiones híbridas** hoja, haga clic en conexión híbrida de hello recién creado, a continuación, haga clic en **el programa de instalación de agente de escucha**.
   
    ![Click Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. Hola **propiedades de conexión híbrida** abre la hoja. En **Administrador de conexiones híbridas local**, elija **descargar y configurar manualmente**, guardar el paquete de descarga de Hola HybridConnectionManager.msi y copie la cadena de conexión de puerta de enlace de Hola.
   
    ![Haga clic aquí tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. Desde un símbolo del sistema de administrador, escriba lo siguiente Hola comandos de instalador de Hola toostart:
   
        start HybridConnectionManager.msi
4. Después de Hola se ejecuta el instalador, haga clic en **ahora no**, a continuación, busque la carpeta de %ProgramFiles%\Microsoft\HybridConnectionManager toohello, ejecute HCMConfigWizard.exe y haga clic en **Sí** en hello **usuario Control de cuentas de** cuadro de diálogo.
5. Pegue la cadena de conexión híbrida de Hola que copió anteriormente y haga clic en **Aceptar**. 
   
    ![Instalación](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. Cuando se haya completado la instalación de hello, haga clic en **cerrar**.
   
    ![Click Close](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    En hello **conexiones híbridas** hoja, hello **estado** columna muestra ahora **conectado**. 
   
    ![Connected Status](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

