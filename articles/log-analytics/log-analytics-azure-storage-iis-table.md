---
title: "almacenamiento de blobs de aaaUse para IIS y la tabla de almacenamiento para los eventos de análisis de registros de Azure | Documentos de Microsoft"
description: "Análisis de registros pueden leer registros de Hola para servicios de Azure que escriben tootable almacenamiento de diagnóstico o registros de IIS que se escriban tooblob almacenamiento."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="5b800-103">Uso de Azure Blob Storage para el almacenamiento de tablas de Azure e IIS de eventos con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5b800-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="5b800-104">Análisis de registros pueden leer los registros de Hola para hello después servicios que escriben diagnósticos tootable tooblob escrito almacenamiento de registros de almacenamiento o IIS:</span><span class="sxs-lookup"><span data-stu-id="5b800-104">Log Analytics can read hello logs for hello following services that write diagnostics tootable storage or IIS logs written tooblob storage:</span></span>

* <span data-ttu-id="5b800-105">Clústeres de Service Fabric (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="5b800-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="5b800-106">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="5b800-106">Virtual Machines</span></span>
* <span data-ttu-id="5b800-107">Roles web y de trabajo</span><span class="sxs-lookup"><span data-stu-id="5b800-107">Web/Worker Roles</span></span>

<span data-ttu-id="5b800-108">Antes de que Log Analytics pueda recopilar los datos de estos recursos, es necesario habilitar Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b800-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="5b800-109">Una vez que se habilitan los diagnósticos, puede usar Hola portal de Azure o PowerShell configurar registros de análisis de registros toocollect Hola.</span><span class="sxs-lookup"><span data-stu-id="5b800-109">Once diagnostics are enabled, you can use hello Azure portal or PowerShell configure Log Analytics toocollect hello logs.</span></span>

<span data-ttu-id="5b800-110">Diagnósticos de Azure es una extensión de Azure que permite toocollect de datos de diagnóstico de un rol de trabajo, el rol web o la máquina virtual se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="5b800-110">Azure Diagnostics is an Azure extension that enables you toocollect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="5b800-111">datos de Hola se almacenan en una cuenta de almacenamiento de Azure y, a continuación, se pueden recopilar mediante el análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="5b800-111">hello data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="5b800-112">Para el análisis de registros toocollect estos registros de diagnósticos de Azure, registros de hello deben estar en hello ubicaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b800-112">For Log Analytics toocollect these Azure Diagnostics logs, hello logs must be in hello following locations:</span></span>

| <span data-ttu-id="5b800-113">Tipo de registro</span><span class="sxs-lookup"><span data-stu-id="5b800-113">Log Type</span></span> | <span data-ttu-id="5b800-114">Tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="5b800-114">Resource Type</span></span> | <span data-ttu-id="5b800-115">La ubicación</span><span class="sxs-lookup"><span data-stu-id="5b800-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b800-116">Registros IIS</span><span class="sxs-lookup"><span data-stu-id="5b800-116">IIS logs</span></span> |<span data-ttu-id="5b800-117">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="5b800-117">Virtual Machines</span></span> <br> <span data-ttu-id="5b800-118">Roles web</span><span class="sxs-lookup"><span data-stu-id="5b800-118">Web roles</span></span> <br> <span data-ttu-id="5b800-119">Roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="5b800-119">Worker roles</span></span> |<span data-ttu-id="5b800-120">wad-iis-logfiles (Blob Storage)</span><span class="sxs-lookup"><span data-stu-id="5b800-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="5b800-121">syslog</span><span class="sxs-lookup"><span data-stu-id="5b800-121">Syslog</span></span> |<span data-ttu-id="5b800-122">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="5b800-122">Virtual Machines</span></span> |<span data-ttu-id="5b800-123">LinuxsyslogVer2v0 (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="5b800-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="5b800-124">Eventos operativos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b800-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="5b800-125">Nodos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b800-125">Service Fabric nodes</span></span> |<span data-ttu-id="5b800-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="5b800-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="5b800-127">Service Fabric Reliable Actor Events</span><span class="sxs-lookup"><span data-stu-id="5b800-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="5b800-128">Nodos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b800-128">Service Fabric nodes</span></span> |<span data-ttu-id="5b800-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="5b800-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="5b800-130">Service Fabric Reliable Service Events</span><span class="sxs-lookup"><span data-stu-id="5b800-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="5b800-131">Nodos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b800-131">Service Fabric nodes</span></span> |<span data-ttu-id="5b800-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="5b800-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="5b800-133">Registros de eventos de Windows</span><span class="sxs-lookup"><span data-stu-id="5b800-133">Windows Event logs</span></span> |<span data-ttu-id="5b800-134">Nodos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b800-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="5b800-135">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="5b800-135">Virtual Machines</span></span> <br> <span data-ttu-id="5b800-136">Roles web</span><span class="sxs-lookup"><span data-stu-id="5b800-136">Web roles</span></span> <br> <span data-ttu-id="5b800-137">Roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="5b800-137">Worker roles</span></span> |<span data-ttu-id="5b800-138">WADWindowsEventLogsTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="5b800-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="5b800-139">Registros de ETW de Windows</span><span class="sxs-lookup"><span data-stu-id="5b800-139">Windows ETW logs</span></span> |<span data-ttu-id="5b800-140">Nodos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b800-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="5b800-141">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="5b800-141">Virtual Machines</span></span> <br> <span data-ttu-id="5b800-142">Roles web</span><span class="sxs-lookup"><span data-stu-id="5b800-142">Web roles</span></span> <br> <span data-ttu-id="5b800-143">Roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="5b800-143">Worker roles</span></span> |<span data-ttu-id="5b800-144">WADETWEventTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="5b800-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="5b800-145">Los registros de IIS de Sitios web Azure no son compatibles actualmente.</span><span class="sxs-lookup"><span data-stu-id="5b800-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="5b800-146">Para máquinas virtuales, tiene la opción de hello de la instalación de hello [agente de análisis de registros](log-analytics-azure-vm-extension.md) en la visión adicional de tooenable de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5b800-146">For virtual machines, you have hello option of installing hello [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine tooenable additional insights.</span></span> <span data-ttu-id="5b800-147">Además toobeing tooanalyze capaz de los registros de IIS y registros de eventos, puede realizar análisis adicionales como seguimiento de cambios de configuración, evaluación de SQL y evaluación de actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="5b800-147">In addition toobeing able tooanalyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="5b800-148">Habilitación de Diagnósticos de Azure en una máquina virtual para la recopilación de registros de IIS y de eventos</span><span class="sxs-lookup"><span data-stu-id="5b800-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="5b800-149">Hola de uso siguiendo el procedimiento tooenable diagnósticos de Azure en una máquina virtual para la colección mediante el portal de Microsoft Azure Hola de registros de IIS y el registro de eventos.</span><span class="sxs-lookup"><span data-stu-id="5b800-149">Use hello following procedure tooenable Azure diagnostics in a virtual machine for Event Log and IIS log collection using hello Microsoft Azure portal.</span></span>

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="5b800-150">tooenable diagnósticos de Azure en una máquina virtual con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5b800-150">tooenable Azure diagnostics in a virtual machine with hello Azure portal</span></span>
1. <span data-ttu-id="5b800-151">Instalar agente de máquina virtual de hello cuando se crea una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5b800-151">Install hello VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="5b800-152">Si ya existe una máquina virtual de hello, compruebe que Hola que ya está instalado el agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5b800-152">If hello virtual machine already exists, verify that hello VM Agent is already installed.</span></span>

   * <span data-ttu-id="5b800-153">En Hola portal de Azure, navegue toohello virtual machine, seleccione **configuración opcional**, a continuación, **diagnósticos** y establecer **estado** demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="5b800-153">In hello Azure portal, navigate toohello virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** too**On**.</span></span>

     <span data-ttu-id="5b800-154">Al finalizar, Hola VM tiene la extensión de diagnósticos de Azure de hello instalada y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="5b800-154">Upon completion, hello VM has hello Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="5b800-155">Esta extensión se encarga de recopilar datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5b800-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="5b800-156">Habilite la supervisión y configure el registro de eventos en una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="5b800-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="5b800-157">Puede habilitar el diagnóstico en hello nivel de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5b800-157">You can enable diagnostics at hello VM level.</span></span> <span data-ttu-id="5b800-158">tooenable diagnósticos y, a continuación, configurar el registro de eventos, realice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5b800-158">tooenable diagnostics and then configure event logging, perform hello following steps:</span></span>

   1. <span data-ttu-id="5b800-159">Seleccione Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5b800-159">Select hello VM.</span></span>
   2. <span data-ttu-id="5b800-160">Haga clic en **Supervisión**.</span><span class="sxs-lookup"><span data-stu-id="5b800-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="5b800-161">Haga clic en **Diagnósticos**.</span><span class="sxs-lookup"><span data-stu-id="5b800-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="5b800-162">Conjunto hello **estado** demasiado**ON**.</span><span class="sxs-lookup"><span data-stu-id="5b800-162">Set hello **Status** too**ON**.</span></span>
   5. <span data-ttu-id="5b800-163">Seleccione cada registro de diagnósticos que desea toocollect.</span><span class="sxs-lookup"><span data-stu-id="5b800-163">Select each diagnostics log that you want toocollect.</span></span>
   6. <span data-ttu-id="5b800-164">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5b800-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="5b800-165">Activación de Diagnósticos de Azure en un rol web para la recopilación de eventos y registros de IIS</span><span class="sxs-lookup"><span data-stu-id="5b800-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="5b800-166">Consulte demasiado[cómo tooEnable diagnósticos en un servicio de nube](../cloud-services/cloud-services-dotnet-diagnostics.md) para conocer los pasos generales acerca de cómo habilitar diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b800-166">Refer too[How tooEnable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="5b800-167">Estas instrucciones Hola utilizan esta información y personalizarla para su uso con análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="5b800-167">hello instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="5b800-168">Con el diagnóstico de Azure habilitado:</span><span class="sxs-lookup"><span data-stu-id="5b800-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="5b800-169">Registros de IIS se almacenan de forma predeterminada, con los datos transferidos en el intervalo de transferencia de scheduledTransferPeriod Hola.</span><span class="sxs-lookup"><span data-stu-id="5b800-169">IIS logs are stored by default, with log data transferred at hello scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="5b800-170">Los registros de eventos de Windows no se transfieren de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5b800-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="tooenable-diagnostics"></a><span data-ttu-id="5b800-171">diagnóstico de tooenable</span><span class="sxs-lookup"><span data-stu-id="5b800-171">tooenable diagnostics</span></span>
<span data-ttu-id="5b800-172">tooenable registros de eventos de Windows o toochange Hola scheduledTransferPeriod, configure diagnósticos de Azure mediante el archivo de configuración de hello XML (diagnostics.wadcfg), como se muestra en [paso 4: crear el archivo de configuración de diagnóstico e instalar Hola extensión](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="5b800-172">tooenable Windows Event Logs, or toochange hello scheduledTransferPeriod, configure Azure Diagnostics using hello XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="5b800-173">Hello siguiente archivo de configuración de ejemplo recopila registros de IIS y todos los eventos de aplicación hello y registros del sistema:</span><span class="sxs-lookup"><span data-stu-id="5b800-173">hello following example configuration file collects IIS Logs and all Events from hello Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

<span data-ttu-id="5b800-174">Asegúrese de que ConfigurationSettings especifica una cuenta de almacenamiento, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="5b800-174">Ensure that your ConfigurationSettings specifies a storage account, as in hello following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="5b800-175">Hola **AccountName** y **AccountKey** valores se encuentran en hello portal de Azure en el panel de cuenta de almacenamiento de hello, bajo administrar claves de acceso.</span><span class="sxs-lookup"><span data-stu-id="5b800-175">hello **AccountName** and **AccountKey** values are found in hello Azure portal in hello storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="5b800-176">Protocolo de Hola de cadena de conexión de hello debe ser **https**.</span><span class="sxs-lookup"><span data-stu-id="5b800-176">hello protocol for hello connection string must be **https**.</span></span>

<span data-ttu-id="5b800-177">Una vez que se aplica la configuración de diagnóstico actualizada hello tooyour servicio en la nube y se está escribiendo tooAzure almacenamiento de información de diagnóstico, tú eres listo tooconfigure análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="5b800-177">Once hello updated diagnostic configuration is applied tooyour cloud service and it is writing diagnostics tooAzure Storage, then you are ready tooconfigure Log Analytics.</span></span>

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a><span data-ttu-id="5b800-178">Usar registros de Azure toocollect portal Hola desde el almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="5b800-178">Use hello Azure portal toocollect logs from Azure Storage</span></span>
<span data-ttu-id="5b800-179">Puede usar los registros de Hola de toocollect de hello tooconfigure portal Azure análisis de registros para hello después de los servicios de Azure:</span><span class="sxs-lookup"><span data-stu-id="5b800-179">You can use hello Azure portal tooconfigure Log Analytics toocollect hello logs for hello following Azure services:</span></span>

* <span data-ttu-id="5b800-180">Clústeres de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b800-180">Service Fabric clusters</span></span>
* <span data-ttu-id="5b800-181">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="5b800-181">Virtual Machines</span></span>
* <span data-ttu-id="5b800-182">Roles web y de trabajo</span><span class="sxs-lookup"><span data-stu-id="5b800-182">Web/Worker Roles</span></span>

<span data-ttu-id="5b800-183">Hola portal de Azure, navegar por el área de trabajo de análisis de registros tooyour y realizar Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="5b800-183">In hello Azure portal, navigate tooyour Log Analytics workspace and perform hello following tasks:</span></span>

1. <span data-ttu-id="5b800-184">Haga clic en *Storage accounts logs* (Registros de las cuentas de almacenamiento)</span><span class="sxs-lookup"><span data-stu-id="5b800-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="5b800-185">Haga clic en hello *agregar* tarea</span><span class="sxs-lookup"><span data-stu-id="5b800-185">Click hello *Add* task</span></span>
3. <span data-ttu-id="5b800-186">Seleccionar cuenta de almacenamiento de Hola que contiene registros de diagnósticos de Hola</span><span class="sxs-lookup"><span data-stu-id="5b800-186">Select hello Storage account that contains hello diagnostics logs</span></span>
   * <span data-ttu-id="5b800-187">Esta cuenta puede ser una cuenta de almacenamiento clásico o una cuenta de almacenamiento de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5b800-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="5b800-188">Seleccione Hola desea toocollect registros para el tipo de datos</span><span class="sxs-lookup"><span data-stu-id="5b800-188">Select hello Data Type you want toocollect logs for</span></span>
   * <span data-ttu-id="5b800-189">Opciones de Hello son registros de IIS; Eventos; Syslog (Linux); Registros ETW; Eventos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b800-189">hello choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="5b800-190">valor de Hello para el origen se rellena automáticamente en función de hello, tipo de datos y no se puede cambiar</span><span class="sxs-lookup"><span data-stu-id="5b800-190">hello value for Source is automatically populated based on hello data type and cannot be changed</span></span>
6. <span data-ttu-id="5b800-191">Haga clic en Aceptar toosave Hola configuración</span><span class="sxs-lookup"><span data-stu-id="5b800-191">Click OK toosave hello configuration</span></span>

<span data-ttu-id="5b800-192">Repita los pasos 2 a 6 para los tipos de cuentas y los datos de almacenamiento adicional que desee toocollect de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="5b800-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics toocollect.</span></span>

<span data-ttu-id="5b800-193">En aproximadamente 30 minutos, es capaz de toosee datos de cuenta de almacenamiento de hello en análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="5b800-193">In approximately 30 minutes, you are able toosee data from hello storage account in Log Analytics.</span></span> <span data-ttu-id="5b800-194">Sólo verá los datos que se escriben toostorage después de aplica la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b800-194">You will only see data that is written toostorage after hello configuration is applied.</span></span> <span data-ttu-id="5b800-195">Análisis de registros no leen datos preexistentes Hola de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b800-195">Log Analytics does not read hello pre-existing data from hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="5b800-196">portal de Hello no valida que Hola origen existe en la cuenta de almacenamiento de Hola o si se está escribiendo datos nuevos.</span><span class="sxs-lookup"><span data-stu-id="5b800-196">hello portal does not validate that hello Source exists in hello storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="5b800-197">Habilitación de Diagnósticos de Azure en una máquina virtual para la recopilación de registros de IIS y de eventos con PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b800-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="5b800-198">Hola de uso de los pasos de [tooindex de análisis de registros de configuración de diagnósticos de Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread diagnósticos de Azure que se escriben tootable almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5b800-198">Use hello steps in [Configuring Log Analytics tooindex Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread from Azure diagnostics that are written tootable storage.</span></span>

<span data-ttu-id="5b800-199">Con Azure PowerShell puede especificar con mayor precisión los eventos de Hola que se escriben tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5b800-199">Using Azure PowerShell you can more precisely specify hello events that are written tooAzure Storage.</span></span>
<span data-ttu-id="5b800-200">Para obtener más información, vea[Habilitación de Diagnósticos en Azure](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5b800-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="5b800-201">Puede habilitar y actualizar los diagnósticos de Azure mediante el siguiente script de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b800-201">You can enable and update Azure diagnostics using hello following PowerShell script.</span></span>
<span data-ttu-id="5b800-202">También puede utilizar este script con una configuración de registro personalizada.</span><span class="sxs-lookup"><span data-stu-id="5b800-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="5b800-203">Modificar la cuenta de almacenamiento de hello script tooset Hola, nombre del servicio y nombre de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5b800-203">Modify hello script tooset hello storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="5b800-204">script de Hola usa cmdlets para máquinas virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="5b800-204">hello script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="5b800-205">Revisar Hola siguiendo el ejemplo de script, cópielo, modifíquelo según sea necesario, guarde el ejemplo de Hola como un archivo de script de PowerShell y, a continuación, ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b800-205">Review hello following script sample, copy it, modify it as needed, save hello sample as a PowerShell script file, and then run hello script.</span></span>

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="5b800-206">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b800-206">Next steps</span></span>
* <span data-ttu-id="5b800-207">[Recopilación de registros y métricas de los servicios de Azure](log-analytics-azure-storage.md) para los servicios compatibles de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b800-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="5b800-208">[Habilitar soluciones](log-analytics-add-solutions.md) visión tooprovide datos Hola.</span><span class="sxs-lookup"><span data-stu-id="5b800-208">[Enable Solutions](log-analytics-add-solutions.md) tooprovide insight into hello data.</span></span>
* <span data-ttu-id="5b800-209">[Usar consultas de búsqueda](log-analytics-log-searches.md) tooanalyze datos de saludo.</span><span class="sxs-lookup"><span data-stu-id="5b800-209">[Use search queries](log-analytics-log-searches.md) tooanalyze hello data.</span></span>
