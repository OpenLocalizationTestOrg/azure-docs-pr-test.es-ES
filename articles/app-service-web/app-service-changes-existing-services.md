---
title: aaaAzure servicio de aplicaciones y su impacto en los servicios de Azure existentes
description: "Explica cómo Hola nuevo servicio de aplicación de Azure y sus características de afectan a los servicios existentes en Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Servicio de aplicaciones de Azure y los servicios de Azure existentes
En este artículo se describe Hola cambios tooexisting servicios de Azure como parte de hello cambio toobring junto varios servicios de Azure en [servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/), una nueva oferta integrada.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Información general
[Servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/) es un servicio de nube nuevos y únicos que permite a los desarrolladores toocreate web y aplicaciones móviles para cualquier plataforma y en cualquier dispositivo. Servicio de aplicaciones es que una solución integrada diseñada toostreamline repite las funciones de codificación, integrar con enterprise y sistemas de SaaS y automatizar procesos de negocio al tiempo que satisface sus necesidades de seguridad, confiabilidad y escalabilidad.

Servicio de aplicaciones reúne Hola después de Azure existentes services - [sitios Web](https://azure.microsoft.com/services/websites/), [servicios móviles](https://azure.microsoft.com/services/mobile-services/), y [servicios de Biztalk](https://azure.microsoft.com/services/biztalk-services/) en una sola combinan servicio, mientras que agregar nuevas capacidades.  Servicio de aplicaciones permite hello toohost siguientes tipos de aplicación:

* Web Apps
* Mobile Apps
* API Apps
* Logic Apps

Hello tabla siguiente explica cómo existente Azure servicios asignan tooApp hello y servicio aplicación tipos disponibles dentro de él.

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%">Servicio de Azure existente</th>
<th align="left", style="width:10%">Servicio de aplicaciones de Azure</th>
<th align="left", style="width:80%">Qué cambia</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Sitios web Azure</td>
<td align="left">Web Apps</td>
<td align="left"><li>Para los sitios Web de Azure, servicio de aplicaciones está estrictamente limitado toochanging Hola nombre sitios Web tooWeb aplicaciones.
<p><li>Todas las instancias existentes de Sitios web serán ahora Aplicaciones web en el Servicio de aplicaciones.</p>
<p><li>Puede tener acceso a sus sitios Web existente a través de hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Portal de Azure</a>, donde encontrará todos los sitios existentes en <em>aplicaciones Web</em>.</p>
<p><li><em>Plan de hospedaje de Web</em> es ahora <em>Plan de servicio de aplicaciones</em>. Un <em>plan de App Service</em> puede hospedar cualquier tipo de aplicación de App Service, como Web Apps, Mobile Apps, Logic Apps o API Apps.</p>
<p><li>Aplicaciones web del Servicio de aplicaciones de Azure tiene ahora disponibilidad general.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Obtener más información sobre las aplicaciones Web</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Servicios móviles de Azure</td>
<td align="left">Mobile Apps</td>
<td align="left"><p><li>Servicios móviles continuar toobe disponible como un servicio independiente y siguen siendo totalmente compatibles.</p>
<p><li>Aplicaciones móviles es un tipo de aplicación de servicio de aplicaciones, que integra toda la funcionalidad de hello de servicios móviles y mucho más.</p>
<p><li>Es fácil demasiado<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrar desde servicios móviles tooMobile aplicaciones</a>.</p>
<p><li>Como parte de App Service, Mobile Apps incluye nuevas funcionalidades, además de Mobile Services, como la integración con sistemas locales y SaaS, espacios de ensayo, WebJobs y opciones de escalado mejoradas, entre otras.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Obtener más información sobre aplicaciones móviles</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">API Apps</td>
<td align="left">
<p><li>Aplicaciones de API es un nuevo tipo de aplicación de servicio de aplicaciones que permite crear y utilizar las API en la nube de hello con facilidad.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/api/">Más información acerca de las aplicaciones de la API</a>.</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">Logic Apps</td>
<td align="left">
<p><li>Aplicaciones lógicas es un nuevo tipo de aplicación de App Service que permite automatizar los procesos de negocio fácilmente.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/logic/">Obtener más información sobre las aplicaciones lógicas</a>.</p></td>
</tr>
<tr class="odd">
<td align="left">Servicios de BizTalk de Azure</td>
<td align="left">Aplicaciones de API de BizTalk</td>
<td align="left">
<li><p>Servicios de BizTalk continuar toobe disponible como un servicio independiente y siguen siendo totalmente compatibles.</p>
<li><p>Todas las funcionalidades de hello de servicios de BizTalk se integran en servicio de aplicaciones como aplicaciones de API permite a los usuarios tooperform integraciones y escenarios de integración de B2B con cualquiera de los tipos de aplicación hello en el servicio de aplicaciones.</p>
<li><p>Con las aplicaciones lógicas, ahora puede automatizar procesos empresariales mediante una experiencia visual diseñar toocreate flujos de trabajo.</p></td>
</tr>
</tbody>
</table>

toolearn más información, visite [documentación de servicio de aplicaciones](https://azure.microsoft.com/documentation/services/app-service/).

