---
title: Interfaz de usuario de Mobile Engagement - aaaAzure de segmentos
description: "Obtenga información acerca de cómo toocreate y administran segmentos de patrones de uso de los usuarios tooidentify con Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a>¿Cómo toocreate y administran segmentos de patrones de uso de los usuarios tooidentify
Este artículo describe hello **segmentos** ficha de hello **Mobile Engagement** portal. Usar hello **Mobile Engagement** toomonitor portal y administrar aplicaciones móviles.

sección de segmentos de Hola de hello interfaz de usuario le permite toowork en la segmentación de los usuarios según un comportamiento diferente Hola y de análisis que puede obtener de la aplicación hello y también puede tener acceso a través de la API de segmentos de Hola. Segmentos se calculan primero 24 horas después de que se crearon y se vuelven a calcular cada 24 horas en función de la información de análisis más reciente de Hola. Una vez que se calcula un segmento, muestra un gráfico de "Historial de tooday día" cada día.

> [!NOTE]
> Muchas de las secciones de hello **Mobile Engagement** portal de interfaz de usuario contienen hello **ayuda para mostrar** botón. Presione este botón tooget más información contextual sobre una sección.
> 
> 

## <a name="create-segments"></a>Crear segmentos
Puede crear un segmento basándose en los criterios de too10 en un período específico días laborables too60 Hola pasado desde la sección de análisis de Hola. Por ejemplo, puede crear un segmento basándose en hello quienes han consultado ciertas páginas o buscar contenido específico dentro de la aplicación dentro de hello últimos 10 días. Esta información está disponible en la sección de análisis de Hola. Por lo tanto, puede usar las expresiones toocreate un segmento y, a continuación, configurar una tootarget de notificación de inserción este subconjunto de usuarios tooget les toocome toohello atrás aplicación. 

> [!NOTE]
> Una vez que se ha calculado un segmento, no se puede editar; solo se puede clonar (copiar) o destruir (eliminar). Se puede clonar un segmento dentro de hello misma aplicación (con Hola AppID mismo), y también se puede clonar en otras aplicaciones (con un AppID diferentes). 

 ![segments1][35] 

## <a name="examples-segments"></a>Segmentos de ejemplo
 ![segments2][36]

Segmentos de permitir que los usuarios finales de toosegment hello de la aplicación.
La segmentación de los usuarios es una estrategia de marketing importante. Azure Mobile Engagement le permite tooget los datos históricos y crear segmentos personalizados. Esta eficaz herramienta le permite toolearn sobre la experiencia de los clientes en la aplicación. Puede analizar fácilmente los segmentos y utilizarlos como destinos de inserción.
Un caso de uso común es que desea toosend una inserción de una notificación tooencourage su toorate de los usuarios finales la aplicación en el almacén de Hola. En lugar de enviar una notificación tooall los usuarios finales, puede crear un segmento que especificaría solo los usuarios que han usado la aplicación cada día para hello último mes y que han tenido un usuario gran experiencia. Cuando se envían menos notificaciones de inserción de mayor grado de orientación, se obtiene una mayor rentabilidad.

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a>Segmentos que se pueden crear en función de los elementos principales de Azure Mobile Engagement de hello:
* Evento: crear un segmento de ese evento específico uno de destinos de la aplicación hello que se produjeron más de dos veces por semana. 
* Sesión: crear un segmento de usuarios que han usado la aplicación hello más de 5 veces la semana pasada.
* Actividad: cree un segmento de los usuarios que hayan utilizado una página o contenido más o menos de 10 horas el último mes.
* Trabajo: cree un segmento de usuarios que ha completado un trabajo más de dos veces al día.
* Bloqueo: crear un segmento de todos los usuarios de Hola que han tenido un bloqueo más de 10 veces la semana pasada. (Puede insertar este segmento con una disculpa o incluso un cupón).
* Error: crear un segmento de todos los usuarios de Hola que han tenido un error más de 100 veces últimos 3 días.
* Información de la aplicación: crear un segmento que tenga como destino una información de aplicación personalizada que se produjo durante el saludo últimos 25 días.
  
  ![segments4][38]

toouse segmento de una forma óptima, debe haber hecho una integración personalizada de hello SDK en la aplicación con un plan de etiquetado de etiquetas "Información de la aplicación".
A continuación, ir a página de inicio de toohello de interfaz de hello, seleccione aplicación de Hola que desee y haga clic en la sección de "Segmentos" Hola.

1. Seleccione la sección de "Segmentos" Hola.
2. Haga clic en "Nuevo segmento" hello botón toocreate un segmento nuevo.

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a>Ejemplo en la vida real: cree un segmento simple basado en la información de "Sesión"
Crear un segmento de todos los usuarios finales de Hola que ha usado la aplicación al menos 50 veces de hello última semana. Desde allí, buscar solo usuarios finales de Hola que han invertido al menos 30 segundos en la aplicación por sesión. Esto mostrará todos los usuarios finales de Hola que tengan una experiencia positiva en la aplicación. A continuación, segmento Hola creado podría ser utilizado toopush un tooask de los usuarios finales de notificación toothese les toorate la aplicación Hola almacenar.

 ![segments5][39]

1. Asigne un nombre de segmento en orden toofind rápidamente en la lista de "Segmento" Hola.
2. Haga clic en hello botón "Crear".
   
   ![segments6][40]

Seleccione la sesión.

 ![segments7][41]

1. Seleccione el período de Hola de "Última semana".
2. Haga clic en Siguiente.
   
   ![segments8][42]
3. Seleccione Hola operador que es relevante en lista de hello: =; ≥, ≤.
4. Escriba Hola número que desea.
5. Seleccione Hola aparición que desee. 
6. Haga clic en Siguiente.
   En este ejemplo se establece para esa over Hola última semana, los usuarios de coincidencia que han realizado al menos 50 sesiones.
   
   ![segments9][43]

Para hello segmentación de sesión, puede elegir longitud Hola por sesión como criterio.

1. Seleccione Hola operador de hello lista.
2. Proporcionar Hola longitud por sesión.
3. Haga clic en Siguiente.
   En este ejemplo, dice que omite todo hello las sesiones que se ha segmentado en la sección de la aparición de hello, seleccione sólo Hola los usuarios que han invertido más de 30 segundos por sesión.
   
   ![segments10][44]

El criterio en tooretrieve pedido en hello completar el nombre de embudo y haga clic en Finalizar.

 ![segments11][45]

Cuando haya terminado de configurar el criterio, aparecerá en el embudo de segmento de Hola.
Dado que los segmentos se basan en un segmento de datos de análisis, los segmentos se calculan una vez al día.
En este ejemplo, 47,7% de los usuarios finales de hello total coincide con el criterio de Hola. Deben ser usuarios de Hola que han tenido una buena experiencia y se pueden tooprovide probablemente una clasificación mayor si se inserta una notificación pedirles toorate aplicación de hello en el almacén de Hola.

## <a name="see-also"></a>Otras referencias
* [Conceptos][Link 6]
* [Guía de solución de problemas de servicios][Link 24]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

