---
title: " Administración de un servidor de configuración en Azure Site Recovery | Microsoft Docs"
description: "En este artículo se describe cómo configurar y administrar un servidor de configuración."
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
ms.openlocfilehash: 36da8c7d0f3ace194522e5288f26069cf46d470e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="0ac9a-103">Administración de un servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="0ac9a-103">Manage a Configuration Server</span></span>

<span data-ttu-id="0ac9a-104">El servidor de configuración actúa como coordinador entre los servicios de Site Recovery y la infraestructura local.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-104">Configuration Server acts as a coordinator between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="0ac9a-105">En este artículo se describe cómo instalar, configurar y administrar el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-105">This article describes how you can set up, configure, and manage the Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ac9a-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0ac9a-106">Prerequisites</span></span>
<span data-ttu-id="0ac9a-107">A continuación se indican los requisitos mínimos de hardware, software y red necesarios para instalar un servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-107">The following are the minimum hardware, software, and network configuration required to set up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="0ac9a-108">La [planificación de la capacidad](site-recovery-capacity-planner.md) es un paso importante para tener la seguridad de que implementa el servidor de configuración con una configuración que satisfaga sus requisitos de carga.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="0ac9a-109">Lea más sobre los [requisitos de tamaño de un servidor de configuración](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="0ac9a-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a><span data-ttu-id="0ac9a-110">Descarga del software del servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="0ac9a-110">Downloading the Configuration Server software</span></span>
1. <span data-ttu-id="0ac9a-111">Inicie sesión en Azure Portal y busque el almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="0ac9a-112">Vaya a **Site Recovery Infrastructure** (Infraestructura de Site Recovery)  > **Servidores de configuración** (en For VMware & Physical Machines [Para máquinas físicas y VMware]).</span><span class="sxs-lookup"><span data-stu-id="0ac9a-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Página Agregar servidores](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="0ac9a-114">Haga clic en el botón **+Servidores**.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-114">Click the **+Servers** button.</span></span>
4. <span data-ttu-id="0ac9a-115">En la página **Agregar servidor**, haga clic en el botón Descargar para descargar la clave de Registro.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-115">On the **Add Server** page, click the Download button to download the Registration key.</span></span> <span data-ttu-id="0ac9a-116">Necesitará esta clave durante la instalación del servidor de configuración para registrarla en el servicio Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-116">You need this key during the Configuration Server installation to register it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="0ac9a-117">Haga clic en el vínculo **Download the Microsoft Azure Site Recovery Unified Setup** (Descargar la instalación unificada de Microsoft Azure Site Recovery) para descargar la versión más reciente del servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Configuration Server.</span></span>

  ![Página de descarga](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="0ac9a-119">La versión más reciente del servidor de configuración se puede descargar directamente desde [la página del Centro de descarga de Microsoft](http://aka.ms/unifiedsetup).</span><span class="sxs-lookup"><span data-stu-id="0ac9a-119">Latest version of the Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="0ac9a-120">Instalación y registro de un servidor de configuración desde la interfaz gráfica de usuario</span><span class="sxs-lookup"><span data-stu-id="0ac9a-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="0ac9a-121">Instalación y registro de un servidor de configuración desde la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="0ac9a-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="0ac9a-122">Ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="0ac9a-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="0ac9a-123">Argumentos de línea de comandos del instalador del servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="0ac9a-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="0ac9a-124">Creación de un archivo de credenciales de MySql</span><span class="sxs-lookup"><span data-stu-id="0ac9a-124">Create a MySql credentials file</span></span>
<span data-ttu-id="0ac9a-125">El parámetro MySQLCredsFilePath toma como entrada un archivo.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="0ac9a-126">Cree el archivo con el siguiente formato y páselo como parámetro de entrada MySQLCredsFilePath.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-126">Create the file using the following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="0ac9a-127">Creación de un archivo de configuración de proxy</span><span class="sxs-lookup"><span data-stu-id="0ac9a-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="0ac9a-128">El parámetro ProxySettingsFilePath toma un archivo como entrada.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="0ac9a-129">Cree el archivo con el siguiente formato y páselo como parámetro de entrada ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-129">Create the file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="0ac9a-130">Modificación de la configuración de proxy del servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="0ac9a-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="0ac9a-131">Inicie sesión en el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-131">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="0ac9a-132">Inicie el archivo cspsconfigtool.exe mediante el acceso directo del escritorio.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-132">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
3. <span data-ttu-id="0ac9a-133">Haga clic en la pestaña **Registro de almacén**.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-133">Click the **Vault Registration** tab.</span></span>
4. <span data-ttu-id="0ac9a-134">Descargue un nuevo archivo de registro de almacén desde el portal y proporciónelo como entrada a la herramienta.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-134">Download a new Vault Registration file from the portal and provide it as input to the tool.</span></span>

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="0ac9a-136">Proporcione los detalles del nuevo servidor proxy y haga clic en el botón **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-136">Provide the new Proxy Server details and click the **Register** button.</span></span>
6. <span data-ttu-id="0ac9a-137">Abra una ventana de comandos de administrador de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="0ac9a-138">Ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-138">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="0ac9a-139">Si tiene conectados a este servidor de configuración de servidores de procesos de escalado horizontal, deberá [corregir la configuración del proxy de todos los servidores de proceso de escalado horizontal](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) de su implementación.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-139">If you have Scale-out Process servers attached to this Configuration Server, you need to [fix the proxy settings on all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a><span data-ttu-id="0ac9a-140">Volver a registrar un servidor de configuración con el mismo almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="0ac9a-140">Re-register a Configuration Server with the same Recovery Services Vault</span></span>
  1. <span data-ttu-id="0ac9a-141">Inicie sesión en el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-141">Login to your Configuration Server.</span></span>
  2. <span data-ttu-id="0ac9a-142">Inicie el archivo cspsconfigtool.exe mediante el acceso directo del escritorio.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-142">Launch the cspsconfigtool.exe using the shortcut on your desktop.</span></span>
  3. <span data-ttu-id="0ac9a-143">Haga clic en la pestaña **Registro de almacén**.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-143">Click the **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="0ac9a-144">Descargue un nuevo archivo de registro del portal y proporciónelo como entrada a la herramienta.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-144">Download a new Registration file from the portal and provide it as input to the tool.</span></span>
        <span data-ttu-id="0ac9a-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="0ac9a-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="0ac9a-146">Proporcione los detalles del servidor proxy y haga clic en el botón **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-146">Provide the Proxy Server details and click the **Register** button.</span></span>  
  6. <span data-ttu-id="0ac9a-147">Abra una ventana de comandos de administrador de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="0ac9a-148">Ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-148">Run the following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="0ac9a-149">Si tiene conectados servidores de procesos de escalado horizontal a este servidor de configuración, debe [volver a registrar todos los servidores de proceso de escalado horizontal](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) de su implementación.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-149">If you have Scale-out Process servers attached to this Configuration Server, you need to [re-register all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="0ac9a-150">Registro de un servidor de configuración con un almacén de Recovery Services diferente</span><span class="sxs-lookup"><span data-stu-id="0ac9a-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="0ac9a-151">Inicie sesión en el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-151">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="0ac9a-152">En el símbolo del sistema de administrador, ejecute el comando</span><span class="sxs-lookup"><span data-stu-id="0ac9a-152">from an admin command prompt, run the command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="0ac9a-153">Inicie el archivo cspsconfigtool.exe mediante el acceso directo del escritorio.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-153">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
4. <span data-ttu-id="0ac9a-154">Haga clic en la pestaña **Registro de almacén**.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-154">Click the **Vault Registration** tab.</span></span>
5. <span data-ttu-id="0ac9a-155">Descargue un nuevo archivo de registro del portal y proporciónelo como entrada a la herramienta.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-155">Download a new Registration file from the portal and provide it as input to the tool.</span></span>

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="0ac9a-157">Proporcione los detalles del servidor proxy y haga clic en el botón **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-157">Provide the Proxy Server details and click the **Register** button.</span></span>  
7. <span data-ttu-id="0ac9a-158">Abra una ventana de comandos de administrador de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="0ac9a-159">Ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-159">Run the following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="0ac9a-160">Retirada de un servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="0ac9a-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="0ac9a-161">Antes de comenzar la retirada de su servidor de configuración, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0ac9a-161">Ensure the following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="0ac9a-162">Deshabilite la protección en todas las máquinas virtuales de este servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="0ac9a-163">Desasocie todas las directivas de replicación del servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-163">Disassociate all Replication policies from the Configuration Server.</span></span>
3. <span data-ttu-id="0ac9a-164">Elimine todos los servidores vCenter y hosts de vSphere que estén asociados con el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-164">Delete all vCenters servers/vSphere hosts that are associated to the Configuration Server.</span></span>

### <a name="delete-the-configuration-server-from-azure-portal"></a><span data-ttu-id="0ac9a-165">Eliminación del servidor de configuración de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0ac9a-165">Delete the Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="0ac9a-166">En Azure Portal, vaya a **Site Recovery Infrastructure** (Infraestructura de Site Recovery)  > **Servidores de configuración** en el menú Almacén.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-166">In Azure portal, browse to **Site Recovery Infrastructure** > **Configuration Servers** from the Vault menu.</span></span>
2. <span data-ttu-id="0ac9a-167">Haga clic en el servidor de configuración que quiere retirar.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-167">Click the Configuration Server that you want to decommission.</span></span>
3. <span data-ttu-id="0ac9a-168">En la página de detalles del servidor de configuración, haga clic en el botón Eliminar.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-168">On the Configuration Server's details page, click the Delete button.</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="0ac9a-170">Haga clic en **Sí** para confirmar la eliminación del servidor.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-170">Click **Yes** to confirm the deletion of the server.</span></span>

  >[!WARNING]
  <span data-ttu-id="0ac9a-171">Si tiene máquinas virtuales, directivas de replicación o servidores vCenter/hosts de vSphere asociados con este servidor de configuración, no se puede eliminar el servidor.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete the server.</span></span> <span data-ttu-id="0ac9a-172">Elimine estas entidades antes de intentar eliminar el almacén.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-172">Delete these entities before you try to delete the vault.</span></span>

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="0ac9a-173">Desinstalación del software de servidor de configuración y sus dependencias</span><span class="sxs-lookup"><span data-stu-id="0ac9a-173">Uninstall the Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="0ac9a-174">Si tiene pensado volver a usar el servidor de configuración con Azure Site Recovery, puede ir al paso 4 directamente.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-174">If you plan to reuse the Configuration Server with Azure Site Recovery again, then you can skip to step 4 directly</span></span>

1. <span data-ttu-id="0ac9a-175">Inicie sesión como administrador en el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-175">Log on to the Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="0ac9a-176">Abra Panel de Control > Programas > Desinstalar programas.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="0ac9a-177">Desinstale los programas en el orden siguiente:</span><span class="sxs-lookup"><span data-stu-id="0ac9a-177">Uninstall the programs in the following sequence:</span></span>
  * <span data-ttu-id="0ac9a-178">Agente de Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="0ac9a-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="0ac9a-179">Servicio de movilidad de Microsoft Azure Site Recovery/servidor de destino maestro</span><span class="sxs-lookup"><span data-stu-id="0ac9a-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="0ac9a-180">Proveedor de Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0ac9a-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="0ac9a-181">Servidor de configuración/servidor de procesos de Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0ac9a-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="0ac9a-182">Dependencias del servidor de configuración de Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0ac9a-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="0ac9a-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="0ac9a-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="0ac9a-184">Ejecute el siguiente comando desde un símbolo del sistema de administrador:</span><span class="sxs-lookup"><span data-stu-id="0ac9a-184">Run the following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="0ac9a-185">Renovación de certificados de Capa de sockets seguros (SSL) del servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="0ac9a-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="0ac9a-186">El servidor de configuración lleva integrado un servidor web, que coordina las actividades del servicio de movilidad, los servidores de procesos y los servidores de destino maestros conectados a él.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-186">The Configuration Server has an inbuilt webserver, which orchestrates the activities of the Mobility Service, Process Servers, and Master Target servers connected to the Configuration Server.</span></span> <span data-ttu-id="0ac9a-187">El servidor web del servidor de configuración usa un certificado SSL para autenticar a sus clientes.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-187">The Configuration Server's webserver uses an SSL certificate to authenticate its clients.</span></span> <span data-ttu-id="0ac9a-188">Este certificado tiene una fecha de expiración de tres años y se puede renovar en cualquier momento mediante el siguiente método:</span><span class="sxs-lookup"><span data-stu-id="0ac9a-188">This certificate has an expiry of three years and can be renewed at any time using the following method:</span></span>

> [!WARNING]
<span data-ttu-id="0ac9a-189">La expiración del certificado solo se puede realizar en la versión 9.4.XXXX.X o superior.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="0ac9a-190">Actualice todos los componentes de Azure Site Recovery (servidor de configuración, servidor de procesos, servidor de destino maestro y servicio de movilidad) antes de comenzar el flujo de trabajo de renovación de certificados.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-190">Upgrade all the Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start the Renew Certificates workflow.</span></span>

1. <span data-ttu-id="0ac9a-191">En Azure Portal, vaya a Almacén > Site Recovery Infrastructure (Infraestructura de Site Recovery) > Configuration Server (Servidor de configuración).</span><span class="sxs-lookup"><span data-stu-id="0ac9a-191">On the Azure portal, browse to your Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="0ac9a-192">Haga clic en el servidor de configuración para el que necesita renovar el certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-192">Click the Configuration Server for which you need to renew the SSL Certificate for.</span></span>
3. <span data-ttu-id="0ac9a-193">En el mantenimiento del servidor de configuración, puede ver la fecha de expiración del certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-193">Under the Configuration Server health, you can see the expiry date for the SSL Certificate.</span></span>
4. <span data-ttu-id="0ac9a-194">Para renovar el certificado, haga clic en la acción **Renovar certificados** tal y como se muestra en la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="0ac9a-194">Renew the certificate by clicking the **Renew Certificates** action as shown in the following image:</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="0ac9a-196">Advertencia de expiración de certificado de Capa de sockets seguros</span><span class="sxs-lookup"><span data-stu-id="0ac9a-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="0ac9a-197">La validez del certificado SSL para todas las instalaciones que han sucedido antes del mayo de 2016 se estableció en un año.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-197">The SSL Certificate's validity for all installations that happened before May 2016 was set to one year.</span></span> <span data-ttu-id="0ac9a-198">Ha comenzado a ver notificaciones de expiración de certificados en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-198">you have started seeing certificate expiry notifications showing up in the Azure portal.</span></span>

1. <span data-ttu-id="0ac9a-199">Si el certificado SSL del servidor de configuración va a expirar en los próximos dos meses, el servicio comienza a notificarlo a los usuarios en Azure Portal y por correo electrónico (debe estar suscrito a las notificaciones de Azure Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="0ac9a-199">If the Configuration Server's SSL certificate is going to expire in the next two months, the service starts notifying users via the Azure portal & email (you need to be subscribed to Azure Site Recovery notifications).</span></span> <span data-ttu-id="0ac9a-200">Comienza a ver un banner de notificación en la página de recursos del almacén.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-200">You start seeing a notification banner on the Vault's resource page.</span></span>

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="0ac9a-202">Haga clic en el banner para obtener detalles adicionales sobre la expiración del certificado.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-202">Click the banner to get additional details on the Certificate expiry.</span></span>

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="0ac9a-204">Si, en lugar del botón **Renovar ahora**, ve un botón **Actualizar ahora**,</span><span class="sxs-lookup"><span data-stu-id="0ac9a-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="0ac9a-205">significa que hay algunos componentes en su entorno que aún no se han actualizado a 9.4.xxxx.x o versiones superiores.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-205">This means that there are some components in your environment that have not yet been upgraded to 9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="0ac9a-206">Requisitos de tamaño de un servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="0ac9a-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="0ac9a-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="0ac9a-207">**CPU**</span></span> | <span data-ttu-id="0ac9a-208">**Memoria**</span><span class="sxs-lookup"><span data-stu-id="0ac9a-208">**Memory**</span></span> | <span data-ttu-id="0ac9a-209">**Tamaño del disco de caché**</span><span class="sxs-lookup"><span data-stu-id="0ac9a-209">**Cache disk size**</span></span> | <span data-ttu-id="0ac9a-210">**Frecuencia de cambio de datos**</span><span class="sxs-lookup"><span data-stu-id="0ac9a-210">**Data change rate**</span></span> | <span data-ttu-id="0ac9a-211">**Máquinas protegidas**</span><span class="sxs-lookup"><span data-stu-id="0ac9a-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0ac9a-212">8 vCPU (2 sockets * 4 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="0ac9a-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="0ac9a-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="0ac9a-213">16 GB</span></span> |<span data-ttu-id="0ac9a-214">< 300 GB</span><span class="sxs-lookup"><span data-stu-id="0ac9a-214">300 GB</span></span> |<span data-ttu-id="0ac9a-215">500 GB o menos</span><span class="sxs-lookup"><span data-stu-id="0ac9a-215">500 GB or less</span></span> |<span data-ttu-id="0ac9a-216">Replicar menos de 100 máquinas.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="0ac9a-217">12 vCPUs (2 sockets * 6 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="0ac9a-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="0ac9a-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="0ac9a-218">18 GB</span></span> |<span data-ttu-id="0ac9a-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="0ac9a-219">600 GB</span></span> |<span data-ttu-id="0ac9a-220">500 GB a 1 TB</span><span class="sxs-lookup"><span data-stu-id="0ac9a-220">500 GB to 1 TB</span></span> |<span data-ttu-id="0ac9a-221">Replicar entre 100 y 150 máquinas.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="0ac9a-222">16 vCPUs (2 sockets * 8 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="0ac9a-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="0ac9a-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="0ac9a-223">32 GB</span></span> |<span data-ttu-id="0ac9a-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="0ac9a-224">1 TB</span></span> |<span data-ttu-id="0ac9a-225">1 TB a 2 TB</span><span class="sxs-lookup"><span data-stu-id="0ac9a-225">1 TB to 2 TB</span></span> |<span data-ttu-id="0ac9a-226">Replicar entre 150 y 200 máquinas.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="0ac9a-227">Si la actividad diaria de datos supera los 2 TB o planea replicar más de 200 máquinas virtuales, se recomienda implementar servidores de procesos adicionales para equilibrar el tráfico de replicación.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-227">If your daily data churn exceeds 2 TB, or you plan to replicate more than 200 virtual machines, it is recommended to deploy additional process servers to load balance the replication traffic.</span></span> <span data-ttu-id="0ac9a-228">Aprenda cómo implementar servidores de procesos de escalado horizontal.</span><span class="sxs-lookup"><span data-stu-id="0ac9a-228">Learn more about How to deploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="0ac9a-229">Problemas comunes</span><span class="sxs-lookup"><span data-stu-id="0ac9a-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
