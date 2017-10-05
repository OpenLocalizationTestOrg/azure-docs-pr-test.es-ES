---
title: "Preguntas más frecuentes sobre VM de Linux en Azure | Microsoft Docs"
description: "Proporciona respuestas a algunas de las preguntas frecuentes sobre las máquinas virtuales de Linux creadas con el modelo de Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0e06d21bd0b6ef807f38e41dcd50c9cd715607a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="4fd57-103">Preguntas frecuentes sobre las máquinas virtuales de Linux</span><span class="sxs-lookup"><span data-stu-id="4fd57-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="4fd57-104">En este artículo se responden algunas preguntas comunes que los usuarios plantean sobre las máquinas virtuales Linux creadas en Azure mediante el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4fd57-104">This article addresses some common questions about Linux virtual machines created in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="4fd57-105">Para ver la versión de Windows de este tema, consulte [Preguntas más frecuentes sobre máquinas virtuales Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4fd57-105">For the Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="4fd57-106">¿Qué puedo ejecutar en una máquina virtual de Azure?</span><span class="sxs-lookup"><span data-stu-id="4fd57-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="4fd57-107">Todos los suscriptores pueden ejecutar software de servidor en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd57-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="4fd57-108">Para más información, consulte [Linux en distribuciones aprobadas por Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4fd57-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="4fd57-109">¿Cuánto almacenamiento puedo usar con una máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="4fd57-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="4fd57-110">Cada disco de datos puede ser de hasta 1 TB.</span><span class="sxs-lookup"><span data-stu-id="4fd57-110">Each data disk can be up to 1 TB.</span></span> <span data-ttu-id="4fd57-111">El número de discos de datos que puede usar depende del tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4fd57-111">The number of data disks you can use depends on the size of the virtual machine.</span></span> <span data-ttu-id="4fd57-112">Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4fd57-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="4fd57-113">Una cuenta de almacenamiento de Azure proporciona almacenamiento para el disco del sistema operativo y los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="4fd57-113">An Azure storage account provides storage for the operating system disk and any data disks.</span></span> <span data-ttu-id="4fd57-114">Cada disco es un archivo .vhd almacenado como un blob en páginas.</span><span class="sxs-lookup"><span data-stu-id="4fd57-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="4fd57-115">Para obtener información detallada sobre los precios, consulte [Detalles de precios de almacenamiento](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="4fd57-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="4fd57-116">¿Cómo puedo tener acceso a mi máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="4fd57-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="4fd57-117">Establezca una conexión remota para iniciar sesión en la máquina virtual mediante Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="4fd57-117">Establish a remote connection to log on to the virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="4fd57-118">Consulte las instrucciones sobre cómo conectarse [desde Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [desde Linux y Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4fd57-118">See the instructions on how to connect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4fd57-119">De forma predeterminada, SSH permite un máximo de 10 conexiones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="4fd57-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="4fd57-120">Puede aumentar este número editando el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="4fd57-120">You can increase this number by editing the configuration file.</span></span>

<span data-ttu-id="4fd57-121">Si tiene problemas, consulte [Solución de problemas de conexiones de Secure Shell (SSH)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4fd57-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-the-temporary-disk-devsdb1-to-store-data"></a><span data-ttu-id="4fd57-122">¿Puedo usar el disco temporal (/dev/sdb1) para almacenar datos?</span><span class="sxs-lookup"><span data-stu-id="4fd57-122">Can I use the temporary disk (/dev/sdb1) to store data?</span></span>
<span data-ttu-id="4fd57-123">No utilice el disco temporal (/dev/sdb1) para almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="4fd57-123">Don't use the temporary disk (/dev/sdb1) to store data.</span></span> <span data-ttu-id="4fd57-124">Solo existe para el almacenamiento temporal.</span><span class="sxs-lookup"><span data-stu-id="4fd57-124">It is only there for temporary storage.</span></span> <span data-ttu-id="4fd57-125">Corre el riesgo de perder datos que no se podrán recuperar.</span><span class="sxs-lookup"><span data-stu-id="4fd57-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="4fd57-126">¿Puedo copiar o clonar una máquina virtual de Azure existente?</span><span class="sxs-lookup"><span data-stu-id="4fd57-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="4fd57-127">Sí.</span><span class="sxs-lookup"><span data-stu-id="4fd57-127">Yes.</span></span> <span data-ttu-id="4fd57-128">Para obtener instrucciones, consulte [Creación de una copia de una máquina virtual Linux en el modelo de implementación de Resource Manager](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4fd57-128">For instructions, see [How to create a copy of a Linux virtual machine in the Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="4fd57-129">¿Por qué no veo las regiones de Canadá central y Canadá oriental por medio de Azure Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="4fd57-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="4fd57-130">Las dos nuevas áreas Canadá central y Canadá oriental no se registran automáticamente para la creación de máquinas virtuales en las suscripciones de Azure existentes.</span><span class="sxs-lookup"><span data-stu-id="4fd57-130">The two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="4fd57-131">Este registro se realizará automáticamente cuando se implementa una máquina virtual mediante el Portal de Azure en cualquier otra región usando Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4fd57-131">This registration is done automatically when a virtual machine is deployed through the Azure portal to any other region using Azure Resource Manager.</span></span> <span data-ttu-id="4fd57-132">Después de implementar una máquina virtual en cualquier otra región de Azure, las áreas nuevas deberán estar disponibles para las máquinas virtuales siguientes.</span><span class="sxs-lookup"><span data-stu-id="4fd57-132">After a virtual machine is deployed to any other Azure region, the new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-to-my-vm-after-its-created"></a><span data-ttu-id="4fd57-133">¿Puedo agregar una NIC a mi máquina virtual después de crearla?</span><span class="sxs-lookup"><span data-stu-id="4fd57-133">Can I add a NIC to my VM after it's created?</span></span>
<span data-ttu-id="4fd57-134">Sí, ahora es posible.</span><span class="sxs-lookup"><span data-stu-id="4fd57-134">Yes, this is now possible.</span></span> <span data-ttu-id="4fd57-135">En primer lugar, la máquina virtual debe detenerse desasignada.</span><span class="sxs-lookup"><span data-stu-id="4fd57-135">The VM first needs to be stopped deallocated.</span></span> <span data-ttu-id="4fd57-136">A continuación, puede agregar o quitar una NIC (a menos que sea la última en la máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="4fd57-136">Then you can add or remove a NIC (unless it's the last NIC on the VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="4fd57-137">¿Hay algún requisito de nombre de equipo?</span><span class="sxs-lookup"><span data-stu-id="4fd57-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="4fd57-138">Sí.</span><span class="sxs-lookup"><span data-stu-id="4fd57-138">Yes.</span></span> <span data-ttu-id="4fd57-139">El nombre del equipo puede tener un máximo de 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4fd57-139">The computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="4fd57-140">Consulte el artículo sobre las [convenciones y restricciones de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para más información sobre la denominación de los recursos.</span><span class="sxs-lookup"><span data-stu-id="4fd57-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="4fd57-141">¿Existen algunos requisitos para los nombres de grupos de recursos?</span><span class="sxs-lookup"><span data-stu-id="4fd57-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="4fd57-142">Sí.</span><span class="sxs-lookup"><span data-stu-id="4fd57-142">Yes.</span></span> <span data-ttu-id="4fd57-143">El nombre del grupo de recursos puede tener como máximo 90 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4fd57-143">The resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="4fd57-144">Consulte el artículo sobre las [convenciones y restricciones de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para más información sobre los grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="4fd57-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-the-username-requirements-when-creating-a-vm"></a><span data-ttu-id="4fd57-145">¿Cuáles son los requisitos de nombre de usuario cuando se crea una VM?</span><span class="sxs-lookup"><span data-stu-id="4fd57-145">What are the username requirements when creating a VM?</span></span>
<span data-ttu-id="4fd57-146">Los nombres de usuario deben tener entre 1 y 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4fd57-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="4fd57-147">No se permiten los siguientes nombres de usuario:</span><span class="sxs-lookup"><span data-stu-id="4fd57-147">The following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="4fd57-148">administrator</span><span class="sxs-lookup"><span data-stu-id="4fd57-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-149">admin</span><span class="sxs-lookup"><span data-stu-id="4fd57-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-150">user</span><span class="sxs-lookup"><span data-stu-id="4fd57-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-151">user1</span><span class="sxs-lookup"><span data-stu-id="4fd57-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="4fd57-152">test</span><span class="sxs-lookup"><span data-stu-id="4fd57-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-153">user2</span><span class="sxs-lookup"><span data-stu-id="4fd57-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-154">test1</span><span class="sxs-lookup"><span data-stu-id="4fd57-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-155">user3</span><span class="sxs-lookup"><span data-stu-id="4fd57-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="4fd57-156">admin1</span><span class="sxs-lookup"><span data-stu-id="4fd57-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-157">1</span><span class="sxs-lookup"><span data-stu-id="4fd57-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-158">123</span><span class="sxs-lookup"><span data-stu-id="4fd57-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-159">a</span><span class="sxs-lookup"><span data-stu-id="4fd57-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="4fd57-160">actuser</span><span class="sxs-lookup"><span data-stu-id="4fd57-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="4fd57-161">adm</span><span class="sxs-lookup"><span data-stu-id="4fd57-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-162">admin2</span><span class="sxs-lookup"><span data-stu-id="4fd57-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="4fd57-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="4fd57-164">backup</span><span class="sxs-lookup"><span data-stu-id="4fd57-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-165">console</span><span class="sxs-lookup"><span data-stu-id="4fd57-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-166">david</span><span class="sxs-lookup"><span data-stu-id="4fd57-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-167">guest</span><span class="sxs-lookup"><span data-stu-id="4fd57-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="4fd57-168">john</span><span class="sxs-lookup"><span data-stu-id="4fd57-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-169">owner</span><span class="sxs-lookup"><span data-stu-id="4fd57-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-170">root</span><span class="sxs-lookup"><span data-stu-id="4fd57-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-171">server</span><span class="sxs-lookup"><span data-stu-id="4fd57-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="4fd57-172">sql</span><span class="sxs-lookup"><span data-stu-id="4fd57-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-173">support</span><span class="sxs-lookup"><span data-stu-id="4fd57-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="4fd57-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-175">sys</span><span class="sxs-lookup"><span data-stu-id="4fd57-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="4fd57-176">test2</span><span class="sxs-lookup"><span data-stu-id="4fd57-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-177">test3</span><span class="sxs-lookup"><span data-stu-id="4fd57-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-178">user4</span><span class="sxs-lookup"><span data-stu-id="4fd57-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="4fd57-179">user5</span><span class="sxs-lookup"><span data-stu-id="4fd57-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-the-password-requirements-when-creating-a-vm"></a><span data-ttu-id="4fd57-180">¿Cuáles son los requisitos de contraseña cuando se crea una VM?</span><span class="sxs-lookup"><span data-stu-id="4fd57-180">What are the password requirements when creating a VM?</span></span>
<span data-ttu-id="4fd57-181">Las contraseñas deben tener entre 6 y 72 caracteres y deben cumplir 3 de estos 4 requisitos de complejidad:</span><span class="sxs-lookup"><span data-stu-id="4fd57-181">Passwords must be 6 - 72 characters in length and meet 3 out of the following 4 complexity requirements:</span></span>

* <span data-ttu-id="4fd57-182">Deben incluir caracteres en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="4fd57-182">Have lower characters</span></span>
* <span data-ttu-id="4fd57-183">Deben incluir caracteres en mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="4fd57-183">Have upper characters</span></span>
* <span data-ttu-id="4fd57-184">Deben incluir un dígito.</span><span class="sxs-lookup"><span data-stu-id="4fd57-184">Have a digit</span></span>
* <span data-ttu-id="4fd57-185">Deben incluir un carácter especial (REGEX.MATCH [\W_]).</span><span class="sxs-lookup"><span data-stu-id="4fd57-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="4fd57-186">No se permiten las siguientes contraseñas:</span><span class="sxs-lookup"><span data-stu-id="4fd57-186">The following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="4fd57-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="4fd57-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="4fd57-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="4fd57-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="4fd57-189">Password!</span><span class="sxs-lookup"><span data-stu-id="4fd57-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="4fd57-190">Password1</span><span class="sxs-lookup"><span data-stu-id="4fd57-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="4fd57-191">Password22</span><span class="sxs-lookup"><span data-stu-id="4fd57-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="4fd57-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="4fd57-192">iloveyou!</span></span></td>
    </tr>
</table>
