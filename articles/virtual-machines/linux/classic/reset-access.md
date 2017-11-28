---
title: "aaaReset contraseña de VM de Linux y SSH clave desde Hola CLI | Documentos de Microsoft"
description: "Cómo corregir la configuración de SSH Hola Hola toouse la extensión VMAccess de interfaz de línea de comandos (CLI) de Azure de hello tooreset una contraseña de VM de Linux o clave SSH y comprobar la coherencia de disco"
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
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a><span data-ttu-id="4b190-103">Cómo tooreset una contraseña de VM de Linux o clave SSH, corrija la configuración de SSH de Hola y comprobar la coherencia de disco con la extensión VMAccess Hola</span><span class="sxs-lookup"><span data-stu-id="4b190-103">How tooreset a Linux VM password or SSH key, fix hello SSH configuration, and check disk consistency using hello VMAccess extension</span></span>
<span data-ttu-id="4b190-104">Si no se puede conectar la máquina virtual de Linux tooa en Azure debido a una contraseña olvidada, una clave de Shell seguro (SSH) incorrecta o un problema con la configuración de SSH de hello, usar hello extensión VMAccessForLinux con hello Azure CLI tooreset Hola contraseña o una clave SSH, corregir configuración de SSH de Hola y comprobar la coherencia de disco.</span><span class="sxs-lookup"><span data-stu-id="4b190-104">If you can't connect tooa Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with hello SSH configuration, use hello VMAccessForLinux extension with hello Azure CLI tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="4b190-105">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4b190-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4b190-106">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="4b190-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4b190-107">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b190-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4b190-108">Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="4b190-108">Learn how too[perform these steps using hello Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="4b190-109">Con hello CLI de Azure, use hello **conjunto de extensión de máquina virtual de azure** comando de los comandos de tooaccess de interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema).</span><span class="sxs-lookup"><span data-stu-id="4b190-109">With hello Azure CLI, you use hello **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) tooaccess commands.</span></span> <span data-ttu-id="4b190-110">Ejecute el comando **azure help vm extension set** para obtener más información sobre el uso de la extensión.</span><span class="sxs-lookup"><span data-stu-id="4b190-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="4b190-111">Con hello CLI de Azure, puede hacer hello las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="4b190-111">With hello Azure CLI, you can do hello following tasks:</span></span>

* [<span data-ttu-id="4b190-112">Hola de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="4b190-112">Reset hello password</span></span>](#pwresetcli)
* [<span data-ttu-id="4b190-113">Restablecer la clave SSH Hola</span><span class="sxs-lookup"><span data-stu-id="4b190-113">Reset hello SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="4b190-114">Restablecer la clave SSH de hello hello y contraseña</span><span class="sxs-lookup"><span data-stu-id="4b190-114">Reset hello password and hello SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="4b190-115">Crear una nueva cuenta de usuario de sudo</span><span class="sxs-lookup"><span data-stu-id="4b190-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="4b190-116">Restablecer configuración de SSH Hola</span><span class="sxs-lookup"><span data-stu-id="4b190-116">Reset hello SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="4b190-117">Eliminar un usuario</span><span class="sxs-lookup"><span data-stu-id="4b190-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="4b190-118">Mostrar el estado de Hola de hello extensión VMAccess</span><span class="sxs-lookup"><span data-stu-id="4b190-118">Display hello status of hello VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="4b190-119">Comprobar la coherencia de los discos agregados</span><span class="sxs-lookup"><span data-stu-id="4b190-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="4b190-120">Reparar los discos agregados a la VM de Linux</span><span class="sxs-lookup"><span data-stu-id="4b190-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="4b190-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4b190-121">Prerequisites</span></span>
<span data-ttu-id="4b190-122">Se necesita toodo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b190-122">You will need toodo hello following:</span></span>

* <span data-ttu-id="4b190-123">Necesitará demasiado[instalar hello Azure CLI](../../../cli-install-nodejs.md) y [conectar tooyour suscripción](../../../xplat-cli-connect.md) toouse Azure recursos asociados a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="4b190-123">You will need too[install hello Azure CLI](../../../cli-install-nodejs.md) and [connect tooyour subscription](../../../xplat-cli-connect.md) toouse Azure resources associated with your account.</span></span>
* <span data-ttu-id="4b190-124">Establecer modo correcto de hello para el modelo de implementación clásica de hello escribiendo siguiente de hello en línea de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="4b190-124">Set hello correct mode for hello classic deployment model by typing hello following at hello command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="4b190-125">Tiene una nueva contraseña o un conjunto de claves SSH, si desea que tooreset ninguna de ellas.</span><span class="sxs-lookup"><span data-stu-id="4b190-125">Have a new password or set of SSH keys, if you want tooreset either one.</span></span> <span data-ttu-id="4b190-126">No necesita estos si desea que la configuración de SSH de tooreset Hola.</span><span class="sxs-lookup"><span data-stu-id="4b190-126">You don't need these if you want tooreset hello SSH configuration.</span></span>

## <span data-ttu-id="4b190-127"><a name="pwresetcli"></a>Hola de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="4b190-127"><a name="pwresetcli"></a>Reset hello password</span></span>
1. <span data-ttu-id="4b190-128">Cree un archivo en el equipo local denominado "PrivateConf.json" con estas líneas.</span><span class="sxs-lookup"><span data-stu-id="4b190-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="4b190-129">Reemplace **myUserName** y **myP@ssW0rd** por su propio nombre de usuario y una contraseña y establezca su propia fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="4b190-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="4b190-130">Ejecute este comando, sustituyendo el nombre hello de la máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="4b190-130">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="4b190-131"><a name="sshkeyresetcli"></a>Restablecer la clave SSH Hola</span><span class="sxs-lookup"><span data-stu-id="4b190-131"><a name="sshkeyresetcli"></a>Reset hello SSH key</span></span>
1. <span data-ttu-id="4b190-132">Cree un archivo llamado PrivateConf.json con este contenido.</span><span class="sxs-lookup"><span data-stu-id="4b190-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="4b190-133">Reemplace hello **myUserName** y **mySSHKey** valores con su propia información.</span><span class="sxs-lookup"><span data-stu-id="4b190-133">Replace hello **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="4b190-134">Ejecute este comando, sustituyendo el nombre hello de la máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="4b190-134">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="4b190-135"><a name="resetbothcli"></a>Restablecimiento de contraseña de Hola y clave SSH de Hola</span><span class="sxs-lookup"><span data-stu-id="4b190-135"><a name="resetbothcli"></a>Reset both hello password and hello SSH key</span></span>
1. <span data-ttu-id="4b190-136">Cree un archivo llamado PrivateConf.json con este contenido.</span><span class="sxs-lookup"><span data-stu-id="4b190-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="4b190-137">Reemplace hello **myUserName**, **mySSHKey** y  **myP@ssW0rd**  valores con su propia información.</span><span class="sxs-lookup"><span data-stu-id="4b190-137">Replace hello **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="4b190-138">Ejecute este comando, sustituyendo el nombre hello de la máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="4b190-138">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="4b190-139"><a name="createnewsudocli"></a>Crear una nueva cuenta de usuario de sudo</span><span class="sxs-lookup"><span data-stu-id="4b190-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="4b190-140">Si ha olvidado su nombre de usuario, puede utilizar VMAccess toocreate uno nuevo con autoridad «sudo» de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b190-140">If you forget your user name, you can use VMAccess toocreate a new one with hello sudo authority.</span></span> <span data-ttu-id="4b190-141">En este caso, Hola nombre de usuario existente y no se modificará la contraseña.</span><span class="sxs-lookup"><span data-stu-id="4b190-141">In this case, hello existing user name and password will not be modified.</span></span>

<span data-ttu-id="4b190-142">un nuevo usuario de sudo con acceso de contraseña, usar la secuencia de comandos de hello en toocreate [Hola de restablecimiento de contraseña](#pwresetcli) y especifique el nombre de usuario nuevo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b190-142">toocreate a new sudo user with password access, use hello script in [Reset hello password](#pwresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="4b190-143">toocreate un nuevo usuario de sudo con acceso de clave SSH, usar la secuencia de comandos de hello en [clave SSH de restablecimiento de hello](#sshkeyresetcli) y especifique el nombre de usuario nuevo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b190-143">toocreate a new sudo user with SSH key access, use hello script in [Reset hello SSH key](#sshkeyresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="4b190-144">También puede usar [de restablecimiento de contraseña de Hola y clave SSH de hello](#resetbothcli) toocreate un nuevo usuario con acceso a la clave SSH y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="4b190-144">You can also use [Reset hello password and hello SSH key](#resetbothcli) toocreate a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="4b190-145"><a name="sshconfigresetcli"></a>Restablecer configuración de SSH Hola</span><span class="sxs-lookup"><span data-stu-id="4b190-145"><a name="sshconfigresetcli"></a>Reset hello SSH configuration</span></span>
<span data-ttu-id="4b190-146">Si la configuración de SSH Hola está en un estado no deseado, también podría perder acceso toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4b190-146">If hello SSH configuration is in an undesired state, you might also lose access toohello VM.</span></span> <span data-ttu-id="4b190-147">Puede usar hello VMAccess extensión tooreset Hola configuración tooits estado predeterminado.</span><span class="sxs-lookup"><span data-stu-id="4b190-147">You can use hello VMAccess extension tooreset hello configuration tooits default state.</span></span> <span data-ttu-id="4b190-148">toodo por lo tanto, solo necesita tooset Hola "reset_ssh" clave demasiado "True".</span><span class="sxs-lookup"><span data-stu-id="4b190-148">toodo so, you just need tooset hello “reset_ssh” key too“True”.</span></span> <span data-ttu-id="4b190-149">extensión de Hello reiniciar servidor SSH de hello, abrir el puerto SSH de hello en la máquina virtual y restablecer los valores de toodefault de configuración de SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b190-149">hello extension will restart hello SSH server, open hello SSH port on your VM, and reset hello SSH configuration toodefault values.</span></span> <span data-ttu-id="4b190-150">no se cambiará la cuenta de usuario de Hello (nombre, la contraseña o claves SSH).</span><span class="sxs-lookup"><span data-stu-id="4b190-150">hello user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="4b190-151">archivo de configuración de SSH de Hola que restablece se encuentra en /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="4b190-151">hello SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="4b190-152">Cree un archivo llamado PrivateConf.json con este contenido.</span><span class="sxs-lookup"><span data-stu-id="4b190-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="4b190-153">Ejecute este comando, sustituyendo el nombre hello de la máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="4b190-153">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="4b190-154"><a name="deletecli"></a>Eliminar un usuario</span><span class="sxs-lookup"><span data-stu-id="4b190-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="4b190-155">Si desea toodelete una cuenta de usuario sin iniciar sesión en toohello VM directamente, puede utilizar esta secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="4b190-155">If you want toodelete a user account without logging into toohello VM directly, you can use this script.</span></span>

1. <span data-ttu-id="4b190-156">Cree un archivo denominado PrivateConf.json con este contenido, sustituyendo hello tooremove de nombre de usuario para **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="4b190-156">Create a file named PrivateConf.json with this content, substituting hello user name tooremove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="4b190-157">Ejecute este comando, sustituyendo el nombre hello de la máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="4b190-157">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="4b190-158"><a name="statuscli"></a>Mostrar el estado de Hola de hello extensión VMAccess</span><span class="sxs-lookup"><span data-stu-id="4b190-158"><a name="statuscli"></a>Display hello status of hello VMAccess extension</span></span>
<span data-ttu-id="4b190-159">estado de hello toodisplay de hello la extensión VMAccess, ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="4b190-159">toodisplay hello status of hello VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="4b190-160"><a name='checkdisk'></a>Comprobar la coherencia de los discos agregados</span><span class="sxs-lookup"><span data-stu-id="4b190-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="4b190-161">toorun fsck en todos los discos de la máquina virtual de Linux, se necesita toodo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b190-161">toorun fsck on all disks in your Linux virtual machine, you will need toodo hello following:</span></span>

1. <span data-ttu-id="4b190-162">Cree un archivo llamado PrivateConf.json con este contenido.</span><span class="sxs-lookup"><span data-stu-id="4b190-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="4b190-163">Comprobar disco toma un valor booleano para si toocheck discos adjunta la máquina virtual de tooyour o no.</span><span class="sxs-lookup"><span data-stu-id="4b190-163">Check Disk takes a boolean for whether toocheck disks attached tooyour virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="4b190-164">Ejecute este tooexecute de comando, sustituyendo el nombre de saludo de la máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="4b190-164">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="4b190-165"><a name='repairdisk'></a>Reparación de los discos</span><span class="sxs-lookup"><span data-stu-id="4b190-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="4b190-166">toorepair los discos que no va a montar o tienen errores de configuración de montaje, use la configuración del montaje hello VMAccess extensión tooreset hello en la máquina virtual de Linux.</span><span class="sxs-lookup"><span data-stu-id="4b190-166">toorepair disks that are not mounting or have mount configuration errors, use hello VMAccess extension tooreset hello mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="4b190-167">Nombre de hello sustituyendo del disco para **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="4b190-167">Substituting hello name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="4b190-168">Cree un archivo llamado PrivateConf.json con este contenido.</span><span class="sxs-lookup"><span data-stu-id="4b190-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="4b190-169">Ejecute este tooexecute de comando, sustituyendo el nombre de saludo de la máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="4b190-169">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="4b190-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b190-170">Next steps</span></span>
* <span data-ttu-id="4b190-171">Si desea toouse cmdlets de PowerShell de Azure o la contraseña de administrador de recursos de Azure plantillas tooreset Hola o la clave SSH, corrija la configuración de SSH de hello y comprobar la coherencia de disco, vea hello [documentación sobre la extensión VMAccess en GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="4b190-171">If you want toouse Azure PowerShell cmdlets or Azure Resource Manager templates tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency, see hello [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="4b190-172">También puede usar hello [portal de Azure](https://portal.azure.com) tooreset contraseña de Hola o clave SSH de una VM de Linux se implementa en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b190-172">You can also use hello [Azure portal](https://portal.azure.com) tooreset hello password or SSH key of a Linux VM deployed in hello classic deployment model.</span></span> <span data-ttu-id="4b190-173">No se utiliza actualmente Hola realice portal toothis para una VM Linux implementada en el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b190-173">You can't currently use hello portal do toothis for a Linux VM deployed in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="4b190-174">Consulte [Acerca de las características y extensiones de las máquinas virtuales](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para más información sobre el uso de extensiones de máquinas virtuales para las de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b190-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

