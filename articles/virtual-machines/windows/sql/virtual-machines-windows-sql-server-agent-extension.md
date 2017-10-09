---
title: "tareas de administración de aaaAutomate en máquinas virtuales de SQL (Administrador de recursos) | Documentos de Microsoft"
description: "Este tema describe cómo toomanage Hola extensión del Agente SQL Server, que automatiza las tareas de administración de SQL Server específicas. Entre ellas se incluyen la copia de seguridad automatizada, la aplicación de revisiones automatizada y la integración de Azure Key Vault. Este tema utiliza el modo de implementación de Resource Manager Hola."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="f6805-105">Automatizar tareas de administración de máquinas virtuales de Azure con hello extensión del Agente SQL Server (Administrador de recursos)</span><span class="sxs-lookup"><span data-stu-id="f6805-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6805-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f6805-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="f6805-107">Clásico</span><span class="sxs-lookup"><span data-stu-id="f6805-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="f6805-108">Hola (SQLIaaSExtension) de extensión del agente de IaaS de SQL Server se ejecuta en máquinas virtuales de Azure tooautomate las tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="f6805-108">hello SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="f6805-109">Este tema proporciona información general de servicios de hello admitidos por la extensión de hello, así como las instrucciones de instalación, estado y eliminación.</span><span class="sxs-lookup"><span data-stu-id="f6805-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="f6805-110">tooview Hola clásico versión de este artículo, consulte [extensión del Agente SQL Server para clásico de máquinas virtuales de SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f6805-110">tooview hello classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="f6805-111">Servicios admitidos</span><span class="sxs-lookup"><span data-stu-id="f6805-111">Supported services</span></span>
<span data-ttu-id="f6805-112">Hola extensión del agente de IaaS de SQL Server admite Hola después de las tareas de administración:</span><span class="sxs-lookup"><span data-stu-id="f6805-112">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="f6805-113">Característica de administración</span><span class="sxs-lookup"><span data-stu-id="f6805-113">Administration feature</span></span> | <span data-ttu-id="f6805-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="f6805-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6805-115">**Copia de seguridad automatizada de SQL**</span><span class="sxs-lookup"><span data-stu-id="f6805-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="f6805-116">Automatiza la programación de Hola de copias de seguridad para todas las bases de datos para la instancia de predeterminada Hola de SQL Server en VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6805-116">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="f6805-117">Para más información, consulte [Copia de seguridad automatizada para SQL Server en Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="f6805-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="f6805-118">**Aplicación de revisiones automatizada de SQL**</span><span class="sxs-lookup"><span data-stu-id="f6805-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="f6805-119">Configura una ventana de mantenimiento durante las actualizaciones que coloca tooyour VM puede tardar, por lo que puede evitar las actualizaciones durante las horas de máxima para la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f6805-119">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="f6805-120">Para más información, consulte [Aplicación de revisión automatizada para SQL Server en Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="f6805-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="f6805-121">**Integración del Almacén de claves de Azure**</span><span class="sxs-lookup"><span data-stu-id="f6805-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="f6805-122">Permite tooautomatically instalar y configurar el almacén de claves de Azure en la VM de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f6805-122">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="f6805-123">Para más información, consulte [Configuración de la integración de Azure Key Vault para SQL Server en Azure Virtual Machines (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="f6805-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="f6805-124">Una vez instalado y en ejecución, Hola extensión del agente de IaaS de SQL Server hace que estas características de administración estén disponibles en el panel de SQL Server de Hola de Hola máquina virtual en hello Portal de Azure y a través de PowerShell de Azure para las imágenes de marketplace de SQL Server y a través de Azure PowerShell para las instalaciones manuales de extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6805-124">Once installed and running, hello SQL Server IaaS Agent Extension makes these administration features available on hello SQL Server panel of hello virtual machine in hello Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of hello extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f6805-125">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f6805-125">Prerequisites</span></span>
<span data-ttu-id="f6805-126">Requisitos toouse Hola extensión del agente de IaaS de SQL Server en la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="f6805-126">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="f6805-127">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="f6805-127">**Operating System**:</span></span>

* <span data-ttu-id="f6805-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f6805-128">Windows Server 2012</span></span>
* <span data-ttu-id="f6805-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f6805-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="f6805-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f6805-130">Windows Server 2016</span></span>

<span data-ttu-id="f6805-131">**Versiones de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="f6805-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="f6805-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="f6805-132">SQL Server 2012</span></span>
* <span data-ttu-id="f6805-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="f6805-133">SQL Server 2014</span></span>
* <span data-ttu-id="f6805-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="f6805-134">SQL Server 2016</span></span>

<span data-ttu-id="f6805-135">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="f6805-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="f6805-136">Descargar y configurar los comandos de PowerShell de Azure más recientes de Hola</span><span class="sxs-lookup"><span data-stu-id="f6805-136">Download and configure hello latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="f6805-137">Instalación</span><span class="sxs-lookup"><span data-stu-id="f6805-137">Installation</span></span>
<span data-ttu-id="f6805-138">Hola extensión del agente de IaaS de SQL Server se instala automáticamente al aprovisionar una de las imágenes de galería de máquinas virtuales de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6805-138">hello SQL Server IaaS Agent Extension is automatically installed when you provision one of hello SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="f6805-139">Si necesita la extensión de hello tooreinstall manualmente en una de estas máquinas virtuales de SQL Server, use Hola siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f6805-139">If you need tooreinstall hello extension manually on one of these SQL Server VMs, use hello following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="f6805-140">También es posible tooinstall Hola extensión del agente de IaaS de SQL Server en una máquina virtual de solo por el sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="f6805-140">It is also possible tooinstall hello SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="f6805-141">Esto solo se permite si además ha instalado manualmente SQL Server en ese equipo.</span><span class="sxs-lookup"><span data-stu-id="f6805-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="f6805-142">A continuación, instalar la extensión de hello manualmente mediante el uso de Hola mismo **AzureVMSqlServerExtension conjunto** cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6805-142">Then install hello extension manually by using hello same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="f6805-143">Si instala manualmente Hola extensión del agente de IaaS de SQL Server en una VM solo por el sistema operativo de Windows Server, no puede administrar opciones de configuración de SQL Server de hello mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6805-143">If you manually install hello SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage hello SQL Server configuration settings through hello Azure portal.</span></span> <span data-ttu-id="f6805-144">En este escenario debe realizar todos los cambios con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6805-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="f6805-145">Estado</span><span class="sxs-lookup"><span data-stu-id="f6805-145">Status</span></span>
<span data-ttu-id="f6805-146">Una manera de tooverify que se instala la extensión de hello es tooview el estado del agente de hello en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6805-146">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="f6805-147">Seleccione **toda la configuración de** en Hola hoja de la máquina virtual y, a continuación, haga clic en **extensiones**.</span><span class="sxs-lookup"><span data-stu-id="f6805-147">Select **All settings** in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="f6805-148">Debería ver Hola **SQLIaaSExtension** las extensiones que aparece.</span><span class="sxs-lookup"><span data-stu-id="f6805-148">You should see hello **SQLIaaSExtension** extension listed.</span></span>

![Extensión del Agente de IaaS SQL Server en Azure Portal](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="f6805-150">También puede usar hello **AzureVMSqlServerExtension Get** cmdlet de Powershell de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6805-150">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="f6805-151">comando anterior Hola confirma agente Hola se instala y proporciona información de estado general.</span><span class="sxs-lookup"><span data-stu-id="f6805-151">hello previous command confirms hello agent is installed and provides general status information.</span></span> <span data-ttu-id="f6805-152">También puede obtener información de estado específica acerca de la copia de seguridad automatizada y aplicación de revisiones con hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="f6805-152">You can also get specific status information about Automated Backup and Patching with hello following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="f6805-153">Eliminación</span><span class="sxs-lookup"><span data-stu-id="f6805-153">Removal</span></span>
<span data-ttu-id="f6805-154">Hola Portal de Azure, puede desinstalar extensión Hola haciendo clic en el botón de puntos suspensivos de hello en hello **extensiones** hoja de propiedades de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f6805-154">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="f6805-155">Después, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="f6805-155">Then click **Delete**.</span></span>

![Desinstalar Hola extensión del agente de IaaS de SQL Server en el Portal de Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="f6805-157">También puede usar hello **Remove-AzureRmVMSqlServerExtension** cmdlet de Powershell.</span><span class="sxs-lookup"><span data-stu-id="f6805-157">You can also use hello **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="f6805-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6805-158">Next Steps</span></span>
<span data-ttu-id="f6805-159">Empezar a usar uno de los servicios de hello compatibles con la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6805-159">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="f6805-160">Para obtener más información, vea los temas de hello hace referencia en hello [admite servicios](#supported-services) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="f6805-160">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="f6805-161">Para obtener más información sobre cómo ejecutar SQL Server en Azure Virtual Machines, consulte [Información general sobre SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f6805-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

