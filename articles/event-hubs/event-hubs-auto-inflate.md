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
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a>Escalado vertical y automático de las unidades de procesamiento de Azure Event Hubs

## <a name="overview"></a>Información general

Azure Event Hubs es una plataforma de streaming de datos muy escalable. Por lo tanto, los clientes de los centros de eventos a menudo mejora su uso después de la incorporación toohello servicio. Dichos aumentos requieren creciente Hola predeterminado rendimiento unidades (sus) tooscale centros de eventos y asimilar velocidades de transferencia más grandes. Hola *aumentar automáticamente* característica de centros de eventos se escala automáticamente el número de Hola de sus necesidades de uso de toomeet. Al aumentar las TU, se evitan escenarios de limitación en los que nos encontramos con:

* Velocidades de entrada de datos que superan las TU establecidas
* Velocidades de solicitud de salida de datos que superan las TU establecidas

## <a name="how-auto-inflate-works"></a>Funcionamiento del inflado automático

El tráfico de Event Hubs lo controlan las unidades de procesamiento. Una sola TU permite una entrada de 1 MB/s y una salida que duplica esas cifras. Event Hubs estándar se puede configurar con un número de unidades de procesamiento del 1 a 20. Aumentar automática permite toostart poco a poco con unidades de rendimiento necesarios mínimo Hola. característica Hello, a continuación, amplía automáticamente toohello límite máximo de unidades de rendimiento que necesite, función hello aumento en el tráfico. Aumentar automáticamente proporciona Hola siguientes ventajas:

- Una eficaz toostart mecanismo escala pequeña y ampliación vertical como crecer.
- Escalar automáticamente toohello de límite superior especificado sin problemas de limitación.
- Más control sobre el escalado, como controlar cuándo y cuánto tooscale.

## <a name="enable-auto-inflate-on-a-namespace"></a>Habilitación del inflado automático en un espacio de nombres

Puede habilitar o deshabilitar aumentar automáticamente en un espacio de nombres utilizando cualquiera de los siguientes métodos de hello:

1. Hola [portal de Azure](https://portal.azure.com).
2. Una plantilla de Azure Resource Manager

### <a name="enable-auto-inflate-through-hello-portal"></a>Habilitar aumentar automáticamente a través del portal de Hola

Puede habilitar características de hello aumentar automáticamente en un espacio de nombres al crear un espacio de nombres de los centros de eventos:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

Con esta opción habilitada, puede empezar poco a poco con las unidades de procesamiento y escalarlas verticalmente a medida que sus necesidades de uso sean más exigentes. Hello límite superior para inflación no afecta a precios, que depende de número de Hola de sus utilizado por hora.

También puede habilitar aumentar automáticamente mediante hello **escala** opción en la hoja de configuración de hello en el portal de hello:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a>Habilitación del inflado automático mediante una plantilla de Azure Resource Manager

Puede habilitar el inflado automático durante la implementación de una plantilla de Azure Resource Manager. Por ejemplo, un conjunto de hello `isAutoInflateEnabled` propiedad demasiado**true** y establecer `maximumThroughputUnits` too10.

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

Para la plantilla completa de hello, vea hello [espacio de nombres de los centros de eventos de crear y habilitar aumentar](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) plantilla en GitHub.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Información general de Event Hubs](event-hubs-what-is-event-hubs.md)
* [Creación de un centro de eventos](event-hubs-create.md)
