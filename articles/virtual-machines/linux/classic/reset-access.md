---
title: "Restablecimiento de la contraseña de máquina virtual Linux y clave SSH desde la CLI | Microsoft Docs"
description: "Uso de la extensión VMAccess desde la interfaz de la línea de comandos de Azure (CLI) para restablecer una contraseña de VM de Linux o clave SSH, corregir la configuración de SSH y comprobar la coherencia de disco"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 74765877e7836d6878284b350a25d8355dc83d7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-a-linux-vm-password-or-ssh-key-fix-the-ssh-configuration-and-check-disk-consistency-using-the-vmaccess-extension"></a><span data-ttu-id="028e7-103">Cómo restablecer una contraseña de máquina virtual Linux o clave SSH, corregir la configuración de SSH y comprobar la coherencia de disco con la extensión VMAccess</span><span class="sxs-lookup"><span data-stu-id="028e7-103">How to reset a Linux VM password or SSH key, fix the SSH configuration, and check disk consistency using the VMAccess extension</span></span>
<span data-ttu-id="028e7-104">Si no puede conectarse a una máquina virtual Linux porque olvidó la contraseña, la clave de Shell seguro (SSH) es incorrecta o hay un problema con la configuración de SSH, use la extensión VMAccessForLinux con la CLI de Azure para restablecer la contraseña o la clave SSH, corregir la configuración de SSH y comprobar la coherencia de los discos.</span><span class="sxs-lookup"><span data-stu-id="028e7-104">If you can't connect to a Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with the SSH configuration, use the VMAccessForLinux extension with the Azure CLI to reset the password or SSH key, fix the SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="028e7-105">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="028e7-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="028e7-106">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="028e7-106">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="028e7-107">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="028e7-107">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="028e7-108">Obtenga información sobre cómo [realizar estos pasos con el modelo de Resource Manager](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="028e7-108">Learn how to [perform these steps using the Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="028e7-109">Con la CLI de Azure, puede usar el comando **azure vm extension set** desde su interfaz de línea de comandos (símbolo del sistema Command, Terminal y Bash) para acceder a los comandos.</span><span class="sxs-lookup"><span data-stu-id="028e7-109">With the Azure CLI, you use the **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) to access commands.</span></span> <span data-ttu-id="028e7-110">Ejecute el comando **azure help vm extension set** para obtener más información sobre el uso de la extensión.</span><span class="sxs-lookup"><span data-stu-id="028e7-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="028e7-111">Con la CLI de Azure, puede realizar las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="028e7-111">With the Azure CLI, you can do the following tasks:</span></span>

* [<span data-ttu-id="028e7-112">Restablecer la contraseña</span><span class="sxs-lookup"><span data-stu-id="028e7-112">Reset the password</span></span>](#pwresetcli)
* [<span data-ttu-id="028e7-113">Restablecer la clave SSH</span><span class="sxs-lookup"><span data-stu-id="028e7-113">Reset the SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="028e7-114">Restablecer la contraseña y la clave SSH</span><span class="sxs-lookup"><span data-stu-id="028e7-114">Reset the password and the SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="028e7-115">Crear una nueva cuenta de usuario de sudo</span><span class="sxs-lookup"><span data-stu-id="028e7-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="028e7-116">Restablecer la configuración de SSH</span><span class="sxs-lookup"><span data-stu-id="028e7-116">Reset the SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="028e7-117">Eliminar un usuario</span><span class="sxs-lookup"><span data-stu-id="028e7-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="028e7-118">Mostrar el estado de la extensión VMAccess</span><span class="sxs-lookup"><span data-stu-id="028e7-118">Display the status of the VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="028e7-119">Comprobar la coherencia de los discos agregados</span><span class="sxs-lookup"><span data-stu-id="028e7-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="028e7-120">Reparar los discos agregados a la VM de Linux</span><span class="sxs-lookup"><span data-stu-id="028e7-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="028e7-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="028e7-121">Prerequisites</span></span>
<span data-ttu-id="028e7-122">Deberá hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="028e7-122">You will need to do the following:</span></span>

* <span data-ttu-id="028e7-123">También necesitará [instalar la CLI de Azure](../../../cli-install-nodejs.md) y [conectarse a su suscripción](../../../xplat-cli-connect.md) para usar recursos de Azure asociados a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="028e7-123">You will need to [install the Azure CLI](../../../cli-install-nodejs.md) and [connect to your subscription](../../../xplat-cli-connect.md) to use Azure resources associated with your account.</span></span>
* <span data-ttu-id="028e7-124">Establezca el modo correcto para el modelo de implementación clásica escribiendo lo siguiente en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="028e7-124">Set the correct mode for the classic deployment model by typing the following at the command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="028e7-125">Obtenga una nueva contraseña o un conjunto de claves SSH, si desea restablecer cualquiera de ellos.</span><span class="sxs-lookup"><span data-stu-id="028e7-125">Have a new password or set of SSH keys, if you want to reset either one.</span></span> <span data-ttu-id="028e7-126">No los necesita si desea restablecer la configuración de SSH.</span><span class="sxs-lookup"><span data-stu-id="028e7-126">You don't need these if you want to reset the SSH configuration.</span></span>

## <span data-ttu-id="028e7-127"><a name="pwresetcli"></a>Restablecer la contraseña</span><span class="sxs-lookup"><span data-stu-id="028e7-127"><a name="pwresetcli"></a>Reset the password</span></span>
1. <span data-ttu-id="028e7-128">Cree un archivo en el equipo local denominado "PrivateConf.json" con estas líneas.</span><span class="sxs-lookup"><span data-stu-id="028e7-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="028e7-129">Reemplace **myUserName** y **myP@ssW0rd** por su propio nombre de usuario y una contraseña y establezca su propia fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="028e7-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="028e7-130">Ejecute este comando y sustituya el nombre de la máquina virtual en **myVM**.</span><span class="sxs-lookup"><span data-stu-id="028e7-130">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="028e7-131"><a name="sshkeyresetcli"></a>Restablecer la clave SSH</span><span class="sxs-lookup"><span data-stu-id="028e7-131"><a name="sshkeyresetcli"></a>Reset the SSH key</span></span>
1. <span data-ttu-id="028e7-132">Cree un archivo llamado PrivateConf.json con este contenido.</span><span class="sxs-lookup"><span data-stu-id="028e7-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="028e7-133">Reemplace los valores de **myUserName** y **mySSHKey** por su propia información.</span><span class="sxs-lookup"><span data-stu-id="028e7-133">Replace the **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="028e7-134">Ejecute este comando y sustituya el nombre de la máquina virtual en **myVM**.</span><span class="sxs-lookup"><span data-stu-id="028e7-134">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="028e7-135"><a name="resetbothcli"></a>Restablecimiento de la contraseña y la clave SSH</span><span class="sxs-lookup"><span data-stu-id="028e7-135"><a name="resetbothcli"></a>Reset both the password and the SSH key</span></span>
1. <span data-ttu-id="028e7-136">Cree un archivo llamado PrivateConf.json con este contenido.</span><span class="sxs-lookup"><span data-stu-id="028e7-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="028e7-137">Reemplace los valores de **myUserName**, **mySSHKey** y **myP@ssW0rd** por su propia información.</span><span class="sxs-lookup"><span data-stu-id="028e7-137">Replace the **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="028e7-138">Ejecute este comando y sustituya el nombre de la máquina virtual en **myVM**.</span><span class="sxs-lookup"><span data-stu-id="028e7-138">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="028e7-139"><a name="createnewsudocli"></a>Crear una nueva cuenta de usuario de sudo</span><span class="sxs-lookup"><span data-stu-id="028e7-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="028e7-140">Si olvida su nombre de usuario, puede utilizar VMAccess para crear uno nuevo con la autoridad de sudo.</span><span class="sxs-lookup"><span data-stu-id="028e7-140">If you forget your user name, you can use VMAccess to create a new one with the sudo authority.</span></span> <span data-ttu-id="028e7-141">En este caso, no se modificarán el nombre de usuario y la contraseña existentes.</span><span class="sxs-lookup"><span data-stu-id="028e7-141">In this case, the existing user name and password will not be modified.</span></span>

<span data-ttu-id="028e7-142">Para crear un nuevo usuario de sudo con acceso de contraseña, utilice el script en [Restablecer la contraseña](#pwresetcli) y especifique el nuevo nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="028e7-142">To create a new sudo user with password access, use the script in [Reset the password](#pwresetcli) and specify the new user name.</span></span>

<span data-ttu-id="028e7-143">Para crear un nuevo usuario de sudo con acceso de clave SSH, utilice el script de [Restablecer la contraseña](#sshkeyresetcli) y especifique el nuevo nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="028e7-143">To create a new sudo user with SSH key access, use the script in [Reset the SSH key](#sshkeyresetcli) and specify the new user name.</span></span>

<span data-ttu-id="028e7-144">También puede usar [Restablecer la contraseña y la clave SSH](#resetbothcli) para crear un nuevo usuario con acceso de contraseña y de clave SSH.</span><span class="sxs-lookup"><span data-stu-id="028e7-144">You can also use [Reset the password and the SSH key](#resetbothcli) to create a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="028e7-145"><a name="sshconfigresetcli"></a>Restablecer la configuración de SSH</span><span class="sxs-lookup"><span data-stu-id="028e7-145"><a name="sshconfigresetcli"></a>Reset the SSH configuration</span></span>
<span data-ttu-id="028e7-146">Si la configuración de SSH se encuentra en un estado no deseado, podría perder el acceso a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="028e7-146">If the SSH configuration is in an undesired state, you might also lose access to the VM.</span></span> <span data-ttu-id="028e7-147">Puede usar la extensión VMAccess para restablecer la configuración a su estado predeterminado.</span><span class="sxs-lookup"><span data-stu-id="028e7-147">You can use the VMAccess extension to reset the configuration to its default state.</span></span> <span data-ttu-id="028e7-148">Para ello, basta con establecer la clave "reset_ssh" en "True".</span><span class="sxs-lookup"><span data-stu-id="028e7-148">To do so, you just need to set the “reset_ssh” key to “True”.</span></span> <span data-ttu-id="028e7-149">La extensión reinicia el servidor SSH, abre el puerto SSH en su máquina virtual y restablece la configuración de SSH al valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="028e7-149">The extension will restart the SSH server, open the SSH port on your VM, and reset the SSH configuration to default values.</span></span> <span data-ttu-id="028e7-150">No se cambiará la cuenta de usuario (nombre, contraseña o claves SSH).</span><span class="sxs-lookup"><span data-stu-id="028e7-150">The user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="028e7-151">El archivo de configuración de SSH que obtiene el restablecimiento se encuentra en /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="028e7-151">The SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="028e7-152">Cree un archivo llamado PrivateConf.json con este contenido.</span><span class="sxs-lookup"><span data-stu-id="028e7-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="028e7-153">Ejecute este comando y sustituya el nombre de la máquina virtual en **myVM**.</span><span class="sxs-lookup"><span data-stu-id="028e7-153">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="028e7-154"><a name="deletecli"></a>Eliminar un usuario</span><span class="sxs-lookup"><span data-stu-id="028e7-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="028e7-155">Si desea eliminar una cuenta de usuario sin iniciar sesión en la máquina virtual directamente, puede utilizar esta secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="028e7-155">If you want to delete a user account without logging into to the VM directly, you can use this script.</span></span>

1. <span data-ttu-id="028e7-156">Cree un archivo llamado PrivateConf.json con este contenido y sustituya el nombre de usuario que quiere eliminar en **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="028e7-156">Create a file named PrivateConf.json with this content, substituting the user name to remove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="028e7-157">Ejecute este comando y sustituya el nombre de la máquina virtual en **myVM**.</span><span class="sxs-lookup"><span data-stu-id="028e7-157">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="028e7-158"><a name="statuscli"></a>Mostrar el estado de la extensión VMAccess</span><span class="sxs-lookup"><span data-stu-id="028e7-158"><a name="statuscli"></a>Display the status of the VMAccess extension</span></span>
<span data-ttu-id="028e7-159">Para mostrar el estado de la extensión VMAccess, ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="028e7-159">To display the status of the VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="028e7-160"><a name='checkdisk'></a>Comprobar la coherencia de los discos agregados</span><span class="sxs-lookup"><span data-stu-id="028e7-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="028e7-161">Para ejecutar fsck en todos los discos de la máquina virtual de Linux, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="028e7-161">To run fsck on all disks in your Linux virtual machine, you will need to do the following:</span></span>

1. <span data-ttu-id="028e7-162">Cree un archivo llamado PrivateConf.json con este contenido.</span><span class="sxs-lookup"><span data-stu-id="028e7-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="028e7-163">Comprobar disco toma un valor booleano para comprobar los discos conectados a la máquina virtual o no.</span><span class="sxs-lookup"><span data-stu-id="028e7-163">Check Disk takes a boolean for whether to check disks attached to your virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="028e7-164">Ejecute este comando y sustituya el nombre de la máquina virtual en **myVM**.</span><span class="sxs-lookup"><span data-stu-id="028e7-164">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="028e7-165"><a name='repairdisk'></a>Reparación de los discos</span><span class="sxs-lookup"><span data-stu-id="028e7-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="028e7-166">Para reparar discos que no se están montando o que tienen errores de configuración de montaje, use la extensión VMAccess para restablecer la configuración de montaje en la máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="028e7-166">To repair disks that are not mounting or have mount configuration errors, use the VMAccess extension to reset the mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="028e7-167">Sustituya el nombre del disco en **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="028e7-167">Substituting the name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="028e7-168">Cree un archivo llamado PrivateConf.json con este contenido.</span><span class="sxs-lookup"><span data-stu-id="028e7-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="028e7-169">Ejecute este comando y sustituya el nombre de la máquina virtual en **myVM**.</span><span class="sxs-lookup"><span data-stu-id="028e7-169">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="028e7-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="028e7-170">Next steps</span></span>
* <span data-ttu-id="028e7-171">Si desea usar cmdlets de Azure PowerShell o plantillas de Azure Resource Manager para restablecer la contraseña o la clave SSH, corregir la configuración de SSH y comprobar la coherencia de disco, consulte la [documentación sobre la extensión VMAccess en GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="028e7-171">If you want to use Azure PowerShell cmdlets or Azure Resource Manager templates to reset the password or SSH key, fix the SSH configuration, and check disk consistency, see the [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="028e7-172">También puede utilizar el [Portal de Azure](https://portal.azure.com) para restablecer la contraseña o la clave SSH de una máquina virtual de Linux implementada en el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="028e7-172">You can also use the [Azure portal](https://portal.azure.com) to reset the password or SSH key of a Linux VM deployed in the classic deployment model.</span></span> <span data-ttu-id="028e7-173">Actualmente, no puede usar el portal para realizar esta tarea en una máquina virtual de Linux implementada en el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="028e7-173">You can't currently use the portal do to this for a Linux VM deployed in the Resource Manager deployment model.</span></span>
* <span data-ttu-id="028e7-174">Consulte [Acerca de las características y extensiones de las máquinas virtuales](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para más información sobre el uso de extensiones de máquinas virtuales para las de Azure.</span><span class="sxs-lookup"><span data-stu-id="028e7-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

