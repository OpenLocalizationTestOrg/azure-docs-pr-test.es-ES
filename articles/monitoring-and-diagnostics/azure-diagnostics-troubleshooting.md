---
title: "aaaTroubleshooting diagnósticos de Azure | Documentos de Microsoft"
description: "Solucione problemas al utilizar Diagnósticos de instancias de Azure Virtual Machine, Service Fabric o Cloud Services."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: robb
ms.openlocfilehash: daaf9fa4c40982eb9ba04030d7e8ea1ad9fe085b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Solución de problemas de Diagnósticos de Azure
Solución de problemas de información relevante toousing diagnósticos de Azure. Para obtener información sobre Diagnósticos de Azure, consulte la [introducción a Diagnósticos de Azure](azure-diagnostics.md).

## <a name="logical-components"></a>Componentes lógicos
**Selector de complemento de diagnóstico (DiagnosticsPluginLauncher.exe)**: extensión de diagnósticos de Azure Hola se inicia. Proceso de punto de actúa como entrada de Hola.

**Complemento de diagnóstico (DiagnosticsPlugin.exe)**: proceso principal que se inicia mediante el selector de hello anterior y configura el agente de supervisión de hello, lo inicia y administra su duración. 

**Agente de supervisión (agente de supervisión\*procesos .exe)**: estos procesos Hola la mayor parte del trabajo de hello; es decir, la supervisión, la colección y la transferencia de Hola datos de diagnóstico.  

## <a name="logartifact-paths"></a>Rutas de acceso de registro y artefacto
Estos son registros importantes de toosome de rutas de acceso de Hola y artefactos. Seguimos que hace referencia toothese a lo largo del resto de saludo del documento de hello:
### <a name="cloud-services"></a>Cloud Services
| Artefacto | path |
| --- | --- |
| **Archivo de configuración de Azure Diagnostics** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version>\Config.txt |
| **Archivos de registro** | C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version>\ |
| **Almacén local para los datos de diagnóstico** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Tables |
| **Archivo de configuración del agente de supervisión** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MaConfig.xml |
| **Paquete de extensión de Azure Diagnostics** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version> |
| **Ruta de acceso a la utilidad de recopilación de registros** | %SystemDrive%\Packages\GuestAgent\ |
| **Archivo de registro de MonAgentHost** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

### <a name="virtual-machines"></a>Máquinas virtuales
| Artefacto | path |
| --- | --- |
| **Archivo de configuración de Azure Diagnostics** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\RuntimeSettings |
| **Archivos de registro** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\Logs\ |
| **Almacén local para los datos de diagnóstico** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Tables |
| **Archivo de configuración del agente de supervisión** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Configuration\MaConfig.xml |
| **Archivo de estado** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\Status |
| **Paquete de extensión de Azure Diagnostics** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>|
| **Ruta de acceso a la utilidad de recopilación de registros** | C:\WindowsAzure\Packages |
| **Archivo de registro de MonAgentHost** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

## <a name="metric-data-doesnt-show-in-azure-portal"></a>Los datos de métrica no se muestran en Azure Portal
Azure Diagnostics proporciona una serie de datos de métrica, que se pueden mostrar en Azure Portal. Si tiene problemas al ver estos datos en el portal, cuenta de almacenamiento de diagnóstico de comprobación de hello -> WADMetrics\* tabla toosee si existen registros de métrica de hello correspondientes. En este caso, hello PartitionKey de tabla de hello es el identificador de recurso de Hola de máquina virtual o un conjunto de escalas de máquina virtual y hello RowKey es el nombre de la métrica hello es decir, el nombre de contador de rendimiento.

Si el identificador de recurso de hello es incorrecto, compruebe la configuración de diagnóstico -> métricas -> ResourceId toosee si Hola Id. de recurso se ha establecido correctamente.

Si no hay ningún dato de métrica específica de hello, compruebe la configuración de diagnóstico -> PerformanceCounter toosee si se incluye la métrica de hello (contador de rendimiento). Se permiten Hola siguiendo los contadores de forma predeterminada.
- \Processor(_Total)\% Processor Time
- \Memoria\Bytes disponibles
- \ASP.NET Applications(__Total__)\Requests/Sec [\Aplicaciones ASP.NET(Total)\Solicitudes/s]
- \ASP.NET Applications(__Total__)\Errors Total/Sec [\Aplicaciones ASP.NET(Total)\Total de errores/s]
- \ASP.NET\Requests Queued (\ASP.NET\Solicitudes en cola)
- \ASP.NET\Requests Rejected (\ASP.NET\Solicitudes rechazadas)
- \Processor(w3wp)\% Processor Time [\Procesador(w3wp) Tiempo de procesador]
- \Process(w3wp)\Private Bytes [\Proceso(w3wp)\Bytes privados]
- \Process(WaIISHost)\% Processor Time [\Proceso(WaIISHost) Tiempo de procesador]
- \Process(WaIISHost)\Private Bytes [\Proceso(WallSHost)\Bytes privados]
- \Process(WaWorkerHost)\% Processor Time [\Proceso(WaWorkerHost) Tiempo de procesador]
- \Process(WaWorkerHost)\Private Bytes (\Proceso(WaWorkerHost)\Bytes privados)
- \Memory\Page Faults/sec (\Memoria\Errores de página/s)
- \.NET CLR Memory(_Global_)\% Time in GC [Memoria CLR NET(Global) Tiempo en GC]
- \LogicalDisk(C:)\Disk Write Bytes/sec [\DiscoLógico(C:)\Bytes de escritura en disco/segundo]
- \LogicalDisk(C:)\Disk Read Bytes/sec [\DiscoLógico(C:)\Bytes de lectura en disco/s]
- \LogicalDisk(D:)\Disk Write Bytes/sec [\DiscoLógico(D:)\Bytes de escritura en disco/s]
- \LogicalDisk(D:)\Disk Read Bytes/sec [\DiscoLógico(D:)\Bytes de lectura en disco/s]

Si Hola se ha configurado correctamente, pero todavía no puede ver datos de métrica de hello, seguir directrices de Hola a continuación para una investigación más Hola.


## <a name="azure-diagnostics-is-not-starting"></a>Diagnósticos de Azure no se inicia
Mire **DiagnosticsPluginLauncher.log** y **DiagnosticsPlugin.log** archivos de registro de archivos de ubicación de Hola de hello proporcionado anteriormente para obtener información sobre por qué diagnostics no pudo toostart. 

Si estos registros indican `Monitoring Agent not reporting success after launch`, significa que hubo un error al iniciar MonAgentHost.exe. Examine los registros de Hola para que en la ubicación de hello indicada para `MonAgentHost log file` en la sección de hello anterior.

Hola última línea de archivos de registro de hello contiene código de salida de hello.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Si encuentra un **negativo** código de salida, consulte toohello [tabla de códigos de salida](#azure-diagnostics-plugin-exit-codes) en hello [referencias](#references).

## <a name="diagnostics-data-is-not-logged-tooazure-storage"></a>Datos de diagnóstico están no ha iniciado sesión tooAzure almacenamiento
Determine si no aparece ningún dato o solo algunos de los datos de hello no aparecen.

### <a name="diagnostics-infrastructure-logs"></a>Registros de infraestructura de diagnóstico
Los registros de infraestructura de diagnóstico es donde Azure Diagnostics registra los errores encontrados. Asegúrese de que ha habilitado ([cómo?](#how-to-check-diagnostics-extension-configuration)) captura de registros de infraestructura de diagnóstico en la configuración y buscar rápidamente los errores correspondientes que aparecen en hello `DiagnosticInfrastructureLogsTable` tabla en su cuenta de almacenamiento configurada.

### <a name="no-data-is-showing-up"></a>No se muestra ningún dato
causa más común de Hola de datos de evento que falta por completo es información de la cuenta de almacenamiento definidas incorrectamente.

Solución: corrija la configuración de Diagnostics y vuelva a instalar esta extensión.

Si la cuenta de almacenamiento de hello está configurado correctamente, remoto escritorio en la marca y el equipo de hello seguro DiagnosticsPlugin.exe y MonAgentCore.exe se ejecutan. Si no se están ejecutando, siga las instrucciones de la sección [Azure Diagnostics no se inicia](#azure-diagnostics-is-not-starting). Si se ejecutan procesos de hello, saltar demasiado[datos obtener captura localmente](#is-data-getting-captured-locally) y siga esta guía desde allí.

### <a name="part-of-hello-data-is-missing"></a>Parte de los datos de hello es que faltan
Si quiere obtener algunos datos pero no otros. Esto significa que la recopilación de datos Hola / canalización de transferencia se ha establecido correctamente. Siga subsecciones Hola aquí toonarrow qué problema hello es:
#### <a name="is-collection-configured"></a>¿Está configurada la colección? 
Configuración de diagnóstico contiene parte de Hola que indica un tipo determinado de toobe de datos recopilado. [Revise la configuración de](#how-to-check-diagnostics-extension-configuration) toomake seguro de que no busca datos no se ha configurado para la colección.
#### <a name="is-hello-host-generating-data"></a>Host de hello genera datos:
- **Contadores de rendimiento**: abrir el Monitor de rendimiento y comprobar contador Hola.
- **Los registros de seguimiento**: escritorio remoto en Hola VM y agregue el archivo de configuración de la aplicación de toohello TextWriterTraceListener.  Vea http://msdn.microsoft.com/library/sk36c28t.aspx tooset detector de texto hello.  Asegúrese de hello seguro `<trace>` elemento tiene `<trace autoflush="true">`.<br />
Si no ve que se generen registros de seguimiento, consulte [Más sobre registros de seguimiento que faltan](#more-about-trace-logs-missing).
- **Seguimientos de ETW**: escritorio remoto en hello máquina virtual e instale PerfView.  En PerfView, ejecute File (Archivo) -> User Command (Comando de usuario) -> Listen (Escuchar) etwprovder1, etwprovider2, etc.  Tenga en cuenta que el comando de escucha de hello distingue mayúsculas de minúsculas y no puede haber espacios entre la lista separada por comas de Hola de proveedores de ETW.  Si el comando de hello no toorun, puede hacer clic en botón de 'Iniciar' hello en la esquina inferior derecha de Hola de hello Perfview herramienta toosee ¿cuál era toorun intento y el resultado de hello fue.  Suponiendo que la entrada de hello sea correcta, a continuación, aparecerá una nueva ventana de seguridad y en unos segundos empezará ver seguimientos de ETW.
- **Registros de eventos**: escritorio remoto en hello máquina virtual. Abra `Event Viewer` y asegúrese de que existen eventos Hola.
#### <a name="is-data-getting-captured-locally"></a>¿Se capturan los datos localmente?
A continuación, asegúrese de que se obtener captura datos de hello localmente.
datos de Hola se almacenan localmente en `*.tsf` archivos [almacén local de Hola para datos de diagnóstico](#log-artifacts-path). Diferentes tipos de registros se recopilan en diferentes archivos `.tsf`. nombres de Hello son nombres de tabla de toohello similar en el almacenamiento de azure. Por ejemplo, `Performance Counters` se recopilan en `PerformanceCountersTable.tsf`, los registros de eventos en `WindowsEventLogsTable.tsf`, etc. Siga las instrucciones de hello en [extracción de registro Local](#local-log-extraction) tooopen Hola recopilación local archivos de sección y asegúrese de que verlos obtener recopilados en el disco.

Si no ve registros obtener recopilados localmente y ya ha comprobado que host hello es generar los datos, es probable que tenga un problema de configuración. Revise la configuración de cuidadosamente para la sección correspondiente de Hola. Revisar configuración Hola generado para MonitoringAgent [MaConfig.xml](#log-artifacts-path) y asegúrese de que no hay algunos sección que describe el origen del registro relevantes de Hola y que no se pierdan durante la traducción entre la configuración de diagnósticos de azure y la configuración de agente de supervisión.
#### <a name="is-data-getting-transferred"></a>¿Se transfieren los datos?
Si ha comprobado se obtener captura datos de hello localmente pero aún no lo ve en la cuenta de almacenamiento: 
- En primer lugar y ante todo, asegúrese de que ha proporcionado una cuenta de almacenamiento correcta y que no han sustituido claves etc.for Hola dado cuenta de almacenamiento. Para los servicios en la nube, en ocasiones vemos que la gente no actualiza su valor de `useDevelopmentStorage=true`.
- Si se proporciona, la cuenta de almacenamiento es correcta. Asegúrese de que no tiene algunas restricciones de red que no permiten componentes hello tooreach extremos de almacenamiento público. Toodo unidireccional que es tooremote escritorio en hello máquina e intente toowrite algo toohello mismo almacenamiento cuenta usted mismo.
- Por último, intente ver qué errores notifica el agente de supervisión. Agente de supervisión escribe sus archivos de registro `maeventtable.tsf` ubicado en [almacén local de Hola para datos de diagnóstico](#log-artifacts-path). Siga las instrucciones de [extracción de registro Local](#local-log-extraction) sección tooopen este archivo y pruebe y averiguar si hay `errors` que indica los archivos locales de errores tooread o escribir toostorage.

### <a name="capturing--archiving-logs"></a>Captura y archivo de registros
Palabras clave han tenido Hola anteriormente pasos pero no pudo determinar qué es correcto y está pensando acerca de cómo ponerse en contacto con soporte técnico. en primer lugar de Hello puede pedirle que es toocollect registros desde el equipo. Para ahorrar tiempo, hágalo usted mismo. Ejecute hello `CollectGuestLogs.exe` utilidad en [ruta de acceso de herramienta de recopilación de registro](#log-artifacts-path) y genera un archivo zip con todos los registros de azure pertinentes en hello misma carpeta.

## <a name="diagnostics-data-tables-not-found"></a>Tablas de datos de diagnóstico no encontradas
tablas de Hello en el almacenamiento de Azure que contiene los eventos ETW se denominan utilizando Hola siguiente código:

```C#
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

Aquí tiene un ejemplo:

```XML
        <EtwEventSourceProviderConfiguration provider="prov1">
          <Event id="1" />
          <Event id="2" eventDestination="dest1" />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider="prov2">
          <DefaultEvents eventDestination="dest2" />
        </EtwEventSourceProviderConfiguration>
```
```JSON
"EtwEventSourceProviderConfiguration": [
    {
        "provider": "prov1",
        "Event": [
            {
                "id": 1
            },
            {
                "id": 2,
                "eventDestination": "dest1"
            }
        ],
        "DefaultEvents": {
            "eventDestination": "DefaultEventDestination",
            "sinks": ""
        }
    },
    {
        "provider": "prov2",
        "DefaultEvents": {
            "eventDestination": "dest2"
        }
    }
]
```
Que genera 4 tablas:

| Evento | Nombre de la tabla |
| --- | --- |
| provider=”prov1” &lt;Event id=”1” /&gt; |WADEvent+MD5(“prov1”)+”1” |
| provider=”prov1” &lt;Event id=”2” eventDestination=”dest1” /&gt; |WADdest1 |
| provider=”prov1” &lt;DefaultEvents /&gt; |WADDefault+MD5(“prov1”) |
| provider=”prov2” &lt;DefaultEvents eventDestination=”dest2” /&gt; |WADdest2 |

## <a name="references"></a>Referencias

### <a name="how-toocheck-diagnostics-extension-configuration"></a>¿Cómo toocheck configuración de la extensión de diagnósticos
Hola toocheck de manera más fácil su configuración de la extensión es toonavigate toohttp://resources.azure.com, navegar por los servicio virtual de máquina o en la nube de toohello en qué Hola extensión de diagnósticos de Azure (IaaSDiagnostics / PaaDiagnostics) está en peligro.

Como alternativa, escritorio remoto en la máquina de Hola y busque en el archivo de configuración de diagnóstico de Azure de hello se describe en la sección correspondiente de hello [aquí](#log-artifacts-path).

En cualquier caso, busque **Microsoft.Azure.Diagnostics** a continuación en hello **xmlCfg** o **WadCfg** campo. 

En el caso de máquinas virtuales, si el campo de hello WadCfg está presente, significa Hola config es JSON. Si el campo de hello xmlCfg está presente, significa Hola config está en formato XML y está codificado en base64. Necesita demasiado[descodificarla](http://www.bing.com/search?q=base64+decoder) toosee Hola XML que se cargaron con diagnósticos.

Para el rol de servicio en la nube, si elige la configuración de Hola desde el disco, datos de hello están codificado por lo que necesitará demasiado en base64[descodificarla](http://www.bing.com/search?q=base64+decoder) toosee Hola XML que se cargaron con diagnósticos.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Códigos de salida del complemento Azure Diagnostics
complemento de Hello devuelve Hola siguientes códigos de salida:

| Código de salida | Descripción |
| --- | --- |
| 0 |Correcta. |
| -1 |Error genérico. |
| -2 |Archivo de rcf de hello tooload no se puede.<p>Este error interno solo debe ocurrir si incorrectamente, selector de complemento de agente de invitado de hello manualmente se invoca en hello máquina virtual. |
| -3 |No se puede cargar el archivo de configuración de diagnósticos de Hola.<p><p>Solución: esto se debe a que un archivo de configuración no supera la validación del esquema. solución de Hello es tooprovide un archivo de configuración que es compatible con el esquema de Hola. |
| -4 |Otra instancia del programa Hola a diagnóstico de agente de supervisión ya está usando el directorio de recursos locales de Hola.<p><p>Solución: Especifique un valor distinto para **LocalResourceDirectory**. |
| -6 |Selector de complemento de agente de invitado de Hello intentó realizar diagnósticos de toolaunch con una línea de comandos no válido.<p><p>Este error interno solo debe ocurrir si incorrectamente, selector de complemento de agente de invitado de hello manualmente se invoca en hello máquina virtual. |
| -10 |complemento de diagnóstico de Hello terminó con una excepción no controlada. |
| -11 |agente de invitado de Hello era proceso de Hola de toocreate no se puede responsable iniciar y supervisar el agente de supervisión de Hola.<p><p>Solución: Compruebe que suficientes recursos del sistema están disponibles toolaunch nuevos procesos.<p> |
| -101 |Argumentos no válidos al llamar al complemento de diagnóstico de Hola.<p><p>Este error interno solo debe ocurrir si incorrectamente, selector de complemento de agente de invitado de hello manualmente se invoca en hello máquina virtual. |
| -102 |proceso del complemento de Hello es no se puede tooinitialize propio.<p><p>Solución: Compruebe que suficientes recursos del sistema están disponibles toolaunch nuevos procesos. |
| -103 |proceso del complemento de Hello es no se puede tooinitialize propio. En concreto es objeto de registrador hello toocreate no se puede.<p><p>Solución: Compruebe que suficientes recursos del sistema están disponibles toolaunch nuevos procesos. |
| -104 |Archivo de tooload no se puede hello rcf proporcionada por el agente de invitado Hola.<p><p>Este error interno solo debe ocurrir si incorrectamente, selector de complemento de agente de invitado de hello manualmente se invoca en hello máquina virtual. |
| -105 |complemento de diagnóstico de Hello no puede abrir el archivo de configuración de diagnósticos de Hola.<p><p>Este error interno solo debe ocurrir si incorrectamente, complemento de diagnóstico de hello manualmente se invoca en hello máquina virtual. |
| -106 |No se puede leer el archivo de configuración de diagnósticos de Hola.<p><p>Solución: esto se debe a que un archivo de configuración no supera la validación del esquema. Por lo que la solución de hello es tooprovide un archivo de configuración que es compatible con el esquema de Hola. Vea [cómo toocheck configuración de la extensión de diagnósticos](#how-to-check-diagnostics-extension-configuration). |
| -107 |directorio de recursos de Hello paso toohello agente de supervisión no es válido.<p><p>Este error interno solo debe ocurrir si incorrectamente, agente de supervisión de hello manualmente se invoca en hello máquina virtual.</p> |
| -108 |No se puede tooconvert el archivo de configuración de diagnósticos de hello en el archivo de configuración de agente de supervisión de Hola.<p><p>Este error interno solo debe ocurrir si el complemento de diagnóstico de Hola se invoca manualmente con un archivo de configuración no válida. |
| -110 |Error de configuración general de Diagnósticos.<p><p>Este error interno solo debe ocurrir si el complemento de diagnóstico de Hola se invoca manualmente con un archivo de configuración no válida. |
| -111 |Agente de supervisión de hello toostart no se puede.<p><p>Solución: compruebe que hay suficientes recursos del sistema disponibles. |
| -112 |Error general |

### <a name="local-log-extraction"></a>Extracción de registros locales
Hola, agente de supervisión recopila registros y artefactos como `.tsf` archivos. El archivo `.tsf` no se puede leer pero puede convertirlo a `.csv` de la manera siguiente: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Llama a un nuevo archivo `<relevantLogFile>.csv` se creará en hello misma ruta de acceso correspondiente de hello `.tsf` archivo.

**Tenga en cuenta**: solo necesita toorun esta utilidad en archivo de tsf principal hello (p. ej., PerformanceCountersTable.tsf). Hola que acompaña a los archivos (p. ej., PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*002.jpg tsf etc.) se procesarán automáticamente.

### <a name="more-about-trace-logs-missing"></a>Más sobre registros de seguimiento que faltan

**Nota:** se aplica principalmente toocloud servicios solo a menos que se haya configurado hello DiagnosticsMonitorTraceListener de una aplicación que se ejecuta en la VM de IaaS. 

- Asegúrese de hello seguro de que DiagnosticMonitorTraceListener esté configurado en hello web.config o app.config.  Esto se configura de forma predeterminada en los proyectos de servicios de nube, pero algunos clientes comentan fuera lo que hará que toonot de instrucciones de seguimiento de hello recopilarán diagnósticos. 
- Si no obtener se escriben los registros del método OnStart o ejecución de Hola que seguro Hola que diagnosticmonitortracelistener está en un archivo app.config de Hola.  De forma predeterminada es en el archivo web.config de hello, pero solo se aplica toocode que se ejecuta en w3wp.exe; por lo que necesita en los seguimientos de app.config toocapture que se ejecutan en WaIISHost.exe.
- Asegúrese de que usa Diagnostics.Trace.TraceXXX en lugar de Diagnostics.Debug.WriteXXX.  Hello instrucciones de depuración se va a quitar de una versión de lanzamiento.
- Asegúrese de que el código de hello compilado realmente tiene líneas de Diagnostics.Trace Hola (usar tooverify Reflector, ildasm o ILSpy).  Comandos de Diagnostics.Trace se han quitado desde el archivo binario de hello compilado a menos que utilice el símbolo de compilación condicional de seguimiento de Hola.  Si utiliza msbuild toobuild Hola proyecto es un toorun problema común en.

## <a name="known-issues-and-mitigations"></a>Problemas conocidos y mitigaciones
Esta es una lista de problemas conocidos con mitigaciones conocidas:

**1. Dependencia de .NET 4.5:**

WAD tiene una dependencia de tiempo de ejecución en la plataforma .NET 4.5 o superior. En tiempo de hello de la escritura de esto, todos los equipos aprovisionados para servicios en la nube, así como todos los oficial azure base imágenes de máquina Virtual tienen .NET 4.5 o anteriormente instalado. Es posible todavía sin embargo tooland en una situación en la que trate toorun WAD en un equipo que no tiene .NET 4.5 o una versión posterior. Esto sucede cuando crea su máquina a partir de una imagen o instantánea anterior, o trae su propio disco personalizado.

Generalmente se manifiesta como un código de salida **255** al ejecutar DiagnosticsPluginLauncher.exe. Error se produce debido a excepciones no controlada de toohello: 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Mitigación:** instale .NET 4.5 o superior en su máquina.

**2. Los datos de los contadores de rendimiento están disponibles en el almacenamiento pero no se muestran en el portal**

La experiencia del portal de las máquinas virtuales muestra de forma predeterminada determinados contadores de rendimiento. Si no se ven y se sabe que se estén generando datos Hola porque está disponible en el almacenamiento de. Comprobar:
- Si los datos de hello en el almacenamiento tienen nombres de contador en inglés. Si los nombres de contadores de hello no están en inglés, portal gráfico de métricas no será capaz de toorecognize lo.
- Si utiliza caracteres comodín (\*) en los nombres de contador de rendimiento, portal hello no será capaz de toocorrelate Hola configurado y recopilados de contador.

**Mitigación**: cambiar tooEnglish de idioma de la máquina de Hola para las cuentas del sistema. El Panel de control -> región -> Administración -> configuración de copia -> desactive "Bienvenida de pantalla y cuentas del sistema" para que no sea el lenguaje personalizado Hola aplica toosystem cuenta. Además, asegúrese de que no utilice caracteres comodín si desea toobe portal su experiencia de consumo principal.
