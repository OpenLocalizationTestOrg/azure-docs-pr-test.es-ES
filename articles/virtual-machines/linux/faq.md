---
title: "aaaFrequently pregunta para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Proporciona respuestas toosome de preguntas frecuentes de hello sobre máquinas virtuales Linux creadas con el modelo del Administrador de recursos de Hola."
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
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="bb2f5-103">Preguntas frecuentes sobre las máquinas virtuales de Linux</span><span class="sxs-lookup"><span data-stu-id="bb2f5-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="bb2f5-104">Este artículo tratan algunas preguntas comunes sobre máquinas virtuales Linux creadas en Azure con el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-104">This article addresses some common questions about Linux virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="bb2f5-105">Para la versión de Windows hello de este tema, consulte [preguntas más frecuentes acerca de máquinas virtuales de Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bb2f5-105">For hello Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="bb2f5-106">¿Qué puedo ejecutar en una máquina virtual de Azure?</span><span class="sxs-lookup"><span data-stu-id="bb2f5-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="bb2f5-107">Todos los suscriptores pueden ejecutar software de servidor en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="bb2f5-108">Para más información, consulte [Linux en distribuciones aprobadas por Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bb2f5-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="bb2f5-109">¿Cuánto almacenamiento puedo usar con una máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="bb2f5-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="bb2f5-110">Cada disco de datos puede ser hasta too1 TB.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-110">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="bb2f5-111">número de Hola de discos de datos que puede usar depende de tamaño de Hola de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-111">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="bb2f5-112">Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bb2f5-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="bb2f5-113">Una cuenta de almacenamiento de Azure proporciona almacenamiento para el disco del sistema operativo de Hola y los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-113">An Azure storage account provides storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="bb2f5-114">Cada disco es un archivo .vhd almacenado como un blob en páginas.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="bb2f5-115">Para obtener información detallada sobre los precios, consulte [Detalles de precios de almacenamiento](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="bb2f5-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="bb2f5-116">¿Cómo puedo tener acceso a mi máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="bb2f5-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="bb2f5-117">Establecer un toolog de conexión remota en la máquina virtual de toohello, mediante Shell seguro (SSH).</span><span class="sxs-lookup"><span data-stu-id="bb2f5-117">Establish a remote connection toolog on toohello virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="bb2f5-118">Vea Hola instrucciones sobre cómo tooconnect [desde Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [de Linux y Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bb2f5-118">See hello instructions on how tooconnect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="bb2f5-119">De forma predeterminada, SSH permite un máximo de 10 conexiones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="bb2f5-120">Puede aumentar este número editando el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-120">You can increase this number by editing hello configuration file.</span></span>

<span data-ttu-id="bb2f5-121">Si tiene problemas, consulte [Solución de problemas de conexiones de Secure Shell (SSH)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bb2f5-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a><span data-ttu-id="bb2f5-122">¿Puedo usar datos de toostore de saludo disco temporal (/ dev/sdb1)?</span><span class="sxs-lookup"><span data-stu-id="bb2f5-122">Can I use hello temporary disk (/dev/sdb1) toostore data?</span></span>
<span data-ttu-id="bb2f5-123">No use datos de toostore de saludo disco temporal (/ dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="bb2f5-123">Don't use hello temporary disk (/dev/sdb1) toostore data.</span></span> <span data-ttu-id="bb2f5-124">Solo existe para el almacenamiento temporal.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-124">It is only there for temporary storage.</span></span> <span data-ttu-id="bb2f5-125">Corre el riesgo de perder datos que no se podrán recuperar.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="bb2f5-126">¿Puedo copiar o clonar una máquina virtual de Azure existente?</span><span class="sxs-lookup"><span data-stu-id="bb2f5-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="bb2f5-127">Sí.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-127">Yes.</span></span> <span data-ttu-id="bb2f5-128">Para obtener instrucciones, consulte [cómo toocreate una copia de una máquina virtual de Linux en Hola modelo de implementación del Administrador de recursos](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bb2f5-128">For instructions, see [How toocreate a copy of a Linux virtual machine in hello Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="bb2f5-129">¿Por qué no veo las regiones de Canadá central y Canadá oriental por medio de Azure Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="bb2f5-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="bb2f5-130">Hola dos nuevas áreas de Canadá Central y este de Canadá no se registran automáticamente para la creación de máquinas virtuales para las suscripciones de Azure existentes.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-130">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="bb2f5-131">Este registro se realiza automáticamente cuando se implementa una máquina virtual a través de Hola tooany portal Azure otra región con el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-131">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="bb2f5-132">Después de una máquina virtual está implementada tooany otra región de Azure, nuevas áreas de hello deben estar disponibles para máquinas virtuales posteriores.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-132">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="bb2f5-133">¿Puedo agregar una VM de NIC toomy después de crearla?</span><span class="sxs-lookup"><span data-stu-id="bb2f5-133">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="bb2f5-134">Sí, ahora es posible.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-134">Yes, this is now possible.</span></span> <span data-ttu-id="bb2f5-135">Hola VM primera necesidades toobe detenida desasignada.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-135">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="bb2f5-136">A continuación, puede agregar o quitar una NIC (a menos que sea Hola última NIC en hello VM).</span><span class="sxs-lookup"><span data-stu-id="bb2f5-136">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="bb2f5-137">¿Hay algún requisito de nombre de equipo?</span><span class="sxs-lookup"><span data-stu-id="bb2f5-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="bb2f5-138">Sí.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-138">Yes.</span></span> <span data-ttu-id="bb2f5-139">nombre del equipo Hola puede ser un máximo de 64 caracteres de longitud.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-139">hello computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="bb2f5-140">Consulte el artículo sobre las [convenciones y restricciones de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para más información sobre la denominación de los recursos.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="bb2f5-141">¿Existen algunos requisitos para los nombres de grupos de recursos?</span><span class="sxs-lookup"><span data-stu-id="bb2f5-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="bb2f5-142">Sí.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-142">Yes.</span></span> <span data-ttu-id="bb2f5-143">nombre de grupo de recursos de Hello puede tener un máximo de 90 caracteres de longitud.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-143">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="bb2f5-144">Consulte el artículo sobre las [convenciones y restricciones de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para más información sobre los grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="bb2f5-145">¿Cuáles son los requisitos de nombre de usuario de hello al crear una máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="bb2f5-145">What are hello username requirements when creating a VM?</span></span>
<span data-ttu-id="bb2f5-146">Los nombres de usuario deben tener entre 1 y 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="bb2f5-147">no se permite Hola siguiendo los nombres de usuario:</span><span class="sxs-lookup"><span data-stu-id="bb2f5-147">hello following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="bb2f5-148">administrator</span><span class="sxs-lookup"><span data-stu-id="bb2f5-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-149">admin</span><span class="sxs-lookup"><span data-stu-id="bb2f5-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-150">user</span><span class="sxs-lookup"><span data-stu-id="bb2f5-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-151">user1</span><span class="sxs-lookup"><span data-stu-id="bb2f5-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="bb2f5-152">test</span><span class="sxs-lookup"><span data-stu-id="bb2f5-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-153">user2</span><span class="sxs-lookup"><span data-stu-id="bb2f5-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-154">test1</span><span class="sxs-lookup"><span data-stu-id="bb2f5-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-155">user3</span><span class="sxs-lookup"><span data-stu-id="bb2f5-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="bb2f5-156">admin1</span><span class="sxs-lookup"><span data-stu-id="bb2f5-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-157">1</span><span class="sxs-lookup"><span data-stu-id="bb2f5-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-158">123</span><span class="sxs-lookup"><span data-stu-id="bb2f5-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-159">a</span><span class="sxs-lookup"><span data-stu-id="bb2f5-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="bb2f5-160">actuser</span><span class="sxs-lookup"><span data-stu-id="bb2f5-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="bb2f5-161">adm</span><span class="sxs-lookup"><span data-stu-id="bb2f5-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-162">admin2</span><span class="sxs-lookup"><span data-stu-id="bb2f5-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="bb2f5-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="bb2f5-164">backup</span><span class="sxs-lookup"><span data-stu-id="bb2f5-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-165">console</span><span class="sxs-lookup"><span data-stu-id="bb2f5-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-166">david</span><span class="sxs-lookup"><span data-stu-id="bb2f5-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-167">guest</span><span class="sxs-lookup"><span data-stu-id="bb2f5-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="bb2f5-168">john</span><span class="sxs-lookup"><span data-stu-id="bb2f5-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-169">owner</span><span class="sxs-lookup"><span data-stu-id="bb2f5-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-170">root</span><span class="sxs-lookup"><span data-stu-id="bb2f5-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-171">server</span><span class="sxs-lookup"><span data-stu-id="bb2f5-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="bb2f5-172">sql</span><span class="sxs-lookup"><span data-stu-id="bb2f5-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-173">support</span><span class="sxs-lookup"><span data-stu-id="bb2f5-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="bb2f5-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-175">sys</span><span class="sxs-lookup"><span data-stu-id="bb2f5-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="bb2f5-176">test2</span><span class="sxs-lookup"><span data-stu-id="bb2f5-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-177">test3</span><span class="sxs-lookup"><span data-stu-id="bb2f5-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-178">user4</span><span class="sxs-lookup"><span data-stu-id="bb2f5-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="bb2f5-179">user5</span><span class="sxs-lookup"><span data-stu-id="bb2f5-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="bb2f5-180">¿Cuáles son los requisitos de contraseña de hello al crear una máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="bb2f5-180">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="bb2f5-181">Las contraseñas deben tener 6 a 72 caracteres de longitud y cumplen 3 fuera Hola según los requisitos de complejidad 4:</span><span class="sxs-lookup"><span data-stu-id="bb2f5-181">Passwords must be 6 - 72 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="bb2f5-182">Deben incluir caracteres en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-182">Have lower characters</span></span>
* <span data-ttu-id="bb2f5-183">Deben incluir caracteres en mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-183">Have upper characters</span></span>
* <span data-ttu-id="bb2f5-184">Deben incluir un dígito.</span><span class="sxs-lookup"><span data-stu-id="bb2f5-184">Have a digit</span></span>
* <span data-ttu-id="bb2f5-185">Deben incluir un carácter especial (REGEX.MATCH [\W_]).</span><span class="sxs-lookup"><span data-stu-id="bb2f5-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="bb2f5-186">no se permite Hola siguientes contraseñas:</span><span class="sxs-lookup"><span data-stu-id="bb2f5-186">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="bb2f5-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="bb2f5-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="bb2f5-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="bb2f5-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="bb2f5-189">Password!</span><span class="sxs-lookup"><span data-stu-id="bb2f5-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="bb2f5-190">Password1</span><span class="sxs-lookup"><span data-stu-id="bb2f5-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="bb2f5-191">Password22</span><span class="sxs-lookup"><span data-stu-id="bb2f5-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="bb2f5-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="bb2f5-192">iloveyou!</span></span></td>
    </tr>
</table>
