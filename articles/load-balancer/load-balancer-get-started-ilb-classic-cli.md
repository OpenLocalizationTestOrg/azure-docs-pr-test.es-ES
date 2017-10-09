---
title: "aaaCreate un interno cargar equilibrador - CLI de Azure clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un equilibrador de carga interno utilizando Hola CLI de Azure en el modelo de implementación clásica de Hola"
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
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a><span data-ttu-id="02152-103">Empezar a crear un equilibrador de carga interno (clásico) mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="02152-103">Get started creating an internal load balancer (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="02152-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02152-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="02152-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="02152-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="02152-106">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="02152-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="02152-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="02152-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="02152-108">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="02152-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="02152-109">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="02152-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="02152-110">Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="02152-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="02152-111">toocreate un equilibrador de carga interno establecido para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="02152-111">toocreate an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="02152-112">toocreate un equilibrador de carga interno establecido y Hola servidores que enviarán su tráfico tooit, debe hacer los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="02152-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you must do hello following:</span></span>

1. <span data-ttu-id="02152-113">Cree una instancia de interno equilibrio de carga que será el punto de conexión de Hola de carga de toobe tráfico entrante están equilibrada en los servidores de Hola de un conjunto con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="02152-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="02152-114">Agregue extremos correspondientes máquinas virtuales de toohello que va a recibir el tráfico entrante Hola.</span><span class="sxs-lookup"><span data-stu-id="02152-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="02152-115">Configure los servidores de Hola que van a enviar equilibrio de carga de hello tráfico toobe toosend su tráfico toohello dirección IP virtual (VIP) de instancia de equilibrio de carga interno de Hola.</span><span class="sxs-lookup"><span data-stu-id="02152-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="02152-116">Creación paso a paso de un equilibrador de carga interno mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="02152-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="02152-117">Esta guía muestra cómo se toocreate un equilibrador de carga interno basada en escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="02152-117">This guide shows how toocreate an internal load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="02152-118">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="02152-118">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="02152-119">Ejecute hello **modo de configuración de azure** tooswitch tooclassic modo de comandos, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="02152-119">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="02152-120">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="02152-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="02152-121">Crear punto de conexión y conjunto de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="02152-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="02152-122">escenario de Hello supone Hola máquinas "DB1" y "DB2" en un servicio de nube denominado "mytestcloud".</span><span class="sxs-lookup"><span data-stu-id="02152-122">hello scenario assumes hello virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="02152-123">Ambas máquinas virtuales usan una red virtual denominada mi "testvnet" con la subred "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="02152-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="02152-124">Esta guía creará un conjunto de equilibrador de carga interno mediante el puerto 1433 como puerto privado y 1433 como puerto local.</span><span class="sxs-lookup"><span data-stu-id="02152-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="02152-125">Se trata de un escenario común donde haya máquinas virtuales de SQL sobre el uso de back-end de hello que no se expondrá un servidores de bases de datos de carga interno equilibrador tooguarantee Hola directamente mediante una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="02152-125">This is a common scenario where you have SQL virtual machines on hello back end using an internal load balancer tooguarantee hello database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="02152-126">Paso 1</span><span class="sxs-lookup"><span data-stu-id="02152-126">Step 1</span></span>

<span data-ttu-id="02152-127">Crear un conjunto de equilibrador de carga interno mediante `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="02152-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="02152-128">Para obtener más información, consulte `azure service internal-load-balancer --help` .</span><span class="sxs-lookup"><span data-stu-id="02152-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="02152-129">Puede comprobar las propiedades de equilibrador de carga interno de hello mediante comandos de hello `azure service internal-load-balancer list` *nombre de servicio de nube*.</span><span class="sxs-lookup"><span data-stu-id="02152-129">You can check hello internal load balancer properties using hello command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="02152-130">Sigue aquí un ejemplo de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="02152-130">Here follows an example of hello output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="02152-131">Paso 2</span><span class="sxs-lookup"><span data-stu-id="02152-131">Step 2</span></span>

<span data-ttu-id="02152-132">Configure el equilibrador de carga interno de hello establecido cuando se agrega el primer punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="02152-132">You configure hello internal load balancer set when you add hello first endpoint.</span></span> <span data-ttu-id="02152-133">Se asociará Hola extremo, la máquina virtual y sondeo puerto toohello equilibrador de carga interno establecido en este paso.</span><span class="sxs-lookup"><span data-stu-id="02152-133">You will associate hello endpoint, virtual machine and probe port toohello internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="02152-134">Paso 3</span><span class="sxs-lookup"><span data-stu-id="02152-134">Step 3</span></span>

<span data-ttu-id="02152-135">Compruebe la configuración de equilibrador de carga de hello con `azure vm show` *nombre de máquina virtual*</span><span class="sxs-lookup"><span data-stu-id="02152-135">Verify hello load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="02152-136">salida de Hello será:</span><span class="sxs-lookup"><span data-stu-id="02152-136">hello output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="02152-137">Crear un punto de conexión de escritorio remoto para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="02152-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="02152-138">Puede crear un tráfico de red de tooforward de punto de conexión de escritorio remoto desde un puerto local tooa del puerto público para una máquina virtual específica mediante `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="02152-138">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="02152-139">Quitar máquina virtual del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="02152-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="02152-140">Puede quitar una máquina virtual de un equilibrador de carga interno establecido mediante la eliminación de punto de conexión de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="02152-140">You can remove a virtual machine from an internal load balancer set by deleting hello associated endpoint.</span></span> <span data-ttu-id="02152-141">Una vez que se quita el punto de conexión de hello, máquina virtual de hello no pertenecen equilibrador de carga de toohello ya establecido.</span><span class="sxs-lookup"><span data-stu-id="02152-141">Once hello endpoint is removed, hello virtual machine won't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="02152-142">Utilizando el ejemplo de Hola anterior, puede quitar extremo de hello creado para la máquina virtual "DB1" de equilibrador de carga interno "ilbset" mediante el comando de hello `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="02152-142">Using hello example above, you can remove hello endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="02152-143">Para obtener más información, consulte `azure vm endpoint --help` .</span><span class="sxs-lookup"><span data-stu-id="02152-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02152-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="02152-144">Next steps</span></span>

[<span data-ttu-id="02152-145">Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen</span><span class="sxs-lookup"><span data-stu-id="02152-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="02152-146">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="02152-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
