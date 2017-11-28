---
title: "aaaMove archivos tooand desde máquinas virtuales de Linux de Azure con SCP | Documentos de Microsoft"
description: Mover de forma segura los archivos tooand desde una VM de Linux en Azure mediante el SCP y un par de claves de SSH.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a><span data-ttu-id="d400d-103">Mover archivos tooand desde una VM de Linux mediante SCP</span><span class="sxs-lookup"><span data-stu-id="d400d-103">Move files tooand from a Linux VM using SCP</span></span>

<span data-ttu-id="d400d-104">Este artículo muestra cómo se toomove los archivos de la estación de trabajo de tooan VM de Linux de Azure, o de una VM de Linux de Azure hacia abajo de la estación de trabajo tooyour, mediante copia Secure (SCP).</span><span class="sxs-lookup"><span data-stu-id="d400d-104">This article shows how toomove files from your workstation up tooan Azure Linux VM, or from an Azure Linux VM down tooyour workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="d400d-105">El traslado de archivos entre su estación de trabajo y una máquina virtual Linux, de forma rápida y segura, es una parte fundamental de la administración de la infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="d400d-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="d400d-106">En este artículo, necesita una máquina virtual Linux implementada en Azure mediante [archivos de clave privada y pública de SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d400d-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d400d-107">También necesita un cliente SCP para el equipo local.</span><span class="sxs-lookup"><span data-stu-id="d400d-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="d400d-108">Es creado sobre SSH e incluido en el shell de Bash Hola predeterminado de la mayoría de los equipos Linux y Mac y algunos shells de Windows.</span><span class="sxs-lookup"><span data-stu-id="d400d-108">It is built on top of SSH and included in hello default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="d400d-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="d400d-109">Quick commands</span></span>

<span data-ttu-id="d400d-110">Copiar un archivo de seguridad toohello VM de Linux</span><span class="sxs-lookup"><span data-stu-id="d400d-110">Copy a file up toohello Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="d400d-111">Copiar un archivo hacia abajo de hello VM de Linux</span><span class="sxs-lookup"><span data-stu-id="d400d-111">Copy a file down from hello Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="d400d-112">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="d400d-112">Detailed walkthrough</span></span>

<span data-ttu-id="d400d-113">Como ejemplos, se mueve un archivo de configuración de Azure la VM de Linux tooa y tire hacia abajo de un directorio de archivos de registro, ambos utilizando claves SCP y SSH.</span><span class="sxs-lookup"><span data-stu-id="d400d-113">As examples, we move an Azure configuration file up tooa Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="d400d-114">Autenticación del par de claves de SSH</span><span class="sxs-lookup"><span data-stu-id="d400d-114">SSH key pair authentication</span></span>

<span data-ttu-id="d400d-115">SCP usa SSH para la capa de transporte de Hola.</span><span class="sxs-lookup"><span data-stu-id="d400d-115">SCP uses SSH for hello transport layer.</span></span> <span data-ttu-id="d400d-116">Identificadores de SSH Hola autenticación Hola host de destino, y los mueve archivo hello en un túnel cifrado que se proporcionan de forma predeterminada mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="d400d-116">SSH handles hello authentication on hello destination host, and it moves hello file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="d400d-117">Para la autenticación SSH, se pueden utilizar nombres de usuario y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="d400d-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="d400d-118">Sin embargo, se recomienda la autenticación clave pública y privada de SSH como procedimiento recomendado de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d400d-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="d400d-119">Una vez SSH autenticó conexión hello, SCP comienza, a continuación, copiar el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="d400d-119">Once SSH has authenticated hello connection, SCP then begins copying hello file.</span></span> <span data-ttu-id="d400d-120">Con un objeto configurado adecuadamente `~/.ssh/config` y claves públicas y privadas de SSH, conexión Hola SCP se pueden establecer simplemente utilizando un nombre de servidor (o dirección IP).</span><span class="sxs-lookup"><span data-stu-id="d400d-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, hello SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="d400d-121">Si solo tiene una clave SSH, SCP lo buscará en hello `~/.ssh/` directorio y lo utiliza de forma predeterminada toolog en toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d400d-121">If you only have one SSH key, SCP looks for it in hello `~/.ssh/` directory, and uses it by default toolog in toohello VM.</span></span>

<span data-ttu-id="d400d-122">Para más información acerca de cómo configurar las claves públicas y privadas de SSH y `~/.ssh/config`, consulte [Creación de claves SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d400d-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-tooa-linux-vm"></a><span data-ttu-id="d400d-123">SCP un tooa archivo VM de Linux</span><span class="sxs-lookup"><span data-stu-id="d400d-123">SCP a file tooa Linux VM</span></span>

<span data-ttu-id="d400d-124">Para el primer ejemplo de Hola, se copie un archivo de configuración de Azure seguridad tooa VM de Linux que es la automatización de toodeploy usado.</span><span class="sxs-lookup"><span data-stu-id="d400d-124">For hello first example, we copy an Azure configuration file up tooa Linux VM that is used toodeploy automation.</span></span> <span data-ttu-id="d400d-125">Como este archivo contiene las credenciales de la API de Azure, que incluyen secretos, la seguridad es importante.</span><span class="sxs-lookup"><span data-stu-id="d400d-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="d400d-126">túnel cifrado Hola proporcionada por SSH protege contenido Hola de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="d400d-126">hello encrypted tunnel provided by SSH protects hello contents of hello file.</span></span>

<span data-ttu-id="d400d-127">Hola siguientes comando copias Hola local *.azure/config* tooan VM de Azure con el FQDN de archivos *myserver.eastus.cloudapp.azure.com*. nombre de usuario de administrador de hello en hello Azure VM es *azureuser* .</span><span class="sxs-lookup"><span data-stu-id="d400d-127">hello following command copies hello local *.azure/config* file tooan Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. hello admin user name on hello Azure VM is *azureuser*.</span></span> <span data-ttu-id="d400d-128">archivo Hello es destino toohello */home/azureuser/* directory.</span><span class="sxs-lookup"><span data-stu-id="d400d-128">hello file is targeted toohello */home/azureuser/* directory.</span></span> <span data-ttu-id="d400d-129">Sustituya sus valores propios en este comando.</span><span class="sxs-lookup"><span data-stu-id="d400d-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="d400d-130">SCP de un directorio desde una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="d400d-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="d400d-131">En este ejemplo, se copie un directorio de archivos de registro de hello VM de Linux hacia abajo de la estación de trabajo de tooyour.</span><span class="sxs-lookup"><span data-stu-id="d400d-131">For this example, we copy a directory of log files from hello Linux VM down tooyour workstation.</span></span> <span data-ttu-id="d400d-132">Un archivo de registro puede contener datos confidenciales o secretos, o no.</span><span class="sxs-lookup"><span data-stu-id="d400d-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="d400d-133">Sin embargo, el uso de SCP garantiza Hola contenido de archivos de registro de hello está cifrado.</span><span class="sxs-lookup"><span data-stu-id="d400d-133">However, using SCP ensures hello contents of hello log files are encrypted.</span></span> <span data-ttu-id="d400d-134">Con archivos de SCP tootransfer hello es tooget de manera más fácil de Hola Hola directorio de registro y archivos de estación de trabajo de tooyour pero también segura.</span><span class="sxs-lookup"><span data-stu-id="d400d-134">Using SCP tootransfer hello files is hello easiest way tooget hello log directory and files down tooyour workstation while also being secure.</span></span>

<span data-ttu-id="d400d-135">Hello siguiente comando copia archivos en hello */principal/azureuser/logs/* directorio en el directorio de hello Azure VM toohello/tmp local:</span><span class="sxs-lookup"><span data-stu-id="d400d-135">hello following command copies files in hello */home/azureuser/logs/* directory on hello Azure VM toohello local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="d400d-136">Hola `-r` cli marca indica SCP toorecursively copiar Hola archivos y directorios del punto de hello del directorio Hola que aparece en el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="d400d-136">hello `-r` cli flag instructs SCP toorecursively copy hello files and directories from hello point of hello directory listed in hello command.</span></span>  <span data-ttu-id="d400d-137">También observe que Hola sintaxis de línea de comandos es similar tooa `cp` comando Copiar.</span><span class="sxs-lookup"><span data-stu-id="d400d-137">Also notice that hello command-line syntax is similar tooa `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d400d-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d400d-138">Next steps</span></span>

* [<span data-ttu-id="d400d-139">Administrar usuarios, SSH y verificación o reparación de discos sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión</span><span class="sxs-lookup"><span data-stu-id="d400d-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
