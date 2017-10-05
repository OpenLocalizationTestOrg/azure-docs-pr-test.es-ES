---
title: Uso de Blob Storage para IIS y Table Storage para eventos en Azure Log Analytics | Microsoft Docs
description: "Log Analytics puede leer los registros de los servicios de Azure que escriben los diagnósticos en Table Storage o los registros de IIS Blob Storage."
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
ms.openlocfilehash: 459ef90ca1d76bada6565bfefd7b4bd1086197d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="c26da-103">Uso de Azure Blob Storage para el almacenamiento de tablas de Azure e IIS de eventos con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c26da-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="c26da-104">Log Analytics puede leer los registros de los siguientes servicios que escriben los diagnósticos Table Storage o los registros de IIS en Blob Storage:</span><span class="sxs-lookup"><span data-stu-id="c26da-104">Log Analytics can read the logs for the following services that write diagnostics to table storage or IIS logs written to blob storage:</span></span>

* <span data-ttu-id="c26da-105">Clústeres de Service Fabric (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="c26da-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="c26da-106">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c26da-106">Virtual Machines</span></span>
* <span data-ttu-id="c26da-107">Roles web y de trabajo</span><span class="sxs-lookup"><span data-stu-id="c26da-107">Web/Worker Roles</span></span>

<span data-ttu-id="c26da-108">Antes de que Log Analytics pueda recopilar los datos de estos recursos, es necesario habilitar Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c26da-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="c26da-109">Una vez que se habilitan los diagnósticos, puede usar Azure Portal o PowerShell para configurar Log Analytics para recopilar los registros.</span><span class="sxs-lookup"><span data-stu-id="c26da-109">Once diagnostics are enabled, you can use the Azure portal or PowerShell configure Log Analytics to collect the logs.</span></span>

<span data-ttu-id="c26da-110">Diagnósticos de Azure es una extensión de Azure que le permite recopilar datos de diagnóstico de un rol de trabajo, un rol web o una máquina virtual en ejecución en Azure.</span><span class="sxs-lookup"><span data-stu-id="c26da-110">Azure Diagnostics is an Azure extension that enables you to collect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="c26da-111">Los datos se almacenan en una cuenta de Azure Storage para que se puedan recopilar con Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c26da-111">The data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="c26da-112">Para que Log Analytics recopile estos registros de Diagnóstico de Azure, deben estar en las siguientes ubicaciones:</span><span class="sxs-lookup"><span data-stu-id="c26da-112">For Log Analytics to collect these Azure Diagnostics logs, the logs must be in the following locations:</span></span>

| <span data-ttu-id="c26da-113">Tipo de registro</span><span class="sxs-lookup"><span data-stu-id="c26da-113">Log Type</span></span> | <span data-ttu-id="c26da-114">Tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="c26da-114">Resource Type</span></span> | <span data-ttu-id="c26da-115">La ubicación</span><span class="sxs-lookup"><span data-stu-id="c26da-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c26da-116">Registros IIS</span><span class="sxs-lookup"><span data-stu-id="c26da-116">IIS logs</span></span> |<span data-ttu-id="c26da-117">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c26da-117">Virtual Machines</span></span> <br> <span data-ttu-id="c26da-118">Roles web</span><span class="sxs-lookup"><span data-stu-id="c26da-118">Web roles</span></span> <br> <span data-ttu-id="c26da-119">Roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="c26da-119">Worker roles</span></span> |<span data-ttu-id="c26da-120">wad-iis-logfiles (Blob Storage)</span><span class="sxs-lookup"><span data-stu-id="c26da-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="c26da-121">syslog</span><span class="sxs-lookup"><span data-stu-id="c26da-121">Syslog</span></span> |<span data-ttu-id="c26da-122">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c26da-122">Virtual Machines</span></span> |<span data-ttu-id="c26da-123">LinuxsyslogVer2v0 (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="c26da-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="c26da-124">Eventos operativos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c26da-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="c26da-125">Nodos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c26da-125">Service Fabric nodes</span></span> |<span data-ttu-id="c26da-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="c26da-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="c26da-127">Service Fabric Reliable Actor Events</span><span class="sxs-lookup"><span data-stu-id="c26da-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="c26da-128">Nodos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c26da-128">Service Fabric nodes</span></span> |<span data-ttu-id="c26da-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="c26da-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="c26da-130">Service Fabric Reliable Service Events</span><span class="sxs-lookup"><span data-stu-id="c26da-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="c26da-131">Nodos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c26da-131">Service Fabric nodes</span></span> |<span data-ttu-id="c26da-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="c26da-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="c26da-133">Registros de eventos de Windows</span><span class="sxs-lookup"><span data-stu-id="c26da-133">Windows Event logs</span></span> |<span data-ttu-id="c26da-134">Nodos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c26da-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="c26da-135">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c26da-135">Virtual Machines</span></span> <br> <span data-ttu-id="c26da-136">Roles web</span><span class="sxs-lookup"><span data-stu-id="c26da-136">Web roles</span></span> <br> <span data-ttu-id="c26da-137">Roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="c26da-137">Worker roles</span></span> |<span data-ttu-id="c26da-138">WADWindowsEventLogsTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="c26da-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="c26da-139">Registros de ETW de Windows</span><span class="sxs-lookup"><span data-stu-id="c26da-139">Windows ETW logs</span></span> |<span data-ttu-id="c26da-140">Nodos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c26da-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="c26da-141">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c26da-141">Virtual Machines</span></span> <br> <span data-ttu-id="c26da-142">Roles web</span><span class="sxs-lookup"><span data-stu-id="c26da-142">Web roles</span></span> <br> <span data-ttu-id="c26da-143">Roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="c26da-143">Worker roles</span></span> |<span data-ttu-id="c26da-144">WADETWEventTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="c26da-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="c26da-145">Los registros de IIS de Sitios web Azure no son compatibles actualmente.</span><span class="sxs-lookup"><span data-stu-id="c26da-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="c26da-146">Para máquinas virtuales, también tiene la opción de instalar el [agente de Log Analytics](log-analytics-azure-vm-extension.md) en la máquina virtual para permitir información adicional.</span><span class="sxs-lookup"><span data-stu-id="c26da-146">For virtual machines, you have the option of installing the [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine to enable additional insights.</span></span> <span data-ttu-id="c26da-147">Además de poder analizar registros de IIS y registros de eventos, también podrá realizar análisis adicionales, como seguimiento de cambios de configuración, evaluación de SQL y evaluación de actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="c26da-147">In addition to being able to analyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="c26da-148">Habilitación de Diagnósticos de Azure en una máquina virtual para la recopilación de registros de IIS y de eventos</span><span class="sxs-lookup"><span data-stu-id="c26da-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="c26da-149">Use el siguiente procedimiento para habilitar Diagnósticos de Azure en una máquina virtual para la recopilación de registros de IIS y de eventos mediante Microsoft Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c26da-149">Use the following procedure to enable Azure diagnostics in a virtual machine for Event Log and IIS log collection using the Microsoft Azure portal.</span></span>

### <a name="to-enable-azure-diagnostics-in-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="c26da-150">Pasos para habilitar Diagnósticos de Azure en una máquina virtual con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c26da-150">To enable Azure diagnostics in a virtual machine with the Azure portal</span></span>
1. <span data-ttu-id="c26da-151">Instale al agente de máquina virtual cuando cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c26da-151">Install the VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="c26da-152">Si la máquina virtual ya existe, compruebe que el agente de máquina virtual ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="c26da-152">If the virtual machine already exists, verify that the VM Agent is already installed.</span></span>

   * <span data-ttu-id="c26da-153">En Azure Portal, acceda a la máquina virtual, seleccione **Configuración opcional**, luego **Diagnósticos** y establezca **Estado** en **Activado**.</span><span class="sxs-lookup"><span data-stu-id="c26da-153">In the Azure portal, navigate to the virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** to **On**.</span></span>

     <span data-ttu-id="c26da-154">Tras la finalización, la máquina virtual tendrá la extensión de Diagnósticos de Azure instalada y ejecutándose.</span><span class="sxs-lookup"><span data-stu-id="c26da-154">Upon completion, the VM has the Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="c26da-155">Esta extensión se encarga de recopilar datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c26da-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="c26da-156">Habilite la supervisión y configure el registro de eventos en una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="c26da-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="c26da-157">Puede habilitar el diagnóstico en el nivel de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c26da-157">You can enable diagnostics at the VM level.</span></span> <span data-ttu-id="c26da-158">Para activar el diagnóstico y, a continuación, configurar el registro de eventos, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c26da-158">To enable diagnostics and then configure event logging, perform the following steps:</span></span>

   1. <span data-ttu-id="c26da-159">Seleccione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c26da-159">Select the VM.</span></span>
   2. <span data-ttu-id="c26da-160">Haga clic en **Supervisión**.</span><span class="sxs-lookup"><span data-stu-id="c26da-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="c26da-161">Haga clic en **Diagnósticos**.</span><span class="sxs-lookup"><span data-stu-id="c26da-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="c26da-162">Establezca el **Estado** en **Activado**.</span><span class="sxs-lookup"><span data-stu-id="c26da-162">Set the **Status** to **ON**.</span></span>
   5. <span data-ttu-id="c26da-163">Seleccione los registros de diagnóstico que desee recopilar.</span><span class="sxs-lookup"><span data-stu-id="c26da-163">Select each diagnostics log that you want to collect.</span></span>
   6. <span data-ttu-id="c26da-164">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c26da-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="c26da-165">Activación de Diagnósticos de Azure en un rol web para la recopilación de eventos y registros de IIS</span><span class="sxs-lookup"><span data-stu-id="c26da-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="c26da-166">Consulte [Cómo habilitar diagnósticos en un servicio en la nube](../cloud-services/cloud-services-dotnet-diagnostics.md) para conocer los pasos generales para habilitar Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c26da-166">Refer to [How To Enable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="c26da-167">Las instrucciones siguientes utilizan esta información y la personalizan para utilizarse con Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c26da-167">The instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="c26da-168">Con el diagnóstico de Azure habilitado:</span><span class="sxs-lookup"><span data-stu-id="c26da-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="c26da-169">Los registros de IIS se almacenan de forma predeterminada, con los datos transferidos en el intervalo de transferencia de scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="c26da-169">IIS logs are stored by default, with log data transferred at the scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="c26da-170">Los registros de eventos de Windows no se transfieren de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c26da-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="to-enable-diagnostics"></a><span data-ttu-id="c26da-171">Para habilitar diagnósticos</span><span class="sxs-lookup"><span data-stu-id="c26da-171">To enable diagnostics</span></span>
<span data-ttu-id="c26da-172">Para habilitar los registros de eventos de Windows, o para cambiar scheduledTransferPeriod, configure Diagnósticos de Azure con el archivo de configuración XML (diagnostics.wadcfg) como se muestra en el [Paso 4: crear el archivo de configuración de Diagnósticos e instalar la extensión](../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="c26da-172">To enable Windows Event Logs, or to change the scheduledTransferPeriod, configure Azure Diagnostics using the XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install the extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="c26da-173">El siguiente archivo de configuración de ejemplo recopila los registros de IIS y todos los eventos desde los registros de aplicación y sistema:</span><span class="sxs-lookup"><span data-stu-id="c26da-173">The following example configuration file collects IIS Logs and all Events from the Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant to Web roles -->
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

<span data-ttu-id="c26da-174">Asegúrese de que ConfigurationSettings especifica una cuenta de almacenamiento, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c26da-174">Ensure that your ConfigurationSettings specifies a storage account, as in the following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="c26da-175">Los valores de **AccountName** y **AccountKey** se encuentran en el panel de cuentas de almacenamiento de Azure Portal, en Administrar claves de acceso.</span><span class="sxs-lookup"><span data-stu-id="c26da-175">The **AccountName** and **AccountKey** values are found in the Azure portal in the storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="c26da-176">El protocolo de la cadena de conexión debe ser **https**.</span><span class="sxs-lookup"><span data-stu-id="c26da-176">The protocol for the connection string must be **https**.</span></span>

<span data-ttu-id="c26da-177">Una vez que se aplica la configuración de diagnóstico actualizada al servicio en la nube y se escribe el diagnóstico en Azure Storage, está preparado para configurar Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c26da-177">Once the updated diagnostic configuration is applied to your cloud service and it is writing diagnostics to Azure Storage, then you are ready to configure Log Analytics.</span></span>

## <a name="use-the-azure-portal-to-collect-logs-from-azure-storage"></a><span data-ttu-id="c26da-178">Uso de Azure Portal para recopilar registros de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c26da-178">Use the Azure portal to collect logs from Azure Storage</span></span>
<span data-ttu-id="c26da-179">Con Azure Portal puede configurar Log Analytics para recopilar los registros para los siguientes servicios de Azure:</span><span class="sxs-lookup"><span data-stu-id="c26da-179">You can use the Azure portal to configure Log Analytics to collect the logs for the following Azure services:</span></span>

* <span data-ttu-id="c26da-180">Clústeres de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c26da-180">Service Fabric clusters</span></span>
* <span data-ttu-id="c26da-181">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c26da-181">Virtual Machines</span></span>
* <span data-ttu-id="c26da-182">Roles web y de trabajo</span><span class="sxs-lookup"><span data-stu-id="c26da-182">Web/Worker Roles</span></span>

<span data-ttu-id="c26da-183">En Azure Portal, vaya hasta el área de trabajo de Log Analytics y realice las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="c26da-183">In the Azure portal, navigate to your Log Analytics workspace and perform the following tasks:</span></span>

1. <span data-ttu-id="c26da-184">Haga clic en *Storage accounts logs* (Registros de las cuentas de almacenamiento)</span><span class="sxs-lookup"><span data-stu-id="c26da-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="c26da-185">Haga clic en la tarea *Agregar*</span><span class="sxs-lookup"><span data-stu-id="c26da-185">Click the *Add* task</span></span>
3. <span data-ttu-id="c26da-186">Seleccione la cuenta de almacenamiento que contenga los registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="c26da-186">Select the Storage account that contains the diagnostics logs</span></span>
   * <span data-ttu-id="c26da-187">Esta cuenta puede ser una cuenta de almacenamiento clásico o una cuenta de almacenamiento de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c26da-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="c26da-188">Seleccione el tipo de datos de los cuales desea recopilar registros</span><span class="sxs-lookup"><span data-stu-id="c26da-188">Select the Data Type you want to collect logs for</span></span>
   * <span data-ttu-id="c26da-189">Las opciones serán registros de IIS; eventos; Syslog (Linux); registros de ETW; eventos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c26da-189">The choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="c26da-190">El valor de origen se rellenará automáticamente según el tipo de datos y no se puede cambiar</span><span class="sxs-lookup"><span data-stu-id="c26da-190">The value for Source is automatically populated based on the data type and cannot be changed</span></span>
6. <span data-ttu-id="c26da-191">Haga clic en Aceptar para guardar la configuración</span><span class="sxs-lookup"><span data-stu-id="c26da-191">Click OK to save the configuration</span></span>

<span data-ttu-id="c26da-192">Repita los pasos 2 a 6 para los tipos de datos y cuentas de almacenamiento adicionales que quiera que recopile Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c26da-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics to collect.</span></span>

<span data-ttu-id="c26da-193">En aproximadamente 30 minutos podrá ver los datos de la cuenta de almacenamiento en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c26da-193">In approximately 30 minutes, you are able to see data from the storage account in Log Analytics.</span></span> <span data-ttu-id="c26da-194">Solo verá los datos que se escriban en el almacenamiento de una vez aplicada la configuración.</span><span class="sxs-lookup"><span data-stu-id="c26da-194">You will only see data that is written to storage after the configuration is applied.</span></span> <span data-ttu-id="c26da-195">Log Analytics no lee los datos preexistentes de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c26da-195">Log Analytics does not read the pre-existing data from the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="c26da-196">El portal no valida la existencia del origen en la cuenta de almacenamiento o si se escriben nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="c26da-196">The portal does not validate that the Source exists in the storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="c26da-197">Habilitación de Diagnósticos de Azure en una máquina virtual para la recopilación de registros de IIS y de eventos con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c26da-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="c26da-198">Siga los pasos de [Configuración de Log Analytics para indizar Diagnósticos de Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) para usar PowerShell con el fin de leer datos desde los diagnósticos de Azure que se escribe en Table Storage.</span><span class="sxs-lookup"><span data-stu-id="c26da-198">Use the steps in [Configuring Log Analytics to index Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) to use PowerShell to read from Azure diagnostics that are written to table storage.</span></span>

<span data-ttu-id="c26da-199">Con PowerShell de Azure puede especificar con mayor precisión los eventos que se escriben en Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c26da-199">Using Azure PowerShell you can more precisely specify the events that are written to Azure Storage.</span></span>
<span data-ttu-id="c26da-200">Para obtener más información, vea[Habilitación de Diagnósticos en Azure](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="c26da-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="c26da-201">Puede habilitar y actualizar Diagnósticos de Azure mediante el siguiente script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c26da-201">You can enable and update Azure diagnostics using the following PowerShell script.</span></span>
<span data-ttu-id="c26da-202">También puede utilizar este script con una configuración de registro personalizada.</span><span class="sxs-lookup"><span data-stu-id="c26da-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="c26da-203">Modifique el script para establecer la cuenta de almacenamiento, el nombre del servicio y el nombre de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c26da-203">Modify the script to set the storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="c26da-204">El script usa cmdlets para máquinas virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="c26da-204">The script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="c26da-205">Revise el siguiente ejemplo de script, cópielo, modifíquelo según sea necesario, guarde el ejemplo como un archivo de script de PowerShell y, a continuación, ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="c26da-205">Review the following script sample, copy it, modify it as needed, save the sample as a PowerShell script file, and then run the script.</span></span>

```
    #Connect to Azure
    Add-AzureAccount

    # settings to change:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert to config format

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
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of the extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="c26da-206">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c26da-206">Next steps</span></span>
* <span data-ttu-id="c26da-207">[Recopilación de registros y métricas de los servicios de Azure](log-analytics-azure-storage.md) para los servicios compatibles de Azure.</span><span class="sxs-lookup"><span data-stu-id="c26da-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="c26da-208">[Incorporación de soluciones de Log Analytics desde la galería de soluciones](log-analytics-add-solutions.md) para más información sobre los datos.</span><span class="sxs-lookup"><span data-stu-id="c26da-208">[Enable Solutions](log-analytics-add-solutions.md) to provide insight into the data.</span></span>
* <span data-ttu-id="c26da-209">[Búsquedas de registros en Log Analytics](log-analytics-log-searches.md) para analizar los datos.</span><span class="sxs-lookup"><span data-stu-id="c26da-209">[Use search queries](log-analytics-log-searches.md) to analyze the data.</span></span>
