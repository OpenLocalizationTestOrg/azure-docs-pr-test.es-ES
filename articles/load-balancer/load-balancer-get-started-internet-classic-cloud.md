---
title: "Creación de un equilibrador de carga con conexión a Internet para Azure Cloud Services | Microsoft Docs"
description: "Obtenga información acerca de cómo crear un equilibrador de carga orientado a Internet en el modelo de implementación clásica para servicios en la nube"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 1ceaafebcaebecb04314c7da62c69b2e9b5ba39a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="d01d6-103">Introducción a la creación de un equilibrador de carga orientado a Internet para servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="d01d6-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d01d6-104">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="d01d6-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="d01d6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d01d6-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="d01d6-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d01d6-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="d01d6-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="d01d6-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="d01d6-108">Antes de trabajar con recursos de Azure, es importante comprender que Azure tiene actualmente dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="d01d6-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="d01d6-109">Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-classic-rm.md) antes de trabajar con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d01d6-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="d01d6-110">Puede ver la documentación de las distintas herramientas haciendo clic en las fichas en la parte superior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="d01d6-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="d01d6-111">Este artículo trata sobre el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="d01d6-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="d01d6-112">También puede [obtener información sobre cómo crear un equilibrador de carga orientado a Internet con el Administrador de recursos de Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d01d6-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="d01d6-113">Los servicios en la nube se configuran automáticamente con un equilibrador de carga y se pueden personalizar mediante el modelo de servicio.</span><span class="sxs-lookup"><span data-stu-id="d01d6-113">Cloud services are automatically configured with a load balancer and can be customized via the service model.</span></span>

## <a name="create-a-load-balancer-using-the-service-definition-file"></a><span data-ttu-id="d01d6-114">Crear un equilibrador de carga mediante el archivo de definición de servicio</span><span class="sxs-lookup"><span data-stu-id="d01d6-114">Create a load balancer using the service definition file</span></span>

<span data-ttu-id="d01d6-115">Puede aprovechar el SDK de Azure para .NET 2.5 para actualizar el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="d01d6-115">You can leverage the Azure SDK for .NET 2.5 to update your cloud service.</span></span> <span data-ttu-id="d01d6-116">La configuración de puntos de conexión para los servicios en la nube se realiza en el archivo .csdef de [definición de servicio](https://msdn.microsoft.com/library/azure/gg557553.aspx).</span><span class="sxs-lookup"><span data-stu-id="d01d6-116">Endpoint settings for cloud services are made in the [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="d01d6-117">En el ejemplo siguiente se muestra cómo se configura un archivo servicedefinition.csdef para una implementación en la nube:</span><span class="sxs-lookup"><span data-stu-id="d01d6-117">The following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="d01d6-118">Si comprueba el fragmento de código para el archivo .csdef generado por una implementación en la nube, verá el punto de conexión externo configurado para usar puertos HTTP en los puertos 10000, 10001 y 10002.</span><span class="sxs-lookup"><span data-stu-id="d01d6-118">Checking the snippet for the .csdef file generated by a cloud deployment, you can see the external endpoint configured to use ports HTTP on port 10000, 10001, and 10002.</span></span>

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="d01d6-119">Comprobación del estado de mantenimiento del equilibrador de carga para servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="d01d6-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="d01d6-120">A continuación se muestra un sondeo de estado:</span><span class="sxs-lookup"><span data-stu-id="d01d6-120">The following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="d01d6-121">El equilibrador de carga combina la información del punto de conexión y la información del sondeo para crear una dirección URL con el formato `http://{DIP of VM}:80/Probe.aspx` que se puede usar para consultar el estado del servicio.</span><span class="sxs-lookup"><span data-stu-id="d01d6-121">The load balancer combines the information of the endpoint and the information of the probe to create a URL in the form of `http://{DIP of VM}:80/Probe.aspx` that can be used to query the health of the service.</span></span>

<span data-ttu-id="d01d6-122">El servicio detecta sondeos periódicos desde la misma dirección IP.</span><span class="sxs-lookup"><span data-stu-id="d01d6-122">The service detects periodic probes from the same IP address.</span></span> <span data-ttu-id="d01d6-123">Se trata de la solicitud de sondeo de estado procedente del host del nodo donde se ejecuta la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d01d6-123">This is the health probe request coming from the host of the node where the virtual machine is running.</span></span> <span data-ttu-id="d01d6-124">El servicio debe responder con un código de estado HTTP 200 para que el equilibrador de carga asuma que el estado del servicio es correcto.</span><span class="sxs-lookup"><span data-stu-id="d01d6-124">The service has to respond with a HTTP 200 status code for the load balancer to assume that the service is healthy.</span></span> <span data-ttu-id="d01d6-125">Cualquier otro código de estado HTTP (por ejemplo, el 503) extrae directamente la máquina virtual de la rotación.</span><span class="sxs-lookup"><span data-stu-id="d01d6-125">Any other HTTP status code (for example 503) directly takes the virtual machine out of rotation.</span></span>

<span data-ttu-id="d01d6-126">La definición de sondeo también controla la frecuencia del sondeo.</span><span class="sxs-lookup"><span data-stu-id="d01d6-126">The probe definition also controls the frequency of the probe.</span></span> <span data-ttu-id="d01d6-127">En nuestro caso anterior, el equilibrador de carga está sondeando el extremo de cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="d01d6-127">In our case above, the load balancer is probing the endpoint every 5 secs.</span></span> <span data-ttu-id="d01d6-128">Si no se recibe una respuesta positiva durante 10 segundos (dos intervalos de sondeo), se supone que el sondeo es negativo y la máquina virtual se excluye de la rotación.</span><span class="sxs-lookup"><span data-stu-id="d01d6-128">If no positive answer is received for 10 secs (two probe intervals), the probe is assumed down, and the virtual machine is taken out of rotation.</span></span> <span data-ttu-id="d01d6-129">De forma similar, si el servicio está fuera de la rotación y se recibe una respuesta positiva, el servicio se pone de nuevo en rotación de forma inmediata.</span><span class="sxs-lookup"><span data-stu-id="d01d6-129">Similarly, if the service is out of rotation and a positive answer is received, the service is put back to rotation right away.</span></span> <span data-ttu-id="d01d6-130">Si el servicio fluctúa entre correcto e incorrecto, el equilibrador de carga puede decidir retrasar la reintroducción del servicio a rotación hasta que ha sido correcto durante un número de sondeos.</span><span class="sxs-lookup"><span data-stu-id="d01d6-130">If the service is fluctuating between healthy and unhealthy, the load balancer can decide to delay the re-introduction of the service back to rotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="d01d6-131">Compruebe el esquema de definición del [sondeo de estado](https://msdn.microsoft.com/library/azure/jj151530.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="d01d6-131">Check the service definition schema for the [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d01d6-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d01d6-132">Next steps</span></span>

[<span data-ttu-id="d01d6-133">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="d01d6-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="d01d6-134">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d01d6-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d01d6-135">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d01d6-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

