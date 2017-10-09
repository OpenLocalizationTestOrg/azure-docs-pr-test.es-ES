---
title: muestreo de aaaTelemetry en Azure Application Insights | Documentos de Microsoft
description: "¿Cómo tookeep Hola volumen de telemetría bajo control."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a>Muestreo en Application Insights.


El muestreo es una característica de [Azure Application Insights](app-insights-overview.md). Es tráfico de manera tooreduce telemetría y almacenamiento, recomienda Hola conservando un análisis estadísticamente correcto de datos de la aplicación. filtro de Hello selecciona los elementos que están relacionados, por lo que puede navegar entre elementos cuando realiza una de las investigaciones de diagnóstico.
Cuando los recuentos de métrica se presentan tooyou en el portal de hello, son normalizarse tootake cuenta de hello de muestreo, toominimize cualquier efecto en las estadísticas de Hola.

El muestreo reduce los costos de tráfico y datos y le ayuda a evitar la limitación.

## <a name="in-brief"></a>En resumen:
* Muestreo conserva 1 en  *n*  registra y descarta el resto de Hola. Por ejemplo, podría retener los eventos de 1 a 5, una velocidad de muestreo del 20 %. 
* El muestreo se produce automáticamente si la aplicación envía una gran cantidad de telemetría en las aplicaciones de servidor web ASP.NET.
* También puede establecer muestreo manualmente, ya sea en hello portal en hello página; de precios o bien, en hello SDK para ASP.NET en el archivo .config de hello, tooalso reducir el tráfico de red de Hola.
* Si registra eventos personalizados y desea toomake seguro de que un conjunto de eventos se conservan o se descartan juntas, asegúrese de que haya Hola mismo valor de Id.
* divisor de muestreo de Hello  *n*  se notifica en cada registro de la propiedad de hello `itemCount`, que en la búsqueda aparece bajo nombre descriptivo de Hola "número de solicitudes" o "recuento de eventos". Cuando el muestreo no está en funcionamiento, `itemCount==1`.
* Si escribe consultas de Analytics, debería [tener en cuenta el muestreo](app-insights-analytics-tour.md#counting-sampled-data). En concreto, en lugar de simplemente contar registros, debería usar `summarize sum(itemCount)`.

## <a name="types-of-sampling"></a>Tipos de muestreo
Existen tres métodos de muestreo alternativos:

* **Muestreo adaptativo** ajusta automáticamente el volumen de Hola de telemetría enviado desde Hola SDK en la aplicación ASP.NET. Valor predeterminado del SDK v 2.0.0-beta3. Actualmente solo está disponible para la telemetría de servidor ASP.NET. 
* **Muestreo de tipo fijo** reduce el volumen de Hola de telemetría que se envían desde el servidor de ASP.NET y de los exploradores de los usuarios. Establecer la velocidad de Hola. Hola cliente y servidor sincronizarán su muestreo por lo que, la búsqueda en, puede navegar entre las vistas de página relacionados y las solicitudes.
* **Muestreo de ingesta** funciona en hello portal de Azure. Descarta algunas de telemetría de Hola que llega desde su aplicación a una velocidad que se establece. Aunque no reduce el tráfico de telemetría, le ayuda a mantenerse dentro de su cuota mensual. Hola gran ventaja de muestreo de ingesta es que puede establecer sin volver a implementar la aplicación y uniformemente funciona para todos los clientes y servidores. 

Si el muestreo de velocidad adaptable o fija está funcionando, el muestreo de ingesta se deshabilita.

## <a name="ingestion-sampling"></a>muestreo de ingesta
Esta forma de muestreo se aplica en punto de Hola donde telemetría Hola desde el servidor web, exploradores y dispositivos alcanza el extremo de servicio de Application Insights de Hola. Aunque no reduce el tráfico de telemetría de hello enviado desde la aplicación, reducir la cantidad de hello procesados y conservan (y cobra por) con Application Insights.

Use este tipo de muestreo si la aplicación a menudo supera la cuota mensual y no tendrá posibilidad de Hola de mediante cualquiera de los tipos basados en SDK de Hola de muestreo. 

Establecer la frecuencia de muestreo de Hola Hola cuotas y hoja de precios:

![Desde la hoja de información general sobre la aplicación hello, haga clic en configuración, cuota, ejemplos, a continuación, seleccione una frecuencia de muestreo y haga clic en actualizar.](./media/app-insights-sampling/04.png)

Al igual que otros tipos de muestreo, el algoritmo de hello conserva elementos de telemetría relacionada. Por ejemplo, al inspeccionar la telemetría de hello en la búsqueda, podrá excepciones concretas tooa relacionados con la solicitud de hello toofind. Los recuentos de métrica, como la tasa de solicitudes y la tasa de excepciones se mantienen correctamente.

Los puntos de datos que se descartan por muestreo no están disponibles en ninguna característica de Application Insights como [exportación continua](app-insights-export-telemetry.md).

El muestreo de ingesta no funciona mientras el muestreo adaptativo o de frecuencia fija basado en el SDK está en funcionamiento. Si la velocidad de muestreo de hello en hello SDK es menor del 100%, a continuación, hello frecuencia de muestreo de ingesta que establezca se omite.

> [!WARNING]
> valor de Hola que se muestra en el icono de hello indica valor Hola que establezca para el muestreo de recopilación. Frecuencia de muestreo de hello real, no representa si el muestreo de SDK está en funcionamiento.
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a>Muestreo adaptable en el servidor web
Muestreo adaptable está disponible para hello Application Insights SDK para ASP.NET v 2.0.0-beta3 y versiones posteriores y está habilitada de forma predeterminada. 

Muestreo adaptativo afecta al volumen de Hola de telemetría enviado desde su aplicación de servidor web toohello servicio Application Insights. Hello volumen se ajusta automáticamente tookeep dentro de un tipo de tráfico máximo especificado.

No funciona con volúmenes bajos de telemetría, así que una aplicación en proceso de depuración o un sitio web con poca utilización no se verán afectados.

se descarta el volumen de destino de hello tooachieve, algunos de telemetría de hello generado. Pero al igual que otros tipos de muestreo, el algoritmo de hello conserva elementos de telemetría relacionada. Por ejemplo, al inspeccionar la telemetría de hello en la búsqueda, podrá excepciones concretas tooa relacionados con la solicitud de hello toofind. 

Métrica de cuenta como tasa de solicitud y la tasa de excepciones están toocompensate ajustada para hello muestreo velocidad, para que muestren los valores correctos aproximadamente en el Explorador de métrica.

**Actualizar NuGet su proyecto** paquetes toohello más reciente *preliminares* versión de Application Insights: haga clic en proyecto de hello en el Explorador de soluciones, elija Administrar paquetes de NuGet, consulte **Include versión preliminar** y busque Microsoft.ApplicationInsights.Web. 

En [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), puede ajustar varios parámetros en hello `AdaptiveSamplingTelemetryProcessor` nodo. cifras de Hola que se muestran son valores predeterminados de hello:

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    Hello velocidad de destino que Hola algoritmo adaptable tiene como objetivo **en cada host de servidor**. Si la aplicación web se ejecuta en varios hosts, por lo tanto como tooremain dentro de la tasa de destino de tráfico en el portal de Application Insights Hola reducir este valor.
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    intervalo de saludo en qué Hola tasa actual de telemetría se vuelve a evaluar. La evaluación se realiza como una media móvil. Conviene tooshorten este intervalo si la telemetría es responsable toosudden ráfagas.
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    Una vez cambia de valor de porcentaje de muestreo, ¿con qué frecuencia después se permite toolower muestreo de porcentaje nuevo toocapture menos datos.
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    Una vez cambia de valor de porcentaje de muestreo, ¿con qué frecuencia después se permite tooincrease muestreo de porcentaje nuevo toocapture más datos.
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    Medida que varía de muestreo de porcentaje, ¿qué es el valor mínimo de Hola nos estamos permite tooset.
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    Medida que varía de muestreo de porcentaje, ¿cuál es el valor máximo de hello nos estamos permite tooset.
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    En el cálculo de Hola de hello Media móvil, peso Hola asignado valor más reciente de toohello. Use un tooor igual valor menor que 1. Los valores más pequeños modificar algoritmo Hola menos reactiva toosudden.
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    valor de Hello asignado cuando se acaba de iniciar aplicación hello. No lo reduzca durante la depuración. 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    Lista de tipos que no desea toobe muestrear delimitada por un punto y coma. Los tipos reconocidos son Dependency, Event, Exception, PageView, Request, Trace. Todas las instancias de hello especifican se transmiten los tipos; se muestrean los tipos de Hola que no se especifican.

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    Una lista delimitada por punto y coma de tipos que desee toobe muestrear. Los tipos reconocidos son Dependency, Event, Exception, PageView, Request, Trace. Hola especificado se muestrean tipos; todas las instancias de hello siempre se transmitirá otros tipos.


**tooswitch desactivar** muestreo adaptable, quitar un nodo AdaptiveSamplingTelemetryProcessor Hola desde la configuración de applicationinsights.

### <a name="alternative-configure-adaptive-sampling-in-code"></a>Alternativa: configure el muestreo adaptivo en el código
En lugar de ajuste de muestreo en el archivo .config de hello, puede utilizar código. Esto le permite toospecify una función de devolución de llamada que se invoca cuando se vuelve a evaluar la frecuencia de muestreo de Hola. Podría utilizar esto, por ejemplo, está usándola toofind fuera de la velocidad de muestreo.

Quitar hello `AdaptiveSamplingTelemetryProcessor` nodo desde el archivo .config de Hola.

*C#*

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Más información sobre los procesadores de telemetría](app-insights-api-filtering-sampling.md#filtering)).

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a>Muestreo para páginas web con JavaScript
Puede configurar páginas web para el muestreo de frecuencia fija desde cualquier servidor. 

Cuando se [configurar páginas web de Hola para Application Insights](app-insights-javascript.md), modificar el fragmento de código de hello que obtendrá de portal de Application Insights de Hola. (En las aplicaciones ASP.NET, el fragmento de código de hello normalmente va en _Layout.cshtml.)  Insertar una línea como `samplingPercentage: 10,` antes de la clave de instrumentación de hello:

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

Para el porcentaje de muestreo de hello, elija un porcentaje que es cerrar too100/N donde N es un entero.  Actualmente el muestreo no es compatible con otros valores.

Si también habilita el muestreo de tipo fijo en el servidor de hello, servidor y los clientes de hello sincronizará por lo que, la búsqueda en, puede navegar entre las vistas de página relacionados y las solicitudes.

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a>Muestreo de frecuencia fija para sitios web ASP.NET
Muestreo de tarifa fija que reduce el tráfico de hello enviado desde el servidor web y los exploradores web. A diferencia del muestreo adaptable, reduce la telemetría a una tasa fija que usted decide. También sincroniza cliente hello y muestreo de servidor para que se conservan elementos relacionados: por ejemplo, por lo que si observa una vista de página en la búsqueda, puede encontrar su solicitud relacionadas.

algoritmo de muestreo de Hello conserva los elementos relacionados. Para cada evento de solicitud HTTP, este y sus eventos relacionados se descartan o transmiten. 

En el Explorador de métricas, velocidades como recuentos de solicitud y la excepción se multiplican por un toocompensate de factor de velocidad de muestreo de hello, para que sean aproximadamente correctos.

1. **Actualizar paquetes de NuGet de su proyecto** toohello más reciente *preliminares* versión de Application Insights. Haga clic en proyecto de hello en el Explorador de soluciones, elija Administrar paquetes de NuGet, consulte **incluir versión preliminar** y busque Microsoft.ApplicationInsights.Web. 
2. **Deshabilitar muestreo adaptativo**: en [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), quite o marque como comentario hello `AdaptiveSamplingTelemetryProcessor` nodo.
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. **Habilitar el módulo de tipo fijo muestreo de Hola.** Agregue este fragmento demasiado[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> Para el porcentaje de muestreo de hello, elija un porcentaje que es cerrar too100/N donde N es un entero.  Actualmente el muestreo no es compatible con otros valores.
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a>Alternativa: habilitación del muestreo de frecuencia fija en el código de servidor
En lugar de establecer el parámetro de muestreo de hello en el archivo .config de hello, puede utilizar código. 

*C#*

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Más información sobre los procesadores de telemetría](app-insights-api-filtering-sampling.md#filtering)).

## <a name="when-toouse-sampling"></a>¿Cuando toouse muestreo?
Muestreo adaptable se habilita automáticamente si usas hello 2.0.0-beta3 de versión de SDK de ASP.NET o una versión posterior. Independientemente de la versión del SDK que utilice, puede emplear el muestreo de ingesta (en nuestro servidor).

Para la mayoría de las aplicaciones pequeñas y medianas no es necesario realizar muestreos. información de diagnóstico más útil de Hola y estadísticas más precisas se obtienen mediante la recopilación de datos en todas las actividades de usuario. 

son las principales ventajas de Hola de muestreo:

* El servicio de Application Insights descarta ("limita") puntos de datos cuando la aplicación envía un número muy elevado de telemetría en un intervalo de tiempo corto. 
* tookeep dentro de hello [cuota](app-insights-pricing.md) de puntos de datos para el nivel de precios. 
* tráfico de red tooreduce de colección de Hola de telemetría. 

### <a name="which-type-of-sampling-should-i-use"></a>¿Qué tipo de muestreo debo utilizar?
**Use el muestreo de ingesta si:**

* Con frecuencia sobrepasa su cuota mensual de telemetría.
* Está usando una versión de Hola SDK que no admite el muestreo - por ejemplo, hello Java SDK o versiones ASP.NET anteriores a 2.
* Recibe mucha telemetría de los exploradores web de sus usuarios.

**Use el muestreo de frecuencia fija si:**

* Usa Hola Application Insights SDK para la versión de servicios web ASP.NET 2.0.0 o posterior, y
* Desea muestreo sincronizados entre cliente y servidor, por lo que, cuando se está investigando eventos en [búsqueda](app-insights-diagnostic-search.md), puede navegar entre los eventos relacionados en el cliente de Hola y servidor, como las vistas de página y las solicitudes http.
* Esté seguro de porcentaje de hello muestreo adecuado para la aplicación. Debe estar suficientemente alto tooget métricas precisas, pero a continuación Hola velocidad que supera la cuota de precios y Hola límites de procesos. 

**Use el muestreo adaptable si:**

De lo contrario, se recomienda el muestreo adaptable. Esta opción está habilitada de forma predeterminada en el servidor ASP.NET Hola SDK, versión 2.0.0-beta3 o posterior. No reduce el tráfico hasta una determinada tasa mínima, así que no afectará a los sitios de utilización baja.

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a>¿Cómo se puede saber si el muestreo está en funcionamiento?
hello toodiscover real muestreo tasa independientemente de donde se ha aplicado, use un [consulta de análisis](app-insights-analytics.md) como este:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

En cada uno de ellos conserva el registro, `itemCount` indica Hola número de registros original que representa, too1 igual + número de Hola de registros descartados anteriores. 

## <a name="how-does-sampling-work"></a>¿Cómo funciona el muestreo?
Tipo fijo y muestreo adaptativo son una característica de hello SDK en las versiones de ASP.NET de 2.0.0 y versiones posteriores. Muestreo de recopilación es una característica de hello servicio Application Insights y puede estar en funcionamiento si Hola SDK no está realizando el muestreo. 

algoritmo de muestreo de Hello decide qué toodrop de elementos de telemetría y qué tookeep los (si está en hello SDK o en servicio de Application Insights de hello). Decisión de muestreo de Hola se basa en varias reglas que tienen como objetivo toopreserve todos los puntos de datos interrelacionados intacto y mantener una experiencia de diagnóstico en Application Insights que es práctica y confiable incluso con un conjunto de datos reducido. Por ejemplo, si para una solicitud errónea su aplicación envía elementos de telemetría adicionales (como la excepción y los seguimientos registrados para dicha solicitud), el muestreo no dividirá esta solicitud y otra telemetría. Escogerá mantenerlos o descartarlos todos juntos Como resultado, cuando se examina en detalles de la solicitud de hello en Application Insights, siempre puede ver solicitud Hola junto con sus elementos de telemetría asociado. 

Para las aplicaciones que definen el "usuario" (es decir, las aplicaciones web más típicas), decisión de muestreo de Hola se basa en el hash de Hola de Id. de usuario de hello, lo que significa que todos los telemetría para un usuario concreto se conserva o se quita. Para los tipos de Hola de aplicaciones que no definen los usuarios (por ejemplo, servicios web) Decisión de muestreo de Hola se basa en Id. de operación de saludo de solicitud de saludo. Por último, para los elementos de telemetría de Hola que no tienen el identificador de usuario ni la operación de conjunto (por ejemplo elementos de telemetría notificados de subprocesos asincrónicos no tienen ningún contexto de http) muestreo simplemente captura un porcentaje de elementos de telemetría de cada tipo. 

Cuando se presentan tooyou atrás de telemetría, Hola Application Insights servicio ajusta las métricas de Hola por Hola mismo porcentaje de muestreo que se usaron en tiempo de Hola de colección, toocompensate para hello puntos de datos que faltan. Por lo tanto, al examinar telemetría hello en Application Insights, los usuarios de hello están viendo aproximaciones estadísticamente correctas que son muy próxima toohello los números reales.

precisión de Hola de aproximación de hello depende en gran medida de porcentaje de muestreo de hello configurado. Asimismo, precisión Hola aumenta para aplicaciones que manejan un gran volumen de solicitudes suelen ser parecidos de una gran cantidad de usuarios. En Hola otra parte, para las aplicaciones que no funcionan con una carga significativa, no es necesario el muestreo como para estas aplicaciones normalmente pueden enviar todas su telemetría manteniéndose dentro de la cuota de hello, sin causar pérdida de datos de la limitación. 

Tenga en cuenta que Application Insights no muestra tipos de telemetría de métricas y las sesiones, desde para estos tipos, reducción de la precisión de hello puede ser muy deseable. 

### <a name="adaptive-sampling"></a>muestreo adaptable
Muestreo adaptativo agrega esa tasa actual de Hola de monitores de transmisión de un componente de hello SDK y ajusta Hola muestreo porcentaje tootry toostay dentro de la velocidad máxima del destino de Hola. ajuste de Hola se vuelve a calcular a intervalos regulares y se basa en una media móvil de hello velocidad de transmisión de salida.

## <a name="sampling-and-hello-javascript-sdk"></a>Hello SDK de JavaScript y muestreo
Hola cliente (JavaScript) SDK participa en tipo fijo muestreo junto con el servidor de hello SDK. páginas de Hello instrumentado sólo enviará telemetría de cliente de hello mismos usuarios para qué Hola servidor realiza su decisión demasiado "de ejemplo en." Esta lógica es la integridad de toomaintain diseñada de sesión de usuario a través de lado cliente y servidor. Como resultado, a partir de cualquier elemento específico de telemetría en Application Insights, puede encontrar todos los demás elementos de telemetría para ese usuario o esa sesión. 

*Las telemetrías del lado de cliente y de servidor no muestran ejemplos coordinados tal y como se describe anteriormente.*

* Compruebe que habilitó el muestreo de frecuencia fija tanto en el cliente como en el servidor.
* Asegúrese de que esa versión SDK de hello es 2.0 o superior.
* Compruebe que establece Hola mismo muestreo de porcentaje en el cliente de Hola y el servidor.

## <a name="frequently-asked-questions"></a>Preguntas frecuentes
*¿Por qué realizar un muestreo no consiste simplemente en "recopilar X por ciento de cada tipo de telemetría"?*

* Aunque este método de muestreo se proporcionan con una precisión de muy alta en aproximaciones métricas, interrumpirá datos de diagnóstico de capacidad toocorrelate por usuario, la sesión y la solicitud, lo cual resulta esencial para diagnósticos. Por lo tanto, el muestreo funciona mejor con una lógica "recopilar todos los elementos de telemetría para X por ciento de los usuarios de la aplicación", o "recopilar toda la telemetría para X por ciento de las solicitudes de aplicación". Para los elementos de telemetría de hello no asociados a las solicitudes de hello (por ejemplo, el procesamiento asincrónico en segundo plano), otoño de hello volver resulta demasiado "recopilar X por ciento de todos los elementos de cada tipo de telemetría." 

*¿Porcentaje de muestreo de hello cambian con el tiempo?*

* Sí, cambia porcentaje de muestreo de hello, en función de hello observados actualmente el volumen de telemetría de hello adaptable gradualmente de muestreo.

*Si utiliza el muestreo de tipo fijo, ¿cómo puedo saber qué muestreo de porcentaje funcionará Hola mejor para mi aplicación?*

* Una manera es toostart con muestreo adaptable, obtenga más información sobre qué clasificarlo liquida en (consulte Hola pregunta anterior), y, a continuación, con esa tasa de muestreo de velocidad toofixed de conmutador. 
  
    De lo contrario, tendrá que tooguess. Analizar el uso actual de telemetría en AI, observe cualquier limitación es decir que se producen y volumen de Hola de estimación de telemetría recopilado de Hola. Estas tres entradas, junto con el nivel de precios seleccionado, sugieren cuánto puede tooreduce volumen de Hola de telemetría recopilado de Hola. Sin embargo, un aumento en número de Hola de los usuarios o algunas otras MAYÚS en volumen de Hola de telemetría podrían invalidar la estimación.

*¿Qué sucede si configuro un porcentaje de muestreo demasiado bajo?*

* Porcentaje de muestreo excesivamente baja (muestreo demasiado minuciosa) reduce precisión Hola de aproximaciones hello, cuando trate de Application Insights visualización de hello toocompensate de datos de hello para la reducción de volumen de datos de Hola. Además, diagnóstico experiencia podría verse afectado negativamente, como algunos de hello con poca frecuencia se producen errores o se pueden muestrear solicitudes lentas.

*¿Qué sucede si configuro un porcentaje de muestreo demasiado alto?*

* Configurar muestreo demasiado alto porcentaje (no agresiva suficientemente) resultados una reducción insuficiente del volumen Hola de hello recopilan telemetría. Todavía puede experimentar pérdida de datos relacionados con toothrottling y el costo de Hola de usar Application Insights pueden ser mayor que el planeó debido toooverage cargos de telemetría.

*¿En qué plataformas puedo usar muestreo?*

* Muestreo de ingesta podrá realizarse automáticamente para cualquier telemetría por encima de un volumen si Hola SDK no está realizando el muestreo. Esto podría funcionar, por ejemplo, si su aplicación usa un servidor de Java, o si está utilizando una versión anterior de hello SDK de ASP.NET.
* Si usa las versiones del SDK de ASP.NET 2.0.0 y versiones posteriores (hospedado en Azure o en su propio servidor), recibirá adaptable de muestreo de forma predeterminada, pero puede cambiar la tasa de toofixed tal y como se ha descrito anteriormente. Con el muestreo de tipo fijo, Explorador de hello SDK sincroniza automáticamente toosample eventos relacionados. 

*Hay ciertos eventos excepcionales toosee suele. ¿Cómo se puede obtener ellos más allá de muestreo de hello módulo?*

* Inicializar una instancia independiente de TelemetryClient con un nuevo TelemetryConfiguration (no Hola de forma predeterminada está activa). Use ese toosend los eventos excepcionales.

## <a name="next-steps"></a>Pasos siguientes
* [filtro](app-insights-api-filtering-sampling.md) puede proporcionar un control más estricto de los SDK que envía.

