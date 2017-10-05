---
title: "Restablecimiento del acceso en máquinas virtuales Linux de Azure con la extensión VMAccess | Microsoft Docs"
description: "Restablezca el acceso en las máquinas virtuales de Linux de Azure con la extensión VMAccess."
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
ms.openlocfilehash: 278bf1785aac71068ab94cf9916af69a204c44be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-the-vmaccess-extension-with-the-azure-cli-10"></a><span data-ttu-id="9f6e8-103">Administración de usuarios, SSH, y comprobación o reparación de discos en máquinas virtuales Linux de Azure con la extensión VMAccess y la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9f6e8-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension with the Azure CLI 1.0</span></span>
<span data-ttu-id="9f6e8-104">En este artículo se muestra cómo usar la extensión VMAccess de Azure para comprobar o reparar un disco, restablecer el acceso de usuario, administrar cuentas de usuario o restablecer la configuración de SSHD en Linux.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-104">This article shows you how to use the Azure VMAcesss Extension to check or repair a disk, reset user access, manage user accounts, or reset the SSHD configuration on Linux.</span></span> <span data-ttu-id="9f6e8-105">Este artículo requiere:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-105">The article requires:</span></span>

* <span data-ttu-id="9f6e8-106">una cuenta de Azure ([obtenga aquí una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/));</span><span class="sxs-lookup"><span data-stu-id="9f6e8-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="9f6e8-107">la [CLI de Azure](../../cli-install-nodejs.md) en la que se inició sesión con `azure login`;</span><span class="sxs-lookup"><span data-stu-id="9f6e8-107">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="9f6e8-108">la CLI de Azure *debe estar en* el modo Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="9f6e8-109">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="9f6e8-109">CLI versions to complete the task</span></span>
<span data-ttu-id="9f6e8-110">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="9f6e8-111">[CLI de Azure 1.0](#quick-commands): la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="9f6e8-111">[Azure CLI 1.0](#quick-commands)– our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9f6e8-112">[CLI de Azure 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): la CLI de última generación para el modelo de implementación de administración de recursos</span><span class="sxs-lookup"><span data-stu-id="9f6e8-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="9f6e8-113">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="9f6e8-113">Quick commands</span></span>
<span data-ttu-id="9f6e8-114">Existen dos maneras de usar VMAccess en las máquinas virtuales Linux:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-114">There are two ways to use VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="9f6e8-115">Con la CLI de Azure 1.0 y los parámetros necesarios.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-115">Using the Azure CLI 1.0 and the required parameters.</span></span>
* <span data-ttu-id="9f6e8-116">Con archivos JSON sin formato que procesa VMAccess para luego realizar acciones en ellos.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="9f6e8-117">Para ver la sección de comandos rápidos, usaremos el método `azure vm reset-access` de la CLI de Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-117">For the quick command section, we are going to use the Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="9f6e8-118">En los siguientes ejemplos de comandos, reemplace los valores que contienen "example" por los valores de su propio entorno.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-118">In the following command examples, replace the values that contain "example" with the values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="9f6e8-119">Creación de un grupo de recursos y una VM Linux</span><span class="sxs-lookup"><span data-stu-id="9f6e8-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="9f6e8-120">Creación de una máquina virtual Debian</span><span class="sxs-lookup"><span data-stu-id="9f6e8-120">Create a Debian VM</span></span>
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

## <a name="reset-root-password"></a><span data-ttu-id="9f6e8-121">Restablecimiento de la contraseña raíz</span><span class="sxs-lookup"><span data-stu-id="9f6e8-121">Reset root password</span></span>
<span data-ttu-id="9f6e8-122">Para restablecer la contraseña raíz:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-122">To reset the root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="9f6e8-123">Restablecimiento de la clave SSH</span><span class="sxs-lookup"><span data-stu-id="9f6e8-123">SSH key reset</span></span>
<span data-ttu-id="9f6e8-124">Para restablecer la clave SSH de un usuario no raíz:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-124">To reset the SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="9f6e8-125">Creación de un usuario</span><span class="sxs-lookup"><span data-stu-id="9f6e8-125">Create a user</span></span>
<span data-ttu-id="9f6e8-126">Para crear un usuario:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-126">To create a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="9f6e8-127">Eliminación de un usuario</span><span class="sxs-lookup"><span data-stu-id="9f6e8-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="9f6e8-128">Restablecer SSHD</span><span class="sxs-lookup"><span data-stu-id="9f6e8-128">Reset SSHD</span></span>
<span data-ttu-id="9f6e8-129">Para restablecer la configuración de SSHD:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-129">To reset the SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="9f6e8-130">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="9f6e8-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="9f6e8-131">VMAccess definido:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-131">VMAccess defined:</span></span>
<span data-ttu-id="9f6e8-132">El disco de la máquina virtual de Linux muestra errores.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-132">The disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="9f6e8-133">De alguna forma, restableció la contraseña raíz de la máquina virtual de Linux o eliminó por accidente la clave privada SSH.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-133">You somehow reset the root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="9f6e8-134">Si esto sucedió en el centro de datos, deberá ir ahí y, luego, abrir el conmutador KVM para llegar a la consola del servidor.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-134">If that happened back in the days of the datacenter, you would need to drive there and then open the KVM to get at the server console.</span></span> <span data-ttu-id="9f6e8-135">Piense en la extensión VMAccess de Azure como ese conmutador KVM que le permite tener acceso a la consola para restablecer el acceso a Linux o realizar el mantenimiento de nivel de disco.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-135">Think of the Azure VMAccess extension as that KVM switch that allows you to access the console to reset access to Linux or perform disk level maintenance.</span></span>

<span data-ttu-id="9f6e8-136">En el tutorial detallado vamos a usar el formato largo de VMAccess, que usa archivos JSON sin formato.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-136">For the detailed walkthrough, we are going to use the long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="9f6e8-137">Estos archivos JSON de VMAccess también se pueden llamar desde las plantillas de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-to-check-or-repair-the-disk-of-a-linux-vm"></a><span data-ttu-id="9f6e8-138">Uso de VMAccess para comprobar o reparar el disco de una máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="9f6e8-138">Using VMAccess to check or repair the disk of a Linux VM</span></span>
<span data-ttu-id="9f6e8-139">Con VMAccess, puede ejecutar fsck en el disco de la máquina virtual de Linux.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-139">Using VMAccess you can do a fsck run on the disk under your Linux VM.</span></span>  <span data-ttu-id="9f6e8-140">También puede hacer una comprobación y reparación de disco con VMAccess.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="9f6e8-141">Para comprobar y luego reparar el disco, use este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-141">To check, and then repair the disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="9f6e8-142">Ejecute el script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-142">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-to-reset-user-access-to-linux"></a><span data-ttu-id="9f6e8-143">Uso de VMAccess para restablecer el acceso de usuario a Linux</span><span class="sxs-lookup"><span data-stu-id="9f6e8-143">Using VMAccess to reset user access to Linux</span></span>
<span data-ttu-id="9f6e8-144">Si perdió el acceso a la raíz de la máquina virtual Linux, puede iniciar un script de VMAccess para restablecer la contraseña raíz.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-144">If you have lost access to root on your Linux VM, you can launch a VMAccess script to reset the root password.</span></span>

<span data-ttu-id="9f6e8-145">Para restablecer la contraseña raíz, use este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-145">To reset the root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="9f6e8-146">Ejecute el script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-146">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="9f6e8-147">Para restablecer la clave SSH de un usuario no raíz, use este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-147">To reset the SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="9f6e8-148">Ejecute el script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-148">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-to-manage-user-accounts-on-linux"></a><span data-ttu-id="9f6e8-149">Uso de VMAccess para administrar cuentas de usuario en Linux</span><span class="sxs-lookup"><span data-stu-id="9f6e8-149">Using VMAccess to manage user accounts on Linux</span></span>
<span data-ttu-id="9f6e8-150">VMAccess es un script de Python que se puede usar para administrar usuarios en la máquina virtual de Linux sin iniciar sesión y mediante la cuenta raíz o sudo.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-150">VMAccess is a Python script that can be used to manage users on your Linux VM without logging in and using sudo or the root account.</span></span>

<span data-ttu-id="9f6e8-151">Para crear un usuario, use este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-151">To create a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="9f6e8-152">Ejecute el script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-152">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="9f6e8-153">Para eliminar un usuario, use este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-153">To delete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="9f6e8-154">Ejecute el script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-154">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-to-reset-the-sshd-configuration"></a><span data-ttu-id="9f6e8-155">Uso de VMAccess para restablecer la configuración SSHD</span><span class="sxs-lookup"><span data-stu-id="9f6e8-155">Using VMAccess to reset the SSHD configuration</span></span>
<span data-ttu-id="9f6e8-156">Si realiza cambios en la configuración SSHD de máquinas virtuales de Linux y cerrar la conexión SSH antes de comprobar los cambios, es posible que se le impida volver a realizar la conexión SSH.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-156">If you make changes to the Linux VMs SSHD configuration and close the SSH connection before verifying the changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="9f6e8-157">VMAccess se puede usar para restablecer la configuración SSHD nuevamente a una buena configuración conocida sin tener que iniciar sesión a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-157">VMAccess can be used to reset the SSHD configuration back to a known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="9f6e8-158">Para restablecer la configuración SSHD, use este script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-158">To reset the SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="9f6e8-159">Ejecute el script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="9f6e8-159">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="9f6e8-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f6e8-160">Next steps</span></span>
<span data-ttu-id="9f6e8-161">Actualizar Linux con las extensiones VMAccess de Azure es un método para hacer cambios en una VM de Linux en ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-161">Updating Linux using Azure VMAccess Extensions is one method to make changes on a running Linux VM.</span></span>  <span data-ttu-id="9f6e8-162">También puede usar herramientas como cloud-init y plantillas de Azure para modificar la VM de Linux en el arranque.</span><span class="sxs-lookup"><span data-stu-id="9f6e8-162">You can also use tools like cloud-init and Azure Templates to modify your Linux VM on boot.</span></span>

[<span data-ttu-id="9f6e8-163">Acerca de las características y extensiones de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9f6e8-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="9f6e8-164">Creación de plantillas de Azure Resource Manager con extensiones de máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="9f6e8-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="9f6e8-165">Uso de cloud-init para personalizar una VM de Linux durante la creación</span><span class="sxs-lookup"><span data-stu-id="9f6e8-165">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

