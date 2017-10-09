---
title: "aaaHow toouse diagnósticos de Azure (. NET) con servicios en la nube | Documentos de Microsoft"
description: "Mediante Diagnósticos de Azure toogather datos de Azure servicios en la nube para la depuración, medir el rendimiento, supervisión, análisis del tráfico y mucho más."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="cac90-103">Habilitación de diagnósticos de Azure en servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="cac90-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="cac90-104">Consulte [Introducción a Diagnósticos de Azure](../azure-diagnostics.md) para obtener información sobre Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="cac90-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a><span data-ttu-id="cac90-105">¿Cómo tooEnable diagnósticos en un rol de trabajo</span><span class="sxs-lookup"><span data-stu-id="cac90-105">How tooEnable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="cac90-106">Este tutorial describe cómo tooimplement un rol de trabajador de Azure que emite los datos de telemetría mediante Hola .NET EventSource (clase).</span><span class="sxs-lookup"><span data-stu-id="cac90-106">This walkthrough describes how tooimplement an Azure worker role that emits telemetry data using hello .NET EventSource class.</span></span> <span data-ttu-id="cac90-107">Diagnósticos de Azure son toocollect usa los datos de telemetría hello y almacenan en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="cac90-107">Azure Diagnostics is used toocollect hello telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="cac90-108">Al crear un rol de trabajo, Visual Studio permite automáticamente Diagnostics 1.0 como parte de la solución de hello en Azure SDK para .NET 2.4 y versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="cac90-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of hello solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="cac90-109">Hello las instrucciones siguientes describen Hola proceso para crear el rol de trabajo de hello, deshabilitar Diagnostics 1.0 de solución de Hola y la implementación de diagnóstico 1.2 o rol de trabajo tooyour 1.3.</span><span class="sxs-lookup"><span data-stu-id="cac90-109">hello following instructions describe hello process for creating hello worker role, disabling Diagnostics 1.0 from hello solution, and deploying Diagnostics 1.2 or 1.3 tooyour worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cac90-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cac90-110">Prerequisites</span></span>
<span data-ttu-id="cac90-111">En este artículo se supone que tiene una suscripción de Azure y está utilizando Visual Studio con hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="cac90-111">This article assumes you have an Azure subscription and are using Visual Studio with hello Azure SDK.</span></span> <span data-ttu-id="cac90-112">Si no tiene una suscripción de Azure, puede registrarse para hello [gratuita][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="cac90-112">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="cac90-113">Asegúrese de que demasiado[instalar y configurar Azure PowerShell versión 0.8.7 o posterior][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="cac90-113">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="cac90-114">Paso 1: crear roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="cac90-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="cac90-115">Inicie **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="cac90-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="cac90-116">Crear un **servicio de nube de Azure** proyecto a partir de hello **nube** plantilla cuyo destino es .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="cac90-116">Create an **Azure Cloud Service** project from hello **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="cac90-117">Denomine el proyecto de Hola "WadExample" y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="cac90-117">Name hello project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="cac90-118">Seleccione **Rol de trabajo** y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="cac90-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="cac90-119">se creará el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac90-119">hello project will be created.</span></span>
4. <span data-ttu-id="cac90-120">En **el Explorador de soluciones**, haga doble clic en hello **WorkerRole1** archivo de propiedades.</span><span class="sxs-lookup"><span data-stu-id="cac90-120">In **Solution Explorer**, double-click hello **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="cac90-121">Hola **configuración** ficha desactive **habilitar diagnósticos** toodisable Diagnostics 1.0 (Azure SDK 2.4 y anterior).</span><span class="sxs-lookup"><span data-stu-id="cac90-121">In hello **Configuration** tab, un-check **Enable Diagnostics** toodisable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="cac90-122">Compilar la solución tooverify que no aparece ningún error.</span><span class="sxs-lookup"><span data-stu-id="cac90-122">Build your solution tooverify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="cac90-123">Paso 2: instrumentar el código</span><span class="sxs-lookup"><span data-stu-id="cac90-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="cac90-124">Reemplace el contenido de Hola de WorkerRole.cs con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="cac90-124">Replace hello contents of WorkerRole.cs with hello following code.</span></span> <span data-ttu-id="cac90-125">Hola clase SampleEventSourceWriter, que se hereda de hello [EventSource (clase)][EventSource Class], implementa los cuatro métodos de registro: **SendEnums**, **MessageMethod** , **SetOther** y **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="cac90-125">hello class SampleEventSourceWriter, inherited from hello [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="cac90-126">Hola primera toohello parámetro **WriteEvent** método define el identificador hello para el evento correspondiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac90-126">hello first parameter toohello **WriteEvent** method defines hello ID for hello respective event.</span></span> <span data-ttu-id="cac90-127">Hola método Run implementa un bucle infinito que llama a cada uno de hello registro en los métodos implementados en hello **SampleEventSourceWriter** clase cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="cac90-127">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through hello loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="cac90-128">Paso 3: implementar roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="cac90-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="cac90-129">Implementar el rol de trabajo tooAzure desde dentro de Visual Studio seleccionando hello **WadExample** proyecto Hola, a continuación, el Explorador de soluciones **publicar** de hello **generar** menú.</span><span class="sxs-lookup"><span data-stu-id="cac90-129">Deploy your worker role tooAzure from within Visual Studio by selecting hello **WadExample** project in hello Solution Explorer then **Publish** from hello **Build** menu.</span></span>
2. <span data-ttu-id="cac90-130">Elija su suscripción.</span><span class="sxs-lookup"><span data-stu-id="cac90-130">Choose your subscription.</span></span>
3. <span data-ttu-id="cac90-131">Hola **configuración de publicación de Microsoft Azure** cuadro de diálogo, seleccione **crear nuevo...** .</span><span class="sxs-lookup"><span data-stu-id="cac90-131">In hello **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="cac90-132">Hola **crear servicio en la nube y cuenta de almacenamiento** cuadro de diálogo, escriba un **nombre** (por ejemplo, "WadExample") y seleccione una región o un grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="cac90-132">In hello **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="cac90-133">Conjunto hello **entorno** demasiado**ensayo**.</span><span class="sxs-lookup"><span data-stu-id="cac90-133">Set hello **Environment** too**Staging**.</span></span>
6. <span data-ttu-id="cac90-134">Modifique cualquier otro parámetro de **Configuración** según sea necesario y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="cac90-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="cac90-135">Una vez finalizada la implementación, compruebe en hello portal de Azure que el servicio de nube está en un **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="cac90-135">After deployment has completed, verify in hello Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a><span data-ttu-id="cac90-136">Paso 4: Crear el archivo de configuración de diagnóstico e instalar extensión de Hola</span><span class="sxs-lookup"><span data-stu-id="cac90-136">Step 4: Create your Diagnostics configuration file and install hello extension</span></span>
1. <span data-ttu-id="cac90-137">Descargar definición de esquema de archivo de configuración pública de hello ejecutando el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="cac90-137">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="cac90-138">Agregar una tooyour de archivo XML **WorkerRole1** proyecto con el botón secundario en hello **WorkerRole1** de proyecto y seleccione **agregar** -> **nuevo elemento...**</span><span class="sxs-lookup"><span data-stu-id="cac90-138">Add an XML file tooyour **WorkerRole1** project by right-clicking on hello **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="cac90-139"> -> **Elementos de Visual C#** -> **Datos** -> **Archivo XML**.</span><span class="sxs-lookup"><span data-stu-id="cac90-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="cac90-140">Nombre de archivo hello "WadExample.xml".</span><span class="sxs-lookup"><span data-stu-id="cac90-140">Name hello file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="cac90-142">Asociar el archivo de configuración de Hola Hola WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="cac90-142">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="cac90-143">Asegúrese de que la ventana del editor de hello WadExample.xml es la ventana activa de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac90-143">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="cac90-144">Presione **F4** tooopen hello **propiedades** ventana.</span><span class="sxs-lookup"><span data-stu-id="cac90-144">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="cac90-145">Haga clic en hello **esquemas** propiedad Hola **propiedades** ventana.</span><span class="sxs-lookup"><span data-stu-id="cac90-145">Click hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="cac90-146">Haga clic en hello **...**</span><span class="sxs-lookup"><span data-stu-id="cac90-146">Click hello **…**</span></span> <span data-ttu-id="cac90-147">Hola **esquemas** propiedad.</span><span class="sxs-lookup"><span data-stu-id="cac90-147">in hello **Schemas** property.</span></span> <span data-ttu-id="cac90-148">Haga clic en hello **agregar...**</span><span class="sxs-lookup"><span data-stu-id="cac90-148">Click hello **Add…**</span></span> <span data-ttu-id="cac90-149">botón y navegar por la ubicación de toohello donde guardó archivo XSD de Hola y Hola Seleccione archivo WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="cac90-149">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="cac90-150">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="cac90-150">Click **OK**.</span></span>

4. <span data-ttu-id="cac90-151">Reemplace el contenido de Hola Hola WadExample.xml del archivo de configuración con hello continuación de XML y guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="cac90-151">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="cac90-152">Este archivo de configuración define un par toocollect de contadores de rendimiento: uno para el uso de CPU y otro para el uso de memoria.</span><span class="sxs-lookup"><span data-stu-id="cac90-152">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="cac90-153">A continuación, la configuración de hello define cuatro eventos de hello correspondientes métodos toohello Hola SampleEventSourceWriter clase.</span><span class="sxs-lookup"><span data-stu-id="cac90-153">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="cac90-154">Paso 5: instalar Diagnósticos en roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="cac90-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="cac90-155">Hello cmdlets de PowerShell para administrar los diagnósticos en un rol web o de trabajo son: AzureServiceDiagnosticsExtension Set y Get-AzureServiceDiagnosticsExtension, Remove-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="cac90-155">hello PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="cac90-156">Abra Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cac90-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="cac90-157">Hola script tooinstall diagnóstico se ejecuta en el rol de trabajo (reemplace *StorageAccountKey* con clave de cuenta de almacenamiento de hello para la cuenta de almacenamiento de wadexample y *config_path* con ruta de acceso de Hola toohello *WadExample.xml* archivo):</span><span class="sxs-lookup"><span data-stu-id="cac90-157">Execute hello script tooinstall Diagnostics on your worker role (replace *StorageAccountKey* with hello storage account key for your wadexample storage account and *config_path* with hello path toohello *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="cac90-158">Paso 6: consultar los datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="cac90-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="cac90-159">En Visual Studio hello **Explorador de servidores**, navegar por la cuenta de almacenamiento de toohello wadexample.</span><span class="sxs-lookup"><span data-stu-id="cac90-159">In hello Visual Studio **Server Explorer**, navigate toohello wadexample storage account.</span></span> <span data-ttu-id="cac90-160">Después de servicio en la nube Hola se ha estado ejecutando unos minutos cinco (5), debería ver las tablas de hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** y **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="cac90-160">After hello cloud service has been running about five (5) minutes, you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="cac90-161">Haga doble clic en uno de telemetría de Hola de tooview de tablas de Hola que se han recopilado.</span><span class="sxs-lookup"><span data-stu-id="cac90-161">Double-click one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="cac90-163">Esquema del archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="cac90-163">Configuration File Schema</span></span>
<span data-ttu-id="cac90-164">archivo de configuración de diagnósticos de Hello define valores que son valores de configuración de diagnóstico de tooinitialize usado cuando se inicia el agente de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac90-164">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="cac90-165">Vea hello [referencia de esquema más reciente](https://msdn.microsoft.com/library/azure/mt634524.aspx) para los valores válidos y ejemplos.</span><span class="sxs-lookup"><span data-stu-id="cac90-165">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cac90-166">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="cac90-166">Troubleshooting</span></span>
<span data-ttu-id="cac90-167">Si tiene problemas, consulte [Solución de problemas de Diagnósticos de Azure](../azure-diagnostics-troubleshooting.md) para obtener ayuda relacionada con problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="cac90-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cac90-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cac90-168">Next Steps</span></span>
<span data-ttu-id="cac90-169">[Ver una lista de relacionados artículos de diagnóstico de máquina virtual Azure](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) datos de hello toochange va a recopilar, solucionar problemas o para obtener más información sobre diagnósticos en general.</span><span class="sxs-lookup"><span data-stu-id="cac90-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
