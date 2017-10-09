---
title: "un módulo de borde de IoT de Azure con C# aaaCreate | Documentos de Microsoft"
description: "Este tutorial muestra cómo toowrite una Bilitar datos convertidor módulo mediante Hola más recientes paquetes de NuGet de borde de IoT de Azure, código de Visual Studio y C#."
services: iot-hub
author: jeffreyCline
manager: timlt
keywords: "azure, iot, tutorial, módulo, nuget, vscode, csharp, edge"
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: jcline
ms.openlocfilehash: b104609c05d1613e21acc7d7bed547f311179151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a>Creación de un módulo de Azure IoT Edge con C&#x23;

Este tutorial muestra cómo toocreate un módulo para `Azure IoT Edge` con `Visual Studio Code` y `C#`.

En este tutorial, recorreremos instalación de entorno y cómo toowrite una [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) datos convertidor módulo mediante Hola más reciente `Azure IoT Edge NuGet` paquetes. 

>[!NOTE]
Este tutorial usa hello `.NET Core SDK`, que admite la compatibilidad multiplataforma. Hello tutorial siguiente se escribe utilizando hello `Windows 10` sistema operativo. Algunos de los comandos de hello en este tutorial pueden ser diferente en función de su `development environment`. 

## <a name="prerequisites"></a>Requisitos previos

En esta sección, se configura el entorno para el desarrollo de un módulo de `Azure IoT Edge`. Se aplica tooboth **Windows de 64 bits** y **Linux de 64 bits (8 Debian y Ubuntu)** sistemas operativos.

Hola siguiente software es necesario:

- [Cliente de GIT](https://git-scm.com/downloads)
- [SDK de .NET Core](https://www.microsoft.com/net/core#windowscmd)
- [código de Visual Studio](https://code.visualstudio.com/)

No es necesario el repositorio de hello tooclone para este ejemplo, sin embargo todos Hola se utilizan en este tutorial de código de ejemplo se encuentra en hello después de repositorio:

- `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a>Introducción

1. Instalar `.NET Core SDK`.
2. Instalar `Visual Studio Code` hello y `C# extension` de hello Marketplace de código de Visual Studio.

Ver esto [vídeo tutorial rápido](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) acerca de cómo tooget a usar `Visual Studio Code` hello y `.NET Core SDK`.

## <a name="creating-hello-azure-iot-edge-converter-module"></a>Crear módulo de convertidor de hello borde de IoT de Azure

1. Inicializar un nuevo proyecto de biblioteca de clase de C# `.NET Core`:
    - Abra una ventana de símbolo del sistema (`Windows + R` -> `cmd` -> `enter`).
    - Desplazarse por las carpetas de toohello dónde se desea hello toocreate `C#` proyecto.
    - Escriba **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**. 
    - Este comando crea una clase vacía denominada `Class1.cs` en el directorio de proyectos.
2. Desplazarse por las carpetas de toohello donde se acaba de crear el proyecto de biblioteca de clases de hello escribiendo **cd IoTEdgeConverterModule**.
3. Proyecto abierto hello en `Visual Studio Code` escribiendo **código.**.
4. Una vez que se abre el proyecto de hello en `Visual Studio Code`, haga clic en hello **IoTEdgeConverterModule.csproj** tooopen archivo de hello como se muestra en hello después de imagen:

    ![Ventana de edición de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. Insertar hello `XML` blob se muestra en hello siguiente fragmento de código entre cierre hello `PropertyGroup` etiquetar y Hola cerrar `Project` etiqueta; línea seis de hello anterior imagen y guarde el archivo de hello presionando `Ctrl`  +  `S`.

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. Una vez que guarde hello `.csproj` archivo `Visual Studio Code` debe solicitarle que con un `unresolved dependencies` tal como se muestra en hello después de la imagen del cuadro de diálogo: 

    ![Cuadro de diálogo de restauración de dependencias de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    un) haga clic en `Restore` toorestore todas las de hello referencias en proyectos de hello `.csproj` archivo incluido hello `PackageReferences` hemos agregado. 

    b) `Visual Studio Code` crea automáticamente hello `project.assets.json` archivo en los proyectos `obj` carpeta. Este archivo contiene información acerca dependencias toomake posteriores restauraciones de su proyecto más rápidas.
 
    >[!NOTE]
    `.NET Core Tools` ahora, están basadas en MSBuild. Lo que significa que se crea un archivo de proyecto `.csproj` en lugar de un `project.json`.

    - Si `Visual Studio Code` no le solicita su confirmación, puede hacerse manualmente. Hola abierto `Visual Studio Code` ventana de terminal integrado por hello presionando `Ctrl`  +  `backtick` claves o mediante los menús de hello `View`  ->  `Integrated Terminal`.
    - Hola `Integrated Terminal` tipo de ventana **dotnet restauración**.
    
7. Cambiar el nombre de hello `Class1.cs` archivo demasiado`BleConverterModule.cs`. 

    ) archivo de hello toorename primero haga clic en el archivo hello y presione hello `F2` clave.
    
    b) tipo en un nuevo nombre hello **BleConverterModule**, tal como se muestra en hello después de imagen:

    ![Cambio de nombre de una clase en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. Reemplazar el código existente de Hola Hola `BleConverterModule.cs` archivo copiando y Hola pegado siguiente fragmento de código en su `BleConverterModule.cs` archivo.

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Globalization;
   using System.Linq;
   using System.Text;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace IoTEdgeConverterModule
   {
       public class BleConverterModule : IGatewayModule, IGatewayModuleStart
       {
           private Broker broker;
           private string configuration;
           private int messageCount;

           public void Create(Broker broker, byte[] configuration)
           {
               this.broker = broker;
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Start()
           {
           }

           public void Destroy()
           {
           }

           public void Receive(Message received_message)
           {
               string recMsg = Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               BleData receivedData = JsonConvert.DeserializeObject<BleData>(recMsg);

               float temperature = float.Parse(receivedData.Temperature, CultureInfo.InvariantCulture.NumberFormat); 
               Dictionary<string, string> receivedProperties = received_message.Properties;
            
               Dictionary<string, string> properties = new Dictionary<string, string>();
               properties.Add("source", receivedProperties["source"]);
               properties.Add("macAddress", receivedProperties["macAddress"]);
               properties.Add("temperatureAlert", temperature > 30 ? "true" : "false");
   
               String content = String.Format("{0} \"deviceId\": \"Intel NUC Gateway\", \"messageId\": {1}, \"temperature\": {2} {3}", "{", ++this.messageCount, temperature, "}");
               Message messageToPublish = new Message(content, properties);
   
               this.broker.Publish(messageToPublish);
           }
       }
   }
   ```

9. Guardar archivo hello presionando `Ctrl`  +  `S`.

10. Crear un nuevo archivo denominado `Untitled-1` por hello presionando `Ctrl`  +  `N` claves tal como se muestra en hello después de imagen:

    ![Nuevo archivo en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. Hola toodeserialize `JSON` objeto que se recibe de hello simulado `BLE` dispositivo, Hola copia sigue código en hello `Untitled-1` ventana del editor de código de archivo. 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace IoTEdgeConverterModule
   {
       public class BleData
       {
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

12. Guardar archivo de hello como `BleData.cs` presionando `Ctrl`  +  `Shift`  +  `S` claves.
    - En hello Guardar como cuadro de diálogo hello `Save as Type` menú desplegable, seleccione `C# (*.cs;*.csx)` tal como se muestra en hello después de imagen:

    ![Cuadro de diálogo Guardar como de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. Crear un nuevo archivo denominado `Untitled-1` por hello presionando `Ctrl`  +  `N` claves.

14. Copie y pegue Hola siguiente fragmento de código en hello `Untitled-1` archivo. Esta clase es un `Azure IoT Edge` módulo, que se utilizan los datos de hello toooutput recibidos de nuestros `BleConverterModule`.

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace PrinterModule
   {
       public class DotNetPrinterModule : IGatewayModule
       {
           private string configuration;
           public void Create(Broker broker, byte[] configuration)
           {
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Destroy()
           {
           }
   
           public void Receive(Message received_message)
           {
               string recMsg = System.Text.Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               Dictionary<string, string> receivedProperties = received_message.Properties;
               
               BleConverterData receivedData = JsonConvert.DeserializeObject<BleConverterData>(recMsg);
   
               Console.WriteLine();
               Console.WriteLine("Module           : [DotNetPrinterModule]");
               Console.WriteLine("received_message : {0}", recMsg);
   
               if(received_message.Properties["source"] == "bleTelemetry")
               {
                   Console.WriteLine("Source           : {0}", receivedProperties["source"]);
                   Console.WriteLine("MAC address      : {0}", receivedProperties["macAddress"]);
                   Console.WriteLine("Temperature Alert: {0}", receivedProperties["temperatureAlert"]);
                   Console.WriteLine("Deserialized Obj : [BleConverterData]");
                   Console.WriteLine("  DeviceId       : {0}", receivedData.DeviceId);
                   Console.WriteLine("  MessageId      : {0}", receivedData.MessageId);
                   Console.WriteLine("  Temperature    : {0}", receivedData.Temperature);
               }
   
               Console.WriteLine();
           }
       }
   }
   ```

15. Guardar archivo de hello como `DotNetPrinterModule.cs` presionando `Ctrl`  +  `Shift`  +  `S`.
    - En hello Guardar como cuadro de diálogo hello `Save as Type` menú desplegable, seleccione `C# (*.cs;*.csx)`.

16. Crear un nuevo archivo denominado `Untitled-1` por hello presionando `Ctrl`  +  `N` claves.

17. Hola toodeserialize `JSON` objeto que se recibe de hello `BleConverterModule`, copiar y pegar siguiente de hello fragmento de código en hello `Untitled-1` archivo. 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace PrinterModule
   {
       public class BleConverterData
       {
           [JsonProperty(PropertyName = "deviceId")]
           public string DeviceId { get; set; }
   
           [JsonProperty(PropertyName = "messageId")]
           public string MessageId { get; set; }
   
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

18. Guardar archivo de hello como `BleConverterData.cs` presionando `Ctrl`  +  `Shift`  +  `S`.
    - En hello Guardar como cuadro de diálogo hello `Save as Type` menú desplegable, seleccione `C# (*.cs;*.csx)`.

19. Crear un nuevo archivo denominado `Untitled-1` por hello presionando `Ctrl`  +  `N` claves.

20. Copie y pegue Hola siguiente fragmento de código en hello `Untitled-1` archivo.

   ```json
   {
       "loaders": [
           {
               "type": "dotnetcore",
               "name": "dotnetcore",
               "configuration": {
                   "binding.path": "dotnetcore.dll",
                   "binding.coreclrpath": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\coreclr.dll",
                   "binding.trustedplatformassemblieslocation": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\"
               }
           }
       ],
          "modules": [
           {
               "name": "simulated_device",
               "loader": {
                   "name": "native",
                   "entrypoint": {
                       "module.path": "simulated_device.dll"
                   }
               },
               "args": {
                   "macAddress": "01:02:03:03:02:01",
                   "messagePeriod": 500
               }
           },
           {
               "name": "ble_converter_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "IoTEdgeConverterModule.BleConverterModule"
                   }
               },
               "args": ""
           },
           {
               "name": "printer_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "PrinterModule.DotNetPrinterModule"
                   }
               },
               "args": ""
           }
       ],
       "links": [
           {
               "source": "simulated_device", "sink": "ble_converter_module"
           },
           {
               "source": "ble_converter_module", "sink": "printer_module"
           }
   ]
   }
   ```

21. Guardar archivo de hello como `gw-config.json` presionando `Ctrl`  +  `Shift`  +  `S`.
    - En hello Guardar como cuadro de diálogo hello `Save as Type` menú desplegable, seleccione `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.

22. Copiar tooenable de toohello de archivo de configuración de hello directorio, Hola de actualización de resultados `IoTEdgeConverterModule.csproj` con hello después blob XML:

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - Hola actualiza `IoTEdgeConverterModule.csproj` debe Hola tenga el aspecto siguiente imagen:

    ![Archivo .csproj actualizado en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. Crear un nuevo archivo denominado `Untitled-1` por hello presionando `Ctrl`  +  `N` claves.

24. Copie y pegue Hola siguiente fragmento de código en hello `Untitled-1` archivo.

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. Guardar archivo de hello como `binplace.ps1` presionando `Ctrl`  +  `Shift`  +  `S`.
    - En hello Guardar como cuadro de diálogo hello `Save as Type` menú desplegable, seleccione `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.

26. Compilar el proyecto de Hola Hola presionando `Ctrl`  +  `Shift`  +  `B` claves. Al compilar el proyecto de Hola para hello primera vez, `Visual Studio Code` le pide que con hello `No build task defined.` tal como se muestra en hello después de la imagen del cuadro de diálogo:

    ![Cuadro de diálogo Tarea de compilación de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    un) haga clic en hello `Configure Build Task` botón.

    b) en hello `Select a Task Runner` menú desplegable del cuadro de diálogo. Seleccione `.NET Core` tal como se muestra en hello después de imagen: 

    ![Cuadro de diálogo seleccionar una tarea de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    Hola de c) si hace clic en `.NET Core` elemento crea hello `tasks.json` un archivo en su `.vscode` directorio del sistema y abre Hola archivo Hola `code editor` ventana. Este archivo, ficha Hola cerrar no hay ninguna necesidad de toomodify.

27.  Hola abierto `Visual Studio Code` ventana de terminal integrado por hello presionando `Ctrl`  +  `backtick` claves o mediante los menús de hello `View`  ->  `Integrated Terminal` y el tipo de **.\binplace.ps1**en hello `PowerShell` símbolo del sistema. Este comando copia nuestro de directorio de salida toohello de dependencias.

28. Navegar por el directorio de salida de proyectos de toohello Hola `Integrated Terminal` ventana escribiendo **.\bin\Debug\netstandard1.3 cd**.

29. Ejecutar el proyecto de ejemplo de Hola escribiendo **. \gw.exe gw-config.json** en hello `Integrated Terminal` indicador de la ventana. 
    - Si ha seguido los pasos de hello estrechamente en este tutorial, deberá ahora ejecutar hello `Azure IoT Edge BLE Data Converter Module` proyecto de ejemplo como se muestra en hello después de imagen:
    
        ![Ejemplo de dispositivo simulado en ejecución en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - Si desea que la aplicación de hello tooterminate, presione hello `<Enter>` clave.

>[!IMPORTANT]
No se recomienda toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` aplicación de puerta de enlace (es decir, **gw.exe**). Como esta acción puede provocar Hola proceso tooterminate de forma anómala.

