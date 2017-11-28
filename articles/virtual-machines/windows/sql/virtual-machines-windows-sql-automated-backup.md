---
title: Copia de seguridad automatizada para SQL Server 2014 en Azure Virtual Machines | Microsoft Docs
description: "Se explica la característica Copia de seguridad automatizada para SQL Server 2014 en máquinas virtuales que se ejecutan en Azure. Este artículo trata exactamente sobre las máquinas virtuales que usan Resource Manager."
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
ms.openlocfilehash: 91aab896dd5f06c950ee0ed8f36cc6a953d91611
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="3529e-104">Copia de seguridad automatizada para SQL Server 2014 en Azure Virtual Machines (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="3529e-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3529e-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="3529e-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="3529e-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="3529e-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="3529e-107">Copia de seguridad automatizada configura automáticamente [Copia de seguridad administrada para Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todas las bases de datos existentes y nuevas en una máquina virtual de Azure que ejecuta SQL Server 2014 Standard y Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3529e-107">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="3529e-108">Esto le permite configurar copias de seguridad de datos normales que utilizan el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="3529e-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="3529e-109">Copia de seguridad automatizada se basa en la [Extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3529e-109">Automated Backup depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="3529e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3529e-110">Prerequisites</span></span>
<span data-ttu-id="3529e-111">Para utilizar Copia de seguridad automatizada, tenga en cuenta los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="3529e-111">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="3529e-112">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="3529e-112">**Operating System**:</span></span>

- <span data-ttu-id="3529e-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3529e-113">Windows Server 2012</span></span>
- <span data-ttu-id="3529e-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3529e-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="3529e-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3529e-115">Windows Server 2016</span></span>

<span data-ttu-id="3529e-116">**Edición/versión de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="3529e-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="3529e-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="3529e-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="3529e-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="3529e-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3529e-119">Copia de seguridad automatizada funciona con SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="3529e-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="3529e-120">Si usa SQL Server 2016, puede usar Copia de seguridad automatizada v2 para hacer copias de seguridad de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="3529e-120">If you are using SQL Server 2016, you can use Automated Backup v2 to back up your databases.</span></span> <span data-ttu-id="3529e-121">Para obtener más información, vea [Copia de seguridad automatizada v2 para SQL Server 2016 en Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="3529e-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="3529e-122">**Configuración de base de datos**:</span><span class="sxs-lookup"><span data-stu-id="3529e-122">**Database configuration**:</span></span>

- <span data-ttu-id="3529e-123">Las bases de datos de destino deben utilizar el modelo de recuperación completa.</span><span class="sxs-lookup"><span data-stu-id="3529e-123">Target databases must use the full recovery model.</span></span> <span data-ttu-id="3529e-124">Para obtener más información sobre el impacto del modelo de recuperación completa en las copias de seguridad, vea [Copia de seguridad en el modelo de recuperación completa](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="3529e-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="3529e-125">Las bases de datos de destino deben estar en la instancia predeterminada de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3529e-125">Target databases must be on the default SQL Server instance.</span></span> <span data-ttu-id="3529e-126">La extensión de IaaS de SQL Server no admite instancias con nombre.</span><span class="sxs-lookup"><span data-stu-id="3529e-126">The SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="3529e-127">**Modelo de implementación de Azure**:</span><span class="sxs-lookup"><span data-stu-id="3529e-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="3529e-128">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3529e-128">Resource Manager</span></span>

<span data-ttu-id="3529e-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="3529e-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="3529e-130">[Instale los comandos de Azure PowerShell más recientes](/powershell/azure/overview) si planea configurar Copia de seguridad automatizada con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3529e-130">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="3529e-131">Copia de seguridad automatizada se basa en la Extensión Agente de IaaS de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3529e-131">Automated Backup relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="3529e-132">Las imágenes actuales de la galería de máquinas virtuales de SQL agregan esta extensión de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3529e-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="3529e-133">Para más información, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3529e-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="3529e-134">Settings</span><span class="sxs-lookup"><span data-stu-id="3529e-134">Settings</span></span>

<span data-ttu-id="3529e-135">En la siguiente tabla se describen las opciones que pueden configurarse para Copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="3529e-135">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="3529e-136">Los pasos de configuración reales varían si usa Azure Portal o comandos de Windows PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="3529e-136">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="3529e-137">Configuración</span><span class="sxs-lookup"><span data-stu-id="3529e-137">Setting</span></span> | <span data-ttu-id="3529e-138">Intervalo (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="3529e-138">Range (Default)</span></span> | <span data-ttu-id="3529e-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="3529e-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3529e-140">**Copia de seguridad automatizada**</span><span class="sxs-lookup"><span data-stu-id="3529e-140">**Automated Backup**</span></span> | <span data-ttu-id="3529e-141">Habilitar/deshabilitar (deshabilitado)</span><span class="sxs-lookup"><span data-stu-id="3529e-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="3529e-142">Habilita o deshabilita la copia de seguridad automatizada para una máquina virtual de Azure que ejecuta SQL Server 2014 Standard o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3529e-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="3529e-143">**Período de retención**</span><span class="sxs-lookup"><span data-stu-id="3529e-143">**Retention Period**</span></span> | <span data-ttu-id="3529e-144">1-30 días (30 días)</span><span class="sxs-lookup"><span data-stu-id="3529e-144">1-30 days (30 days)</span></span> | <span data-ttu-id="3529e-145">El número de días para retener una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3529e-145">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="3529e-146">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="3529e-146">**Storage Account**</span></span> | <span data-ttu-id="3529e-147">Cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3529e-147">Azure storage account</span></span> | <span data-ttu-id="3529e-148">Una cuenta de Azure Storage que usar para almacenar archivos de Copia de seguridad automatizada en Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="3529e-148">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="3529e-149">Se crea un contenedor en esta ubicación para guardar todos los archivos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3529e-149">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="3529e-150">La convención de nomenclatura del archivo de copia de seguridad incluye la fecha, la hora y el nombre de máquina.</span><span class="sxs-lookup"><span data-stu-id="3529e-150">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="3529e-151">**Cifrado**</span><span class="sxs-lookup"><span data-stu-id="3529e-151">**Encryption**</span></span> | <span data-ttu-id="3529e-152">Habilitar/deshabilitar (deshabilitado)</span><span class="sxs-lookup"><span data-stu-id="3529e-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="3529e-153">Habilita o deshabilita el cifrado.</span><span class="sxs-lookup"><span data-stu-id="3529e-153">Enables or disables encryption.</span></span> <span data-ttu-id="3529e-154">Cuando se habilita el cifrado, los certificados usados para restaurar la copia de seguridad se ubican en la cuenta de almacenamiento especificada en el mismo contenedor `automaticbackup` con la misma convención de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="3529e-154">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same `automaticbackup` container using the same naming convention.</span></span> <span data-ttu-id="3529e-155">Si la contraseña cambia, se genera un nuevo certificado con esa contraseña, pero el certificado antiguo permanece para restaurar copias de seguridad anteriores.</span><span class="sxs-lookup"><span data-stu-id="3529e-155">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="3529e-156">**Password**</span><span class="sxs-lookup"><span data-stu-id="3529e-156">**Password**</span></span> | <span data-ttu-id="3529e-157">Texto de contraseña</span><span class="sxs-lookup"><span data-stu-id="3529e-157">Password text</span></span> | <span data-ttu-id="3529e-158">Una contraseña para claves de cifrado.</span><span class="sxs-lookup"><span data-stu-id="3529e-158">A password for encryption keys.</span></span> <span data-ttu-id="3529e-159">Esto solo es necesario si se habilita el cifrado.</span><span class="sxs-lookup"><span data-stu-id="3529e-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="3529e-160">Para restaurar una copia de seguridad cifrada, debe disponer de la contraseña correcta y del certificado relacionado que se usó en el momento en el que se realizó la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3529e-160">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="3529e-161">Configuración en el Portal</span><span class="sxs-lookup"><span data-stu-id="3529e-161">Configuration in the Portal</span></span>

<span data-ttu-id="3529e-162">Puede usar Azure Portal para configurar Copia de seguridad automatizada durante el aprovisionamiento o para las máquinas virtuales existentes de SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="3529e-162">You can use the Azure portal to configure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="3529e-163">Nuevas máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="3529e-163">New VMs</span></span>

<span data-ttu-id="3529e-164">Utilice Azure Portal para configurar la opción Copia de seguridad automatizada cuando cree una nueva máquina virtual con SQL Server 2014 en el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3529e-164">Use the Azure portal to configure Automated Backup when you create a new SQL Server 2014 Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="3529e-165">En la hoja **Configuración de SQL Server**, seleccione **Copia de seguridad automatizada**.</span><span class="sxs-lookup"><span data-stu-id="3529e-165">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="3529e-166">La siguiente captura de pantalla de Azure Portal muestra la hoja **Copia de seguridad automatizada de SQL** .</span><span class="sxs-lookup"><span data-stu-id="3529e-166">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![Configuración de Copia de seguridad automatizada de SQL en Azure Portal](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="3529e-168">Para conocer el contexto, consulte el tema completo en [Aprovisionamiento de una máquina virtual de SQL Server en Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="3529e-168">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="3529e-169">Máquinas virtuales existentes</span><span class="sxs-lookup"><span data-stu-id="3529e-169">Existing VMs</span></span>

<span data-ttu-id="3529e-170">Para las máquinas virtuales de SQL Server existentes, seleccione su máquina virtual de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3529e-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="3529e-171">Después, seleccione la sección **Configuración de SQL Server** de la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="3529e-171">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Copia de seguridad automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="3529e-173">En la hoja **Configuración de SQL Server**, haga clic en el botón **Editar** de la sección Copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="3529e-173">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![Configuración de Copia de seguridad automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="3529e-175">Cuando termine, haga clic en el botón **Aceptar** situado en la parte inferior de la hoja **Configuración de SQL Server** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="3529e-175">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="3529e-176">Si habilita Copia de seguridad automatizada por primera vez, Azure configura el Agente de IaaS de SQL Server en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="3529e-176">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="3529e-177">Durante este tiempo, es posible que Azure Portal no muestre que se ha configurado Copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="3529e-177">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="3529e-178">Espere unos minutos hasta que el agente se instale y configure.</span><span class="sxs-lookup"><span data-stu-id="3529e-178">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="3529e-179">Después, Azure Portal mostrará la nueva configuración.</span><span class="sxs-lookup"><span data-stu-id="3529e-179">After that the Azure portal will reflect the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="3529e-180">También puede usar una plantilla para configurar Copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="3529e-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="3529e-181">Para más información, consulte [la plantilla de inicio rápido de Azure para Copia de seguridad automatizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="3529e-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="3529e-182">Configuración con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3529e-182">Configuration with PowerShell</span></span>

<span data-ttu-id="3529e-183">Puede usar PowerShell para configurar Copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="3529e-183">You can use PowerShell to configure Automated Backup.</span></span> <span data-ttu-id="3529e-184">Antes de comenzar:</span><span class="sxs-lookup"><span data-stu-id="3529e-184">Before you begin, you must:</span></span>

- <span data-ttu-id="3529e-185">[Descargue e instale la última versión de Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="3529e-185">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="3529e-186">Abra Windows PowerShell y asócielo con su cuenta.</span><span class="sxs-lookup"><span data-stu-id="3529e-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="3529e-187">Puede hacerlo siguiendo los pasos descritos en la sección [Configuración de su suscripción](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) del tema sobre aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="3529e-187">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="3529e-188">Instalación de la extensión IaaS de SQL Server</span><span class="sxs-lookup"><span data-stu-id="3529e-188">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="3529e-189">Si se aprovisiona una máquina virtual con SQL Server desde Azure Portal, la extensión IaaS de SQL Server también debe estar instalada.</span><span class="sxs-lookup"><span data-stu-id="3529e-189">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="3529e-190">Puede determinar si está instalada para la VM llamando al comando **Get-AzureRmVM** y examinando la propiedad **Extensiones**.</span><span class="sxs-lookup"><span data-stu-id="3529e-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="3529e-191">Si la extensión del agente IaaS de SQL Server está instalada, debe aparecer como "SqlIaaSAgent" o "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="3529e-191">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="3529e-192">**ProvisioningState** para la extensión también debería aparecer como “Correcto”.</span><span class="sxs-lookup"><span data-stu-id="3529e-192">**ProvisioningState** for the extension should also show “Succeeded”.</span></span>

<span data-ttu-id="3529e-193">Si no está instalada o no se ha podido aprovisionar, puede instalarla con el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="3529e-193">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="3529e-194">Además del grupo de recursos y del nombre de VM, también debe especificar la región (**$region**) en que se encuentra dicha VM.</span><span class="sxs-lookup"><span data-stu-id="3529e-194">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="3529e-195"><a id="verifysettings"></a> Verificación de la configuración actual</span><span class="sxs-lookup"><span data-stu-id="3529e-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="3529e-196">Si ha habilitado la copia de seguridad automatizada durante el aprovisionamiento, puede usar PowerShell para comprobar la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="3529e-196">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="3529e-197">Ejecute el comando **Get-AzureRmVMSqlServerExtension** y examine la propiedad **AutoBackupSettings**:</span><span class="sxs-lookup"><span data-stu-id="3529e-197">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="3529e-198">Debería obtener una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="3529e-198">You should get output similar to the following:</span></span>

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

<span data-ttu-id="3529e-199">Si la salida muestra que la opción **Habilitar** está establecida en **False**, tiene que habilitar la copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="3529e-199">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="3529e-200">Lo bueno es que habilita y configura la copia de seguridad automatizada de la misma manera.</span><span class="sxs-lookup"><span data-stu-id="3529e-200">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="3529e-201">Vea la sección siguiente para leer esta información.</span><span class="sxs-lookup"><span data-stu-id="3529e-201">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="3529e-202">Si comprueba la configuración inmediatamente después de realizar un cambio, es posible que obtenga los valores de configuración anteriores.</span><span class="sxs-lookup"><span data-stu-id="3529e-202">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="3529e-203">Espere unos minutos y compruebe la configuración de nuevo para asegurarse de que se hayan aplicado los cambios.</span><span class="sxs-lookup"><span data-stu-id="3529e-203">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="3529e-204">Configurar Copia de seguridad automatizada</span><span class="sxs-lookup"><span data-stu-id="3529e-204">Configure Automated Backup</span></span>
<span data-ttu-id="3529e-205">Puede usar PowerShell para habilitar la copia de seguridad automatizada, así como para modificar su configuración y comportamiento en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="3529e-205">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span>

<span data-ttu-id="3529e-206">En primer lugar, seleccione o cree una cuenta de almacenamiento para los archivos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3529e-206">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="3529e-207">El script siguiente selecciona una cuenta de almacenamiento o la crea si no existe.</span><span class="sxs-lookup"><span data-stu-id="3529e-207">The following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="3529e-208">Copia de seguridad automatizada no permite almacenar las copias de seguridad en Premium Storage, pero pueden realizar copias de seguridad de discos de VM que usan Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="3529e-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="3529e-209">Luego use el comando **New-AzureRmVMSqlServerAutoBackupConfig** para habilitar y configurar los valores de Copia de seguridad automatizada para almacenar copias de seguridad en la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3529e-209">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="3529e-210">En este ejemplo, las copias de seguridad están configuradas para que se conserven durante 10 días.</span><span class="sxs-lookup"><span data-stu-id="3529e-210">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="3529e-211">El segundo comando, **Set-AzureRmVMSqlServerExtension**, actualiza la VM de Azure especificada con esta configuración.</span><span class="sxs-lookup"><span data-stu-id="3529e-211">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="3529e-212">La instalación y configuración del agente de Iaas de SQL Server puede tardar algunos minutos.</span><span class="sxs-lookup"><span data-stu-id="3529e-212">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="3529e-213">Hay otras opciones de **New-AzureRmVMSqlServerAutoBackupConfig** que solo se aplican a SQL Server 2016 y a Copia de seguridad automatizada v2.</span><span class="sxs-lookup"><span data-stu-id="3529e-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only to SQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="3529e-214">SQL Server 2014 no es compatible con las siguientes opciones: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours** y **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="3529e-214">SQL Server 2014 does not support the following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="3529e-215">Si intenta configurar estas opciones en una máquina virtual de SQL Server 2014, no hay ningún error, pero no se aplica la configuración.</span><span class="sxs-lookup"><span data-stu-id="3529e-215">If you attempt to configure these settings on a SQL Server 2014 virtual machine, there is no error, but the settings do not get applied.</span></span> <span data-ttu-id="3529e-216">Si quiere usar estas opciones en una máquina virtual de SQL Server 2016, vea [Copia de seguridad automatizada v2 para Azure Virtual Machines con SQL Server 2016 (Resource Manager)](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="3529e-216">If you want to use these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="3529e-217">Para habilitar el cifrado, modifique el script anterior para pasar el parámetro **EnableEncryption** junto con una contraseña (cadena segura) para el parámetro **CertificatePassword**.</span><span class="sxs-lookup"><span data-stu-id="3529e-217">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="3529e-218">El siguiente script habilita la configuración de Copia de seguridad automatizada en el ejemplo anterior y agrega cifrado.</span><span class="sxs-lookup"><span data-stu-id="3529e-218">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

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

<span data-ttu-id="3529e-219">Para confirmar que se ha aplicado la configuración, [verifique la configuración de Copia de seguridad automatizada](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="3529e-219">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="3529e-220">Deshabilitar Copia de seguridad automatizada</span><span class="sxs-lookup"><span data-stu-id="3529e-220">Disable Automated Backup</span></span>

<span data-ttu-id="3529e-221">Para deshabilitar Copia de seguridad automatizada, ejecute el mismo script sin el parámetro **-Enable** en el comando **New-AzureRmVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="3529e-221">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="3529e-222">La ausencia del parámetro **-Enable** indica al comando que deshabilite la característica.</span><span class="sxs-lookup"><span data-stu-id="3529e-222">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="3529e-223">Al igual que la instalación, la deshabilitación de Copia de seguridad automatizada puede tardar algunos minutos.</span><span class="sxs-lookup"><span data-stu-id="3529e-223">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="3529e-224">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3529e-224">Example script</span></span>

<span data-ttu-id="3529e-225">El script siguiente proporciona un conjunto de variables que se pueden personalizar para habilitar y configurar Copia de seguridad automatizada para la VM.</span><span class="sxs-lookup"><span data-stu-id="3529e-225">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="3529e-226">En su caso, debe personalizar el script en función de sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="3529e-226">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="3529e-227">Por ejemplo, debe realizar cambios si desea deshabilitar la copia de seguridad de bases de datos del sistema o habilitar el cifrado.</span><span class="sxs-lookup"><span data-stu-id="3529e-227">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="3529e-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3529e-228">Next steps</span></span>

<span data-ttu-id="3529e-229">Copia de seguridad automatizada configura Copia de seguridad administrada en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="3529e-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="3529e-230">Por lo tanto, es importante [revisar la documentación de la Copia de seguridad administrada](https://msdn.microsoft.com/library/dn449496.aspx) para comprender el comportamiento y las implicaciones.</span><span class="sxs-lookup"><span data-stu-id="3529e-230">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="3529e-231">Puede encontrar directrices adicionales sobre la copia de seguridad y la restauración para SQL Server en máquinas virtuales de Azure en el siguiente tema: [Copias de seguridad y restauración para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="3529e-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="3529e-232">Para más información acerca de otras tareas de automatización disponibles, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3529e-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="3529e-233">Para más información sobre cómo ejecutar SQL Server en máquinas virtuales de Azure, consulte [Introducción a SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3529e-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

