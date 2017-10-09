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
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>Habilitación de diagnósticos en máquinas virtuales de Azure
Consulte [Introducción a Diagnósticos de Azure](../monitoring-and-diagnostics/azure-diagnostics.md) para obtener información sobre Diagnósticos de Azure.

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a>¿Cómo tooEnable diagnósticos en una máquina Virtual
Este tutorial describe cómo tooremotely instalar diagnóstico tooan máquina virtual de Azure desde un equipo de desarrollo. También aprenderá cómo tooimplement una aplicación que se ejecuta en esa máquina virtual de Azure y envía datos de telemetría mediante Hola .NET [EventSource (clase)][EventSource Class]. Diagnósticos de Azure es la telemetría de hello toocollect usado y almacenan en una cuenta de almacenamiento de Azure.

### <a name="pre-requisites"></a>Requisitos previos
Este tutorial se supone que tiene una suscripción de Azure y está usando Visual Studio de 2017 con hello Azure SDK. Si no tiene una suscripción de Azure, puede registrarse para hello [gratuita][Free Trial]. Asegúrese de que demasiado[instalar y configurar Azure PowerShell versión 0.8.7 o posterior][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-virtual-machine"></a>Paso 1: crear una máquina virtual
1. En el equipo del desarrollador, inicie Visual Studio 2017.
2. En Visual Studio hello **Explorador de servidores** expanda **Azure**, haga clic en **máquinas virtuales** , a continuación, seleccione **crear Máquina Virtual**.
3. Seleccione la suscripción de Azure en hello **elegir una suscripción** cuadro de diálogo y haga clic en **siguiente**.
4. Seleccione **Windows Server 2012 R2 Datacenter, junio de 2017** en hello **seleccionar una imagen de máquina Virtual** cuadro de diálogo y haga clic en **siguiente**.
5. Hola **configuración básica de máquina Virtual**, establezca el nombre de la máquina virtual de hello demasiado "wadexample". Establezca su nombre de usuario y contraseña de administrador y haga clic en **Siguiente**.
6. Hola **configuración de servicio de nube** cuadro de diálogo Crear un nuevo servicio de nube denominado "wadexampleVM". Cree una nueva cuenta de almacenamiento con el nombre "wadexample" y haga clic en **Siguiente**.
7. Haga clic en **Crear**.

### <a name="step-2-create-your-application"></a>Paso 2: crear la aplicación
1. En el equipo del desarrollador, inicie Visual Studio 2017.
2. Cree una aplicación de consola de Visual C# nueva dirigida a .NET Framework 4.5. Proyecto de Hola de nombre "WadExampleVM".

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. Reemplace el contenido de Hola de Program.cs con el siguiente código de hello. Hola clase **SampleEventSourceWriter** implementa los cuatro métodos de registro: **SendEnums**, **MessageMethod**, **SetOther** y  **HighFreq**. Hola primer parámetro toohello método WriteEvent define identificador hello para el evento correspondiente de Hola. Hola método Run implementa un bucle infinito que llama a cada uno de hello registro en los métodos implementados en hello **SampleEventSourceWriter** clase cada 10 segundos.

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
4. Guarde el archivo hello y seleccione **compilar solución** de hello **compilar** menú toobuild el código.

### <a name="step-3-deploy-your-application"></a>Paso 3: implementar la aplicación
1. Haga doble clic en hello **WadExampleVM** proyecto **el Explorador de soluciones** y elija **Abrir carpeta en el Explorador de archivos**.
2. Navegue toohello *bin\Debug* carpeta y copie Hola a todos los archivos (WadExampleVM.*)
3. En **Explorador de servidores** doble clic en la máquina virtual de Hola y elija **conectar utilizando Escritorio remoto**.
4. Una vez conectado toohello VM cree una carpeta denominada WadExampleVM y pegue los archivos de aplicación en la carpeta de Hola.
5. Inicie la aplicación hello WadExampleVM.exe. Debe ver una ventana de la consola en blanco.

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a>Paso 4: Crear la configuración de diagnóstico e instalar extensión Hola
1. Descargue el equipo de desarrollo tooyour definición de esquema de la archivo de configuración pública de hello ejecutando el siguiente comando de PowerShell de hello:

     (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
2. Abra un nuevo archivo XML en Visual Studio, ya sea en un proyecto que ya tenga abierto o en una instancia de Visual Studio sin proyectos abiertos. En Visual Studio, seleccione **Agregar** -> **Nuevo elemento...** -> **Elementos de Visual C#** -> **Datos** -> **Archivo XML**. Nombre de archivo hello "WadExample.xml"
3. Asociar el archivo de configuración de Hola Hola WadConfig.xsd. Asegúrese de que la ventana del editor de hello WadExample.xml es la ventana activa de Hola. Presione **F4** tooopen hello **propiedades** ventana. Haga clic en hello **esquemas** propiedad Hola **propiedades** ventana. Haga clic en hello **...** Hola **esquemas** propiedad. Haga clic en hello **agregar...** botón y navegar por la ubicación de toohello donde guardó archivo XSD de Hola y Hola Seleccione archivo WadConfig.xsd. Haga clic en **Aceptar**.
4. Reemplace el contenido de Hola Hola WadExample.xml del archivo de configuración con hello continuación de XML y guarde el archivo hello. Este archivo de configuración define un par toocollect de contadores de rendimiento: uno para el uso de CPU y otro para el uso de memoria. A continuación, la configuración de hello define cuatro eventos de hello correspondientes métodos toohello Hola SampleEventSourceWriter clase.

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a>Paso 5: instalar Diagnósticos de forma remota en la máquina virtual de Azure
Hello cmdlets de PowerShell para administrar los diagnósticos en una máquina virtual son: AzureVMDiagnosticsExtension Set y Get-AzureVMDiagnosticsExtension, Remove-AzureVMDiagnosticsExtension.

1. En el equipo del desarrollador, abra Azure PowerShell.
2. Tooremotely instalar diagnóstico de hello secuencia de comandos se ejecuta en la máquina virtual (reemplace `<user>` con el nombre de directorio del usuario. Reemplace `<StorageAccountKey>` con clave de cuenta de almacenamiento de hello para la cuenta de almacenamiento wadexamplevm):
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
### <a name="step-6-look-at-your-telemetry-data"></a>Paso 6: consultar los datos de telemetría
En Visual Studio hello **Explorador de servidores** navegar por la cuenta de almacenamiento de toohello wadexample. Después de la máquina virtual se ha estado ejecutando aproximadamente 5 minutos de Hola verá tablas hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** y **WADSetOtherTable**. Haga doble clic en uno de telemetría de Hola de tooview de tablas de Hola que se han recopilado.

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>Esquema del archivo de configuración
archivo de configuración de diagnósticos de Hello define valores que son valores de configuración de diagnóstico de tooinitialize usado cuando se inicia el agente de diagnóstico de Hola. Vea hello [referencia de esquema más reciente](https://msdn.microsoft.com/library/azure/mt634524.aspx) para los valores válidos y ejemplos.

## <a name="troubleshooting"></a>Solución de problemas
Consulte [Solución de problemas de Diagnósticos de Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) para obtener más información.

## <a name="next-steps"></a>Pasos siguientes
[Vea una lista de máquina virtual relacionados con artículos de diagnósticos de Azure](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) datos de hello toochange va a recopilar, solucionar problemas o para obtener más información sobre diagnósticos en general.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
