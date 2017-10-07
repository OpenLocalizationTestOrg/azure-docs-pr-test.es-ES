---
title: "aaaAutomated aplicación de revisiones para las máquinas virtuales de SQL Server (clásico) | Documentos de Microsoft"
description: "Explica característica de aplicación de revisiones automatizada de Hola para SQL Server máquinas virtuales que ejecutan en Azure utilizando el modo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="833ac-103">Aplicación de revisiones automatizadas para SQL Server en máquinas virtuales de Azure (implementación clásica)</span><span class="sxs-lookup"><span data-stu-id="833ac-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="833ac-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="833ac-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="833ac-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="833ac-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="833ac-106">Aplicación de revisión automatizada establece una ventana de mantenimiento para una máquina virtual de Azure con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="833ac-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="833ac-107">Actualizaciones automatizadas solo puede instalarse durante esta ventana de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="833ac-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="833ac-108">Para SQL Server, esto garantiza que las actualizaciones del sistema y los reinicios asociados se producen en tiempo posible mejor hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="833ac-108">For SQL Server, this ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="833ac-109">Aplicación de revisiones automatizada depende de hello [extensión del agente de IaaS de SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="833ac-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="833ac-110">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="833ac-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="833ac-111">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="833ac-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="833ac-112">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="833ac-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="833ac-113">versión de administrador de recursos de hello tooview de este artículo, consulte [aplicación de revisiones automatizada para SQL Server en el Administrador de recursos de máquinas virtuales de Azure](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="833ac-113">tooview hello Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="833ac-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="833ac-114">Prerequisites</span></span>
<span data-ttu-id="833ac-115">toouse aplicación de revisiones automatizada, considere la posibilidad de hello siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="833ac-115">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="833ac-116">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="833ac-116">**Operating System**:</span></span>

* <span data-ttu-id="833ac-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="833ac-117">Windows Server 2012</span></span>
* <span data-ttu-id="833ac-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="833ac-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="833ac-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="833ac-119">Windows Server 2016</span></span>

<span data-ttu-id="833ac-120">**Versión de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="833ac-120">**SQL Server version**:</span></span>

* <span data-ttu-id="833ac-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="833ac-121">SQL Server 2012</span></span>
* <span data-ttu-id="833ac-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="833ac-122">SQL Server 2014</span></span>
* <span data-ttu-id="833ac-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="833ac-123">SQL Server 2016</span></span>

<span data-ttu-id="833ac-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="833ac-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="833ac-125">[Comandos de PowerShell de Azure más recientes de Hola de instalación](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="833ac-125">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="833ac-126">**Extensión IaaS de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="833ac-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="833ac-127">[Instalar extensión de IaaS de SQL Server de hello](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="833ac-127">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="833ac-128">Settings</span><span class="sxs-lookup"><span data-stu-id="833ac-128">Settings</span></span>
<span data-ttu-id="833ac-129">Hello siguiente tabla describe las opciones de Hola que pueden configurarse para la aplicación de revisiones automatizada.</span><span class="sxs-lookup"><span data-stu-id="833ac-129">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="833ac-130">Para las máquinas virtuales clásicas, debe usar PowerShell tooconfigure esta configuración.</span><span class="sxs-lookup"><span data-stu-id="833ac-130">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="833ac-131">Configuración</span><span class="sxs-lookup"><span data-stu-id="833ac-131">Setting</span></span> | <span data-ttu-id="833ac-132">Valores posibles</span><span class="sxs-lookup"><span data-stu-id="833ac-132">Possible values</span></span> | <span data-ttu-id="833ac-133">Description</span><span class="sxs-lookup"><span data-stu-id="833ac-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="833ac-134">**Aplicación de revisiones automatizada**</span><span class="sxs-lookup"><span data-stu-id="833ac-134">**Automated Patching**</span></span> |<span data-ttu-id="833ac-135">Habilitar/deshabilitar (deshabilitado)</span><span class="sxs-lookup"><span data-stu-id="833ac-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="833ac-136">Habilita o deshabilita Aplicación de revisión automatizada para una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="833ac-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="833ac-137">**Programación de mantenimiento**</span><span class="sxs-lookup"><span data-stu-id="833ac-137">**Maintenance schedule**</span></span> |<span data-ttu-id="833ac-138">Cada día, el lunes, el martes, el miércoles, el jueves, el viernes, el sábado, el domingo</span><span class="sxs-lookup"><span data-stu-id="833ac-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="833ac-139">programación de Hola para descargar e instalar actualizaciones de Microsoft, Windows y SQL Server para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="833ac-139">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="833ac-140">**Hora de inicio de mantenimiento**</span><span class="sxs-lookup"><span data-stu-id="833ac-140">**Maintenance start hour**</span></span> |<span data-ttu-id="833ac-141">0-24</span><span class="sxs-lookup"><span data-stu-id="833ac-141">0-24</span></span> |<span data-ttu-id="833ac-142">Hola inicio local tiempo tooupdate Hola la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="833ac-142">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="833ac-143">**Duración de la ventana de mantenimiento**</span><span class="sxs-lookup"><span data-stu-id="833ac-143">**Maintenance window duration**</span></span> |<span data-ttu-id="833ac-144">30-180</span><span class="sxs-lookup"><span data-stu-id="833ac-144">30-180</span></span> |<span data-ttu-id="833ac-145">número de Hola de minutos permitido descarga de hello toocomplete e instalación de actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="833ac-145">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="833ac-146">**Categoría de la revisión**</span><span class="sxs-lookup"><span data-stu-id="833ac-146">**Patch Category**</span></span> |<span data-ttu-id="833ac-147">Importante</span><span class="sxs-lookup"><span data-stu-id="833ac-147">Important</span></span> |<span data-ttu-id="833ac-148">categoría de Hola de toodownload actualizaciones e instalar.</span><span class="sxs-lookup"><span data-stu-id="833ac-148">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="833ac-149">Configuración con PowerShell</span><span class="sxs-lookup"><span data-stu-id="833ac-149">Configuration with PowerShell</span></span>
<span data-ttu-id="833ac-150">En el siguiente ejemplo de Hola, PowerShell es usado tooconfigure aplicación de revisiones automatizada en una máquina virtual existente de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="833ac-150">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="833ac-151">Hola **New-AzureVMSqlServerAutoPatchingConfig** comando configura una nueva ventana de mantenimiento para las actualizaciones automáticas.</span><span class="sxs-lookup"><span data-stu-id="833ac-151">hello **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="833ac-152">Siguiendo con este ejemplo, hello tabla siguiente describen efecto práctico de hello en el destino de hello VM de Azure:</span><span class="sxs-lookup"><span data-stu-id="833ac-152">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="833ac-153">Parámetro</span><span class="sxs-lookup"><span data-stu-id="833ac-153">Parameter</span></span> | <span data-ttu-id="833ac-154">Efecto</span><span class="sxs-lookup"><span data-stu-id="833ac-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="833ac-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="833ac-155">**DayOfWeek**</span></span> |<span data-ttu-id="833ac-156">Las revisiones instaladas cada jueves.</span><span class="sxs-lookup"><span data-stu-id="833ac-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="833ac-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="833ac-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="833ac-158">Inicia las actualizaciones a las 11:00 a.m.</span><span class="sxs-lookup"><span data-stu-id="833ac-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="833ac-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="833ac-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="833ac-160">Las revisiones deben instalarse en un plazo de 120 minutos.</span><span class="sxs-lookup"><span data-stu-id="833ac-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="833ac-161">En función del tiempo de inicio de hello, debe finalizar a la 1:00 pm.</span><span class="sxs-lookup"><span data-stu-id="833ac-161">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="833ac-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="833ac-162">**PatchCategory**</span></span> |<span data-ttu-id="833ac-163">Hola solo configuración posible para este parámetro es "Importante".</span><span class="sxs-lookup"><span data-stu-id="833ac-163">hello only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="833ac-164">Podría tardar varios tooinstall minutos y configure Hola agente de IaaS de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="833ac-164">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="833ac-165">toodisable aplicación de revisiones automatizada, ejecución Hola mismo script sin Hola - Enable parámetro toohello New-AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="833ac-165">toodisable Automated Patching, run hello same script without hello -Enable parameter toohello New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="833ac-166">Como con la instalación, puede tardar varios toodisable minutos aplicación de revisiones automatizada.</span><span class="sxs-lookup"><span data-stu-id="833ac-166">As with installation, it can take several minutes toodisable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="833ac-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="833ac-167">Next steps</span></span>
<span data-ttu-id="833ac-168">Para más información acerca de otras tareas de automatización disponibles, consulte la [extensión Agente de IaaS de SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="833ac-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="833ac-169">Para más información sobre cómo ejecutar SQL Server en máquinas virtuales de Azure, consulte [Introducción a SQL Server en Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="833ac-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

