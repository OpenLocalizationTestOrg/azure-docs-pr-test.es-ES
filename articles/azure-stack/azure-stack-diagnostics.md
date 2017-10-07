---
title: aaaDiagnostics en la pila de Azure | Documentos de Microsoft
description: "Cómo archivos de registro de toocollect para el diagnóstico en la pila de Azure"
services: azure-stack
documentationcenter: 
author: adshar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: adshar
ms.openlocfilehash: a4a5ddf29e75df710e9fae366d6ac16e6fb36d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-diagnostics-tools"></a><span data-ttu-id="b8d42-103">Herramientas de diagnóstico de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b8d42-103">Azure Stack diagnostics tools</span></span>
 
<span data-ttu-id="b8d42-104">Azure Stack es una gran colección de componentes que funcionan juntos e interactúan entre sí.</span><span class="sxs-lookup"><span data-stu-id="b8d42-104">Azure Stack is a large collection of components working together and interacting with each other.</span></span> <span data-ttu-id="b8d42-105">Todos estos componentes generan sus propios registros únicos, lo que significa que los problemas de diagnóstico pueden convertirse rápidamente en una tarea difícil, especialmente en el caso de los errores procedentes de varios componentes que interactúan en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b8d42-105">All these components  generate their own unique logs, which means that diagnosing issues can quickly become a challenging task, especially for errors coming from multiple interacting Azure Stack components.</span></span> 

<span data-ttu-id="b8d42-106">Nuestras herramientas de diagnóstico ayudan a asegurarse de que el mecanismo de recopilación de registro de hello es fácil y eficaz.</span><span class="sxs-lookup"><span data-stu-id="b8d42-106">Our diagnostics tools help make sure hello log collection mechanism is easy and efficient.</span></span> <span data-ttu-id="b8d42-107">Hello siguiente diagrama muestra cómo iniciar herramientas de recopilación en los trabajos de la pila de Azure:</span><span class="sxs-lookup"><span data-stu-id="b8d42-107">hello following diagram shows how log collection tools in Azure Stack work:</span></span>

![Herramientas de recopilación de registros](media/azure-stack-diagnostics/image01.png)
 
 
## <a name="trace-collector"></a><span data-ttu-id="b8d42-109">Recopilador de seguimiento</span><span class="sxs-lookup"><span data-stu-id="b8d42-109">Trace Collector</span></span>
 
<span data-ttu-id="b8d42-110">Hola recopilador de seguimiento está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b8d42-110">hello Trace Collector is enabled by default.</span></span> <span data-ttu-id="b8d42-111">Lo continuamente se ejecuta en segundo plano de Hola y recopila todos los registros de seguimiento de eventos para Windows (ETW) de servicios de componentes en la pila de Azure y almacenarlos en un recurso compartido local.</span><span class="sxs-lookup"><span data-stu-id="b8d42-111">It continuously runs in hello background and collects all Event Tracing for Windows (ETW) logs from component services on Azure Stack and stores them on a common local share.</span></span> 

<span data-ttu-id="b8d42-112">son las siguientes de Hello tooknow aspectos importantes sobre Hola recopilador de seguimiento:</span><span class="sxs-lookup"><span data-stu-id="b8d42-112">hello following are important things tooknow about hello Trace Collector:</span></span>
 
* <span data-ttu-id="b8d42-113">Hola recopilador de seguimiento se ejecuta sin interrupción con límites de tamaño de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b8d42-113">hello Trace Collector runs continuously with default size limits.</span></span> <span data-ttu-id="b8d42-114">Hola tamaño máximo predeterminado permitido para cada archivo (200 MB) es **no** un tamaño límite.</span><span class="sxs-lookup"><span data-stu-id="b8d42-114">hello default maximum size allowed for each file (200 MB) is **not** a cutoff size.</span></span> <span data-ttu-id="b8d42-115">Se produce una comprobación de tamaño periódicamente (actualmente cada 10 minutos) y si el archivo actual de hello es > = 200 MB, se guarda y se genera un nuevo archivo.</span><span class="sxs-lookup"><span data-stu-id="b8d42-115">A size check occurs periodically (currently every 10 minutes) and if hello current file is >= 200 MB, it is saved and a new file is generated.</span></span> <span data-ttu-id="b8d42-116">También hay un límite (configurable) de 8 GB en tamaño total del archivo de hello generado por sesión de eventos.</span><span class="sxs-lookup"><span data-stu-id="b8d42-116">There is also an 8 GB (configurable) limit on hello total file size generated per event session.</span></span> <span data-ttu-id="b8d42-117">Una vez que se alcanza este límite, se eliminan los archivos más antiguos de hello cuando se crean nuevos.</span><span class="sxs-lookup"><span data-stu-id="b8d42-117">Once this limit is reached, hello oldest files are deleted as new ones are created.</span></span>
* <span data-ttu-id="b8d42-118">Hay un límite de edad de 5 días en los registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8d42-118">There is a 5-day age limit on hello logs.</span></span> <span data-ttu-id="b8d42-119">Este límite también es configurable.</span><span class="sxs-lookup"><span data-stu-id="b8d42-119">This limit is also configurable.</span></span> 
* <span data-ttu-id="b8d42-120">Cada componente define las propiedades de configuración de seguimiento de Hola a través de un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="b8d42-120">Each component defines hello trace configuration properties through a JSON file.</span></span> <span data-ttu-id="b8d42-121">Hola JSON archivos se almacenan en `C:\TraceCollector\Configuration`.</span><span class="sxs-lookup"><span data-stu-id="b8d42-121">hello JSON files are stored in `C:\TraceCollector\Configuration`.</span></span> <span data-ttu-id="b8d42-122">Si es necesario, estos archivos se pueden editar los límites de antigüedad y el tamaño de hello toochange de hello recopilan registros.</span><span class="sxs-lookup"><span data-stu-id="b8d42-122">If necessary, these files can be edited toochange hello age and size limits of hello collected logs.</span></span> <span data-ttu-id="b8d42-123">Archivos de toothese de cambios requieren un reinicio de hello *el recopilador de seguimiento de pila de Microsoft Azure* servicio para hello cambia tootake efecto.</span><span class="sxs-lookup"><span data-stu-id="b8d42-123">Changes toothese files require a restart of hello *Microsoft Azure Stack Trace Collector* service for hello changes tootake effect.</span></span>
* <span data-ttu-id="b8d42-124">Hello en el ejemplo siguiente se es un archivo JSON de configuración de seguimiento para las operaciones de FabricRingServices de hello XRP VM:</span><span class="sxs-lookup"><span data-stu-id="b8d42-124">hello following example is a trace configuration JSON file for FabricRingServices Operations from hello XRP VM:</span></span> 

```
{
    "LogFile": 
    {
        "SessionName": "FabricRingServicesOperationsLogSession",
        "FileName": "\\\\SU1FileServer\\SU1_ManagementLibrary_1\\Diagnostics\\FabricRingServices\\Operations\\AzureStack.Common.Infrastructure.Operations.etl",
        "RollTimeStamp": "00:00:00",
        "MaxDaysOfFiles": "5",
        "MaxSizeInMB": "200",
        "TotalSizeInMB": "5120"
    },
    "EventSources":
    [
        {"Name": "Microsoft-AzureStack-Common-Infrastructure-ResourceManager" },
        {"Name": "Microsoft-OperationManager-EventSource" },
        {"Name": "Microsoft-Operation-EventSource" }
    ]
}
```

* <span data-ttu-id="b8d42-125">**MaxDaysOfFiles**</span><span class="sxs-lookup"><span data-stu-id="b8d42-125">**MaxDaysOfFiles**</span></span>

    <span data-ttu-id="b8d42-126">Este parámetro controla la edad de Hola de tookeep de archivos.</span><span class="sxs-lookup"><span data-stu-id="b8d42-126">This parameter controls hello age of files tookeep.</span></span> <span data-ttu-id="b8d42-127">Los archivos más antiguos se eliminan.</span><span class="sxs-lookup"><span data-stu-id="b8d42-127">Older log files are deleted.</span></span>
* <span data-ttu-id="b8d42-128">**MaxSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="b8d42-128">**MaxSizeInMB**</span></span>

    <span data-ttu-id="b8d42-129">Este parámetro controla el umbral de tamaño de Hola para un único archivo.</span><span class="sxs-lookup"><span data-stu-id="b8d42-129">This parameter controls hello size threshold for a single file.</span></span> <span data-ttu-id="b8d42-130">Si se alcanza el tamaño de hello, se crea un nuevo archivo .etl.</span><span class="sxs-lookup"><span data-stu-id="b8d42-130">If hello size is reached, a new .etl file is created.</span></span>
* <span data-ttu-id="b8d42-131">**TotalSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="b8d42-131">**TotalSizeInMB**</span></span>

    <span data-ttu-id="b8d42-132">Este parámetro controla el tamaño total de Hola de hello .etl archivos generados a partir de una sesión de eventos.</span><span class="sxs-lookup"><span data-stu-id="b8d42-132">This parameter controls hello total size of hello .etl files generated from an event session.</span></span> <span data-ttu-id="b8d42-133">Si el tamaño total del archivo de hello es mayor que este valor de parámetro, se eliminan los archivos antiguos.</span><span class="sxs-lookup"><span data-stu-id="b8d42-133">If hello total file size is greater than this parameter value, older files are deleted.</span></span>
  
## <a name="log-collection-tool"></a><span data-ttu-id="b8d42-134">Herramienta de recopilación de registros</span><span class="sxs-lookup"><span data-stu-id="b8d42-134">Log collection tool</span></span>
 
<span data-ttu-id="b8d42-135">comando de PowerShell de Hola `Get-AzureStackLog` puede ser usado toocollect registros de todos los componentes de hello en un entorno de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8d42-135">hello PowerShell command `Get-AzureStackLog` can be used toocollect logs from all hello components  in an Azure Stack environment.</span></span> <span data-ttu-id="b8d42-136">Los guarda en archivos ZIP en una ubicación definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="b8d42-136">It saves them in zip files in a user defined location.</span></span> <span data-ttu-id="b8d42-137">Si nuestro technical ajuste a las necesidades de equipo su toohelp registros solucionar un problema, puede pedirle toorun esta herramienta.</span><span class="sxs-lookup"><span data-stu-id="b8d42-137">If our technical support team needs your logs toohelp troubleshoot an issue, they may ask you toorun this tool.</span></span>

> [!CAUTION]
> <span data-ttu-id="b8d42-138">Estos archivos de registro pueden contener información de identificación personal (PII).</span><span class="sxs-lookup"><span data-stu-id="b8d42-138">These log files may contain personally identifiable information (PII).</span></span> <span data-ttu-id="b8d42-139">Tenga esto en cuenta antes de publicar los archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="b8d42-139">Take this into account before you publicly post any log files.</span></span>
 
<span data-ttu-id="b8d42-140">Actualmente, recopilamos Hola siguientes tipos de registro:</span><span class="sxs-lookup"><span data-stu-id="b8d42-140">We currently collect hello following log types:</span></span>
*   <span data-ttu-id="b8d42-141">**Registros de implementación de Azure Stack**</span><span class="sxs-lookup"><span data-stu-id="b8d42-141">**Azure Stack deployment logs**</span></span>
*   <span data-ttu-id="b8d42-142">**Registros de eventos de Windows**</span><span class="sxs-lookup"><span data-stu-id="b8d42-142">**Windows event logs**</span></span>
*   <span data-ttu-id="b8d42-143">**Registros de Panther**</span><span class="sxs-lookup"><span data-stu-id="b8d42-143">**Panther logs**</span></span>

     <span data-ttu-id="b8d42-144">problemas de creación de VM de tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="b8d42-144">tootroubleshoot VM creation issues.</span></span>
*   <span data-ttu-id="b8d42-145">**Registros de clúster**</span><span class="sxs-lookup"><span data-stu-id="b8d42-145">**Cluster logs**</span></span>
*   <span data-ttu-id="b8d42-146">**Registros de diagnóstico de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="b8d42-146">**Storage diagnostic logs**</span></span>
*   <span data-ttu-id="b8d42-147">**Registros de ETW**</span><span class="sxs-lookup"><span data-stu-id="b8d42-147">**ETW logs**</span></span>

    <span data-ttu-id="b8d42-148">Estos se recopilan por hello recopilador de seguimiento y almacenados en un recurso compartido desde el que se `Get-AzureStackLog` recuperarlas.</span><span class="sxs-lookup"><span data-stu-id="b8d42-148">These are collected by hello Trace Collector and stored in a share from where `Get-AzureStackLog` retrieves them.</span></span>
 
<span data-ttu-id="b8d42-149">tooidentify todos Hola registros que se recopilan de todos los componentes de hello, consulte toohello `<Logs>` etiquetas en el archivo de configuración de cliente hello ubicados en `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span><span class="sxs-lookup"><span data-stu-id="b8d42-149">tooidentify all hello logs that get collected from all hello components, refer toohello `<Logs>` tags in hello customer configuration file located at `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span></span>
 
### <a name="toorun-get-azurestacklog"></a><span data-ttu-id="b8d42-150">Get-AzureStackLog toorun</span><span class="sxs-lookup"><span data-stu-id="b8d42-150">toorun Get-AzureStackLog</span></span>
1.  <span data-ttu-id="b8d42-151">Inicie sesión como AzureStack\AzureStackAdmin en host Hola.</span><span class="sxs-lookup"><span data-stu-id="b8d42-151">Log in as AzureStack\AzureStackAdmin on hello host.</span></span>
2.  <span data-ttu-id="b8d42-152">Abra una ventana de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="b8d42-152">Open a PowerShell window as an administrator.</span></span>
3.  <span data-ttu-id="b8d42-153">Ejecute `Get-AzureStackLog`.</span><span class="sxs-lookup"><span data-stu-id="b8d42-153">Run `Get-AzureStackLog`.</span></span>  

    <span data-ttu-id="b8d42-154">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="b8d42-154">**Examples**</span></span>

    - <span data-ttu-id="b8d42-155">Recopilar todos los registros de todos los roles:</span><span class="sxs-lookup"><span data-stu-id="b8d42-155">Collect all logs for all roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs`

    - <span data-ttu-id="b8d42-156">Recopilar registros de los roles VirtualMachines y BareMetal:</span><span class="sxs-lookup"><span data-stu-id="b8d42-156">Collect logs from VirtualMachines and BareMetal roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal`

    - <span data-ttu-id="b8d42-157">Recopilar registros de roles VirtualMachines y BareMetal, con fecha de filtrado de archivos de registro de hello últimas 8 horas:</span><span class="sxs-lookup"><span data-stu-id="b8d42-157">Collect logs from VirtualMachines and BareMetal roles, with date filtering for log files for hello past 8 hours:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)`

<span data-ttu-id="b8d42-158">Si hello `FromDate` y `ToDate` no se especifican parámetros, los registros se recopilan para hello últimas 4 horas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b8d42-158">If hello `FromDate` and `ToDate` parameters are not specified, logs are collected for hello past 4 hours by default.</span></span>

<span data-ttu-id="b8d42-159">Actualmente no se puede usar hello `FilterByRole` recopilación de registros de parámetro toofilter por hello siguientes roles:</span><span class="sxs-lookup"><span data-stu-id="b8d42-159">Currently, you can use hello `FilterByRole` parameter toofilter log collection by hello following roles:</span></span>

|   |   |   |
| - | - | - |
| `ACSMigrationService`     | `ACSMonitoringService`   | `ACSSettingsService` |
| `ACS`                     | `ACSFabric`              | `ACSFrontEnd`        |
| `ACSTableMaster`          | `ACSTableServer`         | `ACSWac`             |
| `ADFS`                    | `ASAppGateway`           | `BareMetal`          |
| `BRP`                     | `CA`                     | `CPI`                |
| `CRP`                     | `DeploymentMachine`      | `DHCP`               |
|`Domain`                   | `ECE`                    | `ECESeedRing`        |        
| `FabricRing`              | `FabricRingServices`     | `FRP`                |
|` Gateway`                 | `HealthMonitoring`       | `HRP`                |               
| `IBC`                     | `InfraServiceController` | `KeyVaultAdminResourceProvider`|
| `KeyVaultControlPlane`    | `KeyVaultDataPlane`      | `NC`                 |            
| `NonPrivilegedAppGateway` | `NRP`                    | `SeedRing`           |
| `SeedRingServices`        | `SLB`                    | `SQL`                |     
| `SRP`                     | `Storage`                | `StorageController`  |
| `URP`                     | `UsageBridge`            | `VirtualMachines`    |  
| `WAS`                     | `WASPUBLIC`              | `WDS`                |


<span data-ttu-id="b8d42-160">Toonote algunas cosas:</span><span class="sxs-lookup"><span data-stu-id="b8d42-160">A few things toonote:</span></span>

* <span data-ttu-id="b8d42-161">Este comando tardará un rato en recopilar los registros en función de los registros del rol que se recopilen.</span><span class="sxs-lookup"><span data-stu-id="b8d42-161">This command takes some time for log collection based on which role logs are collected.</span></span> <span data-ttu-id="b8d42-162">Factores incluyen hello duración especificada para la recopilación de registros y números de Hola de nodos en el entorno de Azure pila Hola.</span><span class="sxs-lookup"><span data-stu-id="b8d42-162">Contributing factors include hello time duration specified for log collection, and hello numbers of nodes in hello Azure Stack environment.</span></span>
* <span data-ttu-id="b8d42-163">Una vez finalizada la recopilación de registros, compruebe la carpeta nueva hello en hello `-OutputPath` los parámetros especificados en el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8d42-163">After log collection completes, check hello new folder created in hello `-OutputPath` parameter specified in hello command.</span></span>
* <span data-ttu-id="b8d42-164">Un archivo denominado `Get-AzureStackLog_Output.log` se crea en la carpeta de Hola que contiene los archivos zip Hola e incluye la salida del comando hello, que se puede usar para solucionar problemas de errores en la colección de registros.</span><span class="sxs-lookup"><span data-stu-id="b8d42-164">A file called `Get-AzureStackLog_Output.log` is created in hello folder containing hello zip files and includes hello command output, which can be used for troubleshooting any failures in log collection.</span></span>
* <span data-ttu-id="b8d42-165">Cada rol tiene sus registros dentro de un archivo ZIP individual.</span><span class="sxs-lookup"><span data-stu-id="b8d42-165">Each role has its logs inside an individual zip file.</span></span> 
* <span data-ttu-id="b8d42-166">tooinvestigate un error específico, pueden resultar necesario registros de más de un componente.</span><span class="sxs-lookup"><span data-stu-id="b8d42-166">tooinvestigate a specific failure, logs may be needed from more than one component.</span></span>
    -   <span data-ttu-id="b8d42-167">Sistema y registros de eventos para todas las máquinas virtuales de infraestructura se recopilan en hello *VirtualMachines* rol.</span><span class="sxs-lookup"><span data-stu-id="b8d42-167">System and Event logs for all infrastructure VMs are collected in hello *VirtualMachines* role.</span></span>
    -   <span data-ttu-id="b8d42-168">Sistema y registros de eventos para todos los hosts se recopilan en hello *BareMetal* rol.</span><span class="sxs-lookup"><span data-stu-id="b8d42-168">System and Event logs for all hosts are collected in hello *BareMetal* role.</span></span>
    -   <span data-ttu-id="b8d42-169">Registros de eventos de clúster de conmutación por error y Hyper-V se recopilan en hello *almacenamiento* rol.</span><span class="sxs-lookup"><span data-stu-id="b8d42-169">Failover Cluster and Hyper-V event logs are collected in hello *Storage* role.</span></span>
    -   <span data-ttu-id="b8d42-170">Registros de ACS se recopilan en hello *almacenamiento* y *ACS* roles.</span><span class="sxs-lookup"><span data-stu-id="b8d42-170">ACS logs are collected in hello *Storage* and *ACS* roles.</span></span>
* <span data-ttu-id="b8d42-171">Para obtener más detalles, puede hacer referencia a toohello archivo de configuración de cliente.</span><span class="sxs-lookup"><span data-stu-id="b8d42-171">For more details, you can refer toohello customer configuration file.</span></span> <span data-ttu-id="b8d42-172">Investigar hello `<Logs>` etiquetas para distintas funciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8d42-172">Investigate hello `<Logs>` tags for hello different roles.</span></span>

> [!NOTE]
> <span data-ttu-id="b8d42-173">Le estamos aplique tamaño y edad limita los registros de toohello tal y como resulta esencial tooensure un uso eficaz de los toomake de espacio de almacenamiento seguro no obtener congestiona con registros se recopilan.</span><span class="sxs-lookup"><span data-stu-id="b8d42-173">We are enforcing size and age limits toohello logs collected as it is essential tooensure efficient utilization of your storage space toomake sure it doesn't get flooded with logs.</span></span> <span data-ttu-id="b8d42-174">Dicho esto, cuando se diagnostica un problema a menudo necesitará registros que no exista ya debido a límites de toothese que se apliquen.</span><span class="sxs-lookup"><span data-stu-id="b8d42-174">Having said that, when diagnosing a problem you will often need logs that might not exist anymore due toothese limits being enforced.</span></span> <span data-ttu-id="b8d42-175">Por lo tanto, es **recomienda** la descarga de su espacio de almacenamiento externo de tooan registros (una cuenta de almacenamiento de Azure público, un dispositivo de almacenamiento local adicional etc.) cada 8 horas too12 y mantenerlos existe para 1-3 meses en función de los requisitos.</span><span class="sxs-lookup"><span data-stu-id="b8d42-175">Hence, it is **highly recommended** that you offload your logs tooan external storage space (a storage account in public Azure, an additional on-prem storage device etc.) every 8 too12 hours and keep them there for 1 - 3 months depending on your requirements.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b8d42-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8d42-176">Next steps</span></span>
[<span data-ttu-id="b8d42-177">Solución de problemas de Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b8d42-177">Microsoft Azure Stack troubleshooting</span></span>](azure-stack-troubleshooting.md)
