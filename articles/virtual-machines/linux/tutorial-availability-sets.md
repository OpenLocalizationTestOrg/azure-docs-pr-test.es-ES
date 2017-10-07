---
title: "aaaAvailability establece el tutorial para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de hello conjuntos de disponibilidad para máquinas virtuales de Linux en Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="77bdc-103">¿Cómo se establece toouse disponibilidad</span><span class="sxs-lookup"><span data-stu-id="77bdc-103">How toouse availability sets</span></span>


<span data-ttu-id="77bdc-104">En este tutorial, obtendrá información sobre cómo la disponibilidad de hello tooincrease y la confiabilidad de las soluciones de la máquina Virtual en Azure con una capacidad de llamar conjuntos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="77bdc-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="77bdc-105">Conjuntos de disponibilidad Asegúrese de que las máquinas virtuales se implementan en Azure se distribuyen entre varios clústeres de hardware aislados de Hola.</span><span class="sxs-lookup"><span data-stu-id="77bdc-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="77bdc-106">Esto garantiza que, si se produce un error de hardware o software dentro de Azure, solo un subjuego de las máquinas virtuales se verán afectado y que la solución general permanecerá disponible y en funcionamiento desde la perspectiva de Hola de los clientes de usarlo.</span><span class="sxs-lookup"><span data-stu-id="77bdc-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span>

<span data-ttu-id="77bdc-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="77bdc-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="77bdc-108">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="77bdc-108">Create an availability set</span></span>
> * <span data-ttu-id="77bdc-109">Crear una máquina virtual en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="77bdc-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="77bdc-110">Comprobar los tamaños de máquina virtual disponibles</span><span class="sxs-lookup"><span data-stu-id="77bdc-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="77bdc-111">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="77bdc-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="77bdc-112">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="77bdc-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="77bdc-113">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="77bdc-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="77bdc-114">Información general sobre conjuntos de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="77bdc-114">Availability set overview</span></span>

<span data-ttu-id="77bdc-115">Un conjunto de disponibilidad es una capacidad de agrupación lógica que puede usar en Azure tooensure que los recursos de máquina virtual de Hola que se coloca dentro de él están aislados entre sí cuando se implementan en un centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="77bdc-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="77bdc-116">Azure garantiza que las máquinas virtuales se coloca dentro de un conjunto de disponibilidad que se ejecute en varios servidores físicos de hello, proceso racks, unidades de almacenamiento y conmutadores de red.</span><span class="sxs-lookup"><span data-stu-id="77bdc-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="77bdc-117">Esto garantiza que en caso de hello de un error hardware o software de Azure, solo un subconjunto de las máquinas virtuales se verán afectado, y la aplicación global se mantienen actualizados y continuar a toobe tooyour disponibles clientes.</span><span class="sxs-lookup"><span data-stu-id="77bdc-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="77bdc-118">Usar conjuntos de disponibilidad es una capacidad fundamental tooleverage cuando desee que las soluciones de nube confiable toobuild.</span><span class="sxs-lookup"><span data-stu-id="77bdc-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="77bdc-119">Veamos una solución basada en máquina virtual típica en la podría haber 4 servidores web front-end y usar 2 máquinas virtuales de back-end que hospedan una base de datos.</span><span class="sxs-lookup"><span data-stu-id="77bdc-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="77bdc-120">Con Azure, desearía toodefine dos conjuntos de disponibilidad antes de implementar las máquinas virtuales: conjunto de disponibilidad de uno para la capa de "web" de Hola y un conjunto de disponibilidad de nivel de "database" Hola.</span><span class="sxs-lookup"><span data-stu-id="77bdc-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="77bdc-121">Cuando se crea una nueva máquina virtual, a continuación, puede especificar el conjunto como una máquina virtual de parámetro toohello az crear comandos y Azure automáticamente asegurará de que hello las máquinas virtuales que cree en hello disponible de la disponibilidad de hello conjunto están aislados entre varios recursos de hardware físico.</span><span class="sxs-lookup"><span data-stu-id="77bdc-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="77bdc-122">Esto significa que si el hardware físico de Hola que uno de su servidor Web o máquinas virtuales del servidor de base de datos se ejecuta en tiene un problema, sabe que Hola otras instancias de servidor Web y máquinas virtuales de la base de datos seguirá ejecutándose correctamente porque están en un hardware diferente.</span><span class="sxs-lookup"><span data-stu-id="77bdc-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="77bdc-123">Debe utilizar siempre los conjuntos de disponibilidad cuando desee que las soluciones basadas en VM confiable toodeploy dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="77bdc-123">You should always use Availability Sets when you want toodeploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="77bdc-124">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="77bdc-124">Create an availability set</span></span>

<span data-ttu-id="77bdc-125">Puede crear el conjunto de disponibilidad mediante [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="77bdc-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="77bdc-126">En este ejemplo, establecemos ambos en número de dominios de actualización y error en hello *2* para el conjunto con nombre de la disponibilidad de hello *myAvailabilitySet* en hello *myResourceGroupAvailability*grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="77bdc-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="77bdc-127">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="77bdc-127">Create a resource group.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

<span data-ttu-id="77bdc-128">Conjuntos de disponibilidad permiten tooisolate recursos entre "dominios de error" y "Actualizar dominios".</span><span class="sxs-lookup"><span data-stu-id="77bdc-128">Availability Sets allow you tooisolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="77bdc-129">Un **dominio de error** representa una colección aislada de recursos de almacenamiento, red y servidor.</span><span class="sxs-lookup"><span data-stu-id="77bdc-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="77bdc-130">En el anterior ejemplo de Hola, indicamos que queremos que toobe distribuida en al menos dos dominios de error cuando se implementan máquinas virtuales de nuestro conjunto de nuestra disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="77bdc-130">In hello preceding example, we indicate that we want our availability set toobe distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="77bdc-131">También especificamos que queremos que nuestro conjunto de disponibilidad se distribuya entre dos **dominios de actualización**.</span><span class="sxs-lookup"><span data-stu-id="77bdc-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="77bdc-132">Dos dominios de actualización Asegúrese de que, cuando Azure lleva a cabo las actualizaciones de software nuestros recursos de máquina virtual estén aislados, evitar todo el software Hola ejecutando debajo de la máquina virtual desde la que se está actualizando en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="77bdc-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all hello software running underneath our VM from being updated at hello same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="77bdc-133">Configuración de una red virtual</span><span class="sxs-lookup"><span data-stu-id="77bdc-133">Configure virtual network</span></span>
<span data-ttu-id="77bdc-134">Antes de implementar algunas máquinas virtuales y puede probar su equilibrador, crear Hola compatibilidad con recursos de red virtual.</span><span class="sxs-lookup"><span data-stu-id="77bdc-134">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="77bdc-135">Para obtener más información sobre las redes virtuales, vea hello [administrar redes virtuales de Azure](tutorial-virtual-network.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="77bdc-135">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="77bdc-136">Crear recursos de red</span><span class="sxs-lookup"><span data-stu-id="77bdc-136">Create network resources</span></span>
<span data-ttu-id="77bdc-137">Cree la red virtual con el comando [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="77bdc-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="77bdc-138">Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* con una subred denominada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="77bdc-138">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="77bdc-139">Las NIC virtuales se crean con el comando [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="77bdc-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="77bdc-140">Hello en el ejemplo siguiente se crea tres NIC virtuales.</span><span class="sxs-lookup"><span data-stu-id="77bdc-140">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="77bdc-141">(Una NIC virtual para cada máquina virtual crea para la aplicación Hola siguiendo los pasos).</span><span class="sxs-lookup"><span data-stu-id="77bdc-141">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="77bdc-142">Puede crear NIC virtuales adicionales y las máquinas virtuales en cualquier momento y agregarlos toohello equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="77bdc-142">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="77bdc-143">Creación de VM dentro de un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="77bdc-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="77bdc-144">Las máquinas virtuales deben crearse dentro de hello disponibilidad conjunto toomake seguro de que se distribuyen correctamente a través de hardware de Hola.</span><span class="sxs-lookup"><span data-stu-id="77bdc-144">VMs must be created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="77bdc-145">No se puede agregar un grupo de disponibilidad de tooan VM establecer después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="77bdc-145">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="77bdc-146">Cuando se crea una máquina virtual mediante [crear vm az](/cli/azure/vm#create) especificar Hola conjunto de disponibilidad mediante hello `--availability-set` nombre del parámetro toospecify Hola Hola del conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="77bdc-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify hello availability set using hello `--availability-set` parameter toospecify hello name of hello availability set.</span></span>

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

<span data-ttu-id="77bdc-147">Ahora tenemos dos máquinas virtuales en nuestro conjunto de disponibilidad recién creado.</span><span class="sxs-lookup"><span data-stu-id="77bdc-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="77bdc-148">Hola mismo porque están en el conjunto de disponibilidad, Azure asegurará de que las máquinas virtuales de Hola y todos sus recursos (incluidos los discos de datos) se distribuyen a través de hardware físico aislado.</span><span class="sxs-lookup"><span data-stu-id="77bdc-148">Because they are in hello same availability set, Azure will ensure that hello VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="77bdc-149">Esta distribución ayuda a garantizar una mayor disponibilidad de nuestra solución de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="77bdc-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="77bdc-150">Único lo que se puede encontrar a medida que agregue las máquinas virtuales es que un determinado tamaño de máquina virtual ya no está disponible toouse dentro de su conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="77bdc-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available toouse within your availability set.</span></span> <span data-ttu-id="77bdc-151">Este problema puede suceder si ya no es suficiente tooadd capacidad conservando el conjunto de disponibilidad de hello aislamiento reglas Hola exige.</span><span class="sxs-lookup"><span data-stu-id="77bdc-151">This issue can happen if there is no longer enough capacity tooadd it while preserving hello isolation rules hello availability set enforces.</span></span> <span data-ttu-id="77bdc-152">Puede comprobar toosee qué tamaños de máquina virtual son toouse disponible dentro de un grupo de disponibilidad que se establecen a través de hello `--availability-set list-sizes` parámetro.</span><span class="sxs-lookup"><span data-stu-id="77bdc-152">You can check toosee what VM sizes are available toouse within an existing availability set using hello `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="77bdc-153">Comprobación de los tamaños de VM disponibles</span><span class="sxs-lookup"><span data-stu-id="77bdc-153">Check for available VM sizes</span></span> 

<span data-ttu-id="77bdc-154">Puede agregar más máquinas virtuales toohello conjunto de disponibilidad posteriormente, pero necesita tooknow qué tamaños de máquinas virtuales están disponibles en el hardware de Hola.</span><span class="sxs-lookup"><span data-stu-id="77bdc-154">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="77bdc-155">Use [lista-tamaños del conjunto de disponibilidad de máquinas virtuales az](/cli/azure/availability-set#list-sizes) toolist todos los tamaños disponibles de hello en hardware de Hola de clúster para el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="77bdc-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="77bdc-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="77bdc-156">Next steps</span></span>

<span data-ttu-id="77bdc-157">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="77bdc-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="77bdc-158">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="77bdc-158">Create an availability set</span></span>
> * <span data-ttu-id="77bdc-159">Crear una máquina virtual en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="77bdc-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="77bdc-160">Comprobar los tamaños de máquina virtual disponibles</span><span class="sxs-lookup"><span data-stu-id="77bdc-160">Check available VM sizes</span></span>

<span data-ttu-id="77bdc-161">Avanzar toohello toolearn de tutorial siguiente sobre conjuntos de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="77bdc-161">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="77bdc-162">Creación de un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="77bdc-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

