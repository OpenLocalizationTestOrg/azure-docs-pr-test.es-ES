---
title: "información general del aaaRedirect de puerta de enlace de aplicaciones de Azure | Documentos de Microsoft"
description: "Obtenga información sobre la funcionalidad de redirección de hello en la puerta de enlace de aplicaciones de Azure"
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a>Introducción a la redirección de Application Gateway

Un escenario común para muchas aplicaciones web es toosupport automática HTTP tooHTTPS redirección tooensure que todas las comunicaciones entre la aplicación y los usuarios se produce a través de una ruta de acceso cifrado. Hola anteriores, los clientes han utilizado técnicas como la creación de un grupo dedicado back-end cuyo único propósito es solicitudes tooredirect recibe en tooHTTPS HTTP.  Puerta de enlace de aplicaciones admite ahora el tráfico de tooredirect de capacidad en hello Application Gateway. Esto simplifica la configuración de la aplicación, optimiza el uso de recursos de Hola y es compatible con nuevos escenarios de redirección incluidos global y basada en la ruta de acceso de redirección. Compatibilidad con redirección de puerta de enlace de aplicaciones no se limita tooHTTP -> redirección HTTPS independiente. Se trata de un mecanismo de redirección genérico, que permite la redirección del tráfico recibido en el agente de escucha de un agente de escucha tooanother en puerta de enlace de aplicaciones. También admite la redirección tooan sitio externo también. Compatibilidad con redirección de puerta de enlace de aplicaciones ofrece Hola siguientes capacidades:

1. Redirección global de agente de escucha de un agente de escucha tooanother en hello puerta de enlace. Esto habilita la redirección de tooHTTPS HTTP en un sitio.
2. Redirección basada en la ruta de acceso. Este tipo de redirección habilita la redirección de tooHTTPS HTTP solo en un área de sitio específico, por ejemplo un área de carro de la compra se indica mediante/carro / *.
3. Sitio de tooexternal de redirección.

![redirección](./media/application-gateway-redirect-overview/redirect.png)

Con este cambio, los clientes tienen un nuevo objeto de configuración de redirección, que especifica el agente de escucha de hello destino toocreate o redirección de toowhich sitio externo se desea. elemento de configuración de Hello también admite tooenable opciones anexar la ruta de acceso URI de Hola y cadena toohello redirige la dirección URL de consulta. Los clientes también pueden elegir si la redirección es un archivo temporal (código de estado HTTP 302) o a una redirección permanente (código de estado HTTP 301). Una vez creada esta configuración de redirección es agente de escucha del origen toohello conectados a través de una nueva regla. Cuando usa una regla básica, configuración de redirección de hello está asociado a un agente de escucha de origen y una redirección global. Cuando se utiliza una regla basada en la ruta de acceso, configuración de redirección de Hola se define en el mapa de ruta de acceso de dirección URL de hello y, por tanto, solo aplica toohello área de ruta de acceso específica de un sitio.

### <a name="next-steps"></a>Pasos siguientes

[Configuración de la redirección de direcciones URL en una puerta de enlace de aplicaciones](application-gateway-configure-redirect-powershell.md)
