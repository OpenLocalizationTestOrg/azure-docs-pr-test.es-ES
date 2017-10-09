---
title: "aaaAzure aplicación visión instantánea depurador para las aplicaciones de .NET | Documentos de Microsoft"
description: "Depuración de las instantáneas que se recopilan automáticamente cuando se producen excepciones en aplicaciones de producción de .NET"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a>Depurar instantáneas cuando se producen excepciones en aplicaciones de .NET

Cuando se produce una excepción, puede recopilar automáticamente una instantánea de depuración desde la aplicación web activa. instantánea de Hello muestra el estado de Hola de código fuente y variables Hola momento Hola mensaje de excepción lanzada. Hola instantánea depurador (versión preliminar) en [Azure Application Insights](app-insights-overview.md) supervisa la telemetría de excepción de la aplicación web. Recopila instantáneas en las parte superior: iniciar excepciones para que tenga información de Hola que necesita toodiagnose problemas en producción. Incluir hello [paquete de NuGet del compilador instantánea](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) en la aplicación y, opcionalmente, configurar los parámetros de recopilación en [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Las instantáneas aparecen en [excepciones](app-insights-asp-net-exceptions.md) en el portal de Application Insights Hola.

Puede ver instantáneas de depuración en la pila de llamadas de Hola Hola toosee portal e inspeccionar las variables en cada marco de pila de llamadas. una experiencia de depuración más eficaz con el código fuente, abra instantáneas con Visual Studio Enterprise de 2017 por tooget [descargar la extensión del depurador de instantánea de Hola para Visual Studio](https://aka.ms/snapshotdebugger).

La recopilación de instantáneas está disponible para:
* Aplicaciones de .NET Framework y ASP.NET que ejecuten .NET Framework 4.5 o posterior.
* Aplicaciones de .NET Core 2.0 y ASP.NET Core 2.0 que se ejecuten en Windows.

### <a name="configure-snapshot-collection-for-aspnet-applications"></a>Configurar la recopilación de instantáneas para aplicaciones ASP.NET

1. [Habilite Application Insights en su aplicación web](app-insights-asp-net.md), si aún no lo ha hecho.

2. Incluir hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) paquete de NuGet en la aplicación. 

3. Revisar opciones predeterminadas de Hola que Hola paquete agregado demasiado[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. Las instantáneas se recopilan sólo en las excepciones que son notificados tooApplication visión. En algunos casos (por ejemplo, versiones anteriores de la plataforma .NET de hello), puede que tenga demasiado[configurar la recopilación de excepción](app-insights-asp-net-exceptions.md#exceptions) toosee excepciones con las instantáneas en el portal de Hola.


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a>Configurar la recopilación de instantáneas para aplicaciones ASP.NET Core 2.0

1. [Habilite Application Insights en su aplicación web ASP.NET Core](app-insights-asp-net-core.md), si aún no lo ha hecho.

2. Incluir hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) paquete de NuGet en la aplicación.

3. Modificar hello `ConfigureServices` método de la aplicación `Startup` clase procesador de telemetría del recopilador de tooadd Hola instantánea. debe agregar el código de Hello depende de la versión que se hace referencia de Hola de hello paquete Microsoft.ApplicationInsights.ASPNETCore NuGet.

   Para Microsoft.ApplicationInsights.AspNetCore 2.1.0, agregue:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   Para Microsoft.ApplicationInsights.AspNetCore 2.1.1, agregue:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a>Configurar la recopilación de instantáneas para otras aplicaciones .NET

1. Si la aplicación ya no está instrumentada con Application Insights, empezar por [habilitar Application Insights y clave de instrumentación de configuración hello](app-insights-windows-desktop.md).

2. Agregar hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) paquete de NuGet en la aplicación.

3. Las instantáneas se recopilan sólo en las excepciones que son notificados tooApplication visión. Puede que necesite toomodify su tooreport código ellos. código de control de excepciones de Hello depende de la estructura de saludo de la aplicación, pero es un ejemplo a continuación:
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a>Concesión de permisos

Los propietarios de hello suscripción de Azure pueden inspeccionar las instantáneas. Otros usuarios deben obtener permiso de un propietario.

permiso de toogrant, asignar Hola `Application Insights Snapshot Debugger` toousers de rol que inspeccionará las instantáneas. Esta función se puede asignar tooindividual a los usuarios o grupos por propietarios de suscripciones de recurso de información de la aplicación de destino de Hola o su grupo de recursos o suscripción.

1. Abra la hoja de Control de acceso (IAM) de Hola.
1. Haga clic en Hola + botón Agregar.
1. Seleccione a depurador de instantánea de información de aplicación de lista desplegable de hello Roles.
1. Buscar y escriba un nombre para hello tooadd de usuario.
1. Haga clic en función de hello guardar botón tooadd Hola usuario toohello.


[!IMPORTANT]
    Las instantáneas pueden contener información personal y otra información confidencial en valores de variables y parámetros.

## <a name="debug-snapshots-in-hello-application-insights-portal"></a>Depurar las instantáneas en el portal de Application Insights Hola

Si una instantánea está disponible para una determinada excepción o un Id. del problema, un **Abrir instantánea depurar** botón se muestra en hello [excepción](app-insights-asp-net-exceptions.md) en el portal de Application Insights Hola.

![Botón Abrir instantánea de depuración de la excepción](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

Hola vista de instantánea de depurar, verá una pila de llamadas y un panel de variables. Cuando se selecciona marcos de llamada de Hola se apilan en el panel de pila de llamadas de hello, puede ver las variables locales y parámetros de dicha función llame a en el panel de variables de Hola.

![Vista de depuración instantánea en el portal de Hola](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

Las instantáneas pueden contener información confidencial y, de forma predeterminada, no están visibles. tooview instantáneas, debe tener hello `Application Insights Snapshot Debugger` tooyou rol asignado.

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a>Depuración de instantáneas con Visual Studio Enterprise 2017
1. Haga clic en hello **descargar instantánea** toodownload botón un `.diagsession` archivo, que puede abrirse en Visual Studio Enterprise de 2017. 

2. Hola tooopen `.diagsession` archivo, primero debe [descargar e instalar la extensión del depurador de instantánea de Hola para Visual Studio](https://aka.ms/snapshotdebugger).

3. Después de abrir el archivo de instantánea de hello, aparece la página de depuración de minivolcado de hello en Visual Studio. Haga clic en **depurar código administrado** toostart depuración instantánea Hola. instantánea de Hello abre toohello línea de código donde se inició la excepción de Hola para que se puede depurar el estado actual de hello del proceso de Hola.

    ![Visualización de la instantánea de depuración en Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

Hola descargado instantánea contiene los archivos de símbolos que se encontraron en el servidor de aplicaciones web. Estos archivos de símbolos son datos de instantánea tooassociate necesarios con el código fuente. Para las aplicaciones de servicio de aplicaciones, asegúrese de implementación de símbolos tooenable seguro al publicar las aplicaciones web.

## <a name="how-snapshots-work"></a>Funcionamiento de las instantáneas

Cuando se inicia la aplicación, se crea un proceso independiente de usuario de carga de instantáneas que supervisa las solicitudes de instantáneas de la aplicación. Cuando se solicita una instantánea, se realiza una instantánea de hello ejecutando el proceso en unos 10 minutos de too20. a continuación, se analiza el proceso de instantáneas de Hello y una instantánea se crea mientras continúa el proceso principal de hello toorun sirven para toousers de tráfico. Hello instantánea es cargado tooApplication visión junto con los archivos pertinentes símbolos (.pdb) que necesita tooview instantánea Hola.

## <a name="current-limitations"></a>Limitaciones actuales

### <a name="publish-symbols"></a>Publicación de símbolos
Hola instantánea depurador requiere archivos de símbolos en variables de toodecode de servidor de producción de hello y tooprovide una experiencia de depuración en Visual Studio. versión de Hola 15,2 de Visual Studio de 2017 publica símbolos para versiones de lanzamiento de forma predeterminada cuando se publique tooApp servicio. En las versiones anteriores, necesita tooadd Hola siguiente perfil de publicación de la línea tooyour `.pubxml` de archivos para que los símbolos se publican en modo de lanzamiento:

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

Para el cálculo de Azure y otros tipos, asegúrese de que los archivos de símbolos de Hola Hola misma carpeta del archivo .dll de aplicación principal de hello (normalmente, `wwwroot/bin`) o están disponibles en la ruta de acceso actual de Hola.

### <a name="optimized-builds"></a>Compilaciones optimizadas
En algunos casos, las variables locales no pueda visualizarse en versiones de lanzamiento debido a optimizaciones que se aplican durante el proceso de compilación de Hola.

## <a name="troubleshooting"></a>Solución de problemas

Estas sugerencias de ayudarán para solucionar problemas con hello depurador de instantánea.

### <a name="verify-hello-instrumentation-key"></a>Compruebe la clave de instrumentación de Hola

Asegúrese de que está utilizando la clave de instrumentación correcta de hello en la aplicación publicada. Por lo general, Application Insights lee clave de instrumentación de Hola Hola ApplicationInsights.config archivo. Compruebe que el valor de hello es Hola igual como clave de instrumentación de hello para el recurso de Application Insights de Hola que aparece en el portal de Hola.

### <a name="check-hello-uploader-logs"></a>Compruebe los registros de cargador de Hola

Después de crear una instantánea, se crea un archivo de minivolcado (.dmp) en el disco. Un proceso independiente de la herramienta de envío toma ese archivo de minivolcado y lo carga, junto con los archivos PDB asociados, tooApplication almacenamiento de visión instantánea depurador. Una vez minivolcado Hola ha cargado correctamente, se elimina del disco. archivos de registro de Hello de cargador de minivolcado Hola se conservan en disco. En un entorno de App Service, puede encontrar estos registros en `D:\Home\LogFiles\Uploader_*.log`. Sitio de administración de uso hello Kudu para el servicio de aplicaciones toofind estos archivos de registro.

1. Abra la aplicación de servicio de aplicaciones en hello portal de Azure.

2. Seleccione hello **herramientas avanzadas** hoja o buscar **Kudu**.
3. Haga clic en **Ir**.
4. Hola **consola de depuración** cuadro de lista desplegable, seleccione **CMD**.
5. Haga clic en **LogFiles**.

Debería ver al menos un archivo con un nombre que comienza con `Uploader_` y una extensión `.log`. Haga clic en toodownload de icono adecuado de hello los archivos de registro o abrirlos en un explorador.
nombre de archivo de Hello incluye el nombre del equipo de Hola. Si la instancia de App Service se hospeda en más de un equipo, hay archivos de registro independientes para cada equipo. Cuando el cargador de hello detecta un nuevo archivo de minivolcado, se registra en el archivo de registro de hello. Este es un ejemplo de carga correcta:

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

En el ejemplo anterior de hello, es la clave de instrumentación de hello `c12a605e73c44346a984e00000000000`. Este valor debe coincidir con la clave de instrumentación de hello para la aplicación.
minivolcado Hola está asociado a una instantánea con el Id. de hello `139e411a23934dc0b9ea08a626db16c5`. Puede utilizar este identificador posterior hello toolocate asociados telemetría de excepción en el análisis de visión de aplicaciones.

cargador de Hello busca archivos PDB nuevo una vez cada 15 minutos. Este es un ejemplo:

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

Para las aplicaciones que son _no_ hospedado en el servicio de aplicaciones, los registros de cargador de hello están en hello misma carpeta que minivolcados de hello: `%TEMP%\Dumps\<ikey>` (donde `<ikey>` es la clave de instrumentación).

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a>Use Application Insights buscar excepciones toofind con instantáneas

Cuando se crea una instantánea, Hola producir la excepción se etiqueta con un identificador de instantánea. Una vez telemetría de excepción de hello tooApplication notificado visión, ese identificador de la instantánea se incluye como una propiedad personalizada. Hoja de búsqueda de hello en Application Insights, puede utilizar para buscar todos los telemetría con hello `ai.snapshot.id` propiedad personalizada.

1. Buscar recursos de Application Insights tooyour Hola portal de Azure.
2. Haga clic en **Buscar**.
3. Tipo `ai.snapshot.id` en Hola cuadro de texto Buscar y presione ENTRAR.

![Búsqueda de telemetría con un identificador de la instantánea en el portal de Hola](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

Si esta búsqueda no devuelve ningún resultado, no hay instantáneas eran visión tooApplication notificado para su aplicación en el intervalo de tiempo de hello seleccionado.

toosearch para un identificador de la instantánea específico de registros de cargador de hello, escriba ese identificador en el cuadro de búsqueda de Hola. Si no se encuentra la telemetría para una instantánea que sabe que se cargó, siga estos pasos:

1. Compruebe que está viendo en el recurso de Application Insights derecho Hola comprobando clave de instrumentación de Hola.

2. Al usar Hola marca de tiempo de registro de cargador de hello, ajustar filtro de intervalo de tiempo de Hola de hello búsqueda toocover ese intervalo de tiempo.

Si aún no ve una excepción con ese identificador de la instantánea, excepción de telemetría de hello no estaba incluido tooApplication visión. Esta situación puede ocurrir si se bloqueó la aplicación después de que tomó la instantánea de hello, pero para que notifique telemetría de excepción de Hola. En este caso, compruebe Hola inicia el servicio de aplicaciones con `Diagnose and solve problems` toosee si hubiera inesperado se reinicia o las excepciones no controladas.

## <a name="next-steps"></a>Pasos siguientes

* [Establecer snappoints en el código](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget instantáneas sin tener que esperar una excepción.
* [Diagnosticar las excepciones en las aplicaciones web](app-insights-asp-net-exceptions.md) explica cómo toomake tooApplication visible de excepciones más información. 
* [Detección inteligente](app-insights-proactive-diagnostics.md) detecta automáticamente las anomalías de rendimiento.
