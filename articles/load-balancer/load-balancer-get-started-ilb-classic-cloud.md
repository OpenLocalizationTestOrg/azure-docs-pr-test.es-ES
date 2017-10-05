---
title: "Creación de un equilibrador de carga interno para Azure Cloud Services | Microsoft Docs"
description: "Información sobre cómo crear un equilibrador de carga interno mediante PowerShell con el modelo de implementación clásica"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 8dbc951416d577fa7f534c2eab1605c6bee61fce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="a0471-103">Introducción a la creación de un equilibrador de carga interno (clásico) para servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="a0471-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0471-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0471-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="a0471-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a0471-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="a0471-106">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a0471-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="a0471-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a0471-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a0471-108">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="a0471-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="a0471-109">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a0471-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="a0471-110">Obtenga información sobre cómo [realizar estos pasos con el modelo de Resource Manager](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a0471-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="a0471-111">Configuración del equilibrador de carga interno para los servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="a0471-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="a0471-112">El equilibrador de carga interno es compatible tanto con las máquinas virtuales como con los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="a0471-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="a0471-113">Un punto de conexión del equilibrador de carga interno creado en un servicio en la nube que está fuera de una red virtual regional solo será accesible dentro del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="a0471-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within the cloud service.</span></span>

<span data-ttu-id="a0471-114">La configuración del equilibrador de carga interno se debe establecer durante la creación de la primera implementación en el servicio en la nube, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="a0471-114">The internal load balancer configuration has to be set during the creation of the first deployment in the cloud service, as shown in the sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0471-115">Un requisito previo para ejecutar los pasos siguientes es tener ya creada una red virtual para la implementación en la nube.</span><span class="sxs-lookup"><span data-stu-id="a0471-115">A prerequisite to run the steps below is to have a virtual network already created for the cloud deployment.</span></span> <span data-ttu-id="a0471-116">Necesitarás el nombre de red virtual y el nombre de la subred para crear el Equilibrio de carga interno.</span><span class="sxs-lookup"><span data-stu-id="a0471-116">You will need the virtual network name and subnet name to create the Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="a0471-117">Paso 1</span><span class="sxs-lookup"><span data-stu-id="a0471-117">Step 1</span></span>

<span data-ttu-id="a0471-118">Abre el archivo de configuración de servicio (.cscfg) para la implementación en la nube en Visual Studio y agrega la siguiente sección para crear el Equilibrio de carga interno en el último elemento «`</Role>`» para la configuración de red.</span><span class="sxs-lookup"><span data-stu-id="a0471-118">Open the service configuration file (.cscfg) for your cloud deployment in Visual Studio and add the following section to create the Internal Load Balancing under the last "`</Role>`" item for the network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of the load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="a0471-119">Vamos a agregar los valores para que el archivo de configuración de red muestre su aspecto.</span><span class="sxs-lookup"><span data-stu-id="a0471-119">Let's add the values for the network configuration file to show how it will look.</span></span> <span data-ttu-id="a0471-120">En el ejemplo, supongamos que creó una red virtual denominada "test_vnet" con una subred 10.0.0.0/24 denominada test_subnet y la dirección IP estática 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="a0471-120">In the example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="a0471-121">El equilibrador de carga se denominará testLB.</span><span class="sxs-lookup"><span data-stu-id="a0471-121">The load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="a0471-122">Para obtener más información sobre el esquema del equilibrador de carga, consulta [Agregar equilibrador de carga](https://msdn.microsoft.com/library/azure/dn722411.aspx)</span><span class="sxs-lookup"><span data-stu-id="a0471-122">For more information about the load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="a0471-123">Paso 2</span><span class="sxs-lookup"><span data-stu-id="a0471-123">Step 2</span></span>

<span data-ttu-id="a0471-124">Cambia los archivos de definición (.csdef) para agregar extremos al Equilibrio de carga interno.</span><span class="sxs-lookup"><span data-stu-id="a0471-124">Change the service definition (.csdef) file to add endpoints to the Internal Load Balancing.</span></span> <span data-ttu-id="a0471-125">Cuando se crea una instancia de rol, el archivo de definición de servicio agregará las instancias de rol al Equilibrio de carga interno.</span><span class="sxs-lookup"><span data-stu-id="a0471-125">The moment a role instance is created, the service definition file will add the role instances to the Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="a0471-126">Vamos a agregar los valores del archivo de definición de servicio siguiendo los mismos valores del ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="a0471-126">Following the same values from the example above, let's add the values to the service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="a0471-127">La carga del tráfico de red se equilibrará mediante el equilibrador de carga testLB, en el que se usa el puerto 80 para las solicitudes entrantes y se envía a instancias de rol de trabajo también en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="a0471-127">The network traffic will be load balanced using the testLB load balancer using port 80 for incoming requests, sending to worker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0471-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a0471-128">Next steps</span></span>

[<span data-ttu-id="a0471-129">Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen</span><span class="sxs-lookup"><span data-stu-id="a0471-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a0471-130">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="a0471-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

