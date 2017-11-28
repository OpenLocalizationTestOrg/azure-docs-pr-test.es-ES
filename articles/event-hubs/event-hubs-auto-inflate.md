---
title: escala de aaaAutomatically unidades de rendimiento de los centros de eventos de Azure | Documentos de Microsoft
description: "Habilitar aumentar automáticamente en un espacio de nombres tooautomatically de escalado vertical unidades de rendimiento"
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
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="ede25-103">Escalado vertical y automático de las unidades de procesamiento de Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ede25-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="ede25-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ede25-104">Overview</span></span>

<span data-ttu-id="ede25-105">Azure Event Hubs es una plataforma de streaming de datos muy escalable.</span><span class="sxs-lookup"><span data-stu-id="ede25-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="ede25-106">Por lo tanto, los clientes de los centros de eventos a menudo mejora su uso después de la incorporación toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="ede25-106">As such, Event Hubs customers often increase their usage after onboarding toohello service.</span></span> <span data-ttu-id="ede25-107">Dichos aumentos requieren creciente Hola predeterminado rendimiento unidades (sus) tooscale centros de eventos y asimilar velocidades de transferencia más grandes.</span><span class="sxs-lookup"><span data-stu-id="ede25-107">Such increases require increasing hello predetermined throughput units (TUs) tooscale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="ede25-108">Hola *aumentar automáticamente* característica de centros de eventos se escala automáticamente el número de Hola de sus necesidades de uso de toomeet.</span><span class="sxs-lookup"><span data-stu-id="ede25-108">hello *Auto-inflate* feature of Event Hubs automatically scales up hello number of TUs toomeet usage needs.</span></span> <span data-ttu-id="ede25-109">Al aumentar las TU, se evitan escenarios de limitación en los que nos encontramos con:</span><span class="sxs-lookup"><span data-stu-id="ede25-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="ede25-110">Velocidades de entrada de datos que superan las TU establecidas</span><span class="sxs-lookup"><span data-stu-id="ede25-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="ede25-111">Velocidades de solicitud de salida de datos que superan las TU establecidas</span><span class="sxs-lookup"><span data-stu-id="ede25-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="ede25-112">Funcionamiento del inflado automático</span><span class="sxs-lookup"><span data-stu-id="ede25-112">How Auto-inflate works</span></span>

<span data-ttu-id="ede25-113">El tráfico de Event Hubs lo controlan las unidades de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="ede25-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="ede25-114">Una sola TU permite una entrada de 1 MB/s y una salida que duplica esas cifras.</span><span class="sxs-lookup"><span data-stu-id="ede25-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="ede25-115">Event Hubs estándar se puede configurar con un número de unidades de procesamiento del 1 a 20.</span><span class="sxs-lookup"><span data-stu-id="ede25-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="ede25-116">Aumentar automática permite toostart poco a poco con unidades de rendimiento necesarios mínimo Hola.</span><span class="sxs-lookup"><span data-stu-id="ede25-116">Auto-inflate enables you toostart small with hello minimum required throughput units.</span></span> <span data-ttu-id="ede25-117">característica Hello, a continuación, amplía automáticamente toohello límite máximo de unidades de rendimiento que necesite, función hello aumento en el tráfico.</span><span class="sxs-lookup"><span data-stu-id="ede25-117">hello feature then scales automatically toohello maximum limit of throughput units you need, depending on hello increase in your traffic.</span></span> <span data-ttu-id="ede25-118">Aumentar automáticamente proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ede25-118">Auto-inflate provides hello following benefits:</span></span>

- <span data-ttu-id="ede25-119">Una eficaz toostart mecanismo escala pequeña y ampliación vertical como crecer.</span><span class="sxs-lookup"><span data-stu-id="ede25-119">An efficient scaling mechanism toostart small and scale up as you grow.</span></span>
- <span data-ttu-id="ede25-120">Escalar automáticamente toohello de límite superior especificado sin problemas de limitación.</span><span class="sxs-lookup"><span data-stu-id="ede25-120">Automatically scale toohello specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="ede25-121">Más control sobre el escalado, como controlar cuándo y cuánto tooscale.</span><span class="sxs-lookup"><span data-stu-id="ede25-121">More control over scaling, as you control when and how much tooscale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="ede25-122">Habilitación del inflado automático en un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="ede25-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="ede25-123">Puede habilitar o deshabilitar aumentar automáticamente en un espacio de nombres utilizando cualquiera de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="ede25-123">You can enable or disable Auto-inflate on a namespace using either of hello following methods:</span></span>

1. <span data-ttu-id="ede25-124">Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ede25-124">hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ede25-125">Una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ede25-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-hello-portal"></a><span data-ttu-id="ede25-126">Habilitar aumentar automáticamente a través del portal de Hola</span><span class="sxs-lookup"><span data-stu-id="ede25-126">Enable Auto-inflate through hello portal</span></span>

<span data-ttu-id="ede25-127">Puede habilitar características de hello aumentar automáticamente en un espacio de nombres al crear un espacio de nombres de los centros de eventos:</span><span class="sxs-lookup"><span data-stu-id="ede25-127">You can enable hello Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="ede25-128">Con esta opción habilitada, puede empezar poco a poco con las unidades de procesamiento y escalarlas verticalmente a medida que sus necesidades de uso sean más exigentes.</span><span class="sxs-lookup"><span data-stu-id="ede25-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="ede25-129">Hello límite superior para inflación no afecta a precios, que depende de número de Hola de sus utilizado por hora.</span><span class="sxs-lookup"><span data-stu-id="ede25-129">hello upper limit for inflation does not affect pricing, which depends on hello number of TUs used per hour.</span></span>

<span data-ttu-id="ede25-130">También puede habilitar aumentar automáticamente mediante hello **escala** opción en la hoja de configuración de hello en el portal de hello:</span><span class="sxs-lookup"><span data-stu-id="ede25-130">You can also enable Auto-inflate using hello **Scale** option on hello settings blade in hello portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="ede25-131">Habilitación del inflado automático mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ede25-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="ede25-132">Puede habilitar el inflado automático durante la implementación de una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ede25-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="ede25-133">Por ejemplo, un conjunto de hello `isAutoInflateEnabled` propiedad demasiado**true** y establecer `maximumThroughputUnits` too10.</span><span class="sxs-lookup"><span data-stu-id="ede25-133">For example, set hello `isAutoInflateEnabled` property too**true** and set `maximumThroughputUnits` too10.</span></span>

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

<span data-ttu-id="ede25-134">Para la plantilla completa de hello, vea hello [espacio de nombres de los centros de eventos de crear y habilitar aumentar](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) plantilla en GitHub.</span><span class="sxs-lookup"><span data-stu-id="ede25-134">For hello complete template, see hello [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ede25-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ede25-135">Next steps</span></span>

<span data-ttu-id="ede25-136">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="ede25-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="ede25-137">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ede25-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ede25-138">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="ede25-138">Create an Event Hub</span></span>](event-hubs-create.md)
