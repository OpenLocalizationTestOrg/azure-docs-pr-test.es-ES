---
title: "Creación de una máquina virtual (clásica) con varias NIC (Azure PowerShell) | Microsoft Docs"
description: "Obtenga información sobre cómo crear una máquina virtual (clásica) con varias NIC mediante PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 923d4817d96399fc423b0a89cbf88f8d397f1af0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="b16f0-103">Crear una VM (clásica) con varias NIC mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="b16f0-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="b16f0-104">Puede crear máquinas virtuales (VM) en Azure y asociar varias interfaces de red (NIC) a cada una de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b16f0-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="b16f0-105">Varias NIC permiten la separación de tipos de tráfico a través de las NIC.</span><span class="sxs-lookup"><span data-stu-id="b16f0-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="b16f0-106">Por ejemplo, una NIC podría comunicarse con Internet, mientras que la otra solo se comunica con los recursos internos no conectados a Internet.</span><span class="sxs-lookup"><span data-stu-id="b16f0-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="b16f0-107">La capacidad de separar el tráfico de red a través de varias NIC es necesaria para muchos dispositivos virtuales de red, como la entrega de aplicaciones y soluciones para la optimización de WAN.</span><span class="sxs-lookup"><span data-stu-id="b16f0-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b16f0-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b16f0-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b16f0-109">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="b16f0-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="b16f0-110">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b16f0-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="b16f0-111">Obtenga información sobre cómo realizar estos pasos con el [modelo de implementación de Resource Manager](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b16f0-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="b16f0-112">En los pasos siguientes se usa un grupo de recursos denominado *IaaSStory* para los servidores web y un grupo de recursos denominado *IaaSStory-BackEnd* para los servidores de base de datos.</span><span class="sxs-lookup"><span data-stu-id="b16f0-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b16f0-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b16f0-113">Prerequisites</span></span>

<span data-ttu-id="b16f0-114">Antes de crear los servidores de base de datos, necesita crear el grupo de recursos *IaaSStory* con todos los recursos necesarios para este escenario.</span><span class="sxs-lookup"><span data-stu-id="b16f0-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="b16f0-115">Para crear estos recursos, complete los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="b16f0-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="b16f0-116">Cree una red virtual siguiendo los pasos del artículo [Create a virtual network (Crear una red virtual)](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b16f0-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="b16f0-117">Crear las máquinas virtuales back-end</span><span class="sxs-lookup"><span data-stu-id="b16f0-117">Create the back-end VMs</span></span>
<span data-ttu-id="b16f0-118">Las máquinas virtuales back-end dependen de la creación de los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="b16f0-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="b16f0-119">**Subred de back-end**.</span><span class="sxs-lookup"><span data-stu-id="b16f0-119">**Backend subnet**.</span></span> <span data-ttu-id="b16f0-120">Los servidores de bases de datos formarán parte de una subred independiente para separar el tráfico.</span><span class="sxs-lookup"><span data-stu-id="b16f0-120">The database servers will be part of a separate subnet, to segregate traffic.</span></span> <span data-ttu-id="b16f0-121">El siguiente script debe tener su subred en una red virtual denominada *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="b16f0-121">The script below expects this subnet to exist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="b16f0-122">**Cuenta de almacenamiento en discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="b16f0-122">**Storage account for data disks**.</span></span> <span data-ttu-id="b16f0-123">Para mejorar el rendimiento, los discos de datos en los servidores de base de datos usarán la tecnología de unidad de estado sólido (SSD), que requiere una cuenta de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="b16f0-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="b16f0-124">Asegúrese de que la ubicación de Azure que implementa admita el almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="b16f0-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="b16f0-125">**Conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="b16f0-125">**Availability set**.</span></span> <span data-ttu-id="b16f0-126">Todos los servidores de base de datos se agregarán al conjunto de disponibilidad único para asegurarse de que al menos una de las máquinas virtuales está activa y ejecutándose durante el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b16f0-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="b16f0-127">Paso 1: inicio del script</span><span class="sxs-lookup"><span data-stu-id="b16f0-127">Step 1 - Start your script</span></span>
<span data-ttu-id="b16f0-128">Puede descargar el script de PowerShell completo que ha usado [aquí](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="b16f0-128">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="b16f0-129">Siga los pasos siguientes para cambiar el script para que funcione en su entorno.</span><span class="sxs-lookup"><span data-stu-id="b16f0-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="b16f0-130">Cambie los valores de las variables siguientes en función de su grupo de recursos existente implementado anteriormente en [Requisitos previos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="b16f0-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="b16f0-131">Cambie los valores de las variables siguientes según los valores que desee usar para la implementación back-end.</span><span class="sxs-lookup"><span data-stu-id="b16f0-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="b16f0-132">Paso 2: creación de los recursos necesarios para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="b16f0-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="b16f0-133">Necesita crear un servicio en la nube y una cuenta de almacenamiento para los discos de datos de todas las VM.</span><span class="sxs-lookup"><span data-stu-id="b16f0-133">You need to create a new cloud service and a storage account for the data disks for all VMs.</span></span> <span data-ttu-id="b16f0-134">Asimismo, también debe especificar una imagen y una cuenta de administrador local para las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b16f0-134">You also need to specify an image, and a local administrator account for the VMs.</span></span> <span data-ttu-id="b16f0-135">Para crear estos recursos, complete los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b16f0-135">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="b16f0-136">Cree un nuevo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="b16f0-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="b16f0-137">Cree una cuenta de Almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="b16f0-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="b16f0-138">Establezca la cuenta de almacenamiento creada anteriormente como la cuenta de almacenamiento actual para la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b16f0-138">Set the storage account created above as the current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="b16f0-139">Seleccione una imagen para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b16f0-139">Select an image for the VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="b16f0-140">Establezca las credenciales de la cuenta de administrador local</span><span class="sxs-lookup"><span data-stu-id="b16f0-140">Set the local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="b16f0-141">Paso 3: crear máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="b16f0-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="b16f0-142">Debe usar un bucle para crear tantas máquinas virtuales como desee y así poder crear las NIC y las máquinas virtuales dentro del bucle.</span><span class="sxs-lookup"><span data-stu-id="b16f0-142">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="b16f0-143">Para crear las NIC y las máquinas virtuales, realice los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="b16f0-143">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="b16f0-144">Inicie un bucle `for` para repetir los comandos que se usarán para crear una máquina virtual y dos NIC tantas veces como sea necesario, según el valor de la variable `$numberOfVMs`.</span><span class="sxs-lookup"><span data-stu-id="b16f0-144">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="b16f0-145">Cree un objeto `VMConfig` especificando la imagen, el tamaño y el conjunto de disponibilidad para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b16f0-145">Create a `VMConfig` object specifying the image, size, and availability set for the VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="b16f0-146">Aprovisione la máquina virtual como una máquina virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="b16f0-146">Provision the VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="b16f0-147">Establezca la NIC predeterminada y asígnela a una dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="b16f0-147">Set the default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="b16f0-148">Agregue una segunda NIC para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b16f0-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="b16f0-149">Cree dos discos de datos para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b16f0-149">Create to data disks for each VM.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. <span data-ttu-id="b16f0-150">Cree cada máquina virtual y finalice el bucle.</span><span class="sxs-lookup"><span data-stu-id="b16f0-150">Create each VM, and end the loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="b16f0-151">Paso 4: ejecución del script</span><span class="sxs-lookup"><span data-stu-id="b16f0-151">Step 4 - Run the script</span></span>
<span data-ttu-id="b16f0-152">Ahora que descargó y cambió el script según sus necesidades, ejecute el script para crear las máquinas virtuales de la base de datos de back-end con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="b16f0-152">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="b16f0-153">Guarde el script y ejecútelo desde el símbolo del sistema **PowerShell** o desde **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="b16f0-153">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="b16f0-154">Verá el resultado inicial, tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="b16f0-154">You will see the initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="b16f0-155">Rellene la información necesaria cuando le soliciten las credenciales y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b16f0-155">Fill out the information needed in the credentials prompt and click **OK**.</span></span> <span data-ttu-id="b16f0-156">Se devuelve el resultado siguiente.</span><span class="sxs-lookup"><span data-stu-id="b16f0-156">The output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
