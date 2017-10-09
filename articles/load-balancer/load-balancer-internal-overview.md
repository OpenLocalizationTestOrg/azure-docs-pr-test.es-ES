---
title: "información general del equilibrador de carga aaaInternal | Documentos de Microsoft"
description: "Información general de equilibrador de carga interno y sus características. Cómo funciona un equilibrador de carga para los extremos de Azure y posibles escenarios tooconfigure internos"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a>Información general sobre el equilibrador de carga interno

A diferencia de hello Internet orientados al equilibrador de carga equilibrador de carga interno de hello (ILB) dirige el tráfico tooresources solo dentro de servicio de nube de Hola o mediante VPN tooaccess Hola infraestructura de Azure. infraestructura de Hello restringe el acceso toohello con equilibrio de carga direcciones IP virtual (VIP) de un servicio de nube o una red Virtual para que nunca será el punto de conexión de tooan directamente expuesto Internet. Esto permite una línea interna de toorun de las aplicaciones de negocio (LOB) en Azure y tener acceso desde dentro de la nube de Hola o desde recursos locales.

## <a name="why-you-may-need-an-internal-load-balancer"></a>Por qué es posible que sea necesario un equilibrador de carga interno

El equilibrio de carga interno (ILB) de Azure proporciona equilibrio de carga entre las máquinas virtuales que residen dentro de un servicio en la nube o en una red virtual con un ámbito regional. Para obtener información sobre el uso de Hola y la configuración de redes virtuales con un ámbito regional, consulte [redes virtuales regionales](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) Hola blog de Azure. Las redes virtuales existentes que se han configurado para un grupo de afinidad no pueden usar ILB.

ILB habilita Hola siguientes tipos de equilibrio de carga:

* Dentro de un servicio de nube de máquinas virtuales tooa conjunto de máquinas virtuales que residen dentro de hello mismo servicio en la nube (consulte la figura 1).
* En una red virtual, desde máquinas virtuales en el conjunto de tooa de red virtual de Hola de máquinas virtuales que residen dentro de hello mismo servicio en la nube de hello virtual de red (consulte la figura 2).
* Para una red virtual entre entornos, de conjunto de tooa de equipos locales de máquinas virtuales que residen dentro de hello mismo servicio en la nube de hello virtual de red (consulte la figura 3).
* Aplicaciones accesibles desde Internet, de varios niveles en el que los niveles de back-end de hello no son accesibles desde Internet pero requieren equilibrio de carga para tráfico de capa de hello orientado a Internet.
* Equilibrio de carga para las aplicaciones LOB hospedadas en Azure sin requerir hardware ni software adicional de equilibrador de carga. Incluir servidores locales Hola conjunto de equipos cuyo tráfico tiene una carga equilibrada.

## <a name="internet-facing-multi-tier-applications"></a>Aplicaciones de niveles múltiples accesibles desde Internet

nivel de Hello web tiene extremos con conexión a Internet para clientes de Internet y forma parte de un conjunto con equilibrio de carga. equilibrador de carga de Hello distribuye el tráfico entrante de los clientes web para TCP puerto 443 (HTTPS) toohello los servidores web.

servidores de base de datos de Hello están detrás de un punto de conexión ILB que usan servidores web de hello para el almacenamiento. Esta carga del servicio de base de datos con equilibrio de punto de conexión, qué tráfico se carga equilibrada entre los servidores de base de datos de hello en hello ILB conjunto.

siguiente imagen muestra de Hola Hola Internet con conexión a la aplicación de varios niveles dentro de hello mismo servicio en la nube.

![Equilibrio de carga interno en un solo servicio en la nube](./media/load-balancer-internal-overview/IC736321.png)

Figura 1 - Una aplicación de niveles múltiples accesible desde Internet

Otro uso posible para una aplicación de varios nivel es cuando hello ILB implementa el servicio de nube diferente de tooa de Hola a un servicio de consumo de Hola para hello ILB.

En la nube con hello tendrá la misma red virtual de servicios tienen acceso a extremo ILB toohello. Hola siguiendo la imagen se muestra en servidores front-end web están en un servicio de nube diferente de la base de datos back-end de Hola y utilizando Hola extremo ILB dentro de hello misma red virtual.

![Equilibrio de carga interno entre servicios en la nube](./media/load-balancer-internal-overview/IC744147.png)

Figura 2 - Servidores front-end en un servicio en la nube diferente

## <a name="intranet-line-of-business-applications"></a>Aplicaciones de línea de negocio de Intranet

Tráfico de los clientes de red local de hello obtener el equilibrio de carga en conjunto Hola de los servidores LOB con red de tooAzure de conexión VPN.

equipo de cliente Hello tendrá acceso tooan dirección IP del servicio de VPN de Azure con VPN de punto toosite. Permite Hola uso Hola aplicación LOB hospedada detrás de punto de conexión de hello ILB.

![Con VPN de punto toosite de equilibrio de carga interno](./media/load-balancer-internal-overview/IC744148.png)

Figura 3: aplicaciones LOB hospedadas detrás de punto de conexión de hello LB

Otro escenario para hello LOB es toohave una red para el toohello virtual de sitio toosite VPN donde se configura el punto de conexión de hello ILB. Esto permite que el punto de conexión de local red tráfico toobe enrutado toohello ILB.

![Usar toosite VPN de sitio de equilibrio de carga interno](./media/load-balancer-internal-overview/IC744150.png)

Figura 4 - tráfico de red local enrutada toohello ILB extremo

## <a name="limitations"></a>Limitaciones

Las configuraciones del equilibrador de carga interno no son compatibles con SNAT. En el contexto de Hola de este documento, SNAT hace referencia a traducción de direcciones en la red de origen de tooport enmascarado.  Esto aplica tooscenarios que una máquina virtual en un grupo de equilibradores de carga tiene dirección IP del tooreach Hola respectivos interno equilibrador de carga servidor front-end. Este escenario no es compatible con el equilibrador de carga interno. Errores de conexión se producirán al flujo de hello es toohello de carga equilibrada VM que se originaron flujo Hola. Debe usar un equilibrador de carga de estilo proxy para estos escenarios.

## <a name="next-steps"></a>Pasos siguientes

[Compatibilidad de Azure Resource Manager con Azure Load Balancer](load-balancer-arm.md)

[Introducción a la configuración de un equilibrador de carga accesible desde Internet](load-balancer-get-started-internet-arm-ps.md)

[Introducción a la configuración de un equilibrador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
