---
title: salto de toonext aaaIntroduction en Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de Monitor de red de Hola capacidad de salto siguiente"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a>Salto de toonext de introducción en el Monitor de red de Azure

El tráfico de una máquina virtual se envía un destino tooa basándose en rutas efectivas Hola asociadas con una NIC. Próximo salto obtiene tipo hello de próximo salto y la dirección IP de un paquete desde una máquina virtual específica y la NIC. Esto ayuda a toodetermine si hello paquete se está dirigido toohello destino o se holed de tráfico de Hola que se va a negro. Una configuración incorrecta de las rutas por usuario de hello, donde un tráfico es dirigido tooan local ubicación o un dispositivo virtual, puede dar lugar a problemas de tooconnectivity. Próximo salto también devuelve la tabla de rutas de hello asociada de próximo salto Hola. Al consultar un próximo salto si Hola ruta se define como una ruta definida por el usuario, se devolverá esa ruta. De lo contrario, la funcionalidad devolverá "Ruta de sistema".

![información general sobre próximo salto][1]

Hola aquí te mostramos una lista de hello tipos de próximo salto que se pueden devolver al consultar el próximo salto.

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

### <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo toouse siguiente salto toofind problemas con conectividad de red visitando [comprobación Hola de próximo salto en una máquina virtual](network-watcher-check-next-hop-portal.md)

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













