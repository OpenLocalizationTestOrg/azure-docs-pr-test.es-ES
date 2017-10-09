---
title: "flujo de hello aaaTrace en una aplicación de servicios de nube con diagnósticos de Azure | Documentos de Microsoft"
description: "Agregar seguimiento mensajes tooan Azure toohelp la depuración de aplicaciones, medir el rendimiento, supervisión, análisis del tráfico y mucho más."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a>Flujo de Hola de seguimiento de una aplicación de servicios en la nube con diagnósticos de Azure
El seguimiento es una manera toomonitor Hola la ejecución de la aplicación mientras se está ejecutando. Puede usar hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), y [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) clases toorecord información sobre los errores y ejecución de la aplicación en registros, archivos de texto u otros dispositivos para su análisis posterior. Para obtener más información acerca del seguimiento, consulte [Seguimiento e instrumentación de aplicaciones](https://msdn.microsoft.com/library/zs6s4h68.aspx).

## <a name="use-trace-statements-and-trace-switches"></a>Uso de las instrucciones de seguimiento y los modificadores de seguimiento
Seguimiento de implementar en la aplicación de servicios en la nube mediante la adición de hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello configuración de la aplicación y realizar llamadas tooSystem.Diagnostics.Trace o a System.Diagnostics.Debug en su código de la aplicación. Utilizar el archivo de configuración de hello *app.config* para hello y roles de trabajo *web.config* para los roles web. Cuando se crea un nuevo servicio hospedado mediante una plantilla de Visual Studio, diagnósticos de Azure se agrega automáticamente el proyecto toohello y hello DiagnosticMonitorTraceListener se agrega toohello el archivo de configuración adecuado para los roles de Hola que agregue.

Para obtener información sobre cómo colocar instrucciones de seguimiento, vea [Cómo: agregar instrucciones de seguimiento tooApplication código](https://msdn.microsoft.com/library/zd83saa2.aspx).

Al colocar [modificadores de seguimiento](https://msdn.microsoft.com/library/3at424ac.aspx) en el código, puede controlar si se realiza el seguimiento y cuál es su alcance. Esto le permite supervisar el estado de saludo de la aplicación en un entorno de producción. Esto es especialmente importante en una aplicación empresarial que usa varios componentes que se ejecutan en varios equipos. Para obtener más información, consulte [Procedimientos: configuración de modificadores de seguimiento](https://msdn.microsoft.com/library/t06xyy08.aspx).

## <a name="configure-hello-trace-listener-in-an-azure-application"></a>Configurar el agente de escucha de seguimiento de hello en una aplicación de Azure
Trace, Debug y TraceSource, deberá configurar "agentes de escucha" toocollect y mensajes de saludo de registro que se envían. Los agentes de escucha de recopilan, almacenan y enrutan los mensajes de seguimiento. Estos flujos dirigen Hola seguimiento salida tooan destino apropiado, como un registro, una ventana o un archivo de texto. Diagnósticos de Azure usa hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) clase.

Antes de completar Hola siguiendo el procedimiento, debe inicializar Hola monitor de diagnóstico de Azure. toodo, vea [habilitar diagnósticos en Microsoft Azure](cloud-services-dotnet-diagnostics.md).

Tenga en cuenta que si usa plantillas de Hola que se proporcionan con Visual Studio, Hola configuración de agente de escucha de Hola se agrega automáticamente para usted.

### <a name="add-a-trace-listener"></a>Incorporación de un agente de escucha de seguimiento
1. Abra el archivo web.config o app.config de hello para el rol.
2. Agregar Hola siguiente archivo de código toohello. Cambiar Hola atributo toouse Hola versión número de versión Hola ensamblado que se hace referencia. versión del ensamblado Hello no necesariamente cambiar con cada versión del SDK de Azure a menos que haya actualizaciones tooit.
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > Asegúrese de que tiene un toohello de referencia de proyecto Microsoft.WindowsAzure.Diagnostics ensamblado. Número de versión de actualización hello en xml de Hola por encima de la versión de Hola toomatch de hello al que hace referencia el ensamblado Microsoft.WindowsAzure.Diagnostics.
   > 
   > 
3. Guarde el archivo de configuración de Hola.

Para más información sobre los agentes de escucha, vea [Agentes de escucha de seguimiento](https://msdn.microsoft.com/library/4y5y10s7.aspx).

Después de completar el agente de escucha de hello pasos tooadd hello, puede agregar código de tooyour de instrucciones de seguimiento.

### <a name="tooadd-trace-statement-tooyour-code"></a>código de tooyour de instrucción de seguimiento tooadd
1. Abra un archivo de origen para la aplicación. Por ejemplo, hello <RoleName>archivo .cs para el rol de trabajo de Hola o web.
2. Agregue Hola siguientes mediante la instrucción si ya no se ha agregado:
    ```
        using System.Diagnostics;
    ```
3. Agregar instrucciones de seguimiento donde desea toocapture información sobre el estado de saludo de la aplicación. Puede utilizar una variedad de salida de hello tooformat de métodos de hello instrucción de seguimiento. Para obtener más información, consulte [Cómo: agregar instrucciones de seguimiento tooApplication código](https://msdn.microsoft.com/library/zd83saa2.aspx).
4. Guarde el archivo de código fuente de Hola.

