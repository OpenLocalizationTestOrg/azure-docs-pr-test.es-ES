---
title: "Creación de una máquina virtual de SQL Server en Azure PowerShell (implementación clásica)| Microsoft Docs"
description: "Ofrece pasos y scripts de PowerShell para crear una máquina virtual de Azure con imágenes de la galería de máquinas virtuales de SQL Server. En este tema se usa el modelo de implementación clásica."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: c3bd4329e8a22ce8503d6593560d29c2a3135e83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="692c8-104">Aprovisionamiento de una máquina virtual de SQL mediante Azure PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="692c8-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="692c8-105">En este artículo se ofrecen los pasos para crear una máquina virtual de SQL Server en Azure mediante los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="692c8-105">This article provides steps for how to create a SQL Server virtual machine in Azure by using the PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="692c8-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="692c8-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="692c8-107">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="692c8-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="692c8-108">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="692c8-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="692c8-109">Para ver la versión de Resource Manager de este tema, consulte [Aprovisionamiento de una máquina virtual de SQL mediante Azure PowerShell (Resource Manager)](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="692c8-109">For the Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="692c8-110">Instalación y configuración de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="692c8-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="692c8-111">Si no tiene una cuenta de Azure, visite [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="692c8-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="692c8-112">[Descargue e instale los comandos más recientes de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="692c8-112">[Download and install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="692c8-113">Inicie Windows PowerShell y conéctelo con su suscripción de Azure mediante el comando **Add-AzureAccount** .</span><span class="sxs-lookup"><span data-stu-id="692c8-113">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="692c8-114">Determinar su región de Azure de destino</span><span class="sxs-lookup"><span data-stu-id="692c8-114">Determine your target Azure region</span></span>

<span data-ttu-id="692c8-115">La máquina virtual de SQL Server se hospedará en un servicio en la nube que reside en una región de Azure específica.</span><span class="sxs-lookup"><span data-stu-id="692c8-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="692c8-116">Los siguientes pasos le ayudan a determinar la región, la cuenta de almacenamiento y servicio en la nube que se usará para el resto del tutorial.</span><span class="sxs-lookup"><span data-stu-id="692c8-116">The following steps help you to determine your region, storage account, and cloud service that will be used for the rest of the tutorial.</span></span>

1. <span data-ttu-id="692c8-117">Determine el centro de datos que quiere usar para hospedar su máquina virtual de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="692c8-117">Determine the data center that you want to use to host your SQL Server VM.</span></span> <span data-ttu-id="692c8-118">El siguiente comando de PowerShell muestra una lista de nombres de las regiones disponibles.</span><span class="sxs-lookup"><span data-stu-id="692c8-118">The following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="692c8-119">Cuando haya identificado la ubicación que prefiera, establezca una variable denominada **$dcLocation** en dicha región.</span><span class="sxs-lookup"><span data-stu-id="692c8-119">Once you've identified your preferred location, set a variable named **$dcLocation** to that region.</span></span> <span data-ttu-id="692c8-120">Por ejemplo, el siguiente comando establece la región en "este de EE. UU.":</span><span class="sxs-lookup"><span data-stu-id="692c8-120">For example, the following command sets the region to "East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="692c8-121">Establecimiento de la cuenta de suscripción y almacenamiento</span><span class="sxs-lookup"><span data-stu-id="692c8-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="692c8-122">Determinar la suscripción de Azure que usará para la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="692c8-122">Determine the Azure subscription you will use for the new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="692c8-123">Asignar su suscripción de Azure de destino a la variable **$subscr** .</span><span class="sxs-lookup"><span data-stu-id="692c8-123">Assign your target Azure subscription to the **$subscr** variable.</span></span> <span data-ttu-id="692c8-124">Establézcala como su suscripción de Azure actual.</span><span class="sxs-lookup"><span data-stu-id="692c8-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="692c8-125">Luego busque las cuentas de almacenamiento existentes.</span><span class="sxs-lookup"><span data-stu-id="692c8-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="692c8-126">El siguiente script muestra todas las cuentas de almacenamiento que existen en la región que elija:</span><span class="sxs-lookup"><span data-stu-id="692c8-126">The following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="692c8-127">Si necesita una nueva cuenta de almacenamiento, cree primero un nombre de cuenta de almacenamiento en minúsculas con el comando New-AzureStorageAccount, tal como se muestra en el siguiente ejemplo: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="692c8-127">If you require a new storage account, first create an all-lower-case storage account name with the New-AzureStorageAccount command as in the following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="692c8-128">Asigne el nombre de la cuenta de almacenamiento de destino en **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="692c8-128">Assign the target storage account name to the **$staccount**.</span></span> <span data-ttu-id="692c8-129">A continuación, use **Set-AzureSubscription** para establecer la suscripción y la cuenta de almacenamiento actual.</span><span class="sxs-lookup"><span data-stu-id="692c8-129">Then use **Set-AzureSubscription** to set the subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="692c8-130">Seleccionar una imagen de máquina virtual de SQL Server</span><span class="sxs-lookup"><span data-stu-id="692c8-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="692c8-131">Averigüe la lista de imágenes de máquinas virtuales de SQL Server disponibles de la galería.</span><span class="sxs-lookup"><span data-stu-id="692c8-131">Find out the list of available SQL Server virtual machines images from the gallery.</span></span> <span data-ttu-id="692c8-132">Todas estas imágenes tendrán una propiedad **ImageFamily** que empieza por "SQL".</span><span class="sxs-lookup"><span data-stu-id="692c8-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="692c8-133">La consulta siguiente muestra la familia de imágenes que tiene a su disposición que tiene SQL Server preinstalado.</span><span class="sxs-lookup"><span data-stu-id="692c8-133">The following query displays the image family available to you that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="692c8-134">Cuando encuentre la familia de imágenes de la máquina virtual, podría haber varias imágenes publicadas en esta familia.</span><span class="sxs-lookup"><span data-stu-id="692c8-134">When you find the  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="692c8-135">Use el siguiente script para buscar el nombre de la imagen máquina virtual publicada más reciente para su familia de imágenes seleccionada (como **SQL Server 2016 RTM Enterprise en Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="692c8-135">Use the following script to find the latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-the-virtual-machine"></a><span data-ttu-id="692c8-136">Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="692c8-136">Create the virtual machine</span></span>

<span data-ttu-id="692c8-137">Por último, cree la máquina virtual con la PowerShell:</span><span class="sxs-lookup"><span data-stu-id="692c8-137">Finally, create the virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="692c8-138">Cree un servicio en la nube para hospedar la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="692c8-138">Create a cloud service to host the new VM.</span></span> <span data-ttu-id="692c8-139">Tenga en cuenta que también es posible utilizar un servicio en la nube existente en su lugar.</span><span class="sxs-lookup"><span data-stu-id="692c8-139">Note that it is also possible to use an existing cloud service instead.</span></span> <span data-ttu-id="692c8-140">Cree una nueva variable **$svcname** con el nombre corto del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="692c8-140">Create a new variable **$svcname** with the short name of the cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="692c8-141">Especifique el nombre de la máquina virtual y un tamaño.</span><span class="sxs-lookup"><span data-stu-id="692c8-141">Specify the virtual machine name and a size.</span></span> <span data-ttu-id="692c8-142">Para obtener información sobre los tamaños de máquina virtual, consulte [Tamaños de máquina virtual para Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="692c8-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see the link to the other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="692c8-143">Especifique la cuenta de administrador local y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="692c8-143">Specify the local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type the name and password of the local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="692c8-144">Ejecute el script siguiente para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="692c8-144">Run the following script to create the virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="692c8-145">Para obtener una explicación adicional y opciones de configuración, vea la sección **Generar su conjunto de comandos** en [Usar Azure PowerShell para crear y preconfigurar máquinas virtuales basadas en Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="692c8-145">For additional explanation and configuration options, see the **Build your command set** section in [Use Azure PowerShell to create and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="692c8-146">Script de PowerShell de ejemplo</span><span class="sxs-lookup"><span data-stu-id="692c8-146">Example PowerShell script</span></span>

<span data-ttu-id="692c8-147">El siguiente script ofrece un ejemplo de un script completo que crea una máquina virtual de **SQL Server 2016 RTM Enterprise en Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="692c8-147">The following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="692c8-148">Si usa este script, debe personalizar las variables iniciales basadas en los pasos anteriores de este tema.</span><span class="sxs-lookup"><span data-stu-id="692c8-148">If you use this script, you must customize the initial variables based on the previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set the current subscription and storage account
# Comment out the New-AzureStorageAccount line if the account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select the most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create the new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create the VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type the name and password of the local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create the SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="692c8-149">Conexión con el Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="692c8-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="692c8-150">Cree los archivos .RDP en la carpeta de documentos del usuario actual para iniciar estas máquinas virtuales para completar la instalación:</span><span class="sxs-lookup"><span data-stu-id="692c8-150">Create the RDP files in the current user's document folder to launch these virtual machines to complete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="692c8-151">En el directorio de documentos, inicie el archivo RDP.</span><span class="sxs-lookup"><span data-stu-id="692c8-151">In the documents directory, launch the RDP file.</span></span> <span data-ttu-id="692c8-152">Póngase en contacto con el nombre de usuario de administrador y la contraseña que se ofreció anteriormente (por ejemplo, si su nombre de usuario era VMAdmin, especifique "\VMAdmin" como el usuario y ofrezca la contraseña).</span><span class="sxs-lookup"><span data-stu-id="692c8-152">Connect with the administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as the user and provide the password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-the-configuration-of-the-sql-server-machine-for-remote-access"></a><span data-ttu-id="692c8-153">Completar la configuración de la máquina de SQL Server para acceso remoto</span><span class="sxs-lookup"><span data-stu-id="692c8-153">Complete the configuration of the SQL Server Machine for remote access</span></span>

<span data-ttu-id="692c8-154">Después de iniciar sesión en el equipo con Escritorio remoto, configure SQL Server según las instrucciones de los [Pasos para configurar la conectividad de SQL Server en una máquina virtual de Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="692c8-154">After logging on to the machine with remote desktop, configure SQL Server based on the instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="692c8-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="692c8-155">Next steps</span></span>

<span data-ttu-id="692c8-156">Puede encontrar instrucciones adicionales para el aprovisionamiento de máquinas virtuales con PowerShell en la [documentación de máquinas virtuales](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="692c8-156">You can find additional instructions for provisioning virtual machines with PowerShell in the [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="692c8-157">En muchos casos, el siguiente paso es migrar las bases de datos a esta nueva VM de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="692c8-157">In many cases, the next step is to migrate your databases to this new SQL Server VM.</span></span> <span data-ttu-id="692c8-158">Para obtener instrucciones sobre la migración de bases de datos, consulte [Migración de una base de datos a SQL Server en una máquina virtual de Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="692c8-158">For database migration guidance, see [Migrating a Database to SQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="692c8-159">Si también le interesa utilizar Azure Portal para crear máquinas virtuales de SQL, consulte [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md)(Aprovisionamiento de una máquina virtual de SQL Server en Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="692c8-159">If you're also interested in using the Azure portal to create SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="692c8-160">Tenga en cuenta que el tutorial que le guiará a través del portal crea máquinas virtuales con el modelo recomendado del Administrador de recursos, en lugar de con el modelo clásico usado en este tema de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="692c8-160">Note that the tutorial that walks you through the portal creates VMs using the recommended Resource Manager model, rather than the classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="692c8-161">Además de estos recursos, le recomendamos que revise [otros temas relacionados con la ejecución de SQL Server en Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="692c8-161">In addition to these resources, we recommend that you review [other topics related to running SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
