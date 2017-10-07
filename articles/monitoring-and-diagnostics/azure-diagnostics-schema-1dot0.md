---
title: "aaaAzure esquema de configuración de diagnósticos 1.0 | Documentos de Microsoft"
description: "SOLO es pertinente si utiliza Azure SDK 2.4 y versiones anteriores con Azure Virtual Machines, conjuntos de escalado de máquinas virtuales, Service Fabric o Cloud Services."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a>Esquema de configuración de Diagnósticos de Azure 1.0
> [!NOTE]
> Diagnósticos de Azure es Hola componente usado toocollect los contadores de rendimiento y otras estadísticas de máquinas virtuales de Azure, conjuntos de escalas de máquina Virtual, Service Fabric y servicios en la nube.  Esta página solo es pertinente si está usando uno de estos servicios.
>

Diagnósticos de Azure se usa con otros productos de diagnósticos de Microsoft, como Azure Monitor, Application Insights y Log Analytics.

archivo de configuración de diagnósticos de Azure de Hello define valores que son usados tooinitialize Hola Monitor de diagnóstico. Este archivo es configuración de diagnóstico de tooinitialize usado cuando inicia de monitor de diagnóstico de Hola.  

 De forma predeterminada, archivo de esquema de configuración de diagnósticos de Azure de hello es toohello instalado `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory. Reemplace `<version>` con la versión de Hola instalado de hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).  

> [!NOTE]
>  archivo de configuración de diagnósticos de Hola se suele utilizar con las tareas de inicio que requieren toobe de datos de diagnóstico recopilada anteriormente en el proceso de inicio de Hola. Para más información sobre Diagnósticos de Azure, consulte [Recopilación de datos de registro mediante Diagnósticos de Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Ejemplo de archivo de configuración de diagnósticos de Hola  
 Hola de ejemplo siguiente muestra un archivo de configuración de diagnóstico típico:  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a>Espacio de nombres DiagnosticsConfiguration  
 espacio de nombres XML de Hello para el archivo de configuración de diagnósticos de hello es:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a>Elementos de esquema  
 archivo de configuración de diagnósticos de Hello incluye Hola siguientes elementos.


## <a name="diagnosticmonitorconfiguration-element"></a>Elemento DiagnosticMonitorConfiguration  
elemento de nivel superior de Hola Hola diagnósticos del archivo de configuración.  

Atributos:

|Atributo  |Escriba   |Obligatorio| Valor predeterminado | Descripción|  
|-----------|-------|--------|---------|------------|  
|**configurationChangePollInterval**|duration|Opcional | PT1M| Especifica el intervalo de hello en los sondeos de monitor de diagnóstico de Hola para cambios de configuración de diagnóstico.|  
|**overallQuotaInMB**|unsignedInt|Opcional| 4000 MB. Si proporciona un valor, no debe superar esta cantidad. |cantidad total de Hola de almacenamiento del sistema de archivos asignado para todos los búferes de registro.|  

## <a name="diagnosticinfrastructurelogs-element"></a>Elemento DiagnosticInfrastructureLogs  
Define la configuración de búfer de Hola para registros de hello generadas por la infraestructura de diagnóstico subyacente de Hola.

Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  

Atributos:

|Atributo|Tipo|Descripción|  
|---------|----|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcional. Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.<br /><br /> Hola predeterminado es 0.|  
|**scheduledTransferLogLevelFilter**|cadena|Opcional. Especifica el nivel de gravedad mínimo de Hola para las entradas de registro que se transfieren. es el valor predeterminado de Hello **Undefined**. Otros valores posibles son **Verbose**, **Information**, **Warning**, **Error** y **Critical**.|  
|**scheduledTransferPeriod**|duration|Opcional. Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.<br /><br /> valor predeterminado de Hello es PT0S.|  

## <a name="logs-element"></a>Elemento Logs  
 Define la configuración de búfer de Hola para los registros básicos de Azure.

 Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  

Atributos:  

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcional. Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.<br /><br /> Hola predeterminado es 0.|  
|**scheduledTransferLogLevelFilter**|cadena|Opcional. Especifica el nivel de gravedad mínimo de Hola para las entradas de registro que se transfieren. es el valor predeterminado de Hello **Undefined**. Otros valores posibles son **Verbose**, **Information**, **Warning**, **Error** y **Critical**.|  
|**scheduledTransferPeriod**|duration|Opcional. Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.<br /><br /> valor predeterminado de Hello es PT0S.|  

## <a name="directories-element"></a>Elemento Directories  
Define la configuración de búfer de Hola para los registros basados en archivos que se pueden definir.

Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  


Atributos:  

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcional. Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.<br /><br /> Hola predeterminado es 0.|  
|**scheduledTransferPeriod**|duration|Opcional. Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.<br /><br /> valor predeterminado de Hello es PT0S.|  

## <a name="crashdumps-element"></a>Elemento CrashDumps  
 Define el directorio de archivos de volcado de bloqueo de Hola.

 Elemento principal: [elemento Directories](#Directories).  

Atributos:  

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**container**|cadena|nombre del saludo del contenedor de Hola donde el contenido de hello del directorio de hello es toobe transfiere.|  
|**directoryQuotaInMB**|unsignedInt|Opcional. Especifica el tamaño máximo de hello del directorio de hello en megabytes.<br /><br /> Hola predeterminado es 0.|  

## <a name="failedrequestlogs-element"></a>Elemento FailedRequestLogs  
 Define el directorio de registro de solicitudes con error de Hola.

 Elemento principal: [elemento Directories](#Directories).  

Atributos:  

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**container**|cadena|nombre del saludo del contenedor de Hola donde el contenido de hello del directorio de hello es toobe transfiere.|  
|**directoryQuotaInMB**|unsignedInt|Opcional. Especifica el tamaño máximo de hello del directorio de hello en megabytes.<br /><br /> Hola predeterminado es 0.|  

##  <a name="iislogs-element"></a>Elemento IISLogs  
 Define el directorio de registro IIS de Hola.

 Elemento principal: [elemento Directories](#Directories).  

Atributos:  

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**container**|cadena|nombre del saludo del contenedor de Hola donde el contenido de hello del directorio de hello es toobe transfiere.|  
|**directoryQuotaInMB**|unsignedInt|Opcional. Especifica el tamaño máximo de hello del directorio de hello en megabytes.<br /><br /> Hola predeterminado es 0.|  

## <a name="datasources-element"></a>Elemento DataSources  
 Define cero o más directorios de registro adicionales.

 Elemento principal: [elemento Directories](#Directories).

## <a name="directoryconfiguration-element"></a>Elemento DirectoryConfiguration  
 Define el directorio de Hola de toomonitor de archivos de registro.

 Elemento principal: [elemento DataSources](#DataSources).

Atributos:

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**container**|cadena|nombre del saludo del contenedor de Hola donde el contenido de hello del directorio de hello es toobe transfiere.|  
|**directoryQuotaInMB**|unsignedInt|Opcional. Especifica el tamaño máximo de hello del directorio de hello en megabytes.<br /><br /> Hola predeterminado es 0.|  

## <a name="absolute-element"></a>Elemento Absolute  
 Define una ruta de acceso absoluta de hello toomonitor de directorio con la extensión del entorno opcional.

 Elemento principal: [elemento DirectoryConfiguration](#DirectoryConfiguration).  

Atributos:  

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**path**|string|Necesario. Hola toomonitor de directorio toohello de ruta de acceso absoluta.|  
|**expandEnvironment**|boolean|Necesario. Si establece demasiado**true**, las variables de entorno en la ruta de acceso de Hola se expanden.|  

## <a name="localresource-element"></a>Elemento LocalResource  
 Define un recurso local de ruta de acceso relativa tooa definido en la definición del servicio Hola.

 Elemento principal: [elemento DirectoryConfiguration](#DirectoryConfiguration).  

Atributos:  

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**name**|string|Necesario. nombre de Hola de recurso local Hola que contiene Hola directory toomonitor.|  
|**relativePath**|string|Necesario. Hola toomonitor de ruta de acceso relativa toohello recurso local.|  

## <a name="performancecounters-element"></a>Elemento PerformanceCounters  
 Define toocollect de contador de rendimiento de hello ruta de acceso toohello.

 Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).


 Atributos:  

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcional. Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.<br /><br /> Hola predeterminado es 0.|  
|**scheduledTransferPeriod**|duration|Opcional. Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.<br /><br /> valor predeterminado de Hello es PT0S.|  

## <a name="performancecounterconfiguration-element"></a>Elemento PerformanceCounterConfiguration  
 Define toocollect de contador de rendimiento de Hola.

 Elemento principal: [elemento PerformanceCounters](#PerformanceCounters)  

 Atributos:  

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**counterSpecifier**|string|Necesario. Hola toocollect de contador de rendimiento de toohello de ruta de acceso.|  
|**sampleRate**|duration|Necesario. velocidad de Hello en qué Hola se deben recopilar contadores de rendimiento.|  

## <a name="windowseventlog-element"></a>Elemento WindowsEventLog  
 Define hello toomonitor de registros de eventos.

 Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).

  Atributos:

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcional. Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.<br /><br /> Hola predeterminado es 0.|  
|**scheduledTransferLogLevelFilter**|cadena|Opcional. Especifica el nivel de gravedad mínimo de Hola para las entradas de registro que se transfieren. es el valor predeterminado de Hello **Undefined**. Otros valores posibles son **Verbose**, **Information**, **Warning**, **Error** y **Critical**.|  
|**scheduledTransferPeriod**|duration|Opcional. Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.<br /><br /> valor predeterminado de Hello es PT0S.|  

## <a name="datasource-element"></a>Elemento DataSource  
 Define hello toomonitor de registro de eventos.

 Elemento principal: [elemento WindowsEventLog](#windowsEventLog).  

 Atributos:

|Atributo|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**name**|string|Necesario. Expresión XPath que especifica toocollect de registro de hello.|  
