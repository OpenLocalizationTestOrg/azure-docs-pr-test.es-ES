---
title: "Creación de una máquina virtual (clásica) con varias NIC: CLI de Azure 1.0 | Microsoft Docs"
description: "Aprenda a crear una máquina virtual (clásica) con varias NIC mediante la interfaz de la línea de comandos (CLI) de Azure 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b62421b7289650818748d0016dccfdf42ef0a768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="af32a-103">Creación de una máquina virtual (clásica) con varias NIC mediante la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="af32a-103">Create a VM (Classic) with multiple NICs using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="af32a-104">Puede crear máquinas virtuales (VM) en Azure y asociar varias interfaces de red (NIC) a cada una de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="af32a-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="af32a-105">Varias NIC permiten la separación de tipos de tráfico a través de las NIC.</span><span class="sxs-lookup"><span data-stu-id="af32a-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="af32a-106">Por ejemplo, una NIC podría comunicarse con Internet, mientras que la otra solo se comunica con los recursos internos no conectados a Internet.</span><span class="sxs-lookup"><span data-stu-id="af32a-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="af32a-107">La capacidad de separar el tráfico de red a través de varias NIC es necesaria para muchos dispositivos virtuales de red, como la entrega de aplicaciones y soluciones para la optimización de WAN.</span><span class="sxs-lookup"><span data-stu-id="af32a-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af32a-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="af32a-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="af32a-109">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="af32a-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="af32a-110">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="af32a-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="af32a-111">Obtenga información sobre cómo realizar estos pasos con el [modelo de implementación de Resource Manager](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="af32a-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="af32a-112">En los pasos siguientes se usa un grupo de recursos denominado *IaaSStory* para los servidores web y un grupo de recursos denominado *IaaSStory-BackEnd* para los servidores de base de datos.</span><span class="sxs-lookup"><span data-stu-id="af32a-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af32a-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="af32a-113">Prerequisites</span></span>
<span data-ttu-id="af32a-114">Antes de crear los servidores de base de datos, necesita crear el grupo de recursos *IaaSStory* con todos los recursos necesarios para este escenario.</span><span class="sxs-lookup"><span data-stu-id="af32a-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="af32a-115">Para crear estos recursos, complete los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="af32a-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="af32a-116">Cree una red virtual siguiendo los pasos del artículo [Creación de una red virtual](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="af32a-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-the-back-end-vms"></a><span data-ttu-id="af32a-117">Implementación de las máquinas virtuales de back-end</span><span class="sxs-lookup"><span data-stu-id="af32a-117">Deploy the back-end VMs</span></span>
<span data-ttu-id="af32a-118">Las máquinas virtuales de back-end dependen de la creación de los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="af32a-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="af32a-119">**Cuenta de almacenamiento en discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="af32a-119">**Storage account for data disks**.</span></span> <span data-ttu-id="af32a-120">Para mejorar el rendimiento, los discos de datos en los servidores de base de datos usarán la tecnología de unidad de estado sólido (SSD), que requiere una cuenta de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="af32a-120">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="af32a-121">Asegúrese de que la ubicación de Azure que implementa admita el almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="af32a-121">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="af32a-122">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="af32a-122">**NICs**.</span></span> <span data-ttu-id="af32a-123">Cada VM tendrá dos NIC, una para el acceso de la base de datos y otra para la administración.</span><span class="sxs-lookup"><span data-stu-id="af32a-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="af32a-124">**Conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="af32a-124">**Availability set**.</span></span> <span data-ttu-id="af32a-125">Todos los servidores de base de datos se agregarán al conjunto de disponibilidad único para asegurarse de que al menos una de las máquinas virtuales está activa y ejecutándose durante el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="af32a-125">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="af32a-126">Paso 1: inicio del script</span><span class="sxs-lookup"><span data-stu-id="af32a-126">Step 1 - Start your script</span></span>
<span data-ttu-id="af32a-127">Puede descargar el script de Bash completo que haya usado [aquí](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="af32a-127">You can download the full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="af32a-128">Complete los pasos siguientes para cambiar el script de forma que funcione en su entorno:</span><span class="sxs-lookup"><span data-stu-id="af32a-128">Complete the following steps to change the script to work in your environment:</span></span>

1. <span data-ttu-id="af32a-129">Cambie los valores de las variables siguientes en función de su grupo de recursos existente implementado anteriormente en [Requisitos previos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="af32a-129">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="af32a-130">Cambie los valores de las variables siguientes según los valores que desee usar para la implementación back-end.</span><span class="sxs-lookup"><span data-stu-id="af32a-130">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="af32a-131">Paso 2: creación de los recursos necesarios para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="af32a-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="af32a-132">Cree un nuevo servicio en la nube para todas las máquinas virtuales de back-end.</span><span class="sxs-lookup"><span data-stu-id="af32a-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="af32a-133">Observe cómo se usa la variable `$backendCSName` para el nombre del grupo de recursos, y `$location` para la región de Azure.</span><span class="sxs-lookup"><span data-stu-id="af32a-133">Notice the use of the `$backendCSName` variable for the resource group name, and `$location` for the Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="af32a-134">Cree una cuenta de almacenamiento Premium para los discos de datos y sistemas operativos que usarán sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="af32a-134">Create a premium storage account for the OS and data disks to be used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="af32a-135">Paso 3: crear máquinas virtuales con varias NIC</span><span class="sxs-lookup"><span data-stu-id="af32a-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="af32a-136">Inicie un bucle para crear varias máquinas virtuales, según las variables `numberOfVMs` .</span><span class="sxs-lookup"><span data-stu-id="af32a-136">Start a loop to create multiple VMs, based on the `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="af32a-137">Para cada máquina virtual, especifique el nombre y la dirección IP de cada una de las dos NIC.</span><span class="sxs-lookup"><span data-stu-id="af32a-137">For each VM, specify the name and IP address of each of the two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="af32a-138">Cree la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af32a-138">Create the VM.</span></span> <span data-ttu-id="af32a-139">Tenga en cuenta que deberá usar el parámetro `--nic-config` , el cual contiene una lista de todas las NIC con nombre, subred y dirección IP.</span><span class="sxs-lookup"><span data-stu-id="af32a-139">Notice the usage of the `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. <span data-ttu-id="af32a-140">Cree dos discos de datos por cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af32a-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="af32a-141">Paso 4: ejecución del script</span><span class="sxs-lookup"><span data-stu-id="af32a-141">Step 4 - Run the script</span></span>
<span data-ttu-id="af32a-142">Ahora que descargó y cambió el script según sus necesidades, ejecute el script para crear las máquinas virtuales de la base de datos back-end con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="af32a-142">Now that you downloaded and changed the script based on your needs, run the script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="af32a-143">Guarde el script y ejecútelo desde su terminal de **Bash** .</span><span class="sxs-lookup"><span data-stu-id="af32a-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="af32a-144">Verá el resultado inicial, tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="af32a-144">You will see the initial output, as shown below.</span></span>

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. <span data-ttu-id="af32a-145">Después de unos minutos, la ejecución finalizará y verá el resto del resultado como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="af32a-145">After a few minutes, the execution will end and you will see the rest of the output as shown below.</span></span>

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
