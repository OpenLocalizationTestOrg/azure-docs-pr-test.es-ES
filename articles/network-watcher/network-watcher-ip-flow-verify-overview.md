---
title: comprobar el flujo de tooIP aaaIntroduction en Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de hello IP de Monitor de red flujo comprobar la capacidad"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a>Comprobar el flujo de introducción tooIP en Monitor de red de Azure

Flujo IP Compruebe comprueba si un paquete se permite o deniega tooor desde una máquina virtual basada en la información de tupla de 5. Esta información está formada por la dirección, el protocolo, la dirección IP local, la dirección IP remota, el puerto local y el puerto remoto. Si el paquete de saludo ha sido denegado por un grupo de seguridad, se devuelve el nombre de Hola de regla de Hola que deniega el paquete de saludo. Aunque puede elegir cualquier dirección IP de origen o destino, esta característica ayuda a los administradores diagnosticar rápidamente problemas de conectividad de o toohello internet y desde o entorno local de toohello.

La comprobación de flujo de IP tiene como destino una interfaz de red de una máquina virtual. Flujo de tráfico, a continuación, se comprueba en función de hello configurado tooor de configuración de esa interfaz de red. Esta capacidad es útil para confirmar si una regla en un grupo de seguridad de red está bloqueando tooor de tráfico de entrada o salida de una máquina virtual.

Comprobar una instancia del Monitor de red necesidades toobe creado en todas las regiones que planea toorun flujo IP. Monitor de red es un servicio regional y solo se ejecutó con los recursos en hello misma región. Esto no afecta a Hola comprobar resultados de flujo IP como ruta de hello asociada Hola que NIC todavía se devolverá.

![1][1]

## <a name="next-steps"></a>Pasos siguientes

Visite Hola después toolearn artículo si un paquete se permite o deniega para una máquina virtual específica a través del portal de Hola. [Compruebe si se permite el tráfico en una máquina virtual con IP flujo Compruebe mediante el portal de Hola](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












