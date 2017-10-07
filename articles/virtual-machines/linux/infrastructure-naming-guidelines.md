---
title: infraestructura de aaaAzure instrucciones - Linux de nomenclatura | Documentos de Microsoft
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para asignar nombres a los servicios de infraestructura de Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="9b376-103">Directrices de nomenclatura de la infraestructura de Azure para máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="9b376-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="9b376-104">En este artículo se centra en describir cómo tooapproach las convenciones de nomenclatura para todos los su toobuild varios recursos de Azure una lógica y fácilmente identificable configuración de recursos en todo el entorno.</span><span class="sxs-lookup"><span data-stu-id="9b376-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="9b376-105">Directrices de implementación para las convenciones de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="9b376-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="9b376-106">Decisiones:</span><span class="sxs-lookup"><span data-stu-id="9b376-106">Decisions:</span></span>

* <span data-ttu-id="9b376-107">¿Cuáles son sus convenciones de nomenclatura para los recursos de Azure?</span><span class="sxs-lookup"><span data-stu-id="9b376-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="9b376-108">Tareas:</span><span class="sxs-lookup"><span data-stu-id="9b376-108">Tasks:</span></span>

* <span data-ttu-id="9b376-109">Definir Hola pondrá toouse a través de la coherencia de toomaintain de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b376-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="9b376-110">Definir la cuenta de almacenamiento nombres Hola requisito para ellos toobe único global.</span><span class="sxs-lookup"><span data-stu-id="9b376-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="9b376-111">Hola de documento toobe de convención de nomenclatura usa y distribuir tooall partes implicadas tooensure coherencia entre implementaciones.</span><span class="sxs-lookup"><span data-stu-id="9b376-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="9b376-112">Convenciones de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="9b376-112">Naming conventions</span></span>
<span data-ttu-id="9b376-113">Debe existir una buena convención de nomenclatura antes de crear cualquier elemento en Azure.</span><span class="sxs-lookup"><span data-stu-id="9b376-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="9b376-114">Una convención de nomenclatura garantiza que todos los recursos de hello tienen un nombre de predicción, lo que ayuda a la menor carga administrativa de hello asociada con la administración de esos recursos.</span><span class="sxs-lookup"><span data-stu-id="9b376-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="9b376-115">Puede elegir toofollow un conjunto específico de convenciones de nomenclatura definidas para toda la organización o para una cuenta o suscripción de Azure específica.</span><span class="sxs-lookup"><span data-stu-id="9b376-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="9b376-116">Aunque resulta fácil para los usuarios dentro de las reglas de las organizaciones tooestablish implícita cuando se trabaja con recursos de Azure, necesitará toobe puede tooscale para los equipos que trabajan juntos en Azure.</span><span class="sxs-lookup"><span data-stu-id="9b376-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, you need toobe able tooscale for teams working together in Azure.</span></span>

<span data-ttu-id="9b376-117">Debe acordar por adelantado el conjunto de convenciones de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="9b376-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="9b376-118">Existen algunas consideraciones sobre las convenciones de nomenclatura que trascienden los conjuntos de reglas.</span><span class="sxs-lookup"><span data-stu-id="9b376-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="9b376-119">Afijos</span><span class="sxs-lookup"><span data-stu-id="9b376-119">Affixes</span></span>
<span data-ttu-id="9b376-120">Cuando examine toodefine una convención de nomenclatura, una decisión es si conviene poner hello en:</span><span class="sxs-lookup"><span data-stu-id="9b376-120">As you look toodefine a naming convention, one decision is whether hello affix is at:</span></span>

* <span data-ttu-id="9b376-121">principio de Hello del nombre de hello (prefijo)</span><span class="sxs-lookup"><span data-stu-id="9b376-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="9b376-122">final de Hello del nombre de hello (sufijo)</span><span class="sxs-lookup"><span data-stu-id="9b376-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="9b376-123">Por ejemplo, presentamos dos nombres posibles para un grupo de recursos con hello `rg` colocará:</span><span class="sxs-lookup"><span data-stu-id="9b376-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="9b376-124">Rg-WebApp (prefijo)</span><span class="sxs-lookup"><span data-stu-id="9b376-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="9b376-125">WebApp-Rg (sufijo)</span><span class="sxs-lookup"><span data-stu-id="9b376-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="9b376-126">Pondrá puede hacer referencia a aspectos de toodifferent que se describen los recursos específicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b376-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="9b376-127">Hello tabla siguiente muestran algunos ejemplos que se utilizan normalmente.</span><span class="sxs-lookup"><span data-stu-id="9b376-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="9b376-128">Aspecto</span><span class="sxs-lookup"><span data-stu-id="9b376-128">Aspect</span></span> | <span data-ttu-id="9b376-129">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="9b376-129">Examples</span></span> | <span data-ttu-id="9b376-130">Notas</span><span class="sxs-lookup"><span data-stu-id="9b376-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="9b376-131">Environment</span><span class="sxs-lookup"><span data-stu-id="9b376-131">Environment</span></span> |<span data-ttu-id="9b376-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="9b376-132">dev, stg, prod</span></span> |<span data-ttu-id="9b376-133">Según el propósito de Hola y el nombre de cada entorno.</span><span class="sxs-lookup"><span data-stu-id="9b376-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="9b376-134">Ubicación</span><span class="sxs-lookup"><span data-stu-id="9b376-134">Location</span></span> |<span data-ttu-id="9b376-135">usw (Oeste de EE. UU.), use (Este de EE. UU. 2)</span><span class="sxs-lookup"><span data-stu-id="9b376-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="9b376-136">Función de la región Hola del centro de datos de Hola o región de Hola de organización de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b376-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="9b376-137">Componente, servicio o producto de Azure</span><span class="sxs-lookup"><span data-stu-id="9b376-137">Azure component, service, or product</span></span> |<span data-ttu-id="9b376-138">Rg para grupo de recursos, VNet para red virtual</span><span class="sxs-lookup"><span data-stu-id="9b376-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="9b376-139">Dependiendo del producto Hola para qué hello recurso proporciona soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="9b376-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="9b376-140">Rol</span><span class="sxs-lookup"><span data-stu-id="9b376-140">Role</span></span> |<span data-ttu-id="9b376-141">bd, aplicación, web</span><span class="sxs-lookup"><span data-stu-id="9b376-141">db, app, web</span></span> |<span data-ttu-id="9b376-142">Dependiendo de la función hello de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b376-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="9b376-143">Instance</span><span class="sxs-lookup"><span data-stu-id="9b376-143">Instance</span></span> |<span data-ttu-id="9b376-144">01, 02, 03, etc.</span><span class="sxs-lookup"><span data-stu-id="9b376-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="9b376-145">Para los recursos que pueden tener más de una instancia.</span><span class="sxs-lookup"><span data-stu-id="9b376-145">For resources that have more than one instance.</span></span> <span data-ttu-id="9b376-146">Por ejemplo, servidores web de carga equilibrada en un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="9b376-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="9b376-147">Al establecer las convenciones de nomenclatura, asegúrese de que especifican claramente que pondrá toouse para cada tipo de recurso y en qué posición (sufijo de vs de prefijo).</span><span class="sxs-lookup"><span data-stu-id="9b376-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="9b376-148">Fechas</span><span class="sxs-lookup"><span data-stu-id="9b376-148">Dates</span></span>
<span data-ttu-id="9b376-149">A menudo resulta importante toodetermine fecha de Hola de creación de un recurso de nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b376-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="9b376-150">Se recomienda el formato de fecha de hello AAAAMMDD.</span><span class="sxs-lookup"><span data-stu-id="9b376-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="9b376-151">Este formato garantiza que no solo es Hola completa se registra la fecha, pero también que dos recursos cuyos nombres únicamente se diferencian en fecha Hola se ordenan alfabéticamente y cronológicamente.</span><span class="sxs-lookup"><span data-stu-id="9b376-151">This format ensures that not only is hello full date is recorded, but also that two resources whose names differ only on hello date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="9b376-152">Asignación de nombres a recursos</span><span class="sxs-lookup"><span data-stu-id="9b376-152">Naming resources</span></span>
<span data-ttu-id="9b376-153">Definir cada tipo de recurso de convención de nomenclatura de hello, que debe tener reglas que definen cómo tooassign nombres tooeach recursos que se crea.</span><span class="sxs-lookup"><span data-stu-id="9b376-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="9b376-154">Estas reglas deben aplicar tooall tipos de recursos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9b376-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="9b376-155">Suscripciones</span><span class="sxs-lookup"><span data-stu-id="9b376-155">Subscriptions</span></span>
* <span data-ttu-id="9b376-156">Cuentas</span><span class="sxs-lookup"><span data-stu-id="9b376-156">Accounts</span></span>
* <span data-ttu-id="9b376-157">Cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="9b376-157">Storage accounts</span></span>
* <span data-ttu-id="9b376-158">Redes virtuales</span><span class="sxs-lookup"><span data-stu-id="9b376-158">Virtual networks</span></span>
* <span data-ttu-id="9b376-159">Subredes</span><span class="sxs-lookup"><span data-stu-id="9b376-159">Subnets</span></span>
* <span data-ttu-id="9b376-160">Conjuntos de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="9b376-160">Availability sets</span></span>
* <span data-ttu-id="9b376-161">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="9b376-161">Resource groups</span></span>
* <span data-ttu-id="9b376-162">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9b376-162">Virtual machines</span></span>
* <span data-ttu-id="9b376-163">Extremos</span><span class="sxs-lookup"><span data-stu-id="9b376-163">Endpoints</span></span>
* <span data-ttu-id="9b376-164">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="9b376-164">Network security groups</span></span>
* <span data-ttu-id="9b376-165">Roles</span><span class="sxs-lookup"><span data-stu-id="9b376-165">Roles</span></span>

<span data-ttu-id="9b376-166">tooensure que Hola nombre proporciona suficientes recursos de información toodetermine toowhich hace referencia, debe usar nombres descriptivos.</span><span class="sxs-lookup"><span data-stu-id="9b376-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="9b376-167">Nombres de equipo</span><span class="sxs-lookup"><span data-stu-id="9b376-167">Computer names</span></span>
<span data-ttu-id="9b376-168">Cuando se crea una máquina virtual (VM), Azure requiere un nombre de VM de los caracteres de too64 que se usa para el nombre del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b376-168">When you create a virtual machine (VM), Azure requires a VM name of up too64 characters that is used for hello resource name.</span></span> <span data-ttu-id="9b376-169">Azure usa Hola mismo nombre para el sistema de operativo Hola instalado Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9b376-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="9b376-170">Sin embargo, estos nombres pueden no siempre se Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="9b376-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="9b376-171">Si se crea una máquina virtual desde un archivo de imagen .vhd que ya contiene un sistema operativo, nombre de la máquina virtual de hello en Azure puede diferir de hello nombre de equipo del sistema operativo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9b376-171">If a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="9b376-172">Esta situación puede agregar un grado de administración de tooVM de dificultad, que por lo tanto, no se recomienda.</span><span class="sxs-lookup"><span data-stu-id="9b376-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="9b376-173">Asignar Hola Hola de recursos de máquina virtual de Azure mismo nombre como nombre de equipo de Hola que asigne el sistema de operativo toohello de esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9b376-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="9b376-174">Se recomienda ese nombre de máquina virtual de Azure hello es Hola igual que Hola subyacente nombre de equipo del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="9b376-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="9b376-175">Nombres de cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="9b376-175">Storage account names</span></span>
<span data-ttu-id="9b376-176">En esta sección no se aplica demasiado[discos de Azure administrados](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ya que no se cree una cuenta de almacenamiento independiente.</span><span class="sxs-lookup"><span data-stu-id="9b376-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="9b376-177">En los discos no administrados, las cuentas de almacenamiento tienen reglas especiales que regulan sus nombres.</span><span class="sxs-lookup"><span data-stu-id="9b376-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="9b376-178">Sólo puede utilizar minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="9b376-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="9b376-179">Para obtener más información, consulte [Creación de una cuenta de almacenamiento](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="9b376-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="9b376-180">Además, nombre de cuenta de almacenamiento de hello, con core.windows.net, debe tener un nombre DNS válido globalmente único.</span><span class="sxs-lookup"><span data-stu-id="9b376-180">Additionally, hello storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="9b376-181">Por ejemplo, si se llama a la cuenta de almacenamiento de hello mystorageaccount, hello siguientes nombres DNS resultantes deben ser únicos:</span><span class="sxs-lookup"><span data-stu-id="9b376-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="9b376-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="9b376-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="9b376-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="9b376-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="9b376-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="9b376-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b376-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b376-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

