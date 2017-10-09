---
title: "comprobación de tooconnectivity aaaIntroduction en Monitor de red de Azure | Documentos de Microsoft"
description: "Esta página proporciona una visión general de hello capacidad de conectividad de Monitor de red"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a>Comprobación de tooconnectivity de introducción en el Monitor de red de Azure

Hello conectividad característica de Monitor de red proporciona Hola capacidad toocheck una conexión TCP directa de una máquina virtual tooa máquina virtual (VM), el nombre de dominio completo (FQDN), URI, o la dirección IPv4. Los escenarios de red son complejos, se implementan mediante grupos de seguridad de red, firewalls, rutas definidas por el usuario y recursos proporcionados por Azure. Las configuraciones complejas dificultan la solución de problemas de conectividad. Monitor de red ayuda a reducir la cantidad de Hola de toofind de tiempo y detectar problemas de conectividad. resultados de Hello devueltos pueden proporcionar información sobre si es un problema de conectividad de vencimiento tooa plataforma o un problema de configuración de usuario. La conectividad se puede comprobar con [PowerShell](network-watcher-connectivity-powershell.md), la [CLI de Azure](network-watcher-connectivity-cli.md) y la [API de REST](network-watcher-connectivity-rest.md).

> [!IMPORTANT]
> La comprobación de conectividad requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`. Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="response"></a>Response

Hello en la tabla siguiente muestra las propiedades de hello devueltos cuando una comprobación de conectividad ha terminado de ejecutarse.

|Propiedad  |Descripción  |
|---------|---------|
|ConnectionStatus     | estado de Hola de comprobación de conectividad de Hola. Los resultados posibles son **Reachable** y **Unreachable**.        |
|AvgLatencyInMs     | Promedio de latencia durante la comprobación de conectividad de hello en milisegundos. (Solo se muestra si el estado de la comprobación es accesible).        |
|MinLatencyInMs     | Comprobación de latencia mínima durante la conectividad de hello en milisegundos. (Solo se muestra si el estado de la comprobación es accesible).        |
|MaxLatencyInMs     | Comprobación de la latencia máxima durante la conectividad de hello en milisegundos. (Solo se muestra si el estado de la comprobación es accesible).        |
|ProbesSent     | Número de sondeos que se envía durante la comprobación de Hola. El valor máximo es 100.        |
|ProbesFailed     | Número de sondeos que dieron error durante la comprobación de Hola. El valor máximo es 100.        |
|Hops     | Salto por ruta de acceso de salto de toodestination de origen.        |
|Hops[].Type     | Tipo de recurso. Los valores posibles son **Source**, **VirtualAppliance**, **VnetLocal** e **Internet**.        |
|Hops[].Id | Identificador único del salto Hola.|
|Hops[].Address | Dirección IP de salto de Hola.|
|Hops[].ResourceId | ResourceID de salto de hello si salto de hello es un recurso de Azure. Si se trata de un recurso de Internet, el identificador de recurso es **Internet**. |
|Hops[].NextHopIds | Identificador único de Hello del próximo salto de hello realizada.|
|Hops[].Issues | Una colección de los problemas que se encontraron durante la comprobación de hello en ese salto. Si no hubiera ningún problema, Hola está en blanco.|
|Hops[].Issues[].Origin | Hola actual salto, donde se produjo el problema. Los valores posibles son:<br/> **Entrada** -problema está en vínculo Hola Hola anterior salto toohello actual salto<br/>**Salida** -problema está en vínculo Hola Hola actual salto toohello próximo salto<br/>**Local** -problema es en salto actual Hola.|
|Hops[].Issues[].Severity | gravedad de Hola de problema de hello detectado. Los valores posibles son **Error** and **Warning**. |
|Hops[].Issues[].Type |tipo de Hola de ha detectado un problema. Los valores posibles son: <br/>**CPU**<br/>**Memoria**<br/>**GuestFirewall**<br/>**DnsResolution**<br/>**NetworkSecurityRule**<br/>**UserDefinedRoute** |
|Hops[].Issues[].Context |Detalles sobre Hola ha detectado un problema.|
|Hops[].Issues[].Context[].key |Devuelve la clave del par de clave-valor Hola.|
|Hops[].Issues[].Context[].value |Devuelve el valor del par de clave-valor Hola.|

Hola aquí te mostramos un ejemplo de un problema que se encuentra en un salto.

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a>Tipo de error

comprobación de conectividad de Hello devuelve los tipos de error acerca de la conexión de Hola. Hello tabla siguiente proporciona una lista de tipos de errores actual Hola devuelta.

|Tipo  |Descripción  |
|---------|---------|
|CPU     | Alta utilización de CPU.       |
|Memoria     | Alta utilización de memoria.       |
|GuestFirewall     | El tráfico se bloquea debido a tooa configuración del firewall de máquina virtual.        |
|DNSResolution     | Error en la resolución DNS para la dirección de destino de Hola.        |
|NetworkSecurityRule    | Una regla de NSG bloquea el tráfico (se devuelve la regla).        |
|UserDefinedRoute|El tráfico se interrumpe debido tooa definido por el usuario o la ruta de sistema. |

### <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooa recurso de conectividad a tooverify visitando: [Compruebe la conectividad con el Monitor de red de Azure](network-watcher-connectivity-powershell.md).

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

