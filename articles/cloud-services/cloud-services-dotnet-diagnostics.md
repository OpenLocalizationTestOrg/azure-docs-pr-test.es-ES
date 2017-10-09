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
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a>Habilitación de diagnósticos de Azure en servicios en la nube de Azure
Consulte [Introducción a Diagnósticos de Azure](../azure-diagnostics.md) para obtener información sobre Diagnósticos de Azure.

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a>¿Cómo tooEnable diagnósticos en un rol de trabajo
Este tutorial describe cómo tooimplement un rol de trabajador de Azure que emite los datos de telemetría mediante Hola .NET EventSource (clase). Diagnósticos de Azure son toocollect usa los datos de telemetría hello y almacenan en una cuenta de almacenamiento de Azure. Al crear un rol de trabajo, Visual Studio permite automáticamente Diagnostics 1.0 como parte de la solución de hello en Azure SDK para .NET 2.4 y versiones anteriores. Hello las instrucciones siguientes describen Hola proceso para crear el rol de trabajo de hello, deshabilitar Diagnostics 1.0 de solución de Hola y la implementación de diagnóstico 1.2 o rol de trabajo tooyour 1.3.

### <a name="prerequisites"></a>Requisitos previos
En este artículo se supone que tiene una suscripción de Azure y está utilizando Visual Studio con hello Azure SDK. Si no tiene una suscripción de Azure, puede registrarse para hello [gratuita][Free Trial]. Asegúrese de que demasiado[instalar y configurar Azure PowerShell versión 0.8.7 o posterior][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-worker-role"></a>Paso 1: crear roles de trabajo
1. Inicie **Visual Studio**.
2. Crear un **servicio de nube de Azure** proyecto a partir de hello **nube** plantilla cuyo destino es .NET Framework 4.5.  Denomine el proyecto de Hola "WadExample" y haga clic en Aceptar.
3. Seleccione **Rol de trabajo** y haga clic en Aceptar. se creará el proyecto de Hola.
4. En **el Explorador de soluciones**, haga doble clic en hello **WorkerRole1** archivo de propiedades.
5. Hola **configuración** ficha desactive **habilitar diagnósticos** toodisable Diagnostics 1.0 (Azure SDK 2.4 y anterior).
6. Compilar la solución tooverify que no aparece ningún error.

### <a name="step-2-instrument-your-code"></a>Paso 2: instrumentar el código
Reemplace el contenido de Hola de WorkerRole.cs con el siguiente código de hello. Hola clase SampleEventSourceWriter, que se hereda de hello [EventSource (clase)][EventSource Class], implementa los cuatro métodos de registro: **SendEnums**, **MessageMethod** , **SetOther** y **HighFreq**. Hola primera toohello parámetro **WriteEvent** método define el identificador hello para el evento correspondiente de Hola. Hola método Run implementa un bucle infinito que llama a cada uno de hello registro en los métodos implementados en hello **SampleEventSourceWriter** clase cada 10 segundos.

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


### <a name="step-3-deploy-your-worker-role"></a>Paso 3: implementar roles de trabajo

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. Implementar el rol de trabajo tooAzure desde dentro de Visual Studio seleccionando hello **WadExample** proyecto Hola, a continuación, el Explorador de soluciones **publicar** de hello **generar** menú.
2. Elija su suscripción.
3. Hola **configuración de publicación de Microsoft Azure** cuadro de diálogo, seleccione **crear nuevo...** .
4. Hola **crear servicio en la nube y cuenta de almacenamiento** cuadro de diálogo, escriba un **nombre** (por ejemplo, "WadExample") y seleccione una región o un grupo de afinidad.
5. Conjunto hello **entorno** demasiado**ensayo**.
6. Modifique cualquier otro parámetro de **Configuración** según sea necesario y haga clic en **Publicar**.
7. Una vez finalizada la implementación, compruebe en hello portal de Azure que el servicio de nube está en un **ejecutando** estado.

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a>Paso 4: Crear el archivo de configuración de diagnóstico e instalar extensión de Hola
1. Descargar definición de esquema de archivo de configuración pública de hello ejecutando el siguiente comando de PowerShell de hello:

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. Agregar una tooyour de archivo XML **WorkerRole1** proyecto con el botón secundario en hello **WorkerRole1** de proyecto y seleccione **agregar** -> **nuevo elemento...** -> **Elementos de Visual C#** -> **Datos** -> **Archivo XML**. Nombre de archivo hello "WadExample.xml".

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. Asociar el archivo de configuración de Hola Hola WadConfig.xsd. Asegúrese de que la ventana del editor de hello WadExample.xml es la ventana activa de Hola. Presione **F4** tooopen hello **propiedades** ventana. Haga clic en hello **esquemas** propiedad Hola **propiedades** ventana. Haga clic en hello **...** Hola **esquemas** propiedad. Haga clic en hello **agregar...** botón y navegar por la ubicación de toohello donde guardó archivo XSD de Hola y Hola Seleccione archivo WadConfig.xsd. Haga clic en **Aceptar**.

4. Reemplace el contenido de Hola Hola WadExample.xml del archivo de configuración con hello continuación de XML y guarde el archivo hello. Este archivo de configuración define un par toocollect de contadores de rendimiento: uno para el uso de CPU y otro para el uso de memoria. A continuación, la configuración de hello define cuatro eventos de hello correspondientes métodos toohello Hola SampleEventSourceWriter clase.

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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a>Paso 5: instalar Diagnósticos en roles de trabajo
Hello cmdlets de PowerShell para administrar los diagnósticos en un rol web o de trabajo son: AzureServiceDiagnosticsExtension Set y Get-AzureServiceDiagnosticsExtension, Remove-AzureServiceDiagnosticsExtension.

1. Abra Azure PowerShell.
2. Hola script tooinstall diagnóstico se ejecuta en el rol de trabajo (reemplace *StorageAccountKey* con clave de cuenta de almacenamiento de hello para la cuenta de almacenamiento de wadexample y *config_path* con ruta de acceso de Hola toohello *WadExample.xml* archivo):

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a>Paso 6: consultar los datos de telemetría
En Visual Studio hello **Explorador de servidores**, navegar por la cuenta de almacenamiento de toohello wadexample. Después de servicio en la nube Hola se ha estado ejecutando unos minutos cinco (5), debería ver las tablas de hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** y **WADSetOtherTable**. Haga doble clic en uno de telemetría de Hola de tooview de tablas de Hola que se han recopilado.

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a>Esquema del archivo de configuración
archivo de configuración de diagnósticos de Hello define valores que son valores de configuración de diagnóstico de tooinitialize usado cuando se inicia el agente de diagnóstico de Hola. Vea hello [referencia de esquema más reciente](https://msdn.microsoft.com/library/azure/mt634524.aspx) para los valores válidos y ejemplos.

## <a name="troubleshooting"></a>Solución de problemas
Si tiene problemas, consulte [Solución de problemas de Diagnósticos de Azure](../azure-diagnostics-troubleshooting.md) para obtener ayuda relacionada con problemas comunes.

## <a name="next-steps"></a>Pasos siguientes
[Ver una lista de relacionados artículos de diagnóstico de máquina virtual Azure](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) datos de hello toochange va a recopilar, solucionar problemas o para obtener más información sobre diagnósticos en general.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
