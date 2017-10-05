---
title: "Creación de un módulo de Azure IoT Edge con C# | Microsoft Docs"
description: "Este tutorial muestra cómo escribir un módulo convertidor de datos BLE usando los paquetes de NuGet de Azure Iot Edge más recientes, Visual Studio Code y C#."
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
ms.openlocfilehash: 7175ffc8de2c043593d61143b402484d33e4a8cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="e88b7-104">Creación de un módulo de Azure IoT Edge con C&#x23;</span><span class="sxs-lookup"><span data-stu-id="e88b7-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="e88b7-105">Este tutorial muestra cómo crear un módulo para `Azure IoT Edge` con `Visual Studio Code` y `C#`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-105">This tutorial showcases how to create a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="e88b7-106">En este tutorial, se tratará la configuración del entorno y cómo escribir un módulo convertidor de datos [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) usando la versión más reciente de los paquetes `Azure IoT Edge NuGet`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-106">In this tutorial, we walk through environment set-up and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="e88b7-107">Este tutorial utiliza el `.NET Core SDK`, que admite la compatibilidad multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="e88b7-107">This tutorial is using the `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="e88b7-108">El tutorial siguiente se escribe utilizando el sistema operativo `Windows 10`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-108">The following tutorial is written using the `Windows 10` operating system.</span></span> <span data-ttu-id="e88b7-109">Algunos de los comandos en este tutorial pueden ser diferentes en función de su `development environment`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-109">Some of the commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e88b7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e88b7-110">Prerequisites</span></span>

<span data-ttu-id="e88b7-111">En esta sección, se configura el entorno para el desarrollo de un módulo de `Azure IoT Edge`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="e88b7-112">Se aplica a los sistemas operativos **Windows de 64 bits** y **Linux de 64 bits (Ubuntu y Debian 8)**.</span><span class="sxs-lookup"><span data-stu-id="e88b7-112">It applies to both **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="e88b7-113">Se requiere el software siguiente:</span><span class="sxs-lookup"><span data-stu-id="e88b7-113">The following software is required:</span></span>

- [<span data-ttu-id="e88b7-114">Cliente de GIT</span><span class="sxs-lookup"><span data-stu-id="e88b7-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="e88b7-115">SDK de .NET Core</span><span class="sxs-lookup"><span data-stu-id="e88b7-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="e88b7-116">código de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e88b7-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="e88b7-117">No es necesario clonar el repositorio para este ejemplo, sin embargo, todo el código de ejemplo que se utiliza en este tutorial se encuentra en el repositorio siguiente:</span><span class="sxs-lookup"><span data-stu-id="e88b7-117">You do not need to clone the repo for this sample, however all of the sample code discussed in this tutorial is located in the following repository:</span></span>

- <span data-ttu-id="e88b7-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="e88b7-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="e88b7-119">Getting started</span></span>

1. <span data-ttu-id="e88b7-120">Instalar `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="e88b7-121">Instalar `Visual Studio Code` y `C# extension` desde Visual Studio Code Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e88b7-121">Install `Visual Studio Code` and the `C# extension` from the Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="e88b7-122">Vea este [vídeo tutorial rápido](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) acerca de cómo empezar a usar `Visual Studio Code` y `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how to get started using `Visual Studio Code` and the `.NET Core SDK`.</span></span>

## <a name="creating-the-azure-iot-edge-converter-module"></a><span data-ttu-id="e88b7-123">Creación de un módulo convertidor de Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="e88b7-123">Creating the Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="e88b7-124">Inicializar un nuevo proyecto de biblioteca de clase de C# `.NET Core`:</span><span class="sxs-lookup"><span data-stu-id="e88b7-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="e88b7-125">Abra una ventana de símbolo del sistema (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="e88b7-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="e88b7-126">Navegue hasta la carpeta donde desea crear el proyecto `C#`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-126">Navigate to the folder where you'd like to create the `C#` project.</span></span>
    - <span data-ttu-id="e88b7-127">Escriba **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="e88b7-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="e88b7-128">Este comando crea una clase vacía denominada `Class1.cs` en el directorio de proyectos.</span><span class="sxs-lookup"><span data-stu-id="e88b7-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="e88b7-129">Navegue hasta la carpeta donde se acaba de crear el proyecto de biblioteca de clases escribiendo **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="e88b7-129">Navigate to the folder where we just created the class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="e88b7-130">Abra el proyecto en `Visual Studio Code` escribiendo **code .**.</span><span class="sxs-lookup"><span data-stu-id="e88b7-130">Open the project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="e88b7-131">Una vez se abre el proyecto en `Visual Studio Code`, haga clic en **IoTEdgeConverterModule.csproj** para abrir el archivo como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="e88b7-131">Once the project is opened in `Visual Studio Code`, click on the **IoTEdgeConverterModule.csproj** to open the file as shown in the following image:</span></span>

    ![Ventana de edición de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="e88b7-133">Inserte el blob `XML` que se muestra en el siguiente fragmento de código entre la etiqueta de cierre de `PropertyGroup` y la etiqueta de cierre de `Project`; la línea seis en la imagen anterior y guarde el archivo presionando `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-133">Insert the `XML` blob shown in the following code snippet between the closing `PropertyGroup` tag and the closing `Project` tag; line six in the preceding image and save the file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="e88b7-134">Una vez guardado el archivo `.csproj`, `Visual Studio Code` debe solicitarle mediante un cuadro de diálogo `unresolved dependencies` tal como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="e88b7-134">Once you save the `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in the following image:</span></span> 

    ![Cuadro de diálogo de restauración de dependencias de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="e88b7-136">a) Haga clic en `Restore` para restaurar todas las referencias en el archivo del proyecto `.csproj` incluida la recién agregada `PackageReferences`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-136">a) Click `Restore` to restore all of the references in the projects `.csproj` file including the `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="e88b7-137">b) `Visual Studio Code` crea automáticamente el archivo `project.assets.json` en la carpeta `obj` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="e88b7-137">b) `Visual Studio Code` automatically creates the `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="e88b7-138">Este archivo contiene información sobre las dependencias del proyecto para agilizar las restauraciones posteriores.</span><span class="sxs-lookup"><span data-stu-id="e88b7-138">This file contains information about your project's dependencies to make subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="e88b7-139">`.NET Core Tools` ahora, están basadas en MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e88b7-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="e88b7-140">Lo que significa que se crea un archivo de proyecto `.csproj` en lugar de un `project.json`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="e88b7-141">Si `Visual Studio Code` no le solicita su confirmación, puede hacerse manualmente.</span><span class="sxs-lookup"><span data-stu-id="e88b7-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="e88b7-142">Abra la ventana de terminal integrada de `Visual Studio Code` presionando `Ctrl`  +  `backtick` o mediante los menús `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-142">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="e88b7-143">En la ventana `Integrated Terminal`, escriba **dotnet restore**.</span><span class="sxs-lookup"><span data-stu-id="e88b7-143">In the `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="e88b7-144">Cambie el nombre del archivo `Class1.cs` a `BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-144">Rename the `Class1.cs` file to `BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="e88b7-145">a) Para cambiar el nombre del archivo haga clic en el archivo y, a continuación, presione la tecla `F2`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-145">a) To rename the file first click on the file then press the `F2` key.</span></span>
    
    <span data-ttu-id="e88b7-146">b) Escriba el nuevo nombre **BleConverterModule**, tal como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="e88b7-146">b) Type in the new name **BleConverterModule**, as seen in the following image:</span></span>

    ![Cambio de nombre de una clase en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="e88b7-148">Reemplace el código existente en el archivo `BleConverterModule.cs` copiando y pegando el siguiente fragmento de código en su archivo `BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-148">Replace the existing code in the `BleConverterModule.cs` file by copying and pasting the following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="e88b7-149">Guarde el archivo presionando `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-149">Save the file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="e88b7-150">Cree un nuevo archivo denominado `Untitled-1` presionando las teclas `Ctrl`  +  `N` tal como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="e88b7-150">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys as seen in the following image:</span></span>

    ![Nuevo archivo en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="e88b7-152">Para deserializar el objeto `JSON` que se recibe desde el dispositivo simulado `BLE`, copie el código siguiente en la ventana del editor de código del archivo `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-152">To deserialize the `JSON` object that we receive from the simulated `BLE` device, copy the following code into the `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="e88b7-153">Guarde el archivo como `BleData.cs` presionando las teclas `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-153">Save the file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="e88b7-154">En el cuadro de diálogo Guardar como, en el menú desplegable `Save as Type`, seleccione `C# (*.cs;*.csx)` tal como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="e88b7-154">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in the following image:</span></span>

    ![Cuadro de diálogo Guardar como de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="e88b7-156">Cree un nuevo archivo denominado `Untitled-1` presionando las teclas `Ctrl`  +  `N`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-156">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="e88b7-157">Copie y pegue el siguiente fragmento de código en el archivo `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-157">Copy and paste the following code snippet into the `Untitled-1` file.</span></span> <span data-ttu-id="e88b7-158">Esta clase es un módulo de `Azure IoT Edge` que se utiliza para dar salida a los datos recibidos desde `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-158">This class is a `Azure IoT Edge` module, which we use to output the data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="e88b7-159">Guarde el archivo como `DotNetPrinterModule.cs` presionando `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-159">Save the file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="e88b7-160">En el cuadro de diálogo Guardar como, en el menú desplegable `Save as Type`, seleccione `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-160">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="e88b7-161">Cree un nuevo archivo denominado `Untitled-1` presionando las teclas `Ctrl`  +  `N`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-161">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="e88b7-162">Para deserializar el objeto `JSON` que se recibe desde el módulo `BleConverterModule`, copie y pegue el siguiente fragmento de código en el archivo `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-162">To deserialize the `JSON` object that we receive from the `BleConverterModule`, Copy and paste the following code snippet into the `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="e88b7-163">Guarde el archivo como `BleConverterData.cs` presionando `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-163">Save the file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="e88b7-164">En el cuadro de diálogo Guardar como, en el menú desplegable `Save as Type`, seleccione `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-164">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="e88b7-165">Cree un nuevo archivo denominado `Untitled-1` presionando las teclas `Ctrl`  +  `N`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-165">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="e88b7-166">Copie y pegue el siguiente fragmento de código en el archivo `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-166">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="e88b7-167">Guarde el archivo como `gw-config.json` presionando `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-167">Save the file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="e88b7-168">En el cuadro de diálogo Guardar como, en el menú desplegable `Save as Type`, seleccione `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-168">On the save as dialog box, in the `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="e88b7-169">Para habilitar la copia del archivo de configuración en el directorio de salida, actualice `IoTEdgeConverterModule.csproj` con el objeto blob XML siguiente:</span><span class="sxs-lookup"><span data-stu-id="e88b7-169">To enable copying of the configuration file to the output directory, update the `IoTEdgeConverterModule.csproj` with the following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="e88b7-170">El archivo `IoTEdgeConverterModule.csproj` actualizado debería ser similar a la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="e88b7-170">The updated `IoTEdgeConverterModule.csproj` should look like the following image:</span></span>

    ![Archivo .csproj actualizado en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="e88b7-172">Cree un nuevo archivo denominado `Untitled-1` presionando las teclas `Ctrl`  +  `N`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-172">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="e88b7-173">Copie y pegue el siguiente fragmento de código en el archivo `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-173">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="e88b7-174">Guarde el archivo como `binplace.ps1` presionando `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-174">Save the file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="e88b7-175">En el cuadro de diálogo Guardar como, en el menú desplegable `Save as Type`, seleccione `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-175">On the save as dialog box, in the `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="e88b7-176">Compile el proyecto presionando las teclas `Ctrl` + `Shift` + `B`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-176">Build the project by pressing the `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="e88b7-177">Al compilar el proyecto por primera vez, `Visual Studio Code` muestra un cuadro de diálogo `No build task defined.` tal como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="e88b7-177">When you build the project for the first time, `Visual Studio Code` prompts you with the `No build task defined.` dialog as seen in the following image:</span></span>

    ![Cuadro de diálogo Tarea de compilación de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="e88b7-179">a) Haga clic en el botón `Configure Build Task`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-179">a) Click the `Configure Build Task` button.</span></span>

    <span data-ttu-id="e88b7-180">b) En el menú desplegable del cuadro de diálogo `Select a Task Runner`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-180">b) In the `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="e88b7-181">Seleccione `.NET Core` tal como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="e88b7-181">Select `.NET Core` as seen in the following image:</span></span> 

    ![Cuadro de diálogo seleccionar una tarea de Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="e88b7-183">c) Si hace clic en el elemento `.NET Core`, se crea el archivo `tasks.json` en el directorio `.vscode` y se abre el archivo en la ventana `code editor`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-183">c) Clicking the `.NET Core` item creates the `tasks.json` file in your `.vscode` directory and opens the file in the `code editor` window.</span></span> <span data-ttu-id="e88b7-184">No es necesario modificar este archivo, puede cerrar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="e88b7-184">There is no need to modify this file, close the tab.</span></span>

27.  <span data-ttu-id="e88b7-185">Abra la ventana de terminal integrada de `Visual Studio Code` presionando las teclas `Ctrl`  +  `backtick` o mediante los menús `View`  ->  `Integrated Terminal` y escriba **.\binplace.ps1** en el símbolo del sistema de `PowerShell`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-185">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into the `PowerShell` command prompt.</span></span> <span data-ttu-id="e88b7-186">Este comando copia todas las dependencias en el directorio de salida.</span><span class="sxs-lookup"><span data-stu-id="e88b7-186">This command copies all our dependencies to the output directory.</span></span>

28. <span data-ttu-id="e88b7-187">Navegue hasta el directorio de salida del proyecto en la ventana `Integrated Terminal` escribiendo **cd .\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="e88b7-187">Navigate to the projects output directory in the `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="e88b7-188">Ejecute el proyecto de ejemplo escribiendo **. \gw.exe gw-config.json** en la ventana `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-188">Run the sample project by typing **.\gw.exe gw-config.json** into the `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="e88b7-189">Si ha seguido todos los pasos de este tutorial, ahora debe tener en ejecución el proyecto de ejemplo `Azure IoT Edge BLE Data Converter Module` tal como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="e88b7-189">If you have followed the steps in this tutorial closely, you should now be running the `Azure IoT Edge BLE Data Converter Module` sample project as seen in the following image:</span></span>
    
        ![Ejemplo de dispositivo simulado en ejecución en Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="e88b7-191">Si desea finalizar la aplicación, presione la tecla `<Enter>`.</span><span class="sxs-lookup"><span data-stu-id="e88b7-191">If you want to terminate the application, press the `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="e88b7-192">No se recomienda usar `Ctrl`  +  `C` para terminar la aplicación de puerta de enlace de `IoT Edge` (es decir, **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="e88b7-192">It is not recommended to use `Ctrl` + `C` to terminate the `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="e88b7-193">Esta acción puede hacer que el proceso finalice de forma anómala.</span><span class="sxs-lookup"><span data-stu-id="e88b7-193">As this action may cause the process to terminate abnormally.</span></span>

