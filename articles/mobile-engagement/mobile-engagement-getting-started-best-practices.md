---
title: aaaAzure Mobile Engagement Getting Started Guide con los procedimientos recomendados
description: "Guía de introducción para Azure Mobile Engagement y prácticas recomendadas para la incorporación"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: dfce1183-6398-466e-aa7e-ed702fb52818
ms.service: mobile-engagement
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: d3f81c34fe74f741a60ca511caa55c312af73b1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---getting-started-guide-with-best-practices"></a>Azure Mobile Engagement - Guía de introducción con prácticas recomendadas
## <a name="overview"></a>Información general
**pantalla de bienvenida móvil es un espacio muy atestado:** en 2013, se encuentra un estudio de dispositivos móviles promedio de hello tenían 27 aplicaciones instaladas. Los usuarios solían pasar normalmente unas 30 horas al mes en sus aplicaciones. La mayor parte de este tiempo se dedicaba a las redes sociales y a los juegos (unas 20 horas). 2014, Hola mercado Android tenía alrededor de 1,5 millones de aplicaciones para toochoose a los usuarios de. tienda de Apple Hola contenía aproximadamente 1,2 millones aplicaciones. El uso de aplicaciones móviles sigue aumentando a medida que los desarrolladores compiten en este mercado en expansión. 

usuario promedio móvil de Hello van a instalar y desinstalar aplicaciones con frecuencia según cambiar intereses y las experiencias de aplicación. Éxito de hello toodetermine de orden de una aplicación resulta vital tooknow más que simplemente cuántos usuarios instalan la aplicación. Es importante tooknow cómo útil es la aplicación y si ese tendencias de uso está cambiando. Hola siguientes preguntas es importante:

* ¿Los usuarios empiezan toofind la aplicación no interesa u obsoleta? 
* ¿Cuántos usuarios han dejado de usar su aplicación? 
* ¿Está la tendencia de adquisición de la aplicación subiendo o bajando?
* ¿No se usuarios superan los flujos de trabajo toocomplete debido a problemas con la aplicación hello o falta de interés? 
* ¿Puede mantener la aplicación relevante y útil mediante la aplicación de usuario de nueva tooyour contenido base? 
* ¿Este contenido nuevo sería Hola igual para todos los usuarios o tiene el foco en segmentos de usuario basados en el comportamiento de la aplicación? 

Respuestas tooquestions similar toothese podría ayudar a prolongar la vida hello y los ingresos de la aplicación. También pueden ayudarle a definir y mantener su base de usuarios. 

Medios relacionados con las aplicaciones suelen toohave algunos de retención máximo de hello entre usuarios. Una razón para esto es que están proporcionando constantemente toousers contenido nuevo. Adopción temprana de las notificaciones de inserción útil dirige el segmento de usuario tooa tiende toohave un gran impacto en la retención de la aplicación. 

programa de Azure Mobile Engagement Hello es toohelp diseñada ampliar la vida de Hola y retención de la aplicación proporcionando un método toogather y analizar información detallada sobre el uso de saludo de la aplicación. Le ayudará a clasificar su base de usuarios según toobehavior y crear campañas tiene el foco para entregar notificaciones de inserción y los mensajes de aplicación tooidentified segmentos de usuarios. Los indicadores clave de rendimiento (KPI) miden la actividad de los usuarios en los distintos aspectos de la aplicación. Azure Mobile Engagement proporciona métodos de hello necesita toodetermine estos KPI. Ayuda a aumentar Hola retorno de la inversión (ROI) al proporcionar la infraestructura de hello necesita tooincrease interacción con la aplicación móvil. 

Hola tooget de orden más fuera de Azure Mobile Engagement, deberá toostart con un plan de contratación bien diseñada. El plan ayudará a identificar deberá toobe puede toosegment el usuario de base de datos pormenorizados Hola. Esto puede basarse en el comportamiento y las experiencias de la aplicación. En orden para su toobe de plan correcta, es un tooclearly de práctica recomendada definir Hola KPI que mida objetivos de saludo de la aplicación. Con indicadores de rendimiento desactive definidos, puede insertar fácilmente lógica necesaria hello en sus toocollect bien específica datos de la aplicación que tendrá que usar tooanalyze y evaluar los KPI. Este tema es una guía de prácticas recomendadas para definir el KPI de Hola que va a utilizar con el plan de contratación. 

## <a name="step-1-define-your-kpis-toofit-hello-bet-model"></a>Paso 1: Definir el modelo de opción de KPI toofit Hola
Definir correctamente los KPI puede ser una tarea difícil toocomplete. Las aplicaciones diseñadas para diferentes sectores tienen sus propias características y objetivos. Esto puede suelen tooconfuse el enfoque. toohelp evitar esto, los objetivos y los KPI debe clasificarse en tres categorías principales: **Business**, **interacción**, y **técnica**. Esto es lo que llamamos hello **modelo PROBABLES**.

Un buen plan puede tener objetivos con los KPI de Hola que miden las operaciones correctas de hello en cada uno de hello siguientes categorías de modelo de opción de Hola.

#### <a name="business-kpis"></a>KPI de negocio
KPI comerciales deben hello más fácil parte toobuild. Probablemente ya los había definido de algún modo al planear su aplicación móvil. Estos KPI ayudan en general a medir los ingresos y la rentabilidad de la inversión de la aplicación. Hello siguiente lista proporciona algunos ejemplos de KPI de negocio que puede orientarse al definir los indicadores de rendimiento:

* KPI de negocio de medios
  * Número de anuncios pulsados
  * Número de visitas de la página por usuario
  * Número de suscripciones actuales
* KPI de negocio de juegos
  * Número de compras de la aplicación
  * Ingreso medio por usuario (ARPU)
  * Tiempo empleado por sesión
  * Días jugados y actuales en el nivel de juego
* KPI de negocio de comercio electrónico
  * Días de uso de la aplicación
  * Ingreso medio por usuario (ARPU)
  * Importe medio en carro de la compra al finalizar la compra
  * Categoría de productos para la mayoría de vistas y compras
* KPI de negocio de bancos y seguros
  * Número de cuentas
  * Características activadas
  * Páginas de oferta visitadas
  * Alertas pulsadas o activadas       

#### <a name="engagement-kpis"></a>KPI de compromiso
Un KPI de contratación es un rendimiento indicador toomeasure Hola la participación de los usuarios. Las tendencias en esta área ayudan a determinar retención hello de la aplicación. Estos son algunos indicadores de rendimiento de ejemplo para este tipo de KPI:

* Usuarios activos en hello últimos 7 días
* Recuento de usuarios inactivos de hello últimos 7 días
* Recuento de usuarios que no se han usado la aplicación hello en 30 días  

Algunos factores externos obvios pueden influir en los indicadores en este campo. Por ejemplo, puede considerar un toobe de dispositivos móviles con un usuario en todo momento. Esto puede ser o no verdad. Una aplicación de juegos podría suelen toohave un mayor uso alrededor de las vacaciones cuando un jugador puede que se reproduzca más al trabajo o fuera del centro educativo.   

Bien definida en esta categoría, los KPI le ayudarán a medir la relación de hello entre la aplicación y sus clientes.

#### <a name="technical-kpis"></a>KPI técnicos
Los indicadores de rendimiento de esta categoría le ayudan a determinar si la aplicación se está comportando correctamente, se cuelga o se bloquea. Pueden medir Hola estado de la aplicación y determinar los problemas de facilidad de uso que pueden impedir que los usuarios utilizando la aplicación hello estos indicadores. Información recopilada para esta categoría también podría contener información sobre el rendimiento sería equipos toomarketing relevante. datos de Hello también pudieron ser útiles para solucionar problemas de TI y compatibilidad con los equipos toohelp identificar errores no notificados. 

A continuación se muestran algunos ejemplos de KPI técnicos:

* Recuento e información de excepciones controladas o no controladas 
* Marca de tiempo del último bloqueo
* Último botón pulsado o última página visitada
* Uso de memoria de la aplicación hello
* Velocidad de fotogramas de la aplicación
* Versión del SO Hola aplicación se ejecuta en
* Versión de la aplicación

Definir estos toohelp KPI miden el rendimiento aplicación y detectar posibles errores. Este indicadores deben ayudar a reducir el tiempo de hello que necesita toodeliver una corrección para sus clientes. También pueden ayudar a definir un segmento de usuarios que han tenido problemas específicos. Puede usar que segmentación toocreate campañas toodeliver las notificaciones de usuario con respecto a las revisiones disponibles y posibles toohelp promociones recuperación la satisfacción del cliente. 

#### <a name="playbook-exercise-1-create-your-kpi-dashboard"></a>Ejercicio 1 del cuaderno de estrategias: Creación del panel de KPI
Al definir la estrategia de marketing, los KPI deben presentar una vista para cada uno de los objetivos principales. Deben ser los puntos de datos definida claramente que le permitirá toomonitor información vital toocollect su comportamiento hello y aplicación de usuario final de Hola.

Crear un panel KPI que contiene Hola debajo de información

1. ¿Qué hello KPI para la aplicación hello?
2. ¿Los datos que apunta will utilizo toorepresent cada KPI?
3. ¿Dónde se encuentran estos datos para mi aplicación (es decir, pantalla, configuración, sistema...)?
4. ¿Se puede reproducir una secuencia de compromiso para este KPI?

Puede usar hello **KPI generador** hoja de cálculo en nuestra [la plantilla de Guía multimedia] [ Media Playbook link] para ejemplos e instrucciones.

## <a name="step-2-your-engagement-program"></a>Paso 2: El programa de compromiso
Un gran programa de compromiso de móviles debe considerarse como un componente clave de la aplicación. Sin duda debe incluir un programa Bienvenido excelente que se ejecuta para un usuario durante el saludo primeros días de uso de la aplicación. Esto suele toohave un efecto muy positivo de contratación y retención de la aplicación. Los estudios han demostrado que mayoría Hola de detención de los usuarios mediante un Hola aplicación primeros días después de la instalación. No se desea toostrive toomeet o exceder interés determinante expectativa del cliente al principio mientras usuario Hola todavía se centra en la aplicación. Asegúrese de que presente clave-valor hello y las ventajas de la aplicación tooyour clientes. 

![](./media/mobile-engagement-getting-started-best-practices/unsegmented-push-notifications.png)

Notificaciones de inserción son Hola mejor enfoque tooearly las contrataciones con usuarios de dispositivos móviles. Sin embargo, se debe tener mucho cuidado al segmentar los usuarios para las notificaciones push. Porque si un usuario se siente como si recibiera correo no deseado o notificaciones sin interés, puede tener graves consecuencias. En pocos clics, un usuario puede eliminar la aplicación nunca tooreturn. usuario de Hello debería recibir muy personalizada valor en la aplicación en lugar de spam genérico.

Una vez que los usuarios están comprometidos activamente, a continuación, el programa de interacción puede ayudar a otros aspectos de la aplicación hello.

Por ejemplo, podría configurar una campaña que solicita los usuarios activos toorate la aplicación. Dado que este segmento de usuario es hello más activo y tiene Hola mayoría experiencia con la aplicación, se podría esperar toogive Hola clasificación sean más preciso. Una vez que tenga una clasificación de aplicación alta, puede ayudar a aumentar descarga orgánicas de saludo de la aplicación y reducir los costos de adquisición del cliente nuevo.

#### <a name="engagement-sequence"></a>Secuencia de compromiso
Un programa de compromiso global incluye distintas secuencias de compromiso. Cada secuencia tiene como objetivo tooreach varios objetivos.

###### <a name="life-push-sequence"></a>Secuencia push de ciclo de vida
objetivos de Hola para una secuencia de inserción del vida son diferentes según el ciclo de vida de hello de interacción del usuario de hello con la aplicación hello. Un usuario determinado puede ser nuevo, inactivo o muy activo. En distintas fases del ciclo de vida de una interacción, los usuarios pueden beneficiarse de su contenido nuevo en forma de Hola de toodocumentation sugerencias o vínculos. 

Por ejemplo un nuevo usuario necesita ayudar a obtener tooan orientado a aplicaciones o beneficiarse de un nuevo toohello similar estímulo de usuario después de hello primera vez que inician la aplicación hello...

*"Toohave placer incorporarlo! Recuerde toologin tooget el mes 1 libre! "*

###### <a name="behavioral-push-sequence"></a>Secuencia push de comportamiento
secuencia de inserción de comportamiento de Hello tiene como objetivo uso tooincrease basado en el comportamiento de usuario recopilado para la aplicación hello.  

Por ejemplo, un usuario de una aplicación de fútbol fantasía muy activo podría beneficiarse de está ocupado con hello siguientes a la notificación de inserción...

*"Juan, ¡eres un verdadero hincha del fútbol! Inicie sesión en la sección de la NFL tooour y ganar acceso gratuito toohello SuperBowl!"*

###### <a name="alerting-push-sequence"></a>Secuencia push de alertas
Los usuarios sabrán apreciar las noticias relevantes de sus intereses. Una secuencia push de alertas mejora el compromiso enviando alertas basadas en los intereses que un usuario demuestra tener claramente. Podría tratarse de explícita cuando un usuario selecciona sus propios intereses en aplicación hello. Puede también determinarse implícitamente en función de los datos recopilados durante la interacción del usuario con la aplicación hello.

Por ejemplo, usuario de Hola de una aplicación de comercio electrónico con regularidad puede comprar una marca específica de café que ha capturado con un negocio KPI. Hello alerta siguiente puede mejorar la interacción del usuario con la aplicación hello.

*"Hola Wes, uno de sus marcas favoritas de café estarán en venta 25% Hola primera semana de septiembre de 2015. Le agradecemos como un cliente y deseaba toomake que fuera compatible con".*

###### <a name="rentention-push-sequence"></a>Secuencia push de retención
Esta secuencia objetivos tooretain a los usuarios mediante una toohelp de las campañas de notificación de inserción repetitivos unidad un hábito regular de póngase en contacto con la aplicación hello. Esto puede ayudar a aumentar la retención de aplicación si el usuario de hello disfruta interacciones Hola. 

Por ejemplo, el usuario Hola de una aplicación relacionados de deportes recibe Hola siguientes a la notificación de inserción semanal en función de los equipos favoritos del usuario de hello:

*"Para una toowin posibilidad de 200 puntos, vaya voto si Hola New York Yankees prevalecerá su juego esta semana en Toronto azul Jays!"*

#### <a name="hello-3w-approach"></a>enfoque de Hello 3 w
Controla las secuencias de inserción diferentes Hola le ayudará a ponerse en contacto con los usuarios finales. Sin embargo, todavía necesita toouse Hola 3 w enfoque para personalizar las notificaciones. Hello 3 w enfoque debe abordar que, ¿qué sucede y cuándo de cada notificación. Si responde claramente a estas tres preguntas, sus notificaciones estarán correctamente enfocadas hacia el compromiso.

![](./media/mobile-engagement-getting-started-best-practices/who-what-when.png)

###### <a name="who-hello-user-segment-that-will-receive-messages"></a>Quién: Hola segmento de usuario que recibirá mensajes
Los usuarios de tooyour de notificaciones de inserción se debe considerar un canal de comunicación muy sensibles. Asegúrese de que las notificaciones de hello tienen como objetivo de segmento de usuario de toosend tooa son intereses toohello bien con ámbito de ese segmento de usuario. Una notificación incorrectamente enrutada es toohave es muy probable que un efecto negativo en un usuario. Puede considerar spam a la aplicación tooyour que se están desinstalando. 

Use una combinación de criterios técnicos y de comportamiento específicos al definir los segmentos de usuarios que van a recibir las notificaciones. Un ejemplo sencillo definir un segmento de usuario podría ser similar toohello siguiente instrucción:

"Todos los usuarios que inicien Hola una aplicación móvil para hello primera vez hace tres días y han visitado la página de inicio de sesión de hello dos veces sin completarla realmente un inicio de sesión".

Esa instrucción ayuda a identificar datos Hola necesitaría toocollect toosupport un escenario concreto.

###### <a name="what-hello-message-that-you-will-send"></a>¿Qué: mensaje de Hola que vaya a enviar
**Tono**

En sus compromisos, use un tono que sea adecuado para los usuarios segmentados. Esto es definitivamente un tooconnect buena forma con los usuarios finales y promueva interés de un usuario de la aplicación. 

**Redireccionamiento**

Una notificación de inserción puede usarse para abrir más de una aplicación Hola. Si hello mensaje de notificación proporciona un contexto, como noticias de difusión o la promoción de un producto, este vínculo profundo de mayo de notificación directamente toohello derecha el contenido dentro de la aplicación hello. toosupport esto, debe crear una dirección URL de aplicación de esquema toolet hello administren la redirección de Hola. Cuando trabaja en sus secuencias de compromiso, esto es un paso importante del que no se debe olvidar.

También es posible administrar el redireccionamiento para otros sistemas. Por ejemplo, es posible tooredirect toomany de los usuarios finales con una dirección URL de acción de otros sistemas incluidos Hola siguientes:

* Un sitio web
* Un buzón de correo electrónico con mensajes ya configurados
* Un buzón de SMS
* Un servicio de marcado telefónico
* Directamente toohello tienda de aplicaciones para la aplicación hello de clasificación. 

Esto proporciona numerosas oportunidades de tooengage los usuarios finales y crear las reglas automáticas de rendimiento tooimprove.

**Formato y contenido**

Hay distintos tipos y formatos de notificación push:

1. **Anuncios** : le permite toosend publicidad mensajes toousers en diferentes momentos (fuera de la aplicación, en la aplicación o en cualquier momento).
2. **Sondeos** : habilitado toogather información de los usuarios finales cuando les pregunta preguntas. Las respuestas, a continuación, están disponibles cuando se crean criterios tootarget los usuarios finales.
3. **Inserciones de datos** : le permite toosend un archivo binario o base64 datos archivo tooupdate aplicación hello. información de Hello contenida en una inserción de datos se envía tooyour aplicación toopersonalize Hola experiencia de los usuarios de la aplicación. La aplicación necesita toobe diseñado toosupport Hola datos en una inserción de datos.
4. **Iconos (solo Windows Phone)** : habilitado toouse Hola servicio de notificaciones de inserción de Microsoft (MPNS) toosend notificación de inserción nativa que contiene datos XML (admitidos desde el SDK versión 0.9.0. carga final de Hello en los mosaicos no puede superar los 32 kilobytes.). mensaje de bienvenida aparece directamente en el icono de la placa.
5. **Vista web** : una vista web es una ventana emergente con contenido web. Este elemento emergente aparece cuando se hace clic en para el usuario final de hello en la notificación de inserción de Hola. Una vista web le permite toohave más interacción con el usuario final de Hola.

> [!NOTE]
> Asegúrese de que va a enviar como notificaciones de inserción de contenido de Hola sea compatible con plataforma respectiva hello (iOS, Android, Windows) directrices para el desarrollo de aplicaciones y enviar notificaciones de inserción.
> 
> 

###### <a name="when-hello-timing-of-your-campaign"></a>Cuándo: Hola tiempo de la campaña
¿Cuándo es Hola mejor tiempo tooactivate una campaña desencadenar notificaciones de inserción? ¿Debe ser manual o automática? ¿Debe ser periódica? Determinantes momento oportuno de Hola o frecuencia es esencial tooengage a los usuarios obtener los mejores resultados de Hola. Para cada secuencia de interacciones y escenario, debe especificar cuándo estará Hola mejor tiempo toosend notificaciones de inserción. Estos son algunos ejemplos:

![](./media/mobile-engagement-getting-started-best-practices/campaign-timing-examples.png)

Si va a enviar a diario muchas notificaciones, debe tener en cuenta que los usuarios pueden percibir las comunicaciones como correo no deseado. 

Azure Mobile Engagement proporciona dos maneras de toohelp evitar las comunicaciones que se percibe como correo no deseado. En primer lugar, utilice concretos segmentación tooensure hace Hola de destino no mismos usuarios. Además, Azure Mobile Engagement proporciona una característica de "cuota". Esta característica puede limitar las notificaciones enviadas para una campaña. Por ejemplo, establecer una too5 de cuota predeterminados por semana garantizará que un usuario que se incluye como parte del segmento de usuario de campaña de hello recibe notificaciones de no más de 5 para esa semana.

#### <a name="playbook-exercise-2-create-your-engagement-program"></a>Ejercicio 2 del cuaderno de estrategias: Creación del programa de compromiso
Dedique tiempo resumir los objetivos y la definición de las campañas de hello espera tooplay mediante secuencias específicas. Asegúrese de que las notificaciones de hello 3 w enfoque toohello se aplican en sus campañas. 

Hola de uso **programa interacción** hoja de cálculo de hello [la plantilla de Guía multimedia] [ Media Playbook link] para obtener ejemplos e instrucciones.

## <a name="step-3-app-integration"></a>Paso 3: Integración de la aplicación
#### <a name="create-a-tag-plan"></a>Creación de un plan de etiquetas
toointegrate Azure Mobile Engagement en la aplicación necesitará toocreate un plan de etiqueta. plan de etiqueta de Hello es pilares de hello del proyecto de Hola. Define la relación de hello entre las especificaciones de marketing, flujo de trabajo de Hola de aplicación hello y los datos de etiqueta real Hola recopilados en toomeasure de aplicación Hola KPI. Indica qué análisis, podrá toosee en el portal de Hola. También ayuda a definir segmentos de usuarios y enviar tooengage de notificaciones de inserción tiene el foco de los usuarios finales. Una vez que tenga el plan de la etiqueta de hello definido, agregar toointegrate de código de hello en su aplicación es sencillo con hello Azure Mobile Engagement SDK.

Un plan de etiquetas no debe etiquetarlo todo en una aplicación. Solo debe incluir los datos de etiquetas que forman parte de su estrategia de Mobile Engagement. Esto probablemente variará de una aplicación a otra. Hola [la plantilla de Guía multimedia] [ Media Playbook link] proporcionado por Azure Mobile Engagement le ayuda a crear un plan de etiqueta con un método determinado. Hola de uso **etiqueta Plan** previsto de la etiqueta de hoja de cálculo como un toobuilding de guía.

Al definir una sección de etiqueta en la hoja de cálculo de hello, ser muy específico. Esto es muy importante tooavoid confusión. Proporcione detalles de cada escenario esperado en el que se enviará cada etiqueta. Incluir nombre de Hola de actividad de hello donde se incrusta cada etiqueta. Esto todos se debe incluir en hello **Informative** forma parte de la hoja de cálculo de Hola. hoja de cálculo de Hello etiqueta plan debe ser referencia principal de hello para la comprobación de la prueba. 

Hola **toocollect datos** sección, el equipo de desarrollo debe buscar tipos de hello, los nombres, valores y pares de clave/valor de información adicional necesarias para cada etiqueta que se incrustarán en la aplicación hello.

Se recomienda revisar el plan de etiqueta de Hola a todos los equipos asociados con el proyecto de Hola. Realice las correcciones necesarias y confirme que todo está claro para los equipos de desarrollo y marketing.

Hola **instrucción de trabajo** hoja de cálculo puede ser guía toohelp usado todos los usuarios implicados en el proyecto de Hola.

#### <a name="data-types"></a>Tipo de datos
Estos son los tipos comunes de datos compatibles con Azure Mobile Engagement.

###### <a name="devices-and-users"></a>Dispositivos y usuarios
Azure Mobile Engagement identifica a los usuarios mediante la generación de un identificador único para cada dispositivo. Este identificador se denomina identificador de dispositivo de hello (o deviceid). Se genera de forma que todas las aplicaciones que se ejecutan en ese mismo recurso compartido de dispositivo Hola mismo identificador de dispositivo.

###### <a name="sessions-and-activities"></a>Sesiones y actividades
Una sesión es una instancia de la aplicación hello siendo ejecutado por un usuario. sesión de Hello abarca de tiempo de hello usuario Hola inicia la aplicación hello, hasta que se detiene.

Una actividad es una agrupación lógica de un conjunto de cosas que puede hacer la aplicación hello durante una sesión. Suele ser una pantalla determinada en la aplicación hello, pero puede ser que cualquier cosa definidas por lógica de Hola de aplicación hello. Como mínimo, debe etiquetar cada pantalla o actividad de la aplicación. Esto le permitirá toounderstand Hola usuario-ruta de acceso.

###### <a name="events"></a>Eventos
Los eventos son tooreport usado interacción del usuario con la aplicación hello. Pueden ser acciones instantáneas, como compartir contenido o iniciar un vídeo. Etiquetado de eventos le proporcionará las colecciones de datos que muestran cómo los usuarios interactúan con la aplicación hello. 

###### <a name="jobs"></a>Trabajos
Trabajos son acciones tooreport usadas que tienen una duración. Algunos ejemplos pueden incluir:

* Ejecución de llamadas a la API
* Tiempo de visualización de anuncios
* Duración de tareas en segundo plano 
* Duración del proceso de compra
* Reproducción de un vídeo

###### <a name="errors"></a>Errors
Los errores son problemas detectados por la aplicación hello de tooreport usado. Por ejemplo, acciones de usuario incorrectas o errores de llamadas a la API.

###### <a name="application-information"></a>Información de la aplicación
Se utiliza la información de la aplicación (App-Info) tootag datos relacionados con la experiencia de usuario de tooa con una aplicación. Se genera mediante la interacción del usuario con la aplicación hello. 

Para una clave determinada de información de la aplicación, Azure Mobile Engagement solo realiza un seguimiento de valor más reciente de hello (ningún historial). App-info revela estado de saludo de la aplicación o los usuarios finales. Por ejemplo el estado de inicio de sesión de Hola o el grupo de producto favoritos de un usuario.

###### <a name="crash-data"></a>Datos de bloqueo
Bloqueo de datos recopilados automáticamente por errores de aplicación Hola SDK de Mobile Engagement informes no controlados por la aplicación hello. Por ejemplo, una excepción no controlada que se produzca.

###### <a name="extra-data"></a>Datos adicionales
Los eventos, errores, actividades y trabajos se pueden mejorar mediante parámetros. Se trata de un desarrollador puede proporcionar como datos específicos de la aplicación hello de información adicional. Esto es importante para definir una segmentación específica. 

Por ejemplo, valor de Hola de una etiqueta "artículo" le permitirá toosegment los usuarios finales en función de quién ve ese artículo determinado. Sin embargo, quizás no sea suficiente. Sería mejor si esa misma etiqueta "article" incluyera también información adicional, como "news_category" dentro de una actividad. Esto resultaría útil toodetermine dinámicamente Hola categorías favoritas para usuario Hola. 

La información adicional se notifica como par clave/valor. En el ejemplo de Hola para esta aplicación de medios, información adicional de Hola para "news_category" sería valor Hola para esa categoría. Por ejemplo, "deporte", "economía" o "política".

#### <a name="tag-and-sdk-integration"></a>Etiquetas e integración de SDK
Para obtener instrucciones paso a paso para la integración de hello Azure Mobile Engagement SDK en la aplicación, siga hello [integración con el SDK interacción](mobile-engagement-windows-store-integrate-engagement.md) documentación en el sitio Web de Azure. Elija la plataforma de destino de vínculos de hello en parte superior de Hola de esa página.

Se recomienda crear proyectos para las dos aplicaciones creadas por encima de Azure Mobile Engagement. Uno para hello otro para el almacenamiento provisional de producción y ensayo de prueba y desarrollo. Su equipo de TI, a continuación, puede promover de prueba tooproduction de almacenamiento provisional cuando la prueba de aceptación de usuario de hello es correcta.

#### <a name="user-acceptance-testing-uat"></a>Pruebas de aceptación por el usuario (UAT)
Las pruebas de aceptación por el usuario (UAT) implican asegurarse de que todo funciona tal como se diseñó. Los flujos de trabajo pueden realizarse y recopilar todos los datos necesarios en función de su plan de etiquetas:

* Etiquetado de información debe aplicarse en según toodocumented conceptos AZME
* Se recopila toda la información que necesita (incluidos el valor de información adicional, el valor de información de la aplicación).
* Nomenclatura coincide con tooyout correspondiente Plan de etiqueta
* No hay etiquetas duplicadas enviadas.

Probar exhaustivamente todos los tipos de Hola de comportamiento de las notificaciones que se han incrustado en la aplicación

* Anuncios, sondeos, inserciones de datos fuera de la aplicación y en la aplicación
* Vistas web y de texto
* Actualización de notificaciones y categorías

#### <a name="setup"></a>Configuración
La configuración de Azure Mobile Engagement es muy sencilla. Toda la documentación de hello relacionados con la interfaz de usuario de toohello está disponible en el sitio Web de Azure Mobile Engagement hello, [cómo toonavigate Hola interfaz de usuario](mobile-engagement-user-interface-home.md).

Se recomienda que primero debe configurar los roles adecuados de Hola y pertenencias a roles para los usuarios de hello del proyecto. Esto ayuda a administrar el acceso adecuado toohello plataforma para todos los usuarios. Los roles pueden incluir:

* Administradores
* Desarrolladores
* Lectores 

Posteriormente:

* Registrar su tootest de Id. de dispositivo en el propio dispositivo.
* Ir toohello configuración de la cuenta y configurar gráficos de toohave de zona horaria de Hola y la hora de entrega de notificación establecida con su zona horaria.
* Vaya toohello configuración de la aplicación y registrar Hola "App-info" necesita tootarget por el usuario final a su alcance.

Para obtener más información sobre cómo toorun la primera inserción campaña de notificación, revisión [cómo tooget a usar y administrar inserta tooreach a los usuarios finales de tooyour](mobile-engagement-how-tos.md).

## <a name="conclusion"></a>Conclusión
Los programas de compromiso son iterativos y debe mejorarlos continuamente según vaya sabiendo lo que funciona mejor para su aplicación. 

Inicialmente, al desarrollar experiencia con interacción estrategias no intente toobuild una estrategia de contratación global completa. Adoptar un enfoque de paso a paso la identificación de los KPI y cómo tooleverage ellos. La estrategia de contratación será única para cada aplicación.

Una vez haya desarrollado cierta experiencia que podría agregar Hola siguientes tooyour interacción programas:

* Seguimiento: adquiere usuarios y probablemente defina orígenes de recopilación de datos. Interacción móvil Azure puede ser orígenes de la colección de toodata vinculado. Permite toomonitor prestaciones de cada origen. Esta información será toomaximize interesante su inversión de adquisición. 
* Pruebas A/B: es una parte esencial del programa de compromiso. Cada aplicación tiene sus propias características específicas. Con pruebas A/B, puede mejorar el programa de compromiso.
* Ubicación geográfica: se trata de una gran oportunidad para las marcas. Característica de toothis gracias puede llegar en el momento y lugar derecho Hola. Se recomienda comprobar que recopile suficientes datos de comportamiento del usuario final antes de iniciar toouse ubicación geográfica.
* Inserción de datos: la inserción de datos es una inserción invisible. La inserción de datos permite personalizar la aplicación basándose en el comportamiento de los usuarios finales. Por ejemplo, si un segmento de usuario a menudo consulta productos de vanguardia, propietario de la aplicación hello puede enviar una inserción de datos que se usará para personalizar su página principal con contenido de alta tecnología.

## <a name="next-steps"></a>Pasos siguientes
* [Creación de una cuenta de Azure Mobile Engagement](mobile-engagement-create.md)
* Visite [defina su estrategia de Mobile Engagement](mobile-engagement-define-your-mobile-engagement-strategy.md) toolearn más acerca de cómo definir la estrategia de Mobile Engagement.

<!--Image references-->


<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
