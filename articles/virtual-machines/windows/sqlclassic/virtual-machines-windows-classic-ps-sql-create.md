---
title: "aaaCreate una máquina Virtual de SQL Server en PowerShell de Azure (clásica) | Documentos de Microsoft"
description: "Ofrece pasos y scripts de PowerShell para crear una máquina virtual de Azure con imágenes de la galería de máquinas virtuales de SQL Server. En este tema usa el modo de implementación clásica de Hola."
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
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="6805a-104">Aprovisionamiento de una máquina virtual de SQL mediante Azure PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="6805a-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="6805a-105">Este artículo proporciona los pasos para cómo toocreate una máquina virtual de SQL Server en Azure mediante el uso de Hola cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6805a-105">This article provides steps for how toocreate a SQL Server virtual machine in Azure by using hello PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="6805a-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6805a-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6805a-107">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="6805a-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6805a-108">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6805a-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="6805a-109">Para la versión del Administrador de recursos de Hola de este tema, consulte [aprovisionar una máquina virtual de SQL Server con el Administrador de recursos de Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="6805a-109">For hello Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="6805a-110">Instalación y configuración de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6805a-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="6805a-111">Si no tiene una cuenta de Azure, visite [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6805a-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="6805a-112">[Descargue e instale los comandos de PowerShell de Azure más recientes de hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6805a-112">[Download and install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="6805a-113">Inicie Windows PowerShell y conectar tooyour suscripción de Azure con hello **Add-AzureAccount** comando.</span><span class="sxs-lookup"><span data-stu-id="6805a-113">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="6805a-114">Determinar su región de Azure de destino</span><span class="sxs-lookup"><span data-stu-id="6805a-114">Determine your target Azure region</span></span>

<span data-ttu-id="6805a-115">La máquina virtual de SQL Server se hospedará en un servicio en la nube que reside en una región de Azure específica.</span><span class="sxs-lookup"><span data-stu-id="6805a-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="6805a-116">Hello pasos siguientes ayudarán a toodetermine su región, la cuenta de almacenamiento y el servicio de nube que se usará para el resto de Hola de tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="6805a-116">hello following steps help you toodetermine your region, storage account, and cloud service that will be used for hello rest of hello tutorial.</span></span>

1. <span data-ttu-id="6805a-117">Determine el centro de datos de Hola que desea toouse toohost la VM de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6805a-117">Determine hello data center that you want toouse toohost your SQL Server VM.</span></span> <span data-ttu-id="6805a-118">Hola siguiente comando de PowerShell muestra una lista de nombres de las regiones disponibles.</span><span class="sxs-lookup"><span data-stu-id="6805a-118">hello following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="6805a-119">Una vez que haya identificado la ubicación preferida, Establece una variable denominada **$dcLocation** toothat región.</span><span class="sxs-lookup"><span data-stu-id="6805a-119">Once you've identified your preferred location, set a variable named **$dcLocation** toothat region.</span></span> <span data-ttu-id="6805a-120">Hola, por ejemplo, el siguiente comando establece Hola región demasiado "UU":</span><span class="sxs-lookup"><span data-stu-id="6805a-120">For example, hello following command sets hello region too"East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="6805a-121">Establecimiento de la cuenta de suscripción y almacenamiento</span><span class="sxs-lookup"><span data-stu-id="6805a-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="6805a-122">Determinar Hola va a utilizar para la nueva máquina virtual de Hola de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="6805a-122">Determine hello Azure subscription you will use for hello new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="6805a-123">Asignar su toohello de suscripción de Azure de destino **$subscr** variable.</span><span class="sxs-lookup"><span data-stu-id="6805a-123">Assign your target Azure subscription toohello **$subscr** variable.</span></span> <span data-ttu-id="6805a-124">Establézcala como su suscripción de Azure actual.</span><span class="sxs-lookup"><span data-stu-id="6805a-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="6805a-125">Luego busque las cuentas de almacenamiento existentes.</span><span class="sxs-lookup"><span data-stu-id="6805a-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="6805a-126">Hello secuencia de comandos siguiente muestra todas las cuentas de almacenamiento que existen en su región elegido:</span><span class="sxs-lookup"><span data-stu-id="6805a-126">hello following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="6805a-127">Si necesita una cuenta de almacenamiento, cree primero un nombre de cuenta de almacenamiento de todas las minúsculas con el comando hello AzureStorageAccount de nuevo como en el siguiente ejemplo de Hola:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="6805a-127">If you require a new storage account, first create an all-lower-case storage account name with hello New-AzureStorageAccount command as in hello following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="6805a-128">Asignar toohello de nombre de cuenta de hello destino almacenamiento **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="6805a-128">Assign hello target storage account name toohello **$staccount**.</span></span> <span data-ttu-id="6805a-129">A continuación, utilice **Set-AzureSubscription** tooset Hola suscripción y la cuenta de almacenamiento actual.</span><span class="sxs-lookup"><span data-stu-id="6805a-129">Then use **Set-AzureSubscription** tooset hello subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="6805a-130">Seleccionar una imagen de máquina virtual de SQL Server</span><span class="sxs-lookup"><span data-stu-id="6805a-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="6805a-131">Obtener lista de Hola de imágenes de máquinas virtuales de SQL Server disponibles desde la Galería de Hola.</span><span class="sxs-lookup"><span data-stu-id="6805a-131">Find out hello list of available SQL Server virtual machines images from hello gallery.</span></span> <span data-ttu-id="6805a-132">Todas estas imágenes tendrán una propiedad **ImageFamily** que empieza por "SQL".</span><span class="sxs-lookup"><span data-stu-id="6805a-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="6805a-133">Hola siguiente de consulta muestra hello imagen familia disponibles tooyou que tiene preinstalado de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6805a-133">hello following query displays hello image family available tooyou that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="6805a-134">Cuando encuentre la familia de imágenes de máquina virtual de hello, podría haber varias imágenes publicadas en esta familia.</span><span class="sxs-lookup"><span data-stu-id="6805a-134">When you find hello  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="6805a-135">Script siguiente de Hola de uso se toofind hello más reciente publicada imagen nombre de máquina virtual su familia de la imagen seleccionada (como **SQL Server 2016 RTM Enterprise en Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="6805a-135">Use hello following script toofind hello latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a><span data-ttu-id="6805a-136">Crear la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="6805a-136">Create hello virtual machine</span></span>

<span data-ttu-id="6805a-137">Por último, crear máquina virtual de hello con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6805a-137">Finally, create hello virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="6805a-138">Crear una nube servicio toohost Hola nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6805a-138">Create a cloud service toohost hello new VM.</span></span> <span data-ttu-id="6805a-139">Tenga en cuenta que también es posible toouse un servicio de nube existente en su lugar.</span><span class="sxs-lookup"><span data-stu-id="6805a-139">Note that it is also possible toouse an existing cloud service instead.</span></span> <span data-ttu-id="6805a-140">Crear una nueva variable **$svcname** con nombre corto de hello del servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="6805a-140">Create a new variable **$svcname** with hello short name of hello cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="6805a-141">Especifique el nombre de la máquina virtual de Hola y un tamaño.</span><span class="sxs-lookup"><span data-stu-id="6805a-141">Specify hello virtual machine name and a size.</span></span> <span data-ttu-id="6805a-142">Para obtener información sobre los tamaños de máquina virtual, consulte [Tamaños de máquina virtual para Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6805a-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="6805a-143">Especifique la contraseña y la cuenta de administrador local de Hola.</span><span class="sxs-lookup"><span data-stu-id="6805a-143">Specify hello local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="6805a-144">Ejecute hello después de la máquina virtual de secuencia de comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="6805a-144">Run hello following script toocreate hello virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="6805a-145">Para obtener una explicación adicional y opciones de configuración, vea hello **el conjunto de comandos de compilación** sección [toocreate usar Azure PowerShell y preconfigurar máquinas virtuales basadas en Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6805a-145">For additional explanation and configuration options, see hello **Build your command set** section in [Use Azure PowerShell toocreate and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="6805a-146">Script de PowerShell de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6805a-146">Example PowerShell script</span></span>

<span data-ttu-id="6805a-147">Hello script siguiente proporciona un ejemplo de un script completo que crea un **SQL Server 2016 RTM Enterprise en Windows Server 2012 R2** máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6805a-147">hello following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="6805a-148">Si utiliza esta secuencia de comandos, debe personalizar variables iniciales Hola basadas en los pasos anteriores hello en este tema.</span><span class="sxs-lookup"><span data-stu-id="6805a-148">If you use this script, you must customize hello initial variables based on hello previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="6805a-149">Conexión con el Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="6805a-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="6805a-150">Crear archivos RDP de hello en toolaunch de carpeta de documentos del usuario actual de hello estas máquinas virtuales toocomplete el programa de instalación:</span><span class="sxs-lookup"><span data-stu-id="6805a-150">Create hello RDP files in hello current user's document folder toolaunch these virtual machines toocomplete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="6805a-151">En el directorio de documentos de hello, inicie el archivo RDP de hello.</span><span class="sxs-lookup"><span data-stu-id="6805a-151">In hello documents directory, launch hello RDP file.</span></span> <span data-ttu-id="6805a-152">Conectar con el nombre de usuario de administrador de Hola y la contraseña que proporcionó anteriormente (por ejemplo, si su nombre de usuario era VMAdmin, especifique "\VMAdmin" como usuario de Hola y proporcionar la contraseña de hello).</span><span class="sxs-lookup"><span data-stu-id="6805a-152">Connect with hello administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as hello user and provide hello password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a><span data-ttu-id="6805a-153">Configuración de hello completa de hello equipo con SQL Server para el acceso remoto</span><span class="sxs-lookup"><span data-stu-id="6805a-153">Complete hello configuration of hello SQL Server Machine for remote access</span></span>

<span data-ttu-id="6805a-154">Después de iniciar sesión en la máquina de toohello con Escritorio remoto, configure SQL Server según las instrucciones de hello en [pasos para configurar la conectividad de SQL Server en una máquina virtual de Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="6805a-154">After logging on toohello machine with remote desktop, configure SQL Server based on hello instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6805a-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6805a-155">Next steps</span></span>

<span data-ttu-id="6805a-156">Encontrará instrucciones adicionales para el aprovisionamiento de máquinas virtuales con PowerShell en hello [documentación de máquinas virtuales](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6805a-156">You can find additional instructions for provisioning virtual machines with PowerShell in hello [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="6805a-157">En muchos casos, Hola siguiente paso es toomigrate su toothis de bases de datos nueva VM de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6805a-157">In many cases, hello next step is toomigrate your databases toothis new SQL Server VM.</span></span> <span data-ttu-id="6805a-158">Para obtener instrucciones de migración de base de datos, vea [migrar un servidor en una máquina virtual de Azure de base de datos tooSQL](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6805a-158">For database migration guidance, see [Migrating a Database tooSQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="6805a-159">Si también está interesado en usar hello toocreate portal Azure máquinas virtuales de SQL, vea [aprovisionamiento de una máquina Virtual de SQL Server en Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="6805a-159">If you're also interested in using hello Azure portal toocreate SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="6805a-160">Tenga en cuenta este tutorial Hola que le guían a través del portal de hello crea máquinas virtuales con los recorridos Hola modelo recomendado de administrador de recursos, en lugar de modelo clásico Hola utilizado en este tema de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6805a-160">Note that hello tutorial that walks you through hello portal creates VMs using hello recommended Resource Manager model, rather than hello classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="6805a-161">Además recursos toothese, le recomendamos que revise [otros temas relacionados con SQL Server en máquinas virtuales Azure toorunning](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6805a-161">In addition toothese resources, we recommend that you review [other topics related toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
