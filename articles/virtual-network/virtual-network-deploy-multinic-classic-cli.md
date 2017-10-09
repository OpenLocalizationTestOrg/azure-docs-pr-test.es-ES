---
title: "aaaCreate una máquina virtual (clásica) con varias NIC - 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual (clásica) con varias NIC con hello Azure interfaz de línea de comandos (CLI) 1.0."
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
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="02e6b-103">Crear una máquina virtual (clásica) con varias NIC con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="02e6b-103">Create a VM (Classic) with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="02e6b-104">Puede crear máquinas virtuales (VM) en Azure y conectar múltiples tooeach (NIC) de interfaces de red de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="02e6b-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="02e6b-105">Varias NIC permiten la separación de tipos de tráfico a través de las NIC.</span><span class="sxs-lookup"><span data-stu-id="02e6b-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="02e6b-106">Por ejemplo, una que NIC puede comunicarse con hello Internet, mientras que otra solo se comunica con los recursos internos no conectado toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="02e6b-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="02e6b-107">tráfico de red de Hello capacidad tooseparate entre varios NIC es necesario para muchos dispositivos virtuales red, por ejemplo, la entrega de aplicaciones y soluciones de optimización de la WAN.</span><span class="sxs-lookup"><span data-stu-id="02e6b-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02e6b-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="02e6b-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="02e6b-109">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="02e6b-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="02e6b-110">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="02e6b-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="02e6b-111">Obtenga información acerca de cómo tooperform estos pasos con hello [modelo de implementación del Administrador de recursos](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="02e6b-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="02e6b-112">Hello pasos siguientes utiliza un grupo de recursos denominado *IaaSStory* para servidores WEB de Hola y un grupo de recursos denominado *IaaSStory-back-end* para servidores de Hola DB.</span><span class="sxs-lookup"><span data-stu-id="02e6b-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02e6b-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="02e6b-113">Prerequisites</span></span>
<span data-ttu-id="02e6b-114">Para poder crear Hola servidores de base de datos, necesita hello toocreate *IaaSStory* grupo de recursos con todos los recursos necesarios de Hola para este escenario.</span><span class="sxs-lookup"><span data-stu-id="02e6b-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="02e6b-115">toocreate Hola a estos recursos, completados los pasos que siguen.</span><span class="sxs-lookup"><span data-stu-id="02e6b-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="02e6b-116">Crear una red virtual, siga los pasos de Hola Hola [crear una red virtual](virtual-networks-create-vnet-classic-cli.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="02e6b-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a><span data-ttu-id="02e6b-117">Hola back-end de implementar las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="02e6b-117">Deploy hello back-end VMs</span></span>
<span data-ttu-id="02e6b-118">Hola que dependen de las máquinas virtuales de back-end durante la creación de hello de hello recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="02e6b-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="02e6b-119">**Cuenta de almacenamiento en discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="02e6b-119">**Storage account for data disks**.</span></span> <span data-ttu-id="02e6b-120">Para mejorar el rendimiento, los discos de datos de hello en los servidores de base de datos de hello usará la tecnología de estado sólido (SSD) de la unidad, que requiere una cuenta de almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="02e6b-120">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="02e6b-121">Asegúrese de hello seguro implementar almacenamiento premium de toosupport de ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="02e6b-121">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="02e6b-122">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="02e6b-122">**NICs**.</span></span> <span data-ttu-id="02e6b-123">Cada VM tendrá dos NIC, una para el acceso de la base de datos y otra para la administración.</span><span class="sxs-lookup"><span data-stu-id="02e6b-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="02e6b-124">**Conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="02e6b-124">**Availability set**.</span></span> <span data-ttu-id="02e6b-125">Todos los servidores de base de datos se agregarán tooa único conjunto de disponibilidad, tooensure al menos una de las máquinas virtuales de hello está en funcionamiento durante el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="02e6b-125">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="02e6b-126">Paso 1: inicio del script</span><span class="sxs-lookup"><span data-stu-id="02e6b-126">Step 1 - Start your script</span></span>
<span data-ttu-id="02e6b-127">Puede descargar script de Hola intensiva de errores completa utilizado [aquí](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="02e6b-127">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="02e6b-128">Hola completa siguiendo los pasos toochange Hola script toowork en su entorno:</span><span class="sxs-lookup"><span data-stu-id="02e6b-128">Complete hello following steps toochange hello script toowork in your environment:</span></span>

1. <span data-ttu-id="02e6b-129">Cambiar valores de hello de hello las variables siguientes basadas en el grupo de recursos existente implementado anteriormente en [requisitos previos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="02e6b-129">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="02e6b-130">Cambiar los valores de hello de hello las variables siguientes basadas en valores de hello desea toouse para la implementación de back-end.</span><span class="sxs-lookup"><span data-stu-id="02e6b-130">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="02e6b-131">Paso 2: creación de los recursos necesarios para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="02e6b-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="02e6b-132">Cree un nuevo servicio en la nube para todas las máquinas virtuales de back-end.</span><span class="sxs-lookup"><span data-stu-id="02e6b-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="02e6b-133">Uso de Hola de aviso de hello `$backendCSName` variable nombre de grupo de recursos de hello, y `$location` para hello región de Azure.</span><span class="sxs-lookup"><span data-stu-id="02e6b-133">Notice hello use of hello `$backendCSName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="02e6b-134">Crear una cuenta de almacenamiento premium para hello SO y toobe de discos de datos utilizado por el suyo máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="02e6b-134">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="02e6b-135">Paso 3: crear máquinas virtuales con varias NIC</span><span class="sxs-lookup"><span data-stu-id="02e6b-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="02e6b-136">Iniciar un bucle toocreate varias máquinas virtuales, en función de hello `numberOfVMs` variables.</span><span class="sxs-lookup"><span data-stu-id="02e6b-136">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="02e6b-137">Para cada máquina virtual, especifique el nombre de Hola y dirección IP de cada uno de hello dos NIC.</span><span class="sxs-lookup"><span data-stu-id="02e6b-137">For each VM, specify hello name and IP address of each of hello two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="02e6b-138">Crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="02e6b-138">Create hello VM.</span></span> <span data-ttu-id="02e6b-139">Observa Hola del uso de hello `--nic-config` parámetro, que contiene una lista de todas las NIC con nombre, la subred y la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="02e6b-139">Notice hello usage of hello `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

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

4. <span data-ttu-id="02e6b-140">Cree dos discos de datos por cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="02e6b-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="02e6b-141">Paso 4: secuencia de comandos de ejecución Hola</span><span class="sxs-lookup"><span data-stu-id="02e6b-141">Step 4 - Run hello script</span></span>
<span data-ttu-id="02e6b-142">Ahora que has descargado y cambia según sus necesidades, ejecutar copia Hola Hola de toocreate de secuencia de comandos de script de Hola finalizar máquinas virtuales de la base de datos con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="02e6b-142">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="02e6b-143">Guarde el script y ejecútelo desde su terminal de **Bash** .</span><span class="sxs-lookup"><span data-stu-id="02e6b-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="02e6b-144">Verá Hola iniciales de salida, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="02e6b-144">You will see hello initial output, as shown below.</span></span>

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

2. <span data-ttu-id="02e6b-145">Después de unos minutos, finalizará la ejecución de Hola y verá que el resto de Hola de salida de hello tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="02e6b-145">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>

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
