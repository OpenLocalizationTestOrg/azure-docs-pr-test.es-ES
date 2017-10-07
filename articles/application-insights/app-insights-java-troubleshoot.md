---
title: aaaTroubleshoot Application Insights en un proyecto web de Java
description: "Guía de solución de problemas: supervisión de aplicaciones activas Java con Application Insights."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Solución de problemas y preguntas y respuestas sobre Application Insights para Java
Preguntas o problemas relacionados con [Azure Application Insights en Java][java]. a continuación se incluyen algunas sugerencias.

## <a name="build-errors"></a>Errores de compilación
**En Eclipse, cuando Agregar Hola Application Insights SDK a través de Maven o Gradle, puede obtener errores de validación de suma de comprobación o de compilación.**

* Si Hola dependencia <version> elemento está usando un patrón con caracteres comodín (por ejemplo, (Maven) `<version>[1.0,)</version>` o (Gradle) `version:'1.0.+'`), pruebe a especificar una versión específica en su lugar como `1.0.2`. Vea hello [notas de la versión](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) para la versión más reciente de Hola.

## <a name="no-data"></a>No aparecen datos
**He agregado Application Insights correctamente y se ejecutó la aplicación, pero nunca he visto datos en el portal de Hola.**

* Espere un minuto y haga clic en Actualizar, gráficos de Hello actualización por sí mismas periódicamente, pero también puede actualizar manualmente. intervalo de actualización de Hello depende del intervalo de tiempo de hello del gráfico de Hola.
* Compruebe que tiene una clave de instrumentación definida en hello ApplicationInsights.xml archivo (en la carpeta de recursos de hello en el proyecto)
* Compruebe que no hay ningún `<DisableTelemetry>true</DisableTelemetry>` nodo en el archivo xml de hello.
* En el firewall, es posible que tenga tooopen los puertos TCP 80 y 443 para toodc.services.visualstudio.com de tráfico saliente. Vea hello [lista completa de las excepciones del firewall](app-insights-ip-addresses.md)
* En Microsoft Azure Hola iniciar panel, examine mapa de estado del servicio de Hola. Si hay alguna alerta indicaciones, espere hasta que hayan devuelto tooOK y, a continuación, cierre y vuelva a abrir la hoja de la aplicación Application Insights.
* Activar el registro toohello la ventana de consola del IDE, mediante la adición de un `<SDKLogger />` elemento bajo el nodo de raíz de hello en el archivo de hello ApplicationInsights.xml (en la carpeta de recursos de hello en el proyecto) y busque las entradas que se prologa con [Error].
* Asegúrese de que ese Hola correcto ApplicationInsights.xml archivo se ha cargado correctamente por hello SDK de Java, examinando los mensajes de salida de la consola de Hola para una instrucción "archivo de configuración se encontró correctamente".
* Si no se encuentra el archivo de configuración de hello, compruebe toosee de mensajes de salida de hello donde se busca el archivo de configuración de Hola y asegúrese de que ese hello que applicationinsights.XML se encuentra en una de esas ubicaciones de búsqueda. Como regla general, puede colocar el archivo de configuración de hello cerca Hola aplicación visión SDK JAR. Por ejemplo: en Tomcat, esto significaría Hola carpeta WEB-INF/lib.

#### <a name="i-used-toosee-data-but-it-has-stopped"></a>He usado toosee datos, pero se ha detenido
* Comprobar hello [estado blog](http://blogs.msdn.com/b/applicationinsights-status/).
* ¿Ha alcanzado su cuota mensual de puntos de datos? Abra Configuración/cuotas y precios toofind out. Si es así, puede actualizar el plan o pagar para obtener capacidad adicional. Vea hello [precios esquema](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-hello-data-im-expecting"></a>No veo todos los datos de hello que estoy esperando
* Abra hello las cuotas y precios hoja y compruebe si [muestreo](app-insights-sampling.md) está en funcionamiento. (transmisión de 100% significa que muestreo no está en funcionamiento). Hola servicio Application Insights puede ser conjunto tooaccept sólo una fracción de telemetría de Hola que llega desde la aplicación. Esto le ayuda a mantenerse en su cuota mensual de telemetría. 

## <a name="no-usage-data"></a>No aparecen datos de uso
**Veo datos sobre solicitudes y tiempos de respuesta, pero no de vista de página, del explorador o de datos de usuarios.**

Ha configurado correctamente la la telemetría de toosend de aplicación desde el servidor de Hola. Ahora el siguiente paso es demasiado[configurar la telemetría de toosend de páginas web desde el Explorador de web de hello][usage].

Como alternativa, si el cliente es una aplicación de [teléfono o de cualquier otro dispositivo][platforms], puede enviar datos de telemetría desde este. 

Use Hola mismo tooset clave de instrumentación la telemetría de su cliente y el servidor. datos de Hello aparecerán en Hola mismo recurso de Application Insights y podrá toocorrelate capaz de eventos de cliente y servidor.


## <a name="disabling-telemetry"></a>Deshabilitación de la telemetría
**¿Cómo puedo deshabilitar la recopilación de telemetría?**

En el código:

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**O** 

Actualizar ApplicationInsights.xml (en la carpeta de recursos de hello en el proyecto). Agregue los siguiente hello en el nodo raíz de hello:

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

Mediante el método XML de hello, tendrá que aplicación de hello toorestart cuando se cambia el valor de Hola.

## <a name="changing-hello-target"></a>Cambiar el destino de Hola
**¿Cómo puedo cambiar el recurso de Azure al que mi proyecto envía datos?**

* [Obtener clave de instrumentación de Hola de nuevo recurso de Hola.][java]
* Si agrega el proyecto de tooyour de Application Insights mediante hello Azure Toolkit for Eclipse, haga clic con el proyecto web, seleccione **Azure**, **configurar Application Insights**y cambiar la clave de Hola.
* En caso contrario, actualizar la clave de Hola de ApplicationInsights.xml en la carpeta de recursos de hello en el proyecto.

## <a name="debug-data-from-hello-sdk"></a>Depurar datos de hello SDK

**¿Cómo puedo averiguar qué Hola SDK está haciendo?**

Para obtener más información acerca de lo que ocurre en hello API, agregar a tooget `<SDKLogger/>` en el nodo raíz de Hola Hola ApplicationInsights.xml del archivo de configuración.

También puede indicar al archivo de hello registrador toooutput tooa:

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

Hola archivos pueden encontrarse en `%temp%\javasdklogs` o `java.io.tmpdir` en el caso de servidor de Tomcat.


## <a name="hello-azure-start-screen"></a>pantalla de inicio de Azure de bienvenida
**Estoy observando [Hola portal de Azure](https://portal.azure.com). ¿Mapa Hola decirme algo acerca de mi aplicación?**

No, muestra el estado de Hola de servidores Azure alrededor de Hola a todos.

*En panel de inicio de Azure de hello (pantalla principal), ¿cómo busco datos acerca de mi aplicación?*

Suponiendo que [configurar su aplicación para Application Insights][java], haga clic en Examinar, seleccione Application Insights y seleccionar recurso de aplicación Hola que creó para la aplicación. tooget existe con mayor rapidez en el futuro, puede anclar el panel de inicio de toohello de aplicación.

## <a name="intranet-servers"></a>Servidores de intranet
**¿Puedo supervisar un servidor de mi intranet?**

Sí, siempre que el servidor puede enviar el portal de Application Insights toohello de telemetría a través de Hola internet pública. 

En el firewall, es posible que tenga tooopen los puertos TCP 80 y 443 para toodc.services.visualstudio.com de tráfico saliente y f5.services.visualstudio.com.

## <a name="data-retention"></a>Retención de datos
**¿Cuánto tiempo se retienen los datos en el portal de hello? ¿Es seguro?**

Consulte [Privacidad y retención de los datos][data].

## <a name="next-steps"></a>Pasos siguientes
**He configurado Application Insights para mi aplicación de servidor Java. ¿Qué más puedo hacer?**

* [Supervisar la disponibilidad de sus páginas web][availability]
* [Supervisar el uso de páginas web][usage]
* [Realizar el seguimiento del uso y diagnosticar los problemas en las aplicaciones de su dispositivo][platforms]
* [Escribir un uso tootrack de código de la aplicación][track]
* [Captura de registros de diagnóstico][javalogs]

## <a name="get-help"></a>Obtener ayuda
* [Desbordamiento de la pila](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

