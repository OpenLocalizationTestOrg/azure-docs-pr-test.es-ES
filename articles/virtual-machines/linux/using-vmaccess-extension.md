---
title: aaaReset acceso tooan VM de Linux de Azure | Documentos de Microsoft
description: "Cómo toomanage a los usuarios acceso de restablecimiento sobre el uso de máquinas virtuales de Linux Hola la VMAccess extensión y Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a><span data-ttu-id="04302-103">Administrar usuarios, SSH y comprobación o los discos de reparación sobre el uso de máquinas virtuales de Linux Hola VMAccess extensión con hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="04302-103">Manage users, SSH, and check or repair disks on Linux VMs using hello VMAccess Extension with hello Azure CLI 2.0</span></span>
<span data-ttu-id="04302-104">disco de Hello en la VM de Linux que muestra los errores.</span><span class="sxs-lookup"><span data-stu-id="04302-104">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="04302-105">Algún modo restablecer la contraseña de la raíz de hello para la VM de Linux o había eliminado accidentalmente su clave privada SSH.</span><span class="sxs-lookup"><span data-stu-id="04302-105">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="04302-106">Si esto sucede en días de hello del centro de datos de hello, ¿necesita toodrive existe y después abra Hola KVM tooget en consola de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="04302-106">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="04302-107">Considerar Hola extensión VMAccess de Azure como ese conmutador KVM que permite tooaccess Hola consola tooreset acceso tooLinux o realizar tareas de mantenimiento de nivel de disco.</span><span class="sxs-lookup"><span data-stu-id="04302-107">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="04302-108">Este artículo muestra cómo toouse Hola toocheck de Azure de la VMAccess extensión o reparar un disco, restablecer el acceso de usuario, administrar cuentas de usuario o restablecer la configuración de SSH de hello en Linux.</span><span class="sxs-lookup"><span data-stu-id="04302-108">This article shows you how toouse hello Azure VMAccess Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSH configuration on Linux.</span></span> <span data-ttu-id="04302-109">También puede realizar estos pasos con hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04302-109">You can also perform these steps with hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-toouse-hello-vmaccess-extension"></a><span data-ttu-id="04302-110">Formas toouse Hola VMAccess extensión</span><span class="sxs-lookup"><span data-stu-id="04302-110">Ways toouse hello VMAccess Extension</span></span>
<span data-ttu-id="04302-111">Hay dos formas en que puede utilizar Hola VMAccess extensión en las máquinas virtuales de Linux:</span><span class="sxs-lookup"><span data-stu-id="04302-111">There are two ways that you can use hello VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="04302-112">Utilizar Hola 2.0 de CLI de Azure y los parámetros de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="04302-112">Use hello Azure CLI 2.0 and hello required parameters.</span></span>
* <span data-ttu-id="04302-113">[Archivos de uso sin formato JSON ese proceso de VMAccess extensión hello](#use-json-files-and-the-vmaccess-extension) y, a continuación, actuar en.</span><span class="sxs-lookup"><span data-stu-id="04302-113">[Use raw JSON files that hello VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="04302-114">Hola a consecuencia del uso de ejemplos [usuario de vm az](/cli/azure/vm/user) comandos.</span><span class="sxs-lookup"><span data-stu-id="04302-114">hello following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="04302-115">tooperform estos pasos, necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="04302-115">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="04302-116">Restablecimiento de la clave SSH</span><span class="sxs-lookup"><span data-stu-id="04302-116">Reset SSH key</span></span>
<span data-ttu-id="04302-117">Hello en el ejemplo siguiente se restablece la clave SSH hello para el usuario de hello `azureuser` en hello máquina virtual denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="04302-117">hello following example resets hello SSH key for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="04302-118">Restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="04302-118">Reset password</span></span>
<span data-ttu-id="04302-119">Hello en el ejemplo siguiente se restablece la Hola contraseña de usuario de hello `azureuser` en hello máquina virtual denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="04302-119">hello following example resets hello password for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="04302-120">Reinicio de SSH</span><span class="sxs-lookup"><span data-stu-id="04302-120">Restart SSH</span></span>
<span data-ttu-id="04302-121">Hello en el ejemplo siguiente se reinicia el demonio SSH de Hola y restablece Hola toodefault valores de configuración de SSH en una máquina virtual denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="04302-121">hello following example restarts hello SSH daemon and resets hello SSH configuration toodefault values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="04302-122">Creación de un usuario</span><span class="sxs-lookup"><span data-stu-id="04302-122">Create a user</span></span>
<span data-ttu-id="04302-123">Hello en el ejemplo siguiente se crea un usuario denominado `myNewUser` con una clave SSH para la autenticación en la máquina virtual denominada Hola `myVM`:</span><span class="sxs-lookup"><span data-stu-id="04302-123">hello following example creates a user named `myNewUser` using an SSH key for authentication on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="04302-124">Eliminar un usuario</span><span class="sxs-lookup"><span data-stu-id="04302-124">Delete a user</span></span>
<span data-ttu-id="04302-125">Hello en el ejemplo siguiente se elimina un usuario denominado `myNewUser` en hello máquina virtual denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="04302-125">hello following example deletes a user named `myNewUser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a><span data-ttu-id="04302-126">Usar archivos JSON y Hola VMAccess extensión</span><span class="sxs-lookup"><span data-stu-id="04302-126">Use JSON files and hello VMAccess Extension</span></span>
<span data-ttu-id="04302-127">Hello en los ejemplos siguientes use archivos sin formato de JSON.</span><span class="sxs-lookup"><span data-stu-id="04302-127">hello following examples use raw JSON files.</span></span> <span data-ttu-id="04302-128">Use [conjunto de extensión de vm az](/cli/azure/vm/extension#set) toothen llamar a los archivos JSON.</span><span class="sxs-lookup"><span data-stu-id="04302-128">Use [az vm extension set](/cli/azure/vm/extension#set) toothen call your JSON files.</span></span> <span data-ttu-id="04302-129">Estos archivos JSON también se pueden llamar desde las plantillas de Azure.</span><span class="sxs-lookup"><span data-stu-id="04302-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="04302-130">Restablecimiento del acceso de un usuario</span><span class="sxs-lookup"><span data-stu-id="04302-130">Reset user access</span></span>
<span data-ttu-id="04302-131">Si ha perdido acceso tooroot en la VM de Linux, puede iniciar un tooreset de secuencia de comandos de VMAccess clave SSH o la contraseña de un usuario.</span><span class="sxs-lookup"><span data-stu-id="04302-131">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset a user's SSH key or password.</span></span>

<span data-ttu-id="04302-132">clave pública SSH de tooreset Hola de un usuario, cree un archivo denominado `reset_ssh_key.json` y agregar valores de hello siguiendo el formato.</span><span class="sxs-lookup"><span data-stu-id="04302-132">tooreset hello SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in hello following format.</span></span> <span data-ttu-id="04302-133">Sustituya los valores propios para hello `username` y `ssh_key` parámetros:</span><span class="sxs-lookup"><span data-stu-id="04302-133">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="04302-134">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="04302-134">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="04302-135">tooreset una contraseña de usuario, cree un archivo denominado `reset_user_password.json` y agregar valores de hello siguiendo el formato.</span><span class="sxs-lookup"><span data-stu-id="04302-135">tooreset a user password, create a file named `reset_user_password.json` and add settings in hello following format.</span></span> <span data-ttu-id="04302-136">Sustituya los valores propios para hello `username` y `password` parámetros:</span><span class="sxs-lookup"><span data-stu-id="04302-136">Substitute your own values for hello `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="04302-137">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="04302-137">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="04302-138">Reinicio de SSH</span><span class="sxs-lookup"><span data-stu-id="04302-138">Restart SSH</span></span>
<span data-ttu-id="04302-139">toorestart Hola demonio de SSH y restablezca los valores de toodefault de configuración de SSH de hello, cree un archivo denominado `reset_sshd.json`.</span><span class="sxs-lookup"><span data-stu-id="04302-139">toorestart hello SSH daemon and reset hello SSH configuration toodefault values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="04302-140">Agregue Hola siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="04302-140">Add hello following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="04302-141">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="04302-141">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="04302-142">Administrar usuarios</span><span class="sxs-lookup"><span data-stu-id="04302-142">Manage users</span></span>

<span data-ttu-id="04302-143">toocreate un usuario que utiliza una clave SSH para la autenticación, cree un archivo denominado `create_new_user.json` y agregar valores de hello siguiendo el formato.</span><span class="sxs-lookup"><span data-stu-id="04302-143">toocreate a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in hello following format.</span></span> <span data-ttu-id="04302-144">Sustituya los valores propios para hello `username` y `ssh_key` parámetros:</span><span class="sxs-lookup"><span data-stu-id="04302-144">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="04302-145">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="04302-145">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="04302-146">toodelete un usuario, cree un archivo denominado `delete_user.json` y agregue Hola siguen contenido.</span><span class="sxs-lookup"><span data-stu-id="04302-146">toodelete a user, create a file named `delete_user.json` and add hello following content.</span></span> <span data-ttu-id="04302-147">Sustituya su propio valor para hello `remove_user` parámetro:</span><span class="sxs-lookup"><span data-stu-id="04302-147">Substitute your own value for hello `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="04302-148">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="04302-148">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a><span data-ttu-id="04302-149">Comprobar o reparar el disco de Hola</span><span class="sxs-lookup"><span data-stu-id="04302-149">Check or repair hello disk</span></span>
<span data-ttu-id="04302-150">Uso de VMAccess también puede comprobar y reparar un disco que ha agregado toohello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="04302-150">Using VMAccess you can also check and repair a disk that you added toohello Linux VM.</span></span>

<span data-ttu-id="04302-151">toocheck y, a continuación, disco de reparación de hello, cree un archivo denominado `disk_check_repair.json` y agregar valores de hello siguiendo el formato.</span><span class="sxs-lookup"><span data-stu-id="04302-151">toocheck and then repair hello disk, create a file named `disk_check_repair.json` and add settings in hello following format.</span></span> <span data-ttu-id="04302-152">Sustituya su propio valor para el nombre de Hola de `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="04302-152">Substitute your own value for hello name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="04302-153">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="04302-153">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="04302-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04302-154">Next steps</span></span>
<span data-ttu-id="04302-155">La actualización de Linux utilizando Hola VMAccess extensión de Azure es un método toomake cambia en una VM de Linux de ejecución.</span><span class="sxs-lookup"><span data-stu-id="04302-155">Updating Linux using hello Azure VMAccess Extension is one method toomake changes on a running Linux VM.</span></span> <span data-ttu-id="04302-156">También puede usar herramientas como init de la nube y toomodify de plantillas de Azure Resource Manager la VM de Linux en el arranque.</span><span class="sxs-lookup"><span data-stu-id="04302-156">You can also use tools like cloud-init and Azure Resource Manager templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="04302-157">Características y extensiones de las máquinas virtuales para Linux</span><span class="sxs-lookup"><span data-stu-id="04302-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="04302-158">Creación de plantillas de Azure Resource Manager con extensiones de máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="04302-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="04302-159">Uso de nube init toocustomize una VM de Linux durante la creación</span><span class="sxs-lookup"><span data-stu-id="04302-159">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md)

