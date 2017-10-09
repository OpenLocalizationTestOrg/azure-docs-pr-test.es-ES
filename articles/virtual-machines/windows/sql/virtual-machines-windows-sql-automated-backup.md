---
title: "aaaAutomated copia de seguridad de SQL Server 2014 máquinas virtuales de Azure | Documentos de Microsoft"
description: "Explica la característica de copia de seguridad automatizada de Hola para 2014 VM de SQL Server que se ejecuta en Azure. Este artículo es específico tooVMs mediante Hola, Administrador de recursos."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="84b88-104">Copia de seguridad automatizada para SQL Server 2014 en Azure Virtual Machines (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="84b88-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="84b88-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="84b88-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="84b88-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="84b88-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="84b88-107">Copia de seguridad automatizada configura automáticamente [tooMicrosoft de copia de seguridad administrada Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todas las bases de datos nuevas y existentes en una VM de Azure que ejecuta SQL Server 2014 Standard o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="84b88-107">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="84b88-108">Esto le permite las copias de seguridad de base de datos normal de tooconfigure que utilizan el almacenamiento de blobs de Azure duradero.</span><span class="sxs-lookup"><span data-stu-id="84b88-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="84b88-109">Copia de seguridad automatizada depende de hello [extensión del agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="84b88-109">Automated Backup depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="84b88-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="84b88-110">Prerequisites</span></span>
<span data-ttu-id="84b88-111">toouse copia de seguridad automatizada, considere la posibilidad de hello siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="84b88-111">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="84b88-112">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="84b88-112">**Operating System**:</span></span>

- <span data-ttu-id="84b88-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="84b88-113">Windows Server 2012</span></span>
- <span data-ttu-id="84b88-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="84b88-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="84b88-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="84b88-115">Windows Server 2016</span></span>

<span data-ttu-id="84b88-116">**Edición/versión de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="84b88-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="84b88-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="84b88-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="84b88-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="84b88-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84b88-119">Copia de seguridad automatizada funciona con SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="84b88-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="84b88-120">Si usas SQL Server 2016, puede usar copia de seguridad automatizada v2 tooback seguridad de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="84b88-120">If you are using SQL Server 2016, you can use Automated Backup v2 tooback up your databases.</span></span> <span data-ttu-id="84b88-121">Para obtener más información, vea [Copia de seguridad automatizada v2 para SQL Server 2016 en Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="84b88-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="84b88-122">**Configuración de base de datos**:</span><span class="sxs-lookup"><span data-stu-id="84b88-122">**Database configuration**:</span></span>

- <span data-ttu-id="84b88-123">Las bases de datos de destino deben usar el modelo de recuperación completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="84b88-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="84b88-124">Para obtener más información sobre las repercusiones de Hola Hola completa del modelo de recuperación en copias de seguridad, consulte [Hola de copia de seguridad en el modelo de recuperación completa](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="84b88-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="84b88-125">Las bases de datos de destino deben estar en la instancia de SQL Server predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="84b88-125">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="84b88-126">Hola extensión de IaaS de SQL Server no admite instancias con nombre.</span><span class="sxs-lookup"><span data-stu-id="84b88-126">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="84b88-127">**Modelo de implementación de Azure**:</span><span class="sxs-lookup"><span data-stu-id="84b88-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="84b88-128">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="84b88-128">Resource Manager</span></span>

<span data-ttu-id="84b88-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="84b88-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="84b88-130">[Instalar los comandos de PowerShell de Azure más recientes de hello](/powershell/azure/overview) si tiene previsto tooconfigure copia de seguridad automatizada con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84b88-130">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="84b88-131">Copia de seguridad automatizada se basa en hello extensión del agente de IaaS de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84b88-131">Automated Backup relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="84b88-132">Las imágenes actuales de la galería de máquinas virtuales de SQL agregan esta extensión de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="84b88-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="84b88-133">Para más información, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="84b88-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="84b88-134">Settings</span><span class="sxs-lookup"><span data-stu-id="84b88-134">Settings</span></span>

<span data-ttu-id="84b88-135">Hello siguiente tabla describe las opciones de Hola que se pueden configurar para copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="84b88-135">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="84b88-136">pasos de configuración real de Hello varían dependiendo de si utiliza Hola portal de Azure o comandos de PowerShell de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="84b88-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="84b88-137">Configuración</span><span class="sxs-lookup"><span data-stu-id="84b88-137">Setting</span></span> | <span data-ttu-id="84b88-138">Intervalo (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="84b88-138">Range (Default)</span></span> | <span data-ttu-id="84b88-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="84b88-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84b88-140">**Copia de seguridad automatizada**</span><span class="sxs-lookup"><span data-stu-id="84b88-140">**Automated Backup**</span></span> | <span data-ttu-id="84b88-141">Habilitar/deshabilitar (deshabilitado)</span><span class="sxs-lookup"><span data-stu-id="84b88-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="84b88-142">Habilita o deshabilita la copia de seguridad automatizada para una máquina virtual de Azure que ejecuta SQL Server 2014 Standard o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="84b88-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="84b88-143">**Período de retención**</span><span class="sxs-lookup"><span data-stu-id="84b88-143">**Retention Period**</span></span> | <span data-ttu-id="84b88-144">1-30 días (30 días)</span><span class="sxs-lookup"><span data-stu-id="84b88-144">1-30 days (30 days)</span></span> | <span data-ttu-id="84b88-145">número de Hola de días tooretain una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="84b88-145">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="84b88-146">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="84b88-146">**Storage Account**</span></span> | <span data-ttu-id="84b88-147">Cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="84b88-147">Azure storage account</span></span> | <span data-ttu-id="84b88-148">Un toouse de la cuenta de almacenamiento de Azure para almacenar los archivos de copia de seguridad automatizada en almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="84b88-148">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="84b88-149">Se crea un contenedor en esta ubicación toostore todos los archivos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="84b88-149">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="84b88-150">archivo de copia de seguridad de Hello convención de nomenclatura incluye Hola fecha, hora y nombre de la máquina.</span><span class="sxs-lookup"><span data-stu-id="84b88-150">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="84b88-151">**Cifrado**</span><span class="sxs-lookup"><span data-stu-id="84b88-151">**Encryption**</span></span> | <span data-ttu-id="84b88-152">Habilitar/deshabilitar (deshabilitado)</span><span class="sxs-lookup"><span data-stu-id="84b88-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="84b88-153">Habilita o deshabilita el cifrado.</span><span class="sxs-lookup"><span data-stu-id="84b88-153">Enables or disables encryption.</span></span> <span data-ttu-id="84b88-154">Cuando está habilitado el cifrado, copia de seguridad de hello certificados usados toorestore Hola se encuentran en hello especificado cuenta de almacenamiento en hello mismo `automaticbackup` contenedor mediante Hola la misma convención de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="84b88-154">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same `automaticbackup` container using hello same naming convention.</span></span> <span data-ttu-id="84b88-155">Si cambia la contraseña de hello, se genera un nuevo certificado con esa contraseña, pero los certificados antiguos Hola permanecen toorestore copias de seguridad anteriores.</span><span class="sxs-lookup"><span data-stu-id="84b88-155">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="84b88-156">**Password**</span><span class="sxs-lookup"><span data-stu-id="84b88-156">**Password**</span></span> | <span data-ttu-id="84b88-157">Texto de contraseña</span><span class="sxs-lookup"><span data-stu-id="84b88-157">Password text</span></span> | <span data-ttu-id="84b88-158">Una contraseña para claves de cifrado.</span><span class="sxs-lookup"><span data-stu-id="84b88-158">A password for encryption keys.</span></span> <span data-ttu-id="84b88-159">Esto solo es necesario si se habilita el cifrado.</span><span class="sxs-lookup"><span data-stu-id="84b88-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="84b88-160">En orden toorestore una copia de seguridad cifrada, debe tener contraseña correcta de Hola y el certificado relacionado que se usaron en tiempo de Hola se realizó la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="84b88-160">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="84b88-161">Configuración de hello Portal</span><span class="sxs-lookup"><span data-stu-id="84b88-161">Configuration in hello Portal</span></span>

<span data-ttu-id="84b88-162">Puede usar hello tooconfigure portal Azure copia de seguridad automatizada durante el aprovisionamiento o para SQL Server 2014 las máquinas virtuales existentes.</span><span class="sxs-lookup"><span data-stu-id="84b88-162">You can use hello Azure portal tooconfigure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="84b88-163">Nuevas máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="84b88-163">New VMs</span></span>

<span data-ttu-id="84b88-164">Usar hello tooconfigure portal Azure copia de seguridad automatizada al crear una nueva máquina Virtual de SQL Server 2014 en el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="84b88-164">Use hello Azure portal tooconfigure Automated Backup when you create a new SQL Server 2014 Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="84b88-165">Hola **configuración de SQL Server** hoja, seleccione **copia de seguridad automatizada**.</span><span class="sxs-lookup"><span data-stu-id="84b88-165">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="84b88-166">Hello siguiente captura de pantalla de portal Azure muestra hello **copia de seguridad automatizada de SQL** hoja.</span><span class="sxs-lookup"><span data-stu-id="84b88-166">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Configuración de Copia de seguridad automatizada de SQL en Azure Portal](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="84b88-168">Para el contexto, vea el tema completo de hello en [aprovisionar una máquina virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="84b88-168">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="84b88-169">Máquinas virtuales existentes</span><span class="sxs-lookup"><span data-stu-id="84b88-169">Existing VMs</span></span>

<span data-ttu-id="84b88-170">Para las máquinas virtuales de SQL Server existentes, seleccione su máquina virtual de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84b88-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="84b88-171">A continuación, seleccione hello **configuración de SQL Server** sección de hello **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="84b88-171">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Copia de seguridad automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="84b88-173">Hola **configuración de SQL Server** hoja, haga clic en hello **editar** botón Hola automatizada sección copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="84b88-173">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Configuración de Copia de seguridad automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="84b88-175">Cuando termine, haga clic en hello **Aceptar** botón en la parte inferior de Hola de hello **configuración de SQL Server** toosave hoja los cambios.</span><span class="sxs-lookup"><span data-stu-id="84b88-175">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="84b88-176">Si va a habilitar copia de seguridad automatizada para hello primera vez, Azure configura Hola agente de IaaS de SQL Server en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="84b88-176">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="84b88-177">Durante este tiempo, Hola portal de Azure es posible que no muestre que está configurada la copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="84b88-177">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="84b88-178">Espere unos minutos para hello toobe de agente instalado, configurado.</span><span class="sxs-lookup"><span data-stu-id="84b88-178">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="84b88-179">Después de ese hello Azure portal reflejará nueva configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="84b88-179">After that hello Azure portal will reflect hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="84b88-180">También puede usar una plantilla para configurar Copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="84b88-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="84b88-181">Para más información, consulte [la plantilla de inicio rápido de Azure para Copia de seguridad automatizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="84b88-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="84b88-182">Configuración con PowerShell</span><span class="sxs-lookup"><span data-stu-id="84b88-182">Configuration with PowerShell</span></span>

<span data-ttu-id="84b88-183">Puede usar PowerShell tooconfigure copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="84b88-183">You can use PowerShell tooconfigure Automated Backup.</span></span> <span data-ttu-id="84b88-184">Antes de comenzar:</span><span class="sxs-lookup"><span data-stu-id="84b88-184">Before you begin, you must:</span></span>

- <span data-ttu-id="84b88-185">[Descargue e instale Hola más reciente de PowerShell de Azure](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="84b88-185">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="84b88-186">Abra Windows PowerShell y asócielo con su cuenta.</span><span class="sxs-lookup"><span data-stu-id="84b88-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="84b88-187">Puede hacerlo siguiendo los pasos de Hola Hola [configurar su suscripción](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sección de hello aprovisionamiento tema.</span><span class="sxs-lookup"><span data-stu-id="84b88-187">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="84b88-188">Instalar Hola extensión de IaaS de SQL</span><span class="sxs-lookup"><span data-stu-id="84b88-188">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="84b88-189">Si se aprovisiona una máquina virtual de SQL Server de hello portal de Azure, ya debe instalarse Hola extensión de IaaS de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84b88-189">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="84b88-190">Puede determinar si se instaló para la máquina virtual mediante una llamada a **Get AzureRmVM** comando y el examen de hello **extensiones** propiedad.</span><span class="sxs-lookup"><span data-stu-id="84b88-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="84b88-191">Si Hola extensión del agente de IaaS de SQL Server está instalado, verá que aparece como "SqlIaaSAgent" o "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="84b88-191">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="84b88-192">**Estado de aprovisionamiento** para extensión de hello también debería mostrar "Correcto".</span><span class="sxs-lookup"><span data-stu-id="84b88-192">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span>

<span data-ttu-id="84b88-193">Si no está instalado o no se pudo toobe aprovisionado, puede instalarlo con el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="84b88-193">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="84b88-194">En suma toohello VM nombre del grupo de recursos, también debe especificar la región de hello (**$region**) que la máquina virtual se encuentra en.</span><span class="sxs-lookup"><span data-stu-id="84b88-194">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="84b88-195"><a id="verifysettings"></a> Verificación de la configuración actual</span><span class="sxs-lookup"><span data-stu-id="84b88-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="84b88-196">Si habilita la copia de seguridad automatizada durante el aprovisionamiento, puede usar PowerShell toocheck la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="84b88-196">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="84b88-197">Ejecute hello **Get AzureRmVMSqlServerExtension** comando y examine hello **AutoBackupSettings** propiedad:</span><span class="sxs-lookup"><span data-stu-id="84b88-197">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="84b88-198">Debería obtener siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="84b88-198">You should get output similar toohello following:</span></span>

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

<span data-ttu-id="84b88-199">Si el resultado muestra que **habilitar** se establece demasiado**False**, tendrá que tooenable la copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="84b88-199">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="84b88-200">Hello buenas noticias son que habilitar y configurar la copia de seguridad automatizada en hello igual.</span><span class="sxs-lookup"><span data-stu-id="84b88-200">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="84b88-201">Consulte la sección siguiente de hello esta información.</span><span class="sxs-lookup"><span data-stu-id="84b88-201">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="84b88-202">Si comprobar la configuración de hello inmediatamente después de realizar un cambio, es posible que se pondrá en contacto valores de configuración anteriores Hola.</span><span class="sxs-lookup"><span data-stu-id="84b88-202">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="84b88-203">Espere unos minutos y compruebe la configuración de hello nuevo toomake seguro de que se han aplicado los cambios.</span><span class="sxs-lookup"><span data-stu-id="84b88-203">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="84b88-204">Configurar Copia de seguridad automatizada</span><span class="sxs-lookup"><span data-stu-id="84b88-204">Configure Automated Backup</span></span>
<span data-ttu-id="84b88-205">Puede usar PowerShell tooenable copia de seguridad automatizada, así como toomodify su configuración y el comportamiento en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="84b88-205">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span>

<span data-ttu-id="84b88-206">En primer lugar, seleccione o cree una cuenta de almacenamiento para hello archivos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="84b88-206">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="84b88-207">Hello secuencia de comandos siguiente selecciona una cuenta de almacenamiento o lo crea si no existe.</span><span class="sxs-lookup"><span data-stu-id="84b88-207">hello following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> <span data-ttu-id="84b88-208">Copia de seguridad automatizada no permite almacenar las copias de seguridad en Premium Storage, pero pueden realizar copias de seguridad de discos de VM que usan Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="84b88-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="84b88-209">A continuación, usar hello **New-AzureRmVMSqlServerAutoBackupConfig** tooenable de comandos y configurar copias de seguridad toostore configuración de copia de seguridad automatizada de Hola Hola cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="84b88-209">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="84b88-210">En este ejemplo, las copias de seguridad de Hola se establecen toobe conserva de 10 días.</span><span class="sxs-lookup"><span data-stu-id="84b88-210">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="84b88-211">Hola segundo comando **AzureRmVMSqlServerExtension conjunto**, Hola actualizaciones especificado VM de Azure con esta configuración.</span><span class="sxs-lookup"><span data-stu-id="84b88-211">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="84b88-212">Podría tardar varios tooinstall minutos y configure Hola agente de IaaS de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84b88-212">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="84b88-213">Hay otras opciones para **AzureRmVMSqlServerAutoBackupConfig New** que aplican solo tooSQL Server 2016 y copia de seguridad automatizada v2.</span><span class="sxs-lookup"><span data-stu-id="84b88-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only tooSQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="84b88-214">SQL Server 2014 no admite Hola después de configuración: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, y **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="84b88-214">SQL Server 2014 does not support hello following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="84b88-215">Si intentas tooconfigure esta configuración en una máquina virtual de SQL Server 2014, no hay ningún error, pero no se aplica la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="84b88-215">If you attempt tooconfigure these settings on a SQL Server 2014 virtual machine, there is no error, but hello settings do not get applied.</span></span> <span data-ttu-id="84b88-216">Si desea toouse esta configuración en una máquina virtual de SQL Server 2016, consulte [v2 de copia de seguridad automatizada SQL Server 2016 máquinas virtuales de Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="84b88-216">If you want toouse these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="84b88-217">cifrado de tooenable, modificar Hola Hola de toopass de secuencia de comandos anterior **EnableEncryption** parámetro junto con una contraseña (cadena segura) para hello **CertificatePassword** parámetro.</span><span class="sxs-lookup"><span data-stu-id="84b88-217">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="84b88-218">Hola siguiente script habilita la configuración de copia de seguridad automatizada de hello en el ejemplo anterior de Hola y agrega el cifrado.</span><span class="sxs-lookup"><span data-stu-id="84b88-218">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="84b88-219">tooconfirm su configuración se aplica, [comprobar la configuración de copia de seguridad automatizada de hello](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="84b88-219">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="84b88-220">Deshabilitar Copia de seguridad automatizada</span><span class="sxs-lookup"><span data-stu-id="84b88-220">Disable Automated Backup</span></span>

<span data-ttu-id="84b88-221">toodisable copia de seguridad automatizada, ejecución Hola mismo script sin hello **-habilitar** parámetro toohello **AzureRmVMSqlServerAutoBackupConfig New** comando.</span><span class="sxs-lookup"><span data-stu-id="84b88-221">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="84b88-222">Hola ausencia de hello **-habilitar** característica de parámetro señales Hola comando toodisable Hola.</span><span class="sxs-lookup"><span data-stu-id="84b88-222">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="84b88-223">Al igual que con la instalación, puede tardar varios minutos toodisable copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="84b88-223">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="84b88-224">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="84b88-224">Example script</span></span>

<span data-ttu-id="84b88-225">Hello siguiente script proporciona un conjunto de variables que puede personalizar tooenable y configurar copia de seguridad automatizada para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="84b88-225">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="84b88-226">En su caso, tendrá que secuencia de comandos de toocustomize Hola según sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="84b88-226">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="84b88-227">Por ejemplo, podría tener cambios toomake si deseara copia de seguridad de toodisable Hola de bases de datos del sistema o habilitar el cifrado.</span><span class="sxs-lookup"><span data-stu-id="84b88-227">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="84b88-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="84b88-228">Next steps</span></span>

<span data-ttu-id="84b88-229">Copia de seguridad automatizada configura Copia de seguridad administrada en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="84b88-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="84b88-230">Por lo que es importante[revisar la documentación de Hola para copia de seguridad administrada](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Hola comportamiento e implicaciones.</span><span class="sxs-lookup"><span data-stu-id="84b88-230">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="84b88-231">Puede encontrar la copia de seguridad adicional y restaurar guía para SQL Server en máquinas virtuales de Azure en hello tema siguiente: [de copia de seguridad y restauración para SQL Server en máquinas virtuales Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="84b88-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="84b88-232">Para más información acerca de otras tareas de automatización disponibles, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="84b88-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="84b88-233">Para más información sobre cómo ejecutar SQL Server en máquinas virtuales de Azure, consulte [Introducción a SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84b88-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

