---
title: "aaaInternet orientada hacia la información general del equilibrador de carga | Documentos de Microsoft"
description: "Información general sobre el equilibrador de carga accesible desde Internet y sus características. Cómo funciona un Equilibrador de carga de Azure mediante máquinas virtuales y servicios en la nube."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a>Información general sobre el equilibrador de carga accesible desde Internet

Equilibrador de carga Azure asigna Hola público IP dirección y número de puerto entrante tráfico toohello privada dirección IP y puerto número de máquina virtual de Hola y viceversa para el tráfico de respuesta de saludo de la máquina virtual de Hola. Reglas de equilibrio de carga permiten a toodistribute determinados tipos de tráfico entre varias máquinas virtuales o servicios. Por ejemplo, se puede propagar carga Hola de tráfico de solicitudes web en varios servidores web o roles web.

Para un servicio de nube que contiene instancias de roles web o roles de trabajo, puede definir un extremo público en el archivo de definición (.csdef) del servicio de Hola.

Hola *servicedefinition.csdef* archivo contiene la configuración de punto de conexión de Hola y cuando haya varias instancias de rol para una implementación de rol web o de trabajo, equilibrador de carga de Hola se configurará para él. implementación de nube de Hello forma tooadd instancias tooyour está cambiando el número de instancias de hello en el archivo de configuración de servicio de hello (. csfg).

Hello en la ilustración siguiente se muestra un extremo con equilibrio de carga para tráfico web que se comparte entre tres máquinas virtuales para hello pública y privada puerto TCP 80. Estas tres máquinas virtuales se encuentran en un conjunto con equilibrio de carga.

![ejemplo de equilibrador de carga público](./media/load-balancer-internet-overview/IC727496.png)

Figura 1: punto de conexión de carga equilibrada para tráfico web

Cuando los clientes de Internet envían solicitudes de páginas web toohello de dirección IP pública del servicio de nube de hello en el puerto TCP 80, Hola equilibrador de carga de Azure distribuye las solicitudes de hello entre Hola tres máquinas virtuales en el conjunto de equilibrio de carga de Hola. Para obtener más información acerca de los algoritmos de equilibrador de carga, vea hello [página de información general del equilibrador de carga](load-balancer-overview.md#load-balancer-features).

De forma predeterminada, Azure Load Balancer distribuye el tráfico de red equitativamente entre varias instancias de máquina virtual. También puede configurar la afinidad de la sesión. Para más información, consulte el [modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md).

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de [equilibrador de carga interno](load-balancer-internal-overview.md) toobetter comprender qué equilibrador de carga es mejor para su implementación en la nube.

También puede [empezar a crear un equilibrador de carga accesible desde Internet](load-balancer-get-started-internet-arm-ps.md) y configurar el tipo de [modo de distribución](load-balancer-distribution-mode.md) para un comportamiento especifico del tráfico de red del equilibrador de carga.

Si su aplicación necesita que las conexiones de tookeep activo de servidores detrás de un equilibrador de carga, puede conocer más acerca de [inactivo de la configuración de tiempo de espera TCP para un equilibrador de carga](load-balancer-tcp-idle-timeout.md). Cuando se usa el equilibrador de carga de Azure le servirá de ayuda toolearn acerca del comportamiento de conexión inactiva.
