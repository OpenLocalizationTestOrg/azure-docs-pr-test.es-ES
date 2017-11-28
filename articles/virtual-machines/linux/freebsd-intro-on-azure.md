---
title: aaaIntroduction tooFreeBSD en Azure | Documentos de Microsoft
description: "Aprenda a utilizar máquinas virtuales de FreeBSD en Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a><span data-ttu-id="5d409-103">Introducción tooFreeBSD en Azure</span><span class="sxs-lookup"><span data-stu-id="5d409-103">Introduction tooFreeBSD on Azure</span></span>
<span data-ttu-id="5d409-104">Este tema proporciona una visión general de la ejecución de una máquina virtual de FreeBSD en Azure.</span><span class="sxs-lookup"><span data-stu-id="5d409-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="5d409-105">Información general</span><span class="sxs-lookup"><span data-stu-id="5d409-105">Overview</span></span>
<span data-ttu-id="5d409-106">FreeBSD a Microsoft Azure es que un sistema operativo de equipo avanzada usa toopower moderna servidores, escritorios y plataformas incrustadas.</span><span class="sxs-lookup"><span data-stu-id="5d409-106">FreeBSD for Microsoft Azure is an advanced computer operating system used toopower modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="5d409-107">Microsoft Corporation es ofrecer imágenes de FreeBSD en Azure con hello [agente de invitado de VM de Azure](https://github.com/Azure/WALinuxAgent/) configurado previamente.</span><span class="sxs-lookup"><span data-stu-id="5d409-107">Microsoft Corporation is making images of FreeBSD available on Azure with hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="5d409-108">Actualmente, hello versiones de FreeBSD siguientes se ofrecen como imágenes por Microsoft:</span><span class="sxs-lookup"><span data-stu-id="5d409-108">Currently, hello following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="5d409-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="5d409-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="5d409-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="5d409-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="5d409-111">agente de Hello es responsable de la comunicación entre Hola FreeBSD VM y Hola tejido de Azure para operaciones como el aprovisionamiento Hola VM en el primer uso (nombre de usuario, contraseña o clave SSH, nombre de host, etc.) y la funcionalidad habilitación selectiva extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5d409-111">hello agent is responsible for communication between hello FreeBSD VM and hello Azure fabric for operations such as provisioning hello VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="5d409-112">Que en versiones futuras de FreeBSD, estrategia de hello es toostay actual y que Hola versiones más recientes disponibles poco después de que se publican por equipo de ingeniería de hello FreeBSD versión.</span><span class="sxs-lookup"><span data-stu-id="5d409-112">As for future versions of FreeBSD, hello strategy is toostay current and make hello latest releases available shortly after they are published by hello FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="5d409-113">Implementación de una máquina virtual de FreeBSD</span><span class="sxs-lookup"><span data-stu-id="5d409-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="5d409-114">Implementar una máquina virtual de FreeBSD es un proceso sencillo con una imagen de hello Azure Marketplace de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="5d409-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from hello Azure Marketplace from hello Azure portal:</span></span>

- [<span data-ttu-id="5d409-115">10.3 de FreeBSD en hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5d409-115">FreeBSD 10.3 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="5d409-116">11.0 de FreeBSD en hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5d409-116">FreeBSD 11.0 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="5d409-117">Crear una máquina virtual de FreeBSD mediante la CLI de Azure 2.0 en FreeBSD</span><span class="sxs-lookup"><span data-stu-id="5d409-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="5d409-118">En primer lugar debe tooinstall [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) aunque el siguiente comando en un equipo de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="5d409-118">First you need tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="5d409-119">Si intensiva de errores no está instalado en el equipo de FreeBSD, ejecutar el siguiente comando antes de la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d409-119">If bash is not installed on your FreeBSD machine, run following command before hello installation.</span></span> 

```bash
sudo pkg install bash
```

<span data-ttu-id="5d409-120">Si python no está instalado en el equipo de FreeBSD, ejecute la siguiente comandos antes de la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d409-120">If python is not installed on your FreeBSD machine, run following commands before hello installation.</span></span> 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="5d409-121">Durante la instalación de hello, deberá `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="5d409-121">During hello installation, you are asked `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="5d409-122">Si la respuesta es `y` y escriba `/etc/rc.conf` como `a path tooan rc file tooupdate`, puede cumplir problema hello `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="5d409-122">If you answer `y` and enter `/etc/rc.conf` as `a path tooan rc file tooupdate`, you may meet hello problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="5d409-123">tooresolve este problema, debe conceder de usuario de toocurrent derecho de escritura de hello en archivo hello `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="5d409-123">tooresolve this problem, you should grant hello write right toocurrent user against hello file `etc/rc.conf`.</span></span>

<span data-ttu-id="5d409-124">Ahora puede iniciar sesión en Azure y crear su máquina virtual de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="5d409-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="5d409-125">A continuación se muestra un ejemplo toocreate una máquina virtual 11.0 de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="5d409-125">Below is an example toocreate a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="5d409-126">También puede agregar el parámetro hello `--public-ip-address-dns-name` con un nombre DNS único global para una dirección IP pública recién creado.</span><span class="sxs-lookup"><span data-stu-id="5d409-126">You can also add hello parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="5d409-127">A continuación, puede iniciar sesión en tooyour FreeBSD VM a través de la dirección ip de Hola que imprime en la salida de hello de por encima de la implementación.</span><span class="sxs-lookup"><span data-stu-id="5d409-127">Then you can log in tooyour FreeBSD VM through hello ip address that printed in hello output of above deployment.</span></span> 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="5d409-128">Extensiones de VM para FreeBSD</span><span class="sxs-lookup"><span data-stu-id="5d409-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="5d409-129">A continuación se muestran las extensiones de VM compatibles en FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="5d409-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="5d409-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="5d409-130">VMAccess</span></span>
<span data-ttu-id="5d409-131">Hola [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extensión puede:</span><span class="sxs-lookup"><span data-stu-id="5d409-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="5d409-132">Hola restablecimiento de contraseñas de usuario de hello original sudo.</span><span class="sxs-lookup"><span data-stu-id="5d409-132">Reset hello password of hello original sudo user.</span></span>
* <span data-ttu-id="5d409-133">Crear un nuevo usuario de sudo con contraseña Hola especificada.</span><span class="sxs-lookup"><span data-stu-id="5d409-133">Create a new sudo user with hello password specified.</span></span>
* <span data-ttu-id="5d409-134">Establezca la clave de host público Hola con clave de hello dada.</span><span class="sxs-lookup"><span data-stu-id="5d409-134">Set hello public host key with hello key given.</span></span>
* <span data-ttu-id="5d409-135">Restablecer la clave de host público de hello proporcionada durante la máquina virtual si no se proporcionó una clave de host de Hola de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="5d409-135">Reset hello public host key provided during VM provisioning if hello host key is not provided.</span></span>
* <span data-ttu-id="5d409-136">Abra el puerto SSH de hello (22) y restaurar Hola sshd_config si reset_ssh se establece tootrue.</span><span class="sxs-lookup"><span data-stu-id="5d409-136">Open hello SSH port (22) and restore hello sshd_config if reset_ssh is set tootrue.</span></span>
* <span data-ttu-id="5d409-137">Quitar usuario existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d409-137">Remove hello existing user.</span></span>
* <span data-ttu-id="5d409-138">Comprobar discos.</span><span class="sxs-lookup"><span data-stu-id="5d409-138">Check disks.</span></span>
* <span data-ttu-id="5d409-139">Reparar un disco agregado.</span><span class="sxs-lookup"><span data-stu-id="5d409-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="5d409-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="5d409-140">CustomScript</span></span>
<span data-ttu-id="5d409-141">Hola [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extensión puede:</span><span class="sxs-lookup"><span data-stu-id="5d409-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="5d409-142">Si se proporciona, descargar scripts de saludo personalizado desde el almacenamiento de Azure o almacenamiento público externo (por ejemplo, GitHub).</span><span class="sxs-lookup"><span data-stu-id="5d409-142">If provided, download hello customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="5d409-143">Ejecutar script de punto de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d409-143">Run hello entry point script.</span></span>
* <span data-ttu-id="5d409-144">Admitir comandos en línea.</span><span class="sxs-lookup"><span data-stu-id="5d409-144">Support inline commands.</span></span>
* <span data-ttu-id="5d409-145">Convertir la nueva línea de estilo de Windows en scripts de Shell y Python automáticamente.</span><span class="sxs-lookup"><span data-stu-id="5d409-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="5d409-146">Quitar la marca BOM en scripts de Shell y Python automáticamente.</span><span class="sxs-lookup"><span data-stu-id="5d409-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="5d409-147">Proteger la información confidencial en CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="5d409-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="5d409-148">Por el momento, la máquina virtual de FreeBSD solo es compatible con la versión 1.x de CustomScript.</span><span class="sxs-lookup"><span data-stu-id="5d409-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="5d409-149">Autenticación: nombres de usuario, contraseñas y claves SSH</span><span class="sxs-lookup"><span data-stu-id="5d409-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="5d409-150">Al crear una máquina virtual de FreeBSD utilizando Hola portal de Azure, debe proporcionar un nombre de usuario, la contraseña o la clave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="5d409-150">When you're creating a FreeBSD virtual machine by using hello Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="5d409-151">Nombres de usuario para la implementación de una máquina virtual de FreeBSD en Azure no deben coincidir con los nombres de cuentas del sistema (UID < 100) ya está presente en la máquina virtual de hello (por ejemplo, "raíz").</span><span class="sxs-lookup"><span data-stu-id="5d409-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in hello virtual machine ("root", for example).</span></span>
<span data-ttu-id="5d409-152">Actualmente, se admite solo Hola RSA la clave SSH.</span><span class="sxs-lookup"><span data-stu-id="5d409-152">Currently, only hello RSA SSH key is supported.</span></span> <span data-ttu-id="5d409-153">Una clave SSH multilínea debe comenzar con `---- BEGIN SSH2 PUBLIC KEY ----` y terminar con `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="5d409-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="5d409-154">Obtención de privilegios de superusuario</span><span class="sxs-lookup"><span data-stu-id="5d409-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="5d409-155">cuenta de usuario de Hola que se especifica durante la implementación de la instancia de máquina virtual en Azure es una cuenta con privilegios.</span><span class="sxs-lookup"><span data-stu-id="5d409-155">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="5d409-156">paquete de sudo Hello se instaló una en hello publicado FreeBSD imagen.</span><span class="sxs-lookup"><span data-stu-id="5d409-156">hello package of sudo was installed in hello published FreeBSD image.</span></span>
<span data-ttu-id="5d409-157">Después de que inició sesión a través de esta cuenta de usuario, puede ejecutar comandos como raíz mediante la sintaxis de comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d409-157">After you're logged in through this user account, you can run commands as root by using hello command syntax.</span></span>

```
$ sudo <COMMAND>
```

<span data-ttu-id="5d409-158">También puede obtener un shell root con `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="5d409-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="5d409-159">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="5d409-159">Known issues</span></span>
<span data-ttu-id="5d409-160">Hola [agente de invitado de VM de Azure](https://github.com/Azure/WALinuxAgent/) versión 2.2.2 tiene un [problema conocido] (https://github.com/Azure/WALinuxAgent/pull/517) que produce error de aprovisionamiento de Hola para FreeBSD VM en Azure.</span><span class="sxs-lookup"><span data-stu-id="5d409-160">hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes hello provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="5d409-161">Hello corrección se capturaba [agente de invitado de VM de Azure](https://github.com/Azure/WALinuxAgent/) versión 2.2.3 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="5d409-161">hello fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5d409-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5d409-162">Next steps</span></span>
* <span data-ttu-id="5d409-163">Vaya demasiado[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate una VM FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="5d409-163">Go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate a FreeBSD VM.</span></span>
* <span data-ttu-id="5d409-164">Si desea toobring su propio tooAzure FreeBSD, consultar demasiado[crear y cargar un VHD FreeBSD tooAzure](classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="5d409-164">If you want toobring your own FreeBSD tooAzure, refer too[Create and upload a FreeBSD VHD tooAzure](classic/freebsd-create-upload-vhd.md).</span></span>
