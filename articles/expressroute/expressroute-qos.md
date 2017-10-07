---
title: Requisitos de ExpressRoute aaaQoS | Documentos de Microsoft
description: "En esta página se proporcionan requisitos detallados para configurar y administrar QoS para circuitos ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a>Requisitos de QoS ExpressRoute
Skype Empresarial tiene varias cargas de trabajo que requieren tratamiento diferenciado de QoS. Si tiene previsto tooconsume de servicios de voz a través de ExpressRoute, debe cumplir los requisitos de toohello descritos a continuación.

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> Requisitos de QoS aplican solo al emparejamiento de Microsoft toohello. Restablecer too0 serán los valores DSCP de Hello en el tráfico de red recibido en pares públicos de Azure y Azure intercambio de tráfico privado. 
> 
> 

Hello tabla siguiente proporciona una lista de marcado de DSCP usado Skype para la empresa. Consulte demasiado[administración de QoS para Skype empresarial](https://technet.microsoft.com/library/gg405409.aspx) para obtener más información.

| **Clase de tráfico** | **Tratamiento (marcado de DSCP)** | **Cargas de trabajo de Skype Empresarial** |
| --- | --- | --- |
| **Voz** |EF (46) |Voz de Skype o Lync |
| **Interactivo** |AF41 (34) |Video, VBSS |
| AF21 (18) |Uso compartido de aplicaciones | |
| **Valor predeterminado** |AF11 (10) |Transferencia de archivos |
| CS0 (0) |Nada más | |

* Debe clasificar las cargas de trabajo de Hola y marcar valores DSCP de hello correctos. Siga las instrucciones de hello indicadas [aquí](https://technet.microsoft.com/library/gg405409.aspx) acerca de cómo tooset marcas de DSCP de la red.
* Debe configurar y admitir varias colas de QoS dentro de la red. Debe ser una clase independiente de voz y reciben un tratamiento EF Hola especificado en RFC 3246. 
* Puede decidir Hola Queue mecanismo, la directiva de detección de congestión y asignación de ancho de banda por clase de tráfico. Sin embargo, hello DSCP marcar de Skype para cargas de trabajo de negocios debe conservarse. Si usas marcas DSCP no indicados anteriormente, p. ej. AF31 (26), debe volver a escribir este too0 del valor DSCP antes de enviar tooMicrosoft de paquetes de saludo. Microsoft sólo envía paquetes marcados con hello el valor de DSCP se muestra en hello por encima de la tabla. 

## <a name="next-steps"></a>Pasos siguientes
* Consulte los requisitos de toohello para [enrutamiento](expressroute-routing.md) y [NAT](expressroute-nat.md).
* Vea la siguiente Hola vincula tooconfigure la conexión ExpressRoute.
  
  * [Creación de un circuito ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configuración del enrutamiento](expressroute-howto-routing-classic.md)
  * [Vincular un circuito de ExpressRoute de tooan de red virtual](expressroute-howto-linkvnet-classic.md)

