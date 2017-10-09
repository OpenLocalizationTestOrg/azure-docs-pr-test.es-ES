---
title: "aaaStore y ver datos de diagnóstico en almacenamiento de Azure | Documentos de Microsoft"
description: "Obtención de datos de diagnóstico de Azure en Almacenamiento de Azure y su visualización"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="96f75-103">Almacenamiento y visualización de los datos de diagnóstico en Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="96f75-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="96f75-104">Datos de diagnóstico no se almacenan de forma permanente a menos que transfiera emulador de almacenamiento de Microsoft Azure toohello o tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="96f75-104">Diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="96f75-105">Una vez que se encuentren almacenados, los datos se pueden ver con una de las diversas herramientas disponibles.</span><span class="sxs-lookup"><span data-stu-id="96f75-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="96f75-106">Especificación de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="96f75-106">Specify a storage account</span></span>
<span data-ttu-id="96f75-107">Especificar cuenta de almacenamiento de Hola que desea que toouse en el archivo ServiceConfiguration.cscfg de Hola.</span><span class="sxs-lookup"><span data-stu-id="96f75-107">You specify hello storage account that you want toouse in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="96f75-108">información de la cuenta de Hello se define como una cadena de conexión en un valor de configuración.</span><span class="sxs-lookup"><span data-stu-id="96f75-108">hello account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="96f75-109">Hello en el ejemplo siguiente se muestra hello cadena de conexión predeterminado creado para un nuevo proyecto de servicio de nube en Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="96f75-109">hello following example shows hello default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="96f75-110">Puede cambiar esta información de cuenta de tooprovide de cadena de conexión para una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="96f75-110">You can change this connection string tooprovide account information for an Azure storage account.</span></span>

<span data-ttu-id="96f75-111">Según el tipo de saludo de datos de diagnóstico que se están recopilando, diagnósticos de Azure usa servicio de Blob de Hola o servicio de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="96f75-111">Depending on hello type of diagnostic data that is being collected, Azure Diagnostics uses either hello Blob service or hello Table service.</span></span> <span data-ttu-id="96f75-112">Hello tabla siguiente muestran los orígenes de datos de Hola que se conservan y su formato.</span><span class="sxs-lookup"><span data-stu-id="96f75-112">hello following table shows hello data sources that are persisted and their format.</span></span>

| <span data-ttu-id="96f75-113">Origen de datos</span><span class="sxs-lookup"><span data-stu-id="96f75-113">Data source</span></span> | <span data-ttu-id="96f75-114">Formato de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="96f75-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="96f75-115">Registros de Azure</span><span class="sxs-lookup"><span data-stu-id="96f75-115">Azure logs</span></span> |<span data-ttu-id="96f75-116">Tabla</span><span class="sxs-lookup"><span data-stu-id="96f75-116">Table</span></span> |
| <span data-ttu-id="96f75-117">Registros de IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="96f75-117">IIS 7.0 logs</span></span> |<span data-ttu-id="96f75-118">Blob</span><span class="sxs-lookup"><span data-stu-id="96f75-118">Blob</span></span> |
| <span data-ttu-id="96f75-119">Registros de infraestructura de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="96f75-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="96f75-120">Tabla</span><span class="sxs-lookup"><span data-stu-id="96f75-120">Table</span></span> |
| <span data-ttu-id="96f75-121">Registros de seguimiento de solicitudes con error</span><span class="sxs-lookup"><span data-stu-id="96f75-121">Failed Request Trace logs</span></span> |<span data-ttu-id="96f75-122">Blob</span><span class="sxs-lookup"><span data-stu-id="96f75-122">Blob</span></span> |
| <span data-ttu-id="96f75-123">Registros de eventos de Windows</span><span class="sxs-lookup"><span data-stu-id="96f75-123">Windows Event logs</span></span> |<span data-ttu-id="96f75-124">Tabla</span><span class="sxs-lookup"><span data-stu-id="96f75-124">Table</span></span> |
| <span data-ttu-id="96f75-125">Contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="96f75-125">Performance counters</span></span> |<span data-ttu-id="96f75-126">Tabla</span><span class="sxs-lookup"><span data-stu-id="96f75-126">Table</span></span> |
| <span data-ttu-id="96f75-127">Volcados de memoria</span><span class="sxs-lookup"><span data-stu-id="96f75-127">Crash dumps</span></span> |<span data-ttu-id="96f75-128">Blob</span><span class="sxs-lookup"><span data-stu-id="96f75-128">Blob</span></span> |
| <span data-ttu-id="96f75-129">Registros de errores personalizados</span><span class="sxs-lookup"><span data-stu-id="96f75-129">Custom error logs</span></span> |<span data-ttu-id="96f75-130">Blob</span><span class="sxs-lookup"><span data-stu-id="96f75-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="96f75-131">Transferencia de datos de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="96f75-131">Transfer diagnostic data</span></span>
<span data-ttu-id="96f75-132">SDK 2.5 y versiones posteriores, datos de diagnóstico de hello solicitud tootransfer pueden producirse a través de archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="96f75-132">For SDK 2.5 and later, hello request tootransfer diagnostic data can occur through hello configuration file.</span></span> <span data-ttu-id="96f75-133">Puede transferir datos de diagnóstico a intervalos programados, como se especifica en configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="96f75-133">You can transfer diagnostic data at scheduled intervals as specified in hello configuration.</span></span>

<span data-ttu-id="96f75-134">Para SDK 2.4 y anteriores pueden solicitar datos de diagnóstico de hello tootransfer a través del archivo de configuración de hello como mediante programación.</span><span class="sxs-lookup"><span data-stu-id="96f75-134">For SDK 2.4 and previous you can request tootransfer hello diagnostic data through hello configuration file as well as programmatically.</span></span> <span data-ttu-id="96f75-135">enfoque de programación de Hello también permite a transferencias a petición toodo.</span><span class="sxs-lookup"><span data-stu-id="96f75-135">hello programmatic approach also allows you toodo on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96f75-136">Cuando la transferencia de datos de diagnóstico tooan cuenta de almacenamiento de Azure, se incurre en costos para los recursos de almacenamiento de Hola que usa los datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="96f75-136">When you transfer diagnostic data tooan Azure storage account, you incur costs for hello storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="96f75-137">Almacenamiento de datos de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="96f75-137">Store diagnostic data</span></span>
<span data-ttu-id="96f75-138">Datos de registro se almacenan en almacenamiento de Blob o tabla con hello después de nombres:</span><span class="sxs-lookup"><span data-stu-id="96f75-138">Log data is stored in either Blob or Table storage with hello following names:</span></span>

<span data-ttu-id="96f75-139">**Tablas**</span><span class="sxs-lookup"><span data-stu-id="96f75-139">**Tables**</span></span>

* <span data-ttu-id="96f75-140">**WadLogsTable** : registros escritos en código mediante el agente de escucha de seguimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="96f75-140">**WadLogsTable** - Logs written in code using hello trace listener.</span></span>
* <span data-ttu-id="96f75-141">**WADDiagnosticInfrastructureLogsTable** : monitor de diagnóstico y cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="96f75-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="96f75-142">**WADDirectoriesTable** – directorios ese monitor de diagnóstico de hello está supervisando.</span><span class="sxs-lookup"><span data-stu-id="96f75-142">**WADDirectoriesTable** – Directories that hello diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="96f75-143">Esto incluye los registros de IIS, los registros de solicitudes con error de IIS y los directorios personalizados.</span><span class="sxs-lookup"><span data-stu-id="96f75-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="96f75-144">ubicación de Hola Hola blob del archivo de registro se especifica en el campo de contenedor de Hola y nombre de hello del blob de hello es en el campo RelativePath de Hola.</span><span class="sxs-lookup"><span data-stu-id="96f75-144">hello location of hello blob log file is specified in hello Container field and hello name of hello blob is in hello RelativePath field.</span></span>  <span data-ttu-id="96f75-145">campo AbsolutePath de Hello indica Hola ubicación y el nombre de archivo hello tal como se encontraban en hello máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="96f75-145">hello AbsolutePath field indicates hello location and name of hello file as it existed on hello Azure virtual machine.</span></span>
* <span data-ttu-id="96f75-146">**WADPerformanceCountersTable** : contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="96f75-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="96f75-147">**WADWindowsEventLogsTable** : registros de eventos de Windows.</span><span class="sxs-lookup"><span data-stu-id="96f75-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="96f75-148">**Blobs**</span><span class="sxs-lookup"><span data-stu-id="96f75-148">**Blobs**</span></span>

* <span data-ttu-id="96f75-149">**wad-control-container** : (solo para SDK 2.4 y anteriores) contiene archivos de configuración XML de Hola que controla Hola diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="96f75-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains hello XML configuration files that controls hello Azure diagnostics .</span></span>
* <span data-ttu-id="96f75-150">**wad-iis-failedreqlogfiles** : contiene información de registros de solicitudes con error de IIS.</span><span class="sxs-lookup"><span data-stu-id="96f75-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="96f75-151">**wad-iis-logfiles** : contiene información acerca de los registros de IIS.</span><span class="sxs-lookup"><span data-stu-id="96f75-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="96f75-152">**"custom"** : contenedor personalizado basado en la configuración de directorios supervisados por el monitor de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="96f75-152">**"custom"** – A custom container based on configuring directories that are monitored by hello diagnostic monitor.</span></span>  <span data-ttu-id="96f75-153">nombre de Hola de este contenedor de blob se especificará en WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="96f75-153">hello name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-tooview-diagnostic-data"></a><span data-ttu-id="96f75-154">Datos de diagnóstico de tooview de herramientas</span><span class="sxs-lookup"><span data-stu-id="96f75-154">Tools tooview diagnostic data</span></span>
<span data-ttu-id="96f75-155">Varias herramientas son datos de Hola de tooview disponibles una vez transferido toostorage.</span><span class="sxs-lookup"><span data-stu-id="96f75-155">Several tools are available tooview hello data after it is transferred toostorage.</span></span> <span data-ttu-id="96f75-156">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="96f75-156">For example:</span></span>

* <span data-ttu-id="96f75-157">Explorador de servidores de Visual Studio: si ha instalado hello Azure Tools para Microsoft Visual Studio, puede usar nodo de almacenamiento de Azure de hello en el Explorador de servidores tooview blob y tabla de datos de solo lectura de las cuentas de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="96f75-157">Server Explorer in Visual Studio - If you have installed hello Azure Tools for Microsoft Visual Studio, you can use hello Azure Storage node in Server Explorer tooview read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="96f75-158">Puede mostrar datos de la cuenta del emulador de almacenamiento local y también desde cuentas de almacenamiento que haya creado para Azure.</span><span class="sxs-lookup"><span data-stu-id="96f75-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="96f75-159">Para obtener más información, consulte [Exploración y administración de recursos de almacenamiento con el Explorador de servidores](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="96f75-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="96f75-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente que permite trabajar tooeasily con los datos de almacenamiento de Azure en Linux, Windows y OSX.</span><span class="sxs-lookup"><span data-stu-id="96f75-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="96f75-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) incluye Azure Diagnostics Manager que permite tooview, descargar y administrar datos de diagnóstico de hello recopilados por aplicaciones de Hola que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="96f75-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you tooview, download and manage hello diagnostics data collected by hello applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96f75-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="96f75-162">Next Steps</span></span>
[<span data-ttu-id="96f75-163">Flujo de Hola de seguimiento en una aplicación de servicios en la nube con diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="96f75-163">Trace hello flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

