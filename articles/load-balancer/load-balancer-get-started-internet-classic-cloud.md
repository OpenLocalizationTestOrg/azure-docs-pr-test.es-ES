---
title: "equilibrador de carga de aaaCreate una conexión a Internet para los servicios de nube de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una conexión a Internet equilibrador de carga de modelo de implementación clásica para servicios en la nube"
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
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="2b412-103">Introducción a la creación de un equilibrador de carga orientado a Internet para servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="2b412-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b412-104">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="2b412-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="2b412-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b412-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="2b412-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2b412-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="2b412-107">Servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="2b412-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="2b412-108">Antes de trabajar con recursos de Azure, es importante toounderstand que Azure tiene dos modelos de implementación: Administrador de recursos de Azure y clásico.</span><span class="sxs-lookup"><span data-stu-id="2b412-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="2b412-109">Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-classic-rm.md) antes de trabajar con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b412-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="2b412-110">Puede ver documentación de Hola de distintas herramientas, haga clic en las pestañas de hello en parte superior de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="2b412-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="2b412-111">Este artículo trata el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b412-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="2b412-112">También puede [Obtenga información acerca de cómo toocreate una conexión a Internet cargar equilibrador mediante Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2b412-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="2b412-113">Servicios en la nube se configuran automáticamente con un equilibrador de carga y se pueden personalizar mediante el modelo de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b412-113">Cloud services are automatically configured with a load balancer and can be customized via hello service model.</span></span>

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a><span data-ttu-id="2b412-114">Crear un equilibrador de carga con el archivo de definición de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="2b412-114">Create a load balancer using hello service definition file</span></span>

<span data-ttu-id="2b412-115">Puede aprovechar hello Azure SDK para .NET 2.5 tooupdate su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="2b412-115">You can leverage hello Azure SDK for .NET 2.5 tooupdate your cloud service.</span></span> <span data-ttu-id="2b412-116">Configuración de punto de conexión de servicios en la nube se realiza en hello [definición del servicio](https://msdn.microsoft.com/library/azure/gg557553.aspx) archivo .csdef.</span><span class="sxs-lookup"><span data-stu-id="2b412-116">Endpoint settings for cloud services are made in hello [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="2b412-117">Hello en el ejemplo siguiente se muestra cómo se configura un archivo servicedefinition.csdef para una implementación de nube:</span><span class="sxs-lookup"><span data-stu-id="2b412-117">hello following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="2b412-118">La comprobación de fragmento de código de hello hello .csdef archivo generado por una implementación de nube, puede ver Hola extremo externo configurado toouse puertos HTTP en el puerto 10000 y 10001, 10002.</span><span class="sxs-lookup"><span data-stu-id="2b412-118">Checking hello snippet for hello .csdef file generated by a cloud deployment, you can see hello external endpoint configured toouse ports HTTP on port 10000, 10001, and 10002.</span></span>

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

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="2b412-119">Comprobación del estado de mantenimiento del equilibrador de carga para servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="2b412-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="2b412-120">Hola te mostramos un ejemplo de un sondeo de estado:</span><span class="sxs-lookup"><span data-stu-id="2b412-120">hello following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="2b412-121">Hello equilibrador de carga combina información de Hola de punto de conexión de Hola y Hola de hello sondeo toocreate una dirección URL en forma de Hola de `http://{DIP of VM}:80/Probe.aspx` que puede ser usado tooquery Hola mantenimiento del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b412-121">hello load balancer combines hello information of hello endpoint and hello information of hello probe toocreate a URL in hello form of `http://{DIP of VM}:80/Probe.aspx` that can be used tooquery hello health of hello service.</span></span>

<span data-ttu-id="2b412-122">Hello servicio detecta las comprobaciones periódicas de hello misma dirección IP.</span><span class="sxs-lookup"><span data-stu-id="2b412-122">hello service detects periodic probes from hello same IP address.</span></span> <span data-ttu-id="2b412-123">Se trata de una solicitud de sondeo de estado de hello procedentes de host de hello del nodo de Hola donde se ejecuta la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b412-123">This is hello health probe request coming from hello host of hello node where hello virtual machine is running.</span></span> <span data-ttu-id="2b412-124">servicio de Hello tiene toorespond con un código de estado HTTP 200 para tooassume de equilibrador de carga de Hola que Hola servicio es correcto.</span><span class="sxs-lookup"><span data-stu-id="2b412-124">hello service has toorespond with a HTTP 200 status code for hello load balancer tooassume that hello service is healthy.</span></span> <span data-ttu-id="2b412-125">Cualquier otro código de estado HTTP de código (por ejemplo 503) directamente toma Hola máquina virtual fuera de la rotación.</span><span class="sxs-lookup"><span data-stu-id="2b412-125">Any other HTTP status code (for example 503) directly takes hello virtual machine out of rotation.</span></span>

<span data-ttu-id="2b412-126">definición de sondeo de Hello también controla la frecuencia de Hola de sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b412-126">hello probe definition also controls hello frequency of hello probe.</span></span> <span data-ttu-id="2b412-127">En nuestro caso anterior, el equilibrador de carga de hello es sondeo extremo Hola cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="2b412-127">In our case above, hello load balancer is probing hello endpoint every 5 secs.</span></span> <span data-ttu-id="2b412-128">Si no se recibe ninguna respuesta positiva de 10 segundos (dos intervalos de sondeo), se supone que el sondeo de hello hacia abajo, y máquina virtual de Hola se realiza fuera de la rotación.</span><span class="sxs-lookup"><span data-stu-id="2b412-128">If no positive answer is received for 10 secs (two probe intervals), hello probe is assumed down, and hello virtual machine is taken out of rotation.</span></span> <span data-ttu-id="2b412-129">De forma similar, si el servicio de hello está fuera de la rotación y se recibe una respuesta positiva, servicio de Hola se vuelve a colocar toorotation inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="2b412-129">Similarly, if hello service is out of rotation and a positive answer is received, hello service is put back toorotation right away.</span></span> <span data-ttu-id="2b412-130">Si el servicio de hello fluctúa entre correcto y negativa, equilibrador de carga de hello puede decidir reintroducción hello toodelay de hello servicio back-toorotation hasta que ha sido correcto durante un número de sondeos.</span><span class="sxs-lookup"><span data-stu-id="2b412-130">If hello service is fluctuating between healthy and unhealthy, hello load balancer can decide toodelay hello re-introduction of hello service back toorotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="2b412-131">Compruebe el esquema de definición de servicio de Hola para hello [sondeo de estado](https://msdn.microsoft.com/library/azure/jj151530.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="2b412-131">Check hello service definition schema for hello [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b412-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2b412-132">Next steps</span></span>

[<span data-ttu-id="2b412-133">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="2b412-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="2b412-134">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="2b412-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="2b412-135">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="2b412-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

