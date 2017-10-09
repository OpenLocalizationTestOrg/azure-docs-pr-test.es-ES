---
title: aaaIntroduction tootopology en Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de las capacidades de topología de Monitor de red de Hola"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a>Introducción tootopology en Monitor de red de Azure

La topología devuelve un gráfo de recursos de red de una red virtual. gráfico de Hola traza la interconexión Hola entre conectividad de red tooend de hello recursos toorepresent Hola final.

![información general de la topología][1]

En el portal de hello, topología devuelve objetos de recursos de hello en un cada red virtual. relaciones de Hola se representan mediante líneas entre recursos de hello recursos fuera de la región de Monitor de red de hello, aunque en recursos de hello grupo no se mostrará. recursos de Hola devueltos en la vista de hello portal son un subconjunto de los componentes de red de Hola que se representan. lista completa de hello toosee de recursos de red puede usar [PowerShell](network-watcher-topology-powershell.md) o [REST](network-watcher-topology-rest.md)

> [!NOTE]
> Se requiere una instancia del Monitor de red en cada región que desee toorun topología en.

Los recursos se devuelven conexión Hola entre ellos se modelan en dos relaciones.

- **Contención**: por ejemplo, la red virtual contiene un subconjunto que incluye una NIC.
- **Asociación**: por ejemplo, una NIC está asociada a una máquina virtual.

### <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo ver toouse PowerShell tooretrieve Hola topología visitando [topología de Monitor de red con PowerShell](network-watcher-topology-powershell.md)

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
