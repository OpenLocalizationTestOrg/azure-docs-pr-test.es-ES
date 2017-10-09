---
title: 'conectividad de aaaCheck con Monitor de red de Azure: portal de Azure | Documentos de Microsoft'
description: "Esta página explica cómo comprobar la conectividad de toouse con Monitor de red con hello portal de Azure"
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
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a>Compruebe la conectividad con el Monitor de red de Azure con hello portal de Azure

> [!div class="op_single_selector"]
> - [Portal](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [API de REST de Azure](network-watcher-connectivity-rest.md)

Obtenga información acerca de cómo se puede establecer toouse conectividad tooverify si una conexión TCP directa de una tooa de máquina virtual tiene el punto de conexión.

## <a name="before-you-begin"></a>Antes de empezar

En este artículo se supone que tiene Hola recursos siguientes:

* Una instancia del Monitor de red en la región de Hola que desea toocheck conectividad.

* Conectividad de toocheck de máquinas virtuales con.

> [!IMPORTANT]
> La comprobación de conectividad requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`. Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="check-connectivity-tooa-virtual-machine"></a>Compruebe la conectividad tooa virtual machine

Este ejemplo comprueba la máquina virtual de conectividad tooa destino en el puerto 80.

Navegue tooyour Monitor de red y haga clic en **comprobación de conectividad (versión preliminar)**. Seleccione toocheck conectividad de máquina virtual de Hola de. Hola **destino** sección elija **seleccione una máquina virtual** y elija la máquina virtual correcta de Hola y tootest de puerto.

Una vez que pulses **comprobar**, se comprueban la conectividad de hello entre máquinas virtuales Hola Hola el puerto especificado. En el ejemplo de Hola, Hola destino VM es inaccesible, se muestra una lista de saltos.

![Resultados de la comprobación de la conectividad de una máquina virtual][1]

## <a name="check-remote-endpoint-connectivity"></a>Comprobación de la conectividad de un punto de conexión remoto

conectividad de hello toocheck y el extremo remoto de tooa de latencia, elija hello **especificar manualmente** botón de opción de hello **destino** sección, especifique la dirección url de Hola y el puerto de Hola y haga clic en **comprobar** .  Se utiliza para puntos de conexión remotos como sitios web y puntos de conexión de almacenamiento.

![Resultados de la comprobación de conectividad para un sitio web][2]

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de la captura de paquetes de tooautomate con las alertas de la máquina Virtual mediante la visualización [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)

Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
