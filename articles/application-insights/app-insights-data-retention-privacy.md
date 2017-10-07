---
title: "aaaData retención y almacenamiento de Azure Application Insights | Documentos de Microsoft"
description: "Declaración de directiva de retención y privacidad"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: a6268811-c8df-42b5-8b1b-1d5a7e94cbca
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: bwren
ms.openlocfilehash: 7823431d03a57db5268d2724a0604e40666009f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-collection-retention-and-storage-in-application-insights"></a>Recopilación, retención y almacenamiento de datos en Application Insights


Al instalar [Azure Application Insights] [ start] SDK en la aplicación, envía la telemetría sobre su toohello de aplicación en la nube. Naturalmente, los desarrolladores responsables desean tooknow exactamente qué datos se envían, lo que sucede toohello datos y cómo puede mantener el control del mismo. En concreto, si se puede enviar información confidencial, dónde se almacena y su nivel de seguridad. 

En primer lugar, respuesta corta hello:

* módulos de telemetría estándar de Hola que se ejecutan "fuera del cuadro de Hola" son servicio toohello de toosend poco probable que los datos confidenciales. telemetría Hola se ocupa de la carga, las métricas de uso y rendimiento, informes de excepción y otros datos de diagnóstico. datos de usuario principal de Hello visibles en los informes de diagnóstico de hello son direcciones URL; pero la aplicación no debe colocar en cualquier caso datos confidenciales en texto sin formato en una dirección URL.
* Puede escribir código que envía toohelp telemetría personalizada adicional, con el uso de la supervisión y diagnóstico. (Esta extensibilidad es una excelente característica de Application Insights.) Sería posible, por error, toowrite este código para que incluya personal y otros datos confidenciales. Si la aplicación funciona con estos datos, debe aplicar un código de hello tooall de procesos de revisión exhaustiva que se escribe.
* Al desarrollar y probar la aplicación, es fácil tooinspect lo que se está enviando Hola SDK. datos de Hello aparecen en hello las ventanas del explorador y Hola IDE de salida de depuración. 
* datos de Hola se mantienen en [Microsoft Azure](http://azure.com) servidores en Estados Unidos de Hola o Europa. (La aplicación puede ejecutarse en cualquier lugar). Azure tiene [procesos de seguridad exhaustivos y satisface un amplio intervalo de estándares de cumplimiento](https://azure.microsoft.com/support/trust-center/). Solo usted y su equipo designado tienen acceso a los datos tooyour. Empleados de Microsoft pueden restringir acceso tooit solo en determinadas circunstancias limitados con su conocimiento. Se cifra en tránsito, aunque no se encuentran en servidores de Hola.

resto de Hola de este artículo detalla se elaboran estas respuestas. Se ha diseñado toobe independiente, por lo que puede mostrar toocolleagues que no forman parte de su equipo inmediato.

## <a name="what-is-application-insights"></a>¿Qué es Application Insights?
[Azure Application Insights] [ start] es un servicio proporcionado por Microsoft que le ayuda a mejorar el rendimiento de Hola y facilidad de uso de la aplicación en vivo. Supervisa la aplicación se está ejecutando, durante las pruebas y después de haber publicado o implementarla todo el tiempo Hola. Visión de la aplicación crea gráficos y tablas que muestran, por ejemplo, qué horas del día en que se obtiene la mayoría de los usuarios, es la aplicación siga respondiendo hello y también que cualquier externo ofrece servicios a los que depende. Si no hay bloqueos, errores o problemas de rendimiento, puede buscar a través de los datos de telemetría de hello en causa de hello toodiagnose de detalle. Y Hola service le enviará mensajes de correo electrónico si hay algún cambio en la disponibilidad de Hola y el rendimiento de la aplicación.

En orden tooget esta funcionalidad, se instala un SDK de visión de la aplicación en la aplicación, que se convierte en parte de su código. Cuando se ejecuta la aplicación, Hola SDK supervisa su funcionamiento y envía el servicio de telemetría toohello Application Insights. Se trata de un servicio en la nube hospedado por [Microsoft Azure](http://azure.com). (No obstante, Application Insights funciona con cualquier aplicación, no solo con las hospedadas en Azure.)

![Hola SDK en la aplicación envía telemetría toohello servicio Application Insights.](./media/app-insights-data-retention-privacy/01-scheme.png)

Hola servicio Application Insights almacena y analiza la telemetría de Hola. análisis de hello toosee o buscar a través de hello almacena telemetría, iniciar sesión en tooyour cuenta de Azure y recursos de hello abrir Application Insights para su aplicación. También puede compartir los datos de access toohello con otros miembros del equipo, o con los suscriptores de Azure especificados.

Puede tener datos exportados de hello servicio Application Insights, por ejemplo tooa tooexternal o base de datos de herramientas. Proporciona todas las herramientas con una clave especial que obtenga del servicio de Hola. clave de Hello puede revocarse si es necesario. 

Hay disponibles SDK de visión de aplicación para una gama de tipos de aplicación: servicios web hospedados en sus propios servidores J2EE o ASP.NET, o en Azure; clientes Web: es decir, se ejecuta en una página web; código de hello aplicaciones de escritorio y los servicios; aplicaciones para dispositivos como Windows Phone, iOS y Android. Enviar telemetría toohello mismo servicio.

## <a name="what-data-does-it-collect"></a>¿Qué datos recopila?
### <a name="how-is-hello-data-is-collected"></a>¿Cómo se datos Hola se recopilan?
Hay tres orígenes de datos:

* Hola SDK, que se integra bien con la aplicación [en desarrollo](app-insights-asp-net.md) o [en tiempo de ejecución](app-insights-monitor-performance-live-website-now.md). Existen distintos SDK para los diferentes tipos de aplicaciones. También hay un [SDK para las páginas web](app-insights-javascript.md), que cargará en el Explorador de saludo del usuario final junto con la página de Hola.
  
  * Cada SDK tiene un número de [módulos](app-insights-configuration-with-applicationinsights-config.md), que utilizan diferentes tipos de toocollect de distintas técnicas de telemetría.
  * Si instala Hola SDK en el desarrollo, puede utilizar su propio telemetría, su toosend API en módulos de suma toohello estándar. Esta telemetría personalizada puede incluir los datos que desea toosend.
* En algunos servidores web, también hay agentes que se ejecutan junto con la aplicación hello y envían telemetría acerca de la CPU, memoria y la ocupación de la red. Por ejemplo, las máquinas virtuales de Azure, los hosts de Docker y los [servidores J2EE](app-insights-java-agent.md) pueden tener dichos agentes.
* [Pruebas de disponibilidad](app-insights-monitor-web-app-availability.md) son procesos que se ejecutan por Microsoft que envían las solicitudes tooyour web app a intervalos regulares. servicio de Application Insights toohello se envían los resultados de Hola.

### <a name="what-kinds-of-data-are-collected"></a>¿Qué tipos de datos se recopilan?
Hola las categorías principales son:

* [Telemetría de servidor web](app-insights-asp-net.md) : solicitudes HTTP.  Identificador URI, solicitud de tiempo que tarda tooprocess hello, código de respuesta, dirección IP del cliente. Identificador de sesión.
* [Páginas web](app-insights-javascript.md) : contadores de sesión, página y usuario. Tiempos de carga de las páginas. Excepciones. Llamadas AJAX.
* Contadores de rendimiento: memoria, CPU, E/S, ocupación de la red.
* Contexto de cliente y servidor: SO, configuración regional, tipo de dispositivo, explorador y resolución de pantalla.
* [Excepciones](app-insights-asp-net-exceptions.md) y bloqueos: **volcados de pila**, identificador de compilación y tipo de CPU. 
* [Dependencias](app-insights-asp-net-dependencies.md) -llama a los servicios de tooexternal como REST, SQL, AJAX. Identificador URI o cadena de conexión, duración, con éxito, comando.
* [Pruebas de disponibilidad](app-insights-monitor-web-app-availability.md) : duración de prueba y pasos, respuestas.
* [Registros de seguimiento](app-insights-asp-net-trace-logs.md) y [telemetría personalizada](app-insights-api-custom-events-metrics.md) - **: todo el código que se escribe en los registros o telemetría**.

[Más detalle](#data-sent-by-application-insights).

## <a name="how-can-i-verify-whats-being-collected"></a>¿Cómo se puede comprobar lo que se recopila?
Si está desarrollando una aplicación Hola con Visual Studio, ejecutar la aplicación hello en modo de depuración (F5). telemetría Hola aparece en la ventana de salida de hello. Desde ahí, puede copiarlos y darles formato como JSON para facilitar su inspección. 

![](./media/app-insights-data-retention-privacy/06-vs.png)

También hay una vista más legible en la ventana de diagnóstico de Hola.

En el caso de las páginas web, abra la ventana de depuración del explorador.

![Presione F12 y abra la ficha de red de Hola.](./media/app-insights-data-retention-privacy/08-browser.png)

### <a name="can-i-write-code-toofilter-hello-telemetry-before-it-is-sent"></a>¿Puedo escribir telemetría de hello toofilter de código antes de enviarlo?
Sí, es posible, solo es preciso escribir un [complemento de procesador de telemetría](app-insights-api-filtering-sampling.md).

## <a name="how-long-is-hello-data-kept"></a>¿Cuánto tiempo son los datos de hello mantiene?
Puntos de datos sin procesar (es decir, los elementos que puede consultar en el análisis e inspeccionar en la búsqueda) se conservan durante los días de too90. Si necesita datos tookeep más largo, puede usar [exportación continua](app-insights-export-telemetry.md) toocopy se tooa cuenta de almacenamiento.

Los datos agregados (es decir, recuentos, promedios y otros datos estadísticos que se ven en el Explorador de métricas) se retienen con un nivel de detalle de un minuto durante 90 días.

## <a name="who-can-access-hello-data"></a>¿Quién puede tener acceso a datos de hello?
datos de Hello están tooyou visible y, si tiene una cuenta de organización, los miembros del equipo. 

Se puede exportar por usted y los miembros del equipo y podría ser copiado tooother ubicaciones y pasa tooother personas.

#### <a name="what-does-microsoft-do-with-hello-information-my-app-sends-tooapplication-insights"></a>¿De qué hace Microsoft con la información de hello Mi aplicación envía visión tooApplication?
Microsoft utiliza los datos de hello solo en orden tooprovide Hola servicio tooyou.

## <a name="where-is-hello-data-held"></a>¿Dónde se mantienen datos Hola?
* En Estados Unidos de Hola o Europa. Puede seleccionar ubicación de hello cuando se crea un nuevo recurso de Application Insights. 


#### <a name="does-that-mean-my-app-has-toobe-hosted-in-hello-usa-or-europe"></a>¿Significa que la aplicación tiene toobe hospedado en hello Estados Unidos o Europa?
* No. La aplicación puede ejecutar desde cualquier lugar, en sus propio hosts local o en hello en la nube.

## <a name="how-secure-is-my-data"></a>¿Están seguros mis datos?
Application Insights es un servicio de Azure. Las directivas de seguridad se describen en hello [notas de seguridad de Azure, privacidad y cumplimiento del](http://go.microsoft.com/fwlink/?linkid=392408).

Hola datos se almacenan en servidores de Microsoft Azure. Para las cuentas en hello Portal de Azure, se describen las restricciones de cuenta en hello [documento de seguridad de Azure, privacidad y cumplimiento](http://go.microsoft.com/fwlink/?linkid=392408).

Acceder a los datos de tooyour personal de Microsoft están restringidos. Se acceder a los datos solo con su permiso y, si es necesario toosupport el uso de Application Insights. 

Datos de agregado en todas las aplicaciones de todos los clientes (por ejemplo, tipos de datos y el tamaño medio de seguimientos) son utilizado tooimprove Application Insights.

#### <a name="could-someone-elses-telemetry-interfere-with-my-application-insights-data"></a>¿Puede interferir la telemetría de otro usuario con mis datos de Application Insights?
Podría enviar cuenta tooyour de telemetría adicionales mediante el uso de clave de instrumentación de hello, que puede encontrarse en el código de hello de las páginas web. Si tienen demasiados datos adicionales, las métricas no representan correctamente el rendimiento y el uso de la aplicación.

Si comparte código con otros proyectos, recuerde tooremove su clave de instrumentación.

## <a name="is-hello-data-encrypted"></a>¿Se cifran datos Hola?
No en servidores de hello en la actualidad.

Todos los datos se cifran al moverse entre centros de datos.

#### <a name="is-hello-data-encrypted-in-transit-from-my-application-tooapplication-insights-servers"></a>¿Se cifren datos Hola durante el tránsito mi tooApplication visión desde servidores de aplicaciones?
Sí, usamos https toosend el portal de toohello de datos desde prácticamente todos los SDK, incluidos servidores web, dispositivos y las páginas web HTTPS. Hola única excepción son los datos enviados desde las páginas de web HTTP sin formato. 

## <a name="personally-identifiable-information"></a>Información de identificación personal
#### <a name="could-personally-identifiable-information-pii-be-sent-tooapplication-insights"></a>¿Información de identificación personal (PII) se pudo enviar visión tooApplication?
Sí, es posible. 

Como regla general:

* La mayor parte de la telemetría estándar (es decir, telemetría enviada sin tener que escribir código) no incluye información de identificación personal explícita. Sin embargo, puede que sea posible tooidentify personas por inferencia a partir de una colección de eventos.
* Los mensajes de excepción y seguimiento pueden incluir información de identificación personal.
* Telemetría personalizada: es decir, llamadas como TrackEvent que se escribe en código mediante los seguimientos de API o de registro de hello - puede contener cualquier dato que elija.

tabla de Hello final Hola de este documento contiene descripciones más detalladas de los datos de hello recopilados.

#### <a name="am-i-responsible-for-complying-with-laws-and-regulations-in-regard-toopii"></a>¿Puedo responsable de su cumplimiento con las leyes y regulaciones en tooPII de tener en cuenta?
Sí. Es el tooensure de responsabilidad Hola recopilación y uso de datos de hello cumple con las leyes y regulaciones y Hola términos de Microsoft Online Services.

Debe informar a los clientes adecuadamente sobre datos Hola que la aplicación recopila y cómo se usan los datos de Hola.

#### <a name="can-my-users-turn-off-application-insights"></a>¿Pueden los usuarios desactivar Application Insights?
No directamente. No proporcionamos un conmutador que los usuarios pueden funcionar tooturn desactivar Application Insights.

Sin embargo, puede implementar esta característica en la aplicación. Hola todos los SDK incluye un valor de la API que desactiva la recopilación de telemetría. 

#### <a name="my-application-is-unintentionally-collecting-sensitive-information-can-application-insights-scrub-this-data-so-it-isnt-retained"></a>Mi aplicación recopila información confidencial de forma involuntaria. ¿Puede Application Insights limpiar estos datos para que no se conserven?
Application Insights no filtra ni elimina los datos. Debe administrar correctamente los datos de Hola y evitar el envío de este tipo tooApplication datos visión.

## <a name="data-sent-by-application-insights"></a>Datos enviados por Application Insights
Hola SDK varía entre plataformas y hay varios componentes que se pueden instalar. (Consulte demasiado[Application Insights - información general sobre][start].) Cada componente envía datos diferentes.

#### <a name="classes-of-data-sent-in-different-scenarios"></a>Clases de datos que se envían en distintos escenarios
| Acción del usuario | Clases de datos recopilados (ver tabla siguiente) |
| --- | --- |
| [Agregar proyecto de web de Application Insights SDK tooa .NET][greenbrown] |ServerContext<br/>Inferidos<br/>Contadores de rendimiento<br/>Solicitudes<br/>**Excepciones**<br/>Sesión<br/>users |
| [Instalar el Monitor de estado en IIS][redfield] |Dependencias<br/>ServerContext<br/>Inferidos<br/>Contadores de rendimiento |
| [Agregar la aplicación web de Application Insights SDK tooa Java][java] |ServerContext<br/>Inferidos<br/>Solicitud<br/>Sesión<br/>users |
| [Agregar página de tooweb de SDK de JavaScript][client] |ClientContext  <br/>Inferidos<br/>Page<br/>ClientPerf<br/>Ajax |
| [Definir propiedades predeterminadas][apiproperties] |**Propiedades** en todos los eventos estándar y personalizados |
| [Llamar a TrackMetric][api] |Valores numéricos<br/>**Propiedades** |
| [Llamar a Track*][api] |Nombre del evento<br/>**Propiedades** |
| [Llamar a TrackException][api] |**Excepciones**<br/>Volcado de la pila<br/>**Propiedades** |
| El SDK no puede recopilar datos. Por ejemplo: <br/> - no se puede acceder a los contadores de rendimiento<br/> - excepción en el inicializador de telemetría |Diagnóstico de SDK |

Para los [SDK de otras plataformas][platforms], consulte los documentos correspondientes.

#### <a name="hello-classes-of-collected-data"></a>clases de Hola de los datos recopilados
| Clase de datos recopilados | Se incluyen (no es una lista exhaustiva) |
| --- | --- |
| **Propiedades** |**Cualquier dato - determinado por el código** |
| DeviceContext |Identificador, IP, configuración regional, modelo de dispositivo, red, tipo de red, nombre de OEM, resolución de pantalla, instancia de rol, nombre de rol, tipo de dispositivo |
| ClientContext  |Sistema operativo, configuración regional, idioma, red, resolución de ventana |
| Sesión |identificador de sesión |
| ServerContext |Nombre del equipo, configuración regional, sistema operativo, dispositivo, sesión de usuario, contexto de usuario, operación |
| Inferidos |ubicación geográfica de dirección IP, marca de tiempo, sistema operativo, explorador |
| Métricas |Nombre y valor de la métrica |
| Eventos |Nombre y valor del evento |
| PageViews |URL y nombre de página o nombre de pantalla |
| Rendimiento del cliente |URL o nombre de página, tiempo de carga del explorador |
| Ajax |Llamadas HTTP desde la página web tooserver |
| Solicitudes |URL, duración, código de respuesta |
| Dependencias |Tipo (SQL, HTTP,...), cadena de conexión o URI, sincrónico/asincrónico, duración, éxito, instrucción SQL (con monitor de estado) |
| **Excepciones** |Tipo, **mensaje**, pilas de llamadas, archivo de origen y número de línea, identificador de subproceso |
| Bloqueos |Identificador de proceso, identificador de proceso principal, identificador de subproceso de bloqueo; revisión de aplicación, identificador, compilación; tipo de excepción, dirección, razón; símbolos y registros confusos, direcciones binarias inicial y final, nombre binario y ruta de acceso, tipo de cpu |
| Seguimiento |**Mensaje** y nivel de gravedad |
| Contadores de rendimiento |Tiempo de procesador, memoria disponible, velocidad de solicitudes, tasa de excepciones, bytes privados del proceso, velocidad de E/S, duración de la solicitud, longitud de la cola de solicitudes |
| Disponibilidad |Código de respuesta de prueba web, duración de cada paso de la prueba, nombre de la prueba, marca de tiempo, éxito, tiempo de respuesta, ubicación de la prueba |
| Diagnóstico de SDK |Mensaje de seguimiento o de excepción |

También puede [optar por desactivar algunos de los datos de hello mediante la edición de ApplicationInsights.config][config]

## <a name="credits"></a>Créditos
Este producto incluye datos GeoLite2 creados por MaxMind, disponible en [http://www.maxmind.com](http://www.maxmind.com).



<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[client]: app-insights-javascript.md
[config]: app-insights-configuration-with-applicationinsights-config.md
[greenbrown]: app-insights-asp-net.md
[java]: app-insights-java-get-started.md
[platforms]: app-insights-platforms.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md

