---
title: "aaaGet comenzar con la administración de dispositivos del centro de IoT de Azure (nodo/.NET) | Documentos de Microsoft"
description: "¿Cómo tooinitiate de administración de dispositivos de centro de IoT de Azure toouse reiniciar un dispositivo remoto. Usar dispositivos de IoT de Azure de hello SDK para Node.js tooimplement una aplicación de dispositivo simulado que incluye un método directo y el servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que invoca el método directo Hola Hola."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a>Introducción a la administración de dispositivos (.NET y Node)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

En este tutorial se muestra cómo realizar las siguientes acciones:

* Usar hello toocreate portal Azure un centro de IoT y cree una identidad de dispositivo en el centro de IoT.
* Crear una aplicación de dispositivo simulado que contiene un método directo que reinicia ese dispositivo. Se invocan métodos directos de nube de Hola.
* Crear una aplicación de consola .NET que llama a métodos directas de reinicio de hello en la aplicación de dispositivo simulado de hello a través de su centro de IoT.

Al final de Hola de este tutorial, tendrá una aplicación de dispositivo de consola de Node.js y una aplicación de back-end de consola .NET (C#):

**dmpatterns_getstarted_device.js**, centro de IoT tooyour que conecta con la identidad del dispositivo Hola creado anteriormente, recibe un método directo de reinicio, simula reiniciar el equipo físico e informa Hola el tiempo de último reinicio de Hola.

**TriggerReboot**, que llama a un método directo en la aplicación de dispositivo simulado de hello, muestra la respuesta de Hola y Hola muestra actualizado notificado propiedades.

toocomplete este tutorial, necesita Hola siguientes:

* Visual Studio 2015 o Visual Studio 2017.
* Node.js versión 0.12.x o posteriores. <br/>  [Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Node.js para este tutorial en Windows o Linux.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Desencadenar un reinicio remoto en dispositivo Hola utilizando un método directo
En esta sección, creará una aplicación de consola de .NET (mediante C#) que inicia una actualización remota en un dispositivo mediante un método directo. aplicación Hello usa Hola de toodiscover de consultas última hora de reinicio de dispositivo gemelas para dicho dispositivo.

1. En Visual Studio, agregue una nueva solución de Visual C# escritorio clásico de Windows proyecto tooa mediante el uso de hello **aplicación de consola (.NET Framework)** plantilla de proyecto. Asegúrese de que la versión de .NET Framework de hello es 4.5.1 o posterior. Proyecto de hello Name **TriggerReboot**.

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]

2. En el Explorador de soluciones, haga clic en hello **TriggerReboot** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.
3. Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso. Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.

    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
4. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. Agregar Hola después campos toohello **programa** clase. Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola y el dispositivo de destino de Hola Hola.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. Agregar Hola siguiendo el método toohello **programa** clase.  Este gemelas de dispositivo de código obtiene Hola para reiniciar el sistema hello de dispositivo y las salidas de hello informó de propiedades.
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. Agregar Hola siguiendo el método toohello **programa** clase.  Este código inicia el reinicio de hello en dispositivo Hola utilizando un método directo.

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. Por último, agregue Hola después líneas toohello **Main** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. Compile la solución de Hola.

## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado
En esta sección:

* Crear una aplicación de consola de Node.js que responde tooa método directo llamado en la nube Hola
* Desencadenará un reinicio del dispositivo simulado.
* Hola uso notificado propiedades tooenable dispositivos gemelas consultas tooidentify dispositivos y cuándo reinició por última vez

1. Cree una nueva carpeta vacía denominada "**manageddevice**".  Hola **manageddevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.  Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **manageddevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** paquete del SDK de dispositivo y **azure iot dispositivo-mqtt**paquete:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Con un editor de texto, cree un nuevo **dmpatterns_getstarted_device.js** archivo Hola **manageddevice** carpeta.
4. Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **dmpatterns_getstarted_device.js** archivo:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Agregar un **connectionString** variable y utilizar toocreate un **cliente** instancia.  Reemplace la cadena de conexión de hello con la cadena de conexión del dispositivo.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Agregar Hola siguiendo métodos directas de función tooimplement hello en dispositivo Hola
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Agregue código centro de IoT de tooopen Hola conexión tooyour siguiente de Hola e inicia el agente de escucha de hello método directo:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. Guarde y cierre hello **dmpatterns_getstarted_device.js** archivo.
   
> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].


## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola
Ya estás listo toorun Hola aplicaciones.

1. En línea de comandos de Hola Hola **manageddevice** carpeta, ejecute hello después toobegin comando realizar escuchas de método directo de reinicio de Hola.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Aplicación de consola de hello ejecución C# **TriggerReboot**. Menú contextual hello **TriggerReboot** proyecto, seleccione **depurar**y, a continuación, seleccione **Iniciar nueva instancia**.

3. Consulte dispositivo respuesta toohello directo método hello en la consola de Hola.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/