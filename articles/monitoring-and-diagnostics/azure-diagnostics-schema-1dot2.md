---
title: "Esquema de configuración de diagnósticos 1.2 aaaAzure | Documentos de Microsoft"
description: "SOLO es pertinente si utiliza Azure SDK 2.5 con Azure Virtual Machines, conjuntos de escalado de máquinas virtuales, Service Fabric o Cloud Services."
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
ms.openlocfilehash: 31559317b696556a64b51b58800b176ade9a4679
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-12-configuration-schema"></a>Esquema de configuración de Diagnósticos de Azure 1.2
> [!NOTE]
> Diagnósticos de Azure es Hola componente usado toocollect los contadores de rendimiento y otras estadísticas de máquinas virtuales de Azure, conjuntos de escalas de máquina Virtual, Service Fabric y servicios en la nube.  Esta página solo es pertinente si está usando uno de estos servicios.
>

Diagnósticos de Azure se usa con otros productos de diagnósticos de Microsoft, como Azure Monitor, Application Insights y Log Analytics.

Este esquema define los valores posibles de hello puede usar la configuración de la configuración de diagnóstico de tooinitialize cuando se inicia el monitor de diagnóstico de Hola.  


 Descargar definición de esquema de archivo de configuración pública de hello ejecutando el siguiente comando de PowerShell de hello:  

```PowerShell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 Para más información sobre Diagnósticos de Azure, consulte [Habilitación de Diagnósticos en Azure Cloud Services y Azure Virtual Machines](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Ejemplo de archivo de configuración de diagnósticos de Hola  
 Hola de ejemplo siguiente muestra un archivo de configuración de diagnóstico típico:  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">  
  <WadCfg>  
    <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  
      <PerformanceCounters scheduledTransferPeriod="PT1M">  
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
      </PerformanceCounters>  
      <Directories scheduledTransferPeriod="PT5M">  
        <IISLogs containerName="iislogs" />  
        <FailedRequestLogs containerName="iisfailed" />  
        <DataSources>  
          <DirectoryConfiguration containerName="mynewprocess">  
            <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
          </DirectoryConfiguration>  
          <DirectoryConfiguration containerName="badapp">  
            <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
          </DirectoryConfiguration>  
          <DirectoryConfiguration containerName="goodapp">  
            <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
          </DirectoryConfiguration>  
        </DataSources>  
      </Directories>  
      <EtwProviders>  
        <EtwEventSourceProviderConfiguration provider="MyProviderClass" scheduledTransferPeriod="PT5M">  
          <Event id="0"/>  
          <Event id="1" eventDestination="errorTable"/>  
          <DefaultEvents />  
        </EtwEventSourceProviderConfiguration>  
        <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
          <Event id="0"/>  
          <DefaultEvents eventDestination="defaultTable"/>  
        </EtwManifestProviderConfiguration>  
      </EtwProviders>  
      <WindowsEventLog scheduledTransferPeriod="PT5M">  
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
        <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
        <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
      </WindowsEventLog>  
      <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
        <CrashDumpConfiguration processName="mynewprocess.exe" />  
        <CrashDumpConfiguration processName="badapp.exe"/>  
      </CrashDumps>  
    </DiagnosticMonitorConfiguration>  
  </WadCfg>  
</PublicConfig>  

```  

## <a name="diagnostics-configuration-namespace"></a>Espacio de nombres de configuración de Diagnósticos  
 espacio de nombres XML de Hello para el archivo de configuración de diagnósticos de hello es:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="publicconfig-element"></a>Elemento PublicConfig  
 Elemento de nivel superior del archivo de configuración de diagnósticos de Hola. Hello tabla siguiente describen los elementos de Hola Hola del archivo de configuración.  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**WadCfg**|Necesario. Configuración de toobe de datos de telemetría de hello recopilados.|  
|**StorageAccount**|nombre de Hola Hola almacenamiento de Azure toostore Hola los datos de cuenta en. También se puede especificar esto como un parámetro al ejecutar el cmdlet de hello AzureServiceDiagnosticsExtension del conjunto.|  
|**LocalResourceDirectory**|Hola en hello toobe de máquina virtual usando el directorio Hola datos de eventos de toostore de agente de supervisión. Si no se utiliza el conjunto, el directorio predeterminado de hello:<br /><br /> Para un rol de trabajo o web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Para una máquina virtual: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Los atributos necesarios son:<br /><br /> -                      **ruta de acceso** : hello directorio Hola sistema toobe utilizado por diagnósticos de Azure.<br /><br /> -                      **expandEnvironment** -controla si las variables de entorno se expanden en nombre de ruta de acceso de Hola.|  

## <a name="wadcfg-element"></a>Elemento WadCFG  
Define la configuración para toobe de datos de telemetría de hello recopilados. Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**DiagnosticMonitorConfiguration**|Obligatorio. Los atributos opcionales son:<br /><br /> -                     **overallQuotaInMB** -cantidad máxima de Hola de espacio en disco local que se puede utilizar en hello diversos tipos de datos de diagnóstico recopilan por diagnósticos de Azure. saludo predeterminado es 5.120 MB.<br /><br /> -                     **useProxyServer** -configuración del servidor de proxy configurar diagnósticos de Azure toouse hello como conjunto de configuración de Internet Explorer.|  
|**CrashDumps**|Habilite la recopilación de volcados de memoria. Los atributos opcionales son:<br /><br /> -                     **containerName** -nombre de Hola Hola del contenedor de blobs en su toobe de cuenta de almacenamiento de Azure usa toostore volcados de memoria.<br /><br /> -                     **crashDumpType** -volcados de memoria de diagnósticos de Azure configura toocollect bloqueo Mini o completa.<br /><br /> -                     **directoryQuotaPercentage**-configura el porcentaje de Hola de **overallQuotaInMB** toobe reservado para volcados en hello máquina virtual.|  
|**DiagnosticInfrastructureLogs**|Habilite la recopilación de registros generados por Diagnósticos de Azure. registros de infraestructura de diagnóstico de Hello son útiles para solucionar Hola del sistema de diagnóstico. Los atributos opcionales son:<br /><br /> -                     **scheduledTransferLogLevelFilter** -configura el nivel de gravedad mínimo de Hola de registros de Hola se recopilan.<br /><br /> -                     **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto. valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**Directorios**|Habilita Hola Hola el contenido de un directorio de colección, error de IIS, los registros de solicitud de acceso y registros de IIS. Atributo opcional:<br /><br /> **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto. valor de Hello es un [XML "Tipo de datos de duración".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**EtwProviders**|Configura la recopilación de eventos ETW en EventSource o el manifiesto de ETW en función de los proveedores.|  
|**Métricas**|Este elemento le permite toogenerate una tabla de contador de rendimiento que se optimiza para las consultas rápidas. Cada contador de rendimiento que se define en hello **PerformanceCounters** elemento se almacena en la tabla de métricas de hello en la tabla de contador de rendimiento de toohello de adición. Atributo necesario:<br /><br /> **resourceId** -se trata de Id. de recurso de Hola de hello Máquina Virtual que va a implementar diagnósticos de Azure para. Obtener hello **resourceID** de hello [portal de Azure](https://portal.azure.com). Seleccione **Examinar** -> **Grupos de recursos** -> **<Nombre\>**. Haga clic en hello **propiedades** icono y copie el valor de Hola de hello **identificador** campo.|  
|**PerformanceCounters**|Habilita la recopilación de Hola de contadores de rendimiento. Atributo opcional:<br /><br /> **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto. El valor es un ["tipo de datos de duración" XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  
|**WindowsEventLog**|Habilita la recopilación de Hola de registros de eventos de Windows. Atributo opcional:<br /><br /> **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto. El valor es un ["tipo de datos de duración" XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="crashdumps-element"></a>Elemento CrashDumps  
 Habilita la recopilación de volcados de memoria. Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**CrashDumpConfiguration**|Obligatorio. Atributo necesario:<br /><br /> **processName** : hello nombre del proceso de hello desea toocollect de diagnósticos de Azure un volcado de memoria de.|  
|**crashDumpType**|Configura los diagnósticos de Azure toocollect parcial o completo volcados de memoria.|  
|**directoryQuotaPercentage**|Configura el porcentaje de Hola de **overallQuotaInMB** toobe reservado para volcados en hello máquina virtual.|  

## <a name="directories-element"></a>Elemento Directories  
 Habilita Hola Hola el contenido de un directorio de colección, error de IIS, los registros de solicitud de acceso y registros de IIS. Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**DataSources**|Una lista de directorios toomonitor.|  
|**FailedRequestLogs**|Incluir este elemento en configuración de hello habilita la recopilación de registros sobre las solicitudes con error tooan IIS sitio o aplicación. También debe habilitar las opciones de seguimiento en **system.WebServer** de **Web.config**.|  
|**IISLogs**|Incluir este elemento en configuración de hello habilita la recopilación de Hola de registros de IIS:<br /><br /> **containerName** -nombre de Hola Hola del contenedor de blobs en su toobe de cuenta de almacenamiento de Azure usa toostore Hola los registros de IIS.|  

## <a name="datasources-element"></a>Elemento DataSources  
 Una lista de directorios toomonitor. Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**DirectoryConfiguration**|Obligatorio. Atributo necesario:<br /><br /> **containerName** -nombre de Hola Hola del contenedor de blobs en el almacenamiento de Azure cuenta toostore toobe utiliza archivos de registro de hello.|  

## <a name="directoryconfiguration-element"></a>Elemento DirectoryConfiguration  
 **DirectoryConfiguration** puede incluir cualquier hello **absoluta** o **LocalResource** elemento pero no ambos. Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**Absolute**|Hola toomonitor de directorio toohello de ruta de acceso absoluta. Hola siguientes atributos es necesario:<br /><br /> -                     **Ruta de acceso** -Hola toomonitor de directorio toohello de ruta de acceso absoluta.<br /><br /> -                      **expandEnvironment**: configura si se expanden las variables de entorno en Path.|  
|**LocalResource**|Hola toomonitor de ruta de acceso relativa tooa recurso local. Los atributos necesarios son:<br /><br /> -                     **Nombre de** -Hola recurso local que contiene Hola directory toomonitor<br /><br /> -                     **relativePath** -Hola tooName relativa de ruta de acceso que contiene Hola directory toomonitor|  

## <a name="etwproviders-element"></a>Elemento EtwProviders  
 Configura la recopilación de eventos ETW en EventSource o el manifiesto de ETW en función de los proveedores. Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Configura la recopilación de eventos generados a partir de la [clase EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Atributo necesario:<br /><br /> **proveedor de** -nombre de la clase hello de evento de EventSource Hola.<br /><br /> Los atributos opcionales son:<br /><br /> -                     **scheduledTransferLogLevelFilter** -Hola cuenta de almacenamiento de tooyour tootransfer de nivel de gravedad mínimo.<br /><br /> -                     **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto. El valor es un [tipo de datos de duración XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  
|**EtwManifestProviderConfiguration**|Atributo necesario:<br /><br /> **proveedor** -Hola GUID del proveedor de eventos de Hola<br /><br /> Los atributos opcionales son:<br /><br /> - **scheduledTransferLogLevelFilter** -Hola cuenta de almacenamiento de tooyour tootransfer de nivel de gravedad mínimo.<br /><br /> -                     **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto. El valor es un [tipo de datos de duración XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="etweventsourceproviderconfiguration-element"></a>Elemento EtwEventSourceProviderConfiguration  
 Configura la recopilación de eventos generados a partir de la [clase EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**DefaultEvents**|Atributo opcional:<br /><br /> **eventDestination** : hello nombre hello toostore Hola eventos de tabla en|  
|**Evento**|Atributo necesario:<br /><br /> **Id. de** -Id. de Hola de evento Hola.<br /><br /> Atributo opcional:<br /><br /> **eventDestination** : hello nombre hello toostore Hola eventos de tabla en|  

## <a name="etwmanifestproviderconfiguration-element"></a>Elemento EtwManifestProviderConfiguration  
 Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**DefaultEvents**|Atributo opcional:<br /><br /> **eventDestination** : hello nombre hello toostore Hola eventos de tabla en|  
|**Evento**|Atributo necesario:<br /><br /> **Id. de** -Id. de Hola de evento Hola.<br /><br /> Atributo opcional:<br /><br /> **eventDestination** : hello nombre hello toostore Hola eventos de tabla en|  

## <a name="metrics-element"></a>Elemento Metrics  
 Le permite toogenerate una tabla de contador de rendimiento que se optimiza para las consultas rápidas. Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**MetricAggregation**|Atributo necesario:<br /><br /> **scheduledTransferPeriod** -intervalo de saludo entre las transferencias programadas toostorage redondea toohello más cercano de minuto. El valor es un [tipo de datos de duración XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="performancecounters-element"></a>Elemento PerformanceCounters  
 Habilita la recopilación de Hola de contadores de rendimiento. Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**PerformanceCounterConfiguration**|Hola siguientes atributos es necesario:<br /><br /> -                     **counterSpecifier** : hello nombre de contador de rendimiento de Hola. Por ejemplo: `\Processor(_Total)\% Processor Time`. una lista de contadores de rendimiento en el host que ejecute el comando de hello tooget `typeperf`.<br /><br /> -                     **sampleRate** -¿con qué frecuencia hello contador debe realizarse el muestreo.<br /><br /> Atributo opcional:<br /><br /> **unidad** -Hola unidad de medida de contador de Hola.|  

## <a name="performancecounterconfiguration-element"></a>Elemento PerformanceCounterConfiguration  
 Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**annotation**|Atributo necesario:<br /><br /> **displayName** -nombre para mostrar para el contador de Hola Hola<br /><br /> Atributo opcional:<br /><br /> **configuración regional** -Hola toouse de configuración regional para mostrar el nombre del contador de Hola|  

## <a name="windowseventlog-element"></a>Elemento WindowsEventLog  
 Hello en la tabla siguiente describe los elementos secundarios:  

|Nombre del elemento|Descripción|  
|------------------|-----------------|  
|**DataSource**|Hola toocollect de registros de eventos de Windows. Atributo necesario:<br /><br /> **nombre de** -recopilados de consulta de XPath de Hola que describe toobe de eventos de windows hello. Por ejemplo:<br /><br /> `Application!*[System[(Level >= 3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level >= 3]]`<br /><br /> toocollect todos los eventos, especifique "*".|
