---
title: "Uso de Diagnósticos de Azure en máquinas virtuales | Microsoft Docs"
description: "Use Diagnósticos de Azure para recopilar datos de las máquinas virtuales de Azure para realizar tareas de depuración, medición de rendimiento, supervisión, análisis de tráfico y más."
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
ms.openlocfilehash: 8ff6b9825212359617b748aba1c78ed789b130dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="635c8-103">Habilitación de diagnósticos en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="635c8-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="635c8-104">Consulte [Introducción a Diagnósticos de Azure](../monitoring-and-diagnostics/azure-diagnostics.md) para obtener información sobre Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="635c8-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="635c8-105">Habilitación de Diagnósticos en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="635c8-105">How to Enable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="635c8-106">En este tutorial se describe cómo instalar Diagnósticos de forma remota en una máquina virtual de Azure desde un equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="635c8-106">This walk through describes how to remotely install Diagnostics to an Azure virtual machine from a development computer.</span></span> <span data-ttu-id="635c8-107">También aprenderá a implementar una aplicación que se ejecuta en esa máquina virtual de Azure y emite datos de telemetría con la [clase EventSource][EventSource Class] de .NET.</span><span class="sxs-lookup"><span data-stu-id="635c8-107">You also learn how to implement an application that runs on that Azure virtual machine and emits telemetry data using the .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="635c8-108">Diagnósticos de Azure se usa para recopilar la telemetría y almacenarla en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="635c8-108">Azure Diagnostics is used to collect the telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="635c8-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="635c8-109">Pre-requisites</span></span>
<span data-ttu-id="635c8-110">En este tutorial se supone que tiene una suscripción a Azure y usa Visual Studio 2017 con el SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="635c8-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with the Azure SDK.</span></span> <span data-ttu-id="635c8-111">Si no tiene una suscripción de Azure, puede registrarse para obtener una [prueba gratuita][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="635c8-111">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="635c8-112">Asegúrese de [instalar y configurar Azure PowerShell versión 0.8.7 o posterior][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="635c8-112">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="635c8-113">Paso 1: crear una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="635c8-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="635c8-114">En el equipo del desarrollador, inicie Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="635c8-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="635c8-115">En el **Explorador de servidores** de Visual Studio, expanda **Azure**, haga clic con el botón derecho en **Máquinas virtuales** y, a continuación, seleccione **Crear máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="635c8-115">In the Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="635c8-116">Seleccione la suscripción de Azure en el cuadro de diálogo **Elegir una suscripción** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="635c8-116">Select your Azure subscription in the **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="635c8-117">Seleccione **Windows Server 2012 R2 Datacenter, junio de 2017** en el cuadro de diálogo **Seleccionar una imagen de máquina virtual** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="635c8-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in the **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="635c8-118">En **Configuración básica de máquina virtual**, establezca el nombre de la máquina virtual en "wadexample".</span><span class="sxs-lookup"><span data-stu-id="635c8-118">In the **Virtual Machine Basic Settings**, set the virtual machine name to "wadexample".</span></span> <span data-ttu-id="635c8-119">Establezca su nombre de usuario y contraseña de administrador y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="635c8-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="635c8-120">En el cuadro de diálogo **Configuración del servicio en la nube** , cree un nuevo servicio en la nube denominado "wadexampleVM".</span><span class="sxs-lookup"><span data-stu-id="635c8-120">In the **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="635c8-121">Cree una nueva cuenta de almacenamiento con el nombre "wadexample" y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="635c8-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="635c8-122">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="635c8-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="635c8-123">Paso 2: crear la aplicación</span><span class="sxs-lookup"><span data-stu-id="635c8-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="635c8-124">En el equipo del desarrollador, inicie Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="635c8-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="635c8-125">Cree una aplicación de consola de Visual C# nueva dirigida a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="635c8-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="635c8-126">Asigne al proyecto el nombre "WadExampleVM".</span><span class="sxs-lookup"><span data-stu-id="635c8-126">Name the project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="635c8-128">Reemplace el contenido de Program.cs por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="635c8-128">Replace the contents of Program.cs with the following code.</span></span> <span data-ttu-id="635c8-129">La clase **SampleEventSourceWriter** implementa cuatro métodos de registro: **SendEnums**, **MessageMethod**, **SetOther** y **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="635c8-129">The class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="635c8-130">El primer parámetro del método WriteEvent define el identificador para el evento correspondiente.</span><span class="sxs-lookup"><span data-stu-id="635c8-130">The first parameter to the WriteEvent method defines the ID for the respective event.</span></span> <span data-ttu-id="635c8-131">El método Run implementa un bucle infinito que llama a cada uno de los métodos de registro implementados en la clase **SampleEventSourceWriter** cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="635c8-131">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums to int for efficient logging.
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

             // Emit several events every time we go through the loop
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
4. <span data-ttu-id="635c8-132">Guarde el archivo y seleccione **Compilar solución** en el menú **Compilar** para compilar el código.</span><span class="sxs-lookup"><span data-stu-id="635c8-132">Save the file and select **Build Solution** from the **Build** menu to build your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="635c8-133">Paso 3: implementar la aplicación</span><span class="sxs-lookup"><span data-stu-id="635c8-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="635c8-134">Haga clic con el botón derecho en el proyecto **WadExampleVM** del **Explorador de soluciones** y seleccione **Abrir carpeta en el Explorador de archivos**.</span><span class="sxs-lookup"><span data-stu-id="635c8-134">Right-click on the **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="635c8-135">Vaya a la carpeta *bin\Debug* y copie todos los archivos (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="635c8-135">Navigate to the *bin\Debug* folder and copy all the files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="635c8-136">En el **Explorador de servidores**, haga clic con el botón derecho en la máquina virtual y elija **Conectar utilizando Escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="635c8-136">In **Server Explorer** right-click on the virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="635c8-137">Una vez conectado a la máquina virtual, cree una carpeta con el nombre WadExampleVM y pegue los archivos de la aplicación en la carpeta.</span><span class="sxs-lookup"><span data-stu-id="635c8-137">Once connected to the VM create a folder named WadExampleVM and paste your application files into the folder.</span></span>
5. <span data-ttu-id="635c8-138">Inicie la aplicación WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="635c8-138">Launch the application WadExampleVM.exe.</span></span> <span data-ttu-id="635c8-139">Debe ver una ventana de la consola en blanco.</span><span class="sxs-lookup"><span data-stu-id="635c8-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-the-extension"></a><span data-ttu-id="635c8-140">Paso 4: crear la configuración de Diagnósticos e instalar la extensión</span><span class="sxs-lookup"><span data-stu-id="635c8-140">Step 4: Create your Diagnostics configuration and install the Extension</span></span>
1. <span data-ttu-id="635c8-141">Descargue la definición del esquema del archivo de configuración público en su equipo de desarrollo ejecutando el comando de PowerShell siguiente:</span><span class="sxs-lookup"><span data-stu-id="635c8-141">Download the public configuration file schema definition to your development computer by executing the following PowerShell command:</span></span>

     <span data-ttu-id="635c8-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="635c8-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="635c8-143">Abra un nuevo archivo XML en Visual Studio, ya sea en un proyecto que ya tenga abierto o en una instancia de Visual Studio sin proyectos abiertos.</span><span class="sxs-lookup"><span data-stu-id="635c8-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="635c8-144">En Visual Studio, seleccione **Agregar** -> **Nuevo elemento...**</span><span class="sxs-lookup"><span data-stu-id="635c8-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="635c8-145"> -> **Elementos de Visual C#** -> **Datos** -> **Archivo XML**.</span><span class="sxs-lookup"><span data-stu-id="635c8-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="635c8-146">Asigne al archivo el nombre "WadExample.xml".</span><span class="sxs-lookup"><span data-stu-id="635c8-146">Name the file "WadExample.xml"</span></span>
3. <span data-ttu-id="635c8-147">Asocie WadConfig.xsd al archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="635c8-147">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="635c8-148">Asegúrese de que la ventana del editor de WadExample es la ventana activa.</span><span class="sxs-lookup"><span data-stu-id="635c8-148">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="635c8-149">Presione **F4** para abrir la ventana **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="635c8-149">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="635c8-150">Haga clic en la propiedad **Esquemas** de la ventana **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="635c8-150">Click on the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="635c8-151">Haga clic en **…**</span><span class="sxs-lookup"><span data-stu-id="635c8-151">Click the **…**</span></span> <span data-ttu-id="635c8-152">in the **Esquemas** .</span><span class="sxs-lookup"><span data-stu-id="635c8-152">in the **Schemas** property.</span></span> <span data-ttu-id="635c8-153">Haga clic en **Agregar…**</span><span class="sxs-lookup"><span data-stu-id="635c8-153">Click the **Add…**</span></span> <span data-ttu-id="635c8-154">y vaya a la ubicación en la que ha guardado el archivo XSD y seleccione el archivo WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="635c8-154">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="635c8-155">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="635c8-155">Click **OK**.</span></span>
4. <span data-ttu-id="635c8-156">Reemplace el contenido del archivo de configuración WadExample.xml por el siguiente archivo XM y guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="635c8-156">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="635c8-157">Este archivo de configuración define un par de contadores de rendimiento para recopilar: uno para la utilización de la CPU y el otro para la utilización de memoria.</span><span class="sxs-lookup"><span data-stu-id="635c8-157">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="635c8-158">A continuación, la configuración define los cuatro eventos correspondientes a los métodos de la clase SampleEventSourceWriter.</span><span class="sxs-lookup"><span data-stu-id="635c8-158">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="635c8-159">Paso 5: instalar Diagnósticos de forma remota en la máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="635c8-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="635c8-160">Los cmdlets de PowerShell para administrar Diagnósticos en una máquina virtual son: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension y Remove-AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="635c8-160">The PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="635c8-161">En el equipo del desarrollador, abra Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="635c8-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="635c8-162">Ejecute el script para instalar Diagnostics de forma remota en la máquina virtual (reemplace `<user>` por el nombre de directorio del usuario.</span><span class="sxs-lookup"><span data-stu-id="635c8-162">Execute the script to remotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="635c8-163">Reemplace `<StorageAccountKey>` por la clave de cuenta de almacenamiento para la cuenta de almacenamiento wadexamplevm):</span><span class="sxs-lookup"><span data-stu-id="635c8-163">Replace `<StorageAccountKey>` with the storage account key for your wadexamplevm storage account):</span></span>
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
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="635c8-164">Paso 6: consultar los datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="635c8-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="635c8-165">En el **Explorador de servidores** de Visual Studio, vaya a la cuenta de almacenamiento wadexample.</span><span class="sxs-lookup"><span data-stu-id="635c8-165">In the Visual Studio **Server Explorer** navigate to the wadexample storage account.</span></span> <span data-ttu-id="635c8-166">Cuando la máquina virtual lleve ejecutándose unos 5 minutos, debería ver las tablas **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** y **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="635c8-166">After the VM has been running about 5 minutes you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="635c8-167">Haga doble clic en una de las tablas para ver la telemetría que se ha recopilado.</span><span class="sxs-lookup"><span data-stu-id="635c8-167">Double-click on one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="635c8-169">Esquema del archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="635c8-169">Configuration file schema</span></span>
<span data-ttu-id="635c8-170">El archivo de configuración de Diagnósticos define valores que se usan para inicializar la configuración de diagnóstico al iniciar el agente de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="635c8-170">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="635c8-171">Consulte en la [referencia de esquema más reciente](https://msdn.microsoft.com/library/azure/mt634524.aspx) los valores válidos y ejemplos.</span><span class="sxs-lookup"><span data-stu-id="635c8-171">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="635c8-172">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="635c8-172">Troubleshooting</span></span>
<span data-ttu-id="635c8-173">Consulte [Solución de problemas de Diagnósticos de Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="635c8-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="635c8-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="635c8-174">Next steps</span></span>
<span data-ttu-id="635c8-175">[Vea una lista de artículos sobre Diagnósticos de Azure relacionados con máquinas virtuales](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) para cambiar los datos que se van a recopilar, solucionar problemas u obtener más información sobre los diagnósticos en general.</span><span class="sxs-lookup"><span data-stu-id="635c8-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
