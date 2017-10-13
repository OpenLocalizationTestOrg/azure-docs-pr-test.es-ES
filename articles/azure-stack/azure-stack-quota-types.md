---
title: Tipos de cuota en Azure Stack | Microsoft Docs
description: Repase los diferentes tipos de cuota disponibles para los servicios y recursos de Azure Stack.
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/23/2017
ms.author: erikje
ms.openlocfilehash: 33906514955b76a3d6587b19899a0c76a09018a2
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="quota-types-in-azure-stack"></a><span data-ttu-id="7fc19-103">Tipos de cuota en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7fc19-103">Quota types in Azure Stack</span></span>

<span data-ttu-id="7fc19-104">*Se aplica a: Sistemas integrados de Azure Stack y Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="7fc19-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="7fc19-105">Las [cuotas](azure-stack-plan-offer-quota-overview.md#plans) definen los límites de recursos que puede aprovisionar o consumir una suscripción de usuario.</span><span class="sxs-lookup"><span data-stu-id="7fc19-105">[Quotas](azure-stack-plan-offer-quota-overview.md#plans) define the limits of resources that a user subscription can provision or consume.</span></span> <span data-ttu-id="7fc19-106">Por ejemplo, una cuota podría permitir que un usuario creara hasta cinco máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="7fc19-106">For example, a quota might allow a user to create up to five VMs.</span></span> <span data-ttu-id="7fc19-107">Cada recurso puede tener sus propios tipos de cuotas.</span><span class="sxs-lookup"><span data-stu-id="7fc19-107">Each resource can have its own types of quotas.</span></span>

## <a name="compute-quota-types"></a><span data-ttu-id="7fc19-108">Tipos de cuota de proceso</span><span class="sxs-lookup"><span data-stu-id="7fc19-108">Compute quota types</span></span>
| <span data-ttu-id="7fc19-109">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="7fc19-109">**Type**</span></span> | <span data-ttu-id="7fc19-110">**Valor predeterminado**</span><span class="sxs-lookup"><span data-stu-id="7fc19-110">**Default value**</span></span> | <span data-ttu-id="7fc19-111">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="7fc19-111">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7fc19-112">Número máximo de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7fc19-112">Max number of virtual machines</span></span> |<span data-ttu-id="7fc19-113">50</span><span class="sxs-lookup"><span data-stu-id="7fc19-113">50</span></span> | <span data-ttu-id="7fc19-114">El número máximo de máquinas virtuales que puede crear una suscripción en esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-114">The maximum number of virtual machines that a subscription can create in this location.</span></span> |
| <span data-ttu-id="7fc19-115">Número máximo de núcleos de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7fc19-115">Max number of virtual machine cores</span></span> |<span data-ttu-id="7fc19-116">100</span><span class="sxs-lookup"><span data-stu-id="7fc19-116">100</span></span> | <span data-ttu-id="7fc19-117">El número máximo de núcleos que puede crear una suscripción en esta ubicación (por ejemplo, una máquina virtual A3 tiene cuatro núcleos).</span><span class="sxs-lookup"><span data-stu-id="7fc19-117">The maximum number of cores that a subscription can create in this location (for example, an A3 VM has four cores).</span></span> |
| <span data-ttu-id="7fc19-118">Número máximo de conjuntos de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="7fc19-118">Max number of availability sets</span></span> |<span data-ttu-id="7fc19-119">10</span><span class="sxs-lookup"><span data-stu-id="7fc19-119">10</span></span> | <span data-ttu-id="7fc19-120">El número máximo de conjuntos de disponibilidad que se pueden crear en esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-120">The maximum number of availability sets that can be created in this location.</span></span> |
| <span data-ttu-id="7fc19-121">Número máximo de conjuntos de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7fc19-121">Max number of virtual machine scale sets</span></span> |<span data-ttu-id="7fc19-122">100</span><span class="sxs-lookup"><span data-stu-id="7fc19-122">100</span></span> | <span data-ttu-id="7fc19-123">El número máximo de conjuntos de escalado de máquinas virtuales que se pueden crear en esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-123">The maximum number of virtual machine scale sets that can be created in this location.</span></span> |

> [!NOTE]
> <span data-ttu-id="7fc19-124">Las cuotas de proceso no se aplican a esta versión preliminar técnica.</span><span class="sxs-lookup"><span data-stu-id="7fc19-124">Compute quotas are not enforced in this technical preview.</span></span>
> 
> 

## <a name="storage-quota-types"></a><span data-ttu-id="7fc19-125">Tipos de cuotas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="7fc19-125">Storage quota types</span></span>
| <span data-ttu-id="7fc19-126">**Elemento**</span><span class="sxs-lookup"><span data-stu-id="7fc19-126">**Item**</span></span> | <span data-ttu-id="7fc19-127">**Valor predeterminado**</span><span class="sxs-lookup"><span data-stu-id="7fc19-127">**Default value**</span></span> | <span data-ttu-id="7fc19-128">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="7fc19-128">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7fc19-129">Capacidad máxima (GB)</span><span class="sxs-lookup"><span data-stu-id="7fc19-129">Maximum capacity (GB)</span></span> |<span data-ttu-id="7fc19-130">500</span><span class="sxs-lookup"><span data-stu-id="7fc19-130">500</span></span> |<span data-ttu-id="7fc19-131">Capacidad de almacenamiento total que puede consumir una suscripción en esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-131">Total storage capacity that can be consumed by a subscription in this location.</span></span> |
| <span data-ttu-id="7fc19-132">Número total de cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="7fc19-132">Total number of storage accounts</span></span> |<span data-ttu-id="7fc19-133">20 |</span><span class="sxs-lookup"><span data-stu-id="7fc19-133">20</span></span> |<span data-ttu-id="7fc19-134">El número máximo de cuentas de almacenamiento que puede crear una suscripción en esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-134">The maximum number of storage accounts that a subscription can create in this location.</span></span> |

## <a name="network-quota-types"></a><span data-ttu-id="7fc19-135">Tipos de cuota de red</span><span class="sxs-lookup"><span data-stu-id="7fc19-135">Network quota types</span></span>
| <span data-ttu-id="7fc19-136">**Elemento**</span><span class="sxs-lookup"><span data-stu-id="7fc19-136">**Item**</span></span> | <span data-ttu-id="7fc19-137">**Valor predeterminado**</span><span class="sxs-lookup"><span data-stu-id="7fc19-137">**Default value**</span></span> | <span data-ttu-id="7fc19-138">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="7fc19-138">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7fc19-139">Número máximo de direcciones IP públicas</span><span class="sxs-lookup"><span data-stu-id="7fc19-139">Max public IPs</span></span> |<span data-ttu-id="7fc19-140">50</span><span class="sxs-lookup"><span data-stu-id="7fc19-140">50</span></span> |<span data-ttu-id="7fc19-141">El número máximo de direcciones IP públicas que puede crear una suscripción en esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-141">The maximum number of public IPs that a subscription can create in this location.</span></span> |
| <span data-ttu-id="7fc19-142">Número máximo de redes virtuales</span><span class="sxs-lookup"><span data-stu-id="7fc19-142">Max virtual networks</span></span> |<span data-ttu-id="7fc19-143">50</span><span class="sxs-lookup"><span data-stu-id="7fc19-143">50</span></span> |<span data-ttu-id="7fc19-144">El número máximo de redes virtuales que puede crear una suscripción en esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-144">The maximum number of virtual networks that a subscription can create in this location.</span></span> |
| <span data-ttu-id="7fc19-145">Número máximo de puertas de enlace de red virtual</span><span class="sxs-lookup"><span data-stu-id="7fc19-145">Max virtual network gateways</span></span> |<span data-ttu-id="7fc19-146">1</span><span class="sxs-lookup"><span data-stu-id="7fc19-146">1</span></span> |<span data-ttu-id="7fc19-147">El número máximo de puertas de enlace de red virtual (puertas de enlace de VPN) que puede crear una suscripción en esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-147">The maximum number of virtual network gateways (VPN Gateways) that a subscription can create in this location.</span></span> |
| <span data-ttu-id="7fc19-148">Número máximo de conexiones de red</span><span class="sxs-lookup"><span data-stu-id="7fc19-148">Max network connections</span></span> |<span data-ttu-id="7fc19-149">2</span><span class="sxs-lookup"><span data-stu-id="7fc19-149">2</span></span> |<span data-ttu-id="7fc19-150">El número máximo de conexiones de red (punto a punto o sitio a sitio) que puede crear una suscripción en todas las puertas de enlace de red virtual de esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-150">The maximum number of network connections (point-to-point or site-to-site) that a subscription can create across all virtual network gateways in this location.</span></span> |
| <span data-ttu-id="7fc19-151">Número máximo de equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="7fc19-151">Max load balancers</span></span> |<span data-ttu-id="7fc19-152">50</span><span class="sxs-lookup"><span data-stu-id="7fc19-152">50</span></span> |<span data-ttu-id="7fc19-153">El número máximo de equilibradores de carga que puede crear una suscripción en esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-153">The maximum number of load balancers that a subscription can create in this location.</span></span> |
| <span data-ttu-id="7fc19-154">Nº máx. NIC</span><span class="sxs-lookup"><span data-stu-id="7fc19-154">Max NICs</span></span> |<span data-ttu-id="7fc19-155">100</span><span class="sxs-lookup"><span data-stu-id="7fc19-155">100</span></span> |<span data-ttu-id="7fc19-156">El número máximo de interfaces de red que puede crear una suscripción en esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-156">The maximum number of network interfaces that a subscription can create in this location.</span></span> |
| <span data-ttu-id="7fc19-157">Número máximo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="7fc19-157">Max network security groups</span></span> |<span data-ttu-id="7fc19-158">50</span><span class="sxs-lookup"><span data-stu-id="7fc19-158">50</span></span> |<span data-ttu-id="7fc19-159">El número máximo de grupos de seguridad de red que puede crear una suscripción en esta ubicación.</span><span class="sxs-lookup"><span data-stu-id="7fc19-159">The maximum number of network security groups that a subscription can create in this location.</span></span> |

## <a name="view-an-existing-quota"></a><span data-ttu-id="7fc19-160">Visualización de una cuota existente</span><span class="sxs-lookup"><span data-stu-id="7fc19-160">View an existing quota</span></span>
1. <span data-ttu-id="7fc19-161">Haga clic en **Más servicios** > **Proveedores de recursos**.</span><span class="sxs-lookup"><span data-stu-id="7fc19-161">Click **More services** > **Resource Providers**.</span></span>
2. <span data-ttu-id="7fc19-162">Seleccione el servicio con la cuota que desea ver.</span><span class="sxs-lookup"><span data-stu-id="7fc19-162">Select the service with the quota that you want to view.</span></span>
3. <span data-ttu-id="7fc19-163">Haga clic en **Cuotas** y seleccione la cuota que desea ver.</span><span class="sxs-lookup"><span data-stu-id="7fc19-163">Click **Quotas**, and select the quota you want to view.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fc19-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7fc19-164">Next steps</span></span>
[<span data-ttu-id="7fc19-165">Más información acerca de planes, ofertas y cuotas.</span><span class="sxs-lookup"><span data-stu-id="7fc19-165">Learn more about plans, offers, and quotas.</span></span>](azure-stack-plan-offer-quota-overview.md)

[<span data-ttu-id="7fc19-166">Crear cuotas durante la creación de un plan.</span><span class="sxs-lookup"><span data-stu-id="7fc19-166">Create quotas while creating a plan.</span></span>](azure-stack-create-plan.md)
