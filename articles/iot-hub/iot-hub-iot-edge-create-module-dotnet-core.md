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
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="78a5b-104">Creación de un módulo de Azure IoT Edge con C&#x23;</span><span class="sxs-lookup"><span data-stu-id="78a5b-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="78a5b-105">Este tutorial muestra cómo toocreate un módulo para `Azure IoT Edge` con `Visual Studio Code` y `C#`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-105">This tutorial showcases how toocreate a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="78a5b-106">En este tutorial, recorreremos instalación de entorno y cómo toowrite una [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) datos convertidor módulo mediante Hola más reciente `Azure IoT Edge NuGet` paquetes.</span><span class="sxs-lookup"><span data-stu-id="78a5b-106">In this tutorial, we walk through environment set-up and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="78a5b-107">Este tutorial usa hello `.NET Core SDK`, que admite la compatibilidad multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="78a5b-107">This tutorial is using hello `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="78a5b-108">Hello tutorial siguiente se escribe utilizando hello `Windows 10` sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="78a5b-108">hello following tutorial is written using hello `Windows 10` operating system.</span></span> <span data-ttu-id="78a5b-109">Algunos de los comandos de hello en este tutorial pueden ser diferente en función de su `development environment`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-109">Some of hello commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="78a5b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="78a5b-110">Prerequisites</span></span>

<span data-ttu-id="78a5b-111">En esta sección, se configura el entorno para el desarrollo de un módulo de `Azure IoT Edge`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="78a5b-112">Se aplica tooboth **Windows de 64 bits** y **Linux de 64 bits (8 Debian y Ubuntu)** sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="78a5b-112">It applies tooboth **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="78a5b-113">Hola siguiente software es necesario:</span><span class="sxs-lookup"><span data-stu-id="78a5b-113">hello following software is required:</span></span>

- [<span data-ttu-id="78a5b-114">Cliente de GIT</span><span class="sxs-lookup"><span data-stu-id="78a5b-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="78a5b-115">SDK de .NET Core</span><span class="sxs-lookup"><span data-stu-id="78a5b-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="78a5b-116">código de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="78a5b-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="78a5b-117">No es necesario el repositorio de hello tooclone para este ejemplo, sin embargo todos Hola se utilizan en este tutorial de código de ejemplo se encuentra en hello después de repositorio:</span><span class="sxs-lookup"><span data-stu-id="78a5b-117">You do not need tooclone hello repo for this sample, however all of hello sample code discussed in this tutorial is located in hello following repository:</span></span>

- <span data-ttu-id="78a5b-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="78a5b-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="78a5b-119">Getting started</span></span>

1. <span data-ttu-id="78a5b-120">Instalar `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="78a5b-121">Instalar `Visual Studio Code` hello y `C# extension` de hello Marketplace de código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="78a5b-121">Install `Visual Studio Code` and hello `C# extension` from hello Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="78a5b-122">Ver esto [vídeo tutorial rápido](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) acerca de cómo tooget a usar `Visual Studio Code` hello y `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how tooget started using `Visual Studio Code` and hello `.NET Core SDK`.</span></span>

## <a name="creating-hello-azure-iot-edge-converter-module"></a><span data-ttu-id="78a5b-123">Crear módulo de convertidor de hello borde de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="78a5b-123">Creating hello Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="78a5b-124">Inicializar un nuevo proyecto de biblioteca de clase de C# `.NET Core`:</span><span class="sxs-lookup"><span data-stu-id="78a5b-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="78a5b-125">Abra una ventana de símbolo del sistema (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="78a5b-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="78a5b-126">Desplazarse por las carpetas de toohello dónde se desea hello toocreate `C#` proyecto.</span><span class="sxs-lookup"><span data-stu-id="78a5b-126">Navigate toohello folder where you'd like toocreate hello `C#` project.</span></span>
    - <span data-ttu-id="78a5b-127">Escriba **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="78a5b-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="78a5b-128">Este comando crea una clase vacía denominada `Class1.cs` en el directorio de proyectos.</span><span class="sxs-lookup"><span data-stu-id="78a5b-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="78a5b-129">Desplazarse por las carpetas de toohello donde se acaba de crear el proyecto de biblioteca de clases de hello escribiendo **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="78a5b-129">Navigate toohello folder where we just created hello class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="78a5b-130">Proyecto abierto hello en `Visual Studio Code` escribiendo **código.**.</span><span class="sxs-lookup"><span data-stu-id="78a5b-130">Open hello project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="78a5b-131">Una vez que se abre el proyecto de hello en `Visual Studio Code`, haga clic en hello **IoTEdgeConverterModule.csproj** tooopen archivo de hello como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="78a5b-131">Once hello project is opened in `Visual Studio Code`, click on hello **IoTEdgeConverterModule.csproj** tooopen hello file as shown in hello following image:</span></span>

    ![Ventana de edición de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="78a5b-133">Insertar hello `XML` blob se muestra en hello siguiente fragmento de código entre cierre hello `PropertyGroup` etiquetar y Hola cerrar `Project` etiqueta; línea seis de hello anterior imagen y guarde el archivo de hello presionando `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-133">Insert hello `XML` blob shown in hello following code snippet between hello closing `PropertyGroup` tag and hello closing `Project` tag; line six in hello preceding image and save hello file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="78a5b-134">Una vez que guarde hello `.csproj` archivo `Visual Studio Code` debe solicitarle que con un `unresolved dependencies` tal como se muestra en hello después de la imagen del cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="78a5b-134">Once you save hello `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in hello following image:</span></span> 

    ![Cuadro de diálogo de restauración de dependencias de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="78a5b-136">un) haga clic en `Restore` toorestore todas las de hello referencias en proyectos de hello `.csproj` archivo incluido hello `PackageReferences` hemos agregado.</span><span class="sxs-lookup"><span data-stu-id="78a5b-136">a) Click `Restore` toorestore all of hello references in hello projects `.csproj` file including hello `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="78a5b-137">b) `Visual Studio Code` crea automáticamente hello `project.assets.json` archivo en los proyectos `obj` carpeta.</span><span class="sxs-lookup"><span data-stu-id="78a5b-137">b) `Visual Studio Code` automatically creates hello `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="78a5b-138">Este archivo contiene información acerca dependencias toomake posteriores restauraciones de su proyecto más rápidas.</span><span class="sxs-lookup"><span data-stu-id="78a5b-138">This file contains information about your project's dependencies toomake subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="78a5b-139">`.NET Core Tools` ahora, están basadas en MSBuild.</span><span class="sxs-lookup"><span data-stu-id="78a5b-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="78a5b-140">Lo que significa que se crea un archivo de proyecto `.csproj` en lugar de un `project.json`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="78a5b-141">Si `Visual Studio Code` no le solicita su confirmación, puede hacerse manualmente.</span><span class="sxs-lookup"><span data-stu-id="78a5b-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="78a5b-142">Hola abierto `Visual Studio Code` ventana de terminal integrado por hello presionando `Ctrl`  +  `backtick` claves o mediante los menús de hello `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-142">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="78a5b-143">Hola `Integrated Terminal` tipo de ventana **dotnet restauración**.</span><span class="sxs-lookup"><span data-stu-id="78a5b-143">In hello `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="78a5b-144">Cambiar el nombre de hello `Class1.cs` archivo demasiado`BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-144">Rename hello `Class1.cs` file too`BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="78a5b-145">) archivo de hello toorename primero haga clic en el archivo hello y presione hello `F2` clave.</span><span class="sxs-lookup"><span data-stu-id="78a5b-145">a) toorename hello file first click on hello file then press hello `F2` key.</span></span>
    
    <span data-ttu-id="78a5b-146">b) tipo en un nuevo nombre hello **BleConverterModule**, tal como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="78a5b-146">b) Type in hello new name **BleConverterModule**, as seen in hello following image:</span></span>

    ![Cambio de nombre de una clase en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="78a5b-148">Reemplazar el código existente de Hola Hola `BleConverterModule.cs` archivo copiando y Hola pegado siguiente fragmento de código en su `BleConverterModule.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="78a5b-148">Replace hello existing code in hello `BleConverterModule.cs` file by copying and pasting hello following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="78a5b-149">Guardar archivo hello presionando `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-149">Save hello file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="78a5b-150">Crear un nuevo archivo denominado `Untitled-1` por hello presionando `Ctrl`  +  `N` claves tal como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="78a5b-150">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys as seen in hello following image:</span></span>

    ![Nuevo archivo en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="78a5b-152">Hola toodeserialize `JSON` objeto que se recibe de hello simulado `BLE` dispositivo, Hola copia sigue código en hello `Untitled-1` ventana del editor de código de archivo.</span><span class="sxs-lookup"><span data-stu-id="78a5b-152">toodeserialize hello `JSON` object that we receive from hello simulated `BLE` device, copy hello following code into hello `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="78a5b-153">Guardar archivo de hello como `BleData.cs` presionando `Ctrl`  +  `Shift`  +  `S` claves.</span><span class="sxs-lookup"><span data-stu-id="78a5b-153">Save hello file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="78a5b-154">En hello Guardar como cuadro de diálogo hello `Save as Type` menú desplegable, seleccione `C# (*.cs;*.csx)` tal como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="78a5b-154">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in hello following image:</span></span>

    ![Cuadro de diálogo Guardar como de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="78a5b-156">Crear un nuevo archivo denominado `Untitled-1` por hello presionando `Ctrl`  +  `N` claves.</span><span class="sxs-lookup"><span data-stu-id="78a5b-156">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="78a5b-157">Copie y pegue Hola siguiente fragmento de código en hello `Untitled-1` archivo.</span><span class="sxs-lookup"><span data-stu-id="78a5b-157">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> <span data-ttu-id="78a5b-158">Esta clase es un `Azure IoT Edge` módulo, que se utilizan los datos de hello toooutput recibidos de nuestros `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-158">This class is a `Azure IoT Edge` module, which we use toooutput hello data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="78a5b-159">Guardar archivo de hello como `DotNetPrinterModule.cs` presionando `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-159">Save hello file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="78a5b-160">En hello Guardar como cuadro de diálogo hello `Save as Type` menú desplegable, seleccione `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-160">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="78a5b-161">Crear un nuevo archivo denominado `Untitled-1` por hello presionando `Ctrl`  +  `N` claves.</span><span class="sxs-lookup"><span data-stu-id="78a5b-161">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="78a5b-162">Hola toodeserialize `JSON` objeto que se recibe de hello `BleConverterModule`, copiar y pegar siguiente de hello fragmento de código en hello `Untitled-1` archivo.</span><span class="sxs-lookup"><span data-stu-id="78a5b-162">toodeserialize hello `JSON` object that we receive from hello `BleConverterModule`, Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="78a5b-163">Guardar archivo de hello como `BleConverterData.cs` presionando `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-163">Save hello file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="78a5b-164">En hello Guardar como cuadro de diálogo hello `Save as Type` menú desplegable, seleccione `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-164">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="78a5b-165">Crear un nuevo archivo denominado `Untitled-1` por hello presionando `Ctrl`  +  `N` claves.</span><span class="sxs-lookup"><span data-stu-id="78a5b-165">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="78a5b-166">Copie y pegue Hola siguiente fragmento de código en hello `Untitled-1` archivo.</span><span class="sxs-lookup"><span data-stu-id="78a5b-166">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="78a5b-167">Guardar archivo de hello como `gw-config.json` presionando `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-167">Save hello file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="78a5b-168">En hello Guardar como cuadro de diálogo hello `Save as Type` menú desplegable, seleccione `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-168">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="78a5b-169">Copiar tooenable de toohello de archivo de configuración de hello directorio, Hola de actualización de resultados `IoTEdgeConverterModule.csproj` con hello después blob XML:</span><span class="sxs-lookup"><span data-stu-id="78a5b-169">tooenable copying of hello configuration file toohello output directory, update hello `IoTEdgeConverterModule.csproj` with hello following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="78a5b-170">Hola actualiza `IoTEdgeConverterModule.csproj` debe Hola tenga el aspecto siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="78a5b-170">hello updated `IoTEdgeConverterModule.csproj` should look like hello following image:</span></span>

    ![Archivo .csproj actualizado en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="78a5b-172">Crear un nuevo archivo denominado `Untitled-1` por hello presionando `Ctrl`  +  `N` claves.</span><span class="sxs-lookup"><span data-stu-id="78a5b-172">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="78a5b-173">Copie y pegue Hola siguiente fragmento de código en hello `Untitled-1` archivo.</span><span class="sxs-lookup"><span data-stu-id="78a5b-173">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="78a5b-174">Guardar archivo de hello como `binplace.ps1` presionando `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-174">Save hello file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="78a5b-175">En hello Guardar como cuadro de diálogo hello `Save as Type` menú desplegable, seleccione `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="78a5b-175">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="78a5b-176">Compilar el proyecto de Hola Hola presionando `Ctrl`  +  `Shift`  +  `B` claves.</span><span class="sxs-lookup"><span data-stu-id="78a5b-176">Build hello project by pressing hello `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="78a5b-177">Al compilar el proyecto de Hola para hello primera vez, `Visual Studio Code` le pide que con hello `No build task defined.` tal como se muestra en hello después de la imagen del cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="78a5b-177">When you build hello project for hello first time, `Visual Studio Code` prompts you with hello `No build task defined.` dialog as seen in hello following image:</span></span>

    ![Cuadro de diálogo Tarea de compilación de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="78a5b-179">un) haga clic en hello `Configure Build Task` botón.</span><span class="sxs-lookup"><span data-stu-id="78a5b-179">a) Click hello `Configure Build Task` button.</span></span>

    <span data-ttu-id="78a5b-180">b) en hello `Select a Task Runner` menú desplegable del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="78a5b-180">b) In hello `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="78a5b-181">Seleccione `.NET Core` tal como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="78a5b-181">Select `.NET Core` as seen in hello following image:</span></span> 

    ![Cuadro de diálogo seleccionar una tarea de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="78a5b-183">Hola de c) si hace clic en `.NET Core` elemento crea hello `tasks.json` un archivo en su `.vscode` directorio del sistema y abre Hola archivo Hola `code editor` ventana.</span><span class="sxs-lookup"><span data-stu-id="78a5b-183">c) Clicking hello `.NET Core` item creates hello `tasks.json` file in your `.vscode` directory and opens hello file in hello `code editor` window.</span></span> <span data-ttu-id="78a5b-184">Este archivo, ficha Hola cerrar no hay ninguna necesidad de toomodify.</span><span class="sxs-lookup"><span data-stu-id="78a5b-184">There is no need toomodify this file, close hello tab.</span></span>

27.  <span data-ttu-id="78a5b-185">Hola abierto `Visual Studio Code` ventana de terminal integrado por hello presionando `Ctrl`  +  `backtick` claves o mediante los menús de hello `View`  ->  `Integrated Terminal` y el tipo de **.\binplace.ps1**en hello `PowerShell` símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="78a5b-185">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into hello `PowerShell` command prompt.</span></span> <span data-ttu-id="78a5b-186">Este comando copia nuestro de directorio de salida toohello de dependencias.</span><span class="sxs-lookup"><span data-stu-id="78a5b-186">This command copies all our dependencies toohello output directory.</span></span>

28. <span data-ttu-id="78a5b-187">Navegar por el directorio de salida de proyectos de toohello Hola `Integrated Terminal` ventana escribiendo **.\bin\Debug\netstandard1.3 cd**.</span><span class="sxs-lookup"><span data-stu-id="78a5b-187">Navigate toohello projects output directory in hello `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="78a5b-188">Ejecutar el proyecto de ejemplo de Hola escribiendo **. \gw.exe gw-config.json** en hello `Integrated Terminal` indicador de la ventana.</span><span class="sxs-lookup"><span data-stu-id="78a5b-188">Run hello sample project by typing **.\gw.exe gw-config.json** into hello `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="78a5b-189">Si ha seguido los pasos de hello estrechamente en este tutorial, deberá ahora ejecutar hello `Azure IoT Edge BLE Data Converter Module` proyecto de ejemplo como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="78a5b-189">If you have followed hello steps in this tutorial closely, you should now be running hello `Azure IoT Edge BLE Data Converter Module` sample project as seen in hello following image:</span></span>
    
        ![Ejemplo de dispositivo simulado en ejecución en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="78a5b-191">Si desea que la aplicación de hello tooterminate, presione hello `<Enter>` clave.</span><span class="sxs-lookup"><span data-stu-id="78a5b-191">If you want tooterminate hello application, press hello `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="78a5b-192">No se recomienda toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` aplicación de puerta de enlace (es decir, **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="78a5b-192">It is not recommended toouse `Ctrl` + `C` tooterminate hello `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="78a5b-193">Como esta acción puede provocar Hola proceso tooterminate de forma anómala.</span><span class="sxs-lookup"><span data-stu-id="78a5b-193">As this action may cause hello process tooterminate abnormally.</span></span>

