---
title: "aaaGet a trabajar con información de la aplicación de Azure con Java en Eclipse | Documentos de Microsoft"
description: Usar Hola rendimiento tooadd complemento de Eclipse y uso de supervisar el sitio Web de Java de tooyour con Application Insights
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a>Introducción a Application Insights con Java en Eclipse
Hola Application Insights SDK envía telemetría desde la aplicación web de Java para que se pueden analizar el uso y rendimiento. Hola Eclipse complemento para Application Insights automáticamente instala Hola SDK en el proyecto para sacar partido de telemetría de cuadro de hello, además de una API que puede usar la telemetría personalizada toowrite.   

## <a name="prerequisites"></a>Requisitos previos
Hola complemento funciona actualmente para los proyectos de Maven y proyectos Web dinámicos en Eclipse.
([Tipos de tooother agregar Application Insights de proyecto de Java][java].)

Necesitará:

* Oracle JRE 1.6 o posterior
* Una suscripción demasiado[Microsoft Azure](https://azure.microsoft.com/).
* [Eclipse IDE para Java EE Developers](http://www.eclipse.org/downloads/), Indigo o superior.
* Windows 7 o posterior, o Windows Server 2008 o posterior

## <a name="install-hello-sdk-on-eclipse-one-time"></a>Instalar SDK de hello en Eclipse (una vez)
Solo tiene toodo una vez por equipo. Este paso instala un Kit de herramientas que, a continuación, se puede agregar el SDK de hello tooeach Dynamic Web Project.

1. En Eclipse, haga clic en Ayuda, Instalar nuevo software.

    ![Ayuda, Instalar nuevo software](./media/app-insights-java-eclipse/0-plugin.png)
2. Hola SDK se encuentra en http://dl.microsoft.com/eclipse, en el Kit de herramientas de Azure.
3. Desactive **Ponerse en contacto con todos los sitios de actualización...**

    ![Para el SDK de Application Insights, desactive Ponerse en contacto con todos los sitios de actualización](./media/app-insights-java-eclipse/1-plugin.png)

Siga Hola restantes pasos para cada proyecto de Java.

## <a name="create-an-application-insights-resource-in-azure"></a>Creación de un recurso de Application Insights en Azure
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Cree un recurso de Application Insights. Establezca tooJava de tipo hello aplicación aplicaciones web.  

    ![Haga clic en + y elija Application Insights](./media/app-insights-java-eclipse/01-create.png)  

4. Buscar la clave de instrumentación de Hola de nuevo recurso de Hola. Necesitará toopaste en el proyecto de código en breve.  

    ![En hello nueva información general de recursos, haga clic en propiedades y copiar Hola clave de instrumentación](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a>Agregar proyecto de tooyour Application Insights
1. Agregar Application Insights en menú contextual de Hola de su proyecto web de Java.

    ![En hello nueva información general de recursos, haga clic en propiedades y copiar Hola clave de instrumentación](./media/app-insights-java-eclipse/02-context-menu.png)
2. Pegue la clave de instrumentación de Hola que obtuvo en hello portal de Azure.

    ![En hello nueva información general de recursos, haga clic en propiedades y copiar Hola clave de instrumentación](./media/app-insights-java-eclipse/03-ikey.png)

clave de Hola se envía junto con todos los elementos de telemetría e indica toodisplay Application Insights en el recurso.

## <a name="run-hello-application-and-see-metrics"></a>Ejecutar la aplicación hello y ver las métricas
Ejecute la aplicación.

Devolver el recurso de Application Insights de tooyour en Microsoft Azure.

Datos de las solicitudes HTTP aparecerá en la hoja de información general de Hola. (Si todavía no está ahí, espere unos segundos y, a continuación, haga clic en Actualizar).

![Respuesta del servidor, recuentos de solicitudes y errores ](./media/app-insights-java-eclipse/5-results.png)

Haga clic en a través de cualquier toosee gráfico métricas más detalladas.

![Recuentos de solicitudes por nombre](./media/app-insights-java-eclipse/6-barchart.png)

[Más información acerca de las métricas.][metrics]

Y, al ver las propiedades de Hola de una solicitud, puede ver eventos de telemetría de hello asociados con él, como las solicitudes y las excepciones.

![Todos los seguimientos para esta solicitud](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a>Telemetría de cliente
Desde la hoja de inicio rápido de hello, haga clic en Get código toomonitor páginas web:

![En la hoja de información general sobre la aplicación, elija Inicio rápido, obtener código toomonitor las páginas web. Copie el script de Hola.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

Insertar fragmento de código de hello en el encabezado de Hola de los archivos HTML.

#### <a name="view-client-side-data"></a>Visualización de datos del lado cliente
Abra las páginas web actualizadas y úselas. Espere un minuto o dos, a continuación, devolver tooApplication visión y hoja de uso de hello abierto. (Desde la hoja de información general de hello, desplácese hacia abajo y haga clic en uso).

Métricas de sesión, usuarios y vista de página aparecerán en la hoja de Hola de uso:

![Sesiones, usuarios y vistas de página](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

[Más información sobre la configuración de la telemetría de cliente.][usage]

## <a name="publish-your-application"></a>Publicación de la aplicación
Publicar ahora el servidor de toohello de aplicación, permitir a los usuarios usar e inspeccionar telemetría Hola aparezca en el portal de Hola.

* Asegúrese de que el firewall permite la aplicación toosend puertos toothese de telemetría:

  * dc.services.visualstudio.com:443
  * dc.services.visualstudio.com:80
  * f5.services.visualstudio.com:443
  * f5.services.visualstudio.com:80
* En los servidores de Windows, instale:

  * [Microsoft Visual C++ Redistributable](http://www.microsoft.com/download/details.aspx?id=40784)

    (Esto habilita los contadores de rendimiento.)

## <a name="exceptions-and-request-failures"></a>Excepciones y errores de solicitud
Las excepciones no controladas se recopilan automáticamente:

![](./media/app-insights-java-eclipse/21-exceptions.png)

toocollect datos en otras excepciones, tienes dos opciones:

* [Insertar llamadas tooTrackException en su código](app-insights-api-custom-events-metrics.md#trackexception).
* [Instalar agente Java hello en el servidor](app-insights-java-agent.md). Especificar métodos de Hola que desee toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Supervisión de llamadas a métodos y dependencias externas
[Instalar agente Java hello](app-insights-java-agent.md) toolog especifica métodos internos y las llamadas realizadas a través de JDBC, con datos de tiempo.

## <a name="performance-counters"></a>Contadores de rendimiento
En la hoja de información general, desplácese hacia abajo y haga clic en hello **servidores** icono. Verá diferentes contadores de rendimiento.

![Desplácese hacia abajo del icono de servidores de hello tooclick](./media/app-insights-java-eclipse/11-perf-counters.png)

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

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Contadores de rendimiento de Unix
* [Instalar collectd con el complemento de Application Insights hello](app-insights-java-collectd.md) tooget una amplia variedad de datos del sistema y de red.

## <a name="availability-web-tests"></a>Pruebas web de disponibilidad
Application Insights pueden probar su sitio Web en intervalos regulares toocheck que está en funcionamiento y responder correctamente. [tooset una][availability], desplácese hacia abajo tooclick disponibilidad.

![Desplácese hacia abajo, haga clic en Disponibilidad y, a continuación, en Agregar prueba web](./media/app-insights-java-eclipse/31-config-web-test.png)

Obtendrá gráficos de tiempos de respuesta, junto con notificaciones por correo electrónico si su sitio deja de funcionar.

![Ejemplo de prueba web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

[Más información acerca de las pruebas web de disponibilidad.][availability]

## <a name="diagnostic-logs"></a>Registros de diagnóstico
Si usa Logback o Log4J (v1.2 o v2.0) para el seguimiento, puede que los registros de seguimiento que se envía automáticamente información que le permite explorar y buscar en ellos tooApplication.

[Más información sobre los registros de diagnóstico][javalogs]

## <a name="custom-telemetry"></a>Telemetría personalizada
Insertar unas pocas líneas de código en su toofind de aplicación web de Java a lo que hacen los usuarios con él o toohelp diagnosticar los problemas.

Puede insertar código en la página web JavaScript y en hello servidor Java.

[Obtenga información sobre la telemetría personalizad][track]

## <a name="next-steps"></a>Pasos siguientes
#### <a name="detect-and-diagnose-issues"></a>Detección y diagnóstico de problemas
* [Agregar telemetría de cliente web] [ usage] tooget telemetría de rendimiento de cliente web de Hola.
* [Configurar las pruebas web] [ availability] toomake seguro de la aplicación permanece en vivo y capacidad de respuesta.
* [Buscar eventos y registros] [ diagnostic] toohelp diagnosticar problemas.
* [Captura de los seguimientos Log4J o Logback][javalogs]

#### <a name="track-usage"></a>Seguir el uso
* [Agregar telemetría de cliente web] [ usage] toomonitor página vistas y las métricas de usuario básica.
* [Realizar un seguimiento de eventos personalizados y las métricas](app-insights-web-track-usage.md) toolearn acerca de cómo se utiliza la aplicación, tanto en el cliente de Hola y el servidor de Hola.

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
