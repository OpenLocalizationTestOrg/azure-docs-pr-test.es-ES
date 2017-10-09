---
title: "Interfaz de usuario de Mobile Engagement - aaaAzure de alcanzar la campaña"
description: "Laern cómo toocreate y administrar las campañas de notificación de inserción con Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a>¿Cómo toocreate y administrar las campañas de notificación de inserción
Puede usar Hola alcance de la sección de la interfaz de usuario de hello toocreate una nueva campaña de inserción con una fórmula compleja proporcionando toda la información de hello necesita toosend una notificación de inserción. Hello opciones de una campaña de inserción varían ligeramente dependiendo de los tipos de campaña Hola cuatro: anuncios, sondeos, inserta datos e iconos (solo Windows Phone).

### <a name="option-applies-to"></a>La opción se aplica a:
* Idiomas: todo (anuncios, sondeos, inserciones de datos, iconos).
* Campaña: todo (anuncios, sondeos, inserciones de datos, iconos).
* Notificación: anuncios y sondeos.
* Contenido: único para cada tipo de campaña.
* Público: todo (anuncios, sondeos, inserciones de datos, iconos).
* Período de tiempo: anuncios, sondeos, iconos.
* Prueba: todo (anuncios, sondeos, inserciones de datos, mosaicos).

![Reach-Campaign1][20]

## <a name="languages"></a>Idiomas
Puede usar Hola idiomas desplegable menú toosend una versión diferente de su toodevices de inserción que se establecen toouse diferentes idiomas. De forma predeterminada, todos los dispositivos recibirán Hola mismo Push independientemente del lenguaje en que se establecen toouse. Los usuarios con su dispositivo conjunto tooa otro idioma recibirán la versión de idioma predeterminado de Hola de hello inserción. Muchas de las opciones de campaña de inserción de hello permiten contenido alternativo toospecify para cada idioma adicional de Hola que seleccione. 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a>Las diferencias de los idiomas se aplican a:
* Idiomas: Idiomas únicos pueden seleccionarse en el idioma predeterminado de suma toohello
* Campaña: igual para todos los idiomas.
* Notificación: Único para cada idioma además toohello idioma predeterminado
* Contenido: Único para cada idioma además toohello idioma predeterminado
* Audiencia: se puede filtrar por un criterio de idioma independiente.
* Período de tiempo: igual para todos los idiomas.
* Prueba: Se pueden enviar tooeach idioma a la vez

### <a name="supported-languages"></a>Idiomas admitidos
* Árabe (ar) 
* Búlgaro (bg) 
* Catalán (ca) 
* Chino (zh) 
* Croata (hr) 
* Checo (cs) 
* Danés (da) 
* Neerlandés (Países Bajos) 
* Español (es) 
* Finés (fi) 
* Francés (fr) 
* Alemán (de) 
* Griego (el) 
* Hebreo (he) 
* Hindi (hi) 
* Húngaro (hu) 
* Indonesio (id) 
* Italiano (it) 
* Japonés (ja) 
* Coreano (ko) 
* Letón (lv) 
* Lituano (lt) 
* Malayo (macroidioma) (ms) 
* Noruego Bokmål (nb) 
* Polaco (pl) 
* Portugués (pt) 
* Rumano (ro) 
* Ruso (ru) 
* Serbio (sr) 
* Eslovaco (sk) 
* Esloveno (sl) 
* Español (es) 
* Sueco (sv) 
* Tagalo (tl) 
* Tailandés (th) 
* Turco (tr) 
* Ucraniano (uk) 
* Vietnamita (vi) 

## <a name="campaign"></a>Campaña
Puede usar Hola campaña sección tooset Hola nombre y la categoría de la campaña, así como si planea tooignore sección de audiencia Hola de una campaña de inserción y enviar esta campaña a través de la API de cobertura de hello (y algunos elementos de nivel bajo de hello inserción API) en su lugar. Categorías pueden utilizarse con una notificación personalizada plantilla toocontrol en la aplicación las notificaciones basadas en configuraciones predefinidas. Puede obtener una lista de las "categorías" existentes a través de la API de cobertura de Hola.

> [!WARNING]
> Si utiliza opción de "Omitir audiencia, dejarán de enviarse toousers a través de la API de Hola" hello en hello "Campaña" sección de una campaña de cobertura, campaña de hello no enviará automáticamente, deberá toosend esta manualmente a través de la API de cobertura de Hola.

![Reach-Campaign3][22]

### <a name="option-applies-to"></a>La opción se aplica a:
* Nombre: todo.
* Categoría: anuncios, sondeos.
* Omitir audiencia, dejarán de enviarse toousers a través de la API de hello: todos los

## <a name="notification"></a>Notificación
Puede usar la configuración básica de hello notificación sección tooset la inclusión de inserción: Hola título de hello inserción, mensajes de bienvenida, una imagen de la aplicación, o si se pueden pasar por alto. Muchas opciones de notificación son toohello específico de la plataforma del dispositivo. Puede seleccionar si desea enviar la inserción "en la aplicación", "fuera de la aplicación" o a ambas ubicaciones. (Recuerde que los usuarios pueden "participación en" o "rechazar" de "fuera de la aplicación" inserta en el sistema operativo de hello nivel en sus dispositivos y Azure Mobile Engagement no ser capaz de toooverride esta configuración. Recuerde también que controla la API de Reach Hola "en la aplicación" y "fuera de la aplicación" inserta. Hola API de inserción puede ser usado toohandle "salir del modo de aplicación" inserta demasiado.) Inserciones pueden personalizarse con imágenes o contenido HTML, incluidos los vínculos profundos para vincular fuera de la ubicación de la aplicación o tooanother en la aplicación (Android SDK 2.1.0 o posterior categorías intención necesarios). Puede cambiar el distintivo de icono o iOS hello y enviar contenido web o de texto (un elemento emergente con html, dirección URL vínculo tooanother ubicación del contenido dentro o fuera de la aplicación hello). También puede hacer sonar dispositivos Android o Vibrar con hello inserción. (Recuerde que se necesita Hola correcto permisos de SDK en sus Android tooring del archivo de manifiesto o vibran un dispositivo). Actualmente no hay ningún estándar del sector para tamaños de Android de "Imagen grande", puesto que los tamaños de pantalla son diferentes en cada dispositivo, pero las imágenes de 400 x 100 funcionan en casi cualquier tamaño de pantalla.

### <a name="delivery-types"></a>Tipos de entrega:
* Fuera de la aplicación solo: notificación de Hola se entregarán al usuario de hello no usa la aplicación hello.
* Hola fuera de la notificación de la aplicación sólo requiere un certificado de Apple o Google (certificado APNS o GCM).
* En la aplicación solo: notificación de hello aparece sólo cuando se ejecuta aplicación hello.
* notificación de Hello usa hello Capptain entrega tooreach Hola de usuario del sistema. Puede personalizar completamente Hola diseño/presentación visual de la inserción.
* En cualquier momento: Esta opción garantiza que se envía una notificación de la aplicación hello está ejecutando o no.

![Reach-Campaign4][23]

### <a name="option-applies-to"></a>La opción se aplica a:
* Notificación: anuncios y sondeos.

## <a name="content"></a>Contenido
Puede usar el contenido de Hola de toomodify Hola sección de contenido de los anuncios, sondeos, inserta datos e iconos (solo Windows Phone). configuración de contenido de Hola de las campañas de inserción es toohello específicos de tipo de campaña. 

### <a name="see-also"></a>Otras referencias
* [Documentación de la interfaz de usuario - Cobertura - Insertar contenido][Link 29]

![Reach-Campaign5][24]

## <a name="audience"></a>Público
Puede usar Hola audiencia sección toodefine una lista estándar de elementos toolimit su campaña o los límites de la campaña en función de criterios personalizados. conjunto estándar de Hola de opciones tooLimit la audiencia permite toopush tooeither nuevo o antiguo usuarios o solamente los usuarios de la inserción nativa. También puede establecer un número de hello toolimit de cuota de usuarios que reciben la inserción de Hola. Puede editar manualmente expresión Hola de cómo la campaña es tooinclude filtrado uno o varios usuarios de tootarget de criterio. Manualmente puede escribir una expresión de audiencia. Este tipo de expresión debe definir explícitamente relación Hola entre los criterios. Un criterio se describe mediante un identificador que debe comenzar con una letra mayúscula y no puede contener espacios. relación de Hello entre los criterios de Hola se puede describir mediante 'and', 'or', 'not' operadores, así como '(',')'. Ejemplo: "Criterio1 o (Criterio1 y no Criterio2)".

> [!NOTE]
> Con una amplia audiencia incluida en las campañas, servidor hello examen de destino puede ser lento, especialmente si se trata de toostart varias campañas en Hola mismo tiempo.

* Si es posible, inicie una sola campaña de cada vez.
* En Hola más, sólo inicio cuatro campañas a la vez.
* Solo los usuarios activos tooyour de inserción (casilla "usar solo los usuarios que se pueden alcanzar con inserción nativa" y "Captar solo usuarios activos") para que solo los usuarios que todavía tienen instalada la aplicación de Hola y usarla deberá toobe analizado.
  Una vez que se ha definido la audiencia, puede usar hello simular botón toofind out cuántos usuarios recibirán esta inserción. Esto calculará el número de Hola de usuarios conocidos potencialmente objetivo de esta audiencia (esta es una estimación basada en una muestra aleatoria de usuarios). Tenga en cuenta que los usuarios que hayan desinstalado la aplicación hello también forman parte de esta audiencia, pero no se puede alcanzar.

### <a name="see-also"></a>Otras referencias
* [Documentación de la interfaz de usuario - Cobertura - Nuevo criterio de inserción][Link 28]

![Reach-Campaign6][25]

### <a name="edit-expression"></a>Editar expresión
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a>Limitar la opción de audiencia se aplica a:
* Captar solo un subconjunto de usuarios: todo (anuncios, sondeos, inserciones de datos, iconos).
* Captar solo usuarios antiguos: todo (anuncios, sondeos, inserciones de datos, iconos).
* Captar solo usuarios nuevos: todo (anuncios, sondeos, inserciones de datos, iconos).
* Captar solo usuarios en espera: anuncios, sondeos, iconos.
* Captar solo usuarios activos: todo (anuncios, sondeos, inserciones de datos, iconos).
* Captar solo a los usuarios con los que se puede contactar usando la inserción nativa: anuncios, sondeos.

## <a name="time-frame"></a>Período de tiempo
Puede usar tooset de sección de período de tiempo de hello cuando Hola dejarán de enviarse o puede dejar campaña de hello período de tiempo en blanco toostart Hola inmediatamente. Recuerde que utilizando la zona horaria de usuarios finales de hello puede comienzan campaña Hola un día antes de lo que puede esperar de los usuarios finales en Asia y enviar lotes pequeños de inserciones en uno hasta que todas las zonas horarias en hello world coincidencia Hola período establecido para la campaña. Uso de zona horaria de los usuarios de finales de hello también puede provocar retrasos en las campañas porque tiene tiempo de hello toorequest de teléfono de hello antes de iniciar la inserción de Hola.

> [!NOTE]
> Sin una fecha de finalización puede almacenar en caché de campañas inserciones localmente y todavía mostrarlos después de completar manualmente las campañas. tooavoid este comportamiento, específica de una hora de finalización de las campañas.

### <a name="see-also"></a>Otras referencias
* [Cobertura - Guía práctica - Programación][Link 3] 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a>La configuración se aplica a:
* Período de tiempo: anuncios, sondeos, iconos.

## <a name="test"></a>Prueba
Puede usar Hola prueba sección toosend este dispositivo de prueba propias de inserción tooyour antes de guardar la campaña Hola. Si ha configurado ningún lenguaje personalizado para esta campaña, puede probar la inserción de hello en cada idioma. Puede configurar un dispositivo de prueba desde "Mi cuenta".

> [!NOTE]
> Inserta ningún servidor datos se registran cuando se usa el botón de hello demasiado "test", solo los datos se registran para las campañas de inserción real.

### <a name="see-also"></a>Otras referencias
* [Documentación de la interfaz de usuario - Mi cuenta][Link 14]

![Reach-Campaign9][28]

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

