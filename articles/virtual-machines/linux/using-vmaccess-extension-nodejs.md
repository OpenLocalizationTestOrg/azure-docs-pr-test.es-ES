---
title: "acceso de aaaReset sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión | Documentos de Microsoft"
description: "Restablecer el acceso en máquinas virtuales de Linux de Azure con hello VMAccess extensión."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a><span data-ttu-id="7c568-103">Administrar usuarios, SSH y comprobación o los discos de reparación sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7c568-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="7c568-104">Este artículo muestra cómo toouse hello Azure VMAcesss extensión toocheck o reparar un disco, restablecer el acceso de usuario, administrar cuentas de usuario o restablecer la configuración de SSHD hello en Linux.</span><span class="sxs-lookup"><span data-stu-id="7c568-104">This article shows you how toouse hello Azure VMAcesss Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSHD configuration on Linux.</span></span> <span data-ttu-id="7c568-105">Hola artículo requiere:</span><span class="sxs-lookup"><span data-stu-id="7c568-105">hello article requires:</span></span>

* <span data-ttu-id="7c568-106">una cuenta de Azure ([obtenga aquí una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/));</span><span class="sxs-lookup"><span data-stu-id="7c568-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="7c568-107">Hola [CLI de Azure](../../cli-install-nodejs.md) inició sesión `azure login`.</span><span class="sxs-lookup"><span data-stu-id="7c568-107">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="7c568-108">Hola CLI de Azure *debe estar en* modo Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="7c568-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="7c568-109">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="7c568-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="7c568-110">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="7c568-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="7c568-111">[Azure 1.0 de CLI](#quick-commands)– nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="7c568-111">[Azure CLI 1.0](#quick-commands)– our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="7c568-112">[Azure 2.0 CLI](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="7c568-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="7c568-113">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="7c568-113">Quick commands</span></span>
<span data-ttu-id="7c568-114">Hay dos maneras toouse VMAccess en las máquinas virtuales de Linux:</span><span class="sxs-lookup"><span data-stu-id="7c568-114">There are two ways toouse VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="7c568-115">Utilizar hello y hello Azure CLI 1.0 requiere parámetros.</span><span class="sxs-lookup"><span data-stu-id="7c568-115">Using hello Azure CLI 1.0 and hello required parameters.</span></span>
* <span data-ttu-id="7c568-116">Con archivos JSON sin formato que procesa VMAccess para luego realizar acciones en ellos.</span><span class="sxs-lookup"><span data-stu-id="7c568-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="7c568-117">Para la sección del comando rápido de hello, vamos toouse hello Azure CLI 1.0 `azure vm reset-access` método.</span><span class="sxs-lookup"><span data-stu-id="7c568-117">For hello quick command section, we are going toouse hello Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="7c568-118">Hola siguientes ejemplos de comandos, reemplace los valores de hello que contienen "ejemplo" con valores de hello desde su propio entorno.</span><span class="sxs-lookup"><span data-stu-id="7c568-118">In hello following command examples, replace hello values that contain "example" with hello values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="7c568-119">Creación de un grupo de recursos y una VM Linux</span><span class="sxs-lookup"><span data-stu-id="7c568-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="7c568-120">Creación de una máquina virtual Debian</span><span class="sxs-lookup"><span data-stu-id="7c568-120">Create a Debian VM</span></span>
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a><span data-ttu-id="7c568-121">Restablecimiento de la contraseña raíz</span><span class="sxs-lookup"><span data-stu-id="7c568-121">Reset root password</span></span>
<span data-ttu-id="7c568-122">contraseña de raíz de Hola tooreset:</span><span class="sxs-lookup"><span data-stu-id="7c568-122">tooreset hello root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="7c568-123">Restablecimiento de la clave SSH</span><span class="sxs-lookup"><span data-stu-id="7c568-123">SSH key reset</span></span>
<span data-ttu-id="7c568-124">clave SSH tooreset Hola de un usuario no es de raíz:</span><span class="sxs-lookup"><span data-stu-id="7c568-124">tooreset hello SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="7c568-125">Creación de un usuario</span><span class="sxs-lookup"><span data-stu-id="7c568-125">Create a user</span></span>
<span data-ttu-id="7c568-126">toocreate un usuario:</span><span class="sxs-lookup"><span data-stu-id="7c568-126">toocreate a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="7c568-127">Eliminación de un usuario</span><span class="sxs-lookup"><span data-stu-id="7c568-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="7c568-128">Restablecer SSHD</span><span class="sxs-lookup"><span data-stu-id="7c568-128">Reset SSHD</span></span>
<span data-ttu-id="7c568-129">configuración de tooreset Hola SSHD:</span><span class="sxs-lookup"><span data-stu-id="7c568-129">tooreset hello SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="7c568-130">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="7c568-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="7c568-131">VMAccess definido:</span><span class="sxs-lookup"><span data-stu-id="7c568-131">VMAccess defined:</span></span>
<span data-ttu-id="7c568-132">disco de Hello en la VM de Linux que muestra los errores.</span><span class="sxs-lookup"><span data-stu-id="7c568-132">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="7c568-133">Algún modo restablecer la contraseña de la raíz de hello para la VM de Linux o había eliminado accidentalmente su clave privada SSH.</span><span class="sxs-lookup"><span data-stu-id="7c568-133">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="7c568-134">Si esto sucede en días de hello del centro de datos de hello, ¿necesita toodrive existe y después abra Hola KVM tooget en consola de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c568-134">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="7c568-135">Considerar Hola extensión VMAccess de Azure como ese conmutador KVM que permite tooaccess Hola consola tooreset acceso tooLinux o realizar tareas de mantenimiento de nivel de disco.</span><span class="sxs-lookup"><span data-stu-id="7c568-135">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="7c568-136">Para hello detallada tutorial, vamos toouse hello no abreviada de VMAccess, que usa los archivos sin formato de JSON.</span><span class="sxs-lookup"><span data-stu-id="7c568-136">For hello detailed walkthrough, we are going toouse hello long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="7c568-137">Estos archivos JSON de VMAccess también se pueden llamar desde las plantillas de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c568-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a><span data-ttu-id="7c568-138">Usar disco de Hola de VMAccess toocheck o reparación de una VM de Linux</span><span class="sxs-lookup"><span data-stu-id="7c568-138">Using VMAccess toocheck or repair hello disk of a Linux VM</span></span>
<span data-ttu-id="7c568-139">Uso de VMAccess puede hacer un fsck ejecutar en el disco de hello en la VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="7c568-139">Using VMAccess you can do a fsck run on hello disk under your Linux VM.</span></span>  <span data-ttu-id="7c568-140">También puede hacer una comprobación y reparación de disco con VMAccess.</span><span class="sxs-lookup"><span data-stu-id="7c568-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="7c568-141">toocheck y, a continuación, disco de reparación de hello utilizar esta secuencia de comandos de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7c568-141">toocheck, and then repair hello disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="7c568-142">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="7c568-142">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a><span data-ttu-id="7c568-143">Uso de VMAccess tooreset usuario acceso tooLinux</span><span class="sxs-lookup"><span data-stu-id="7c568-143">Using VMAccess tooreset user access tooLinux</span></span>
<span data-ttu-id="7c568-144">Si ha perdido acceso tooroot en la VM de Linux, puede iniciar una contraseña de la raíz de la secuencia de comandos tooreset VMAccess Hola.</span><span class="sxs-lookup"><span data-stu-id="7c568-144">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset hello root password.</span></span>

<span data-ttu-id="7c568-145">contraseña de la raíz de tooreset hello, use este script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7c568-145">tooreset hello root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="7c568-146">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="7c568-146">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="7c568-147">clave SSH de hello tooreset de un usuario no es de raíz, use este script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7c568-147">tooreset hello SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="7c568-148">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="7c568-148">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a><span data-ttu-id="7c568-149">Uso de cuentas de usuario de VMAccess toomanage en Linux</span><span class="sxs-lookup"><span data-stu-id="7c568-149">Using VMAccess toomanage user accounts on Linux</span></span>
<span data-ttu-id="7c568-150">VMAccess es un script de Python que puede ser usuarios toomanage usado en la VM de Linux sin inicio de sesión y la cuenta raíz sudo o hello.</span><span class="sxs-lookup"><span data-stu-id="7c568-150">VMAccess is a Python script that can be used toomanage users on your Linux VM without logging in and using sudo or hello root account.</span></span>

<span data-ttu-id="7c568-151">toocreate un usuario, use este script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7c568-151">toocreate a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="7c568-152">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="7c568-152">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="7c568-153">toodelete un usuario, use este script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7c568-153">toodelete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="7c568-154">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="7c568-154">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a><span data-ttu-id="7c568-155">Uso de VMAccess tooreset Hola SSHD configuración</span><span class="sxs-lookup"><span data-stu-id="7c568-155">Using VMAccess tooreset hello SSHD configuration</span></span>
<span data-ttu-id="7c568-156">Si realiza la configuración de SSHD de máquinas virtuales de Linux de cambios toohello y conexión de SSH Hola cerrar antes de comprobar los cambios de hello, es podrán que no pueda SSH'ing en.</span><span class="sxs-lookup"><span data-stu-id="7c568-156">If you make changes toohello Linux VMs SSHD configuration and close hello SSH connection before verifying hello changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="7c568-157">VMAccess puede ser usado tooreset Hola SSHD configuración tooa back-configuración válida conocida sin iniciar sesión mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="7c568-157">VMAccess can be used tooreset hello SSHD configuration back tooa known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="7c568-158">configuración de tooreset Hola SSHD utilizar esta secuencia de comandos de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="7c568-158">tooreset hello SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="7c568-159">Ejecute la secuencia de comandos de hello VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="7c568-159">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="7c568-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c568-160">Next steps</span></span>
<span data-ttu-id="7c568-161">La actualización de Linux con extensiones de VMAccess de Azure es un método toomake cambia en una VM de Linux de ejecución.</span><span class="sxs-lookup"><span data-stu-id="7c568-161">Updating Linux using Azure VMAccess Extensions is one method toomake changes on a running Linux VM.</span></span>  <span data-ttu-id="7c568-162">También puede usar herramientas como init de la nube y toomodify de plantillas de Azure la VM de Linux en el arranque.</span><span class="sxs-lookup"><span data-stu-id="7c568-162">You can also use tools like cloud-init and Azure Templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="7c568-163">Acerca de las características y extensiones de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7c568-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="7c568-164">Creación de plantillas de Azure Resource Manager con extensiones de máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="7c568-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="7c568-165">Uso de nube init toocustomize una VM de Linux durante la creación</span><span class="sxs-lookup"><span data-stu-id="7c568-165">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

