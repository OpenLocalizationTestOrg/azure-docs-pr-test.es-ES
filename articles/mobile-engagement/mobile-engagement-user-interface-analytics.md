---
title: "Interfaz de usuario de Mobile Engagement - aaaAzure de análisis"
description: "Obtenga información acerca de cómo tooanalyze los datos históricos sobre su aplicación con Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4a9df11226fed6710cfb1337ae84ece7596d482f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooanalyze-historical-data-about-your-application"></a>¿Cómo tooanalyze datos históricos acerca de la aplicación
Este artículo describe hello **análisis** ficha de hello **Mobile Engagement** portal. Usar hello **Mobile Engagement** toomonitor portal y administrar aplicaciones móviles. Tenga en cuenta que toostart mediante portal Hola primero debe toocreate una **Azure Mobile Engagement** cuenta.

sección de análisis de la interfaz de usuario de Hola Hola proporciona información agregada sobre la aplicación basada en datos históricos que se actualizan cada 24 horas. se muestra información de Hello en paneles diferentes que se compone de mapas, cuadrículas y gráficos de línea/subgráfico. datos de Hello también pueden descargarse como archivos .csv. La mayor parte de esta misma información está disponible en tiempo real en hello sección Monitor de interfaz de usuario de Hola y también son accesibles desde Hola API de análisis.

> [!NOTE]
> Muchas de las secciones de hello **Mobile Engagement** portal de interfaz de usuario contienen hello **ayuda para mostrar** botón. Presione este botón tooget más información contextual sobre una sección.

## <a name="standard-and-custom-analytics"></a>Análisis estándar y personalizado
Azure Mobile Engagement proporciona un conjunto de información analítica básico, estándar acerca de las aplicaciones que se puede representar gráficamente tan pronto como se integre su aplicación con hello SDK. Azure Mobile Engagement también proporciona Hola capacidad toogather análisis personalizada adicional información que desee acerca del comportamiento de sus usuarios finales. Puede hacerlo creando un plan de "etiquetas de información de aplicación" personalizado, creado desde **Configuración** , para que Azure Mobile Engagement pueda recopilar estos datos adicionales por usted.

## <a name="analytics"></a>Análisis
* Panel: muestra información general acerca de los usuarios nuevos y activos y de sus tendencias.
* Usuarios: los usuarios se identifican mediante su identificador de dispositivo: este identificador es único para cada dispositivo (un nuevo usuario es realmente un dispositivo nuevo). Un usuario se considera como nuevo en un intervalo de tiempo determinado si ha realizado su primera sesión durante este intervalo de tiempo. Un usuario se considera retenido si ha realizado al menos una sesión durante Hola últimos 7 días. Los usuarios activos son usuarios que realizaron al menos una sesión durante un período determinado. Puede ordenar por mes, semana, día u hora. Todos los gráficos de hello son similares pero permiten toofilter por diversas características, como la versión de hello de la aplicación y, a continuación, toosort por un período de tiempo. Hello estándar información recopilada mediante la integración de hello SDK incluye siguiente de hello: los usuarios activos, nuevo usuario, número de sesiones, longitud de cada sesión, la información técnica acerca de país de hello, variables locales, ubicación, operador de lenguaje, dispositivos, firmware, red (Wi-Fi), versiones de la aplicación hello y SDK, utilizada por los clientes. Esta información puede verse en tiempo real desde la sección de monitor de Hola.

> [!NOTE]
> Hola período de tiempo se basa en fecha hello de la configuración de dispositivo de los usuarios de hello, para que un usuario cuyo teléfono tiene fecha Hola establecido incorrectamente podría aparecer en hello incorrecto período de tiempo.

* Retención: un usuario se considera como retenido en un intervalo de tiempo determinado si ha realizado su primera sesión durante este intervalo de tiempo. Puede cambiar los intervalos de tiempo de Hola durante los que se cuentan los usuarios retenidos (y los usuarios nuevos) toohours, días, semanas o meses. análisis de retención del usuario de Hola se basa en las cohortes. Un grupo de edad es conjunto Hola de todos los usuarios nuevos de hello detectado durante un período determinado (es decir, el conjunto de Hola de los usuarios que realizan su primera sesión durante este periodo). Utilizamos las cohortes de 1 día, 2 días, 4 días, 7 días o 1 mes. Dado un conjunto cohortes, cada 7 días 1 día, 2 días, 4 días o 1 mes, Azure Mobile Engagement calcula Hola de todos los usuarios que pertenecen toohello cohortes y se sigue activa (es decir, el conjunto de Hola de usuarios que ha realizado al menos una sesión durante el período de hello). Este conjunto de usuarios se denomina versión de la cohorte. (Azure Mobile Engagement puede mostrar cuántos de los usuarios todavía siguen usando la aplicación, pero el almacén específico de plataforma Hola solo puede indicar cuántos de los usuarios desinstalan el iTunes de aplicación: por ejemplo, GooglePlay, tienda de Windows, etcetera.).
* Sesiones: Uno de los usos de la aplicación hello por un usuario. Las sesiones se generan a partir de secuencia de Hola de las actividades realizadas por los usuarios (una actividad es el uso de toohello suelen estar asociados de una pantalla de la aplicación hello, pero esto puede variar dependiendo de Hola Hola de manera SDK se ha integrado en la aplicación hello). Un usuario sólo puede realizar una actividad a la vez: inicia una sesión como usuario Hola su primera actividad inicia y se detiene cuando acabe su última actividad. Si un usuario permanece más de unos pocos segundos sin realizar ninguna actividad, su secuencia de actividades se divide en dos sesiones distintas.
* Actividades: nombres de Hola de cada pantalla de la aplicación y la longitud de Hola de tiempo que los usuarios dedican en cada pantalla. Las actividades son una opción de análisis personalizada que corresponderá toohello etiquetas de "información de la aplicación" que ha configurado para su propia aplicación:
* Ruta de acceso de usuario: muestra cómo navegan los usuarios por las actividades de la aplicación (pantallas). Puede mover el nivel de Hola Hola control deslizante tooadjust de detalle. Los nodos azules representan las actividades de la aplicación. El tamaño es proporcional toohello vez que los usuarios le dedicaron. Los nodos blancos representan el inicio y la detención de la sesión. Los nodos rojos representan bloqueos. Los vínculos representan las transiciones entre las actividades de la aplicación (o entre las actividades y los bloqueos). Haga clic en un nodo o un vínculo toodisplay un mensaje con más información acerca de los datos: Hola tiempo invertido en una pantalla concreta, en recuento de Hola de transiciones y el porcentaje de Hola de transiciones de actividad de destino de hello origen actividad toohello. (Un---60%---> B significa que los usuarios que están en la actividad A deja tooactivity B el 60% de tiempo de Hola.) Puede reordenar el gráfico de hello como desee tooclarify; la posición se guarda cada vez que se realiza un cambio. Puede mostrar u ocultar Hola bloqueos toolighten Hola gráfico.
* Eventos: Acciones específicas realizadas por un usuario en la aplicación hello. distribución de Hola de eventos se muestra como recuento de Hola de eventos por usuario y sesión. Un evento representa una acción instantánea, por ejemplo, al hacer clic en un botón o hello recepción de una notificación. (significado Hola de eventos depende de cómo Hola SDK se ha integrado en la aplicación hello.) Un evento puede producirse durante una sesión o un trabajo o puede ser independiente.
* Trabajos: Tooevents similares excepto que se concentran en longitud Hola de acción de Hola. Por ejemplo, trabajos podrían indicar información técnica sobre el tiempo que tarda tooload contenido o un servicio de tooweb de llamada. También podría mostrar el tiempo que tarda un toofill usuario un formulario, cree una cuenta o realizar una compra. Un trabajo representa Hola duración de una tarea, para un encabezado de tiempo de ejemplo, la duración de Hola de una tarea de descarga u Hola se muestra en la pantalla de bienvenida. (significado Hola de trabajos depende de cómo Hola SDK se ha integrado en la aplicación hello.) Los trabajos se suelen estar asociados a tareas en segundo plano que se realizan fuera de ámbito de Hola de una sesión (es decir, sin ninguna actividad de usuario).
* Technicals: Obtener información técnica acerca de los dispositivos de Hola de usuarios de saludo de la aplicación que puede realizar un seguimiento, como tamaño de configuración regional, operador, red, dispositivos, Firmware y pantalla de dispositivos de los usuarios de Hola Hola y Hola versión de la aplicación y Hola versión SDK utilizada en la aplicación.
* Errores: Información sobre los errores técnicos dentro de la aplicación hello que no producen Hola toocrash de aplicación. Un error es un problema de instantáneo, por ejemplo, un error de red o una manipulación incorrecta. (significado Hola de eventos depende de cómo Hola SDK se ha integrado en la aplicación hello.) Un error puede producirse durante una sesión o un trabajo o puede ser independiente.
* Bloqueos: Información sobre los errores que provocan la toocrash de aplicación. Un bloqueo es una condición inesperada que la aplicación hello deja de realizar sus funciones y debe detenerse. Un bloqueo suele ser debido a errores de tooa en la aplicación hello.

![Analytics2][11]

## <a name="accessing-hello-retention-overview"></a>Hola al acceder a información general de retención
![Analytics3][12]

información general de retención de Hola se desglosa en medio de hello en varias tarjetas, cada introducción de Hola de que se muestra durante un determinado período de retención. período de retención de 2 días de Hola se muestra en el ejemplo de Hola. Hola otras tarjetas mostrar hello 4 días y períodos de retención de 7 días.

## <a name="understanding-hello-retention-overview-cards"></a>Descripción de las tarjetas de información general de retención de Hola
![Analytics4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a>Cada tarjeta se compone de tres partes principales:
1. 1: cohortes de Hola y el período de hello consideran
2. 2-4: Hola retención de hello período actual
3. 5: un minigráfico de historial de Hola

### <a name="here-is-detailed-information-about-each-element"></a>Aquí se detalla información sobre cada elemento:
1. Grupo de edad y período: este encabezado proporciona el tipo de hello del mismo grupo de edad. Aquí "período de 2 días" significa que veremos comportamiento Hola de usuarios más de 2 días, los usuarios que han llegado durante un período de 2 días y si se conectan en hello después de bloques de 2 días. ejemplo de Hola anterior considera que la actividad de hello de usuarios entre Hola 21 y 22 de noviembre.
2. Esto da como resultado Hola retención tasa sobre Hola 21 y 22 de noviembre para los usuarios de Hola que llegan en 19 y 20 de noviembre. Aquí hemos tenido 1 usuario activo entre Hola 21 y 22, sobre Hola 3 que eran nuevos usuarios entre Hola 19 y 20.
3. Este proporciona de indicador visual hello misma información que anteriormente se representa gráficamente. (hello en tercer lugar de hello círculo es de número de un 33% de Hola.) color de Hello proporciona información adicional: verde indica que este número aumenta de cálculo anterior Hola. El color amarillo significa estable, y el rojo significa decreciente.
4. Esto indica los valores de hello utilizados para el cálculo de Hola.
5. Se trata de un minigráfico de historial de Hola de los valores de retención de Hola. Le permite valores de hello toosee en Hola más allá de toohave una vista amplia de cómo evolucionó.

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
