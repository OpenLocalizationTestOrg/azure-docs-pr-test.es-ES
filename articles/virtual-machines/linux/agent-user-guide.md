---
title: "Introducción al agente de máquina virtual Linux aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall y configurar el agente de Linux (waagent) toomanage interacción de su máquina virtual con el controlador de tejido de Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a><span data-ttu-id="0ee4d-103">Comprender y usar Hola agente Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="0ee4d-103">Understanding and using hello Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="0ee4d-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="0ee4d-104">Introduction</span></span>
<span data-ttu-id="0ee4d-105">Agente de Linux Hello Microsoft Azure (waagent) administra Linux y FreeBSD aprovisionamiento y la interacción de VM con hello controlador de tejido de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-105">hello Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="0ee4d-106">Proporciona Hola después funcionalidad para las implementaciones de Linux y FreeBSD IaaS:</span><span class="sxs-lookup"><span data-stu-id="0ee4d-106">It provides hello following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="0ee4d-107">Vea agente de Linux de Azure de hello [Léame](https://github.com/Azure/WALinuxAgent/blob/master/README.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-107">See hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="0ee4d-108">**Aprovisionamiento de imágenes**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="0ee4d-109">Creación de una cuenta de usuario</span><span class="sxs-lookup"><span data-stu-id="0ee4d-109">Creation of a user account</span></span>
  * <span data-ttu-id="0ee4d-110">Configuración de los tipos de autenticación de SSH</span><span class="sxs-lookup"><span data-stu-id="0ee4d-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="0ee4d-111">Implementación de claves públicas y pares de claves de SSH</span><span class="sxs-lookup"><span data-stu-id="0ee4d-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="0ee4d-112">Nombre de host de Hola de configuración</span><span class="sxs-lookup"><span data-stu-id="0ee4d-112">Setting hello host name</span></span>
  * <span data-ttu-id="0ee4d-113">Publicación Hola nombre toohello plataforma del host DNS</span><span class="sxs-lookup"><span data-stu-id="0ee4d-113">Publishing hello host name toohello platform DNS</span></span>
  * <span data-ttu-id="0ee4d-114">SSH host huella digital de clave toohello plataforma de informes</span><span class="sxs-lookup"><span data-stu-id="0ee4d-114">Reporting SSH host key fingerprint toohello platform</span></span>
  * <span data-ttu-id="0ee4d-115">Administración del disco de recursos</span><span class="sxs-lookup"><span data-stu-id="0ee4d-115">Resource Disk Management</span></span>
  * <span data-ttu-id="0ee4d-116">Montar el disco del recurso de Hola y formato</span><span class="sxs-lookup"><span data-stu-id="0ee4d-116">Formatting and mounting hello resource disk</span></span>
  * <span data-ttu-id="0ee4d-117">Configuración del espacio de intercambio</span><span class="sxs-lookup"><span data-stu-id="0ee4d-117">Configuring swap space</span></span>
* <span data-ttu-id="0ee4d-118">**Redes**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-118">**Networking**</span></span>
  
  * <span data-ttu-id="0ee4d-119">Administra las rutas tooimprove compatibilidad con los servidores DHCP de plataforma</span><span class="sxs-lookup"><span data-stu-id="0ee4d-119">Manages routes tooimprove compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="0ee4d-120">Garantiza la estabilidad de Hola de nombre de interfaz de red de Hola</span><span class="sxs-lookup"><span data-stu-id="0ee4d-120">Ensures hello stability of hello network interface name</span></span>
* <span data-ttu-id="0ee4d-121">**Kernel**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-121">**Kernel**</span></span>
  
  * <span data-ttu-id="0ee4d-122">Configura NUMA virtual (deshabilitar para el kernel cuya versión es inferior a la versión 2.6.37)</span><span class="sxs-lookup"><span data-stu-id="0ee4d-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="0ee4d-123">Consume entropía de Hyper-V para /dev/random</span><span class="sxs-lookup"><span data-stu-id="0ee4d-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="0ee4d-124">Configura los tiempos de espera de SCSI para dispositivos de la raíz de hello (que pudieron ser remoto)</span><span class="sxs-lookup"><span data-stu-id="0ee4d-124">Configures SCSI timeouts for hello root device (which could be remote)</span></span>
* <span data-ttu-id="0ee4d-125">**Diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="0ee4d-126">Puerto serie de toohello de redirección de consola</span><span class="sxs-lookup"><span data-stu-id="0ee4d-126">Console redirection toohello serial port</span></span>
* <span data-ttu-id="0ee4d-127">**Implementaciones de SCVMM**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="0ee4d-128">Detecta y ejecuta un agente VMM de Hola para Linux Bootstrap cuando se ejecuta en un entorno de System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0ee4d-128">Detects and bootstraps hello VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="0ee4d-129">**Extensión de máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="0ee4d-130">Insertar componente creado por Microsoft y sus socios en la automatización de software y la configuración de tooenable de VM de Linux (IaaS)</span><span class="sxs-lookup"><span data-stu-id="0ee4d-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) tooenable software and configuration automation</span></span>
  * <span data-ttu-id="0ee4d-131">Implementación de la referencia de la extensión de máquina virtual en [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="0ee4d-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="0ee4d-132">Comunicación</span><span class="sxs-lookup"><span data-stu-id="0ee4d-132">Communication</span></span>
<span data-ttu-id="0ee4d-133">Hola el flujo de información desde el agente de hello plataforma toohello se produce a través de dos canales:</span><span class="sxs-lookup"><span data-stu-id="0ee4d-133">hello information flow from hello platform toohello agent occurs via two channels:</span></span>

* <span data-ttu-id="0ee4d-134">Un DVD conectado de tiempo de arranque para las implementaciones de IaaS.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="0ee4d-135">Este DVD incluye un archivo de configuración compatible con OVF que incluye información de aprovisionamiento de todos los que no sea de pares de claves SSH real Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than hello actual SSH keypairs.</span></span>
* <span data-ttu-id="0ee4d-136">Un punto de conexión TCP que expone una API de REST usa tooobtain implementación y configuración de la topología.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-136">A TCP endpoint exposing a REST API used tooobtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="0ee4d-137">Requisitos</span><span class="sxs-lookup"><span data-stu-id="0ee4d-137">Requirements</span></span>
<span data-ttu-id="0ee4d-138">Hello sistemas siguientes se han probado y se sabe toowork con hello agente Linux de Azure:</span><span class="sxs-lookup"><span data-stu-id="0ee4d-138">hello following systems have been tested and are known toowork with hello Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="0ee4d-139">Esta lista puede diferir de la lista oficial de Hola de sistemas compatibles en hello plataforma de Microsoft Azure, como se describe aquí: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="0ee4d-139">This list may differ from hello official list of supported systems on hello Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="0ee4d-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0ee4d-140">CoreOS</span></span>
* <span data-ttu-id="0ee4d-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="0ee4d-141">CentOS 6.3+</span></span>
* <span data-ttu-id="0ee4d-142">Red Hat Enterprise Linux 6.7+</span><span class="sxs-lookup"><span data-stu-id="0ee4d-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="0ee4d-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="0ee4d-143">Debian 7.0+</span></span>
* <span data-ttu-id="0ee4d-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="0ee4d-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="0ee4d-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="0ee4d-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="0ee4d-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="0ee4d-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="0ee4d-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="0ee4d-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="0ee4d-148">Otros sistemas compatibles:</span><span class="sxs-lookup"><span data-stu-id="0ee4d-148">Other Supported Systems:</span></span>

* <span data-ttu-id="0ee4d-149">FreeBSD 10+ (Agente Linux de Azure v2.0.10+)</span><span class="sxs-lookup"><span data-stu-id="0ee4d-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="0ee4d-150">agente de Linux Hola depende algunos paquetes de sistema en orden toofunction correctamente:</span><span class="sxs-lookup"><span data-stu-id="0ee4d-150">hello Linux agent depends on some system packages in order toofunction properly:</span></span>

* <span data-ttu-id="0ee4d-151">Python 2.6</span><span class="sxs-lookup"><span data-stu-id="0ee4d-151">Python 2.6+</span></span>
* <span data-ttu-id="0ee4d-152">OpenSSL 1.0+</span><span class="sxs-lookup"><span data-stu-id="0ee4d-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="0ee4d-153">OpenSSH 5.3+</span><span class="sxs-lookup"><span data-stu-id="0ee4d-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="0ee4d-154">Utilidades del sistema de archivos: sfdisk, fdisk, mkfs, parted</span><span class="sxs-lookup"><span data-stu-id="0ee4d-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="0ee4d-155">Herramientas de contraseña: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="0ee4d-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="0ee4d-156">Herramientas de procesamiento de texto: sed, grep</span><span class="sxs-lookup"><span data-stu-id="0ee4d-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="0ee4d-157">Herramientas de red: ip-route</span><span class="sxs-lookup"><span data-stu-id="0ee4d-157">Network tools: ip-route</span></span>
* <span data-ttu-id="0ee4d-158">Compatibilidad de kernel para el montaje de sistemas de archivos UDF.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="0ee4d-159">Instalación</span><span class="sxs-lookup"><span data-stu-id="0ee4d-159">Installation</span></span>
<span data-ttu-id="0ee4d-160">Instalación mediante un RPM o un paquete DEB desde el repositorio de paquetes de la distribución es método hello preferido de la instalación y la actualización Hola agente Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-160">Installation using an RPM or a DEB package from your distribution's package repository is hello preferred method of installing and upgrading hello Azure Linux Agent.</span></span> <span data-ttu-id="0ee4d-161">Hola todos los [están aprobados proveedores de distribución](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrar paquetes de agente de Linux de Azure de Hola a sus imágenes y repositorios.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-161">All hello [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate hello Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="0ee4d-162">Consulte la documentación del toohello Hola [repositorio de agente Linux de Azure en GitHub](https://github.com/Azure/WALinuxAgent) para opciones de instalación avanzada, como la instalación desde ubicaciones de origen o toocustom o prefijos.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-162">Refer toohello documentation in hello [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or toocustom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="0ee4d-163">Opciones de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="0ee4d-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="0ee4d-164">Marcas</span><span class="sxs-lookup"><span data-stu-id="0ee4d-164">Flags</span></span>
* <span data-ttu-id="0ee4d-165">verbose: Aumenta el nivel de detalle de un comando específico</span><span class="sxs-lookup"><span data-stu-id="0ee4d-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="0ee4d-166">force: Omite la confirmación interactiva de algunos comandos</span><span class="sxs-lookup"><span data-stu-id="0ee4d-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="0ee4d-167">Comandos:</span><span class="sxs-lookup"><span data-stu-id="0ee4d-167">Commands</span></span>
* <span data-ttu-id="0ee4d-168">Ayuda: enumera los comandos de hello compatible y marcas.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-168">help: Lists hello supported commands and flags.</span></span>
* <span data-ttu-id="0ee4d-169">Desaprovisionamiento: intento de sistema de hello tooclean y que sea adecuado para volver a aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-169">deprovision: Attempt tooclean hello system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="0ee4d-170">Esta operación elimina siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="0ee4d-170">This operation deleted hello following:</span></span>
  
  * <span data-ttu-id="0ee4d-171">Todas las claves de host SSH (si Provisioning.RegenerateSshHostKeyPair es 'y' en el archivo de configuración de hello)</span><span class="sxs-lookup"><span data-stu-id="0ee4d-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="0ee4d-172">Configuración de Nameserver en /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="0ee4d-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="0ee4d-173">Contraseña de la raíz de/etc/shadow (si Provisioning.DeleteRootPassword es 'y' en el archivo de configuración de hello)</span><span class="sxs-lookup"><span data-stu-id="0ee4d-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="0ee4d-174">Concesiones del cliente de DHCP en caché</span><span class="sxs-lookup"><span data-stu-id="0ee4d-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="0ee4d-175">Restablece toolocalhost.localdomain de nombre de host</span><span class="sxs-lookup"><span data-stu-id="0ee4d-175">Resets host name toolocalhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="0ee4d-176">Desaprovisionamiento no garantiza que esa imagen Hola haya borrado de toda la información confidencial y adecuado para su redistribución.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-176">Deprovisioning does not guarantee that hello image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="0ee4d-177">Desaprovisionamiento + user: realiza todo bajo - deprovision (arriba) y también elimina la última cuenta de usuario aprovisionado hello (obtenido de /var/lib/waagent) y los datos asociados.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-177">deprovision+user: Performs everything under -deprovision (above) and also deletes hello last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="0ee4d-178">Este parámetro está presente cuando se desaprovisiona una imagen que se estaba aprovisionando anteriormente en Azure de modo que se pueda capturar y volver a usar.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="0ee4d-179">versión: muestra la versión de Hola de waagent</span><span class="sxs-lookup"><span data-stu-id="0ee4d-179">version: Displays hello version of waagent</span></span>
* <span data-ttu-id="0ee4d-180">serialconsole: configura GRUB toomark ttyS0 (Hola primer puerto serie) como consola de arranque de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-180">serialconsole: Configures GRUB toomark ttyS0 (hello first serial port) as hello boot console.</span></span> <span data-ttu-id="0ee4d-181">Esto garantiza que los registros de arranque de kernel se envía toothe de puerto serie y están disponibles para la depuración.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-181">This ensures that kernel bootup logs are sent toothe serial port and made available for debugging.</span></span>
* <span data-ttu-id="0ee4d-182">demonio: ejecutado waagent como una interacción de toomanage daemon con la plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-182">daemon: Run waagent as a daemon toomanage interaction with hello platform.</span></span> <span data-ttu-id="0ee4d-183">Este argumento es toowaagent especificado en la secuencia de comandos de hello waagent init.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-183">This argument is specified toowaagent in hello waagent init script.</span></span>
* <span data-ttu-id="0ee4d-184">start: Ejecución de waagent como proceso en segundo plano</span><span class="sxs-lookup"><span data-stu-id="0ee4d-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="0ee4d-185">Configuración</span><span class="sxs-lookup"><span data-stu-id="0ee4d-185">Configuration</span></span>
<span data-ttu-id="0ee4d-186">Un archivo de configuración (/ etc/waagent.conf) controles Hola acciones de waagent.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-186">A configuration file (/etc/waagent.conf) controls hello actions of waagent.</span></span> <span data-ttu-id="0ee4d-187">Abajo se muestra un archivo de configuración de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0ee4d-187">A sample configuration file is shown below:</span></span>

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

<span data-ttu-id="0ee4d-188">Hola que distintas opciones de configuración se describen en detalle a continuación.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-188">hello various configuration options are described in detail below.</span></span> <span data-ttu-id="0ee4d-189">Las opciones de configuración son de tres tipos: Boolean, String o Integer.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="0ee4d-190">Opciones de configuración booleano de Hello pueden especificarse como "y" o "n".</span><span class="sxs-lookup"><span data-stu-id="0ee4d-190">hello Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="0ee4d-191">Hola palabra clave especial "" puede utilizarse para algunas entradas de configuración de tipo de cadena como se detalla a continuación.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-191">hello special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="0ee4d-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="0ee4d-193">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0ee4d-193">Type: Boolean</span></span>  
<span data-ttu-id="0ee4d-194">Predeterminado: y</span><span class="sxs-lookup"><span data-stu-id="0ee4d-194">Default: y</span></span>

<span data-ttu-id="0ee4d-195">Esto permite tooenable de usuario de Hola o deshabilitar Hola aprovisionamiento funcionalidad en el agente de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-195">This allows hello user tooenable or disable hello provisioning functionality in hello agent.</span></span> <span data-ttu-id="0ee4d-196">Los valores válidos son "y" o "n".</span><span class="sxs-lookup"><span data-stu-id="0ee4d-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="0ee4d-197">Si se deshabilita el aprovisionamiento, se conservan las claves de host y usuario SSH de imagen de Hola y se omite cualquier configuración especificada en hello API de aprovisionamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-197">If provisioning is disabled, SSH host and user keys in hello image are preserved and any configuration specified in hello Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="0ee4d-198">Hola `Provisioning.Enabled` demasiado "n" en las imágenes de nube de Ubuntu que utilizar init en la nube para el aprovisionamiento de valores predeterminados de parámetros.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-198">hello `Provisioning.Enabled` parameter defaults too"n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="0ee4d-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="0ee4d-200">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0ee4d-200">Type: Boolean</span></span>  
<span data-ttu-id="0ee4d-201">Predeterminado: n</span><span class="sxs-lookup"><span data-stu-id="0ee4d-201">Default: n</span></span>

<span data-ttu-id="0ee4d-202">Si se borra el conjunto, la contraseña de la raíz de hello en el archivo de instantáneas de hello/etcetera/durante Hola proceso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-202">If set, hello root password in hello /etc/shadow file is erased during hello provisioning process.</span></span>

<span data-ttu-id="0ee4d-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="0ee4d-204">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0ee4d-204">Type: Boolean</span></span>  
<span data-ttu-id="0ee4d-205">Predeterminado: y</span><span class="sxs-lookup"><span data-stu-id="0ee4d-205">Default: y</span></span>

<span data-ttu-id="0ee4d-206">Si se elimina el conjunto de todos los host pares de clave SSH (ecdsa, dsa y rsa) durante el proceso de/etc/ssh/de aprovisionamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during hello provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="0ee4d-207">Además, se genera un solo par de clave nuevo.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="0ee4d-208">tipo de cifrado de Hola de par de claves nuevo hello es configurable por hello Provisioning.SshHostKeyPairType entrada.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-208">hello encryption type for hello fresh key pair is configurable by hello Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="0ee4d-209">Tenga en cuenta que algunas distribuciones volverá a crear pares de claves de SSH para cualquier tipo de cifrado que falta cuando se reinicie el demonio de SSH de hello (por ejemplo, después de reiniciar el equipo).</span><span class="sxs-lookup"><span data-stu-id="0ee4d-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when hello SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="0ee4d-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="0ee4d-211">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0ee4d-211">Type: String</span></span>  
<span data-ttu-id="0ee4d-212">Predeterminado: rsa</span><span class="sxs-lookup"><span data-stu-id="0ee4d-212">Default: rsa</span></span>

<span data-ttu-id="0ee4d-213">Se puede establecer tipo de algoritmo de cifrado tooan que sea compatible con el demonio de SSH de hello en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-213">This can be set tooan encryption algorithm type that is supported by hello SSH daemon on hello virtual machine.</span></span> <span data-ttu-id="0ee4d-214">valores de Hello admitida generalmente son "rsa", "dsa" y "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="0ee4d-214">hello typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="0ee4d-215">Tenga en cuenta que "putty.exe" en Windows no admite "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="0ee4d-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="0ee4d-216">Por lo tanto, si piensa toouse putty.exe Windows tooconnect tooa implementación de Linux, use "rsa" o "dsa".</span><span class="sxs-lookup"><span data-stu-id="0ee4d-216">So, if you intend toouse putty.exe on Windows tooconnect tooa Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="0ee4d-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="0ee4d-218">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0ee4d-218">Type: Boolean</span></span>  
<span data-ttu-id="0ee4d-219">Predeterminado: y</span><span class="sxs-lookup"><span data-stu-id="0ee4d-219">Default: y</span></span>

<span data-ttu-id="0ee4d-220">Si establece, waagent supervisará máquina virtual de Linux Hola para cambios de nombre de host (como el devuelto por el comando de "nombre de host" hello) y actualizar automáticamente la configuración de red de hello en hello imagen tooreflect Hola de cambios.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-220">If set, waagent will monitor hello Linux virtual machine for hostname changes (as returned by hello "hostname" command) and automatically update hello networking configuration in hello image tooreflect hello change.</span></span> <span data-ttu-id="0ee4d-221">En nombre de criterio de hello toopush cambie toohello los servidores DNS, las redes se reiniciará en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-221">In order toopush hello name change toohello DNS servers, networking will be restarted in hello virtual machine.</span></span> <span data-ttu-id="0ee4d-222">Esta acción tiene como resultado una breve pérdida de la conectividad con Internet.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="0ee4d-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="0ee4d-224">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0ee4d-224">Type: Boolean</span></span>  
<span data-ttu-id="0ee4d-225">Predeterminado: n</span><span class="sxs-lookup"><span data-stu-id="0ee4d-225">Default: n</span></span>

<span data-ttu-id="0ee4d-226">Si se establece, waagent descodificará CustomData desde Base64.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="0ee4d-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="0ee4d-228">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0ee4d-228">Type: Boolean</span></span>  
<span data-ttu-id="0ee4d-229">Predeterminado: n</span><span class="sxs-lookup"><span data-stu-id="0ee4d-229">Default: n</span></span>

<span data-ttu-id="0ee4d-230">Si se establece, waagent ejecutará CustomData después del aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="0ee4d-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="0ee4d-232">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0ee4d-232">Type:String</span></span>  
<span data-ttu-id="0ee4d-233">Valor predeterminado: 6</span><span class="sxs-lookup"><span data-stu-id="0ee4d-233">Default:6</span></span>

<span data-ttu-id="0ee4d-234">Algoritmo usado por el cifrado al generar el hash de contraseña. </span><span class="sxs-lookup"><span data-stu-id="0ee4d-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="0ee4d-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="0ee4d-235">1 - MD5</span></span>  
 <span data-ttu-id="0ee4d-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="0ee4d-236">2a - Blowfish</span></span>  
 <span data-ttu-id="0ee4d-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="0ee4d-237">5 - SHA-256</span></span>  
 <span data-ttu-id="0ee4d-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="0ee4d-238">6 - SHA-512</span></span>  

<span data-ttu-id="0ee4d-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="0ee4d-240">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0ee4d-240">Type:String</span></span>  
<span data-ttu-id="0ee4d-241">Valor predeterminado: 10</span><span class="sxs-lookup"><span data-stu-id="0ee4d-241">Default:10</span></span>

<span data-ttu-id="0ee4d-242">Longitud del valor salt aleatorio usado al generar el hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="0ee4d-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="0ee4d-244">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0ee4d-244">Type: Boolean</span></span>  
<span data-ttu-id="0ee4d-245">Predeterminado: y</span><span class="sxs-lookup"><span data-stu-id="0ee4d-245">Default: y</span></span>

<span data-ttu-id="0ee4d-246">Si establece, Hola recursos formatea el disco proporcionado por la plataforma de Hola se se y monta waagent si el tipo de sistema de archivos de hello solicitado por el usuario de hello en "ResourceDisk.Filesystem" es un valor distinto de "ntfs".</span><span class="sxs-lookup"><span data-stu-id="0ee4d-246">If set, hello resource disk provided by hello platform will be formatted and mounted by waagent if hello filesystem type requested by hello user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="0ee4d-247">Una sola partición de tipo Linux (83) estará disponible en disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-247">A single partition of type Linux (83) will be made available on hello disk.</span></span> <span data-ttu-id="0ee4d-248">Tenga en cuenta que esta partición no se va a formatear si se puede montar correctamente.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="0ee4d-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="0ee4d-250">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0ee4d-250">Type: String</span></span>  
<span data-ttu-id="0ee4d-251">Predeterminado: ext4</span><span class="sxs-lookup"><span data-stu-id="0ee4d-251">Default: ext4</span></span>

<span data-ttu-id="0ee4d-252">Esto especifica el tipo de sistema de archivos de Hola de disco del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-252">This specifies hello filesystem type for hello resource disk.</span></span> <span data-ttu-id="0ee4d-253">Los valores admitidos varían según la distribución de Linux.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="0ee4d-254">Si la cadena hello es X, a continuación, mkfs. X debe estar presente en la imagen de Linux Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-254">If hello string is X, then mkfs.X should be present on hello Linux image.</span></span> <span data-ttu-id="0ee4d-255">Las imágenes de SLES 11 deben usar generalmente "ext3".</span><span class="sxs-lookup"><span data-stu-id="0ee4d-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="0ee4d-256">Las imágenes de FreeBSD deben usar "ufs2".</span><span class="sxs-lookup"><span data-stu-id="0ee4d-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="0ee4d-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="0ee4d-258">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0ee4d-258">Type: String</span></span>  
<span data-ttu-id="0ee4d-259">Valor predeterminado: /mnt/resource</span><span class="sxs-lookup"><span data-stu-id="0ee4d-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="0ee4d-260">Esto especifica la ruta de acceso de hello en el que está montado el disco del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-260">This specifies hello path at which hello resource disk is mounted.</span></span> <span data-ttu-id="0ee4d-261">Tenga en cuenta ese disco del recurso de hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-261">Note that hello resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span>

<span data-ttu-id="0ee4d-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="0ee4d-263">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0ee4d-263">Type: String</span></span>  
<span data-ttu-id="0ee4d-264">Valor predeterminado: None</span><span class="sxs-lookup"><span data-stu-id="0ee4d-264">Default: None</span></span>

<span data-ttu-id="0ee4d-265">Especifica opciones de montaje disco toobe pasado toohello mount -o comando.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-265">Specifies disk mount options toobe passed toohello mount -o command.</span></span> <span data-ttu-id="0ee4d-266">Esta es una lista de valores separados por comas, por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="0ee4d-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="0ee4d-267">'nodev,nosuid'.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-267">'nodev,nosuid'.</span></span> <span data-ttu-id="0ee4d-268">Consulte mount(8) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-268">See mount(8) for details.</span></span>

<span data-ttu-id="0ee4d-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="0ee4d-270">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0ee4d-270">Type: Boolean</span></span>  
<span data-ttu-id="0ee4d-271">Predeterminado: n</span><span class="sxs-lookup"><span data-stu-id="0ee4d-271">Default: n</span></span>

<span data-ttu-id="0ee4d-272">Si establece un archivo de intercambio (/ swapfile) se crea en el disco del recurso de Hola y agrega el espacio de intercambio de sistema toohello.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-272">If set, a swap file (/swapfile) is created on hello resource disk and added toohello system swap space.</span></span>

<span data-ttu-id="0ee4d-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="0ee4d-274">Tipo: Integer</span><span class="sxs-lookup"><span data-stu-id="0ee4d-274">Type: Integer</span></span>  
<span data-ttu-id="0ee4d-275">Valor predeterminado: 0</span><span class="sxs-lookup"><span data-stu-id="0ee4d-275">Default: 0</span></span>

<span data-ttu-id="0ee4d-276">tamaño de Hola Hola del archivo de intercambio en megabytes.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-276">hello size of hello swap file in megabytes.</span></span>

<span data-ttu-id="0ee4d-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="0ee4d-278">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0ee4d-278">Type: Boolean</span></span>  
<span data-ttu-id="0ee4d-279">Predeterminado: n</span><span class="sxs-lookup"><span data-stu-id="0ee4d-279">Default: n</span></span>

<span data-ttu-id="0ee4d-280">Si se establece, se aumenta el nivel de detalle del registro.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="0ee4d-281">Waagent registra too/var/log/waagent.log y aprovecha la funcionalidad toorotate registros de hello sistema logrotate.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-281">Waagent logs too/var/log/waagent.log and leverages hello system logrotate functionality toorotate logs.</span></span>

<span data-ttu-id="0ee4d-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="0ee4d-283">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0ee4d-283">Type: Boolean</span></span>  
<span data-ttu-id="0ee4d-284">Predeterminado: n</span><span class="sxs-lookup"><span data-stu-id="0ee4d-284">Default: n</span></span>

<span data-ttu-id="0ee4d-285">Si se establece, el agente de Hola se intentarán tooinstall y, a continuación, cargar un controlador de kernel RDMA que coincide con la versión de Hola de firmware Hola Hola subyacente de hardware.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-285">If set, hello agent will attempt tooinstall and then load an RDMA kernel driver that matches hello version of hello firmware on hello underlying hardware.</span></span>

<span data-ttu-id="0ee4d-286">**OS.RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="0ee4d-287">Tipo: Integer</span><span class="sxs-lookup"><span data-stu-id="0ee4d-287">Type: Integer</span></span>  
<span data-ttu-id="0ee4d-288">Valor predeterminado: 300</span><span class="sxs-lookup"><span data-stu-id="0ee4d-288">Default: 300</span></span>

<span data-ttu-id="0ee4d-289">Esto configura el tiempo de espera de hello SCSI en segundos en unidades de disco y los datos de hello SO.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-289">This configures hello SCSI timeout in seconds on hello OS disk and data drives.</span></span> <span data-ttu-id="0ee4d-290">Si no se establece, se usan los valores predeterminados de sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-290">If not set, hello system defaults are used.</span></span>

<span data-ttu-id="0ee4d-291">**OS.OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="0ee4d-292">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0ee4d-292">Type: String</span></span>  
<span data-ttu-id="0ee4d-293">Valor predeterminado: None</span><span class="sxs-lookup"><span data-stu-id="0ee4d-293">Default: None</span></span>

<span data-ttu-id="0ee4d-294">Esto puede resultar toospecify usa una ruta de acceso alternativa para hello openssl binario toouse para operaciones criptográficas.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-294">This can be used toospecify an alternate path for hello openssl binary toouse for cryptographic operations.</span></span>

<span data-ttu-id="0ee4d-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="0ee4d-296">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0ee4d-296">Type: String</span></span>  
<span data-ttu-id="0ee4d-297">Valor predeterminado: None</span><span class="sxs-lookup"><span data-stu-id="0ee4d-297">Default: None</span></span>

<span data-ttu-id="0ee4d-298">Si se establece, agente de hello utilizará este proxy server tooaccess Hola internet.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-298">If set, hello agent will use this proxy server tooaccess hello internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="0ee4d-299">Ubuntu Cloud Images</span><span class="sxs-lookup"><span data-stu-id="0ee4d-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="0ee4d-300">Tenga en cuenta que utilizar imágenes de nube Ubuntu [init de la nube](https://launchpad.net/ubuntu/+source/cloud-init) tooperform Hola de muchas tareas de configuración que en caso contrario, podrían ser administradas por agente Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform many configuration tasks that would otherwise be managed by hello Azure Linux Agent.</span></span>  <span data-ttu-id="0ee4d-301">Tenga en cuenta Hola siguientes diferencias:</span><span class="sxs-lookup"><span data-stu-id="0ee4d-301">Please note hello following differences:</span></span>

* <span data-ttu-id="0ee4d-302">**Provisioning.Enabled** demasiado "n" en las imágenes de nube de Ubuntu que usan tooperform init de la nube tareas de aprovisionamiento de los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="0ee4d-302">**Provisioning.Enabled** defaults too"n" on Ubuntu Cloud Images that use cloud-init tooperform provisioning tasks.</span></span>
* <span data-ttu-id="0ee4d-303">Hola parámetros de configuración siguientes no tiene ningún efecto en las imágenes de nube Ubuntu que usar en la nube init toomanage Hola recurso disco y espacio de intercambio:</span><span class="sxs-lookup"><span data-stu-id="0ee4d-303">hello following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init toomanage hello resource disk and swap space:</span></span>
  
  * <span data-ttu-id="0ee4d-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="0ee4d-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="0ee4d-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="0ee4d-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="0ee4d-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="0ee4d-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="0ee4d-309">Vea Hola después de punto de montaje de disco de recursos de recursos tooconfigure hello e intercambiar espacio en las imágenes de nube Ubuntu durante el aprovisionamiento:</span><span class="sxs-lookup"><span data-stu-id="0ee4d-309">Please see hello following resources tooconfigure hello resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="0ee4d-310">Ubuntu Wiki: Configure Swap Partitions (Configuración de particiones de intercambio)</span><span class="sxs-lookup"><span data-stu-id="0ee4d-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="0ee4d-311">Inyección de datos personalizados en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="0ee4d-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

