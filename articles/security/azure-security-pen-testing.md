---
title: aaaPen pruebas | Documentos de Microsoft
description: "artículo de Hello proporciona información general del proceso (pentest) de prueba de penetración de Hola y el rendimiento de pentest frente a las aplicaciones que se ejecutan en la infraestructura de Azure."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 695d918c-a9ac-4eba-8692-af4526734ccc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: 202c239f46d8693ab7aa85e237235372e743e108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pen-testing"></a>Pruebas de penetración
Una de las grandes virtudes de hello acerca del uso de Microsoft Azure para pruebas de aplicación y la implementación es que no es necesario tooput juntos un toodevelop de infraestructura local, probar e implementar las aplicaciones. Toda la infraestructura de Hola se encarga del servicios de la plataforma Microsoft Azure Hola. No tienes tooworry sobre requisa de entidades, adquirir y "instalación en rack y apilado" su propio hardware local.

Esto es genial, pero seguirá necesitando toomake seguro realizar su seguridad normal diligencia. Uno de cosas Hola que debe toodo es penetración probar hello las aplicaciones se implementan en Azure.

Es posible que ya sepa que realiza Microsoft realiza [pruebas de penetración de nuestro entorno de Azure](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e). Esto nos ayuda a mejorar nuestra plataforma y guía nuestras acciones para mejorar los controles de seguridad, introducir nuevos controles de seguridad y mejorar nuestros procesos de seguridad.

No es de la pluma probar su aplicación, pero sabemos que se desea y necesita tooperform lápiz pruebas en sus propias aplicaciones. Que es bueno, porque cuando se mejorar la seguridad de Hola de las aplicaciones, para ayudar a proteger ecosistema de Azure completo Hola.

Cuando el lápiz probar las aplicaciones, podría parecer un ataque toous. Nosotros [supervisamos continuamente](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) para detectar patrones de ataque e iniciamos un proceso de respuesta a incidentes si es necesario. No ayudarle y no ayuda a nosotros si se activa una respuesta a incidentes due tooyour propio debido diligencia lápiz pruebas.

¿Qué toodo?

Cuando esté listo toopen probar las aplicaciones hospedadas en Azure, tendrá una opción demasiado[háganoslo saber](https://portal.msrc.microsoft.com/en-us/engage/pentest). Una vez que se sabe que va a realizar pruebas específicas de toobe, sin darse cuenta se no se cerró (por ejemplo, la dirección IP de Hola que se está probando de bloqueo), siempre y cuando las pruebas ajustan toohello Azure pluma pruebas términos y condiciones descritos en [En la nube Microsoft Unified penetración probar reglas de compromiso](https://technet.microsoft.com/en-us/mt784683).
Entre las pruebas estándar que puede realizar se incluyen:

* Pruebas en su Hola de toouncover extremos [Abrir proyecto de seguridad aplicación de Web (OWASP) top 10 vulnerabilidades](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
* [Pruebas de vulnerabilidad ante datos aleatorios o inesperados](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) de los puntos de conexión
* [Exploración de puertos](https://en.wikipedia.org/wiki/Port_scanner) de los puntos de conexión

Un tipo de prueba que no puede realizar es ningún tipo de ataque [de denegación de servicio (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) . Esto incluye iniciar un ataque de denegación de servicio o la realización de pruebas relacionadas que puedan determinar, demostrar o simular cualquier tipo de ataque de denegación de servicio.

¿Son que listo tooget partió lápiz probar sus aplicaciones hospedadas en Microsoft Azure? Si es así, principal en sobre toohello [información general de prueba de penetración](https://technet.microsoft.com/library/mt784683.aspx) página (y haga clic en crear un botón Probar solicitud final Hola de página Hola Hola. También encontrará más información sobre el lápiz de hello pruebas términos y condiciones y vínculos útiles en cómo puede crear informes de seguridad si hay errores relacionados tooAzure o cualquier otro servicio de Microsoft.
