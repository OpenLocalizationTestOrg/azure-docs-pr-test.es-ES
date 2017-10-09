
1. <span data-ttu-id="e287d-101">Hola **conexiones híbridas** hoja, haga clic en conexión híbrida de hello recién creado, a continuación, haga clic en **el programa de instalación de agente de escucha**.</span><span class="sxs-lookup"><span data-stu-id="e287d-101">In hello **Hybrid connections** blade, click hello hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Click Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="e287d-103">Hola **propiedades de conexión híbrida** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="e287d-103">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="e287d-104">En **Administrador de conexiones híbridas local**, elija **descargar y configurar manualmente**, guardar el paquete de descarga de Hola HybridConnectionManager.msi y copie la cadena de conexión de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="e287d-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save hello downloaded HybridConnectionManager.msi package, and copy hello gateway connection string.</span></span>
   
    ![Haga clic aquí tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="e287d-106">Desde un símbolo del sistema de administrador, escriba lo siguiente Hola comandos de instalador de Hola toostart:</span><span class="sxs-lookup"><span data-stu-id="e287d-106">From an administrator command prompt, type hello following command toostart hello installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="e287d-107">Después de Hola se ejecuta el instalador, haga clic en **ahora no**, a continuación, busque la carpeta de %ProgramFiles%\Microsoft\HybridConnectionManager toohello, ejecute HCMConfigWizard.exe y haga clic en **Sí** en hello **usuario Control de cuentas de** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e287d-107">After hello installer runs, click **Not now**, then browse toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in hello **User Account Control** dialog.</span></span>
5. <span data-ttu-id="e287d-108">Pegue la cadena de conexión híbrida de Hola que copió anteriormente y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e287d-108">Paste hello hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Instalación](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="e287d-110">Cuando se haya completado la instalación de hello, haga clic en **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="e287d-110">When hello install completes, click **Close**.</span></span>
   
    ![Click Close](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="e287d-112">En hello **conexiones híbridas** hoja, hello **estado** columna muestra ahora **conectado**.</span><span class="sxs-lookup"><span data-stu-id="e287d-112">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

