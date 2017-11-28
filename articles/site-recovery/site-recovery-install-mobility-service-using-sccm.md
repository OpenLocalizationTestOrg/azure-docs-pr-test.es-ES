---
title: "instalación del servicio de movilidad para Azure Site Recovery mediante las herramientas de implementación de software aaaAutomate | Documentos de Microsoft"
description: "Este artículo le ayuda a automatizar la instalación de Mobility Service mediante herramientas de implementación de software como System Center Configuration Manager."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="7c000-103">Automatización de la instalación de Mobility Service mediante herramientas de implementación de software</span><span class="sxs-lookup"><span data-stu-id="7c000-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="7c000-104">En este documento se da por supuesto que está utilizando la versión **9.9.4510.1** o superior.</span><span class="sxs-lookup"><span data-stu-id="7c000-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="7c000-105">En este artículo se proporciona un ejemplo de cómo puede usar System Center Configuration Manager toodeploy Hola servicio de movilidad de Azure Site Recovery en el centro de datos.</span><span class="sxs-lookup"><span data-stu-id="7c000-105">This article provides you an example of how you can use System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="7c000-106">Mediante una herramienta de implementación de software como el Administrador de configuración tiene Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7c000-106">Using a software deployment tool like Configuration Manager has hello following advantages:</span></span>
* <span data-ttu-id="7c000-107">Programación de la implementación de la instalación, ya sean instalaciones nuevas o actualizaciones, durante la ventana de mantenimiento planeada para las actualizaciones de software</span><span class="sxs-lookup"><span data-stu-id="7c000-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="7c000-108">Ajuste de escala toohundreds de implementación de servidores al mismo tiempo</span><span class="sxs-lookup"><span data-stu-id="7c000-108">Scaling deployment toohundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="7c000-109">En este artículo usa la actividad de implementación de System Center Configuration Manager 2012 R2 toodemonstrate Hola.</span><span class="sxs-lookup"><span data-stu-id="7c000-109">This article uses System Center Configuration Manager 2012 R2 toodemonstrate hello deployment activity.</span></span> <span data-ttu-id="7c000-110">También puede automatizar la instalación de Mobility Service mediante [Azure Automation y la configuración de estado deseado](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="7c000-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c000-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7c000-111">Prerequisites</span></span>
1. <span data-ttu-id="7c000-112">Una herramienta de implementación de software, como Configuration Manager, que ya esté implementada en el entorno.</span><span class="sxs-lookup"><span data-stu-id="7c000-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="7c000-113">Cree dos [recopilaciones de dispositivos](https://technet.microsoft.com/library/gg682169.aspx), uno para todos los **servidores Windows**y otro para todos los **servidores Linux**, que desea que tooprotect mediante el uso de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7c000-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want tooprotect by using Site Recovery.</span></span>
3. <span data-ttu-id="7c000-114">Un servidor de configuración que ya esté registrado con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7c000-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="7c000-115">Un red segura recurso compartido de archivos (recurso compartido de bloque de mensajes de servidor) que se puede acceder al servidor de Configuration Manager de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c000-115">A secure network file share (Server Message Block share) that can be accessed by hello Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="7c000-116">Implementación de Mobility Service en equipos que ejecutan Windows</span><span class="sxs-lookup"><span data-stu-id="7c000-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="7c000-117">Este artículo se supone que dirección IP de Hola Hola del servidor de configuración es 192.168.3.121, y ese recurso compartido de red segura archivos hello \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="7c000-117">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="7c000-118">Paso 1: Preparación de la implementación</span><span class="sxs-lookup"><span data-stu-id="7c000-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="7c000-119">Cree una carpeta en el recurso compartido de red de Hola y asígnele el nombre **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="7c000-119">Create a folder on hello network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="7c000-120">Inicie sesión en el servidor de configuración de tooyour y abra un símbolo del sistema administrativo.</span><span class="sxs-lookup"><span data-stu-id="7c000-120">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="7c000-121">Siguiente ejecución Hola comandos toogenerate un archivo de frase de contraseña:</span><span class="sxs-lookup"><span data-stu-id="7c000-121">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="7c000-122">Hola copia **MobSvc.passphrase** archivo en hello **MobSvcWindows** carpeta de recurso compartido de red.</span><span class="sxs-lookup"><span data-stu-id="7c000-122">Copy hello **MobSvc.passphrase** file into hello **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="7c000-123">Examinar toohello repositorio de instalador en el servidor de configuración de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7c000-123">Browse toohello installer repository on hello configuration server by running hello following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="7c000-124">Hola copia  **Microsoft ASR\_UA\_*versión*\_Windows\_GA\_*fecha* \_ Release.exe** toohello **MobSvcWindows** carpeta de recurso compartido de red.</span><span class="sxs-lookup"><span data-stu-id="7c000-124">Copy hello **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** toohello **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="7c000-125">Copiar el siguiente código de hello y guárdelo como **install.bat** en hello **MobSvcWindows** carpeta.</span><span class="sxs-lookup"><span data-stu-id="7c000-125">Copy hello following code, and save it as **install.bat** into hello **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7c000-126">Reemplace los marcadores de posición de hello [CSIP] en esta secuencia de comandos con valores reales de Hola de dirección IP de Hola de su servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="7c000-126">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a><span data-ttu-id="7c000-127">Paso 2: Creación de un paquete</span><span class="sxs-lookup"><span data-stu-id="7c000-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="7c000-128">Inicie sesión en la consola de Configuration Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="7c000-128">Sign in tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="7c000-129">Examinar demasiado**biblioteca de Software** > **administración de aplicaciones** > **paquetes**.</span><span class="sxs-lookup"><span data-stu-id="7c000-129">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="7c000-130">Haga clic con el botón derecho en **Paquetes** y seleccione **Crear paquete**.</span><span class="sxs-lookup"><span data-stu-id="7c000-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="7c000-131">Proporcione valores de versión, descripción, fabricante, idioma y nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c000-131">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="7c000-132">Seleccione hello **este paquete contiene archivos de código fuente** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="7c000-132">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="7c000-133">Haga clic en **examinar**y el recurso compartido de red de hello seleccione donde se almacena el instalador de hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="7c000-133">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="7c000-135">En hello **Elegir tipo de programa Hola que desea toocreate** página, seleccione **programa estándar**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7c000-135">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="7c000-137">En hello **especifique información acerca de este programa estándar** página, proporcione Hola después de entradas y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7c000-137">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="7c000-138">(hello otras entradas pueden utilizar sus valores predeterminados.)</span><span class="sxs-lookup"><span data-stu-id="7c000-138">(hello other inputs can use their default values.)</span></span>

  | <span data-ttu-id="7c000-139">**Nombre de parámetro**</span><span class="sxs-lookup"><span data-stu-id="7c000-139">**Parameter name**</span></span> | <span data-ttu-id="7c000-140">**Valor**</span><span class="sxs-lookup"><span data-stu-id="7c000-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="7c000-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="7c000-141">Name</span></span> | <span data-ttu-id="7c000-142">Instalación del Servicio de movilidad de Microsoft Azure (Windows)</span><span class="sxs-lookup"><span data-stu-id="7c000-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="7c000-143">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="7c000-143">Command line</span></span> | <span data-ttu-id="7c000-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="7c000-144">install.bat</span></span> |
  | <span data-ttu-id="7c000-145">El programa se puede ejecutar</span><span class="sxs-lookup"><span data-stu-id="7c000-145">Program can run</span></span> | <span data-ttu-id="7c000-146">Tanto si un usuario inició sesión como si no</span><span class="sxs-lookup"><span data-stu-id="7c000-146">Whether or not a user is logged on</span></span> |

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="7c000-148">En la página siguiente de hello, seleccionar sistemas operativos de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c000-148">On hello next page, select hello target operating systems.</span></span> <span data-ttu-id="7c000-149">Mobility Service se puede instalar solo en Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="7c000-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="7c000-151">Asistente de hello toocomplete, haga clic en **siguiente** dos veces.</span><span class="sxs-lookup"><span data-stu-id="7c000-151">toocomplete hello wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="7c000-152">script de Hola es compatible con las nuevas instalaciones de agentes de servicio de movilidad y actualiza tooagents que ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="7c000-152">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="7c000-153">Paso 3: Implementar el paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="7c000-153">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="7c000-154">En la consola de Configuration Manager de hello, haga clic en el paquete y seleccione **distribuir contenido**.</span><span class="sxs-lookup"><span data-stu-id="7c000-154">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="7c000-155">![Captura de pantalla de la consola de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="7c000-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="7c000-156">Seleccione hello  **[puntos de distribución](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  en toowhich deben copiarse los paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="7c000-156">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="7c000-157">Asistente de hello completa.</span><span class="sxs-lookup"><span data-stu-id="7c000-157">Complete hello wizard.</span></span> <span data-ttu-id="7c000-158">paquete de Hello, a continuación, inicia replicar toohello especifica puntos de distribución.</span><span class="sxs-lookup"><span data-stu-id="7c000-158">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="7c000-159">Después de realiza la distribución de paquetes de saludo, haga clic en el paquete de Hola y seleccione **implementar**.</span><span class="sxs-lookup"><span data-stu-id="7c000-159">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="7c000-160">![Captura de pantalla de la consola de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="7c000-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="7c000-161">Seleccione la recopilación de dispositivos de Windows Server de Hola que creó en la sección de requisitos previos de hello como recopilación de destino de hello para la implementación.</span><span class="sxs-lookup"><span data-stu-id="7c000-161">Select hello Windows Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Captura de pantalla del Asistente para implementar software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="7c000-163">En hello **especificar destino de contenido de hello** página, seleccione la **puntos de distribución**.</span><span class="sxs-lookup"><span data-stu-id="7c000-163">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="7c000-164">En hello **toocontrol de configuración de especificar cómo se implementará este software** página, asegúrese de que el objetivo de hello es **requiere**.</span><span class="sxs-lookup"><span data-stu-id="7c000-164">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Captura de pantalla del Asistente para implementar software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="7c000-166">En hello **especificar la programación de Hola para esta implementación** página, especifique una programación.</span><span class="sxs-lookup"><span data-stu-id="7c000-166">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="7c000-167">Para más información, consulte [Programación de paquetes](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c000-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="7c000-168">En hello **puntos de distribución** página, configurar las propiedades de hello según las necesidades toohello del centro de datos.</span><span class="sxs-lookup"><span data-stu-id="7c000-168">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="7c000-169">A continuación, complete el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c000-169">Then complete hello wizard.</span></span>

> [!TIP]
> <span data-ttu-id="7c000-170">tooavoid innecesario que se reinicie, instalación de paquete de programación Hola durante la ventana de mantenimiento mensual o la ventana actualizaciones de software.</span><span class="sxs-lookup"><span data-stu-id="7c000-170">tooavoid unnecessary reboots, schedule hello package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="7c000-171">Puede supervisar el progreso de la implementación de hello mediante la consola de Configuration Manager Hola.</span><span class="sxs-lookup"><span data-stu-id="7c000-171">You can monitor hello deployment progress by using hello Configuration Manager console.</span></span> <span data-ttu-id="7c000-172">Vaya demasiado**supervisión** > **implementaciones** > *[el nombre del paquete]*.</span><span class="sxs-lookup"><span data-stu-id="7c000-172">Go too**Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Implementaciones de toomonitor de opción de captura de pantalla de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="7c000-174">Implementación de Mobility Service en equipos que ejecutan Linux</span><span class="sxs-lookup"><span data-stu-id="7c000-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="7c000-175">Este artículo se supone que dirección IP de Hola Hola del servidor de configuración es 192.168.3.121, y ese recurso compartido de red segura archivos hello \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="7c000-175">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="7c000-176">Paso 1: Preparación de la implementación</span><span class="sxs-lookup"><span data-stu-id="7c000-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="7c000-177">Cree una carpeta en el recurso compartido de red de Hola y asígnele el nombre como **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="7c000-177">Create a folder on hello network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="7c000-178">Inicie sesión en el servidor de configuración de tooyour y abra un símbolo del sistema administrativo.</span><span class="sxs-lookup"><span data-stu-id="7c000-178">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="7c000-179">Siguiente ejecución Hola comandos toogenerate un archivo de frase de contraseña:</span><span class="sxs-lookup"><span data-stu-id="7c000-179">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="7c000-180">Hola copia **MobSvc.passphrase** archivo en hello **MobSvcLinux** carpeta de recurso compartido de red.</span><span class="sxs-lookup"><span data-stu-id="7c000-180">Copy hello **MobSvc.passphrase** file into hello **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="7c000-181">Examinar toohello repositorio de instalador en el servidor de configuración de hello mediante la ejecución de comando hello:</span><span class="sxs-lookup"><span data-stu-id="7c000-181">Browse toohello installer repository on hello configuration server by running hello command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="7c000-182">Siguiente de hello copia archivos toohello **MobSvcLinux** carpeta de recurso compartido de red:</span><span class="sxs-lookup"><span data-stu-id="7c000-182">Copy hello following files toohello **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="7c000-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7c000-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="7c000-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7c000-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="7c000-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7c000-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="7c000-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7c000-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="7c000-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7c000-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="7c000-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="7c000-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="7c000-189">Copiar el siguiente código de hello y guárdelo como **install_linux.sh** en hello **MobSvcLinux** carpeta.</span><span class="sxs-lookup"><span data-stu-id="7c000-189">Copy hello following code, and save it as **install_linux.sh** into hello **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="7c000-190">Reemplace los marcadores de posición de hello [CSIP] en esta secuencia de comandos con valores reales de Hola de dirección IP de Hola de su servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="7c000-190">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="7c000-191">Paso 2: Creación de un paquete</span><span class="sxs-lookup"><span data-stu-id="7c000-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="7c000-192">Inicie sesión en la consola de Configuration Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="7c000-192">Sign in  tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="7c000-193">Examinar demasiado**biblioteca de Software** > **administración de aplicaciones** > **paquetes**.</span><span class="sxs-lookup"><span data-stu-id="7c000-193">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="7c000-194">Haga clic con el botón derecho en **Paquetes** y seleccione **Crear paquete**.</span><span class="sxs-lookup"><span data-stu-id="7c000-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="7c000-195">Proporcione valores de versión, descripción, fabricante, idioma y nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c000-195">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="7c000-196">Seleccione hello **este paquete contiene archivos de código fuente** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="7c000-196">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="7c000-197">Haga clic en **examinar**y el recurso compartido de red de hello seleccione donde se almacena el instalador de hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="7c000-197">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="7c000-199">En hello **Elegir tipo de programa Hola que desea toocreate** página, seleccione **programa estándar**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7c000-199">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="7c000-201">En hello **especifique información acerca de este programa estándar** página, proporcione Hola después de entradas y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7c000-201">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="7c000-202">(hello otras entradas pueden utilizar sus valores predeterminados.)</span><span class="sxs-lookup"><span data-stu-id="7c000-202">(hello other inputs can use their default values.)</span></span>

    | <span data-ttu-id="7c000-203">**Nombre de parámetro**</span><span class="sxs-lookup"><span data-stu-id="7c000-203">**Parameter name**</span></span> | <span data-ttu-id="7c000-204">**Valor**</span><span class="sxs-lookup"><span data-stu-id="7c000-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="7c000-205">Nombre</span><span class="sxs-lookup"><span data-stu-id="7c000-205">Name</span></span> | <span data-ttu-id="7c000-206">Instalación del Servicio de movilidad de Microsoft Azure (Linux)</span><span class="sxs-lookup"><span data-stu-id="7c000-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="7c000-207">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="7c000-207">Command line</span></span> | <span data-ttu-id="7c000-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="7c000-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="7c000-209">El programa se puede ejecutar</span><span class="sxs-lookup"><span data-stu-id="7c000-209">Program can run</span></span> | <span data-ttu-id="7c000-210">Tanto si un usuario inició sesión como si no</span><span class="sxs-lookup"><span data-stu-id="7c000-210">Whether or not a user is logged on</span></span> |

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="7c000-212">En la página siguiente de hello, seleccione **este programa puede ejecutarse en cualquier plataforma**.</span><span class="sxs-lookup"><span data-stu-id="7c000-212">On hello next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="7c000-213">![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="7c000-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="7c000-214">Asistente de hello toocomplete, haga clic en **siguiente** dos veces.</span><span class="sxs-lookup"><span data-stu-id="7c000-214">toocomplete hello wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="7c000-215">script de Hola es compatible con las nuevas instalaciones de agentes de servicio de movilidad y actualiza tooagents que ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="7c000-215">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="7c000-216">Paso 3: Implementar el paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="7c000-216">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="7c000-217">En la consola de Configuration Manager de hello, haga clic en el paquete y seleccione **distribuir contenido**.</span><span class="sxs-lookup"><span data-stu-id="7c000-217">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="7c000-218">![Captura de pantalla de la consola de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="7c000-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="7c000-219">Seleccione hello  **[puntos de distribución](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  en toowhich deben copiarse los paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="7c000-219">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="7c000-220">Asistente de hello completa.</span><span class="sxs-lookup"><span data-stu-id="7c000-220">Complete hello wizard.</span></span> <span data-ttu-id="7c000-221">paquete de Hello, a continuación, inicia replicar toohello especifica puntos de distribución.</span><span class="sxs-lookup"><span data-stu-id="7c000-221">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="7c000-222">Después de realiza la distribución de paquetes de saludo, haga clic en el paquete de Hola y seleccione **implementar**.</span><span class="sxs-lookup"><span data-stu-id="7c000-222">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="7c000-223">![Captura de pantalla de la consola de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="7c000-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="7c000-224">Seleccione Hola recopilación de dispositivos de servidor Linux que creó en la sección de requisitos previos de hello como recopilación de destino de hello para la implementación.</span><span class="sxs-lookup"><span data-stu-id="7c000-224">Select hello Linux Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Captura de pantalla del Asistente para implementar software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="7c000-226">En hello **especificar destino de contenido de hello** página, seleccione la **puntos de distribución**.</span><span class="sxs-lookup"><span data-stu-id="7c000-226">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="7c000-227">En hello **toocontrol de configuración de especificar cómo se implementará este software** página, asegúrese de que el objetivo de hello es **requiere**.</span><span class="sxs-lookup"><span data-stu-id="7c000-227">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Captura de pantalla del Asistente para implementar software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="7c000-229">En hello **especificar la programación de Hola para esta implementación** página, especifique una programación.</span><span class="sxs-lookup"><span data-stu-id="7c000-229">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="7c000-230">Para más información, consulte [Programación de paquetes](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c000-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="7c000-231">En hello **puntos de distribución** página, configurar las propiedades de hello según las necesidades toohello del centro de datos.</span><span class="sxs-lookup"><span data-stu-id="7c000-231">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="7c000-232">A continuación, complete el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c000-232">Then complete hello wizard.</span></span>

<span data-ttu-id="7c000-233">Servicio de movilidad se instalará en la recopilación de dispositivos de servidor de Linux, según la programación de toohello configuró Hola.</span><span class="sxs-lookup"><span data-stu-id="7c000-233">Mobility Service gets installed on hello Linux Server Device Collection, according toohello schedule you configured.</span></span>

## <a name="other-methods-tooinstall-mobility-service"></a><span data-ttu-id="7c000-234">Otro tooinstall métodos del servicio de movilidad</span><span class="sxs-lookup"><span data-stu-id="7c000-234">Other methods tooinstall Mobility Service</span></span>
<span data-ttu-id="7c000-235">Aquí tiene otras opciones para instalar Mobility Service:</span><span class="sxs-lookup"><span data-stu-id="7c000-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="7c000-236">Instalación manual mediante la GUI</span><span class="sxs-lookup"><span data-stu-id="7c000-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="7c000-237">Instalación manual mediante la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="7c000-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="7c000-238">Instalación de inserción mediante el servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="7c000-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="7c000-239">Instalación automatizada mediante Azure Automation y la configuración de estado deseado</span><span class="sxs-lookup"><span data-stu-id="7c000-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="7c000-240">Desinstalación de Mobility Service</span><span class="sxs-lookup"><span data-stu-id="7c000-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="7c000-241">Puede crear paquetes de Configuration Manager toouninstall servicio de movilidad.</span><span class="sxs-lookup"><span data-stu-id="7c000-241">You can create Configuration Manager packages toouninstall Mobility Service.</span></span> <span data-ttu-id="7c000-242">El script siguiente de Hola de uso toodo así:</span><span class="sxs-lookup"><span data-stu-id="7c000-242">Use hello following script toodo so:</span></span>

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a><span data-ttu-id="7c000-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c000-243">Next steps</span></span>
<span data-ttu-id="7c000-244">Ya estás listo demasiado[habilitar la protección](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) para las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="7c000-244">You are now ready too[enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
