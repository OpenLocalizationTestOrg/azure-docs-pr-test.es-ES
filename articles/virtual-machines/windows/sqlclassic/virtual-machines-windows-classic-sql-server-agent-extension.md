---
title: "tareas de administración de aaaAutomate en máquinas virtuales de SQL (clásico) | Documentos de Microsoft"
description: "Este tema describe cómo toomanage Hola extensión del Agente SQL Server, que automatiza las tareas de administración de SQL Server específicas. Entre ellas se incluyen la copia de seguridad automatizada, la aplicación de revisiones automatizada y la integración de Azure Key Vault. En este tema usa el modo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a><span data-ttu-id="a4a14-105">Automatizar tareas de administración de máquinas virtuales de Azure con hello extensión del Agente SQL Server (clásico)</span><span class="sxs-lookup"><span data-stu-id="a4a14-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4a14-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a4a14-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="a4a14-107">Clásico</span><span class="sxs-lookup"><span data-stu-id="a4a14-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="a4a14-108">Hola (SQLIaaSAgent) de extensión del agente de IaaS de SQL Server se ejecuta en máquinas virtuales de Azure tooautomate las tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="a4a14-108">hello SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="a4a14-109">Este tema proporciona información general de servicios de hello admitidos por la extensión de hello, así como las instrucciones de instalación, estado y eliminación.</span><span class="sxs-lookup"><span data-stu-id="a4a14-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a4a14-110">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a4a14-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a4a14-111">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="a4a14-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a4a14-112">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4a14-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a4a14-113">versión de administrador de recursos de hello tooview de este artículo, consulte [extensión del Agente SQL Server para el Administrador de recursos en máquinas virtuales de SQL Server](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a4a14-113">tooview hello Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="a4a14-114">Servicios admitidos</span><span class="sxs-lookup"><span data-stu-id="a4a14-114">Supported services</span></span>
<span data-ttu-id="a4a14-115">Hola extensión del agente de IaaS de SQL Server admite Hola después de las tareas de administración:</span><span class="sxs-lookup"><span data-stu-id="a4a14-115">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="a4a14-116">Característica de administración</span><span class="sxs-lookup"><span data-stu-id="a4a14-116">Administration feature</span></span> | <span data-ttu-id="a4a14-117">Descripción</span><span class="sxs-lookup"><span data-stu-id="a4a14-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a4a14-118">**Copia de seguridad automatizada de SQL**</span><span class="sxs-lookup"><span data-stu-id="a4a14-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="a4a14-119">Automatiza la programación de Hola de copias de seguridad para todas las bases de datos para la instancia de predeterminada Hola de SQL Server en VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4a14-119">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="a4a14-120">Para obtener más información, consulte [Copia de seguridad automatizada para SQL Server en máquinas virtuales de Azure (implementación clásica)](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="a4a14-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="a4a14-121">**Aplicación de revisiones automatizada de SQL**</span><span class="sxs-lookup"><span data-stu-id="a4a14-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="a4a14-122">Configura una ventana de mantenimiento durante las actualizaciones que coloca tooyour VM puede tardar, por lo que puede evitar las actualizaciones durante las horas de máxima para la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a4a14-122">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="a4a14-123">Para obtener más información, consulte [Aplicación de revisiones automatizadas para SQL Server en máquinas virtuales de Azure (implementación clásica)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="a4a14-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="a4a14-124">**Integración del Almacén de claves de Azure**</span><span class="sxs-lookup"><span data-stu-id="a4a14-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="a4a14-125">Permite tooautomatically instalar y configurar el almacén de claves de Azure en la VM de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4a14-125">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="a4a14-126">Para obtener más información, consulte [Configuración de la integración de Almacén de claves de Azure para SQL Server en máquinas virtuales de Azure (implementación clásica)](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="a4a14-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="a4a14-127">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a4a14-127">Prerequisites</span></span>
<span data-ttu-id="a4a14-128">Requisitos toouse Hola extensión del agente de IaaS de SQL Server en la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="a4a14-128">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="a4a14-129">Sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="a4a14-129">Operating System:</span></span>
* <span data-ttu-id="a4a14-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a4a14-130">Windows Server 2012</span></span>
* <span data-ttu-id="a4a14-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a4a14-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="a4a14-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a4a14-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="a4a14-133">Versiones de SQL Server:</span><span class="sxs-lookup"><span data-stu-id="a4a14-133">SQL Server versions:</span></span>
* <span data-ttu-id="a4a14-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="a4a14-134">SQL Server 2012</span></span>
* <span data-ttu-id="a4a14-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="a4a14-135">SQL Server 2014</span></span>
* <span data-ttu-id="a4a14-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="a4a14-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="a4a14-137">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a4a14-137">Azure PowerShell:</span></span>
<span data-ttu-id="a4a14-138">[Descargar y configurar los comandos de PowerShell de Azure más recientes de hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4a14-138">[Download and configure hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="a4a14-139">Inicie Windows PowerShell y conectar tooyour suscripción de Azure con hello **Add-AzureAccount** comando.</span><span class="sxs-lookup"><span data-stu-id="a4a14-139">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="a4a14-140">Si tiene varias suscripciones, use **Select-AzureSubscription** suscripción de hello tooselect que contiene el destino de la VM clásico.</span><span class="sxs-lookup"><span data-stu-id="a4a14-140">If you have multiple subscriptions, use **Select-AzureSubscription** tooselect hello subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="a4a14-141">En este momento, puede obtener una lista de máquinas virtuales clásicas de Hola y sus nombres de servicio asociado con hello **Get-AzureVM** comando.</span><span class="sxs-lookup"><span data-stu-id="a4a14-141">At this point, you can get a list of hello classic virtual machines and their associated service names with hello **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="a4a14-142">Instalación</span><span class="sxs-lookup"><span data-stu-id="a4a14-142">Installation</span></span>
<span data-ttu-id="a4a14-143">Para las máquinas virtuales clásicas, debe usar PowerShell tooinstall hello extensión del agente de IaaS de SQL Server y configurar sus servicios asociados.</span><span class="sxs-lookup"><span data-stu-id="a4a14-143">For classic VMs, you must use PowerShell tooinstall hello SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="a4a14-144">Hola de uso **AzureVMSqlServerExtension conjunto** extensión de Hola de tooinstall de cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4a14-144">Use hello **Set-AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello extension.</span></span> <span data-ttu-id="a4a14-145">Por ejemplo, hello siguiente comando instala la extensión de hello en una VM de Windows Server (clásico) y nombres que "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="a4a14-145">For example, hello following command installs hello extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="a4a14-146">Si actualiza la versión más reciente de toohello de hello extensión del agente de IaaS de SQL, debe reiniciar la máquina virtual después de actualizar la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4a14-146">If you update toohello latest version of hello SQL IaaS Agent Extension, you must restart your virtual machine after updating hello extension.</span></span>

> [!NOTE]
> <span data-ttu-id="a4a14-147">Máquinas virtuales clásicas no tienen una opción tooinstall y configurar Hola extensión del agente de IaaS de SQL a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4a14-147">Classic virtual machines do not have an option tooinstall and configure hello SQL IaaS Agent Extension through hello portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="a4a14-148">Estado</span><span class="sxs-lookup"><span data-stu-id="a4a14-148">Status</span></span>
<span data-ttu-id="a4a14-149">Una manera de tooverify que se instala la extensión de hello es tooview el estado del agente de hello en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4a14-149">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="a4a14-150">Seleccione una máquina virtual que se muestran en la hoja de la máquina virtual de hello y, a continuación, haga clic en **extensiones**.</span><span class="sxs-lookup"><span data-stu-id="a4a14-150">Select a virtual machine listed in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="a4a14-151">Debería ver Hola **SQLIaaSAgent** las extensiones que aparece.</span><span class="sxs-lookup"><span data-stu-id="a4a14-151">You should see hello **SQLIaaSAgent** extension listed.</span></span>

![Extensión del Agente de IaaS SQL Server en Azure Portal](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="a4a14-153">También puede usar hello **AzureVMSqlServerExtension Get** cmdlet de Powershell de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4a14-153">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="a4a14-154">Eliminación</span><span class="sxs-lookup"><span data-stu-id="a4a14-154">Removal</span></span>
<span data-ttu-id="a4a14-155">Hola Portal de Azure, puede desinstalar extensión Hola haciendo clic en el botón de puntos suspensivos de hello en hello **extensiones** hoja de propiedades de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a4a14-155">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="a4a14-156">Hacer clic en **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="a4a14-156">Then click **Uninstall**.</span></span>

![Desinstalar Hola extensión del agente de IaaS de SQL Server en el Portal de Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="a4a14-158">También puede usar hello **Remove-AzureVMSqlServerExtension** cmdlet de Powershell.</span><span class="sxs-lookup"><span data-stu-id="a4a14-158">You can also use hello **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="a4a14-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a4a14-159">Next Steps</span></span>
<span data-ttu-id="a4a14-160">Empezar a usar uno de los servicios de hello compatibles con la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4a14-160">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="a4a14-161">Para obtener más información, vea los temas de hello hace referencia en hello [admite servicios](#supported-services) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="a4a14-161">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="a4a14-162">Para obtener más información sobre cómo ejecutar SQL Server en Azure Virtual Machines, consulte [Información general sobre SQL Server en Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4a14-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

