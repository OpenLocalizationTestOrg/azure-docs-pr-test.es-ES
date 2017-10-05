---
title: "Escalado vertical y automático de las unidades de procesamiento de Azure Event Hubs | Microsoft Docs"
description: "Habilite el inflado automático en un espacio de nombres para escalar verticalmente y de gorma automática unidades de procesamiento."
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: b085091ea7bfd601efb0eee84144ddd091422d6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="8851a-103">Escalado vertical y automático de las unidades de procesamiento de Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8851a-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="8851a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8851a-104">Overview</span></span>

<span data-ttu-id="8851a-105">Azure Event Hubs es una plataforma de streaming de datos muy escalable.</span><span class="sxs-lookup"><span data-stu-id="8851a-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="8851a-106">Por lo tanto, los clientes de Event Hubs suelen aumentar su uso después de adoptar el servicio.</span><span class="sxs-lookup"><span data-stu-id="8851a-106">As such, Event Hubs customers often increase their usage after onboarding to the service.</span></span> <span data-ttu-id="8851a-107">Para ello, hay que incrementar las unidades de rendimiento predeterminadas (TU) con el objetivo de escalar Event Hubs y controlar velocidades de transferencia más elevadas.</span><span class="sxs-lookup"><span data-stu-id="8851a-107">Such increases require increasing the predetermined throughput units (TUs) to scale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="8851a-108">La característica de *inflado automático* de Event Hubs escala verticalmente y de forma automática el número de TU para responder a las necesidades de uso.</span><span class="sxs-lookup"><span data-stu-id="8851a-108">The *Auto-inflate* feature of Event Hubs automatically scales up the number of TUs to meet usage needs.</span></span> <span data-ttu-id="8851a-109">Al aumentar las TU, se evitan escenarios de limitación en los que nos encontramos con:</span><span class="sxs-lookup"><span data-stu-id="8851a-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="8851a-110">Velocidades de entrada de datos que superan las TU establecidas</span><span class="sxs-lookup"><span data-stu-id="8851a-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="8851a-111">Velocidades de solicitud de salida de datos que superan las TU establecidas</span><span class="sxs-lookup"><span data-stu-id="8851a-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="8851a-112">Funcionamiento del inflado automático</span><span class="sxs-lookup"><span data-stu-id="8851a-112">How Auto-inflate works</span></span>

<span data-ttu-id="8851a-113">El tráfico de Event Hubs lo controlan las unidades de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="8851a-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="8851a-114">Una sola TU permite una entrada de 1 MB/s y una salida que duplica esas cifras.</span><span class="sxs-lookup"><span data-stu-id="8851a-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="8851a-115">Event Hubs estándar se puede configurar con un número de unidades de procesamiento del 1 a 20.</span><span class="sxs-lookup"><span data-stu-id="8851a-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="8851a-116">El inflado automático permite empezar poco a poco con las unidades de procesamiento mínimas que se requieran.</span><span class="sxs-lookup"><span data-stu-id="8851a-116">Auto-inflate enables you to start small with the minimum required throughput units.</span></span> <span data-ttu-id="8851a-117">Después, la característica escala automáticamente la cantidad hasta el límite máximo de unidades de procesamiento que necesite, según el aumento del tráfico.</span><span class="sxs-lookup"><span data-stu-id="8851a-117">The feature then scales automatically to the maximum limit of throughput units you need, depending on the increase in your traffic.</span></span> <span data-ttu-id="8851a-118">El inflado automático proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8851a-118">Auto-inflate provides the following benefits:</span></span>

- <span data-ttu-id="8851a-119">Un mecanismo de escalado eficaz para empezar poco a poco y escalar verticalmente a medida que aumente el tráfico.</span><span class="sxs-lookup"><span data-stu-id="8851a-119">An efficient scaling mechanism to start small and scale up as you grow.</span></span>
- <span data-ttu-id="8851a-120">Escalado automático hasta el límite superior especificado sin problemas de limitación.</span><span class="sxs-lookup"><span data-stu-id="8851a-120">Automatically scale to the specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="8851a-121">Más control sobre el escalado, ya que se puede controlar el momento y la cantidad que se escala.</span><span class="sxs-lookup"><span data-stu-id="8851a-121">More control over scaling, as you control when and how much to scale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="8851a-122">Habilitación del inflado automático en un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="8851a-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="8851a-123">Puede habilitar o deshabilitar aumentar el inflado automático en un espacio de nombres utilizando cualquiera de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8851a-123">You can enable or disable Auto-inflate on a namespace using either of the following methods:</span></span>

1. <span data-ttu-id="8851a-124">[Azure Portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="8851a-124">The [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8851a-125">Una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8851a-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-the-portal"></a><span data-ttu-id="8851a-126">Habilitación del inflado automático mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8851a-126">Enable Auto-inflate through the portal</span></span>

<span data-ttu-id="8851a-127">Puede habilitar la característica de inflado automático en un espacio de nombres al crear un espacio de nombres de Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="8851a-127">You can enable the Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="8851a-128">Con esta opción habilitada, puede empezar poco a poco con las unidades de procesamiento y escalarlas verticalmente a medida que sus necesidades de uso sean más exigentes.</span><span class="sxs-lookup"><span data-stu-id="8851a-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="8851a-129">El límite superior del inflado no afecta al precio, que depende del número de TU utilizado por hora.</span><span class="sxs-lookup"><span data-stu-id="8851a-129">The upper limit for inflation does not affect pricing, which depends on the number of TUs used per hour.</span></span>

<span data-ttu-id="8851a-130">También puede habilitar el inflado automático mediante la opción **Escalar** de la hoja de configuración del portal:</span><span class="sxs-lookup"><span data-stu-id="8851a-130">You can also enable Auto-inflate using the **Scale** option on the settings blade in the portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="8851a-131">Habilitación del inflado automático mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8851a-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="8851a-132">Puede habilitar el inflado automático durante la implementación de una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8851a-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="8851a-133">Por ejemplo, establezca la propiedad `isAutoInflateEnabled` en **True**, y `maximumThroughputUnits` en 10.</span><span class="sxs-lookup"><span data-stu-id="8851a-133">For example, set the `isAutoInflateEnabled` property to **true** and set `maximumThroughputUnits` to 10.</span></span>

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

<span data-ttu-id="8851a-134">Para ver la plantilla completa, consulte la plantilla [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) (Creación de un espacio de nombres de Event Hubs y habilitación del inflado) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="8851a-134">For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8851a-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8851a-135">Next steps</span></span>

<span data-ttu-id="8851a-136">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8851a-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="8851a-137">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8851a-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="8851a-138">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="8851a-138">Create an Event Hub</span></span>](event-hubs-create.md)
