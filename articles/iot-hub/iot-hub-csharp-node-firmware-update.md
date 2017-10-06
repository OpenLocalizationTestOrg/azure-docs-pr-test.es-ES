---
title: "actualización de firmware de aaaDevice con el centro de IoT de Azure (nodo/.NET) | Documentos de Microsoft"
description: "Cómo actualizar toouse la administración de dispositivos en el centro de IoT de Azure tooinitiate un firmware del dispositivo. Utilice hello servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que desencadena la actualización de firmware de Hola y dispositivo de hello IoT de Azure SDK para Node.js tooimplement una aplicación de dispositivo simulado."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a>Use Administración de dispositivo tooinitiate una actualización de firmware del dispositivo (o nodo de. NET)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Introducción
Hola [empezar a trabajar con la administración de dispositivos] [ lnk-dm-getstarted] tutorial, ha visto cómo hello toouse [gemelas dispositivo] [ lnk-devtwin] y [directo métodos] [ lnk-c2dmethod] tooremotely primitivas reiniciar un dispositivo. Este tutorial se utiliza Hola mismos tipos primitivos de centro de IoT y muestra cómo toodo un extremo a otro simula la actualización de firmware.  Este patrón se utiliza en la implementación de actualización de firmware de Hola para hello [ejemplo de implementación de dispositivo de frambuesa Pi][lnk-rpi-implementation].

En este tutorial se muestra cómo realizar las siguientes acciones:

* Crear una aplicación de consola .NET que llama a métodos directas de hello firmwareUpdate en aplicación del dispositivo simulado de hello a través de su centro de IoT.
* Cree una aplicación de dispositivo simulado que implemente un método directo **firmwareUpdate**. Este método inicia un proceso de varias fase que espera a que la imagen de firmware de hello toodownload, descarga la imagen de firmware de Hola y por último, se aplica la imagen de firmware Hola. Durante cada fase de actualización de hello, Hola dispositivo usa Hola notifica propiedades tooreport en progreso.

Al final de Hola de este tutorial, tendrá una aplicación de dispositivo de consola de Node.js y una aplicación de back-end de consola .NET (C#):

**dmpatterns_fwupdate_service.js**, que llama a un método directo en la aplicación de dispositivo simulado de hello, muestra la respuesta de Hola y periódicamente (cada 500 ms) hello muestra actualizado notificado propiedades.

**TriggerFWUpdate**, centro de IoT tooyour que conecta con la identidad del dispositivo Hola creado anteriormente, recibe un método directo firmwareUpdate, se ejecuta a través de un proceso de varios Estados toosimulate un incluidos de actualización de firmware: espera de descarga de la imagen de hello, Descargar la nueva imagen de Hola y finalmente Aplicar imagen de Hola.

toocomplete este tutorial, necesita Hola siguientes:

* Visual Studio 2015 o Visual Studio 2017.
* Node.js versión 0.12.x o posteriores. <br/>  [Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Node.js para este tutorial en Windows o Linux.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

Siga hello [empezar a trabajar con la administración de dispositivos](iot-hub-csharp-node-device-management-get-started.md) artículo toocreate su centro de IoT y obtener la cadena de conexión de centro de IoT.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Desencadenar una actualización de firmware remoto en dispositivo Hola utilizando un método directo
En esta sección, creará una aplicación de consola de .NET (mediante C#) que inicia una actualización de firmware remota en un dispositivo. aplicación Hello usa una actualización de hello tooinitiate método directo y usa dispositivos gemelas consultas tooperiodically obtener estado de Hola de actualización de firmware active Hola.

1. En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto. Proyecto de hello Name **TriggerFWUpdate**.

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]

1. En el Explorador de soluciones, haga clic en hello **TriggerFWUpdate** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .
1. Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso. Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.

    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. Agregar Hola después campos toohello **programa** clase. Reemplace Hola Hola de varios valores de marcador de posición con cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola y Hola Id. del dispositivo.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. Agregar Hola siguiendo el método toohello **programa** clase:
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. Agregar Hola siguiendo el método toohello **programa** clase:

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. Por último, agregue Hola después líneas toohello **Main** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. Hola el Explorador de soluciones, abra hello **proyectos de inicio establecido...**  y asegúrese de que hello **acción** para **TriggerFWUpdate** proyecto es **iniciar**.

1. Compile la solución de Hola.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola
Ya estás listo toorun Hola aplicaciones.

1. En línea de comandos de Hola Hola **manageddevice** carpeta, ejecute hello después toobegin comando realizar escuchas de método directo de reinicio de Hola.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. En Visual Studio, haga doble clic en hello **TriggerFWUpdate** aplicación de consola de toohello C# projectRun, seleccione **depurar** y **Iniciar nueva instancia**.

3. Consulte dispositivo respuesta toohello directo método hello en la consola de Hola.

    ![Firmware actualizado correctamente][img-fwupdate]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha utilizado un tootrigger método directo un control remoto actualización de firmware en un dispositivo y Hola usado informó sobre el progreso de hello toofollow de propiedades de actualización de firmware de Hola.

toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/