---
title: aaaCreate un equilibrador de carga interno para servicios de nube de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un interno cargar equilibrador de usar PowerShell en el modelo de implementación clásica de Hola"
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
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="9c613-103">Introducción a la creación de un equilibrador de carga interno (clásico) para servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="9c613-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c613-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c613-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="9c613-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9c613-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="9c613-106">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="9c613-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="9c613-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9c613-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="9c613-108">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c613-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="9c613-109">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c613-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="9c613-110">Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9c613-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="9c613-111">Configuración del equilibrador de carga interno para los servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="9c613-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="9c613-112">El equilibrador de carga interno es compatible tanto con las máquinas virtuales como con los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="9c613-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="9c613-113">Un punto de conexión del equilibrador de carga interno creado en un servicio de nube que está fuera de una red virtual regional será accesible únicamente dentro de servicio en la nube Hola.</span><span class="sxs-lookup"><span data-stu-id="9c613-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within hello cloud service.</span></span>

<span data-ttu-id="9c613-114">configuración de equilibrador de carga interno de Hello tiene toobe estableció durante la creación de hello de primera implementación de Hola Hola del servicio en nube, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c613-114">hello internal load balancer configuration has toobe set during hello creation of hello first deployment in hello cloud service, as shown in hello sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c613-115">Un requisito previo toorun Hola estos pasos es una red virtual ya creada para la implementación de nube de hello toohave.</span><span class="sxs-lookup"><span data-stu-id="9c613-115">A prerequisite toorun hello steps below is toohave a virtual network already created for hello cloud deployment.</span></span> <span data-ttu-id="9c613-116">Necesitará Hola red virtual nombre y la subred nombre toocreate Hola equilibrio de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9c613-116">You will need hello virtual network name and subnet name toocreate hello Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="9c613-117">Paso 1</span><span class="sxs-lookup"><span data-stu-id="9c613-117">Step 1</span></span>

<span data-ttu-id="9c613-118">Abra el archivo de configuración de servicio de hello (.cscfg) para la implementación de nube en Visual Studio y agregue Hola después Hola de toocreate sección Equilibrio de carga interno en hello última "`</Role>`" elemento de configuración de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c613-118">Open hello service configuration file (.cscfg) for your cloud deployment in Visual Studio and add hello following section toocreate hello Internal Load Balancing under hello last "`</Role>`" item for hello network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="9c613-119">Vamos a agregar valores de hello para el archivo de configuración de hello red tooshow aspecto que tendrá.</span><span class="sxs-lookup"><span data-stu-id="9c613-119">Let's add hello values for hello network configuration file tooshow how it will look.</span></span> <span data-ttu-id="9c613-120">En el ejemplo de Hola, suponga que crea una red virtual denominada "test_vnet" con una subred 10.0.0.0/24 denominados test_subnet y una dirección IP estática 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="9c613-120">In hello example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="9c613-121">equilibrador de carga de Hola se denominará PruebaCL.</span><span class="sxs-lookup"><span data-stu-id="9c613-121">hello load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="9c613-122">Para obtener más información acerca del esquema de equilibrador de carga de hello, consulte [agregar equilibrador de carga](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c613-122">For more information about hello load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="9c613-123">Paso 2</span><span class="sxs-lookup"><span data-stu-id="9c613-123">Step 2</span></span>

<span data-ttu-id="9c613-124">Cambiar los puntos de conexión Hola servicio (.csdef) de la definición archivo tooadd toohello equilibrio de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9c613-124">Change hello service definition (.csdef) file tooadd endpoints toohello Internal Load Balancing.</span></span> <span data-ttu-id="9c613-125">momento de Hola que se crea una instancia de rol, archivo de definición de servicio de hello agregará toohello de instancias de rol Hola equilibrio de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9c613-125">hello moment a role instance is created, hello service definition file will add hello role instances toohello Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="9c613-126">Después de hello mismo los valores de ejemplo de Hola anterior, vamos a agregar archivo de definición de servicio de hello valores toohello.</span><span class="sxs-lookup"><span data-stu-id="9c613-126">Following hello same values from hello example above, let's add hello values toohello service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="9c613-127">tráfico de red de Hello será carga equilibrada con el equilibrador de carga de hello PruebaCL utilizando el puerto 80 para las solicitudes entrantes, enviar tooworker instancias de rol también en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="9c613-127">hello network traffic will be load balanced using hello testLB load balancer using port 80 for incoming requests, sending tooworker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c613-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c613-128">Next steps</span></span>

[<span data-ttu-id="9c613-129">Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen</span><span class="sxs-lookup"><span data-stu-id="9c613-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="9c613-130">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="9c613-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

