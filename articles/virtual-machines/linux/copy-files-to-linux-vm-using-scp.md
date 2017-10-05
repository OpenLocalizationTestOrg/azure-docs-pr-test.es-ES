---
title: "Traslado de archivos a máquinas virtuales Linux de Azure o desde ella mediante SCP | Microsoft Docs"
description: "Traslado seguro de archivos a la máquina virtual Linux de Azure o desde ella mediante SCP y un par de claves de SSH."
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
ms.openlocfilehash: 736f7c11ec3de04f1ad52ee29d0a4c952c9b0545
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="move-files-to-and-from-a-linux-vm-using-scp"></a><span data-ttu-id="cb285-103">Traslado de archivos a una máquina virtual Linux o desde ella mediante SCP</span><span class="sxs-lookup"><span data-stu-id="cb285-103">Move files to and from a Linux VM using SCP</span></span>

<span data-ttu-id="cb285-104">Este artículo muestra cómo trasladar archivos desde su estación de trabajo hasta una máquina virtual Linux de Azure, o desde una máquina virtual Linux de Azure hasta la estación de trabajo, mediante Secure Copy (SCP).</span><span class="sxs-lookup"><span data-stu-id="cb285-104">This article shows how to move files from your workstation up to an Azure Linux VM, or from an Azure Linux VM down to your workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="cb285-105">El traslado de archivos entre su estación de trabajo y una máquina virtual Linux, de forma rápida y segura, es una parte fundamental de la administración de la infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="cb285-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="cb285-106">En este artículo, necesita una máquina virtual Linux implementada en Azure mediante [archivos de clave privada y pública de SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cb285-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="cb285-107">También necesita un cliente SCP para el equipo local.</span><span class="sxs-lookup"><span data-stu-id="cb285-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="cb285-108">Está compilado sobre SSH y se incluye en el shell de Bash predeterminado de la mayoría de los equipos Linux y Mac y de algunos shells de Windows.</span><span class="sxs-lookup"><span data-stu-id="cb285-108">It is built on top of SSH and included in the default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="cb285-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="cb285-109">Quick commands</span></span>

<span data-ttu-id="cb285-110">Copia de un archivo hacia arriba de la máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="cb285-110">Copy a file up to the Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="cb285-111">Copia de un archivo hacia abajo de la máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="cb285-111">Copy a file down from the Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="cb285-112">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="cb285-112">Detailed walkthrough</span></span>

<span data-ttu-id="cb285-113">Como ejemplos, estamos trasladando un archivo de configuración de Azure a una máquina virtual Linux y extrayendo un directorio de archivos de registro, ambos con claves SCP y SSH.</span><span class="sxs-lookup"><span data-stu-id="cb285-113">As examples, we move an Azure configuration file up to a Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="cb285-114">Autenticación del par de claves de SSH</span><span class="sxs-lookup"><span data-stu-id="cb285-114">SSH key pair authentication</span></span>

<span data-ttu-id="cb285-115">SCP usa SSH para el nivel de transporte.</span><span class="sxs-lookup"><span data-stu-id="cb285-115">SCP uses SSH for the transport layer.</span></span> <span data-ttu-id="cb285-116">SSH administra la autenticación en el host de destino y traslada el archivo en un túnel cifrado proporcionado de forma predeterminada con SSH.</span><span class="sxs-lookup"><span data-stu-id="cb285-116">SSH handles the authentication on the destination host, and it moves the file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="cb285-117">Para la autenticación SSH, se pueden utilizar nombres de usuario y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="cb285-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="cb285-118">Sin embargo, se recomienda la autenticación clave pública y privada de SSH como procedimiento recomendado de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb285-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="cb285-119">Una vez que SSH ha autenticado la conexión, SCP comienza a copiar el archivo.</span><span class="sxs-lookup"><span data-stu-id="cb285-119">Once SSH has authenticated the connection, SCP then begins copying the file.</span></span> <span data-ttu-id="cb285-120">Con claves públicas y privadas de SSH y un `~/.ssh/config` configurado adecuadamente, la conexión de SCP puede establecerse usando únicamente un nombre del servidor (o dirección IP).</span><span class="sxs-lookup"><span data-stu-id="cb285-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, the SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="cb285-121">Si solo tiene una clave SSH, SCP la busca en el directorio `~/.ssh/` y la usa de forma predeterminada para iniciar sesión en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cb285-121">If you only have one SSH key, SCP looks for it in the `~/.ssh/` directory, and uses it by default to log in to the VM.</span></span>

<span data-ttu-id="cb285-122">Para más información acerca de cómo configurar las claves públicas y privadas de SSH y `~/.ssh/config`, consulte [Creación de claves SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cb285-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-to-a-linux-vm"></a><span data-ttu-id="cb285-123">SCP en un archivo para una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="cb285-123">SCP a file to a Linux VM</span></span>

<span data-ttu-id="cb285-124">Para el primer ejemplo, copiamos un archivo de configuración de Azure en una máquina virtual Linux que se usa para implementar la automatización.</span><span class="sxs-lookup"><span data-stu-id="cb285-124">For the first example, we copy an Azure configuration file up to a Linux VM that is used to deploy automation.</span></span> <span data-ttu-id="cb285-125">Como este archivo contiene las credenciales de la API de Azure, que incluyen secretos, la seguridad es importante.</span><span class="sxs-lookup"><span data-stu-id="cb285-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="cb285-126">El túnel cifrado proporcionado por SSH protege el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="cb285-126">The encrypted tunnel provided by SSH protects the contents of the file.</span></span>

<span data-ttu-id="cb285-127">El comando siguiente copia el archivo *.azure/config* local a una máquina virtual de Azure con el FQDN de *myserver.eastus.cloudapp.azure.com*. El nombre de usuario administrador en la máquina virtual de Azure es *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="cb285-127">The following command copies the local *.azure/config* file to an Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. The admin user name on the Azure VM is *azureuser*.</span></span> <span data-ttu-id="cb285-128">El archivo está dirigido al directorio */home/azureuser/*.</span><span class="sxs-lookup"><span data-stu-id="cb285-128">The file is targeted to the */home/azureuser/* directory.</span></span> <span data-ttu-id="cb285-129">Sustituya sus valores propios en este comando.</span><span class="sxs-lookup"><span data-stu-id="cb285-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="cb285-130">SCP de un directorio desde una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="cb285-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="cb285-131">En este ejemplo, copiamos un directorio de archivos de registro de la máquina virtual Linux hasta la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cb285-131">For this example, we copy a directory of log files from the Linux VM down to your workstation.</span></span> <span data-ttu-id="cb285-132">Un archivo de registro puede contener datos confidenciales o secretos, o no.</span><span class="sxs-lookup"><span data-stu-id="cb285-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="cb285-133">Sin embargo, mediante SCP garantiza que el contenido de los archivos de registro está cifrado.</span><span class="sxs-lookup"><span data-stu-id="cb285-133">However, using SCP ensures the contents of the log files are encrypted.</span></span> <span data-ttu-id="cb285-134">El uso de SCP para transferir los archivos es la manera más fácil de obtener el directorio de registro y archivos hacia abajo en la estación de trabajo mientras se mantiene la seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb285-134">Using SCP to transfer the files is the easiest way to get the log directory and files down to your workstation while also being secure.</span></span>

<span data-ttu-id="cb285-135">El siguiente comando copia los archivos en el directorio */home/azureuser/logs/* en la máquina virtual de Azure al directorio /tmp local:</span><span class="sxs-lookup"><span data-stu-id="cb285-135">The following command copies files in the */home/azureuser/logs/* directory on the Azure VM to the local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="cb285-136">La marca de la CLI de `-r` indica a SCP que copie de forma recursiva los archivos y directorios desde el punto del directorio enumerado en el comando.</span><span class="sxs-lookup"><span data-stu-id="cb285-136">The `-r` cli flag instructs SCP to recursively copy the files and directories from the point of the directory listed in the command.</span></span>  <span data-ttu-id="cb285-137">Tenga también en cuenta que la sintaxis de línea de comandos es similar a un comando de copia de `cp`.</span><span class="sxs-lookup"><span data-stu-id="cb285-137">Also notice that the command-line syntax is similar to a `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb285-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb285-138">Next steps</span></span>

* [<span data-ttu-id="cb285-139">Administración de usuarios, SSH y comprobar o reparar discos en máquinas virtuales de Linux de Azure con la extensión VMAccess</span><span class="sxs-lookup"><span data-stu-id="cb285-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)