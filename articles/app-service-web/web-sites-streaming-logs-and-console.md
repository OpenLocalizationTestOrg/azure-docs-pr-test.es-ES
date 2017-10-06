---
title: registros de aaaStreaming y la consola
description: "Información general de la consola y los registros de transmisión"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a>Hello consola y los registros de streaming
## <a name="streaming-logs"></a>Registros de transmisión
Hola **portal de Azure** proporciona un visor de registro de transmisión por secuencias integrado que le permite ver los eventos de seguimiento de su **servicio de aplicaciones** aplicaciones en tiempo real.  

Configurar esta característica requiere algunos pasos sencillos:

* Escritura de seguimientos en el código.
* Habilitación de **registros de diagnósticos** de aplicación para la aplicación
* Secuencia de Hola de vista de integradas de hello **registros de Streaming** interfaz de usuario en hello **portal de Azure**.

### <a name="how-toowrite-traces-in-your-code"></a>¿Cómo realiza el seguimiento de toowrite en el código
La escritura de seguimientos en el código es sencilla.  En C# es tan fácil como escribir el siguiente código de hello:

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

Hola clase Trace reside en el espacio de nombres de hello System.Diagnostics.

Puede escribir este código en una aplicación node.js tooachieve Hola el mismo resultado:

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a>¿Cómo tooenable y vista Hola registros de streaming
![][BrowseSitesScreenshot] El diagnóstico se habilita por aplicación. Comience por explorar sitio toohello que le gustaría tooenable esta característica en.  

![][DiagnosticsLogs]En el menú de configuración, desplácese hacia abajo toohello **supervisión** sección y haga clic en **(1) registros de diagnóstico**. A continuación, **enable (2)** **(Filesystem) de registro de aplicaciones** o **(blob) de registro de aplicaciones** hello **nivel** opción permite cambiar Hola nivel de gravedad de seguimientos toocapture. Si simplemente está tratando de tooget familiarizado con la característica de hello, establecer el nivel de hello demasiado**detallado** tooensure todas las instrucciones de seguimiento se recopilan.

Haga clic en **guardar** princip Hola de hoja de Hola y está listo tooview registros.

> [!NOTE]
> Hola Hola superior **nivel de gravedad** hello más recursos son consumido toolog y Hola se producen varios seguimientos. Asegúrese de que **nivel de gravedad** está configurado toohello detalle correcto para un sitio de mucho tráfico o de producción. 
> 
> 

![][StreamingLogsScreenshot]Hola tooview **los registros de streaming** desde dentro de hello portal de Azure, haga clic en **secuencia de registro (1)** también en hello **supervisión** sección del menú de configuración de Hola. Si la aplicación está escribiendo activamente las instrucciones de seguimiento, debería ver Hola **(2) de transmisión por secuencias registra la interfaz de usuario** casi en tiempo real.

## <a name="console"></a>Consola
Hola **portal de Azure** proporciona la aplicación de consola acceso tooyour. Puede explorar el sistema de archivos de la aplicación y ejecutar los scripts de cmd/powershell. Se enlazan por hello mismos permisos establecidos como la ejecución de código de aplicación al ejecutar comandos de la consola. Directorios de tooprotected de acceso o ejecutar scripts que requieren permisos elevados está bloqueado.  

![][ConsoleScreenshot]En el menú de configuración, desplácese hacia abajo demasiado**herramientas de desarrollo** sección y haga clic en **(1) consola** hello y **(2) consola** toohello derecha abre la interfaz de usuario.

tooget familiarizado con hello **consola**, intente comandos básicos, como:

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
