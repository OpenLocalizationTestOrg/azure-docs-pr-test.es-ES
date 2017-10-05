---
title: "Creación de una máquina virtual con varias NIC: CLI de Azure 1.0 | Microsoft Docs"
description: "Aprenda a crear una máquina virtual con varias NIC mediante la CLI de Azure 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b95bcb38664718bf25ec6981c803415790c6da3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="643a7-103">Creación de una máquina virtual con varias NIC mediante la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="643a7-103">Create a VM with multiple NICs using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="643a7-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="643a7-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="643a7-105">En este artículo se describe el uso del modelo de implementación de Resource Manager, recomendado por Microsoft para la mayoría de las nuevas implementaciones en lugar del [modelo de implementación clásica](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="643a7-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="643a7-106">En los pasos siguientes se usa un grupo de recursos denominado *IaaSStory* para los servidores web y un grupo de recursos denominado *IaaSStory-BackEnd* para los servidores de base de datos.</span><span class="sxs-lookup"><span data-stu-id="643a7-106">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span> <span data-ttu-id="643a7-107">Puede completar esta tarea mediante la CLI de Azure 1.0 (en este artículo) o la [CLI de Azure 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="643a7-107">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="643a7-108">Los valores entre "" para las variables de los pasos siguientes crean recursos con la configuración del escenario.</span><span class="sxs-lookup"><span data-stu-id="643a7-108">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span></span> <span data-ttu-id="643a7-109">Modifique los valores del modo adecuado para su entorno.</span><span class="sxs-lookup"><span data-stu-id="643a7-109">Change the values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="643a7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="643a7-110">Prerequisites</span></span>
<span data-ttu-id="643a7-111">Antes de crear los servidores de base de datos, necesita crear el grupo de recursos *IaaSStory* con todos los recursos necesarios para este escenario.</span><span class="sxs-lookup"><span data-stu-id="643a7-111">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="643a7-112">Para crear estos recursos, complete los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="643a7-112">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="643a7-113">Vaya a [la página de plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="643a7-113">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="643a7-114">En la página de la plantilla, a la derecha de **Grupo de recursos primarios**, haga clic en **Implementar en Azure**.</span><span class="sxs-lookup"><span data-stu-id="643a7-114">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="643a7-115">Si es necesario, cambie los valores de parámetro y siga los pasos en el Portal de vista previa de Azure para implementar el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="643a7-115">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="643a7-116">Asegúrese de que los nombres de cuenta de almacenamiento sean únicos.</span><span class="sxs-lookup"><span data-stu-id="643a7-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="643a7-117">No puede tener nombres de cuenta de almacenamiento duplicados en Azure.</span><span class="sxs-lookup"><span data-stu-id="643a7-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="643a7-118">Creación de las máquinas virtuales de back-end</span><span class="sxs-lookup"><span data-stu-id="643a7-118">Create the back-end VMs</span></span>
<span data-ttu-id="643a7-119">Las máquinas virtuales de back-end dependen de la creación de los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="643a7-119">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="643a7-120">**Cuenta de almacenamiento en discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="643a7-120">**Storage account for data disks**.</span></span> <span data-ttu-id="643a7-121">Para mejorar el rendimiento, los discos de datos en los servidores de base de datos usarán la tecnología de unidad de estado sólido (SSD), que requiere una cuenta de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="643a7-121">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="643a7-122">Asegúrese de que la ubicación de Azure que implementa admita el almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="643a7-122">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="643a7-123">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="643a7-123">**NICs**.</span></span> <span data-ttu-id="643a7-124">Cada VM tendrá dos NIC, una para el acceso de la base de datos y otra para la administración.</span><span class="sxs-lookup"><span data-stu-id="643a7-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="643a7-125">**Conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="643a7-125">**Availability set**.</span></span> <span data-ttu-id="643a7-126">Todos los servidores de base de datos se agregarán al conjunto de disponibilidad único para asegurarse de que al menos una de las máquinas virtuales está activa y ejecutándose durante el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="643a7-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="643a7-127">Paso 1: inicio del script</span><span class="sxs-lookup"><span data-stu-id="643a7-127">Step 1 - Start your script</span></span>
<span data-ttu-id="643a7-128">Puede descargar el script de Bash completo que haya usado [aquí](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="643a7-128">You can download the full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="643a7-129">Siga los pasos siguientes para cambiar el script para que funcione en su entorno.</span><span class="sxs-lookup"><span data-stu-id="643a7-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="643a7-130">Cambie los valores de las variables siguientes en función de su grupo de recursos existente implementado anteriormente en [Requisitos previos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="643a7-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="643a7-131">Cambie los valores de las variables siguientes según los valores que desee usar para la implementación back-end.</span><span class="sxs-lookup"><span data-stu-id="643a7-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```azurecli
    backendRGName="IaaSStory-Backend"
    prmStorageAccountName="wtestvnetstorageprm"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    publisher="Canonical"
    offer="UbuntuServer"
    sku="14.04.2-LTS"
    version="latest"
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskName="datadisk"
    nicNamePrefix="NICDB"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

3. <span data-ttu-id="643a7-132">Recupere el identificador de la subred `BackEnd` donde se crearán las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="643a7-132">Retrieve the ID for the `BackEnd` subnet where the VMs will be created.</span></span> <span data-ttu-id="643a7-133">Debe hacerlo porque las NIC que se asociarán a esta subred estarán en un grupo de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="643a7-133">You need to do this since the NICs to be associated to this subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="643a7-134">El primer comando anterior usa [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) y [manipulación de cadenas](http://tldp.org/LDP/abs/html/string-manipulation.html) (más concretamente, la eliminación de subcadenas).</span><span class="sxs-lookup"><span data-stu-id="643a7-134">The first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="643a7-135">Recupere el identificador del grupo de seguridad de red de `NSG-RemoteAccess` .</span><span class="sxs-lookup"><span data-stu-id="643a7-135">Retrieve the ID for the `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="643a7-136">Debe hacerlo porque las NIC que se asociarán a este grupo de seguridad de red estarán en un grupo de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="643a7-136">You need to do this since the NICs to be associated to this NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="643a7-137">Paso 2: creación de los recursos necesarios para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="643a7-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="643a7-138">Cree un nuevo grupo de recursos para todos los recursos back-end.</span><span class="sxs-lookup"><span data-stu-id="643a7-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="643a7-139">Observe el uso de la variable `$backendRGName` para el nombre del grupo de recursos, y `$location` para la región de Azure.</span><span class="sxs-lookup"><span data-stu-id="643a7-139">Notice the use of the `$backendRGName` variable for the resource group name, and `$location` for the Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="643a7-140">Cree una cuenta de almacenamiento Premium para los discos de datos y sistemas operativos que usarán sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="643a7-140">Create a premium storage account for the OS and data disks to be used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="643a7-141">Cree un conjunto de disponibilidad para las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="643a7-141">Create an availability set for the VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-the-nics-and-back-end-vms"></a><span data-ttu-id="643a7-142">Paso 3: Creación de las NIC y máquinas virtuales de back-end</span><span class="sxs-lookup"><span data-stu-id="643a7-142">Step 3 - Create the NICs and back-end VMs</span></span>

1. <span data-ttu-id="643a7-143">Inicie un bucle para crear varias máquinas virtuales, según las variables `numberOfVMs` .</span><span class="sxs-lookup"><span data-stu-id="643a7-143">Start a loop to create multiple VMs, based on the `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="643a7-144">Para cada máquina virtual, cree una NIC para el acceso a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="643a7-144">For each VM, create a NIC for database access.</span></span>

    ```azurecli
    nic1Name=$nicNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x
    azure network nic create --name $nic1Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress1 \
        --subnet-id $subnetId
    ```

3. <span data-ttu-id="643a7-145">Para cada máquina virtual, cree una NIC para el acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="643a7-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="643a7-146">Observe el parámetro `--network-security-group` que se usa para asociar la NIC a un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="643a7-146">Notice the `--network-security-group` parameter, used to associate the NIC to an NSG.</span></span>

    ```azurecli
    nic2Name=$nicNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    azure network nic create --name $nic2Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress2 \
        --subnet-id $subnetId $vnetName \
        --network-security-group-id $nsgId
    ```

4. <span data-ttu-id="643a7-147">Cree la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="643a7-147">Create the VM.</span></span>

    ```azurecli
    azure vm create --resource-group $backendRGName \
        --name $vmNamePrefix$suffixNumber \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --availset-name $avSetName \
        --nic-names $nic1Name,$nic2Name \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName$suffixNumber.vhd \
        --admin-username $username \
        --admin-password $password
    ```

5. <span data-ttu-id="643a7-148">Para cada máquina virtual, cree dos discos de datos y finalice el bucle con el comando `done` .</span><span class="sxs-lookup"><span data-stu-id="643a7-148">For each VM, create two data disks, and end the loop with the `done` command.</span></span>

    ```azurecli
    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-1.vhd \
        --size-in-gb $diskSize \
        --lun 0

    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \        
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-2.vhd \
        --size-in-gb $diskSize \
        --lun 1
        done
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="643a7-149">Paso 4: ejecución del script</span><span class="sxs-lookup"><span data-stu-id="643a7-149">Step 4 - Run the script</span></span>
<span data-ttu-id="643a7-150">Ahora que descargó y cambió el script según sus necesidades, ejecute el script para crear las máquinas virtuales de la base de datos back-end con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="643a7-150">Now that you downloaded and changed the script based on your needs, run the script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="643a7-151">Guarde el script y ejecútelo desde su terminal de **Bash** .</span><span class="sxs-lookup"><span data-stu-id="643a7-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="643a7-152">Verá el resultado inicial, tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="643a7-152">You will see the initial output, as shown below.</span></span>
   
        info:    Executing command group create
        info:    Getting resource group IaaSStory-Backend
        info:    Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command availset create
        info:    Looking up the availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up the network interface "NICDB1-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-DA
        data:    Name                            : NICDB1-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up the network interface "NICDB1-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-RA
        data:    Name                            : NICDB1-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.54
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up the VM "DB1"
        info:    Using the VM Size "Standard_DS3"
        info:    The [OS, Data] Disk or image configuration requires storage account
        info:    Looking up the storage account wtestvnetstorageprm
        info:    Looking up the availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up the NIC "NICDB1-DA"
        info:    Looking up the NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="643a7-153">Después de unos minutos, la ejecución finalizará y verá el resto del resultado como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="643a7-153">After a few minutes, the execution will end and you will see the rest of the output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB1"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB1"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up the network interface "NICDB2-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-DA
        data:    Name                            : NICDB2-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.5
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up the network interface "NICDB2-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-RA
        data:    Name                            : NICDB2-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.55
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up the VM "DB2"
        info:    Using the VM Size "Standard_DS3"
        info:    The [OS, Data] Disk or image configuration requires storage account
        info:    Looking up the storage account wtestvnetstorageprm
        info:    Looking up the availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up the NIC "NICDB2-DA"
        info:    Looking up the NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB2"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB2"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

