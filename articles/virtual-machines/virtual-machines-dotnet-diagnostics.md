---
title: "aaaHow toouse diagnósticos de Azure en máquinas virtuales | Documentos de Microsoft"
description: "Uso de datos de toogather de diagnósticos de Azure desde máquinas virtuales de Azure para depurar, medir el rendimiento, supervisión, análisis del tráfico y mucho más."
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="e340a-103">Habilitación de diagnósticos en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="e340a-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="e340a-104">Consulte [Introducción a Diagnósticos de Azure](../monitoring-and-diagnostics/azure-diagnostics.md) para obtener información sobre Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e340a-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="e340a-105">¿Cómo tooEnable diagnósticos en una máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="e340a-105">How tooEnable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="e340a-106">Este tutorial describe cómo tooremotely instalar diagnóstico tooan máquina virtual de Azure desde un equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="e340a-106">This walk through describes how tooremotely install Diagnostics tooan Azure virtual machine from a development computer.</span></span> <span data-ttu-id="e340a-107">También aprenderá cómo tooimplement una aplicación que se ejecuta en esa máquina virtual de Azure y envía datos de telemetría mediante Hola .NET [EventSource (clase)][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="e340a-107">You also learn how tooimplement an application that runs on that Azure virtual machine and emits telemetry data using hello .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="e340a-108">Diagnósticos de Azure es la telemetría de hello toocollect usado y almacenan en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e340a-108">Azure Diagnostics is used toocollect hello telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="e340a-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e340a-109">Pre-requisites</span></span>
<span data-ttu-id="e340a-110">Este tutorial se supone que tiene una suscripción de Azure y está usando Visual Studio de 2017 con hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="e340a-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with hello Azure SDK.</span></span> <span data-ttu-id="e340a-111">Si no tiene una suscripción de Azure, puede registrarse para hello [gratuita][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="e340a-111">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="e340a-112">Asegúrese de que demasiado[instalar y configurar Azure PowerShell versión 0.8.7 o posterior][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="e340a-112">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="e340a-113">Paso 1: crear una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e340a-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="e340a-114">En el equipo del desarrollador, inicie Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e340a-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="e340a-115">En Visual Studio hello **Explorador de servidores** expanda **Azure**, haga clic en **máquinas virtuales** , a continuación, seleccione **crear Máquina Virtual**.</span><span class="sxs-lookup"><span data-stu-id="e340a-115">In hello Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="e340a-116">Seleccione la suscripción de Azure en hello **elegir una suscripción** cuadro de diálogo y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e340a-116">Select your Azure subscription in hello **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="e340a-117">Seleccione **Windows Server 2012 R2 Datacenter, junio de 2017** en hello **seleccionar una imagen de máquina Virtual** cuadro de diálogo y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e340a-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in hello **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="e340a-118">Hola **configuración básica de máquina Virtual**, establezca el nombre de la máquina virtual de hello demasiado "wadexample".</span><span class="sxs-lookup"><span data-stu-id="e340a-118">In hello **Virtual Machine Basic Settings**, set hello virtual machine name too"wadexample".</span></span> <span data-ttu-id="e340a-119">Establezca su nombre de usuario y contraseña de administrador y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e340a-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="e340a-120">Hola **configuración de servicio de nube** cuadro de diálogo Crear un nuevo servicio de nube denominado "wadexampleVM".</span><span class="sxs-lookup"><span data-stu-id="e340a-120">In hello **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="e340a-121">Cree una nueva cuenta de almacenamiento con el nombre "wadexample" y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e340a-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="e340a-122">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e340a-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="e340a-123">Paso 2: crear la aplicación</span><span class="sxs-lookup"><span data-stu-id="e340a-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="e340a-124">En el equipo del desarrollador, inicie Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e340a-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="e340a-125">Cree una aplicación de consola de Visual C# nueva dirigida a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e340a-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="e340a-126">Proyecto de Hola de nombre "WadExampleVM".</span><span class="sxs-lookup"><span data-stu-id="e340a-126">Name hello project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="e340a-128">Reemplace el contenido de Hola de Program.cs con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="e340a-128">Replace hello contents of Program.cs with hello following code.</span></span> <span data-ttu-id="e340a-129">Hola clase **SampleEventSourceWriter** implementa los cuatro métodos de registro: **SendEnums**, **MessageMethod**, **SetOther** y  **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="e340a-129">hello class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="e340a-130">Hola primer parámetro toohello método WriteEvent define identificador hello para el evento correspondiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e340a-130">hello first parameter toohello WriteEvent method defines hello ID for hello respective event.</span></span> <span data-ttu-id="e340a-131">Hola método Run implementa un bucle infinito que llama a cada uno de hello registro en los métodos implementados en hello **SampleEventSourceWriter** clase cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="e340a-131">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through hello loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. <span data-ttu-id="e340a-132">Guarde el archivo hello y seleccione **compilar solución** de hello **compilar** menú toobuild el código.</span><span class="sxs-lookup"><span data-stu-id="e340a-132">Save hello file and select **Build Solution** from hello **Build** menu toobuild your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="e340a-133">Paso 3: implementar la aplicación</span><span class="sxs-lookup"><span data-stu-id="e340a-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="e340a-134">Haga doble clic en hello **WadExampleVM** proyecto **el Explorador de soluciones** y elija **Abrir carpeta en el Explorador de archivos**.</span><span class="sxs-lookup"><span data-stu-id="e340a-134">Right-click on hello **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="e340a-135">Navegue toohello *bin\Debug* carpeta y copie Hola a todos los archivos (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="e340a-135">Navigate toohello *bin\Debug* folder and copy all hello files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="e340a-136">En **Explorador de servidores** doble clic en la máquina virtual de Hola y elija **conectar utilizando Escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="e340a-136">In **Server Explorer** right-click on hello virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="e340a-137">Una vez conectado toohello VM cree una carpeta denominada WadExampleVM y pegue los archivos de aplicación en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e340a-137">Once connected toohello VM create a folder named WadExampleVM and paste your application files into hello folder.</span></span>
5. <span data-ttu-id="e340a-138">Inicie la aplicación hello WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="e340a-138">Launch hello application WadExampleVM.exe.</span></span> <span data-ttu-id="e340a-139">Debe ver una ventana de la consola en blanco.</span><span class="sxs-lookup"><span data-stu-id="e340a-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a><span data-ttu-id="e340a-140">Paso 4: Crear la configuración de diagnóstico e instalar extensión Hola</span><span class="sxs-lookup"><span data-stu-id="e340a-140">Step 4: Create your Diagnostics configuration and install hello Extension</span></span>
1. <span data-ttu-id="e340a-141">Descargue el equipo de desarrollo tooyour definición de esquema de la archivo de configuración pública de hello ejecutando el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="e340a-141">Download hello public configuration file schema definition tooyour development computer by executing hello following PowerShell command:</span></span>

     <span data-ttu-id="e340a-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="e340a-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="e340a-143">Abra un nuevo archivo XML en Visual Studio, ya sea en un proyecto que ya tenga abierto o en una instancia de Visual Studio sin proyectos abiertos.</span><span class="sxs-lookup"><span data-stu-id="e340a-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="e340a-144">En Visual Studio, seleccione **Agregar** -> **Nuevo elemento...**</span><span class="sxs-lookup"><span data-stu-id="e340a-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="e340a-145"> -> **Elementos de Visual C#** -> **Datos** -> **Archivo XML**.</span><span class="sxs-lookup"><span data-stu-id="e340a-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="e340a-146">Nombre de archivo hello "WadExample.xml"</span><span class="sxs-lookup"><span data-stu-id="e340a-146">Name hello file "WadExample.xml"</span></span>
3. <span data-ttu-id="e340a-147">Asociar el archivo de configuración de Hola Hola WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="e340a-147">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="e340a-148">Asegúrese de que la ventana del editor de hello WadExample.xml es la ventana activa de Hola.</span><span class="sxs-lookup"><span data-stu-id="e340a-148">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="e340a-149">Presione **F4** tooopen hello **propiedades** ventana.</span><span class="sxs-lookup"><span data-stu-id="e340a-149">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="e340a-150">Haga clic en hello **esquemas** propiedad Hola **propiedades** ventana.</span><span class="sxs-lookup"><span data-stu-id="e340a-150">Click on hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="e340a-151">Haga clic en hello **...**</span><span class="sxs-lookup"><span data-stu-id="e340a-151">Click hello **…**</span></span> <span data-ttu-id="e340a-152">Hola **esquemas** propiedad.</span><span class="sxs-lookup"><span data-stu-id="e340a-152">in hello **Schemas** property.</span></span> <span data-ttu-id="e340a-153">Haga clic en hello **agregar...**</span><span class="sxs-lookup"><span data-stu-id="e340a-153">Click hello **Add…**</span></span> <span data-ttu-id="e340a-154">botón y navegar por la ubicación de toohello donde guardó archivo XSD de Hola y Hola Seleccione archivo WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="e340a-154">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="e340a-155">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e340a-155">Click **OK**.</span></span>
4. <span data-ttu-id="e340a-156">Reemplace el contenido de Hola Hola WadExample.xml del archivo de configuración con hello continuación de XML y guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="e340a-156">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="e340a-157">Este archivo de configuración define un par toocollect de contadores de rendimiento: uno para el uso de CPU y otro para el uso de memoria.</span><span class="sxs-lookup"><span data-stu-id="e340a-157">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="e340a-158">A continuación, la configuración de hello define cuatro eventos de hello correspondientes métodos toohello Hola SampleEventSourceWriter clase.</span><span class="sxs-lookup"><span data-stu-id="e340a-158">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="e340a-159">Paso 5: instalar Diagnósticos de forma remota en la máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="e340a-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="e340a-160">Hello cmdlets de PowerShell para administrar los diagnósticos en una máquina virtual son: AzureVMDiagnosticsExtension Set y Get-AzureVMDiagnosticsExtension, Remove-AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="e340a-160">hello PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="e340a-161">En el equipo del desarrollador, abra Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e340a-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="e340a-162">Tooremotely instalar diagnóstico de hello secuencia de comandos se ejecuta en la máquina virtual (reemplace `<user>` con el nombre de directorio del usuario.</span><span class="sxs-lookup"><span data-stu-id="e340a-162">Execute hello script tooremotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="e340a-163">Reemplace `<StorageAccountKey>` con clave de cuenta de almacenamiento de hello para la cuenta de almacenamiento wadexamplevm):</span><span class="sxs-lookup"><span data-stu-id="e340a-163">Replace `<StorageAccountKey>` with hello storage account key for your wadexamplevm storage account):</span></span>
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="e340a-164">Paso 6: consultar los datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="e340a-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="e340a-165">En Visual Studio hello **Explorador de servidores** navegar por la cuenta de almacenamiento de toohello wadexample.</span><span class="sxs-lookup"><span data-stu-id="e340a-165">In hello Visual Studio **Server Explorer** navigate toohello wadexample storage account.</span></span> <span data-ttu-id="e340a-166">Después de la máquina virtual se ha estado ejecutando aproximadamente 5 minutos de Hola verá tablas hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** y **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="e340a-166">After hello VM has been running about 5 minutes you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="e340a-167">Haga doble clic en uno de telemetría de Hola de tooview de tablas de Hola que se han recopilado.</span><span class="sxs-lookup"><span data-stu-id="e340a-167">Double-click on one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="e340a-169">Esquema del archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="e340a-169">Configuration file schema</span></span>
<span data-ttu-id="e340a-170">archivo de configuración de diagnósticos de Hello define valores que son valores de configuración de diagnóstico de tooinitialize usado cuando se inicia el agente de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="e340a-170">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="e340a-171">Vea hello [referencia de esquema más reciente](https://msdn.microsoft.com/library/azure/mt634524.aspx) para los valores válidos y ejemplos.</span><span class="sxs-lookup"><span data-stu-id="e340a-171">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e340a-172">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="e340a-172">Troubleshooting</span></span>
<span data-ttu-id="e340a-173">Consulte [Solución de problemas de Diagnósticos de Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e340a-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e340a-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e340a-174">Next steps</span></span>
<span data-ttu-id="e340a-175">[Vea una lista de máquina virtual relacionados con artículos de diagnósticos de Azure](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) datos de hello toochange va a recopilar, solucionar problemas o para obtener más información sobre diagnósticos en general.</span><span class="sxs-lookup"><span data-stu-id="e340a-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
