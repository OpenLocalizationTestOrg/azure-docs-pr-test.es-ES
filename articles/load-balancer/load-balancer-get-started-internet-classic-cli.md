---
title: "aaaCreate una conexión a Internet cargar equilibrador - CLI de Azure clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un equilibrador de carga con conexión a Internet en el modelo de implementación clásica utilizando Hola CLI de Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a><span data-ttu-id="b1cfd-103">Empezar a crear un equilibrador de carga (clásica) en hello Azure CLI de Internet</span><span class="sxs-lookup"><span data-stu-id="b1cfd-103">Get started creating an Internet facing load balancer (classic) in hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1cfd-104">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="b1cfd-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="b1cfd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1cfd-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="b1cfd-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b1cfd-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="b1cfd-107">Servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="b1cfd-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="b1cfd-108">Antes de trabajar con recursos de Azure, es importante toounderstand que Azure tiene dos modelos de implementación: Administrador de recursos de Azure y clásico.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="b1cfd-109">Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-classic-rm.md) antes de trabajar con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="b1cfd-110">Puede ver documentación de Hola de distintas herramientas, haga clic en las pestañas de hello en parte superior de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="b1cfd-111">Este artículo trata el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="b1cfd-112">También puede [Obtenga información acerca de cómo toocreate una conexión a Internet cargar equilibrador mediante Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b1cfd-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="b1cfd-113">Creación paso a paso de un equilibrador de carga orientado a Internet con la CLI</span><span class="sxs-lookup"><span data-stu-id="b1cfd-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="b1cfd-114">Esta guía muestra cómo se toocreate un equilibrador de carga de Internet basada en escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-114">This guide shows how toocreate an Internet load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="b1cfd-115">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-115">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="b1cfd-116">Ejecute hello **modo de configuración de azure** tooswitch tooclassic modo de comandos, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-116">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="b1cfd-117">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="b1cfd-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="b1cfd-118">Crear punto de conexión y conjunto de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="b1cfd-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="b1cfd-119">escenario de Hello asume hello las máquinas virtuales "web1" y "web2" se crearon.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-119">hello scenario assumes hello virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="b1cfd-120">Esta guía creará un conjunto de equilibrador de carga mediante el puerto 80 como puerto público y el puerto 80 como puerto local.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="b1cfd-121">También se configura un puerto de sondeo en el puerto 80 y equilibrador de carga con nombre hello establece "lbset".</span><span class="sxs-lookup"><span data-stu-id="b1cfd-121">A probe port is also configured on port 80 and named hello load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="b1cfd-122">Paso 1</span><span class="sxs-lookup"><span data-stu-id="b1cfd-122">Step 1</span></span>

<span data-ttu-id="b1cfd-123">Crear el primer punto de conexión de Hola y establecen a través del equilibrador de carga `azure network vm endpoint create` para la máquina virtual "web1".</span><span class="sxs-lookup"><span data-stu-id="b1cfd-123">Create hello first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="b1cfd-124">Paso 2</span><span class="sxs-lookup"><span data-stu-id="b1cfd-124">Step 2</span></span>

<span data-ttu-id="b1cfd-125">Agregue un segundo conjunto de equilibrador de carga de toohello de máquina virtual "web2".</span><span class="sxs-lookup"><span data-stu-id="b1cfd-125">Add a second virtual machine "web2" toohello load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="b1cfd-126">Paso 3</span><span class="sxs-lookup"><span data-stu-id="b1cfd-126">Step 3</span></span>

<span data-ttu-id="b1cfd-127">Compruebe la configuración de equilibrador de carga de hello utilizando `azure vm show` .</span><span class="sxs-lookup"><span data-stu-id="b1cfd-127">Verify hello load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="b1cfd-128">salida de Hello será:</span><span class="sxs-lookup"><span data-stu-id="b1cfd-128">hello output will be:</span></span>

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="b1cfd-129">Crear un punto de conexión de escritorio remoto para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b1cfd-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="b1cfd-130">Puede crear un tráfico de red de tooforward de punto de conexión de escritorio remoto desde un puerto local tooa del puerto público para una máquina virtual específica mediante `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-130">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="b1cfd-131">Quitar máquina virtual del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="b1cfd-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="b1cfd-132">Tiene el conjunto de equilibrador de carga de la máquina virtual de hello toodelete Hola extremo asociado toohello.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-132">You have toodelete hello endpoint associated toohello load balancer set from hello virtual machine.</span></span> <span data-ttu-id="b1cfd-133">Una vez que se quita el punto de conexión de hello, máquina virtual de hello no pertenece equilibrador de carga de toohello ya establecido.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-133">Once hello endpoint is removed, hello virtual machine doesn't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="b1cfd-134">Utilizando el ejemplo de Hola anterior, puede quitar extremo de hello creado para la máquina virtual "web1" del equilibrador de carga "lbset" mediante el comando hello `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="b1cfd-134">Using hello example above, you can remove hello endpoint created for virtual machine "web1" from load balancer "lbset" using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="b1cfd-135">Puede explorar más opciones toomanage puntos de conexión mediante el comando de Hola`azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="b1cfd-135">You can explore more options toomanage endpoints using hello command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1cfd-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b1cfd-136">Next steps</span></span>

[<span data-ttu-id="b1cfd-137">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="b1cfd-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="b1cfd-138">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="b1cfd-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b1cfd-139">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="b1cfd-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
