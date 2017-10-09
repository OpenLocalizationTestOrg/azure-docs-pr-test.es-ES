---
title: " Administración de un servidor de procesos de escalado horizontal en Azure Site Recovery | Microsoft Docs"
description: "Este artículo se describe cómo tooset una copia de seguridad y administrar un servidor de procesos de escalabilidad horizontal en Azure Site Recovery."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="5edce-103">Administración de un servidor de procesos de escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="5edce-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="5edce-104">Servidor de procesos de escalado horizontal actúa como un coordinador para transferir datos entre los servicios de recuperación de sitio de Hola y la infraestructura local.</span><span class="sxs-lookup"><span data-stu-id="5edce-104">Scale-out Process Server acts as a coordinator for data transfer between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="5edce-105">En este artículo se describe cómo instalar, configurar y administrar un servidor de procesos de escalado horizontal.</span><span class="sxs-lookup"><span data-stu-id="5edce-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5edce-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5edce-106">Prerequisites</span></span>
<span data-ttu-id="5edce-107">siguiente Hola es Hola recomienda hardware, software y red requerida configuración tooset de un servidor de proceso de escalabilidad horizontal.</span><span class="sxs-lookup"><span data-stu-id="5edce-107">hello following are hello recommended hardware, software, and network configuration required tooset up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="5edce-108">[Planificación de capacidad](site-recovery-capacity-planner.md) es un tooensure paso importante implementar Hola servidor de procesos de escalado horizontal con una configuración que satisfaga los requisitos de carga.</span><span class="sxs-lookup"><span data-stu-id="5edce-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="5edce-109">Lea más sobre las [características de escalado de un servidor de procesos de escalado horizontal](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="5edce-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a><span data-ttu-id="5edce-110">Descargar el software de servidor de procesos de escalado horizontal de Hola</span><span class="sxs-lookup"><span data-stu-id="5edce-110">Downloading hello Scale-out Process Server software</span></span>
1. <span data-ttu-id="5edce-111">Inicie sesión en toohello tooyour portal y examinar Azure almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="5edce-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="5edce-112">Examinar demasiado**infraestructura del sitio de recuperación** > **servidores de configuración** (en VMware para la & máquinas físicas).</span><span class="sxs-lookup"><span data-stu-id="5edce-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="5edce-113">Seleccione el toodrill del servidor de configuración hacia abajo en la página de detalles del servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="5edce-113">Select your configuration server toodrill down into hello configuration server's details page.</span></span>
4. <span data-ttu-id="5edce-114">Haga clic en hello **+ servidor de procesos** botón.</span><span class="sxs-lookup"><span data-stu-id="5edce-114">Click hello **+ Process Server** button.</span></span>
5. <span data-ttu-id="5edce-115">Hola **servidor de proceso de agregar** página, seleccione **servidor de proceso de implementar una implementación escalada local** opción de hello **elija dónde desea toodeploy el servidor de procesos** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="5edce-115">In hello **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from hello **Choose where you want toodeploy your process server** drop-down.</span></span>

  ![Página Agregar servidores](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="5edce-117">Haga clic en hello **descarga Hola configuración unificado de Microsoft Azure Site Recovery** versión más reciente Hola de vínculo toodownload de instalación del servidor de procesos de hello escalado horizontal.</span><span class="sxs-lookup"><span data-stu-id="5edce-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="5edce-118">Hello versión el escalado horizontal del servidor de procesos debe ser igual tooor anterior a la versión del servidor de configuración de hello ejecutando en su entorno.</span><span class="sxs-lookup"><span data-stu-id="5edce-118">hello version of your Scale-out Process Server should be equal tooor lesser than hello Configuration Server version running in your environment.</span></span> <span data-ttu-id="5edce-119">Una compatibilidad de versiones de manera sencilla tooensure es toouse Hola mismos bits de instalador que recientemente usado tooinstall o actualizar el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="5edce-119">A simple way tooensure version compatibility is toouse hello same installer bits that you recently used tooinstall/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="5edce-120">Instalación y registro de un servidor de procesos de escalado horizontal desde la interfaz gráfica de usuario</span><span class="sxs-lookup"><span data-stu-id="5edce-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="5edce-121">Si tiene tooscale horizontalmente la implementación más allá de 200 máquinas de origen o a diario total renovación tasa de más de 2 TB, necesita el volumen de tráfico de proceso adicionales servidores toohandle Hola.</span><span class="sxs-lookup"><span data-stu-id="5edce-121">If you have tooscale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers toohandle hello traffic volume.</span></span>

<span data-ttu-id="5edce-122">Comprobar hello [cambiar el tamaño de las recomendaciones para los servidores de proceso](#size-recommendations-for-the-process-server)y, a continuación, siga estos tooset instrucciones servidor de procesos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5edce-122">Check hello [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions tooset up hello process server.</span></span> <span data-ttu-id="5edce-123">Después de configurar el servidor de hello, migrar toouse de máquinas de origen se.</span><span class="sxs-lookup"><span data-stu-id="5edce-123">After setting up hello server, you migrate source machines toouse it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="5edce-124">Instalación y registro de un servidor de procesos de escalado horizontal mediante la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="5edce-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="5edce-125">Ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="5edce-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="5edce-126">Argumentos de línea de comandos del instalador del servidor de procesos de escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="5edce-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="5edce-127">Creación de un archivo de configuración de proxy</span><span class="sxs-lookup"><span data-stu-id="5edce-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="5edce-128">El parámetro ProxySettingsFilePath toma un archivo como entrada.</span><span class="sxs-lookup"><span data-stu-id="5edce-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="5edce-129">Crear archivo con hello siguiente formato y pasarla como parámetro de entrada ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="5edce-129">Create file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="5edce-130">Modificación de la configuración de proxy del servidor de procesos de escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="5edce-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="5edce-131">Inicie sesión en su servidor de procesos de escalado horizontal.</span><span class="sxs-lookup"><span data-stu-id="5edce-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="5edce-132">Abra una ventana de comandos de administrador de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5edce-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="5edce-133">Ejecute el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="5edce-133">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="5edce-134">A continuación busque el directorio de toohello **%PROGRAMDATA%\ASR\Agent** y ejecución Hola siguiente comando</span><span class="sxs-lookup"><span data-stu-id="5edce-134">Next browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="5edce-135">Registro repetido de un servidor de procesos de escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="5edce-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="5edce-136">Después abra un símbolo del sistema de administrador.</span><span class="sxs-lookup"><span data-stu-id="5edce-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="5edce-137">Busque el directorio de toohello **%PROGRAMDATA%\ASR\Agent** y ejecute el comando de Hola</span><span class="sxs-lookup"><span data-stu-id="5edce-137">Browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="5edce-138">Actualización de un servidor de procesos de escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="5edce-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="5edce-139">Retirada de un servidor de procesos de escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="5edce-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="5edce-140">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="5edce-140">Ensure that:</span></span>
  - <span data-ttu-id="5edce-141">Muestra el estado de conexión del servidor de configuración como **conectado** Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5edce-141">Configuration Server's connection state shows as **Connected** in hello Azure portal</span></span>
  - <span data-ttu-id="5edce-142">Servidor de procesos es todavía puede toocommunicate con el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="5edce-142">Process Server's is still able toocommunicate with hello Configuration server.</span></span>
2. <span data-ttu-id="5edce-143">Inicie sesión en el servidor de procesos de toohello como administrador</span><span class="sxs-lookup"><span data-stu-id="5edce-143">Log in toohello process server as an administrator</span></span>
3. <span data-ttu-id="5edce-144">Abra Panel de Control > Programas > Desinstalar programas.</span><span class="sxs-lookup"><span data-stu-id="5edce-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="5edce-145">Desinstalar programas hello secuencia Hola dado que sigue:</span><span class="sxs-lookup"><span data-stu-id="5edce-145">Uninstall hello programs in hello sequence given following:</span></span>
  * <span data-ttu-id="5edce-146">Servidor de configuración/servidor de procesos de Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5edce-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="5edce-147">Dependencias del servidor de configuración de Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5edce-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="5edce-148">Agente de Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="5edce-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="5edce-149">Puede tardar minutos arriba too15 tooreflect de eliminación del servidor de procesos de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5edce-149">It can take up-too15 minutes for hello Process Server deletion tooreflect in hello Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="5edce-150">Si el servidor de procesos de hello es no se puede toocommunicate con servidor de configuración de hello (estado de conexión en el portal se ha desconectado), deberá toofollow Hola siguientes pasos toopurge de hello servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="5edce-150">If hello Process server is unable toocommunicate with hello Configuration Server (Connection State in portal is Disconnected), then you need toofollow hello following steps toopurge it from hello Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="5edce-151">Anulación del registro de un servidor de procesos de escalado horizontal desconectado de un servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="5edce-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="5edce-152">Requisitos de tamaño para un servidor de procesos de escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="5edce-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="5edce-153">**Servidores de procesos adicionales**</span><span class="sxs-lookup"><span data-stu-id="5edce-153">**Additional process server**</span></span> | <span data-ttu-id="5edce-154">**Tamaño del disco de caché**</span><span class="sxs-lookup"><span data-stu-id="5edce-154">**Cache disk size**</span></span> | <span data-ttu-id="5edce-155">**Frecuencia de cambio de datos**</span><span class="sxs-lookup"><span data-stu-id="5edce-155">**Data change rate**</span></span> | <span data-ttu-id="5edce-156">**Máquinas protegidas**</span><span class="sxs-lookup"><span data-stu-id="5edce-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="5edce-157">4 vCPU (2 sockets * 2 núcleos @ 2,5 GHz), 8 GB de memoria</span><span class="sxs-lookup"><span data-stu-id="5edce-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="5edce-158">< 300 GB</span><span class="sxs-lookup"><span data-stu-id="5edce-158">300 GB</span></span> |<span data-ttu-id="5edce-159">250 GB o menos</span><span class="sxs-lookup"><span data-stu-id="5edce-159">250 GB or less</span></span> |<span data-ttu-id="5edce-160">Replicar 85 máquinas o menos.</span><span class="sxs-lookup"><span data-stu-id="5edce-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="5edce-161">8 vCPU (2 sockets * 4 núcleos @ 2,5 GHz), 12 GB de memoria</span><span class="sxs-lookup"><span data-stu-id="5edce-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="5edce-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="5edce-162">600 GB</span></span> |<span data-ttu-id="5edce-163">250 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="5edce-163">250 GB too1 TB</span></span> |<span data-ttu-id="5edce-164">Replicar entre 85 y 150 máquinas.</span><span class="sxs-lookup"><span data-stu-id="5edce-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="5edce-165">12 vCPU (2 sockets * 6 núcleos @ 2,5 GHz) 24 GB de memoria</span><span class="sxs-lookup"><span data-stu-id="5edce-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="5edce-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="5edce-166">1 TB</span></span> |<span data-ttu-id="5edce-167">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="5edce-167">1 TB too2 TB</span></span> |<span data-ttu-id="5edce-168">Replicar entre 150 y 225 máquinas.</span><span class="sxs-lookup"><span data-stu-id="5edce-168">Replicate between 150-225 machines.</span></span> |
