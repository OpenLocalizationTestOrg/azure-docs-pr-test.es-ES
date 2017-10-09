---
title: "aaaCreate una máquina virtual (clásica) con varias NIC - PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual (clásica) con varias NIC con PowerShell."
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
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="6e4cf-103">Crear una VM (clásica) con varias NIC mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e4cf-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="6e4cf-104">Puede crear máquinas virtuales (VM) en Azure y conectar múltiples tooeach (NIC) de interfaces de red de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="6e4cf-105">Varias NIC permiten la separación de tipos de tráfico a través de las NIC.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="6e4cf-106">Por ejemplo, una que NIC puede comunicarse con hello Internet, mientras que otra solo se comunica con los recursos internos no conectado toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="6e4cf-107">tráfico de red de Hello capacidad tooseparate entre varios NIC es necesario para muchos dispositivos virtuales red, por ejemplo, la entrega de aplicaciones y soluciones de optimización de la WAN.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e4cf-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6e4cf-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6e4cf-109">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="6e4cf-110">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6e4cf-111">Obtenga información acerca de cómo tooperform estos pasos con hello [modelo de implementación del Administrador de recursos](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6e4cf-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="6e4cf-112">Hello pasos siguientes utiliza un grupo de recursos denominado *IaaSStory* para servidores WEB de Hola y un grupo de recursos denominado *IaaSStory-back-end* para servidores de Hola DB.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e4cf-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6e4cf-113">Prerequisites</span></span>

<span data-ttu-id="6e4cf-114">Para poder crear Hola servidores de base de datos, necesita hello toocreate *IaaSStory* grupo de recursos con todos los recursos necesarios de Hola para este escenario.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="6e4cf-115">toocreate Hola a estos recursos, completados los pasos que siguen.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="6e4cf-116">Crear una red virtual, siga los pasos de Hola Hola [crear una red virtual](virtual-networks-create-vnet-classic-netcfg-ps.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="6e4cf-117">Crear máquinas virtuales de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="6e4cf-117">Create hello back-end VMs</span></span>
<span data-ttu-id="6e4cf-118">Hola que dependen de las máquinas virtuales de back-end durante la creación de hello de hello recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6e4cf-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="6e4cf-119">**Subred de back-end**.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-119">**Backend subnet**.</span></span> <span data-ttu-id="6e4cf-120">servidores de base de datos de Hello va a formar parte de una subred independiente, toosegregate tráfico.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-120">hello database servers will be part of a separate subnet, toosegregate traffic.</span></span> <span data-ttu-id="6e4cf-121">script de Hola siguiente espera este tooexist de subred en una red virtual denominada *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-121">hello script below expects this subnet tooexist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="6e4cf-122">**Cuenta de almacenamiento en discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-122">**Storage account for data disks**.</span></span> <span data-ttu-id="6e4cf-123">Para mejorar el rendimiento, los discos de datos de hello en los servidores de base de datos de hello usará la tecnología de estado sólido (SSD) de la unidad, que requiere una cuenta de almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="6e4cf-124">Asegúrese de hello seguro implementar almacenamiento premium de toosupport de ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="6e4cf-125">**Conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-125">**Availability set**.</span></span> <span data-ttu-id="6e4cf-126">Todos los servidores de base de datos se agregarán tooa único conjunto de disponibilidad, tooensure al menos una de las máquinas virtuales de hello está en funcionamiento durante el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="6e4cf-127">Paso 1: inicio del script</span><span class="sxs-lookup"><span data-stu-id="6e4cf-127">Step 1 - Start your script</span></span>
<span data-ttu-id="6e4cf-128">Puede descargar Hola script completo de PowerShell usa [aquí](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="6e4cf-128">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="6e4cf-129">Siga los pasos de hello debajo toochange Hola script toowork en su entorno.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="6e4cf-130">Cambiar valores de hello de hello las variables siguientes basadas en el grupo de recursos existente implementado anteriormente en [requisitos previos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="6e4cf-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="6e4cf-131">Cambiar los valores de hello de hello las variables siguientes basadas en valores de hello desea toouse para la implementación de back-end.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="6e4cf-132">Paso 2: creación de los recursos necesarios para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="6e4cf-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="6e4cf-133">Deberá toocreate un nuevo servicio de nube y un almacenamiento de cuenta para los discos de datos de Hola para todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-133">You need toocreate a new cloud service and a storage account for hello data disks for all VMs.</span></span> <span data-ttu-id="6e4cf-134">También necesitará toospecify una imagen y una cuenta de administrador local para hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-134">You also need toospecify an image, and a local administrator account for hello VMs.</span></span> <span data-ttu-id="6e4cf-135">toocreate estos recursos, completar Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6e4cf-135">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="6e4cf-136">Cree un nuevo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="6e4cf-137">Cree una cuenta de Almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="6e4cf-138">Conjunto de la cuenta de almacenamiento Hola creada anteriormente como cuenta de almacenamiento actual de Hola para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-138">Set hello storage account created above as hello current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="6e4cf-139">Seleccione una imagen para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-139">Select an image for hello VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="6e4cf-140">Establecer las credenciales de cuenta de administrador local de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-140">Set hello local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="6e4cf-141">Paso 3: crear máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="6e4cf-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="6e4cf-142">Deberá toouse un bucle toocreate tal y como muchas máquinas virtuales como desee y crear Hola necesarios NIC y las máquinas virtuales en el bucle de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-142">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="6e4cf-143">Hola toocreate NIC y las máquinas virtuales, ejecute hello pasos.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-143">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="6e4cf-144">Iniciar un `for` Hola de bucle toorepeat comandos toocreate una máquina virtual y dos NIC como tantas veces como sea necesario, basados en el valor de Hola de hello `$numberOfVMs` variable.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-144">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="6e4cf-145">Crear un `VMConfig` objeto que especifica la imagen de hello, el tamaño y el conjunto de disponibilidad para VM Hola.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-145">Create a `VMConfig` object specifying hello image, size, and availability set for hello VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="6e4cf-146">Hola aprovisionar máquinas virtuales como una máquina virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-146">Provision hello VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="6e4cf-147">Establezca el valor predeterminado de hello NIC y asignar una dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-147">Set hello default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="6e4cf-148">Agregue una segunda NIC para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="6e4cf-149">Crear discos de toodata para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-149">Create toodata disks for each VM.</span></span>

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

7. <span data-ttu-id="6e4cf-150">Crear cada máquina virtual y al final Hola bucle.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-150">Create each VM, and end hello loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="6e4cf-151">Paso 4: secuencia de comandos de ejecución Hola</span><span class="sxs-lookup"><span data-stu-id="6e4cf-151">Step 4 - Run hello script</span></span>
<span data-ttu-id="6e4cf-152">Ahora que has descargado y cambiaron el script de Hola según sus necesidades, ejecución secuencia de comandos de base de datos de back-end de hello toocreate máquinas virtuales con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-152">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="6e4cf-153">Guardar el script y ejecútelo desde hello **PowerShell** símbolo del sistema, o **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-153">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="6e4cf-154">Verá Hola iniciales de salida, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-154">You will see hello initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="6e4cf-155">Rellene la información de hello necesaria en el símbolo del sistema de hello las credenciales y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-155">Fill out hello information needed in hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="6e4cf-156">se devuelve la salida de Hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="6e4cf-156">hello output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
