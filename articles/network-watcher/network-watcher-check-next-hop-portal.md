---
title: "aaaFind próximo salto con Monitor Azure red próximo salto: portal de Azure | Documentos de Microsoft"
description: "En este artículo se describe cómo puede ver qué Hola siguiente tipo de salto es y dirección ip mediante el uso de salto siguiente Hola portal de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a>Averiguar qué tipo de hello próximo salto es con capacidad de próximo salto de hello en Monitor de red de Azure mediante el portal de Hola

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API de REST de Azure](network-watcher-check-next-hop-rest.md)

Próximo salto es una característica del Monitor de red que proporciona la capacidad de hello obtener tipo hello de próximo salto y la dirección IP basándose en una máquina virtual especificada. Esta característica es útil para determinar si el tráfico que sale de una máquina virtual recorre una puerta de enlace, internet o redes virtuales tooget tooits destino.

## <a name="before-you-begin"></a>Antes de empezar

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red. escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.

## <a name="scenario"></a>Escenario

escenario de Hello descrito en este artículo usa toofind de salto siguiente tipo hello de próximo salto y la dirección IP para un recurso. toolearn más información acerca de próximo salto, visite [información general sobre salto siguiente](network-watcher-next-hop-overview.md).

En este escenario va a:

* Recuperar de próximo salto Hola desde una máquina virtual.

## <a name="get-next-hop"></a>Obtención del próximo salto

### <a name="step-1"></a>Paso 1

Navegar tooyour recurso de Monitor de red en hello portal de Azure.

### <a name="step-2"></a>Paso 2

Haga clic en **del próximo salto** en el panel de navegación de hello, máquina virtual de hello select e interfaz de red, rellenar Hola IP de origen y de destino y haga clic en hello **del próximo salto** botón.

> [!NOTE]
> Salto siguiente requiere que el recurso de máquina virtual de Hola se asigna toorun.

![información general sobre obtención del próximo salto][1]

### <a name="step-3"></a>Paso 3

Una vez completada la tarea hello, se proporcionan los resultados de Hola. Hola dirección IP y el tipo de dispositivo Hola de próximo salto es, se muestra. Hello tabla siguiente muestran los valores devueltos disponibles hello en el portal de Hola.

**Tipo de próximo salto**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

Si una ruta personalizada se ha usado tooroute este tráfico, la ruta definida por el usuario de hello (UDR) se muestra también con los resultados de Hola.

![resultados de obtención del próximo salto][2]

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooreview la configuración del grupo de seguridad de red mediante programación si visita [NSG auditoría con Monitor de red](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














