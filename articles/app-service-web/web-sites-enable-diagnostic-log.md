---
title: "registro de diagnósticos de aaaEnable para las aplicaciones web en el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo tooenable el registro de diagnóstico y Agregar aplicación de tooyour de instrumentación, así como la tooaccess Hola información registrada por Azure."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: c9da27b2-47d4-4c33-a3cb-1819955ee43b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b2903ff31cc93180552cf51196c33505ffbaf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a>Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure
## <a name="overview"></a>Información general
Azure proporciona diagnósticos integrados tooassist con la depuración de un [aplicación de servicio de aplicaciones web](http://go.microsoft.com/fwlink/?LinkId=529714). En este artículo aprenderá cómo tooenable el registro de diagnóstico y Agregar aplicación de tooyour de instrumentación, así como la tooaccess Hola información registrada por Azure.

En este artículo usa hello [Portal de Azure](https://portal.azure.com), PowerShell de Azure y hello toowork de interfaz de línea de comandos (CLI de Azure) de Azure con registros de diagnóstico. Para obtener información acerca de cómo trabajar con registros de diagnóstico mediante Visual Studio, consulte [Solución de problemas de Azure en Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="whatisdiag"></a>Diagnóstico del servidor web y diagnóstico de aplicaciones
Aplicaciones de servicio de aplicaciones web proporcionan funcionalidad de diagnóstico para registrar información de servidor web de Hola y de aplicación web de hello. De forma lógica, estos diagnósticos se dividen en **diagnósticos del servidor web** y **diagnóstico de aplicaciones**.

### <a name="web-server-diagnostics"></a>Diagnósticos del servidor web
Puede habilitar o deshabilitar Hola siguientes tipos de registros:

* **Registro de errores detallado** : registra información detallada de errores para códigos de estado HTTP que indican un problema (código de estado 400 o superior). Esto puede contener información que puede ayudar a determinar por qué servidor de hello devolvió el código de error de Hola.
* **Error de seguimiento de solicitudes con** -información detallada sobre las solicitudes con error, incluidos un seguimiento de hello IIS componentes utilizados tooprocess Hola solicitud y la hora de hello realizada en cada componente. Esto puede resultar útil si está tratando de rendimiento del sitio tooincrease o aislar la causa de que un toobe específico de error HTTP devuelto.
* **Registro del servidor Web** -obtener información acerca de las transacciones HTTP mediante hello [formato de archivo de registro extendido W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Esto es útil al determinar las métricas generales de sitio como el número de Hola de las solicitudes administradas o cuántas solicitudes provienen de una dirección IP específica.

### <a name="application-diagnostics"></a>diagnósticos de la aplicación
Diagnóstico de aplicaciones permite información toocapture generado por una aplicación web. Las aplicaciones de ASP.NET pueden usar hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) el registro de diagnósticos de aplicación de clase toolog información toohello. Por ejemplo:

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

En tiempo de ejecución puede recuperar estos toohelp registros a solucionar el problema. Para obtener más información, consulte [Solución de problemas de aplicaciones web de Azure en Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

Aplicaciones de servicio de aplicaciones web también registrar información sobre la implementación al publicar la aplicación web de contenido tooa. Esta acción se lleva a cabo automáticamente, por lo que no es necesario realizar ninguna configuración para el registro de implementaciones. Registro de implementación le permite toodetermine motivo del error de una implementación. Por ejemplo, si se usa un script de implementación personalizada, podría usar toodetermine de registro de implementación ¿por qué se producen errores en script de Hola.

## <a name="enablediag"></a>¿Cómo tooenable diagnóstico
Diagnósticos de tooenable en hello [Portal de Azure](https://portal.azure.com), toohello hoja de la aplicación web y haga clic en **configuración > registros de diagnóstico**.

<!-- todo:cleanup dogfood addresses in screenshot -->
![Parte de los registros](./media/web-sites-enable-diagnostic-log/logspart.png)

Cuando se habilita **diagnósticos de la aplicación** también elegir hello **nivel**. Esta configuración le permite obtener información de hello toofilter capturada demasiado**informativo**, **advertencia** o **error** información. Si se establece demasiado**detallado** registrará toda la información generada por la aplicación hello.

> [!NOTE]
> A diferencia de cambio de hello web.config archivo, habilitar los diagnósticos de aplicación o cambiar los niveles de registro de diagnóstico no recicla dominio de aplicación de Hola Hola aplicación se ejecuta dentro.
>
>

Hola [portal clásico](https://manage.windowsazure.com) aplicación Web **configurar** ficha, puede seleccionar **almacenamiento** o **sistema de archivos** para **servidor web Registro**. Seleccionar **almacenamiento** permite tooselect una cuenta de almacenamiento y, a continuación, en un contenedor de blobs Hola registros se escribirán en. Todos los demás registros para **diagnósticos de sitio** se escriben toohello solo sistema de archivos.

Hola [portal clásico](https://manage.windowsazure.com) aplicación Web **configurar** ficha también tiene configuraciones adicionales para application diagnostics:

* **Sistema de archivos** -Hola de almacenes de sistema de archivos aplicación web de toohello de la información de diagnósticos de aplicación. Estos archivos se pueden obtener acceso a FTP o descargó como un archivo Zip con hello Azure PowerShell o la interfaz de línea de comandos de Azure (Azure CLI).
* **Almacenamiento de tablas** -Hola de almacenes de información de diagnóstico de aplicación con el nombre de cuenta de almacenamiento de Azure y tabla especificado Hola.
* **Almacenamiento de blobs** -Hola de almacenes de información de diagnóstico de la aplicación en el contenedor especificado de cuenta de almacenamiento de Azure y blob Hola.
* **Período de retención**: de manera predeterminada, los registros no se eliminan automáticamente del **almacenamiento de blobs**. Seleccione **de retención establecido** y escriba Hola número de días tookeep registros si desea tooautomatically eliminarán registros.

> [!NOTE]
> Si se [regenerar claves de acceso de la cuenta de almacenamiento](../storage/common/storage-create-storage-account.md), debe restablecer claves de configuración que Hola registro respectivos toouse Hola actualizado. toodo esto:
>
> 1. Hola **configurar** , configure la característica de registro correspondiente de Hola demasiado**desactivar**. Guarde la configuración.
> 2. Habilitar registro toohello blob de la cuenta de almacenamiento o una tabla de nuevo. Guarde la configuración.
>
>

Cualquier combinación de sistema de archivos, el almacenamiento de tablas o almacenamiento de blobs puede habilitarse en hello al mismo tiempo y tienen configuraciones de nivel de registro individuales. Por ejemplo, es recomendable toolog errores y advertencias del almacenamiento de tooblob como una solución a largo plazo de registro, al habilitar el registro del sistema de archivos con un nivel de detallado.

Mientras que las tres ubicaciones de almacenamiento ofrecen Hola misma información básica de los eventos registrados, **almacenamiento de tablas** y **almacenamiento de blobs** registrar información adicional como Id. de instancia de hello, Id. de subproceso y más marca de tiempo específico (formato de graduación) de registro demasiado**sistema de archivos**.

> [!NOTE]
> Solo se puede obtener acceso a la información almacenada en **table storage** o **blob storage** mediante una aplicación o un cliente de almacenamiento que puedan trabajar directamente con estos sistemas de almacenamiento. Por ejemplo, Visual Studio 2013 contiene un explorador de almacenamiento que pueden ser utilizados tooexplore tabla o almacenamiento de blobs y HDInsight puede tener acceso a los datos almacenados en almacenamiento de blobs. También puede escribir una aplicación que tiene acceso a almacenamiento de Azure mediante uno de hello [Azure SDK](/downloads/#).
>
> [!NOTE]
> También pueden habilitarse diagnósticos de Azure PowerShell con hello **AzureWebsite conjunto** cmdlet. Si no ha instalado Azure PowerShell o no lo ha configurado toouse su suscripción de Azure, consulte [cómo tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

## <a name="download"></a> Descarga de registros
Sistema de archivos de aplicación web de información de diagnóstico almacenada toohello puede tener acceso directamente mediante FTP. También se puede descargar como un archivo Zip con Azure PowerShell o hello interfaz de línea de comandos de Azure.

estructura de directorios de Hola Hola registros se almacenan en es como sigue:

* **Registros de aplicaciones** : /LogFiles/Application/. Esta carpeta contiene uno o varios archivos de texto con información generada por el registro de aplicaciones.
* **Seguimientos de solicitudes con error** : /LogFiles/W3SVC#########/. Esta carpeta contiene un archivo XSL y uno o varios archivos XML. Asegúrese de que descargar archivo XSL de hello en hello mismo directorio que Hola que XML archivo porque el archivo XSL de hello proporciona funcionalidad para dar formato y filtrar el contenido de Hola de hello XML archivos cuando se ve en Internet Explorer.
* **Registros detallados de errores** : /LogFiles/DetailedErrors/. Esta carpeta contiene uno o varios archivos .htm con información amplia de todos los errores HTTP que se han producido.
* **Registros de servidor web** : /LogFiles/http/RawLogs. Esta carpeta contiene uno o varios archivos de texto con formato mediante hello [formato de archivo de registro extendido W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
* **Registros de implementaciones** : /LogFiles/Git. Esta carpeta contiene los registros generados por procesos de implementación interna de hello utilizados por aplicaciones web de Azure, así como los registros para las implementaciones de Git.

### <a name="ftp"></a>FTP
información de diagnóstico de tooaccess con FTP, visite hello **panel** de la aplicación web en hello [portal clásico](https://manage.windowsazure.com). Hola **vista rápida** sección, utilice hello **registros de diagnóstico FTP** vincular archivos de registro de hello tooaccess mediante FTP. Hola **usuario de implementación/FTP** entrada muestra el nombre de usuario de Hola que debe ser el sitio de hello FTP tooaccess usado.

> [!NOTE]
> Si hello **usuario de implementación/FTP** no se establece la entrada, o ha olvidado la contraseña de Hola para este usuario, puede crear un nuevo usuario y una contraseña mediante hello **Restablecer credenciales de implementación** vínculo Hola **vista rápida** sección de hello **panel**.
>
>

### <a name="download-with-azure-powershell"></a>Descarga con Azure PowerShell
archivos de registro de hello toodownload, inicie una nueva instancia de PowerShell de Azure y usar hello siguiente comando:

    Save-AzureWebSiteLog -Name webappname

Esto guardará los registros de hello para la aplicación web de hello especificado por hello **-nombre** archivo tooa de parámetro denominado **logs.zip** en el directorio actual de Hola.

> [!NOTE]
> Si no ha instalado Azure PowerShell o no lo ha configurado toouse su suscripción de Azure, consulte [cómo tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="download-with-azure-command-line-interface"></a>Descarga con la interfaz de la línea de comandos de Azure
archivos de registro de hello toodownload mediante Hola interfaz de línea de comandos de Azure, abra un nuevo símbolo, PowerShell, intensiva de errores o sesión de Terminal y escriba el siguiente comando de hello:

    azure site log download webappname

Esto guardará los registros de hello para la aplicación web de hello denominado 'webappname' tooa archivo denominado **diagnostics.zip** en el directorio actual de Hola.

> [!NOTE]
> Si no ha instalado Hola interfaz de línea de comandos de Azure (Azure CLI), o no lo ha configurado toouse su suscripción de Azure, consulte [cómo tooUse CLI de Azure](../cli-install-nodejs.md).
>
>

## <a name="how-to-view-logs-in-application-insights"></a>Visualización de registros en Application Insights
Application Insights Visual Studio proporciona herramientas para el filtrado y búsqueda de registros y para establecer correlaciones entre registros Hola con las solicitudes y otros eventos.

1. Agregar proyecto de tooyour de Application Insights SDK hello en Visual Studio.
   * En el Explorador de soluciones, haga clic con el botón secundario en el proyecto y elija Agregar Application Insights. Se le guiará a través de pasos que incluyen la creación de un recurso de Application Insights. [Más información](../application-insights/app-insights-asp-net.md)
2. Agregar proyecto de tooyour de paquete de agente de escucha de seguimiento de Hola.
   * Haga clic con el botón secundario en el proyecto y elija Administrar paquetes de NuGet. Seleccione `Microsoft.ApplicationInsights.TraceListener` [Más información](../application-insights/app-insights-asp-net-trace-logs.md)
3. Cargar el proyecto y ejecútelo toogenerate los datos de registro.
4. Hola [Portal de Azure](https://portal.azure.com/), busque tooyour nuevo recurso de Application Insights y abra **búsqueda**. Verá los datos de registro, junto con la solicitud, el uso y otra telemetría. Algunos telemetría puede tardar unos tooarrive minutos: haga clic en actualizar. [Más información](../application-insights/app-insights-diagnostic-search.md)

[Obtenga más información acerca del seguimiento del rendimiento con Application Insights](../application-insights/app-insights-azure-web-apps.md)

## <a name="streamlogs"></a> Registros
Al desarrollar una aplicación, a menudo resulta útil toosee registrar información en tiempo casi real. Esto puede realizarse mediante el streaming de entorno de desarrollo de tooyour registro información mediante Azure PowerShell u Hola interfaz de línea de comandos de Azure.

> [!NOTE]
> Algunos tipos de búfer de registro escriben archivo de registro de toohello, que puede provocar eventos fuera de servicio de flujo de Hola. Por ejemplo, una entrada del registro de aplicación que se produce cuando un usuario visita una página puede mostrarse en secuencia Hola antes de la entrada de registro HTTP correspondiente de hello para la solicitud de página Hola.
>
> [!NOTE]
> Transmisión por secuencias de registro también se transmiten información que se escribe el archivo de texto de tooany almacenado en hello **D:\\principal\\LogFiles\\**  carpeta.
>
>

### <a name="streaming-with-azure-powershell"></a>Transmisión con Azure PowerShell
información de registro de toostream, inicie una nueva instancia de PowerShell de Azure y usar hello siguiente comando:

    Get-AzureWebSiteLog -Name webappname -Tail

Así, conectará toohello web app especificado por hello **-nombre** parámetro e iniciar la transmisión por secuencias de ventana de PowerShell de toohello de información cuando se producen eventos de registro en la aplicación web de Hola. Cualquier información escrita toofiles termina .txt, .log o .htm que se almacenan en el directorio de hello /LogFiles (d:/principal/logfiles) se transmitirá toohello de consola local.

toofilter los eventos específicos, como los errores, usan hello **-mensaje** parámetro. Por ejemplo:

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

tipos de registro específicos de toofilter, como HTTP, utilizan hello **-ruta de acceso** parámetro. Por ejemplo:

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

toosee una lista de rutas de acceso disponibles, utilice hello - ListPath parámetro.

> [!NOTE]
> Si no ha instalado Azure PowerShell o no lo ha configurado toouse su suscripción de Azure, consulte [cómo tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="streaming-with-azure-command-line-interface"></a>Transmisión con la interfaz de la línea de comandos de Azure
información de registro de toostream, abrir un nuevo símbolo, PowerShell, intensiva de errores o una sesión de Terminal y escriba el siguiente comando de hello:

    azure site log tail webappname

Esto conectará toohello web app con el nombre 'webappname' y empezar a transmitir toohello ventana de información cuando se producen eventos de registro en la aplicación web de Hola. Cualquier información escrita toofiles termina .txt, .log o .htm que se almacenan en el directorio de hello /LogFiles (d:/principal/logfiles) se transmitirá toohello de consola local.

toofilter los eventos específicos, como los errores, usan hello **--filtro** parámetro. Por ejemplo:

    azure site log tail webappname --filter Error

tipos de registro específicos de toofilter, como HTTP, utilizan hello **: ruta de acceso** parámetro. Por ejemplo:

    azure site log tail webappname --path http

> [!NOTE]
> Si no ha instalado Hola interfaz de línea de comandos de Azure, o no lo ha configurado toouse su suscripción de Azure, consulte [cómo tooUse interfaz de línea de comandos de Azure](../cli-install-nodejs.md).
>
>

## <a name="understandlogs"></a> Información sobre los registros de diagnóstico
### <a name="application-diagnostics-logs"></a>Registros de diagnóstico de aplicaciones
Diagnósticos de la aplicación almacena información en un formato concreto para aplicaciones. NET, dependiendo de si almacenar registros toohello sistema de archivos, almacenamiento de tabla, o almacenamiento de blobs. conjunto básico de Hola de los datos almacenados es Hola igual a través de los tres tipos de almacenamiento: se ha producido el evento de Hola de fecha y hora de hello, Id. de proceso de Hola que generó el evento de hello, tipo de evento de hello (información, advertencia, error) y mensajes de bienvenida del evento.

**Sistema de archivos**

Cada línea registrado toohello sistema de archivos o recibidos mediante transmisión por secuencias será Hola siguiendo el formato siguiente:

    {Date}  PID[{process id}] {event type/level} {message}

Por ejemplo, un evento de error será similar siguiente toohello siguiente:

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on hello page!

Toohello sistema de archivos de registro, proporciona información más básica de Hola de hello tres métodos disponibles, lo que proporciona solo el tiempo de hello, el Id. de proceso, el nivel de evento y el mensaje.

**Almacenamiento de tablas**

Al iniciar una sesión de almacenamiento tootable, propiedades adicionales son utilizado toofacilitate buscar datos Hola almacenados en la tabla de hello, así como información más detallada en el evento Hola. Hello siguientes propiedades (columnas) se utilizan para cada entidad (fila) que se almacenan en la tabla de Hola.

| Nombre de propiedad | Valor/formato |
| --- | --- |
| PartitionKey |Fecha y hora del evento de hello en formato Aaaammddhh |
| RowKey |Un valor de GUID que identifica a esta entidad de forma exclusiva |
| Timestamp |se produjeron Hola fecha y hora que Hola eventos |
| EventTickCount |Hola fecha y hora que Hola evento se ha producido, en formato de graduación (mayor precisión) |
| ApplicationName |nombre de la aplicación Hello |
| Nivel |Nivel del evento (por ejemplo, error, advertencia o información) |
| EventId |Id. de evento de Hola de este evento<p><p>Valor predeterminado es too0 si no hay ninguna especificada |
| InstanceId |Instancia de la aplicación web de hello que Hola incluso se produjo en |
| Pid |Identificador del proceso |
| Tid |Identificador de subproceso de Hola de subproceso de Hola que generó el evento de Hola |
| Message |Mensaje detallado del evento |

**Blob storage**

Al iniciar sesión tooblob almacenamiento, los datos se almacenan en formato de valores separados por comas (CSV). Almacenamiento tootable similar, campos adicionales son tooprovide registrado información más detallada acerca del evento Hola. Hello siguientes propiedades se utilizan para cada fila de hello CSV:

| Nombre de propiedad | Valor/formato |
| --- | --- |
| Date |se produjeron Hola fecha y hora que Hola eventos |
| Nivel |Nivel del evento (por ejemplo, error, advertencia o información) |
| ApplicationName |nombre de la aplicación Hello |
| InstanceId |Instancia de aplicación web de hello que Hola evento producido en |
| EventTickCount |Hola fecha y hora que Hola evento se ha producido, en formato de graduación (mayor precisión) |
| EventId |Id. de evento de Hola de este evento<p><p>Valor predeterminado es too0 si no hay ninguna especificada |
| Pid |Identificador del proceso |
| Tid |Identificador de subproceso de Hola de subproceso de Hola que generó el evento de Hola |
| Message |Mensaje detallado del evento |

datos de Hello almacenados en un blob sería similar siguiente toohello:

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> primera línea del registro de hello de Hello contiene encabezados de columna de hello como se representa en este ejemplo.
>
>

### <a name="failed-request-traces"></a>Seguimientos de solicitudes con error
El seguimiento de solicitudes con error se almacena en archivos XML con nombre **fr######.xml**. toomake lo más fácil de información de hello optimizado de tooview, una hoja de estilos XSL denominado **freb.xsl** se proporciona en hello mismo directorio como archivos XML de Hola. Uno de los archivos XML Hola abrir en Internet Explorer usará tooprovide de hoja de estilos XSL de hello una visualización con formato de información de seguimiento de Hola. Esta descripción aparecerá a continuación toohello similar:

![en el Explorador de Hola de solicitudes con error](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a>Registros detallados de errores
Los registros de error detallados son documentos HTML que ofrecen información más detallada sobre los errores HTTP que se han producido. Habida cuenta de que se trata sencillamente de documentos HTML, se pueden ver en un explorador web.

### <a name="web-server-logs"></a>Registros de servidor web
Hello registros de servidor web tienen el formato hello [formato de archivo de registro extendido W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Esta información se puede leer con un editor de texto o analizarse con utilidades como el [analizador del registro](http://go.microsoft.com/fwlink/?LinkId=246619).

> [!NOTE]
> Hello registros generados por las aplicaciones web de Azure no admiten hello **s-computername**, **s-ip**, o **cs-version** campos.
>
>

## <a name="nextsteps"></a> Pasos siguientes
* [¿Cómo tooMonitor las aplicaciones Web](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [Solución de problemas de aplicaciones web de Azure en Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md)
* [Análisis de registros de aplicación web en HDInsight](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
>
>

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)
* Para una toohello guía consulte cambio de toohello portal antiguo nuevo portal de hello: [Hola de referencia para navegar por el portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715)
