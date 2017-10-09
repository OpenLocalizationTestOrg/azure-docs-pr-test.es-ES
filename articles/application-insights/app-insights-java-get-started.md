---
title: "análisis de las aplicaciones web aaaJava con Azure Application Insights | Documentos de Microsoft"
description: "Supervisión del rendimiento de aplicaciones web de Java con Application Insights. "
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a>Introducción a Application Insights en un proyecto web de Java


[Application Insights](https://azure.microsoft.com/services/application-insights/) es un servicio de análisis extensible para los desarrolladores web que le ayuda a comprensión el rendimiento de Hola y el uso de la aplicación en vivo. Usarlo demasiado[detectar y diagnosticar problemas de rendimiento y excepciones](app-insights-detect-triage-diagnose.md), y [escribir código] [ api] tootrack qué hacer un usuario con la aplicación.

![datos de ejemplo](./media/app-insights-java-get-started/5-results.png)

Application Insights es compatible con aplicaciones Java que se ejecutan en Linux, Unix o Windows.

Necesita:

* Oracle JRE 1.6 o posterior, o Zulu JRE 1.6 o posterior
* Una suscripción demasiado[Microsoft Azure](https://azure.microsoft.com/).

*Si tiene una aplicación web que ya está en funcionamiento, pueden ir procedimiento alternativo Hola demasiado[agregar Hola SDK en tiempo de ejecución en el servidor web de hello](app-insights-java-live.md). Esa alternativa evita volver a generar código de hello, pero no obtiene la actividad de usuario de hello opción toowrite código tootrack.*

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Obtención de una clave de instrumentación de Application Insights
1. Inicie sesión en toohello [portal de Microsoft Azure](https://portal.azure.com).
2. Cree un recurso en Application Insights. Establezca tooJava de tipo hello aplicación aplicaciones web.

    ![Rellene un nombre, elija la aplicación web de Java y haga clic en Crear.](./media/app-insights-java-get-started/02-create.png)
3. Buscar la clave de instrumentación de Hola de nuevo recurso de Hola. Necesitará toopaste esta clave en el proyecto de código en breve.

    ![En hello nueva información general de recursos, haga clic en propiedades y copiar Hola clave de instrumentación](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a>2. Agregar hello Application Insights SDK para el proyecto de Java tooyour
*Elija la forma adecuada de hello para el proyecto.*

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a>Si está usando Eclipse toocreate un proyecto Web dinámico o Maven...
Hola de uso [Application Insights SDK para Java complemento][eclipse].

#### <a name="if-youre-using-maven"></a>Si está usando Maven...
Si el proyecto ya está configurado toouse Maven de compilación, combine Hola siguiente archivo de código tooyour pom.xml.

A continuación, descargan tooget Hola binarios de actualización Hola proyecto dependencias.

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* *¿Errores de validación en la suma de comprobación o la compilación?* Pruebe en su lugar una versión específica, como:`<version>1.0.n</version>`. Encontrará la versión más reciente de Hola Hola [notas de la versión de SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) o en nuestros [artefactos de Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).
* *¿Necesita tooupdate tooa nuevo SDK?* Actualice las dependencias del proyecto.

#### <a name="if-youre-using-gradle"></a>Si está usando Gradle...
Si el proyecto ya está configurado toouse Gradle de compilación, la mezcla Hola siguiente archivo de código tooyour build.gradle.

Luego se descargarán tooget Hola binarios de actualización Hola proyecto dependencias.

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* *¿Errores de validación de suma de comprobación o de compilación? Utilice en su lugar una versión específica, como:* `version:'1.0.n'` *Encontrará la versión más reciente de Hola Hola [notas de la versión de SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*
* *tooupdate tooa nuevo SDK*
  * Actualice las dependencias del proyecto.

#### <a name="otherwise-"></a>De lo contrario...
Agregar manualmente Hola SDK:

1. Descargar hello [Application Insights SDK para Java](https://aka.ms/aijavasdk).
2. Extraer los archivos binarios de Hola de archivo zip de Hola y agréguelos tooyour proyecto.

### <a name="questions"></a>Preguntas...
* *¿Cuál es la relación de hello entre hello `-core` y `-web` componentes en zip Hola?*

  * `applicationinsights-core`Encontrará Hola reconstrucción API. Este componente se necesita siempre.
  * `applicationinsights-web` proporciona métricas que realizan el seguimiento de recuentos de solicitud HTTP y tiempos de respuesta. Este componente se puede omitir si no se desea que se recopilen automáticamente los datos de esta telemetría. Por ejemplo, si desea que toowrite sus propios.
* *Hola tooupdate SDK cuando se publican los cambios*

  * Descargar más reciente hello [Application Insights SDK para Java](https://aka.ms/qqkaq6) y reemplazar Hola los antiguos.
  * Se describen los cambios en hello [notas de la versión de SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).

## <a name="3-add-an-application-insights-xml-file"></a>3. Adición de un archivo .xml de Application Insights
Agregar carpeta de recursos de ApplicationInsights.xml toohello en el proyecto, o asegúrese de que se agrega la ruta de clase de implementación del proyecto tooyour. Copie Hola continuación de XML en ella.

Sustituya la clave de instrumentación de Hola que obtuvo en hello portal de Azure.

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* clave de instrumentación de Hola se envía junto con todos los elementos de telemetría e indica toodisplay Application Insights en el recurso.
* Hola componente de la solicitud HTTP es opcional. Envía automáticamente telemetría sobre las solicitudes y portal de toohello de tiempos de respuesta.
* Correlación de eventos es un componente de solicitud de incorporación toohello HTTP. Asigna una identificador tooeach las solicitudes recibidas por server hello y agrega este identificador como un elemento de propiedad tooevery de telemetría como propiedad de hello 'Operation.Id'. Le permite la telemetría de hello toocorrelate asociado con cada solicitud estableciendo un filtro [búsqueda diagnóstico][diagnostic].
* clave de Application Insights Hola puede pasarse dinámicamente desde Hola portal de Azure como una propiedad del sistema (-DAPPLICATION_INSIGHTS_IKEY = your_ikey). Si no hay ninguna propiedad definida, busca la variable de entorno (APPLICATION_INSIGHTS_IKEY) en la configuración de las aplicaciones de Azure. Si ambas propiedades hello no están definidos, se usa Hola predeterminado InstrumentationKey desde ApplicationInsights.xml. Esta secuencia ayuda a toomanage InstrumentationKeys distintos para diferentes entornos dinámicamente.

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a>Clave de instrumentación de formas alternativas tooset Hola
Application Insights SDK busca clave hello en este orden:

1. Propiedad del sistema:-DAPPLICATION_INSIGHTS_IKEY = your_ikey
2. Variable de entorno: APPLICATION_INSIGHTS_IKEY
3. Archivo de configuración: ApplicationInsights.xml

También se puede [configurar en el código](app-insights-api-custom-events-metrics.md#ikey):

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a>4. Adición de un filtro HTTP
último paso de configuración Hola permite Hola HTTP solicitud componente toolog cada solicitud web. (No es necesario si desea simplemente API reconstrucción Hola.)

Busque y abra el archivo web.xml de hello en el proyecto y Hola de combinación siguiente código bajo el nodo de la aplicación web de hello, donde se configuran los filtros de aplicación.

resultados más precisos tooget hello, filtro de hello deben asignarse antes de todos los demás filtros.

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a>Si utiliza Spring Web MVC 3.1, o cualquier versión posterior
Editar estos elementos en *-paquete de Application Insights de servlet.xml tooinclude hello:

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a>Si está usando Struts 2
Agregue este archivo de configuración de elemento toohello Struts (generalmente denominado struts.xml o struts default.xml):

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

(Si tiene interceptores definidos en una pila de manera predeterminada, el interceptor de hello puede simplemente agregarán toothat pila).

## <a name="5-run-your-application"></a>5. Ejecución de la aplicación
Ejecutar en modo de depuración en el equipo de desarrollo, o publicar tooyour server.

## <a name="6-view-your-telemetry-in-application-insights"></a>6. Visualización de la telemetría en Application Insights
Devolver recurso de Application Insights tooyour en [portal de Microsoft Azure](https://portal.azure.com).

Datos de las solicitudes HTTP aparecen en la hoja de información general de Hola. (Si todavía no está ahí, espere unos segundos y, a continuación, haga clic en Actualizar).

![datos de ejemplo](./media/app-insights-java-get-started/5-results.png)

[Más información acerca de las métricas.][metrics]

Click-through cualquier toosee gráfico más detallada agrega métricas.

![](./media/app-insights-java-get-started/6-barchart.png)

> Visión de la aplicación, se da por supuesto formato Hola de solicitudes HTTP que las aplicaciones MVC es: `VERB controller/action`. Por ejemplo, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` y `GET Home/Product/sdf96vws` se agrupan en `GET Home/Product`. Esta agrupación permite agregaciones significativas de solicitudes, como el número de solicitudes y el tiempo medio de ejecución de las solicitudes.
>
>

### <a name="instance-data"></a>Datos de instancia
Click-through de una solicitud específica escriba toosee las instancias individuales.

Se muestran dos tipos de datos en Application Insights: datos agregados, almacenados y mostrados como promedios, recuentos y sumas; y datos de instancia, como informes individuales de las solicitudes HTTP, excepciones, vistas de página o eventos personalizados.

Al ver las propiedades de Hola de una solicitud, puede ver eventos de telemetría de hello asociados con él, como las solicitudes y las excepciones.

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a>Analytics: Lenguaje de consulta eficaz
Dado que acumulan más datos, puede ejecutar consultas en ambas instancias de tooaggregate toofind y de datos individuales.  [Analytics](app-insights-analytics.md) es una eficaz herramienta tanto para conocer el rendimiento y el uso, como para el diagnóstico.

![Ejemplo de Analytics](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a>7. Instale la aplicación en el servidor de Hola
Publicar ahora el servidor de toohello de aplicación, permitir a los usuarios usar e inspeccionar telemetría Hola aparezca en el portal de Hola.

* Asegúrese de que el firewall permite la aplicación toosend puertos toothese de telemetría:

  * dc.services.visualstudio.com:443
  * f5.services.visualstudio.com:443

* Si el tráfico saliente debe enrutarse a través de un firewall, defina las propiedades de sistema `http.proxyHost` y `http.proxyPort`.

* En los servidores de Windows, instale:

  * [Microsoft Visual C++ Redistributable](http://www.microsoft.com/download/details.aspx?id=40784)

    (Este componente habilita los contadores de rendimiento.)


## <a name="exceptions-and-request-failures"></a>Excepciones y errores de solicitud
Las excepciones no controladas se recopilan automáticamente:

![Abra Configuración, Errores](./media/app-insights-java-get-started/21-exceptions.png)

toocollect datos en otras excepciones, tienes dos opciones:

* [Insertar llamadas tootrackException() en su código][apiexceptions].
* [Instalar agente Java hello en el servidor](app-insights-java-agent.md). Especificar métodos de Hola que desee toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Supervisión de llamadas a métodos y dependencias externas
[Instalar agente Java hello](app-insights-java-agent.md) toolog especifica métodos internos y las llamadas realizadas a través de JDBC, con datos de tiempo.

## <a name="performance-counters"></a>Contadores de rendimiento
Abra **configuración**, **servidores**, toosee un intervalo de los contadores de rendimiento.

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a>Personalizar la recopilación de contadores de rendimiento
colección de toodisable del conjunto estándar de Hola de contadores de rendimiento, agregar Hola siguiente código en el nodo raíz de Hola de archivo de hello ApplicationInsights.xml:

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a>Recopilar contadores de rendimiento adicionales
Puede especificar toobe de contadores de rendimiento adicionales recopilados.

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a>Contadores JMX (expuestos por máquina Virtual Java de hello)

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* `displayName`: nombre de hello mostrado en el portal de Application Insights Hola.
* `objectName`: nombre de objeto JMX Hola.
* `attribute`: atributo Hola de hello JMX objeto nombre toofetch
* `type`(opcional): Hola tipo de atributo del objeto JMX:
  * Valor predeterminado: un tipo simple como int o long.
  * `composite`: datos de contador de rendimiento de hello están en formato de Hola de 'Attribute.Data'
  * `tabular`: datos de contador de rendimiento de hello están en formato de Hola de una fila de tabla

#### <a name="windows-performance-counters"></a>Contadores de rendimiento de Windows
Cada [contador de rendimiento de Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) es un miembro de una categoría (Hola igual que un campo es un miembro de una clase). Las categorías puede ser globales, o pueden tener instancias con nombre o numeradas.

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* displayName: nombre de hello mostrado en el portal de Application Insights Hola.
* categoryName: Hola categoría contador de rendimiento (objeto de rendimiento) al que está asociado este contador de rendimiento.
* counterName: nombre de Hola Hola del contador de rendimiento.
* instanceName: Hola nombre de instancia de categoría de contador de rendimiento de Hola o una cadena vacía (""), si la categoría de hello contiene una sola instancia. Si Hola categoryName es el proceso y le gustaría toocollect del contador de rendimiento hello es proceso JVM actual de hello en que se ejecuta la aplicación, especifique `"__SELF__"`.

Los contadores de rendimiento están visibles como métricas personalizadas en el [Explorador de métricas][metrics].

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Contadores de rendimiento de Unix
* [Instalar collectd con el complemento de Application Insights hello](app-insights-java-collectd.md) tooget una amplia variedad de datos del sistema y de red.

## <a name="get-user-and-session-data"></a>Obtención de datos de usuario y sesión
Bien, va a enviar telemetría desde el servidor web. Ahora tooget Hola vista de 360 grados completa de la aplicación, puede agregar más supervisión:

* [Agregar páginas web de telemetría tooyour] [ usage] toomonitor página vistas y las métricas de usuario.
* [Configurar las pruebas web] [ availability] toomake seguro de la aplicación permanece en vivo y capacidad de respuesta.

## <a name="capture-log-traces"></a>Captura de seguimiento de registros
Puede usar Application Insights tooslice y reorganizar los registros de Log4J, Logback u otros marcos de registro. Puede correlacionar los registros de hello con las solicitudes HTTP y otro telemetría. [Vea cómo][javalogs].

## <a name="send-your-own-telemetry"></a>Envío de su propia telemetría
Ahora que ha instalado Hola SDK, puede usar Hola API toosend su propio telemetría.

* [Realizar un seguimiento de eventos personalizados y las métricas] [ api] toolearn hacen lo que los usuarios con la aplicación.
* [Buscar eventos y registros] [ diagnostic] toohelp diagnosticar problemas.

## <a name="availability-web-tests"></a>Pruebas web de disponibilidad
Application Insights pueden probar su sitio Web en intervalos regulares toocheck que está en funcionamiento y responder correctamente. [tooset una][availability], haga clic en las pruebas Web.

![Haga clic en Pruebas web y luego en Agregar prueba web](./media/app-insights-java-get-started/31-config-web-test.png)

Obtendrá gráficos de tiempos de respuesta, junto con notificaciones por correo electrónico si su sitio deja de funcionar.

![Ejemplo de prueba web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

[Más información acerca de las pruebas web de disponibilidad.][availability]

## <a name="questions-problems"></a>¿Tiene preguntas? ¿Tiene problemas?
[Solución de problemas de Java](app-insights-java-troubleshoot.md)

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Pasos siguientes
* [Supervisión de llamadas a dependencias](app-insights-java-agent.md)
* [Supervisión de contadores de rendimiento de Unix](app-insights-java-collectd.md)
* Agregar [tooyour las páginas web de supervisión](app-insights-javascript.md) tiempo de carga de la página de toomonitor, llamadas de AJAX, excepciones de explorador.
* Escribir [telemetría personalizada](app-insights-api-custom-events-metrics.md) tootrack uso en el Explorador de Hola o en el servidor de Hola.
* Crear [paneles](app-insights-dashboards.md) gráficos de clave toobring Hola juntos para supervisar el sistema.
* Uso de [Analytics](app-insights-analytics.md) para realizar consultas eficaces sobre los datos de telemetría de la aplicación
* Para más información, visite [Azure para desarrolladores de Java](/java/azure).

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
