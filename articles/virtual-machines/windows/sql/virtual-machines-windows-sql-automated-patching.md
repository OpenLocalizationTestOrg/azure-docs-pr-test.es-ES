---
title: "aaaAutomated aplicación de revisiones para las máquinas virtuales de SQL Server (Administrador de recursos) | Documentos de Microsoft"
description: "Explica el característica de aplicación de revisiones automatizada de Hola para SQL Server máquinas virtuales que ejecutan en Azure mediante el Administrador de recursos."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="bcd37-103">Aplicación de revisión automatizada para SQL Server en máquinas virtuales de Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="bcd37-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bcd37-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bcd37-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="bcd37-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="bcd37-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="bcd37-106">Aplicación de revisión automatizada establece una ventana de mantenimiento para una máquina virtual de Azure con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bcd37-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="bcd37-107">Actualizaciones automatizadas solo puede instalarse durante esta ventana de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="bcd37-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="bcd37-108">Para SQL Server, esta rescriction garantiza que las actualizaciones del sistema y los reinicios asociados se producen en tiempo posible mejor hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcd37-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="bcd37-109">Aplicación de revisiones automatizada depende de hello [extensión del agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bcd37-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="bcd37-110">tooview Hola clásico versión de este artículo, consulte [aplicación de revisiones automatizada para SQL Server en máquinas virtuales de Azure clásico](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="bcd37-110">tooview hello classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcd37-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bcd37-111">Prerequisites</span></span>
<span data-ttu-id="bcd37-112">toouse aplicación de revisiones automatizada, considere la posibilidad de hello siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="bcd37-112">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="bcd37-113">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="bcd37-113">**Operating System**:</span></span>

* <span data-ttu-id="bcd37-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="bcd37-114">Windows Server 2012</span></span>
* <span data-ttu-id="bcd37-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="bcd37-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="bcd37-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="bcd37-116">Windows Server 2016</span></span>

<span data-ttu-id="bcd37-117">**Versión de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="bcd37-117">**SQL Server version**:</span></span>

* <span data-ttu-id="bcd37-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="bcd37-118">SQL Server 2012</span></span>
* <span data-ttu-id="bcd37-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="bcd37-119">SQL Server 2014</span></span>
* <span data-ttu-id="bcd37-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="bcd37-120">SQL Server 2016</span></span>

<span data-ttu-id="bcd37-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="bcd37-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="bcd37-122">[Instalar los comandos de PowerShell de Azure más recientes de hello](/powershell/azure/overview) si tiene previsto tooconfigure aplicación de revisiones automatizada con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bcd37-122">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="bcd37-123">Aplicación de revisiones automatizada se basa en hello extensión del agente de IaaS de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bcd37-123">Automated Patching relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="bcd37-124">Las imágenes actuales de la galería de máquinas virtuales de SQL agregan esta extensión de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bcd37-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="bcd37-125">Para más información, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bcd37-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="bcd37-126">Settings</span><span class="sxs-lookup"><span data-stu-id="bcd37-126">Settings</span></span>
<span data-ttu-id="bcd37-127">Hello siguiente tabla describe las opciones de Hola que pueden configurarse para la aplicación de revisiones automatizada.</span><span class="sxs-lookup"><span data-stu-id="bcd37-127">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="bcd37-128">pasos de configuración real de Hello varían dependiendo de si utiliza Hola portal de Azure o comandos de PowerShell de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd37-128">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="bcd37-129">Configuración</span><span class="sxs-lookup"><span data-stu-id="bcd37-129">Setting</span></span> | <span data-ttu-id="bcd37-130">Valores posibles</span><span class="sxs-lookup"><span data-stu-id="bcd37-130">Possible values</span></span> | <span data-ttu-id="bcd37-131">Description</span><span class="sxs-lookup"><span data-stu-id="bcd37-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bcd37-132">**Aplicación de revisiones automatizada**</span><span class="sxs-lookup"><span data-stu-id="bcd37-132">**Automated Patching**</span></span> |<span data-ttu-id="bcd37-133">Habilitar/deshabilitar (deshabilitado)</span><span class="sxs-lookup"><span data-stu-id="bcd37-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="bcd37-134">Habilita o deshabilita Aplicación de revisión automatizada para una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd37-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="bcd37-135">**Programación de mantenimiento**</span><span class="sxs-lookup"><span data-stu-id="bcd37-135">**Maintenance schedule**</span></span> |<span data-ttu-id="bcd37-136">Cada día, el lunes, el martes, el miércoles, el jueves, el viernes, el sábado, el domingo</span><span class="sxs-lookup"><span data-stu-id="bcd37-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="bcd37-137">programación de Hola para descargar e instalar actualizaciones de Microsoft, Windows y SQL Server para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bcd37-137">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="bcd37-138">**Hora de inicio de mantenimiento**</span><span class="sxs-lookup"><span data-stu-id="bcd37-138">**Maintenance start hour**</span></span> |<span data-ttu-id="bcd37-139">0-24</span><span class="sxs-lookup"><span data-stu-id="bcd37-139">0-24</span></span> |<span data-ttu-id="bcd37-140">Hola inicio local tiempo tooupdate Hola la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bcd37-140">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="bcd37-141">**Duración de la ventana de mantenimiento**</span><span class="sxs-lookup"><span data-stu-id="bcd37-141">**Maintenance window duration**</span></span> |<span data-ttu-id="bcd37-142">30-180</span><span class="sxs-lookup"><span data-stu-id="bcd37-142">30-180</span></span> |<span data-ttu-id="bcd37-143">número de Hola de minutos permitido descarga de hello toocomplete e instalación de actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="bcd37-143">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="bcd37-144">**Categoría de la revisión**</span><span class="sxs-lookup"><span data-stu-id="bcd37-144">**Patch Category**</span></span> |<span data-ttu-id="bcd37-145">Importante</span><span class="sxs-lookup"><span data-stu-id="bcd37-145">Important</span></span> |<span data-ttu-id="bcd37-146">categoría de Hola de toodownload actualizaciones e instalar.</span><span class="sxs-lookup"><span data-stu-id="bcd37-146">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="bcd37-147">Configuración de hello Portal</span><span class="sxs-lookup"><span data-stu-id="bcd37-147">Configuration in hello Portal</span></span>
<span data-ttu-id="bcd37-148">Puede usar hello tooconfigure portal Azure aplicación de revisiones automatizada durante el aprovisionamiento o para las máquinas virtuales existentes.</span><span class="sxs-lookup"><span data-stu-id="bcd37-148">You can use hello Azure portal tooconfigure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="bcd37-149">Nuevas máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="bcd37-149">New VMs</span></span>
<span data-ttu-id="bcd37-150">Hola de uso tooconfigure portal Azure aplicación de revisiones automatizada al crear una nueva máquina Virtual de SQL Server en el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcd37-150">Use hello Azure portal tooconfigure Automated Patching when you create a new SQL Server Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="bcd37-151">Hola **configuración de SQL Server** hoja, seleccione **aplicación de revisiones automatizadas**.</span><span class="sxs-lookup"><span data-stu-id="bcd37-151">In hello **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="bcd37-152">Hello siguiente captura de pantalla de portal Azure muestra hello **SQL aplicación de revisiones automatizada** hoja.</span><span class="sxs-lookup"><span data-stu-id="bcd37-152">hello following Azure portal screenshot shows hello **SQL Automated Patching** blade.</span></span>

![Aplicación de revisión automatizada de SQL en el Portal de Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="bcd37-154">Para el contexto, vea el tema completo de hello en [aprovisionar una máquina virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="bcd37-154">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="bcd37-155">Máquinas virtuales existentes</span><span class="sxs-lookup"><span data-stu-id="bcd37-155">Existing VMs</span></span>
<span data-ttu-id="bcd37-156">Para las máquinas virtuales de SQL Server existentes, seleccione su máquina virtual de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bcd37-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="bcd37-157">A continuación, seleccione hello **configuración de SQL Server** sección de hello **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="bcd37-157">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Aplicación de revisión automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="bcd37-159">Hola **configuración de SQL Server** hoja, haga clic en hello **editar** botón Hola automatizada sección aplicación de revisiones.</span><span class="sxs-lookup"><span data-stu-id="bcd37-159">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated patching section.</span></span>

![Configuración de Aplicación de revisión automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="bcd37-161">Cuando termine, haga clic en hello **Aceptar** botón en la parte inferior de Hola de hello **configuración de SQL Server** toosave hoja los cambios.</span><span class="sxs-lookup"><span data-stu-id="bcd37-161">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="bcd37-162">Si va a habilitar aplicación de revisiones automatizada para hello primera vez, Azure configura Hola agente de IaaS de SQL Server en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcd37-162">If you are enabling Automated Patching for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="bcd37-163">Durante este tiempo, Hola portal de Azure es posible que no muestre que se ha configurado la aplicación de revisiones automatizada.</span><span class="sxs-lookup"><span data-stu-id="bcd37-163">During this time, hello Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="bcd37-164">Espere unos minutos para hello toobe de agente instalado, configurado.</span><span class="sxs-lookup"><span data-stu-id="bcd37-164">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="bcd37-165">Después de ese hello Azure portal refleje nueva configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcd37-165">After that hello Azure portal reflects hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="bcd37-166">También puede usar una plantilla para configurar Aplicación de revisión automatizada.</span><span class="sxs-lookup"><span data-stu-id="bcd37-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="bcd37-167">Para más información, consulte [la plantilla de inicio rápido de Azure para Aplicación de revisión automatizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="bcd37-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="bcd37-168">Configuración con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcd37-168">Configuration with PowerShell</span></span>
<span data-ttu-id="bcd37-169">Después de aprovisionar la VM de SQL, use PowerShell tooconfigure aplicación de revisiones automatizada.</span><span class="sxs-lookup"><span data-stu-id="bcd37-169">After provisioning your SQL VM, use PowerShell tooconfigure Automated Patching.</span></span>

<span data-ttu-id="bcd37-170">En el siguiente ejemplo de Hola, PowerShell es usado tooconfigure aplicación de revisiones automatizada en una máquina virtual existente de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bcd37-170">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="bcd37-171">Hola **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** comando configura una nueva ventana de mantenimiento para las actualizaciones automáticas.</span><span class="sxs-lookup"><span data-stu-id="bcd37-171">hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="bcd37-172">Siguiendo con este ejemplo, hello tabla siguiente describen efecto práctico de hello en el destino de hello VM de Azure:</span><span class="sxs-lookup"><span data-stu-id="bcd37-172">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="bcd37-173">Parámetro</span><span class="sxs-lookup"><span data-stu-id="bcd37-173">Parameter</span></span> | <span data-ttu-id="bcd37-174">Efecto</span><span class="sxs-lookup"><span data-stu-id="bcd37-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="bcd37-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="bcd37-175">**DayOfWeek**</span></span> |<span data-ttu-id="bcd37-176">Las revisiones instaladas cada jueves.</span><span class="sxs-lookup"><span data-stu-id="bcd37-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="bcd37-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="bcd37-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="bcd37-178">Inicia las actualizaciones a las 11:00 a.m.</span><span class="sxs-lookup"><span data-stu-id="bcd37-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="bcd37-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="bcd37-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="bcd37-180">Las revisiones deben instalarse en un plazo de 120 minutos.</span><span class="sxs-lookup"><span data-stu-id="bcd37-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="bcd37-181">En función del tiempo de inicio de hello, debe finalizar a la 1:00 pm.</span><span class="sxs-lookup"><span data-stu-id="bcd37-181">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="bcd37-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="bcd37-182">**PatchCategory**</span></span> |<span data-ttu-id="bcd37-183">Hola única configuración posible para este parámetro es **importante**.</span><span class="sxs-lookup"><span data-stu-id="bcd37-183">hello only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="bcd37-184">Podría tardar varios tooinstall minutos y configure Hola agente de IaaS de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bcd37-184">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="bcd37-185">toodisable aplicación de revisiones automatizada, ejecución Hola mismo script sin hello **-habilitar** parámetro toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="bcd37-185">toodisable Automated Patching, run hello same script without hello **-Enable** parameter toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="bcd37-186">Hola ausencia de hello **-habilitar** característica de parámetro señales Hola comando toodisable Hola.</span><span class="sxs-lookup"><span data-stu-id="bcd37-186">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcd37-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bcd37-187">Next steps</span></span>
<span data-ttu-id="bcd37-188">Para más información acerca de otras tareas de automatización disponibles, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bcd37-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="bcd37-189">Para más información sobre cómo ejecutar SQL Server en máquinas virtuales de Azure, consulte [Introducción a SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcd37-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

