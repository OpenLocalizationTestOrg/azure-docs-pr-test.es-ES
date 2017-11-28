---
title: "Cómo usar Diagnósticos de Azure (.NET) con Cloud Services | Microsoft Docs"
description: "Use Diagnósticos de Azure para recopilar datos de los Servicios en la nube de Azure para realizar tareas de depuración, medición de rendimiento, supervisión, análisis de tráfico y más."
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
ms.openlocfilehash: 333d2f26ce043a167fb84858c8327cb39e868ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="8e71c-103">Habilitación de diagnósticos de Azure en servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="8e71c-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="8e71c-104">Consulte [Introducción a Diagnósticos de Azure](../azure-diagnostics.md) para obtener información sobre Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e71c-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-worker-role"></a><span data-ttu-id="8e71c-105">Habilitación de Diagnósticos en un rol de trabajo</span><span class="sxs-lookup"><span data-stu-id="8e71c-105">How to Enable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="8e71c-106">En este tutorial se describe cómo implementar un rol de trabajo de Azure que emite datos de telemetría mediante la clase EventSource de .NET.</span><span class="sxs-lookup"><span data-stu-id="8e71c-106">This walkthrough describes how to implement an Azure worker role that emits telemetry data using the .NET EventSource class.</span></span> <span data-ttu-id="8e71c-107">Diagnósticos de Azure se usa para recopilar datos de telemetría y almacenarla en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e71c-107">Azure Diagnostics is used to collect the telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="8e71c-108">Al crear un rol de trabajo, Visual Studio habilita automáticamente Diagnósticos 1.0 como parte de la solución en los SDK de Azure para .NET 2.4, y las versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="8e71c-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of the solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="8e71c-109">En las instrucciones siguientes se describe el proceso para crear el rol de trabajo, deshabilitar Diagnósticos 1.0 de la solución e implementar Diagnósticos 1.2 o 1.3 en el rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="8e71c-109">The following instructions describe the process for creating the worker role, disabling Diagnostics 1.0 from the solution, and deploying Diagnostics 1.2 or 1.3 to your worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8e71c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8e71c-110">Prerequisites</span></span>
<span data-ttu-id="8e71c-111">En este artículo se supone que tiene una suscripción a Azure y usa Visual Studio con Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="8e71c-111">This article assumes you have an Azure subscription and are using Visual Studio with the Azure SDK.</span></span> <span data-ttu-id="8e71c-112">Si no tiene una suscripción de Azure, puede registrarse para obtener una [prueba gratuita][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="8e71c-112">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="8e71c-113">Asegúrese de [instalar y configurar Azure PowerShell versión 0.8.7 o posterior][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="8e71c-113">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="8e71c-114">Paso 1: crear roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="8e71c-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="8e71c-115">Inicie **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="8e71c-116">Cree un proyecto en **Azure Cloud Services** desde la plantilla **Nube** cuyo destino sea .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="8e71c-116">Create an **Azure Cloud Service** project from the **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="8e71c-117">Asigne al proyecto el nombre "WadExample" y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="8e71c-117">Name the project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="8e71c-118">Seleccione **Rol de trabajo** y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="8e71c-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="8e71c-119">Se creará el proyecto.</span><span class="sxs-lookup"><span data-stu-id="8e71c-119">The project will be created.</span></span>
4. <span data-ttu-id="8e71c-120">En el **Explorador de soluciones**, haga doble clic en el archivo de propiedades **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-120">In **Solution Explorer**, double-click the **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="8e71c-121">En la pestaña **Configuración**, desactive la opción **Habilitar Diagnostics** para deshabilitar Diagnostics 1.0 (SDK de Azure 2.4 y las versiones anteriores).</span><span class="sxs-lookup"><span data-stu-id="8e71c-121">In the **Configuration** tab, un-check **Enable Diagnostics** to disable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="8e71c-122">Compile la solución para comprobar que no hay errores.</span><span class="sxs-lookup"><span data-stu-id="8e71c-122">Build your solution to verify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="8e71c-123">Paso 2: instrumentar el código</span><span class="sxs-lookup"><span data-stu-id="8e71c-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="8e71c-124">Reemplace el contenido de WorkerRole.cs por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="8e71c-124">Replace the contents of WorkerRole.cs with the following code.</span></span> <span data-ttu-id="8e71c-125">La clase SampleEventSourceWriter, heredada de la [clase EventSource][EventSource Class], implementa cuatro métodos de registro: **SendEnums**, **MessageMethod**, **SetOther** y **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-125">The class SampleEventSourceWriter, inherited from the [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="8e71c-126">El primer parámetro del método **WriteEvent** define el identificador para el evento correspondiente.</span><span class="sxs-lookup"><span data-stu-id="8e71c-126">The first parameter to the **WriteEvent** method defines the ID for the respective event.</span></span> <span data-ttu-id="8e71c-127">El método Run implementa un bucle infinito que llama a cada uno de los métodos de registro implementados en la clase **SampleEventSourceWriter** cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="8e71c-127">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

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
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums to int for efficient logging.
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

                // Emit several events every time we go through the loop
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
            // Set the maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="8e71c-128">Paso 3: implementar roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="8e71c-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="8e71c-129">Implemente su rol de trabajo en Azure desde Visual Studio seleccionando el proyecto **WadExample** en el Explorador de soluciones y luego **Publicar** en el menú **Compilar**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-129">Deploy your worker role to Azure from within Visual Studio by selecting the **WadExample** project in the Solution Explorer then **Publish** from the **Build** menu.</span></span>
2. <span data-ttu-id="8e71c-130">Elija su suscripción.</span><span class="sxs-lookup"><span data-stu-id="8e71c-130">Choose your subscription.</span></span>
3. <span data-ttu-id="8e71c-131">En el cuadro de diálogo **Configuración de publicación de Microsoft Azure**, seleccione **Crear nuevo…**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-131">In the **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="8e71c-132">En el cuadro de diálogo **Crear servicio en la nube y cuenta de almacenamiento**, escriba un **nombre** (por ejemplo, "WadExample") y seleccione una región o un grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="8e71c-132">In the **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="8e71c-133">Establezca el **Entorno** en **Ensayo**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-133">Set the **Environment** to **Staging**.</span></span>
6. <span data-ttu-id="8e71c-134">Modifique cualquier otro parámetro de **Configuración** según sea necesario y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="8e71c-135">Una vez finalizada la implementación, compruebe en Azure Portal que el servicio en la nube está en estado **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-135">After deployment has completed, verify in the Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-the-extension"></a><span data-ttu-id="8e71c-136">Paso 4: crear el archivo de configuración de Diagnósticos e instalar la extensión</span><span class="sxs-lookup"><span data-stu-id="8e71c-136">Step 4: Create your Diagnostics configuration file and install the extension</span></span>
1. <span data-ttu-id="8e71c-137">Descargue la definición del esquema del archivo de configuración público ejecutando el comando de PowerShell siguiente:</span><span class="sxs-lookup"><span data-stu-id="8e71c-137">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="8e71c-138">Agregue un archivo XML para su **WorkerRole1** proyecto con el botón secundario en el **WorkerRole1** de proyecto y seleccione **agregar** -> **nuevo elemento...**</span><span class="sxs-lookup"><span data-stu-id="8e71c-138">Add an XML file to your **WorkerRole1** project by right-clicking on the **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="8e71c-139"> -> **Elementos de Visual C#** -> **Datos** -> **Archivo XML**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="8e71c-140">Asigne al archivo el nombre "WadExample.xml".</span><span class="sxs-lookup"><span data-stu-id="8e71c-140">Name the file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="8e71c-142">Asocie WadConfig.xsd al archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="8e71c-142">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="8e71c-143">Asegúrese de que la ventana del editor de WadExample es la ventana activa.</span><span class="sxs-lookup"><span data-stu-id="8e71c-143">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="8e71c-144">Presione **F4** para abrir la ventana **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-144">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="8e71c-145">Haga clic en la propiedad **Esquemas** de la ventana **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-145">Click the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="8e71c-146">Haga clic en **…**</span><span class="sxs-lookup"><span data-stu-id="8e71c-146">Click the **…**</span></span> <span data-ttu-id="8e71c-147">in the **Esquemas** .</span><span class="sxs-lookup"><span data-stu-id="8e71c-147">in the **Schemas** property.</span></span> <span data-ttu-id="8e71c-148">Haga clic en **Agregar…**</span><span class="sxs-lookup"><span data-stu-id="8e71c-148">Click the **Add…**</span></span> <span data-ttu-id="8e71c-149">y vaya a la ubicación en la que ha guardado el archivo XSD y seleccione el archivo WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="8e71c-149">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="8e71c-150">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-150">Click **OK**.</span></span>

4. <span data-ttu-id="8e71c-151">Reemplace el contenido del archivo de configuración WadExample.xml por el siguiente archivo XM y guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="8e71c-151">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="8e71c-152">Este archivo de configuración define un par de contadores de rendimiento para recopilar: uno para la utilización de la CPU y el otro para la utilización de memoria.</span><span class="sxs-lookup"><span data-stu-id="8e71c-152">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="8e71c-153">A continuación, la configuración define los cuatro eventos correspondientes a los métodos de la clase SampleEventSourceWriter.</span><span class="sxs-lookup"><span data-stu-id="8e71c-153">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="8e71c-154">Paso 5: instalar Diagnósticos en roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="8e71c-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="8e71c-155">Los cmdlets de PowerShell para administrar Diagnósticos en un rol web o de trabajo son: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension y Remove-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="8e71c-155">The PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="8e71c-156">Abra Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8e71c-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="8e71c-157">Ejecute el script para instalar Diagnostics en su rol de trabajo (reemplace *StorageAccountKey* por la clave de cuenta de almacenamiento para la clave de almacenamiento wadexample) y *config_path* por la ruta al archivo *WadExample.xml*:</span><span class="sxs-lookup"><span data-stu-id="8e71c-157">Execute the script to install Diagnostics on your worker role (replace *StorageAccountKey* with the storage account key for your wadexample storage account and *config_path* with the path to the *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="8e71c-158">Paso 6: consultar los datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="8e71c-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="8e71c-159">En el **Explorador de servidores** de Visual Studio, navegue hasta la cuenta de almacenamiento wadexample.</span><span class="sxs-lookup"><span data-stu-id="8e71c-159">In the Visual Studio **Server Explorer**, navigate to the wadexample storage account.</span></span> <span data-ttu-id="8e71c-160">Cuando el servicio en la nube lleve en ejecución unos cinco (5) minutos, debería ver las tablas **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** y **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="8e71c-160">After the cloud service has been running about five (5) minutes, you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="8e71c-161">Haga doble clic en cualquiera de ellas para ver la telemetría que se ha recopilado.</span><span class="sxs-lookup"><span data-stu-id="8e71c-161">Double-click one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="8e71c-163">Esquema del archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="8e71c-163">Configuration File Schema</span></span>
<span data-ttu-id="8e71c-164">El archivo de configuración de Diagnósticos define valores que se usan para inicializar la configuración de diagnóstico al iniciar el agente de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="8e71c-164">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="8e71c-165">Consulte en la [referencia de esquema más reciente](https://msdn.microsoft.com/library/azure/mt634524.aspx) los valores válidos y ejemplos.</span><span class="sxs-lookup"><span data-stu-id="8e71c-165">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8e71c-166">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="8e71c-166">Troubleshooting</span></span>
<span data-ttu-id="8e71c-167">Si tiene problemas, consulte [Solución de problemas de Diagnósticos de Azure](../azure-diagnostics-troubleshooting.md) para obtener ayuda relacionada con problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="8e71c-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e71c-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8e71c-168">Next Steps</span></span>
<span data-ttu-id="8e71c-169">[Vea una lista de artículos relacionados con el diagnóstico de máquinas virtuales de Azure](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) para cambiar los datos que se recopilan, solucionar problemas u obtener más información acerca de los diagnósticos en general.</span><span class="sxs-lookup"><span data-stu-id="8e71c-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
