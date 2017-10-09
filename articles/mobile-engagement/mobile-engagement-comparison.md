---
title: aaaComparing Azure Mobile Engagement con otros servicios de Azure similar
description: "Comparación de Azure Mobile Engagement con otros servicios similares de Azure: HockeyApp, AppInsights y Centros de notificaciones"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f114775-3a9a-4dd4-8d59-b10d1da9a68b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0859ae9980d0fa96ffbc0edfbd795ccc58d2c843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-azure-mobile-engagement-with-other-similar-azure-services"></a>Comparación de Azure Mobile Engagement con otros servicios similares de Azure
lista de Hello de servicios ofrecidos por Microsoft Azure está expandiendo alguna vez y a veces quizás se pregunte cómo es diferente de este otro servicio que acaba de leer o enterarse de Azure Mobile Engagement. Este artículo intenta tooclear confusión de Hola y dirige toochoose Azure Mobile Engagement cuando resulta más adecuada para su uso. 

Azure Mobile Engagement es un servicio dirigido específicamente **para los vendedores/CMOs digitales** pero se puede usar por ninguna **propietario de la aplicación móvil o publicador** que desea tooincrease uso de hello, retención y ahorro de sus aplicaciones móviles. 

*Es una plataforma de participación de usuarios de software como servicio (SaaS) que proporciona información detallada controlada por datos sobre el uso de las aplicaciones y segmentación de usuarios en tiempo real, y habilita las notificaciones push dependientes de contexto y la mensajería en la aplicación.* 

Dividir esta definición, tenemos hello siguientes características clave que también resalta la propuesta de valor único:

1. **Notificaciones push dependientes del contexto y mensajería en la aplicación**
   
   Se trata de foco de núcleo de Hola de producto de hello: realizar notificaciones de inserción de destino y personalizada. Y para este toohappen, que se recopilan datos de análisis de comportamiento enriquecido. 
2. **Información detallada controlada por datos sobre el uso de la aplicación**
   
   Proporcionamos multiplataforma SDK toocollect Hola análisis de comportamiento acerca de los usuarios de aplicación Hola. Tenga en cuenta los análisis de comportamiento de término hello (exactamente igual que en el análisis de rendimiento) porque se centra en cómo los usuarios de aplicación de hello usan aplicación hello. Que se recopilan datos de análisis de rendimiento básicas sobre errores, bloqueos etcetera, pero es decir Hola foco del núcleo de producto de Hola. 
3. **Segmentación de usuarios en tiempo real**
   
   Una vez que hayas recopilado los datos de análisis de comportamiento de los usuarios de la aplicación, le permitimos toosegment según diversos parámetros de la audiencia y tooenable de los datos recopilados se toorun como destino las campañas de inserción. 
4. **Software como servicio (SaaS):**
   
   Tiene un portal independiente desde el portal de administración de Azure de Hola que es toointeract optimizada y ver funciones analíticas enriquecidas comportamientos acerca de los usuarios de aplicación de Hola y ejecutar campañas de inserción. producto de Hello es orientadas tooget dar en ningún momento.   

Con este conjunto de diferenciación en mano, mostramos cómo se comparan con otras ofertas de Azure aparentemente similares: tenga en cuenta ese artículo hello no realiza una comparación de nivel de característica, sino que toma una más toodefine de enfoque de escenario según qué producto funciona mejor:

1. [HockeyApp](https://azure.microsoft.com/services/hockeyapp/) es la solución de DevOps móvil de Microsoft de Hola. Con él, puede distribuir compilaciones toobeta evaluadores, recopilar datos de bloqueo y obtener comentarios del usuario. También se integra en Visual Studio Team Services, lo que facilita las implementaciones de compilaciones y la integración de elementos de trabajo. 
   
   Hola aquí es DevOps y recopilar datos de análisis de rendimiento sobre aplicaciones móviles de Hola. Puede terminar con la integración de ambos HockeyApps y Mobile Engagement en la aplicación y no se podrá inusual porque aunque hay cierta superposición en los datos recopilado de hello, Hola core enfoque de productos de hello es diferente y ayudan a lograr diferentes objetivos para usted.  
2. [Application Insights](../application-insights/app-insights-overview.md) si su aplicación móvil tiene un lado del servidor, a continuación, va a usar el lado del servidor de web Application Insights toomonitor hello de la aplicación pero de lado cliente de hello aplicaciones móviles, debe usar HockeyApp. 
3. [Los centros de notificaciones](https://azure.microsoft.com/services/notification-hubs/) ofrece un servicio ligero en sentido de Hola que no es necesario un SDK integrado en la aplicación móvil de hello y puede tener control total de la aplicación móvil y permite enviar notificaciones de inserción con capacidades básicas de etiquetado. Esto es muy útil para cualquier propietario de la aplicación que se ocupa de menor sobre cómo destinar y más acerca de la información de envío de comunicación al instante tootheir los usuarios de aplicación (difusión tooa grandes llenado). 
   
   Tenga en cuenta foco Hola aquí en el envío de notificaciones rápidas increíblemente con capacidad de segmentación básica. 

Observemos algunos escenarios:

1. TIM forma parte del equipo de marketing digital hello en un almacén de Adventure Works que publique aplicaciones móviles para los usuarios. Objetivo de TIM es tooensure que los usuarios de Hola que descargan sus aplicaciones móviles seguir toouse y con frecuencia. Esto no sólo aumenta una marca de conectar con los usuarios de aplicación Hola sino que también aumenta monetización cuando los usuarios de aplicación Hola realizan compras mediante aplicación móvil de Hola. Para este Tim tendrá toosend destino notificaciones toohello aplicación a los usuarios, lo que le resulte útil, tooencourage les tooopen Hola aplicación y volver a menudo tooit. Aquí es cuando Mobile Engagement le resultará útil a Tim. 
2. JoAnn forma parte del equipo de desarrollo de Hola de hello de aplicaciones móviles de Adventure Works y está buscando una producto toolog los detalles acerca de las excepciones, se bloquean y obtener telemetría de rendimiento de una aplicación. HockeyApp puede ayudar en esto a Joann. JoAnn puede integrar ambas HockeyApp para su desarrollador enfocado escenarios y Azure Mobile Engagement para Tim en Hola Hola de tooget de aplicación mismo lo mejor de ambos. 
3. Round Robin forma parte Hola del equipo de desarrollo de aplicaciones móviles de hello en red de noticias de Contoso y todos los que desea es toosend out importantes a los usuarios el tooall de alertas de noticias sin mucho segmentación tan pronto como se desencadene la alerta de noticias de Hola. Para eso, a Robin le pueden resultar útiles los Centros de notificaciones. 
   En este escenario, es posible sin embargo que ya ha evolucionado aplicación móvil de hello, hay un requisito toodo detalles de segmentación y get mucho más completo acerca del comportamiento del usuario de aplicación Hola. En este momento, Round Robin tendrá tooevaluate Azure Mobile Engagement. 

toorecap, propósito Hola de Mobile Engagement no es simplemente toocollect análisis; no es "otro producto de análisis de Microsoft". Es acerca del envío de notificaciones de inserción de destino y para los destinatarios, que se recopilan datos de análisis de comportamiento pero foco Hola permanece en el envío de notificaciones de inserción que Hola mayoría de los usuarios de aplicación de toohello de sentido para que no ha transmitidas como correo no deseado. 

Para obtener más detalles, eche un vistazo a este [corto vídeo](mobile-engagement-overview.md) donde se resume Mobile Engagement. 

