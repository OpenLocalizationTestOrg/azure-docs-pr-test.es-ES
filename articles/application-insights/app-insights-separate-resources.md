---
title: "telemetría aaaSeparating desde el desarrollo, prueba y suelte en Azure Application Insights | Documentos de Microsoft"
description: "Recursos de toodifferent de telemetría directa para que las marcas de desarrollo, prueba y producción."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a>Separación de la telemetría de desarrollo, prueba y producción

Cuando está desarrollando la próxima versión de Hola de una aplicación web, no desea toomix seguridad hello [Application Insights](app-insights-overview.md) telemetría de la nueva versión de hello y la versión de Hola ya publicado. tooavoid confusión, envío Hola telemetría de desarrollo diferentes fases tooseparate recursos de Application Insights, con claves de instrumentación independiente (ikeys). toomake sea más fácil toochange Hola Instrumental clave como una versión se mueve de una fase tooanother, puede ser útil tooset Hola ikey en el código en lugar de en el archivo de configuración de Hola. 

(Si el sistema es un servicio en la nube de Azure, hay [otra forma de configurar claves separadas](app-insights-cloudservices.md)).

## <a name="about-resources-and-instrumentation-keys"></a>Acerca de los recursos y las claves de instrumentación

Al configurar la supervisión de Application Insights para su aplicación web, se crea un *recurso* de Application Insights en Microsoft Azure. Abrir este recurso en el portal de Azure en orden toosee hello y analizar la telemetría de hello recopilada desde la aplicación. recursos de Hola se identifican mediante un *clave de instrumentación* (ikey). Cuando se instala Hola Application Insights empaquetarla toomonitor, configurarlo con clave de instrumentación de hello, para que sepa dónde toosend Hola telemetría.

Normalmente elija recursos independientes toouse o un único recurso compartido en escenarios diferentes:

* Aplicaciones independientes y diferentes: use un recurso y una clave iKey independientes para cada aplicación.
* Usar varios componentes o funciones de una sola aplicación comercial - un [único recurso compartido](app-insights-monitor-multi-role-apps.md) para todas las aplicaciones de componente de Hola. Puede filtrar o segmentada por propiedad de hello cloud_RoleName telemetría.
* Desarrollo y prueba, versión, usan un recurso independiente y ikey de versiones del sistema de hello en 'marca' o una fase de producción.
* Pruebas A/B: use un único recurso. Cree una tooadd TelemetryInitializer una telemetría de toohello de propiedad que identifica las variantes de Hola.


## <a name="dynamic-ikey"></a> Copia de la clave de instrumentación

toomake, facilitando la toochange Hola ikey como código de hello se mueve entre fases de producción, establézcala en el código en lugar de en el archivo de configuración de Hola.

Establezca la clave de hello en un método de inicialización, como global.aspx.cs en un servicio ASP.NET:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

En este ejemplo, hello ikeys para los distintos recursos de Hola se colocan en las diferentes versiones del archivo de configuración web de Hola. Archivo de configuración de web de hello intercambiando - lo que puede hacer como parte del script de la versión de Hola - intercambiará recurso de destino de Hola.

### <a name="web-pages"></a>Páginas web
Hola iKey también se utiliza en páginas web de la aplicación, en hello [secuencia de comandos que obtuvo en la hoja de inicio rápido de hello](app-insights-javascript.md). En lugar de codificar, literalmente en el script de Hola, generar desde el estado del servidor de Hola. Por ejemplo, en una aplicación ASP.NET:

*JavaScript en Razor*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a>Creación de recurso de Application Insights adicionales
tooseparate telemetría para los componentes de aplicación diferente o para marcas de tiempo diferentes (desarrollo/prueba/producción) de hello mismo componente, entonces tendrá toocreate un nuevo recurso de Application Insights.

Hola [portal.azure.com](https://portal.azure.com), agregar un recurso de información de la aplicación:

![Haga clic en Nuevo, Application Insights.](./media/app-insights-separate-resources/01-new.png)

* **Tipo de aplicación** afecta a lo que ve en la hoja de información general de Hola y Hola propiedades [explorer métrica](app-insights-metrics-explorer.md). Si no ve el tipo de aplicación, elija uno de los tipos de hello web para las páginas web.
* **grupo de recursos** resulta práctico para administrar propiedades como el  como el [control de acceso](app-insights-resources-roles-access-control.md)de Azure. Puede usar grupos de recursos independientes para desarrollo, prueba y producción.
* **suscripción** es su cuenta de pago de Azure.
* **ubicación** es donde se guardan los datos. Actualmente no se puede cambiar. 
* **Agregar toodashboard** coloca un icono de acceso rápido para el recurso en la página principal de Azure. 

Crear recursos de hello tarda unos segundos. Verá una alerta cuando esté listo.

(Puede escribir una [script de PowerShell](app-insights-powershell-script-create-resource.md) toocreate un recurso automáticamente.)

### <a name="getting-hello-instrumentation-key"></a>Obtener clave de instrumentación de Hola
clave de instrumentación de Hello identifica recursos de Hola que ha creado. 

![Haga clic en Essentials, haga clic en hello clave de instrumentación, CTRL + c.](./media/app-insights-separate-resources/02-props.png)

Se necesitan las claves de instrumentación de Hola de todos los toowhich de recursos de Hola la aplicación enviará los datos.

## <a name="filter-on-build-number"></a>Filtrado por número de compilación
Cuando se publica una nueva versión de la aplicación, le interesará telemetría de hello tooseparate capaz de toobe desde diferentes compilaciones.

Puede establecer la propiedad de versión de la aplicación hello para que pueda filtrar [búsqueda](app-insights-diagnostic-search.md) y [explorer métrica](app-insights-metrics-explorer.md) resultados.

![Filtrado según una propiedad](./media/app-insights-separate-resources/050-filter.png)

Existen varios métodos diferentes de establecer la propiedad de versión de la aplicación hello.

* Establezca directamente:

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* Ajustar esa línea en un [inicializador de telemetría](app-insights-api-custom-events-metrics.md#defaults) tooensure que todas las instancias de TelemetryClient se establecen de forma coherente.
* [ASP.NET] Establecer versión de hello en `BuildInfo.config`. módulo de Hello web recogerá versión Hola de nodo de BuildLabel Hola. Incluir este archivo en el proyecto y recordar tooset Hola copiar siempre propiedad el Explorador de soluciones.

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* [ASP.NET] Genere BuildInfo.config automáticamente en MSBuild. toodo, agregar algunas de las líneas de tooyour `.csproj` archivo:

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    Esto genera un archivo denominado *NombreDelProyecto*. Hola BuildInfo.config. proceso de publicación cambia su nombre tooBuildInfo.config.

    etiqueta de compilación de Hello contiene un marcador de posición (AutoGen_...) al compilar con Visual Studio. Pero cuando se compila con MSBuild, se rellena con el número de versión correcto de Hola.

    números de versión de MSBuild toogenerate tooallow, versión del juego de hello como `1.0.*` en AssemblyReference.cs

## <a name="version-and-release-tracking"></a>Versión y seguimiento de versiones
versión de la aplicación hello tootrack, asegúrese de que `buildinfo.config` generado por el proceso de Microsoft Build Engine. En su archivo .csproj, agregue:  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

Cuando tiene información de compilación de hello, agrega automáticamente el módulo de web Application Insights hello **versión de la aplicación** como un elemento de propiedad tooevery de telemetría. Que permite toofilter versión al realizar [búsquedas diagnóstico](app-insights-diagnostic-search.md), o cuando se [explorar métricas](app-insights-metrics-explorer.md).

Sin embargo, observe que el número de versión de compilación de Hola se genera solo por hello Microsoft Build Engine, no por el desarrollador de Hola se crean en Visual Studio.

### <a name="release-annotations"></a>Anotaciones de la versión
Si usa Visual Studio Team Services, puede [obtener un marcador de anotación](app-insights-annotations.md) agregan gráficos tooyour cada vez que publica una versión nueva. Hola siguiente imagen muestra la apariencia de este marcador.

![Captura de pantalla de la anotación de la versión de ejemplo en un gráfico](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a>Pasos siguientes

* [Recursos compartidos para varios roles](app-insights-monitor-multi-role-apps.md)
* [Crear un toodistinguish de inicializador de telemetría A | Variantes de B](app-insights-api-filtering-sampling.md#add-properties)
