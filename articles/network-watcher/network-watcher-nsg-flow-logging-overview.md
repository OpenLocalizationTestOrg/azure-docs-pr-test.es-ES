---
title: registro de tooflow aaaIntroduction para grupos de seguridad de red con Monitor de red de Azure | Documentos de Microsoft
description: "Esta página explica cómo el flujo NSG toouse registra una característica del Monitor de red de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a>Registro de tooflow de introducción para grupos de seguridad de red

Registros de flujo de grupo de seguridad de red son una característica del Monitor de red que permite tooview información sobre el tráfico IP de entrada y de salida a través de un grupo de seguridad de red. Estos registros de flujo se escriben en formato json y mostrar salidos y flujos de entrada en cada regla, Hola flujo Hola NIC que se aplica, tupla de 5 información acerca del flujo de hello (protocolo IP de origen/destino, puerto de origen/destino,) y si hello se permita el tráfico o denegado.

![información general de los registros de flujo][1]

Mientras el flujo de registros de grupos de seguridad de red de destino, no se muestran mismo Hola como Hola otros registros. Registros de flujo se almacenan dentro de una cuenta de almacenamiento y la siguiente ruta de acceso de registro de hello tal y como se muestra en el siguiente ejemplo de Hola:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Hola mismo tooflow registros aplican las directivas de retención, tal como se muestra en otros registros. Los registros tienen una directiva de retención que se pueden establecer en 1 día too365 días. Si no se establece una directiva de retención, Hola registros se mantienen indefinidamente.

## <a name="log-file"></a>Archivo de registro

Los registros de flujo tienen varias propiedades. Hello lista siguiente es una lista de propiedades de Hola que se devuelven en el registro de flujo de hello NSG:

* **tiempo** : tiempo cuando se registra el evento de Hola
* **systemId**: el identificador de recurso del grupo de seguridad de red
* **categoría** -categoría Hola de evento de hello, esto siempre es ser NetworkSecurityGroupFlowEvent
* **ResourceID** -Hola recursos Id. de hello NSG
* **operationName**: siempre es NetworkSecurityGroupFlowEvents
* **propiedades** -una colección de propiedades de flujo de Hola
    * **Versión** -número de versión de esquema de eventos de flujo de registro de hello
    * **flows**: una recopilación de flujos. Esta propiedad tiene varias entradas para diferentes reglas
        * **regla** -regla qué Hola se muestran cuatro flujos
            * **flows**: una recopilación de flujos
                * **Mac** -Hola dirección MAC de hello NIC para hello VM que se recopiló el flujo de Hola
                * **flowTuples** -una cadena que contiene varias propiedades de tupla de flujo de hello en un formato separado por comas
                    * **Marca de tiempo** -este valor es la marca de tiempo hello cuando se produjo el flujo de hello en formato de la ÉPOCA de UNIX
                    * **IP de origen** : hello IP de origen
                    * **Destino IP** -Hola IP de destino
                    * **Puerto de origen** : hello puerto de origen
                    * **Puerto de destino** -Hola puerto de destino
                    * **Protocolo** -Hola protocolo de flujo de Hola. Los valores válidos son **T** para TCP y **U** para UDP
                    * **Flujo del tráfico** -Hola dirección del flujo de tráfico de Hola de. Los valores válidos son **I** para el correo entrante y **O** para el saliente.
                    * **Traffic**: indica si el tráfico se permitió o se denegó. Los valores válidos son **A** para permitido y **D** para denegado.


Hola aquí te mostramos un ejemplo de un registro de flujo. Como puede ver, hay varios registros que siguen la lista de propiedades de Hola se describe en la sección anterior de Hola. 

> [!NOTE]
> Valores de propiedad de hello flowTuples son una lista separada por comas.
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo se registra tooenable flujo visitando [habilitar el flujo de registro](network-watcher-nsg-flow-logging-portal.md).

Obtenga información acerca del registro de NSG visitando [Análisis del registro para grupos de seguridad de red (NSG)](../virtual-network/virtual-network-nsg-manage-log.md).

Averigüe si se permite o no el tráfico en una máquina virtual visitando [Comprobación del tráfico con la comprobación de flujo de IP](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

