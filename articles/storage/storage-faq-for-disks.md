---
title: "Preguntas más frecuentes (P+F) sobre los discos de máquina virtual de IaaS de Azure | Microsoft Docs"
description: "Preguntas más frecuentes sobre los discos de máquina virtual de IaaS de Azure y los discos premium (administrados y no administrados)"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 9e5eed35334f1b95441b8181c8e90645be78b389
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="3ed89-103">Preguntas más frecuentes sobre los discos de máquina virtual de IaaS de Azure y los discos premium administrados y no administrados</span><span class="sxs-lookup"><span data-stu-id="3ed89-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="3ed89-104">En este artículo se responden algunas de las preguntas más frecuentes acerca de Azure Managed Disks y Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="3ed89-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="3ed89-105">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="3ed89-105">Managed Disks</span></span>

<span data-ttu-id="3ed89-106">**¿Qué es Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="3ed89-107">Managed Disks es una característica que simplifica la administración de discos para máquinas virtuales de IaaS de Azure al controlar automáticamente la administración de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3ed89-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="3ed89-108">Para obtener más información, consulte [Introducción a Azure Managed Disks](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ed89-108">For more information, see the [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="3ed89-109">**Si creo un disco administrado estándar a partir un disco duro virtual existente con 80 GB de tamaño, ¿cuánto me costará?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="3ed89-110">Un disco administrado estándar creado a partir de un disco duro virtual de 80 GB se trata como el siguiente tamaño de disco estándar disponible, es decir, un disco S10.</span><span class="sxs-lookup"><span data-stu-id="3ed89-110">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="3ed89-111">Se le cobrará según el precio de disco S10.</span><span class="sxs-lookup"><span data-stu-id="3ed89-111">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="3ed89-112">Consulte la [página de precios](https://azure.microsoft.com/pricing/details/storage)para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="3ed89-112">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="3ed89-113">**¿Existen costes de transacción para los discos administrados estándar?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="3ed89-114">Sí.</span><span class="sxs-lookup"><span data-stu-id="3ed89-114">Yes.</span></span> <span data-ttu-id="3ed89-115">Sí, se le cobrará por cada transacción.</span><span class="sxs-lookup"><span data-stu-id="3ed89-115">You're charged for each transaction.</span></span> <span data-ttu-id="3ed89-116">Consulte la [página de precios](https://azure.microsoft.com/pricing/details/storage)para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="3ed89-116">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="3ed89-117">**Para un disco administrado estándar, ¿se me cobrará por el tamaño real de los datos en el disco o la capacidad aprovisionada del disco?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-117">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="3ed89-118">Se le cobra en función de la capacidad aprovisionada del disco.</span><span class="sxs-lookup"><span data-stu-id="3ed89-118">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="3ed89-119">Consulte la [página de precios](https://azure.microsoft.com/pricing/details/storage)para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="3ed89-119">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="3ed89-120">**¿En qué se diferencian los precios de los discos administrados premium de los de los discos no administrados?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="3ed89-121">Los precios de los discos administrados premium son iguales que los de los discos no administrados premium.</span><span class="sxs-lookup"><span data-stu-id="3ed89-121">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="3ed89-122">**¿Puedo cambiar el tipo de cuenta de almacenamiento (Estándar o Premium) de mis discos administrados?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-122">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="3ed89-123">Sí.</span><span class="sxs-lookup"><span data-stu-id="3ed89-123">Yes.</span></span> <span data-ttu-id="3ed89-124">Puede cambiar el tipo de cuenta de almacenamiento de los discos administrados mediante Azure Portal, PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="3ed89-124">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="3ed89-125">**¿Hay alguna manera de copiar o exportar un disco administrado a una cuenta de almacenamiento privada?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-125">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="3ed89-126">Sí.</span><span class="sxs-lookup"><span data-stu-id="3ed89-126">Yes.</span></span> <span data-ttu-id="3ed89-127">Puede exportar los discos administrados mediante Azure Portal, PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="3ed89-127">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="3ed89-128">**¿Puedo usar un archivo de disco duro virtual en una cuenta de Azure Storage para crear un disco administrado con una suscripción distinta?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-128">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="3ed89-129">No.</span><span class="sxs-lookup"><span data-stu-id="3ed89-129">No.</span></span>

<span data-ttu-id="3ed89-130">**¿Puedo usar un archivo de disco duro virtual en una cuenta de Azure Storage para crear un disco administrado en una región diferente?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-130">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="3ed89-131">No.</span><span class="sxs-lookup"><span data-stu-id="3ed89-131">No.</span></span>

<span data-ttu-id="3ed89-132">**¿Hay alguna limitación de escala para los clientes que usen discos administrados?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="3ed89-133">Managed Disks elimina los límites asociados a las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3ed89-133">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="3ed89-134">Aun así, el número de discos administrados por suscripción está limitado a 2000 de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3ed89-134">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="3ed89-135">Puede llamar al soporte técnico para aumentar este número.</span><span class="sxs-lookup"><span data-stu-id="3ed89-135">You can call support to increase this number.</span></span>

<span data-ttu-id="3ed89-136">**¿Puedo tomar una instantánea incremental de un disco administrado?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="3ed89-137">No.</span><span class="sxs-lookup"><span data-stu-id="3ed89-137">No.</span></span> <span data-ttu-id="3ed89-138">La funcionalidad de instantánea actual realiza una copia completa de un disco administrado.</span><span class="sxs-lookup"><span data-stu-id="3ed89-138">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="3ed89-139">Sin embargo, está previsto admitir instantáneas incrementales en el futuro.</span><span class="sxs-lookup"><span data-stu-id="3ed89-139">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="3ed89-140">**¿Pueden las máquinas virtuales de un conjunto de disponibilidad estar compuestas de una combinación de discos administrados y no administrados?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="3ed89-141">No.</span><span class="sxs-lookup"><span data-stu-id="3ed89-141">No.</span></span> <span data-ttu-id="3ed89-142">Las máquinas virtuales de un conjunto de disponibilidad deben utilizar únicamente discos administrados o no administrados.</span><span class="sxs-lookup"><span data-stu-id="3ed89-142">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="3ed89-143">Cuando cree un conjunto de disponibilidad, puede elegir qué tipo de discos desea usar.</span><span class="sxs-lookup"><span data-stu-id="3ed89-143">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="3ed89-144">**¿Es Managed Disks la opción predeterminada en Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-144">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="3ed89-145">No actualmente, pero lo será en el futuro.</span><span class="sxs-lookup"><span data-stu-id="3ed89-145">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="3ed89-146">**¿Puedo crear un disco administrado vacío?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="3ed89-147">Sí.</span><span class="sxs-lookup"><span data-stu-id="3ed89-147">Yes.</span></span> <span data-ttu-id="3ed89-148">Puede crear un disco vacío.</span><span class="sxs-lookup"><span data-stu-id="3ed89-148">You can create an empty disk.</span></span> <span data-ttu-id="3ed89-149">Un disco administrado se puede crear de forma independiente de una máquina virtual, por ejemplo, sin conectarlo a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3ed89-149">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="3ed89-150">**¿Qué número de dominios de error se admite para un conjunto de disponibilidad que use Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-150">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="3ed89-151">En función de la región en la que se encuentre el conjunto de disponibilidad que use Managed Disks, el número de dominios de error admitidos es de 2 o 3.</span><span class="sxs-lookup"><span data-stu-id="3ed89-151">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="3ed89-152">**¿Cómo se configura una cuenta de almacenamiento estándar para el diagnóstico?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-152">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="3ed89-153">Se configura una cuenta de almacenamiento privada para el diagnóstico de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3ed89-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="3ed89-154">En el futuro, está previsto cambiar también el diagnóstico a Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="3ed89-154">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="3ed89-155">**¿Qué tipo de compatibilidad con el Control de acceso basado en roles está disponible para Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="3ed89-156">Managed Disks admite tres roles predeterminados fundamentales:</span><span class="sxs-lookup"><span data-stu-id="3ed89-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="3ed89-157">Propietario: puede administrar todo, incluido el acceso.</span><span class="sxs-lookup"><span data-stu-id="3ed89-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="3ed89-158">Colaborador: puede administrar todo, excepto el acceso.</span><span class="sxs-lookup"><span data-stu-id="3ed89-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="3ed89-159">Lector: puede ver todo, pero no realizar cambios.</span><span class="sxs-lookup"><span data-stu-id="3ed89-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="3ed89-160">**¿Hay alguna manera de copiar o exportar un disco administrado a una cuenta de almacenamiento privada?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-160">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="3ed89-161">Puede obtener un identificador URI de firma de acceso compartido de solo lectura para el disco administrado y usarlo para copiar el contenido a una cuenta de almacenamiento privada o al almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="3ed89-161">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="3ed89-162">**¿Puedo crear una copia de mi disco administrado?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="3ed89-163">Los clientes pueden crear una instantánea de sus discos administrados y usarla para crear otro disco administrado.</span><span class="sxs-lookup"><span data-stu-id="3ed89-163">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="3ed89-164">**¿Siguen siendo compatibles los discos no administrados?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="3ed89-165">Sí.</span><span class="sxs-lookup"><span data-stu-id="3ed89-165">Yes.</span></span> <span data-ttu-id="3ed89-166">Admitimos discos administrados y no administrados.</span><span class="sxs-lookup"><span data-stu-id="3ed89-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="3ed89-167">Recomendamos que empiece a usar discos administrados para las cargas de trabajo nuevas y migre las cargas de trabajo actuales a discos administrados.</span><span class="sxs-lookup"><span data-stu-id="3ed89-167">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="3ed89-168">**Si creo un disco de 128 GB y después lo aumento a 130 GB, ¿se me cobrará por el siguiente tamaño de disco (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-168">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="3ed89-169">Sí.</span><span class="sxs-lookup"><span data-stu-id="3ed89-169">Yes.</span></span>

<span data-ttu-id="3ed89-170">**¿Puedo crear discos administrados para el almacenamiento con redundancia local, almacenamiento con redundancia geográfica y almacenamiento con redundancia de zona?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="3ed89-171">Actualmente, Azure Managed Disks solo admite discos administrados de almacenamiento con redundancia local.</span><span class="sxs-lookup"><span data-stu-id="3ed89-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="3ed89-172">**¿Puedo reducir mis discos administrados?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="3ed89-173">No.</span><span class="sxs-lookup"><span data-stu-id="3ed89-173">No.</span></span> <span data-ttu-id="3ed89-174">En la actualidad no se admite esta característica.</span><span class="sxs-lookup"><span data-stu-id="3ed89-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="3ed89-175">**¿Se puede cambiar la propiedad de nombre de equipo cuando se usa un disco de sistema operativo especializado (no creado mediante la herramienta de preparación del sistema o generalizado) para aprovisionar una máquina virtual?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-175">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="3ed89-176">No.</span><span class="sxs-lookup"><span data-stu-id="3ed89-176">No.</span></span> <span data-ttu-id="3ed89-177">No se puede actualizar la propiedad de nombre de equipo.</span><span class="sxs-lookup"><span data-stu-id="3ed89-177">You can't update the computer name property.</span></span> <span data-ttu-id="3ed89-178">La nueva máquina virtual lo hereda de la máquina virtual principal que se usó para crear el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="3ed89-178">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="3ed89-179">**¿Dónde puedo encontrar plantillas de Azure Resource Manager de ejemplo para crear máquinas virtuales con discos administrados**</span><span class="sxs-lookup"><span data-stu-id="3ed89-179">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="3ed89-180">Lista de plantillas mediante discos administrados</span><span class="sxs-lookup"><span data-stu-id="3ed89-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="3ed89-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="3ed89-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="3ed89-182">Managed Disks y Storage Service Encryption</span><span class="sxs-lookup"><span data-stu-id="3ed89-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="3ed89-183">**¿Está habilitado el servicio Storage Service Encryption de forma predeterminada al crear un disco administrado?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="3ed89-184">Sí.</span><span class="sxs-lookup"><span data-stu-id="3ed89-184">Yes.</span></span>

<span data-ttu-id="3ed89-185">**¿Quién administra las claves de cifrado?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-185">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="3ed89-186">Microsoft administra las claves de cifrado.</span><span class="sxs-lookup"><span data-stu-id="3ed89-186">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="3ed89-187">**¿Puedo deshabilitar Storage Service Encryption para Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="3ed89-188">No.</span><span class="sxs-lookup"><span data-stu-id="3ed89-188">No.</span></span>

<span data-ttu-id="3ed89-189">**¿Storage Service Encryption está solo disponible en determinadas regiones?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="3ed89-190">No.</span><span class="sxs-lookup"><span data-stu-id="3ed89-190">No.</span></span> <span data-ttu-id="3ed89-191">Está en todas las regiones donde esté disponible Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="3ed89-191">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="3ed89-192">Managed Disks está disponible en todas las regiones públicas y Alemania.</span><span class="sxs-lookup"><span data-stu-id="3ed89-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="3ed89-193">**¿Cómo averiguo si mi disco administrado está cifrado?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="3ed89-194">Puede averiguar la hora de creación de un disco administrado desde Azure Portal, la CLI de Azure y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ed89-194">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="3ed89-195">Si la hora es posterior al 9 de junio de 2017, el disco está cifrado.</span><span class="sxs-lookup"><span data-stu-id="3ed89-195">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="3ed89-196">**¿Cómo puedo cifrar mis discos existentes que se crearon antes del 10 de junio de 2017?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="3ed89-197">A partir del 10 de junio de 2017 los nuevos datos escritos en los discos administrados existentes se cifran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3ed89-197">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="3ed89-198">También tenemos previsto cifrar los datos existentes y el cifrado se realizará de forma asincrónica en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="3ed89-198">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="3ed89-199">Si debe cifrar ahora los datos existentes, cree una copia del disco.</span><span class="sxs-lookup"><span data-stu-id="3ed89-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="3ed89-200">Los discos nuevos se cifrarán.</span><span class="sxs-lookup"><span data-stu-id="3ed89-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="3ed89-201">Copia de discos administrados mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3ed89-201">Copy managed disks by using the Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="3ed89-202">Copia de discos administrados mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ed89-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="3ed89-203">**¿Están cifradas las imágenes e instantáneas administradas?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="3ed89-204">Sí.</span><span class="sxs-lookup"><span data-stu-id="3ed89-204">Yes.</span></span> <span data-ttu-id="3ed89-205">Todas las instantáneas e imágenes administradas creadas después del 9 de junio de 2017 se cifran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3ed89-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="3ed89-206">**¿Puedo convertir máquinas virtuales con discos no administrados que se encuentran en las cuentas de almacenamiento o que se hayan cifrado previamente en discos administrados?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="3ed89-207">Sí</span><span class="sxs-lookup"><span data-stu-id="3ed89-207">Yes</span></span>

<span data-ttu-id="3ed89-208">**¿Se cifrará también un VHD exportado de un disco administrado o de una instantánea?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="3ed89-209">No.</span><span class="sxs-lookup"><span data-stu-id="3ed89-209">No.</span></span> <span data-ttu-id="3ed89-210">Pero si exporta un disco duro virtual a una cuenta de almacenamiento cifrada desde un disco administrado cifrado o una instantánea, en este caso se cifra.</span><span class="sxs-lookup"><span data-stu-id="3ed89-210">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="3ed89-211">Discos premium: tanto administrados como no administrados</span><span class="sxs-lookup"><span data-stu-id="3ed89-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="3ed89-212">**Si una máquina virtual usa una serie de tamaño que admite Premium Storage, como DSv2, ¿puedo conectar discos de datos tanto premium como estándar?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="3ed89-213">Sí.</span><span class="sxs-lookup"><span data-stu-id="3ed89-213">Yes.</span></span>

<span data-ttu-id="3ed89-214">**¿Puedo conectar discos de datos tanto premium como estándar a una serie de tamaño que no admita Premium Storage, por ejemplo, las series D, Dv2, G o F?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-214">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="3ed89-215">No.</span><span class="sxs-lookup"><span data-stu-id="3ed89-215">No.</span></span> <span data-ttu-id="3ed89-216">Solo puede conectar discos de datos estándar a máquinas virtuales que no utilicen una serie de tamaño que admita Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="3ed89-216">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="3ed89-217">**Si creo un disco de datos premium a partir un disco duro virtual existente con 80 GB, ¿cuánto me costará?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="3ed89-218">Un disco de datos premium creado a partir de un disco duro virtual de 80 GB se trata como el siguiente tamaño de disco premium disponible, es decir, P10.</span><span class="sxs-lookup"><span data-stu-id="3ed89-218">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="3ed89-219">Se le cobrará según el precio de disco P10.</span><span class="sxs-lookup"><span data-stu-id="3ed89-219">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="3ed89-220">**¿Hay costos de transacción cuando se usa Premium Storage?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-220">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="3ed89-221">Existe un costo fijo para cada tamaño de disco que esté aprovisionado con límites específicos de IOPS y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="3ed89-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="3ed89-222">Los demás costes son por el ancho de banda de salida y la capacidad para instantáneas, si corresponde.</span><span class="sxs-lookup"><span data-stu-id="3ed89-222">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="3ed89-223">Consulte la [página de precios](https://azure.microsoft.com/pricing/details/storage)para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="3ed89-223">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="3ed89-224">**¿Cuáles son los límites de IOPS y rendimiento que puedo obtener de la caché de disco?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-224">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="3ed89-225">Los límites combinados de memoria caché y SSD local para la serie DS son 4,000 IOPS por núcleo y 33 MB por segundo y núcleo.</span><span class="sxs-lookup"><span data-stu-id="3ed89-225">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="3ed89-226">La serie GS ofrece 5000 IOPS por núcleo y 50 MB por segundo y núcleo.</span><span class="sxs-lookup"><span data-stu-id="3ed89-226">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="3ed89-227">**¿Es el SSD local compatible con máquinas virtuales de Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-227">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="3ed89-228">El SSD local es un almacenamiento temporal que se incluye con una máquina virtual de discos administrados.</span><span class="sxs-lookup"><span data-stu-id="3ed89-228">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="3ed89-229">No existe ningún costo extra para este almacenamiento temporal.</span><span class="sxs-lookup"><span data-stu-id="3ed89-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="3ed89-230">Recomendamos que no use este SSD local para almacenar los datos de la aplicación, ya que no se conserva en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="3ed89-230">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="3ed89-231">**¿Hay alguna repercusión en el uso de TRIM en discos premium?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-231">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="3ed89-232">No hay ningún inconveniente a la hora de usar TRIM en discos de Azure, ya sea en discos estándar o premium.</span><span class="sxs-lookup"><span data-stu-id="3ed89-232">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="3ed89-233">Nuevos tamaños de discos: tanto administrados como no administrados</span><span class="sxs-lookup"><span data-stu-id="3ed89-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="3ed89-234">**¿Cuál es el mayor tamaño de disco compatible con discos de datos y sistema operativo?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-234">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="3ed89-235">El tipo de partición compatible con Azure para un disco del sistema operativo es el registro de arranque maestro (MBR).</span><span class="sxs-lookup"><span data-stu-id="3ed89-235">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="3ed89-236">El formato MBR admite un disco de hasta 2 TB.</span><span class="sxs-lookup"><span data-stu-id="3ed89-236">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="3ed89-237">El tamaño máximo admitido por Azure para un disco del sistema operativo es de 2 TB.</span><span class="sxs-lookup"><span data-stu-id="3ed89-237">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="3ed89-238">Azure admite hasta 4 TB para discos de datos.</span><span class="sxs-lookup"><span data-stu-id="3ed89-238">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="3ed89-239">**¿Cuál es el mayor tamaño de blob en páginas admitido?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-239">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="3ed89-240">El mayor tamaño blob en páginas que admite Azure es 8 TB (8191 GB).</span><span class="sxs-lookup"><span data-stu-id="3ed89-240">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="3ed89-241">No se admiten blobs en páginas mayores de 4 TB (4095 GB) conectados a una máquina virtual como discos de datos o de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="3ed89-241">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="3ed89-242">**¿Es necesario usar una nueva versión de las herramientas de Azure para crear, conectar, cambiar el tamaño y cargar discos de más de 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-242">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="3ed89-243">No es necesario actualizar las herramientas de Azure existentes para crear, conectar o cambiar el tamaño de los discos de más de 1 TB.</span><span class="sxs-lookup"><span data-stu-id="3ed89-243">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="3ed89-244">Para cargar el archivo de disco duro virtual del entorno local directamente en Azure como un blob en páginas o un disco no administrado, debe usar los conjuntos de herramientas más recientes:</span><span class="sxs-lookup"><span data-stu-id="3ed89-244">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="3ed89-245">Herramientas de Azure</span><span class="sxs-lookup"><span data-stu-id="3ed89-245">Azure tools</span></span>      | <span data-ttu-id="3ed89-246">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="3ed89-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="3ed89-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ed89-247">Azure PowerShell</span></span> | <span data-ttu-id="3ed89-248">Número de versión 4.1.0: versión de junio de 2017 o posterior</span><span class="sxs-lookup"><span data-stu-id="3ed89-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="3ed89-249">CLI de Azure v1</span><span class="sxs-lookup"><span data-stu-id="3ed89-249">Azure CLI v1</span></span>     | <span data-ttu-id="3ed89-250">Número de versión 0.10.13: versión de mayo de 2017 o posterior</span><span class="sxs-lookup"><span data-stu-id="3ed89-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="3ed89-251">AzCopy</span><span class="sxs-lookup"><span data-stu-id="3ed89-251">AzCopy</span></span>           | <span data-ttu-id="3ed89-252">Número de versión 6.1.0: versión de junio de 2017 o posterior</span><span class="sxs-lookup"><span data-stu-id="3ed89-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="3ed89-253">La compatibilidad con CLI de Azure v2 y Azure Storage Explorer estará disponible próximamente.</span><span class="sxs-lookup"><span data-stu-id="3ed89-253">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="3ed89-254">**¿Se admiten los tamaños de disco P4 y P6 para blobs en páginas o discos no administrados?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="3ed89-255">No.</span><span class="sxs-lookup"><span data-stu-id="3ed89-255">No.</span></span> <span data-ttu-id="3ed89-256">Los tamaños de disco P4 (32 GB) y P6 (64 GB) solo son compatibles con discos administrados.</span><span class="sxs-lookup"><span data-stu-id="3ed89-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="3ed89-257">La compatibilidad para blobs en páginas y discos no administrados estará disponible próximamente.</span><span class="sxs-lookup"><span data-stu-id="3ed89-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="3ed89-258">**Si mi disco administrado premium existente de menos de 64 GB se creó antes de habilitar el disco pequeño (alrededor del 15 de junio de 2017), ¿cómo se factura?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-258">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="3ed89-259">Los discos pequeños premium de menos de 64 GB se siguen facturando según el plan de tarifa P10.</span><span class="sxs-lookup"><span data-stu-id="3ed89-259">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="3ed89-260">**¿Cómo puedo cambiar el nivel de disco de los discos pequeños premium menores de 64 GB de P10 a P4 o P6?**</span><span class="sxs-lookup"><span data-stu-id="3ed89-260">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="3ed89-261">Puede crear una instantánea de los discos pequeños y, después, crear un disco para cambiar automáticamente el plan de tarifa a P4 o P6, en función del tamaño aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="3ed89-261">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="3ed89-262">Mi pregunta no está respondida aquí. ¿Qué debo hacer?</span><span class="sxs-lookup"><span data-stu-id="3ed89-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="3ed89-263">Si su pregunta no aparece aquí, háganoslo saber y lo ayudaremos a encontrar una respuesta.</span><span class="sxs-lookup"><span data-stu-id="3ed89-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="3ed89-264">Puede publicar una pregunta al final de este artículo en los comentarios.</span><span class="sxs-lookup"><span data-stu-id="3ed89-264">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="3ed89-265">Para ponerse en contacto con el equipo de Azure Storage y otros miembros de la Comunidad sobre este artículo, use el [foro de Azure Storage](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata) de MSDN.</span><span class="sxs-lookup"><span data-stu-id="3ed89-265">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="3ed89-266">Para solicitar características, envíe sus solicitudes e ideas al [foro de comentarios de Azure Storage](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="3ed89-266">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
