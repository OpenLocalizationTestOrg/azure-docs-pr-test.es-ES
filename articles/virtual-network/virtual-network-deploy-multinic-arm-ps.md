---
title: "aaaCreate una máquina virtual con varias NIC - PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con varias NIC con PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 507a413510da3ee69aefed324977ee40e442268b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="fecf7-103">Creación de una máquina virtual con varias NIC mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="fecf7-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fecf7-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fecf7-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="fecf7-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="fecf7-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="fecf7-106">Plantilla</span><span class="sxs-lookup"><span data-stu-id="fecf7-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="fecf7-107">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="fecf7-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="fecf7-108">CLI de Azure (clásico)</span><span class="sxs-lookup"><span data-stu-id="fecf7-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="fecf7-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fecf7-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="fecf7-110">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fecf7-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="fecf7-111">Hello pasos siguientes utiliza un grupo de recursos denominado *IaaSStory* para servidores WEB de Hola y un grupo de recursos denominado *IaaSStory-back-end* para servidores de Hola DB.</span><span class="sxs-lookup"><span data-stu-id="fecf7-111">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fecf7-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fecf7-112">Prerequisites</span></span>
<span data-ttu-id="fecf7-113">Para poder crear Hola servidores de base de datos, necesita hello toocreate *IaaSStory* grupo de recursos con todos los recursos necesarios de Hola para este escenario.</span><span class="sxs-lookup"><span data-stu-id="fecf7-113">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="fecf7-114">toocreate estos recursos, completar Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fecf7-114">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="fecf7-115">Navegue demasiado[página de la plantilla de hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="fecf7-115">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="fecf7-116">En página de la plantilla de hello, toohello derecha de **grupo de recursos primario**, haga clic en **implementar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="fecf7-116">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="fecf7-117">Si es necesario, cambiar los valores de parámetro de hello, a continuación, siga los pasos de hello en grupo de recursos de hello vista previa de Azure portal toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="fecf7-117">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fecf7-118">Asegúrese de que los nombres de cuenta de almacenamiento sean únicos.</span><span class="sxs-lookup"><span data-stu-id="fecf7-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="fecf7-119">No puede tener nombres de cuenta de almacenamiento duplicados en Azure.</span><span class="sxs-lookup"><span data-stu-id="fecf7-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="fecf7-120">Crear máquinas virtuales de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="fecf7-120">Create hello back-end VMs</span></span>
<span data-ttu-id="fecf7-121">Hola que dependen de las máquinas virtuales de back-end durante la creación de hello de hello recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fecf7-121">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="fecf7-122">**Cuenta de almacenamiento en discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="fecf7-122">**Storage account for data disks**.</span></span> <span data-ttu-id="fecf7-123">Para mejorar el rendimiento, los discos de datos de hello en los servidores de base de datos de hello usará la tecnología de estado sólido (SSD) de la unidad, que requiere una cuenta de almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="fecf7-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="fecf7-124">Asegúrese de hello seguro implementar almacenamiento premium de toosupport de ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="fecf7-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="fecf7-125">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="fecf7-125">**NICs**.</span></span> <span data-ttu-id="fecf7-126">Cada VM tendrá dos NIC, una para el acceso de la base de datos y otra para la administración.</span><span class="sxs-lookup"><span data-stu-id="fecf7-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="fecf7-127">**Conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="fecf7-127">**Availability set**.</span></span> <span data-ttu-id="fecf7-128">Todos los servidores de base de datos se agregarán tooa único conjunto de disponibilidad, tooensure al menos una de las máquinas virtuales de hello está en funcionamiento durante el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="fecf7-128">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="fecf7-129">Paso 1: inicio del script</span><span class="sxs-lookup"><span data-stu-id="fecf7-129">Step 1 - Start your script</span></span>
<span data-ttu-id="fecf7-130">Puede descargar Hola script completo de PowerShell usa [aquí](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="fecf7-130">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="fecf7-131">Siga los pasos de hello debajo toochange Hola script toowork en su entorno.</span><span class="sxs-lookup"><span data-stu-id="fecf7-131">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="fecf7-132">Cambiar valores de hello de hello las variables siguientes basadas en el grupo de recursos existente implementado anteriormente en [requisitos previos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="fecf7-132">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="fecf7-133">Cambiar los valores de hello de hello las variables siguientes basadas en valores de hello desea toouse para la implementación de back-end.</span><span class="sxs-lookup"><span data-stu-id="fecf7-133">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. <span data-ttu-id="fecf7-134">Recuperar recursos existentes de hello necesarios para la implementación.</span><span class="sxs-lookup"><span data-stu-id="fecf7-134">Retrieve hello existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="fecf7-135">Paso 2: creación de los recursos necesarios para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="fecf7-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="fecf7-136">Debe toocreate un nuevo grupo de recursos, una cuenta de almacenamiento hello en discos de datos, y un conjunto de disponibilidad para todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fecf7-136">You need toocreate a new resource group, a storage account for hello data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="fecf7-137">Alos necesita credenciales de cuenta de administrador local de Hola para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fecf7-137">You alos need hello local administrator account credentials for each VM.</span></span> <span data-ttu-id="fecf7-138">toocreate estos recursos, ejecute Hola lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="fecf7-138">toocreate these resources, execute hello following steps.</span></span>

1. <span data-ttu-id="fecf7-139">Cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fecf7-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="fecf7-140">Crear una nueva cuenta de almacenamiento premium en grupo de recursos de hello creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fecf7-140">Create a new premium storage account in hello resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="fecf7-141">Cree un conjunto de disponibilidad nuevo.</span><span class="sxs-lookup"><span data-stu-id="fecf7-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="fecf7-142">Obtener a administrador local de hello toobe de credenciales de cuenta utilizado para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fecf7-142">Get hello local administrator account credentials toobe used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="fecf7-143">Paso 3: crear Hola NIC y las máquinas virtuales de back-end</span><span class="sxs-lookup"><span data-stu-id="fecf7-143">Step 3 - Create hello NICs and back-end VMs</span></span>
<span data-ttu-id="fecf7-144">Deberá toouse un bucle toocreate tal y como muchas máquinas virtuales como desee y crear Hola necesarios NIC y las máquinas virtuales en el bucle de Hola.</span><span class="sxs-lookup"><span data-stu-id="fecf7-144">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="fecf7-145">Hola toocreate NIC y las máquinas virtuales, ejecute hello pasos.</span><span class="sxs-lookup"><span data-stu-id="fecf7-145">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="fecf7-146">Iniciar un `for` Hola de bucle toorepeat comandos toocreate una máquina virtual y dos NIC como tantas veces como sea necesario, basados en el valor de Hola de hello `$numberOfVMs` variable.</span><span class="sxs-lookup"><span data-stu-id="fecf7-146">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="fecf7-147">Crear Hola NIC que se usa para el acceso de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="fecf7-147">Create hello NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="fecf7-148">Crear Hola que NIC usado para acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="fecf7-148">Create hello NIC used for remote access.</span></span> <span data-ttu-id="fecf7-149">Observe cómo esta NIC tiene una tooit NSG asociado.</span><span class="sxs-lookup"><span data-stu-id="fecf7-149">Notice how this NIC has an NSG associated tooit.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="fecf7-150">Cree un objeto `vmConfig` .</span><span class="sxs-lookup"><span data-stu-id="fecf7-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="fecf7-151">Cree dos discos de datos por máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fecf7-151">Create two data disks per VM.</span></span> <span data-ttu-id="fecf7-152">Tenga en cuenta que los discos de datos de hello tienen en cuenta de almacenamiento premium de hello creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fecf7-152">Notice that hello data disks are in hello premium storage account created earlier.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. <span data-ttu-id="fecf7-153">Configurar el sistema operativo de Hola y toobe de imagen permiten Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fecf7-153">Configure hello operating system, and image toobe used for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="fecf7-154">Agregar NIC Hola dos creadas anteriormente toohello `vmConfig` objeto.</span><span class="sxs-lookup"><span data-stu-id="fecf7-154">Add hello two NICs created above toohello `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="fecf7-155">Cree el disco del sistema operativo de Hola y Hola VM.</span><span class="sxs-lookup"><span data-stu-id="fecf7-155">Create hello OS disk and create hello VM.</span></span> <span data-ttu-id="fecf7-156">Hola aviso `}` final hello `for` bucle.</span><span class="sxs-lookup"><span data-stu-id="fecf7-156">Notice hello `}` ending hello `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="fecf7-157">Paso 4: secuencia de comandos de ejecución Hola</span><span class="sxs-lookup"><span data-stu-id="fecf7-157">Step 4 - Run hello script</span></span>
<span data-ttu-id="fecf7-158">Ahora que has descargado y cambiaron el script de Hola según sus necesidades, ejecución secuencia de comandos de base de datos de back-end de hello toocreate máquinas virtuales con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="fecf7-158">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="fecf7-159">Guardar el script y ejecútelo desde hello **PowerShell** símbolo del sistema, o **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="fecf7-159">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="fecf7-160">Verá Hola resultado inicial, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="fecf7-160">You will see hello initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="fecf7-161">Después de unos minutos, rellene aviso de credenciales de Hola y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fecf7-161">After a few minutes, fill out hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="fecf7-162">salida de Hello siguiente representa una sola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fecf7-162">hello output below represents a single VM.</span></span> <span data-ttu-id="fecf7-163">Aviso Hola todo proceso tardó toocomplete 8 minutos.</span><span class="sxs-lookup"><span data-stu-id="fecf7-163">Notice hello entire process took 8 minutes toocomplete.</span></span>

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK
