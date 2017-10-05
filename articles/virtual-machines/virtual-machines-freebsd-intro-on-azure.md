---
title: "Introducción a FreeBSD en Azure | Microsoft Docs"
description: "Aprenda a utilizar máquinas virtuales de FreeBSD en Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: d0fc5de34f7d9e5a607495eb97d9e35dc9eb21f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-freebsd-on-azure"></a><span data-ttu-id="e6fae-103">Introducción a FreeBSD en Azure</span><span class="sxs-lookup"><span data-stu-id="e6fae-103">Introduction to FreeBSD on Azure</span></span>
<span data-ttu-id="e6fae-104">Este tema proporciona una visión general de la ejecución de una máquina virtual de FreeBSD en Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fae-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="e6fae-105">Información general</span><span class="sxs-lookup"><span data-stu-id="e6fae-105">Overview</span></span>
<span data-ttu-id="e6fae-106">FreeBSD para Microsoft Azure es un sistema operativo avanzado que se utiliza para servidores modernos, equipos de escritorio y plataformas insertadas.</span><span class="sxs-lookup"><span data-stu-id="e6fae-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="e6fae-107">Microsoft Corporation ofrece imágenes de FreeBSD en Azure con el [agente de invitado de VM de Azure](https://github.com/Azure/WALinuxAgent/) preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="e6fae-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="e6fae-108">Actualmente, Microsoft ofrece las siguientes versiones de FreeBSD como imágenes:</span><span class="sxs-lookup"><span data-stu-id="e6fae-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="e6fae-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="e6fae-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="e6fae-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="e6fae-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="e6fae-111">El agente es responsable de la comunicación entre la VM de FreeBSD y el tejido de Azure para operaciones como el aprovisionamiento de la VM cuando se usa por primera vez (nombre de usuario, contraseña o clave SSH, nombre de host, etc.) y la habilitación de la funcionalidad para extensiones de VM selectivas.</span><span class="sxs-lookup"><span data-stu-id="e6fae-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="e6fae-112">En lo que respecta a futuras versiones de FreeBSD, la estrategia es mantenerse al día y que las últimas versiones estén disponibles al poco tiempo de que el equipo de ingeniería de lanzamientos de FreeBSD las publique.</span><span class="sxs-lookup"><span data-stu-id="e6fae-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="e6fae-113">Implementación de una máquina virtual de FreeBSD</span><span class="sxs-lookup"><span data-stu-id="e6fae-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="e6fae-114">La implementación de una máquina virtual de FreeBSD es un proceso sencillo cuando se usa una imagen de Azure Marketplace desde Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="e6fae-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span></span>

- [<span data-ttu-id="e6fae-115">FreeBSD 10.3 en Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e6fae-115">FreeBSD 10.3 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="e6fae-116">FreeBSD 11.0 en Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e6fae-116">FreeBSD 11.0 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="e6fae-117">Crear una máquina virtual de FreeBSD mediante la CLI de Azure 2.0 en FreeBSD</span><span class="sxs-lookup"><span data-stu-id="e6fae-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="e6fae-118">Primero necesita instalar la [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) mediante el siguiente comando en una máquina de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="e6fae-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="e6fae-119">Si Bash no está instalado en su máquina de FreeBSD, ejecute el siguiente comando antes de la instalación.</span><span class="sxs-lookup"><span data-stu-id="e6fae-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="e6fae-120">Si Python no está instalado en su máquina de FreeBSD, ejecute los siguientes comandos antes de la instalación.</span><span class="sxs-lookup"><span data-stu-id="e6fae-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="e6fae-121">Durante la instalación, se le preguntará lo siguiente: `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="e6fae-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="e6fae-122">Si su respuesta es `y` y escribe `/etc/rc.conf` como `a path to an rc file to update`, puede encontrarse el problema `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="e6fae-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="e6fae-123">Para resolverlo, debe conceder el derecho de escritura al usuario actual en el archivo `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="e6fae-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span></span>

<span data-ttu-id="e6fae-124">Ahora puede iniciar sesión en Azure y crear su máquina virtual de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="e6fae-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="e6fae-125">A continuación se muestra un ejemplo para crear una máquina virtual de FreeBSD 11.0.</span><span class="sxs-lookup"><span data-stu-id="e6fae-125">Below is an example to create a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="e6fae-126">También puede agregar el parámetro `--public-ip-address-dns-name` con un nombre DNS único globalmente para una IP pública recién creada.</span><span class="sxs-lookup"><span data-stu-id="e6fae-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="e6fae-127">Después, puede iniciar sesión en su máquina virtual de FreeBSD mediante la dirección IP que se imprime en la salida de la implementación anterior.</span><span class="sxs-lookup"><span data-stu-id="e6fae-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="e6fae-128">Extensiones de VM para FreeBSD</span><span class="sxs-lookup"><span data-stu-id="e6fae-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="e6fae-129">A continuación se muestran las extensiones de VM compatibles en FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="e6fae-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="e6fae-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="e6fae-130">VMAccess</span></span>
<span data-ttu-id="e6fae-131">La extensión [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) puede:</span><span class="sxs-lookup"><span data-stu-id="e6fae-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="e6fae-132">Restablecer la contraseña del usuario de sudo original.</span><span class="sxs-lookup"><span data-stu-id="e6fae-132">Reset the password of the original sudo user.</span></span>
* <span data-ttu-id="e6fae-133">Crear un nuevo usuario de sudo con la contraseña especificada.</span><span class="sxs-lookup"><span data-stu-id="e6fae-133">Create a new sudo user with the password specified.</span></span>
* <span data-ttu-id="e6fae-134">Establecer la clave pública del host con la clave dada.</span><span class="sxs-lookup"><span data-stu-id="e6fae-134">Set the public host key with the key given.</span></span>
* <span data-ttu-id="e6fae-135">Restablecer la clave pública del host proporcionada durante el aprovisionamiento de VM si no se proporciona clave de host.</span><span class="sxs-lookup"><span data-stu-id="e6fae-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span></span>
* <span data-ttu-id="e6fae-136">Abrir el puerto (22) SSH y restaurar sshd_config si reset_ssh está establecido en true.</span><span class="sxs-lookup"><span data-stu-id="e6fae-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span></span>
* <span data-ttu-id="e6fae-137">Quitar el usuario existente.</span><span class="sxs-lookup"><span data-stu-id="e6fae-137">Remove the existing user.</span></span>
* <span data-ttu-id="e6fae-138">Comprobar discos.</span><span class="sxs-lookup"><span data-stu-id="e6fae-138">Check disks.</span></span>
* <span data-ttu-id="e6fae-139">Reparar un disco agregado.</span><span class="sxs-lookup"><span data-stu-id="e6fae-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="e6fae-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="e6fae-140">CustomScript</span></span>
<span data-ttu-id="e6fae-141">La extensión [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) puede:</span><span class="sxs-lookup"><span data-stu-id="e6fae-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="e6fae-142">Si se proporciona, descargar los scripts desde Azure Storage o desde un almacenamiento público externo (por ejemplo, GitHub).</span><span class="sxs-lookup"><span data-stu-id="e6fae-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="e6fae-143">Ejecutar el script de punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="e6fae-143">Run the entry point script.</span></span>
* <span data-ttu-id="e6fae-144">Admitir comandos en línea.</span><span class="sxs-lookup"><span data-stu-id="e6fae-144">Support inline commands.</span></span>
* <span data-ttu-id="e6fae-145">Convertir la nueva línea de estilo de Windows en scripts de Shell y Python automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e6fae-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="e6fae-146">Quitar la marca BOM en scripts de Shell y Python automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e6fae-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="e6fae-147">Proteger la información confidencial en CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="e6fae-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="e6fae-148">Por el momento, la máquina virtual de FreeBSD solo es compatible con la versión 1.x de CustomScript.</span><span class="sxs-lookup"><span data-stu-id="e6fae-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="e6fae-149">Autenticación: nombres de usuario, contraseñas y claves SSH</span><span class="sxs-lookup"><span data-stu-id="e6fae-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="e6fae-150">Al crear una máquina virtual FreeBSD con el Azure Portal, debe proporcionar un nombre de usuario, una contraseña o una clave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="e6fae-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="e6fae-151">Los nombres de usuario para implementar una máquina virtual de FreeBSD en Azure no deben coincidir con los nombres de cuentas del sistema (UID < 100) ya presentes en la máquina virtual ("raíz", por ejemplo).</span><span class="sxs-lookup"><span data-stu-id="e6fae-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span></span>
<span data-ttu-id="e6fae-152">Actualmente, solo se admite la clave RSA SSH.</span><span class="sxs-lookup"><span data-stu-id="e6fae-152">Currently, only the RSA SSH key is supported.</span></span> <span data-ttu-id="e6fae-153">Una clave SSH multilínea debe comenzar con `---- BEGIN SSH2 PUBLIC KEY ----` y terminar con `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="e6fae-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="e6fae-154">Obtención de privilegios de superusuario</span><span class="sxs-lookup"><span data-stu-id="e6fae-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="e6fae-155">La cuenta de usuario especificada durante la implementación de la instancia de máquina virtual en Azure es una cuenta con privilegios.</span><span class="sxs-lookup"><span data-stu-id="e6fae-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="e6fae-156">Se instaló el paquete de sudo en la imagen de FreeBSD publicada.</span><span class="sxs-lookup"><span data-stu-id="e6fae-156">The package of sudo was installed in the published FreeBSD image.</span></span>
<span data-ttu-id="e6fae-157">Después de iniciar sesión con esta cuenta de usuario, puede ejecutar comandos como root con usando la sintaxis de comando.</span><span class="sxs-lookup"><span data-stu-id="e6fae-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="e6fae-158">También puede obtener un shell root con `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="e6fae-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="e6fae-159">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="e6fae-159">Known issues</span></span>
<span data-ttu-id="e6fae-160">La versión 2.2.2 de [Agente invitado de máquina virtual de Azure](https://github.com/Azure/WALinuxAgent/) tiene un [problema conocido] (https://github.com/Azure/WALinuxAgent/pull/517) que provoca un error de aprovisionamiento de la máquina virtual de FreeBSD en Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fae-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="e6fae-161">La corrección se incluirá en la versión 2.2.3 de [Agente invitado de máquina virtual de Azure](https://github.com/Azure/WALinuxAgent/) y posteriores.</span><span class="sxs-lookup"><span data-stu-id="e6fae-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e6fae-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e6fae-162">Next steps</span></span>
* <span data-ttu-id="e6fae-163">Acuda a [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) para crear una máquina virtual de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="e6fae-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span></span>
* <span data-ttu-id="e6fae-164">Si desea incorporar su propio FreeBSD a Azure, consulte [Creación y carga de un VHD de FreeBSD en Azure](linux/classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="e6fae-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](linux/classic/freebsd-create-upload-vhd.md).</span></span>
