---
title: uso de ancho de banda de red de Azure RemoteApp aaaEstimate | Documentos de Microsoft
description: "Obtenga información acerca de los requisitos de ancho de banda de red de Hola para las colecciones de RemoteApp de Azure y aplicaciones."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 3127f4c7-f532-46c3-ba9b-649f647abec1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 675ee82f26ddb46a3bb3e0ee95ed397e4064e45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="estimate-azure-remoteapp-network-bandwidth-usage"></a>Calcular el uso del ancho de banda de red de Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

RemoteApp de Azure utiliza hello toocommunicate de protocolo de escritorio remoto (RDP) entre aplicaciones que se ejecutan en hello nube de Azure y los usuarios. Este artículo proporciona algunas directrices básicas que puede usar tooestimate que uso de red y potencialmente evaluación el uso de ancho de banda de red por usuario de Azure RemoteApp.

Calcular el uso del ancho de banda por usuario es muy complejo y requiere la ejecución de varias aplicaciones simultáneamente en escenarios multitarea donde las aplicaciones podrían influir en el rendimiento de la otra basándose en la demanda del ancho de banda de red. Tipo de hello incluso de cliente de escritorio remoto (por ejemplo, el cliente de Mac frente a cliente HTML5) puede provocar resultados de ancho de banda de toodifferent. toohelp, trabajar con estas complicaciones, se estropea escenarios de uso de hello en varias situaciones del mundo real Hola comunes categorías tooreplicate. (Donde escenario real de hello es, por supuesto, una combinación de categorías y varía según el usuario.)

Antes de seguir adelante: tenga en cuenta que suponemos RDP proporciona una experiencia de buen tooexcellent para la mayoría de los escenarios de uso en redes con latencia inferior a 120 ms y ancho de banda más de 5 MB: Esto se basa en toodynamically de capacidad de RDP ajustar mediante el uso de red disponible Hola hello y ancho de banda estimado necesidades de ancho de banda de la aplicación. Este artículo va más allá de aquellas toolook de "mayoría escenarios de uso" en el perímetro de hello, donde los escenarios inician toounwind y toodegrade comienza la experiencia del usuario.

Desproteger ahora Hola siguientes artículos para obtener detalles de hello, incluidos los factores tooconsider, recomendaciones de línea base y lo que no incluimos en nuestras estimaciones.

* [¿Cómo funcionan el ancho de banda de red y la calidad de la experiencia conjuntamente?](remoteapp-bandwidthexperience.md)
* [Probar su uso de ancho de banda de red con algunos escenarios comunes](remoteapp-bandwidthtests.md)
* [Directrices rápidas si no tienes tootest de tiempo o capacidad de Hola](remoteapp-bandwidthguidelines.md)

## <a name="what-are-we-not-including"></a>¿Qué no incluimos?
Cuando revise Hola propuestos pruebas y nuestras recomendaciones generales (y abiertamente genéricos), tenga en cuenta que no hay algunos factores que no se tuvo en cuenta. Por ejemplo, Hola complicaciones de experiencia de usuario proporcionadas por naturaleza asimétrica de Hola de carga frente a ancho de banda de descarga. naturaleza asimétrica de Hello de la mayoría de las redes Wi-Fi además afectará al rendimiento de Hola y percepción de experiencia de usuario de Hola. Para escenarios interactivos tráfico de nivel inferior de hello puede asignarse prioridad a inferior a hello en dirección ascendente, que puede aumentar el número de Hola de fotogramas de vídeo o audio perdidos y, por tanto, afectar percepción del usuario de Hola de hello experiencia de transmisión por secuencias. Puede ejecutar su propio toosee experimentos lo que es adecuado para el caso de uso específicos y la red.

Si bien se trata de redirección de dispositivos, no se tuvo en impacto de ancho de banda de consideración Hola Hola de tráfico de red causado por los dispositivos conectados, como el almacenamiento, impresoras, escáneres, cámaras web y otros dispositivos USB. efecto de Hola de dichos dispositivos normalmente pico necesidades de ancho de banda de hello temporalmente y desaparece cuando se completa la tarea hello. Pero si se realiza con frecuencia, la demanda de ancho de banda puede ser bastante notable.

Se también se describe cómo un usuario puede afectar a otros usuarios en hello misma red. Por ejemplo, un usuario que utiliza vídeo de 4K en una red de 100 MB/s significativamente afecte a otros usuarios de esa misma red intentar toodo Hola la misma tarea. Lamentablemente obtiene impacto de hello toodetermine progresivamente más difícil de uso simultáneo toogive una recomendación común o global acerca del rendimiento del sistema de hello en el agregado. Lo único que podamos poner es que Hola protocolo tecnología subyacente harán que Hola mejorar el uso de ancho de banda de red disponible hello, pero tiene sus limitaciones.

