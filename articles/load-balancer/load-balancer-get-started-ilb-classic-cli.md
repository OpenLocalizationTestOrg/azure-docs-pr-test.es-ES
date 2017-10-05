---
title: "Creación de un equilibrador de carga interno: CLI de Azure clásica | Microsoft Docs"
description: "Información sobre cómo crear un equilibrador de carga interno mediante la CLI de Azure en el modelo de implementación clásica"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d24b95f75b5ffd1116b07cf9f8bac33767a9c835
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-the-azure-cli"></a><span data-ttu-id="a6cb6-103">Primeros pasos en la creación de un equilibrador de carga interno (clásico) mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a6cb6-103">Get started creating an internal load balancer (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6cb6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6cb6-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="a6cb6-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a6cb6-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="a6cb6-106">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a6cb6-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="a6cb6-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a6cb6-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a6cb6-108">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="a6cb6-109">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="a6cb6-110">Obtenga información sobre cómo [realizar estos pasos con el modelo de Resource Manager](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a6cb6-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="to-create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="a6cb6-111">Para crear un equilibrador de carga interno establecido para máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a6cb6-111">To create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="a6cb6-112">Para crear un conjunto con equilibrio de carga interno y los servidores que enviarán su tráfico a él, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6cb6-112">To create an internal load balancer set and the servers that will send their traffic to it, you must do the following:</span></span>

1. <span data-ttu-id="a6cb6-113">Crea una instancia de Equilibrio de carga interno que será el extremo del tráfico entrante que su carga se va a equilibrar entre los servidores de un conjunto con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="a6cb6-114">Agregue extremos correspondientes a las máquinas virtuales que van a recibir el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="a6cb6-115">Configura los servidores que van a enviar el tráfico cuya carga se va a equilibrar para que lo hagan a la dirección IP virtual (VIP) de la instancia de Equilibrio de carga interno.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="a6cb6-116">Creación paso a paso de un equilibrador de carga interno mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="a6cb6-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="a6cb6-117">Esta guía muestra cómo crear un equilibrador de carga interno basado en el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-117">This guide shows how to create an internal load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="a6cb6-118">Si nunca ha usado la CLI de Azure, consulte [Instalación y configuración de la CLI de Azure](../cli-install-nodejs.md) y siga las instrucciones hasta el punto donde deba seleccionar su cuenta y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-118">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a6cb6-119">Ejecute el comando **azure config mode** para cambiar al modo clásico, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-119">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="a6cb6-120">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="a6cb6-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="a6cb6-121">Crear punto de conexión y conjunto de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="a6cb6-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="a6cb6-122">En el escenario se supone la presencia de las máquinas virtuales "DB1" y "DB2" en un servicio en la nube denominado "mytestcloud".</span><span class="sxs-lookup"><span data-stu-id="a6cb6-122">The scenario assumes the virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="a6cb6-123">Ambas máquinas virtuales usan una red virtual denominada mi "testvnet" con la subred "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="a6cb6-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="a6cb6-124">Esta guía creará un conjunto de equilibrador de carga interno mediante el puerto 1433 como puerto privado y 1433 como puerto local.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="a6cb6-125">Se trata de un escenario común donde hay máquinas virtuales de SQL en el back-end que usan un equilibrador de carga interno para garantizar que los servidores de base de datos no se exponen directamente mediante una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-125">This is a common scenario where you have SQL virtual machines on the back end using an internal load balancer to guarantee the database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="a6cb6-126">Paso 1</span><span class="sxs-lookup"><span data-stu-id="a6cb6-126">Step 1</span></span>

<span data-ttu-id="a6cb6-127">Crear un conjunto de equilibrador de carga interno mediante `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="a6cb6-128">Para obtener más información, consulte `azure service internal-load-balancer --help` .</span><span class="sxs-lookup"><span data-stu-id="a6cb6-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="a6cb6-129">Puede comprobar las propiedades del equilibrador de carga interno mediante el comando `azure service internal-load-balancer list` *nombre de servicio en la nube*.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-129">You can check the internal load balancer properties using the command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="a6cb6-130">A continuación se sigue un ejemplo de la salida:</span><span class="sxs-lookup"><span data-stu-id="a6cb6-130">Here follows an example of the output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="a6cb6-131">Paso 2</span><span class="sxs-lookup"><span data-stu-id="a6cb6-131">Step 2</span></span>

<span data-ttu-id="a6cb6-132">Configurar el conjunto del equilibrador de carga interno al agregar el primer punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-132">You configure the internal load balancer set when you add the first endpoint.</span></span> <span data-ttu-id="a6cb6-133">En este paso se asociará el punto de conexión, la máquina virtual y el puerto de sondeo al conjunto del equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-133">You will associate the endpoint, virtual machine and probe port to the internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="a6cb6-134">Paso 3</span><span class="sxs-lookup"><span data-stu-id="a6cb6-134">Step 3</span></span>

<span data-ttu-id="a6cb6-135">Comprobar la configuración del equilibrador de carga mediante el `azure vm show` *nombre de la máquina virtual*</span><span class="sxs-lookup"><span data-stu-id="a6cb6-135">Verify the load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="a6cb6-136">El resultado será:</span><span class="sxs-lookup"><span data-stu-id="a6cb6-136">The output will be:</span></span>

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="a6cb6-137">Crear un punto de conexión de escritorio remoto para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a6cb6-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="a6cb6-138">Puede crear un punto de conexión de escritorio remoto para reenviar el tráfico de red desde un puerto público a un puerto local para una máquina virtual específica mediante `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-138">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="a6cb6-139">Quitar máquina virtual del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="a6cb6-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="a6cb6-140">Puede quitar una máquina virtual de un equilibrador de carga interno establecido eliminando el punto de conexión asociado.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-140">You can remove a virtual machine from an internal load balancer set by deleting the associated endpoint.</span></span> <span data-ttu-id="a6cb6-141">Una vez eliminado el punto de conexión, la máquina virtual deja de pertenecer al conjunto de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-141">Once the endpoint is removed, the virtual machine won't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="a6cb6-142">En el ejemplo anterior, puede quitar el punto de conexión creado para la máquina virtual "DB1" del equilibrador de carga interno "ilbset" mediante el comando `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="a6cb6-142">Using the example above, you can remove the endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="a6cb6-143">Para obtener más información, consulte `azure vm endpoint --help` .</span><span class="sxs-lookup"><span data-stu-id="a6cb6-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6cb6-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a6cb6-144">Next steps</span></span>

[<span data-ttu-id="a6cb6-145">Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen</span><span class="sxs-lookup"><span data-stu-id="a6cb6-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a6cb6-146">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="a6cb6-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
