---
title: "aaaCreate una máquina virtual con varias NIC - 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con varias NIC con Hola 1.0 de CLI de Azure."
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
ms.openlocfilehash: 07c660b632bcdc004365a6f910ecf8a5c13cbc6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="c611a-103">Crear una máquina virtual con varias NIC con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c611a-103">Create a VM with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c611a-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c611a-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c611a-105">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c611a-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="c611a-106">Hello pasos siguientes utiliza un grupo de recursos denominado *IaaSStory* para servidores WEB de Hola y un grupo de recursos denominado *IaaSStory-back-end* para servidores de Hola DB.</span><span class="sxs-lookup"><span data-stu-id="c611a-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span> <span data-ttu-id="c611a-107">Puede completar esta tarea mediante hello Azure CLI 1.0 (en este artículo) o hello [CLI de Azure 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c611a-107">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="c611a-108">Hola valores en "" para recursos de creación de variables de hello en los pasos de Hola que sigan con la configuración del escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="c611a-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="c611a-109">Cambiar los valores de hello, según corresponda para su entorno.</span><span class="sxs-lookup"><span data-stu-id="c611a-109">Change hello values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c611a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c611a-110">Prerequisites</span></span>
<span data-ttu-id="c611a-111">Para poder crear Hola servidores de base de datos, necesita hello toocreate *IaaSStory* grupo de recursos con todos los recursos necesarios de Hola para este escenario.</span><span class="sxs-lookup"><span data-stu-id="c611a-111">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="c611a-112">toocreate estos recursos, completar Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c611a-112">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="c611a-113">Navegue demasiado[página de la plantilla de hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="c611a-113">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="c611a-114">En página de la plantilla de hello, toohello derecha de **grupo de recursos primario**, haga clic en **implementar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="c611a-114">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="c611a-115">Si es necesario, cambiar los valores de parámetro de hello, a continuación, siga los pasos de hello en grupo de recursos de hello vista previa de Azure portal toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="c611a-115">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c611a-116">Asegúrese de que los nombres de cuenta de almacenamiento sean únicos.</span><span class="sxs-lookup"><span data-stu-id="c611a-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="c611a-117">No puede tener nombres de cuenta de almacenamiento duplicados en Azure.</span><span class="sxs-lookup"><span data-stu-id="c611a-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="c611a-118">Crear máquinas virtuales de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="c611a-118">Create hello back-end VMs</span></span>
<span data-ttu-id="c611a-119">Hola que dependen de las máquinas virtuales de back-end durante la creación de hello de hello recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c611a-119">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="c611a-120">**Cuenta de almacenamiento en discos de datos**.</span><span class="sxs-lookup"><span data-stu-id="c611a-120">**Storage account for data disks**.</span></span> <span data-ttu-id="c611a-121">Para mejorar el rendimiento, los discos de datos de hello en los servidores de base de datos de hello usará la tecnología de estado sólido (SSD) de la unidad, que requiere una cuenta de almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="c611a-121">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="c611a-122">Asegúrese de hello seguro implementar almacenamiento premium de toosupport de ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="c611a-122">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="c611a-123">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="c611a-123">**NICs**.</span></span> <span data-ttu-id="c611a-124">Cada VM tendrá dos NIC, una para el acceso de la base de datos y otra para la administración.</span><span class="sxs-lookup"><span data-stu-id="c611a-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="c611a-125">**Conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="c611a-125">**Availability set**.</span></span> <span data-ttu-id="c611a-126">Todos los servidores de base de datos se agregarán tooa único conjunto de disponibilidad, tooensure al menos una de las máquinas virtuales de hello está en funcionamiento durante el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="c611a-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="c611a-127">Paso 1: inicio del script</span><span class="sxs-lookup"><span data-stu-id="c611a-127">Step 1 - Start your script</span></span>
<span data-ttu-id="c611a-128">Puede descargar script de Hola intensiva de errores completa utilizado [aquí](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="c611a-128">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="c611a-129">Siga los pasos de hello debajo toochange Hola script toowork en su entorno.</span><span class="sxs-lookup"><span data-stu-id="c611a-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="c611a-130">Cambiar valores de hello de hello las variables siguientes basadas en el grupo de recursos existente implementado anteriormente en [requisitos previos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="c611a-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="c611a-131">Cambiar los valores de hello de hello las variables siguientes basadas en valores de hello desea toouse para la implementación de back-end.</span><span class="sxs-lookup"><span data-stu-id="c611a-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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

3. <span data-ttu-id="c611a-132">Recuperar el Id. de Hola Hola `BackEnd` subred donde se creará hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c611a-132">Retrieve hello ID for hello `BackEnd` subnet where hello VMs will be created.</span></span> <span data-ttu-id="c611a-133">Lo necesita toodo puesto Hola NIC toobe asociado toothis subred están en otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c611a-133">You need toodo this since hello NICs toobe associated toothis subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="c611a-134">Hola primer comando anterior se usa [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) y [manipulación de cadenas](http://tldp.org/LDP/abs/html/string-manipulation.html) (más concretamente, la eliminación de subcadena).</span><span class="sxs-lookup"><span data-stu-id="c611a-134">hello first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="c611a-135">Recuperar el Id. de Hola Hola `NSG-RemoteAccess` NSG.</span><span class="sxs-lookup"><span data-stu-id="c611a-135">Retrieve hello ID for hello `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="c611a-136">Lo necesita toodo desde hello toobe NIC asociadas toothis NSG están en otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c611a-136">You need toodo this since hello NICs toobe associated toothis NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="c611a-137">Paso 2: creación de los recursos necesarios para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c611a-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="c611a-138">Cree un nuevo grupo de recursos para todos los recursos back-end.</span><span class="sxs-lookup"><span data-stu-id="c611a-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="c611a-139">Uso de Hola de aviso de hello `$backendRGName` variable nombre de grupo de recursos de hello, y `$location` para hello región de Azure.</span><span class="sxs-lookup"><span data-stu-id="c611a-139">Notice hello use of hello `$backendRGName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="c611a-140">Crear una cuenta de almacenamiento premium para hello SO y toobe de discos de datos utilizado por el suyo máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c611a-140">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="c611a-141">Crear un conjunto de disponibilidad para hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c611a-141">Create an availability set for hello VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="c611a-142">Paso 3: crear Hola NIC y las máquinas virtuales de back-end</span><span class="sxs-lookup"><span data-stu-id="c611a-142">Step 3 - Create hello NICs and back-end VMs</span></span>

1. <span data-ttu-id="c611a-143">Iniciar un bucle toocreate varias máquinas virtuales, en función de hello `numberOfVMs` variables.</span><span class="sxs-lookup"><span data-stu-id="c611a-143">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="c611a-144">Para cada máquina virtual, cree una NIC para el acceso a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="c611a-144">For each VM, create a NIC for database access.</span></span>

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

3. <span data-ttu-id="c611a-145">Para cada máquina virtual, cree una NIC para el acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="c611a-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="c611a-146">Hola aviso `--network-security-group` parámetro, tooassociate usado Hola NIC tooan NSG.</span><span class="sxs-lookup"><span data-stu-id="c611a-146">Notice hello `--network-security-group` parameter, used tooassociate hello NIC tooan NSG.</span></span>

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

4. <span data-ttu-id="c611a-147">Crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c611a-147">Create hello VM.</span></span>

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

5. <span data-ttu-id="c611a-148">Para cada máquina virtual, cree los discos de datos de dos y al final Hola bucle con hello `done` comando.</span><span class="sxs-lookup"><span data-stu-id="c611a-148">For each VM, create two data disks, and end hello loop with hello `done` command.</span></span>

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

### <a name="step-4---run-hello-script"></a><span data-ttu-id="c611a-149">Paso 4: secuencia de comandos de ejecución Hola</span><span class="sxs-lookup"><span data-stu-id="c611a-149">Step 4 - Run hello script</span></span>
<span data-ttu-id="c611a-150">Ahora que has descargado y cambia según sus necesidades, ejecutar copia Hola Hola de toocreate de secuencia de comandos de script de Hola finalizar máquinas virtuales de la base de datos con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="c611a-150">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="c611a-151">Guarde el script y ejecútelo desde su terminal de **Bash** .</span><span class="sxs-lookup"><span data-stu-id="c611a-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="c611a-152">Verá Hola iniciales de salida, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="c611a-152">You will see hello initial output, as shown below.</span></span>
   
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
        info:    Looking up hello availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up hello network interface "NICDB1-DA"
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
        info:    Looking up hello network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up hello network interface "NICDB1-RA"
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
        info:    Looking up hello VM "DB1"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB1-DA"
        info:    Looking up hello NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="c611a-153">Después de unos minutos, finalizará la ejecución de Hola y verá que el resto de Hola de salida de hello tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="c611a-153">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up hello network interface "NICDB2-DA"
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
        info:    Looking up hello network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up hello network interface "NICDB2-RA"
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
        info:    Looking up hello VM "DB2"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB2-DA"
        info:    Looking up hello NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

