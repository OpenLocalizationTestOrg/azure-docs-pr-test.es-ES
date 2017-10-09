---
title: "aaaUse centro de IoT de Azure dirigir métodos (nodo/.NET) | Documentos de Microsoft"
description: "¿Cómo toouse centro de IoT de Azure dirigir métodos. Usar dispositivos de IoT de Azure de hello SDK para Node.js tooimplement una aplicación de dispositivo simulado que incluye un método directo y el servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que invoca el método directo Hola Hola."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a>Uso de métodos directos (.NET y Node)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

En este tutorial, vamos a toodevelop .NET y una aplicación de consola de Node.js:

* **CallMethodOnDevice.sln**, una aplicación de back-end. NET, que llama a un método de aplicación de dispositivo simulado de hello y muestra la respuesta de Hola.
* **SimulatedDevice.js**, una aplicación Node.js, que simula un dispositivo que se conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y responde método toohello llamado a nube Hola.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.
> 
> 

toocomplete este tutorial, necesita:

* Visual Studio 2015 o Visual Studio 2017.
* Node.js versión 0.10.x, o posteriores.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado
En esta sección, creará una aplicación de consola de Node.js que responde el método tooa llamado a soluciones de hello volver final.

1. Cree una nueva carpeta vacía denominada **simulateddevice**. Hola **simulateddevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema. Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** y **azure-iot-dispositivo-mqtt** paquetes:
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Con un editor de texto, cree un archivo en hello **simulateddevice** carpeta y asígnele el nombre **SimulatedDevice.js**.
4. Agregue Hola siguiente `require` las instrucciones en hello inician de hello **SimulatedDevice.js** archivo:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Agregar un **connectionString** variable y utilizar toocreate un **DeviceClient** instancia. Reemplace **{cadena de conexión de dispositivo}** con cadena de conexión de dispositivo de Hola que generó en hello *crear una identidad de dispositivo* sección:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Agregue Hola siguiendo métodos directas de función tooimplement hello en dispositivo hello:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Abrir el centro de IoT de hello conexión tooyour e inicializar el agente de escucha de hello método:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Guarde y cierre hello **SimulatedDevice.js** archivo.

> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, los reintentos de conexión), tal como se sugiere en el artículo MSDN de hello [control de errores transitorios][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Llamada a un método directo en un dispositivo
En esta sección, creará una aplicación de consola .NET que llama a un método de aplicación de dispositivo simulado de hello y, a continuación, muestra la respuesta de Hola.

1. En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto. Asegúrese de que la versión de .NET Framework de hello es 4.5.1 o posterior. Proyecto de hello Name **CallMethodOnDevice**.
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10]
2. En el Explorador de soluciones, haga clic en hello **CallMethodOnDevice** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .
3. Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso. Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.
   
    ![Ventana del Administrador de paquetes NuGet][11]

4. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Agregar Hola después campos toohello **programa** clase. Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Agregar Hola siguiendo el método toohello **programa** clase:
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Este método invoca un método directo con el nombre `writeLine` en hello `myDeviceId` dispositivo. A continuación, escribe respuesta Hola proporcionada por dispositivo de hello en la consola de Hola. Tenga en cuenta cómo es posible toospecify un valor de tiempo de espera para hello dispositivo toorespond.
7. Por último, agregue Hola después líneas toohello **Main** método:
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a>Ejecutar aplicaciones de Hola
Ya estás listo toorun aplicaciones de Hola.

1. Hola Visual Studio Solution Explorer, haga clic en la solución y, a continuación, haga clic en **Establecer proyectos de inicio...** . Seleccione **proyecto de inicio único**y, a continuación, seleccione hello **CallMethodOnDevice** proyecto en el menú desplegable de Hola.

2. En un símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después de realizar escuchas para las llamadas de método desde el centro de IoT de toostart de comando:
   
    ```
    node SimulatedDevice.js
    ```
   Espere Hola simulada dispositivos tooopen:![][7]
3. Ahora está conectado a ese dispositivo hello y espera para las invocaciones de método, ejecute hello .NET **CallMethodOnDevice** el método de aplicación tooinvoke hello en la aplicación de dispositivo simulado de hello. Debería ver la respuesta del dispositivo Hola escrito en la consola de Hola.
   
    ![][8]
4. dispositivo de Hello, a continuación, reacciona toohello método imprimiendo este mensaje:
   
    ![][9]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Utiliza este toomethods dispositivo identidad tooenable Hola simulada dispositivos aplicación tooreact invocado por la nube de Hola. También crea una aplicación que invoca los métodos en el dispositivo de Hola y muestra la respuesta de hello de dispositivo de Hola. 

toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:

* [Introducción al Centro de IoT]
* [Programación de trabajos en varios dispositivos][lnk-devguide-jobs]

toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Introducción al Centro de IoT]: iot-hub-node-node-getstarted.md
