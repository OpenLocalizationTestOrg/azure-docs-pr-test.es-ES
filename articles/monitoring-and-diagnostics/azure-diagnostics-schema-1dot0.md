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
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="1e296-103">Esquema de configuración de Diagnósticos de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1e296-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="1e296-104">Diagnósticos de Azure es Hola componente usado toocollect los contadores de rendimiento y otras estadísticas de máquinas virtuales de Azure, conjuntos de escalas de máquina Virtual, Service Fabric y servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="1e296-104">Azure Diagnostics is hello component used toocollect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="1e296-105">Esta página solo es pertinente si está usando uno de estos servicios.</span><span class="sxs-lookup"><span data-stu-id="1e296-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="1e296-106">Diagnósticos de Azure se usa con otros productos de diagnósticos de Microsoft, como Azure Monitor, Application Insights y Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1e296-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="1e296-107">archivo de configuración de diagnósticos de Azure de Hello define valores que son usados tooinitialize Hola Monitor de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="1e296-107">hello Azure Diagnostics configuration file defines values that are used tooinitialize hello Diagnostics Monitor.</span></span> <span data-ttu-id="1e296-108">Este archivo es configuración de diagnóstico de tooinitialize usado cuando inicia de monitor de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e296-108">This file is used tooinitialize diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

 <span data-ttu-id="1e296-109">De forma predeterminada, archivo de esquema de configuración de diagnósticos de Azure de hello es toohello instalado `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span><span class="sxs-lookup"><span data-stu-id="1e296-109">By default, hello Azure Diagnostics configuration schema file is installed toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="1e296-110">Reemplace `<version>` con la versión de Hola instalado de hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1e296-110">Replace `<version>` with hello installed version of hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="1e296-111">archivo de configuración de diagnósticos de Hola se suele utilizar con las tareas de inicio que requieren toobe de datos de diagnóstico recopilada anteriormente en el proceso de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e296-111">hello diagnostics configuration file is typically used with startup tasks that require diagnostic data toobe collected earlier in hello startup process.</span></span> <span data-ttu-id="1e296-112">Para más información sobre Diagnósticos de Azure, consulte [Recopilación de datos de registro mediante Diagnósticos de Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="1e296-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="1e296-113">Ejemplo de archivo de configuración de diagnósticos de Hola</span><span class="sxs-lookup"><span data-stu-id="1e296-113">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="1e296-114">Hola de ejemplo siguiente muestra un archivo de configuración de diagnóstico típico:</span><span class="sxs-lookup"><span data-stu-id="1e296-114">hello following example shows a typical diagnostics configuration file:</span></span>  

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

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="1e296-115">Espacio de nombres DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="1e296-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="1e296-116">espacio de nombres XML de Hello para el archivo de configuración de diagnósticos de hello es:</span><span class="sxs-lookup"><span data-stu-id="1e296-116">hello XML namespace for hello diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="1e296-117">Elementos de esquema</span><span class="sxs-lookup"><span data-stu-id="1e296-117">Schema Elements</span></span>  
 <span data-ttu-id="1e296-118">archivo de configuración de diagnósticos de Hello incluye Hola siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="1e296-118">hello diagnostics configuration file includes hello following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="1e296-119">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="1e296-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="1e296-120">elemento de nivel superior de Hola Hola diagnósticos del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="1e296-120">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="1e296-121">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-121">Attributes:</span></span>

|<span data-ttu-id="1e296-122">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-122">Attribute</span></span>  |<span data-ttu-id="1e296-123">Escriba</span><span class="sxs-lookup"><span data-stu-id="1e296-123">Type</span></span>   |<span data-ttu-id="1e296-124">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1e296-124">Required</span></span>| <span data-ttu-id="1e296-125">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="1e296-125">Default</span></span> | <span data-ttu-id="1e296-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="1e296-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="1e296-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="1e296-128">duration</span><span class="sxs-lookup"><span data-stu-id="1e296-128">duration</span></span>|<span data-ttu-id="1e296-129">Opcional</span><span class="sxs-lookup"><span data-stu-id="1e296-129">Optional</span></span> | <span data-ttu-id="1e296-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="1e296-130">PT1M</span></span>| <span data-ttu-id="1e296-131">Especifica el intervalo de hello en los sondeos de monitor de diagnóstico de Hola para cambios de configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="1e296-131">Specifies hello interval at which hello diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="1e296-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1e296-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="1e296-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1e296-133">unsignedInt</span></span>|<span data-ttu-id="1e296-134">Opcional</span><span class="sxs-lookup"><span data-stu-id="1e296-134">Optional</span></span>| <span data-ttu-id="1e296-135">4000 MB.</span><span class="sxs-lookup"><span data-stu-id="1e296-135">4000 MB.</span></span> <span data-ttu-id="1e296-136">Si proporciona un valor, no debe superar esta cantidad.</span><span class="sxs-lookup"><span data-stu-id="1e296-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="1e296-137">cantidad total de Hola de almacenamiento del sistema de archivos asignado para todos los búferes de registro.</span><span class="sxs-lookup"><span data-stu-id="1e296-137">hello total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="1e296-138">Elemento DiagnosticInfrastructureLogs</span><span class="sxs-lookup"><span data-stu-id="1e296-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="1e296-139">Define la configuración de búfer de Hola para registros de hello generadas por la infraestructura de diagnóstico subyacente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e296-139">Defines hello buffer configuration for hello logs that are generated by hello underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="1e296-140">Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1e296-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="1e296-141">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-141">Attributes:</span></span>

|<span data-ttu-id="1e296-142">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-142">Attribute</span></span>|<span data-ttu-id="1e296-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-143">Type</span></span>|<span data-ttu-id="1e296-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="1e296-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1e296-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="1e296-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1e296-146">unsignedInt</span></span>|<span data-ttu-id="1e296-147">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-147">Optional.</span></span> <span data-ttu-id="1e296-148">Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.</span><span class="sxs-lookup"><span data-stu-id="1e296-148">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="1e296-149">Hola predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="1e296-149">hello default is 0.</span></span>|  
|<span data-ttu-id="1e296-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="1e296-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="1e296-151">cadena</span><span class="sxs-lookup"><span data-stu-id="1e296-151">string</span></span>|<span data-ttu-id="1e296-152">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-152">Optional.</span></span> <span data-ttu-id="1e296-153">Especifica el nivel de gravedad mínimo de Hola para las entradas de registro que se transfieren.</span><span class="sxs-lookup"><span data-stu-id="1e296-153">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="1e296-154">es el valor predeterminado de Hello **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="1e296-154">hello default value is **Undefined**.</span></span> <span data-ttu-id="1e296-155">Otros valores posibles son **Verbose**, **Information**, **Warning**, **Error** y **Critical**.</span><span class="sxs-lookup"><span data-stu-id="1e296-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="1e296-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="1e296-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="1e296-157">duration</span><span class="sxs-lookup"><span data-stu-id="1e296-157">duration</span></span>|<span data-ttu-id="1e296-158">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-158">Optional.</span></span> <span data-ttu-id="1e296-159">Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="1e296-159">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="1e296-160">valor predeterminado de Hello es PT0S.</span><span class="sxs-lookup"><span data-stu-id="1e296-160">hello default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="1e296-161">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="1e296-161">Logs Element</span></span>  
 <span data-ttu-id="1e296-162">Define la configuración de búfer de Hola para los registros básicos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e296-162">Defines hello buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="1e296-163">Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1e296-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="1e296-164">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-164">Attributes:</span></span>  

|<span data-ttu-id="1e296-165">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-165">Attribute</span></span>|<span data-ttu-id="1e296-166">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-166">Type</span></span>|<span data-ttu-id="1e296-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1e296-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="1e296-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1e296-169">unsignedInt</span></span>|<span data-ttu-id="1e296-170">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-170">Optional.</span></span> <span data-ttu-id="1e296-171">Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.</span><span class="sxs-lookup"><span data-stu-id="1e296-171">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="1e296-172">Hola predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="1e296-172">hello default is 0.</span></span>|  
|<span data-ttu-id="1e296-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="1e296-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="1e296-174">cadena</span><span class="sxs-lookup"><span data-stu-id="1e296-174">string</span></span>|<span data-ttu-id="1e296-175">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-175">Optional.</span></span> <span data-ttu-id="1e296-176">Especifica el nivel de gravedad mínimo de Hola para las entradas de registro que se transfieren.</span><span class="sxs-lookup"><span data-stu-id="1e296-176">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="1e296-177">es el valor predeterminado de Hello **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="1e296-177">hello default value is **Undefined**.</span></span> <span data-ttu-id="1e296-178">Otros valores posibles son **Verbose**, **Information**, **Warning**, **Error** y **Critical**.</span><span class="sxs-lookup"><span data-stu-id="1e296-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="1e296-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="1e296-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="1e296-180">duration</span><span class="sxs-lookup"><span data-stu-id="1e296-180">duration</span></span>|<span data-ttu-id="1e296-181">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-181">Optional.</span></span> <span data-ttu-id="1e296-182">Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="1e296-182">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="1e296-183">valor predeterminado de Hello es PT0S.</span><span class="sxs-lookup"><span data-stu-id="1e296-183">hello default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="1e296-184">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="1e296-184">Directories Element</span></span>  
<span data-ttu-id="1e296-185">Define la configuración de búfer de Hola para los registros basados en archivos que se pueden definir.</span><span class="sxs-lookup"><span data-stu-id="1e296-185">Defines hello buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="1e296-186">Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1e296-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="1e296-187">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-187">Attributes:</span></span>  

|<span data-ttu-id="1e296-188">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-188">Attribute</span></span>|<span data-ttu-id="1e296-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-189">Type</span></span>|<span data-ttu-id="1e296-190">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1e296-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="1e296-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1e296-192">unsignedInt</span></span>|<span data-ttu-id="1e296-193">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-193">Optional.</span></span> <span data-ttu-id="1e296-194">Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.</span><span class="sxs-lookup"><span data-stu-id="1e296-194">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="1e296-195">Hola predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="1e296-195">hello default is 0.</span></span>|  
|<span data-ttu-id="1e296-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="1e296-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="1e296-197">duration</span><span class="sxs-lookup"><span data-stu-id="1e296-197">duration</span></span>|<span data-ttu-id="1e296-198">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-198">Optional.</span></span> <span data-ttu-id="1e296-199">Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="1e296-199">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="1e296-200">valor predeterminado de Hello es PT0S.</span><span class="sxs-lookup"><span data-stu-id="1e296-200">hello default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="1e296-201">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="1e296-201">CrashDumps Element</span></span>  
 <span data-ttu-id="1e296-202">Define el directorio de archivos de volcado de bloqueo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e296-202">Defines hello crash dumps directory.</span></span>

 <span data-ttu-id="1e296-203">Elemento principal: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="1e296-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="1e296-204">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-204">Attributes:</span></span>  

|<span data-ttu-id="1e296-205">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-205">Attribute</span></span>|<span data-ttu-id="1e296-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-206">Type</span></span>|<span data-ttu-id="1e296-207">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-208">**container**</span><span class="sxs-lookup"><span data-stu-id="1e296-208">**container**</span></span>|<span data-ttu-id="1e296-209">cadena</span><span class="sxs-lookup"><span data-stu-id="1e296-209">string</span></span>|<span data-ttu-id="1e296-210">nombre del saludo del contenedor de Hola donde el contenido de hello del directorio de hello es toobe transfiere.</span><span class="sxs-lookup"><span data-stu-id="1e296-210">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="1e296-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1e296-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="1e296-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1e296-212">unsignedInt</span></span>|<span data-ttu-id="1e296-213">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-213">Optional.</span></span> <span data-ttu-id="1e296-214">Especifica el tamaño máximo de hello del directorio de hello en megabytes.</span><span class="sxs-lookup"><span data-stu-id="1e296-214">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="1e296-215">Hola predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="1e296-215">hello default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="1e296-216">Elemento FailedRequestLogs</span><span class="sxs-lookup"><span data-stu-id="1e296-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="1e296-217">Define el directorio de registro de solicitudes con error de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e296-217">Defines hello failed request log directory.</span></span>

 <span data-ttu-id="1e296-218">Elemento principal: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="1e296-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="1e296-219">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-219">Attributes:</span></span>  

|<span data-ttu-id="1e296-220">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-220">Attribute</span></span>|<span data-ttu-id="1e296-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-221">Type</span></span>|<span data-ttu-id="1e296-222">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-223">**container**</span><span class="sxs-lookup"><span data-stu-id="1e296-223">**container**</span></span>|<span data-ttu-id="1e296-224">cadena</span><span class="sxs-lookup"><span data-stu-id="1e296-224">string</span></span>|<span data-ttu-id="1e296-225">nombre del saludo del contenedor de Hola donde el contenido de hello del directorio de hello es toobe transfiere.</span><span class="sxs-lookup"><span data-stu-id="1e296-225">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="1e296-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1e296-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="1e296-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1e296-227">unsignedInt</span></span>|<span data-ttu-id="1e296-228">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-228">Optional.</span></span> <span data-ttu-id="1e296-229">Especifica el tamaño máximo de hello del directorio de hello en megabytes.</span><span class="sxs-lookup"><span data-stu-id="1e296-229">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="1e296-230">Hola predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="1e296-230">hello default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="1e296-231">Elemento IISLogs</span><span class="sxs-lookup"><span data-stu-id="1e296-231">IISLogs Element</span></span>  
 <span data-ttu-id="1e296-232">Define el directorio de registro IIS de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e296-232">Defines hello IIS log directory.</span></span>

 <span data-ttu-id="1e296-233">Elemento principal: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="1e296-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="1e296-234">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-234">Attributes:</span></span>  

|<span data-ttu-id="1e296-235">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-235">Attribute</span></span>|<span data-ttu-id="1e296-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-236">Type</span></span>|<span data-ttu-id="1e296-237">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-238">**container**</span><span class="sxs-lookup"><span data-stu-id="1e296-238">**container**</span></span>|<span data-ttu-id="1e296-239">cadena</span><span class="sxs-lookup"><span data-stu-id="1e296-239">string</span></span>|<span data-ttu-id="1e296-240">nombre del saludo del contenedor de Hola donde el contenido de hello del directorio de hello es toobe transfiere.</span><span class="sxs-lookup"><span data-stu-id="1e296-240">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="1e296-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1e296-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="1e296-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1e296-242">unsignedInt</span></span>|<span data-ttu-id="1e296-243">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-243">Optional.</span></span> <span data-ttu-id="1e296-244">Especifica el tamaño máximo de hello del directorio de hello en megabytes.</span><span class="sxs-lookup"><span data-stu-id="1e296-244">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="1e296-245">Hola predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="1e296-245">hello default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="1e296-246">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="1e296-246">DataSources Element</span></span>  
 <span data-ttu-id="1e296-247">Define cero o más directorios de registro adicionales.</span><span class="sxs-lookup"><span data-stu-id="1e296-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="1e296-248">Elemento principal: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="1e296-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="1e296-249">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="1e296-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="1e296-250">Define el directorio de Hola de toomonitor de archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="1e296-250">Defines hello directory of log files toomonitor.</span></span>

 <span data-ttu-id="1e296-251">Elemento principal: [elemento DataSources](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="1e296-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="1e296-252">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-252">Attributes:</span></span>

|<span data-ttu-id="1e296-253">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-253">Attribute</span></span>|<span data-ttu-id="1e296-254">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-254">Type</span></span>|<span data-ttu-id="1e296-255">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-256">**container**</span><span class="sxs-lookup"><span data-stu-id="1e296-256">**container**</span></span>|<span data-ttu-id="1e296-257">cadena</span><span class="sxs-lookup"><span data-stu-id="1e296-257">string</span></span>|<span data-ttu-id="1e296-258">nombre del saludo del contenedor de Hola donde el contenido de hello del directorio de hello es toobe transfiere.</span><span class="sxs-lookup"><span data-stu-id="1e296-258">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="1e296-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1e296-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="1e296-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1e296-260">unsignedInt</span></span>|<span data-ttu-id="1e296-261">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-261">Optional.</span></span> <span data-ttu-id="1e296-262">Especifica el tamaño máximo de hello del directorio de hello en megabytes.</span><span class="sxs-lookup"><span data-stu-id="1e296-262">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="1e296-263">Hola predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="1e296-263">hello default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="1e296-264">Elemento Absolute</span><span class="sxs-lookup"><span data-stu-id="1e296-264">Absolute Element</span></span>  
 <span data-ttu-id="1e296-265">Define una ruta de acceso absoluta de hello toomonitor de directorio con la extensión del entorno opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-265">Defines an absolute path of hello directory toomonitor with optional environment expansion.</span></span>

 <span data-ttu-id="1e296-266">Elemento principal: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1e296-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="1e296-267">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-267">Attributes:</span></span>  

|<span data-ttu-id="1e296-268">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-268">Attribute</span></span>|<span data-ttu-id="1e296-269">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-269">Type</span></span>|<span data-ttu-id="1e296-270">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-271">**path**</span><span class="sxs-lookup"><span data-stu-id="1e296-271">**path**</span></span>|<span data-ttu-id="1e296-272">string</span><span class="sxs-lookup"><span data-stu-id="1e296-272">string</span></span>|<span data-ttu-id="1e296-273">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1e296-273">Required.</span></span> <span data-ttu-id="1e296-274">Hola toomonitor de directorio toohello de ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="1e296-274">hello absolute path toohello directory toomonitor.</span></span>|  
|<span data-ttu-id="1e296-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="1e296-275">**expandEnvironment**</span></span>|<span data-ttu-id="1e296-276">boolean</span><span class="sxs-lookup"><span data-stu-id="1e296-276">boolean</span></span>|<span data-ttu-id="1e296-277">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1e296-277">Required.</span></span> <span data-ttu-id="1e296-278">Si establece demasiado**true**, las variables de entorno en la ruta de acceso de Hola se expanden.</span><span class="sxs-lookup"><span data-stu-id="1e296-278">If set too**true**, environment variables in hello path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="1e296-279">Elemento LocalResource</span><span class="sxs-lookup"><span data-stu-id="1e296-279">LocalResource Element</span></span>  
 <span data-ttu-id="1e296-280">Define un recurso local de ruta de acceso relativa tooa definido en la definición del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="1e296-280">Defines a path relative tooa local resource defined in hello service definition.</span></span>

 <span data-ttu-id="1e296-281">Elemento principal: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1e296-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="1e296-282">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-282">Attributes:</span></span>  

|<span data-ttu-id="1e296-283">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-283">Attribute</span></span>|<span data-ttu-id="1e296-284">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-284">Type</span></span>|<span data-ttu-id="1e296-285">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-286">**name**</span><span class="sxs-lookup"><span data-stu-id="1e296-286">**name**</span></span>|<span data-ttu-id="1e296-287">string</span><span class="sxs-lookup"><span data-stu-id="1e296-287">string</span></span>|<span data-ttu-id="1e296-288">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1e296-288">Required.</span></span> <span data-ttu-id="1e296-289">nombre de Hola de recurso local Hola que contiene Hola directory toomonitor.</span><span class="sxs-lookup"><span data-stu-id="1e296-289">hello name of hello local resource that contains hello directory toomonitor.</span></span>|  
|<span data-ttu-id="1e296-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="1e296-290">**relativePath**</span></span>|<span data-ttu-id="1e296-291">string</span><span class="sxs-lookup"><span data-stu-id="1e296-291">string</span></span>|<span data-ttu-id="1e296-292">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1e296-292">Required.</span></span> <span data-ttu-id="1e296-293">Hola toomonitor de ruta de acceso relativa toohello recurso local.</span><span class="sxs-lookup"><span data-stu-id="1e296-293">hello path relative toohello local resource toomonitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="1e296-294">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="1e296-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="1e296-295">Define toocollect de contador de rendimiento de hello ruta de acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="1e296-295">Defines hello path toohello performance counter toocollect.</span></span>

 <span data-ttu-id="1e296-296">Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1e296-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="1e296-297">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-297">Attributes:</span></span>  

|<span data-ttu-id="1e296-298">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-298">Attribute</span></span>|<span data-ttu-id="1e296-299">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-299">Type</span></span>|<span data-ttu-id="1e296-300">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1e296-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="1e296-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1e296-302">unsignedInt</span></span>|<span data-ttu-id="1e296-303">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-303">Optional.</span></span> <span data-ttu-id="1e296-304">Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.</span><span class="sxs-lookup"><span data-stu-id="1e296-304">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="1e296-305">Hola predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="1e296-305">hello default is 0.</span></span>|  
|<span data-ttu-id="1e296-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="1e296-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="1e296-307">duration</span><span class="sxs-lookup"><span data-stu-id="1e296-307">duration</span></span>|<span data-ttu-id="1e296-308">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-308">Optional.</span></span> <span data-ttu-id="1e296-309">Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="1e296-309">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="1e296-310">valor predeterminado de Hello es PT0S.</span><span class="sxs-lookup"><span data-stu-id="1e296-310">hello default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="1e296-311">Elemento PerformanceCounterConfiguration</span><span class="sxs-lookup"><span data-stu-id="1e296-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="1e296-312">Define toocollect de contador de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e296-312">Defines hello performance counter toocollect.</span></span>

 <span data-ttu-id="1e296-313">Elemento principal: [elemento PerformanceCounters](#PerformanceCounters)</span><span class="sxs-lookup"><span data-stu-id="1e296-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="1e296-314">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-314">Attributes:</span></span>  

|<span data-ttu-id="1e296-315">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-315">Attribute</span></span>|<span data-ttu-id="1e296-316">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-316">Type</span></span>|<span data-ttu-id="1e296-317">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="1e296-318">**counterSpecifier**</span></span>|<span data-ttu-id="1e296-319">string</span><span class="sxs-lookup"><span data-stu-id="1e296-319">string</span></span>|<span data-ttu-id="1e296-320">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1e296-320">Required.</span></span> <span data-ttu-id="1e296-321">Hola toocollect de contador de rendimiento de toohello de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="1e296-321">hello path toohello performance counter toocollect.</span></span>|  
|<span data-ttu-id="1e296-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="1e296-322">**sampleRate**</span></span>|<span data-ttu-id="1e296-323">duration</span><span class="sxs-lookup"><span data-stu-id="1e296-323">duration</span></span>|<span data-ttu-id="1e296-324">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1e296-324">Required.</span></span> <span data-ttu-id="1e296-325">velocidad de Hello en qué Hola se deben recopilar contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="1e296-325">hello rate at which hello performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="1e296-326">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="1e296-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="1e296-327">Define hello toomonitor de registros de eventos.</span><span class="sxs-lookup"><span data-stu-id="1e296-327">Defines hello event logs toomonitor.</span></span>

 <span data-ttu-id="1e296-328">Elemento principal: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1e296-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="1e296-329">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-329">Attributes:</span></span>

|<span data-ttu-id="1e296-330">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-330">Attribute</span></span>|<span data-ttu-id="1e296-331">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-331">Type</span></span>|<span data-ttu-id="1e296-332">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1e296-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="1e296-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1e296-334">unsignedInt</span></span>|<span data-ttu-id="1e296-335">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-335">Optional.</span></span> <span data-ttu-id="1e296-336">Especifica Hola cantidad máxima de almacenamiento del sistema de archivos que está disponible para hello especificado datos.</span><span class="sxs-lookup"><span data-stu-id="1e296-336">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="1e296-337">Hola predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="1e296-337">hello default is 0.</span></span>|  
|<span data-ttu-id="1e296-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="1e296-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="1e296-339">cadena</span><span class="sxs-lookup"><span data-stu-id="1e296-339">string</span></span>|<span data-ttu-id="1e296-340">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-340">Optional.</span></span> <span data-ttu-id="1e296-341">Especifica el nivel de gravedad mínimo de Hola para las entradas de registro que se transfieren.</span><span class="sxs-lookup"><span data-stu-id="1e296-341">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="1e296-342">es el valor predeterminado de Hello **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="1e296-342">hello default value is **Undefined**.</span></span> <span data-ttu-id="1e296-343">Otros valores posibles son **Verbose**, **Information**, **Warning**, **Error** y **Critical**.</span><span class="sxs-lookup"><span data-stu-id="1e296-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="1e296-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="1e296-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="1e296-345">duration</span><span class="sxs-lookup"><span data-stu-id="1e296-345">duration</span></span>|<span data-ttu-id="1e296-346">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1e296-346">Optional.</span></span> <span data-ttu-id="1e296-347">Especifica el intervalo de hello entre las transferencias programadas de datos, redondeado hasta toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="1e296-347">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="1e296-348">valor predeterminado de Hello es PT0S.</span><span class="sxs-lookup"><span data-stu-id="1e296-348">hello default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="1e296-349">Elemento DataSource</span><span class="sxs-lookup"><span data-stu-id="1e296-349">DataSource Element</span></span>  
 <span data-ttu-id="1e296-350">Define hello toomonitor de registro de eventos.</span><span class="sxs-lookup"><span data-stu-id="1e296-350">Defines hello event log toomonitor.</span></span>

 <span data-ttu-id="1e296-351">Elemento principal: [elemento WindowsEventLog](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="1e296-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="1e296-352">Atributos:</span><span class="sxs-lookup"><span data-stu-id="1e296-352">Attributes:</span></span>

|<span data-ttu-id="1e296-353">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e296-353">Attribute</span></span>|<span data-ttu-id="1e296-354">Tipo</span><span class="sxs-lookup"><span data-stu-id="1e296-354">Type</span></span>|<span data-ttu-id="1e296-355">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e296-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1e296-356">**name**</span><span class="sxs-lookup"><span data-stu-id="1e296-356">**name**</span></span>|<span data-ttu-id="1e296-357">string</span><span class="sxs-lookup"><span data-stu-id="1e296-357">string</span></span>|<span data-ttu-id="1e296-358">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1e296-358">Required.</span></span> <span data-ttu-id="1e296-359">Expresión XPath que especifica toocollect de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="1e296-359">An XPath expression specifying hello log toocollect.</span></span>|  
