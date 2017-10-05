---
title: "Esquema de configuración de Diagnósticos de Azure 1.0 | Microsoft Docs"
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
ms.openlocfilehash: a8fdfb52d5091d3fc9779657737c7430fcfada51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="93927-103">Esquema de configuración de Diagnósticos de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="93927-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="93927-104">Diagnósticos de Azure es el componente que se usa para recopilar contadores de rendimiento y otras estadísticas de Azure Virtual Machines, conjuntos de escalado de máquinas virtuales, Service Fabric y Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="93927-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="93927-105">Esta página solo es pertinente si está usando uno de estos servicios.</span><span class="sxs-lookup"><span data-stu-id="93927-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="93927-106">Diagnósticos de Azure se usa con otros productos de diagnósticos de Microsoft, como Azure Monitor, Application Insights y Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="93927-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="93927-107">El archivo de configuración de Diagnósticos de Azure define los valores que se usan para inicializar el monitor de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="93927-107">The Azure Diagnostics configuration file defines values that are used to initialize the Diagnostics Monitor.</span></span> <span data-ttu-id="93927-108">Este se usa para inicializar la configuración de diagnóstico al iniciar el monitor de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="93927-108">This file is used to initialize diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

 <span data-ttu-id="93927-109">De forma predeterminada, el archivo de esquema de configuración de Diagnósticos de Azure se instala en el directorio `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas`.</span><span class="sxs-lookup"><span data-stu-id="93927-109">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="93927-110">Reemplace `<version>` por la versión instalada del [SDK de Azure](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="93927-110">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="93927-111">El archivo de configuración de diagnóstico se suele utilizar con las tareas de inicio que requieren los datos de diagnóstico que se van a recopilar antes en el proceso de inicio.</span><span class="sxs-lookup"><span data-stu-id="93927-111">The diagnostics configuration file is typically used with startup tasks that require diagnostic data to be collected earlier in the startup process.</span></span> <span data-ttu-id="93927-112">Para más información sobre Diagnósticos de Azure, consulte [Recopilación de datos de registro mediante Diagnósticos de Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="93927-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="93927-113">Ejemplo del archivo de configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="93927-113">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="93927-114">En el ejemplo siguiente se muestra un archivo de configuración de diagnóstico típico:</span><span class="sxs-lookup"><span data-stu-id="93927-114">The following example shows a typical diagnostics configuration file:</span></span>  

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

      <!-- These three elements specify the special directories   
           that are set up for the log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories the DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative to a local   
                 resource defined in the service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- The counter specifier is in the same format as the imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- The event log name is in the same format as the imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="93927-115">Espacio de nombres DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="93927-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="93927-116">El espacio de nombres XML del archivo de configuración de diagnóstico es:</span><span class="sxs-lookup"><span data-stu-id="93927-116">The XML namespace for the diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="93927-117">Elementos de esquema</span><span class="sxs-lookup"><span data-stu-id="93927-117">Schema Elements</span></span>  
 <span data-ttu-id="93927-118">El archivo de configuración de diagnóstico incluye los siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="93927-118">The diagnostics configuration file includes the following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="93927-119">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="93927-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="93927-120">Elemento de nivel superior del archivo de configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="93927-120">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="93927-121">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-121">Attributes:</span></span>

|<span data-ttu-id="93927-122">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-122">Attribute</span></span>  |<span data-ttu-id="93927-123">Escriba</span><span class="sxs-lookup"><span data-stu-id="93927-123">Type</span></span>   |<span data-ttu-id="93927-124">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="93927-124">Required</span></span>| <span data-ttu-id="93927-125">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="93927-125">Default</span></span> | <span data-ttu-id="93927-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="93927-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="93927-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="93927-128">duration</span><span class="sxs-lookup"><span data-stu-id="93927-128">duration</span></span>|<span data-ttu-id="93927-129">Opcional</span><span class="sxs-lookup"><span data-stu-id="93927-129">Optional</span></span> | <span data-ttu-id="93927-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="93927-130">PT1M</span></span>| <span data-ttu-id="93927-131">Especifica el intervalo en el que el monitor de diagnóstico sondea los cambios de configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="93927-131">Specifies the interval at which the diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="93927-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="93927-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="93927-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="93927-133">unsignedInt</span></span>|<span data-ttu-id="93927-134">Opcional</span><span class="sxs-lookup"><span data-stu-id="93927-134">Optional</span></span>| <span data-ttu-id="93927-135">4000 MB.</span><span class="sxs-lookup"><span data-stu-id="93927-135">4000 MB.</span></span> <span data-ttu-id="93927-136">Si proporciona un valor, no debe superar esta cantidad.</span><span class="sxs-lookup"><span data-stu-id="93927-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="93927-137">La cantidad total de almacenamiento del sistema de archivos asignada para todos los búferes de registro.</span><span class="sxs-lookup"><span data-stu-id="93927-137">The total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="93927-138">Elemento DiagnosticInfrastructureLogs</span><span class="sxs-lookup"><span data-stu-id="93927-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="93927-139">Define la configuración de búfer para los registros generados por la infraestructura de diagnóstico subyacente.</span><span class="sxs-lookup"><span data-stu-id="93927-139">Defines the buffer configuration for the logs that are generated by the underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="93927-140">Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="93927-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="93927-141">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-141">Attributes:</span></span>

|<span data-ttu-id="93927-142">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-142">Attribute</span></span>|<span data-ttu-id="93927-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-143">Type</span></span>|<span data-ttu-id="93927-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="93927-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="93927-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="93927-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="93927-146">unsignedInt</span></span>|<span data-ttu-id="93927-147">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-147">Optional.</span></span> <span data-ttu-id="93927-148">Especifica la cantidad máxima de almacenamiento del sistema de archivos que está disponible para los datos especificados.</span><span class="sxs-lookup"><span data-stu-id="93927-148">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="93927-149">El valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="93927-149">The default is 0.</span></span>|  
|<span data-ttu-id="93927-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="93927-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="93927-151">cadena</span><span class="sxs-lookup"><span data-stu-id="93927-151">string</span></span>|<span data-ttu-id="93927-152">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-152">Optional.</span></span> <span data-ttu-id="93927-153">Especifica el nivel de gravedad mínimo para las entradas de registro que se van a transferir.</span><span class="sxs-lookup"><span data-stu-id="93927-153">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="93927-154">El valor predeterminado es **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="93927-154">The default value is **Undefined**.</span></span> <span data-ttu-id="93927-155">Otros valores posibles son **Verbose**, **Information**, **Warning**, **Error** y **Critical**.</span><span class="sxs-lookup"><span data-stu-id="93927-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="93927-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="93927-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="93927-157">duration</span><span class="sxs-lookup"><span data-stu-id="93927-157">duration</span></span>|<span data-ttu-id="93927-158">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-158">Optional.</span></span> <span data-ttu-id="93927-159">Especifica el intervalo existente entre las transferencias programadas de datos, redondeado al minuto más cercano.</span><span class="sxs-lookup"><span data-stu-id="93927-159">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="93927-160">El valor predeterminado es PT0S.</span><span class="sxs-lookup"><span data-stu-id="93927-160">The default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="93927-161">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="93927-161">Logs Element</span></span>  
 <span data-ttu-id="93927-162">Define la configuración del búfer para los registros básicos de Azure.</span><span class="sxs-lookup"><span data-stu-id="93927-162">Defines the buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="93927-163">Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="93927-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="93927-164">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-164">Attributes:</span></span>  

|<span data-ttu-id="93927-165">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-165">Attribute</span></span>|<span data-ttu-id="93927-166">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-166">Type</span></span>|<span data-ttu-id="93927-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="93927-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="93927-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="93927-169">unsignedInt</span></span>|<span data-ttu-id="93927-170">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-170">Optional.</span></span> <span data-ttu-id="93927-171">Especifica la cantidad máxima de almacenamiento del sistema de archivos que está disponible para los datos especificados.</span><span class="sxs-lookup"><span data-stu-id="93927-171">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="93927-172">El valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="93927-172">The default is 0.</span></span>|  
|<span data-ttu-id="93927-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="93927-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="93927-174">cadena</span><span class="sxs-lookup"><span data-stu-id="93927-174">string</span></span>|<span data-ttu-id="93927-175">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-175">Optional.</span></span> <span data-ttu-id="93927-176">Especifica el nivel de gravedad mínimo para las entradas de registro que se van a transferir.</span><span class="sxs-lookup"><span data-stu-id="93927-176">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="93927-177">El valor predeterminado es **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="93927-177">The default value is **Undefined**.</span></span> <span data-ttu-id="93927-178">Otros valores posibles son **Verbose**, **Information**, **Warning**, **Error** y **Critical**.</span><span class="sxs-lookup"><span data-stu-id="93927-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="93927-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="93927-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="93927-180">duration</span><span class="sxs-lookup"><span data-stu-id="93927-180">duration</span></span>|<span data-ttu-id="93927-181">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-181">Optional.</span></span> <span data-ttu-id="93927-182">Especifica el intervalo existente entre las transferencias programadas de datos, redondeado al minuto más cercano.</span><span class="sxs-lookup"><span data-stu-id="93927-182">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="93927-183">El valor predeterminado es PT0S.</span><span class="sxs-lookup"><span data-stu-id="93927-183">The default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="93927-184">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="93927-184">Directories Element</span></span>  
<span data-ttu-id="93927-185">Define la configuración de búfer para los registros basados en archivos que se pueden definir.</span><span class="sxs-lookup"><span data-stu-id="93927-185">Defines the buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="93927-186">Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="93927-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="93927-187">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-187">Attributes:</span></span>  

|<span data-ttu-id="93927-188">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-188">Attribute</span></span>|<span data-ttu-id="93927-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-189">Type</span></span>|<span data-ttu-id="93927-190">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="93927-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="93927-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="93927-192">unsignedInt</span></span>|<span data-ttu-id="93927-193">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-193">Optional.</span></span> <span data-ttu-id="93927-194">Especifica la cantidad máxima de almacenamiento del sistema de archivos que está disponible para los datos especificados.</span><span class="sxs-lookup"><span data-stu-id="93927-194">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="93927-195">El valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="93927-195">The default is 0.</span></span>|  
|<span data-ttu-id="93927-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="93927-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="93927-197">duration</span><span class="sxs-lookup"><span data-stu-id="93927-197">duration</span></span>|<span data-ttu-id="93927-198">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-198">Optional.</span></span> <span data-ttu-id="93927-199">Especifica el intervalo existente entre las transferencias programadas de datos, redondeado al minuto más cercano.</span><span class="sxs-lookup"><span data-stu-id="93927-199">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="93927-200">El valor predeterminado es PT0S.</span><span class="sxs-lookup"><span data-stu-id="93927-200">The default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="93927-201">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="93927-201">CrashDumps Element</span></span>  
 <span data-ttu-id="93927-202">Define el directorio de archivos de volcado de memoria.</span><span class="sxs-lookup"><span data-stu-id="93927-202">Defines the crash dumps directory.</span></span>

 <span data-ttu-id="93927-203">Elemento principal: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="93927-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="93927-204">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-204">Attributes:</span></span>  

|<span data-ttu-id="93927-205">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-205">Attribute</span></span>|<span data-ttu-id="93927-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-206">Type</span></span>|<span data-ttu-id="93927-207">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-208">**container**</span><span class="sxs-lookup"><span data-stu-id="93927-208">**container**</span></span>|<span data-ttu-id="93927-209">cadena</span><span class="sxs-lookup"><span data-stu-id="93927-209">string</span></span>|<span data-ttu-id="93927-210">El nombre del contenedor donde es se va a transferir el contenido del directorio.</span><span class="sxs-lookup"><span data-stu-id="93927-210">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="93927-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="93927-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="93927-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="93927-212">unsignedInt</span></span>|<span data-ttu-id="93927-213">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-213">Optional.</span></span> <span data-ttu-id="93927-214">Especifica el tamaño máximo del directorio en megabytes.</span><span class="sxs-lookup"><span data-stu-id="93927-214">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="93927-215">El valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="93927-215">The default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="93927-216">Elemento FailedRequestLogs</span><span class="sxs-lookup"><span data-stu-id="93927-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="93927-217">Define el directorio de registro de solicitudes con error.</span><span class="sxs-lookup"><span data-stu-id="93927-217">Defines the failed request log directory.</span></span>

 <span data-ttu-id="93927-218">Elemento principal: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="93927-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="93927-219">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-219">Attributes:</span></span>  

|<span data-ttu-id="93927-220">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-220">Attribute</span></span>|<span data-ttu-id="93927-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-221">Type</span></span>|<span data-ttu-id="93927-222">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-223">**container**</span><span class="sxs-lookup"><span data-stu-id="93927-223">**container**</span></span>|<span data-ttu-id="93927-224">cadena</span><span class="sxs-lookup"><span data-stu-id="93927-224">string</span></span>|<span data-ttu-id="93927-225">El nombre del contenedor donde es se va a transferir el contenido del directorio.</span><span class="sxs-lookup"><span data-stu-id="93927-225">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="93927-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="93927-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="93927-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="93927-227">unsignedInt</span></span>|<span data-ttu-id="93927-228">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-228">Optional.</span></span> <span data-ttu-id="93927-229">Especifica el tamaño máximo del directorio en megabytes.</span><span class="sxs-lookup"><span data-stu-id="93927-229">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="93927-230">El valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="93927-230">The default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="93927-231">Elemento IISLogs</span><span class="sxs-lookup"><span data-stu-id="93927-231">IISLogs Element</span></span>  
 <span data-ttu-id="93927-232">Define el directorio de registro de IIS.</span><span class="sxs-lookup"><span data-stu-id="93927-232">Defines the IIS log directory.</span></span>

 <span data-ttu-id="93927-233">Elemento principal: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="93927-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="93927-234">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-234">Attributes:</span></span>  

|<span data-ttu-id="93927-235">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-235">Attribute</span></span>|<span data-ttu-id="93927-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-236">Type</span></span>|<span data-ttu-id="93927-237">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-238">**container**</span><span class="sxs-lookup"><span data-stu-id="93927-238">**container**</span></span>|<span data-ttu-id="93927-239">cadena</span><span class="sxs-lookup"><span data-stu-id="93927-239">string</span></span>|<span data-ttu-id="93927-240">El nombre del contenedor donde es se va a transferir el contenido del directorio.</span><span class="sxs-lookup"><span data-stu-id="93927-240">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="93927-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="93927-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="93927-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="93927-242">unsignedInt</span></span>|<span data-ttu-id="93927-243">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-243">Optional.</span></span> <span data-ttu-id="93927-244">Especifica el tamaño máximo del directorio en megabytes.</span><span class="sxs-lookup"><span data-stu-id="93927-244">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="93927-245">El valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="93927-245">The default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="93927-246">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="93927-246">DataSources Element</span></span>  
 <span data-ttu-id="93927-247">Define cero o más directorios de registro adicionales.</span><span class="sxs-lookup"><span data-stu-id="93927-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="93927-248">Elemento principal: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="93927-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="93927-249">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="93927-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="93927-250">Define el directorio de archivos de registro que se va a supervisar.</span><span class="sxs-lookup"><span data-stu-id="93927-250">Defines the directory of log files to monitor.</span></span>

 <span data-ttu-id="93927-251">Elemento principal: [elemento DataSources](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="93927-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="93927-252">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-252">Attributes:</span></span>

|<span data-ttu-id="93927-253">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-253">Attribute</span></span>|<span data-ttu-id="93927-254">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-254">Type</span></span>|<span data-ttu-id="93927-255">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-256">**container**</span><span class="sxs-lookup"><span data-stu-id="93927-256">**container**</span></span>|<span data-ttu-id="93927-257">cadena</span><span class="sxs-lookup"><span data-stu-id="93927-257">string</span></span>|<span data-ttu-id="93927-258">El nombre del contenedor donde es se va a transferir el contenido del directorio.</span><span class="sxs-lookup"><span data-stu-id="93927-258">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="93927-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="93927-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="93927-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="93927-260">unsignedInt</span></span>|<span data-ttu-id="93927-261">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-261">Optional.</span></span> <span data-ttu-id="93927-262">Especifica el tamaño máximo del directorio en megabytes.</span><span class="sxs-lookup"><span data-stu-id="93927-262">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="93927-263">El valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="93927-263">The default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="93927-264">Elemento Absolute</span><span class="sxs-lookup"><span data-stu-id="93927-264">Absolute Element</span></span>  
 <span data-ttu-id="93927-265">Define una ruta de acceso absoluta del directorio que se va a supervisar con expansión de entorno opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-265">Defines an absolute path of the directory to monitor with optional environment expansion.</span></span>

 <span data-ttu-id="93927-266">Elemento principal: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="93927-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="93927-267">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-267">Attributes:</span></span>  

|<span data-ttu-id="93927-268">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-268">Attribute</span></span>|<span data-ttu-id="93927-269">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-269">Type</span></span>|<span data-ttu-id="93927-270">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-271">**path**</span><span class="sxs-lookup"><span data-stu-id="93927-271">**path**</span></span>|<span data-ttu-id="93927-272">string</span><span class="sxs-lookup"><span data-stu-id="93927-272">string</span></span>|<span data-ttu-id="93927-273">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="93927-273">Required.</span></span> <span data-ttu-id="93927-274">La ruta de acceso absoluta al directorio que se va a supervisar.</span><span class="sxs-lookup"><span data-stu-id="93927-274">The absolute path to the directory to monitor.</span></span>|  
|<span data-ttu-id="93927-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="93927-275">**expandEnvironment**</span></span>|<span data-ttu-id="93927-276">boolean</span><span class="sxs-lookup"><span data-stu-id="93927-276">boolean</span></span>|<span data-ttu-id="93927-277">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="93927-277">Required.</span></span> <span data-ttu-id="93927-278">Si establece en **true**, las variables de entorno de la ruta de acceso se expanden.</span><span class="sxs-lookup"><span data-stu-id="93927-278">If set to **true**, environment variables in the path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="93927-279">Elemento LocalResource</span><span class="sxs-lookup"><span data-stu-id="93927-279">LocalResource Element</span></span>  
 <span data-ttu-id="93927-280">Define una ruta de acceso relativa a un recurso local definido en la definición del servicio.</span><span class="sxs-lookup"><span data-stu-id="93927-280">Defines a path relative to a local resource defined in the service definition.</span></span>

 <span data-ttu-id="93927-281">Elemento principal: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="93927-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="93927-282">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-282">Attributes:</span></span>  

|<span data-ttu-id="93927-283">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-283">Attribute</span></span>|<span data-ttu-id="93927-284">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-284">Type</span></span>|<span data-ttu-id="93927-285">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-286">**name**</span><span class="sxs-lookup"><span data-stu-id="93927-286">**name**</span></span>|<span data-ttu-id="93927-287">string</span><span class="sxs-lookup"><span data-stu-id="93927-287">string</span></span>|<span data-ttu-id="93927-288">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="93927-288">Required.</span></span> <span data-ttu-id="93927-289">El nombre del recurso local que contiene el directorio que se va a supervisar.</span><span class="sxs-lookup"><span data-stu-id="93927-289">The name of the local resource that contains the directory to monitor.</span></span>|  
|<span data-ttu-id="93927-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="93927-290">**relativePath**</span></span>|<span data-ttu-id="93927-291">string</span><span class="sxs-lookup"><span data-stu-id="93927-291">string</span></span>|<span data-ttu-id="93927-292">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="93927-292">Required.</span></span> <span data-ttu-id="93927-293">La ruta de acceso relativa al recurso local que se va a supervisar.</span><span class="sxs-lookup"><span data-stu-id="93927-293">The path relative to the local resource to monitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="93927-294">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="93927-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="93927-295">Define la ruta de acceso al contador de rendimiento que se va a recopilar.</span><span class="sxs-lookup"><span data-stu-id="93927-295">Defines the path to the performance counter to collect.</span></span>

 <span data-ttu-id="93927-296">Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="93927-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="93927-297">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-297">Attributes:</span></span>  

|<span data-ttu-id="93927-298">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-298">Attribute</span></span>|<span data-ttu-id="93927-299">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-299">Type</span></span>|<span data-ttu-id="93927-300">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="93927-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="93927-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="93927-302">unsignedInt</span></span>|<span data-ttu-id="93927-303">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-303">Optional.</span></span> <span data-ttu-id="93927-304">Especifica la cantidad máxima de almacenamiento del sistema de archivos que está disponible para los datos especificados.</span><span class="sxs-lookup"><span data-stu-id="93927-304">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="93927-305">El valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="93927-305">The default is 0.</span></span>|  
|<span data-ttu-id="93927-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="93927-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="93927-307">duration</span><span class="sxs-lookup"><span data-stu-id="93927-307">duration</span></span>|<span data-ttu-id="93927-308">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-308">Optional.</span></span> <span data-ttu-id="93927-309">Especifica el intervalo existente entre las transferencias programadas de datos, redondeado al minuto más cercano.</span><span class="sxs-lookup"><span data-stu-id="93927-309">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="93927-310">El valor predeterminado es PT0S.</span><span class="sxs-lookup"><span data-stu-id="93927-310">The default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="93927-311">Elemento PerformanceCounterConfiguration</span><span class="sxs-lookup"><span data-stu-id="93927-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="93927-312">Define el contador de rendimiento que se va a recopilar.</span><span class="sxs-lookup"><span data-stu-id="93927-312">Defines the performance counter to collect.</span></span>

 <span data-ttu-id="93927-313">Elemento principal: [elemento PerformanceCounters](#PerformanceCounters)</span><span class="sxs-lookup"><span data-stu-id="93927-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="93927-314">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-314">Attributes:</span></span>  

|<span data-ttu-id="93927-315">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-315">Attribute</span></span>|<span data-ttu-id="93927-316">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-316">Type</span></span>|<span data-ttu-id="93927-317">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="93927-318">**counterSpecifier**</span></span>|<span data-ttu-id="93927-319">string</span><span class="sxs-lookup"><span data-stu-id="93927-319">string</span></span>|<span data-ttu-id="93927-320">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="93927-320">Required.</span></span> <span data-ttu-id="93927-321">La ruta de acceso al contador de rendimiento que se va a recopilar.</span><span class="sxs-lookup"><span data-stu-id="93927-321">The path to the performance counter to collect.</span></span>|  
|<span data-ttu-id="93927-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="93927-322">**sampleRate**</span></span>|<span data-ttu-id="93927-323">duration</span><span class="sxs-lookup"><span data-stu-id="93927-323">duration</span></span>|<span data-ttu-id="93927-324">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="93927-324">Required.</span></span> <span data-ttu-id="93927-325">La velocidad a la que se debe recopilar el contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="93927-325">The rate at which the performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="93927-326">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="93927-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="93927-327">Define los registros de eventos que se van a supervisar.</span><span class="sxs-lookup"><span data-stu-id="93927-327">Defines the event logs to monitor.</span></span>

 <span data-ttu-id="93927-328">Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="93927-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="93927-329">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-329">Attributes:</span></span>

|<span data-ttu-id="93927-330">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-330">Attribute</span></span>|<span data-ttu-id="93927-331">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-331">Type</span></span>|<span data-ttu-id="93927-332">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="93927-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="93927-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="93927-334">unsignedInt</span></span>|<span data-ttu-id="93927-335">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-335">Optional.</span></span> <span data-ttu-id="93927-336">Especifica la cantidad máxima de almacenamiento del sistema de archivos que está disponible para los datos especificados.</span><span class="sxs-lookup"><span data-stu-id="93927-336">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="93927-337">El valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="93927-337">The default is 0.</span></span>|  
|<span data-ttu-id="93927-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="93927-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="93927-339">cadena</span><span class="sxs-lookup"><span data-stu-id="93927-339">string</span></span>|<span data-ttu-id="93927-340">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-340">Optional.</span></span> <span data-ttu-id="93927-341">Especifica el nivel de gravedad mínimo para las entradas de registro que se van a transferir.</span><span class="sxs-lookup"><span data-stu-id="93927-341">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="93927-342">El valor predeterminado es **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="93927-342">The default value is **Undefined**.</span></span> <span data-ttu-id="93927-343">Otros valores posibles son **Verbose**, **Information**, **Warning**, **Error** y **Critical**.</span><span class="sxs-lookup"><span data-stu-id="93927-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="93927-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="93927-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="93927-345">duration</span><span class="sxs-lookup"><span data-stu-id="93927-345">duration</span></span>|<span data-ttu-id="93927-346">Opcional.</span><span class="sxs-lookup"><span data-stu-id="93927-346">Optional.</span></span> <span data-ttu-id="93927-347">Especifica el intervalo existente entre las transferencias programadas de datos, redondeado al minuto más cercano.</span><span class="sxs-lookup"><span data-stu-id="93927-347">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="93927-348">El valor predeterminado es PT0S.</span><span class="sxs-lookup"><span data-stu-id="93927-348">The default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="93927-349">Elemento DataSource</span><span class="sxs-lookup"><span data-stu-id="93927-349">DataSource Element</span></span>  
 <span data-ttu-id="93927-350">Define el registro de eventos que se va a supervisar.</span><span class="sxs-lookup"><span data-stu-id="93927-350">Defines the event log to monitor.</span></span>

 <span data-ttu-id="93927-351">Elemento principal: [elemento WindowsEventLog](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="93927-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="93927-352">Atributos:</span><span class="sxs-lookup"><span data-stu-id="93927-352">Attributes:</span></span>

|<span data-ttu-id="93927-353">Atributo</span><span class="sxs-lookup"><span data-stu-id="93927-353">Attribute</span></span>|<span data-ttu-id="93927-354">Tipo</span><span class="sxs-lookup"><span data-stu-id="93927-354">Type</span></span>|<span data-ttu-id="93927-355">Descripción</span><span class="sxs-lookup"><span data-stu-id="93927-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="93927-356">**name**</span><span class="sxs-lookup"><span data-stu-id="93927-356">**name**</span></span>|<span data-ttu-id="93927-357">string</span><span class="sxs-lookup"><span data-stu-id="93927-357">string</span></span>|<span data-ttu-id="93927-358">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="93927-358">Required.</span></span> <span data-ttu-id="93927-359">Expresión XPath que especifica el registro que se va a recopilar.</span><span class="sxs-lookup"><span data-stu-id="93927-359">An XPath expression specifying the log to collect.</span></span>|  
