---
title: " Administración de un servidor de configuración en Azure Site Recovery | Microsoft Docs"
description: "Este artículo se describe cómo tooset y administrar un servidor de configuración."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="205d0-103">Administración de un servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="205d0-103">Manage a Configuration Server</span></span>

<span data-ttu-id="205d0-104">Servidor de configuración actúa como un coordinador entre servicios de recuperación de sitio de Hola y su infraestructura local.</span><span class="sxs-lookup"><span data-stu-id="205d0-104">Configuration Server acts as a coordinator between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="205d0-105">Este artículo describe cómo instalar, configurar y administrar el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="205d0-105">This article describes how you can set up, configure, and manage hello Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="205d0-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="205d0-106">Prerequisites</span></span>
<span data-ttu-id="205d0-107">siguiente Hola es Hola mínimos de hardware, software y tooset requerida configuración de red de un servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="205d0-107">hello following are hello minimum hardware, software, and network configuration required tooset up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="205d0-108">[Planificación de capacidad](site-recovery-capacity-planner.md) es un tooensure paso importante implementar Hola servidor de configuración con una configuración que satisfaga los requisitos de carga.</span><span class="sxs-lookup"><span data-stu-id="205d0-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="205d0-109">Lea más sobre los [requisitos de tamaño de un servidor de configuración](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="205d0-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a><span data-ttu-id="205d0-110">Descargar el software de servidor de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="205d0-110">Downloading hello Configuration Server software</span></span>
1. <span data-ttu-id="205d0-111">Inicie sesión en toohello tooyour portal y examinar Azure almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="205d0-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="205d0-112">Examinar demasiado**infraestructura del sitio de recuperación** > **servidores de configuración** (en VMware para la & máquinas físicas).</span><span class="sxs-lookup"><span data-stu-id="205d0-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Página Agregar servidores](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="205d0-114">Haga clic en hello **+ servidores** botón.</span><span class="sxs-lookup"><span data-stu-id="205d0-114">Click hello **+Servers** button.</span></span>
4. <span data-ttu-id="205d0-115">En hello **Agregar servidor** página, haga clic en la clave de registro de hello descarga botón toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="205d0-115">On hello **Add Server** page, click hello Download button toodownload hello Registration key.</span></span> <span data-ttu-id="205d0-116">Necesita esta clave durante la tooregister de instalación del servidor de configuración de hello con servicio de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="205d0-116">You need this key during hello Configuration Server installation tooregister it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="205d0-117">Haga clic en hello **descarga Hola configuración unificado de Microsoft Azure Site Recovery** versión más reciente Hola de vínculo toodownload de hello servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="205d0-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Configuration Server.</span></span>

  ![Página de descarga](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="205d0-119">La versión más reciente del programa Hola a servidor de configuración puede descargarse directamente desde [página de descarga de Microsoft Download Center](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="205d0-119">Latest version of hello Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="205d0-120">Instalación y registro de un servidor de configuración desde la interfaz gráfica de usuario</span><span class="sxs-lookup"><span data-stu-id="205d0-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="205d0-121">Instalación y registro de un servidor de configuración desde la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="205d0-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="205d0-122">Ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="205d0-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="205d0-123">Argumentos de línea de comandos del instalador del servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="205d0-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="205d0-124">Creación de un archivo de credenciales de MySql</span><span class="sxs-lookup"><span data-stu-id="205d0-124">Create a MySql credentials file</span></span>
<span data-ttu-id="205d0-125">El parámetro MySQLCredsFilePath toma como entrada un archivo.</span><span class="sxs-lookup"><span data-stu-id="205d0-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="205d0-126">Crear archivo de hello mediante Hola siguiente formato y pasarla como parámetro de entrada MySQLCredsFilePath.</span><span class="sxs-lookup"><span data-stu-id="205d0-126">Create hello file using hello following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="205d0-127">Creación de un archivo de configuración de proxy</span><span class="sxs-lookup"><span data-stu-id="205d0-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="205d0-128">El parámetro ProxySettingsFilePath toma un archivo como entrada.</span><span class="sxs-lookup"><span data-stu-id="205d0-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="205d0-129">Crear archivo de hello mediante Hola siguiente formato y pasarla como parámetro de entrada ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="205d0-129">Create hello file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="205d0-130">Modificación de la configuración de proxy del servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="205d0-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="205d0-131">Servidor de configuración de inicio de sesión tooyour.</span><span class="sxs-lookup"><span data-stu-id="205d0-131">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="205d0-132">Iniciar cspsconfigtool.exe hello mediante acceso directo de hello en el.</span><span class="sxs-lookup"><span data-stu-id="205d0-132">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
3. <span data-ttu-id="205d0-133">Haga clic en hello **registro del almacén** ficha.</span><span class="sxs-lookup"><span data-stu-id="205d0-133">Click hello **Vault Registration** tab.</span></span>
4. <span data-ttu-id="205d0-134">Descargue un nuevo archivo de registro del almacén desde el portal de Hola y proporcionarlo como entrada toohello herramienta.</span><span class="sxs-lookup"><span data-stu-id="205d0-134">Download a new Vault Registration file from hello portal and provide it as input toohello tool.</span></span>

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="205d0-136">Proporcionar detalles de hello nuevo servidor Proxy y haga clic en hello **registrar** botón.</span><span class="sxs-lookup"><span data-stu-id="205d0-136">Provide hello new Proxy Server details and click hello **Register** button.</span></span>
6. <span data-ttu-id="205d0-137">Abra una ventana de comandos de administrador de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="205d0-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="205d0-138">Ejecute el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="205d0-138">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="205d0-139">Si tiene servidores de procesos de escalado horizontal adjunta toothis servidor de configuración, deberá demasiado[corrija la configuración de proxy de hello en todos los servidores de procesos de escalado horizontal de hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) en su implementación.</span><span class="sxs-lookup"><span data-stu-id="205d0-139">If you have Scale-out Process servers attached toothis Configuration Server, you need too[fix hello proxy settings on all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a><span data-ttu-id="205d0-140">Volver a registrar un servidor de configuración con hello mismo almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="205d0-140">Re-register a Configuration Server with hello same Recovery Services Vault</span></span>
  1. <span data-ttu-id="205d0-141">Servidor de configuración de inicio de sesión tooyour.</span><span class="sxs-lookup"><span data-stu-id="205d0-141">Login tooyour Configuration Server.</span></span>
  2. <span data-ttu-id="205d0-142">Iniciar cspsconfigtool.exe hello mediante acceso directo de hello en el escritorio.</span><span class="sxs-lookup"><span data-stu-id="205d0-142">Launch hello cspsconfigtool.exe using hello shortcut on your desktop.</span></span>
  3. <span data-ttu-id="205d0-143">Haga clic en hello **registro del almacén** ficha.</span><span class="sxs-lookup"><span data-stu-id="205d0-143">Click hello **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="205d0-144">Descargue un nuevo archivo de registro desde el portal de Hola y proporcionarlo como entrada toohello herramienta.</span><span class="sxs-lookup"><span data-stu-id="205d0-144">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>
        <span data-ttu-id="205d0-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="205d0-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="205d0-146">Detalles del servidor Proxy de Hola y haga clic en hello **registrar** botón.</span><span class="sxs-lookup"><span data-stu-id="205d0-146">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
  6. <span data-ttu-id="205d0-147">Abra una ventana de comandos de administrador de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="205d0-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="205d0-148">Ejecute el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="205d0-148">Run hello following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="205d0-149">Si tiene servidores de procesos de escalado horizontal adjunta toothis servidor de configuración, deberá demasiado[volver a registrar todos los servidores de procesos de escalado horizontal de hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) en su implementación.</span><span class="sxs-lookup"><span data-stu-id="205d0-149">If you have Scale-out Process servers attached toothis Configuration Server, you need too[re-register all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="205d0-150">Registro de un servidor de configuración con un almacén de Recovery Services diferente</span><span class="sxs-lookup"><span data-stu-id="205d0-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="205d0-151">Servidor de configuración de inicio de sesión tooyour.</span><span class="sxs-lookup"><span data-stu-id="205d0-151">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="205d0-152">desde un símbolo del sistema de administración, ejecute el comando de Hola</span><span class="sxs-lookup"><span data-stu-id="205d0-152">from an admin command prompt, run hello command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="205d0-153">Iniciar cspsconfigtool.exe hello mediante acceso directo de hello en el.</span><span class="sxs-lookup"><span data-stu-id="205d0-153">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
4. <span data-ttu-id="205d0-154">Haga clic en hello **registro del almacén** ficha.</span><span class="sxs-lookup"><span data-stu-id="205d0-154">Click hello **Vault Registration** tab.</span></span>
5. <span data-ttu-id="205d0-155">Descargue un nuevo archivo de registro desde el portal de Hola y proporcionarlo como entrada toohello herramienta.</span><span class="sxs-lookup"><span data-stu-id="205d0-155">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="205d0-157">Detalles del servidor Proxy de Hola y haga clic en hello **registrar** botón.</span><span class="sxs-lookup"><span data-stu-id="205d0-157">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
7. <span data-ttu-id="205d0-158">Abra una ventana de comandos de administrador de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="205d0-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="205d0-159">Ejecute el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="205d0-159">Run hello following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="205d0-160">Retirada de un servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="205d0-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="205d0-161">Asegúrese de siguiente de hello antes de empezar a retirar el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="205d0-161">Ensure hello following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="205d0-162">Deshabilite la protección en todas las máquinas virtuales de este servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="205d0-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="205d0-163">Desasocie todas las directivas de replicación desde el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="205d0-163">Disassociate all Replication policies from hello Configuration Server.</span></span>
3. <span data-ttu-id="205d0-164">Eliminar todos los hosts de servidores/vSphere vCenter que están asociado toohello servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="205d0-164">Delete all vCenters servers/vSphere hosts that are associated toohello Configuration Server.</span></span>

### <a name="delete-hello-configuration-server-from-azure-portal"></a><span data-ttu-id="205d0-165">Eliminar Hola servidor de configuración de portal de Azure</span><span class="sxs-lookup"><span data-stu-id="205d0-165">Delete hello Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="205d0-166">En el portal de Azure, examinar demasiado**infraestructura del sitio de recuperación** > **servidores de configuración** desde el menú de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="205d0-166">In Azure portal, browse too**Site Recovery Infrastructure** > **Configuration Servers** from hello Vault menu.</span></span>
2. <span data-ttu-id="205d0-167">Haga clic en hello servidor de configuración que desea toodecommission.</span><span class="sxs-lookup"><span data-stu-id="205d0-167">Click hello Configuration Server that you want toodecommission.</span></span>
3. <span data-ttu-id="205d0-168">En la página de detalles del servidor de configuración de hello, haga clic en el botón de eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="205d0-168">On hello Configuration Server's details page, click hello Delete button.</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="205d0-170">Haga clic en **Sí** eliminación de hello tooconfirm del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="205d0-170">Click **Yes** tooconfirm hello deletion of hello server.</span></span>

  >[!WARNING]
  <span data-ttu-id="205d0-171">Si tienes máquinas virtuales, las directivas de replicación o hosts de servidores/vSphere vCenter asociados con este servidor de configuración, no se puede eliminar el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="205d0-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete hello server.</span></span> <span data-ttu-id="205d0-172">Eliminar estas entidades antes de probar el almacén de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="205d0-172">Delete these entities before you try toodelete hello vault.</span></span>

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="205d0-173">Desinstalar el software de servidor de configuración de Hola y sus dependencias</span><span class="sxs-lookup"><span data-stu-id="205d0-173">Uninstall hello Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="205d0-174">Si tiene previsto hello tooreuse servidor de configuración con Azure Site Recovery de nuevo, a continuación, puede omitir toostep 4 directamente</span><span class="sxs-lookup"><span data-stu-id="205d0-174">If you plan tooreuse hello Configuration Server with Azure Site Recovery again, then you can skip toostep 4 directly</span></span>

1. <span data-ttu-id="205d0-175">Inicie sesión en el servidor de configuración de toohello como administrador.</span><span class="sxs-lookup"><span data-stu-id="205d0-175">Log on toohello Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="205d0-176">Abra Panel de Control > Programas > Desinstalar programas.</span><span class="sxs-lookup"><span data-stu-id="205d0-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="205d0-177">Desinstalar programas Hola Hola sigue secuencia:</span><span class="sxs-lookup"><span data-stu-id="205d0-177">Uninstall hello programs in hello following sequence:</span></span>
  * <span data-ttu-id="205d0-178">Agente de Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="205d0-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="205d0-179">Servicio de movilidad de Microsoft Azure Site Recovery/servidor de destino maestro</span><span class="sxs-lookup"><span data-stu-id="205d0-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="205d0-180">Proveedor de Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="205d0-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="205d0-181">Servidor de configuración/servidor de procesos de Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="205d0-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="205d0-182">Dependencias del servidor de configuración de Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="205d0-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="205d0-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="205d0-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="205d0-184">Ejecute hello siguiente comando de y el símbolo del sistema de administración.</span><span class="sxs-lookup"><span data-stu-id="205d0-184">Run hello following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="205d0-185">Renovación de certificados de Capa de sockets seguros (SSL) del servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="205d0-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="205d0-186">Hola servidor de configuración tiene un servidor Web integrado, que organiza las actividades de Hola de hello servicio de movilidad, servidores de procesos, y servidores de destino maestro conectan toohello servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="205d0-186">hello Configuration Server has an inbuilt webserver, which orchestrates hello activities of hello Mobility Service, Process Servers, and Master Target servers connected toohello Configuration Server.</span></span> <span data-ttu-id="205d0-187">servidor Web del servidor de configuración de Hola usa un tooauthenticate de certificado SSL de sus clientes.</span><span class="sxs-lookup"><span data-stu-id="205d0-187">hello Configuration Server's webserver uses an SSL certificate tooauthenticate its clients.</span></span> <span data-ttu-id="205d0-188">Este certificado tiene una fecha de expiración de tres años y se puede renovar en cualquier momento con hello siguiente método:</span><span class="sxs-lookup"><span data-stu-id="205d0-188">This certificate has an expiry of three years and can be renewed at any time using hello following method:</span></span>

> [!WARNING]
<span data-ttu-id="205d0-189">La expiración del certificado solo se puede realizar en la versión 9.4.XXXX.X o superior.</span><span class="sxs-lookup"><span data-stu-id="205d0-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="205d0-190">Actualizar todos los componentes de Azure Site Recovery hello (servidor de configuración, el servidor de proceso, servidor de destino maestro, servicio de movilidad) antes de iniciar el flujo de trabajo de hello renovar certificados.</span><span class="sxs-lookup"><span data-stu-id="205d0-190">Upgrade all hello Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start hello Renew Certificates workflow.</span></span>

1. <span data-ttu-id="205d0-191">En Hola portal de Azure, vaya tooyour almacén > infraestructura de recuperación de sitio > servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="205d0-191">On hello Azure portal, browse tooyour Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="205d0-192">Haga clic en el servidor de configuración de hello para la que necesita toorenew Hola certificado SSL para.</span><span class="sxs-lookup"><span data-stu-id="205d0-192">Click hello Configuration Server for which you need toorenew hello SSL Certificate for.</span></span>
3. <span data-ttu-id="205d0-193">En el estado del servidor de configuración de hello, puede ver fecha de expiración de Hola de hello certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="205d0-193">Under hello Configuration Server health, you can see hello expiry date for hello SSL Certificate.</span></span>
4. <span data-ttu-id="205d0-194">Renovar certificado de hello haciendo clic en hello **renovar certificados** acción como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="205d0-194">Renew hello certificate by clicking hello **Renew Certificates** action as shown in hello following image:</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="205d0-196">Advertencia de expiración de certificado de Capa de sockets seguros</span><span class="sxs-lookup"><span data-stu-id="205d0-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="205d0-197">Hello validez del certificado SSL para todas las instalaciones que se produjeron antes de mayo de 2016 estableció tooone año.</span><span class="sxs-lookup"><span data-stu-id="205d0-197">hello SSL Certificate's validity for all installations that happened before May 2016 was set tooone year.</span></span> <span data-ttu-id="205d0-198">se ha iniciado viendo las notificaciones de expiración de certificado aparece en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="205d0-198">you have started seeing certificate expiry notifications showing up in hello Azure portal.</span></span>

1. <span data-ttu-id="205d0-199">Si certificado SSL del servidor de configuración de Hola va a tooexpire en hello en los próximos dos meses, servicio de hello inicia informar a los usuarios a través de hello portal de Azure & correo electrónico (necesita toobe suscrito tooAzure Site Recovery notificaciones).</span><span class="sxs-lookup"><span data-stu-id="205d0-199">If hello Configuration Server's SSL certificate is going tooexpire in hello next two months, hello service starts notifying users via hello Azure portal & email (you need toobe subscribed tooAzure Site Recovery notifications).</span></span> <span data-ttu-id="205d0-200">Empiece a notar un banner de notificación en la página de recursos del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="205d0-200">You start seeing a notification banner on hello Vault's resource page.</span></span>

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="205d0-202">Haga clic en hello pancarta tooget obtener más detalles sobre caducidad del certificado Hola.</span><span class="sxs-lookup"><span data-stu-id="205d0-202">Click hello banner tooget additional details on hello Certificate expiry.</span></span>

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="205d0-204">Si, en lugar del botón **Renovar ahora**, ve un botón **Actualizar ahora**,</span><span class="sxs-lookup"><span data-stu-id="205d0-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="205d0-205">Esto significa que no hay algunos componentes en el entorno que aún no se han actualizado too9.4.xxxx.x o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="205d0-205">This means that there are some components in your environment that have not yet been upgraded too9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="205d0-206">Requisitos de tamaño de un servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="205d0-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="205d0-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="205d0-207">**CPU**</span></span> | <span data-ttu-id="205d0-208">**Memoria**</span><span class="sxs-lookup"><span data-stu-id="205d0-208">**Memory**</span></span> | <span data-ttu-id="205d0-209">**Tamaño del disco de caché**</span><span class="sxs-lookup"><span data-stu-id="205d0-209">**Cache disk size**</span></span> | <span data-ttu-id="205d0-210">**Frecuencia de cambio de datos**</span><span class="sxs-lookup"><span data-stu-id="205d0-210">**Data change rate**</span></span> | <span data-ttu-id="205d0-211">**Máquinas protegidas**</span><span class="sxs-lookup"><span data-stu-id="205d0-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="205d0-212">8 vCPU (2 sockets * 4 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="205d0-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="205d0-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="205d0-213">16 GB</span></span> |<span data-ttu-id="205d0-214">< 300 GB</span><span class="sxs-lookup"><span data-stu-id="205d0-214">300 GB</span></span> |<span data-ttu-id="205d0-215">500 GB o menos</span><span class="sxs-lookup"><span data-stu-id="205d0-215">500 GB or less</span></span> |<span data-ttu-id="205d0-216">Replicar menos de 100 máquinas.</span><span class="sxs-lookup"><span data-stu-id="205d0-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="205d0-217">12 vCPUs (2 sockets * 6 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="205d0-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="205d0-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="205d0-218">18 GB</span></span> |<span data-ttu-id="205d0-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="205d0-219">600 GB</span></span> |<span data-ttu-id="205d0-220">500 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="205d0-220">500 GB too1 TB</span></span> |<span data-ttu-id="205d0-221">Replicar entre 100 y 150 máquinas.</span><span class="sxs-lookup"><span data-stu-id="205d0-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="205d0-222">16 vCPUs (2 sockets * 8 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="205d0-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="205d0-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="205d0-223">32 GB</span></span> |<span data-ttu-id="205d0-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="205d0-224">1 TB</span></span> |<span data-ttu-id="205d0-225">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="205d0-225">1 TB too2 TB</span></span> |<span data-ttu-id="205d0-226">Replicar entre 150 y 200 máquinas.</span><span class="sxs-lookup"><span data-stu-id="205d0-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="205d0-227">Si la actividad diaria de datos supera los 2 TB, o piensa tooreplicate más de 200 máquinas virtuales, se recomienda toodeploy proceso adicional servidores tooload saldo Hola el tráfico de replicación.</span><span class="sxs-lookup"><span data-stu-id="205d0-227">If your daily data churn exceeds 2 TB, or you plan tooreplicate more than 200 virtual machines, it is recommended toodeploy additional process servers tooload balance hello replication traffic.</span></span> <span data-ttu-id="205d0-228">Más información sobre cómo servidores toodeploy proceso de escalabilidad horizontal.</span><span class="sxs-lookup"><span data-stu-id="205d0-228">Learn more about How toodeploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="205d0-229">Problemas comunes</span><span class="sxs-lookup"><span data-stu-id="205d0-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
