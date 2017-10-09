---
title: trabajos de aaaSchedule con el centro de IoT de Azure (nodo/.NET) | Documentos de Microsoft
description: "¿Cómo tooschedule un centro de IoT de Azure trabajo tooinvoke un método directo en varios dispositivos. Usar dispositivos de IoT de Azure de hello SDK para hello servicio IoT de Azure SDK para .NET tooimplement un trabajo de servicio aplicación toorun hello y aplicaciones para dispositivos Node.js tooimplement Hola simulada."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a>Programación y difusión de trabajos (.NET/Node.js)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Utilice los trabajos de tooschedule y realizar un seguimiento de centro de IoT de Azure que actualizan millones de dispositivos. Use los trabajos para:

* Actualizar las propiedades deseadas
* Actualizar etiquetas
* Invocar métodos directos

Un trabajo encapsula una de estas acciones y pistas Hola ejecución con un conjunto de dispositivos que se define mediante una consulta de gemelas de dispositivo. Por ejemplo, una aplicación de back-end puede usar un tooinvoke de trabajo un método directo en 10.000 dispositivos que reinicia dispositivos Hola. Especifique el conjunto de Hola de dispositivos con una consulta de gemelas de dispositivo y programar toorun de trabajo de hello en el futuro. progreso de realiza un seguimiento del trabajo de Hello como cada uno de los dispositivos de Hola recibir y ejecutar el método directo de reinicio de Hola.

toolearn más información acerca de cada una de estas funciones, vea:

* Gemelos de dispositivo y propiedades: [empezar a trabajar con: los gemelos de dispositivo] [ lnk-get-started-twin] y [Tutorial: cómo toouse dispositivo dos propiedades][lnk-twin-props]
* Métodos directos: [Guía del desarrollador de IoT Hub: métodos directos][lnk-dev-methods] y [Tutorial: Uso de métodos directos][lnk-c2d-methods]

En este tutorial se muestra cómo realizar las siguientes acciones:

* Crear una aplicación de dispositivo que implementa un método directo denominado **lockDoor** que puede llamarse mediante aplicaciones de back-end de Hola. aplicación de dispositivo de Hello también recibe cambios de la propiedad deseada desde aplicaciones de back-end de Hola.
* Crear una aplicación de back-end que crea un Hola de trabajo toocall **lockDoor** método directo en varios dispositivos. Otro trabajo envía la propiedad deseada actualiza toomultiple dispositivos.

Al final de Hola de este tutorial, tendrá una aplicación de dispositivo de consola de Node.js y una aplicación de back-end de consola .NET (C#):

**simDevice.js** que se conecta el centro de IoT tooyour, implementa hello **lockDoor** dirigir deseado de método y controla los cambios de propiedad.

**ScheduleJob** que usa Hola de trabajos toocall **lockDoor** directo gemelas del dispositivo de hello método y actualizar las propiedades en varios dispositivos adecuadas.

toocomplete este tutorial, necesita Hola siguientes:

* Visual Studio 2015 o Visual Studio 2017.
* Node.js versión 0.12.x o posteriores. artículo de Hello [preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Node.js para este tutorial en Windows o Linux.
* Una cuenta de Azure activa. En caso de no tener ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a>Programación de trabajos para llamar a un método directo y envío de actualizaciones de dispositivo gemelo

En esta sección, creará una aplicación de consola de .NET (mediante C#) que usa Hola de toocall trabajos **lockDoor** método directo y enviar la propiedad deseada actualiza toomultiple dispositivos.

1. En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto. Proyecto de hello Name **ScheduleJob**.

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]

1. En el Explorador de soluciones, haga clic en hello **ScheduleJob** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .
1. Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso. Este paso descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.

    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. Agregue los siguiente hello `using` instrucción si no están ya presentes en las instrucciones de Hola de forma predeterminada.

    ```csharp
    using System.Threading.Tasks;
    ```

1. Agregar Hola después campos toohello **programa** clase. Reemplace el marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. Agregar Hola siguiendo el método toohello **programa** clase:

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. Agregar Hola siguiendo el método toohello **programa** clase:

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. Agregar Hola siguiendo el método toohello **programa** clase:

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. Por último, agregue Hola después líneas toohello **Main** método:

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. Hola el Explorador de soluciones, abra hello **proyectos de inicio establecido...**  y asegúrese de que hello **acción** para **ScheduleJob** proyecto es **iniciar**. Compile la solución de Hola.

## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado

En esta sección, creará una aplicación de consola de Node.js que responde tooa método directo llamado a la nube de hello, lo que desencadena un reinicio del dispositivo simulado y utiliza Hola notificado propiedades tooenable dispositivos gemelas consultas tooidentify dispositivos y cuando reinició por última vez.

1. Cree una nueva carpeta vacía denominada **simDevice**.  Hola **simDevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.  Acepte todos los valores predeterminados de hello:

    ```cmd/sh
    npm init
    ```

1. En el símbolo del sistema en hello **simDevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** y **azure-iot-dispositivo-mqtt** paquetes:

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Con un editor de texto, cree un nuevo **simDevice.js** archivo Hola **simDevice** carpeta.

1. Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **simDevice.js** archivo:

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. Agregar un **connectionString** variable y utilizar toocreate un **cliente** instancia. Asegúrese de los marcadores de posición hello tooreplace seguro con el programa de instalación de valores tooyour adecuado.

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Agregar Hola después Hola de función toohandle **lockDoor** método.

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. Agregar Hola siguiente controlador de hello tooregister de código de hello **lockDoor** método.

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. Guarde y cierre hello **simDevice.js** archivo.

> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola

Ya estás listo toorun Hola aplicaciones.

1. En línea de comandos de Hola Hola **simDevice** carpeta, ejecute hello después toobegin comando realizar escuchas de método directo de reinicio de Hola.

    ```cmd/sh
    node simDevice.js
    ```

1. Aplicación de consola de hello ejecución C# **ScheduleJob** con el botón secundario en hello **ScheduleJob** proyecto, a continuación, seleccione **depurar** y **Iniciar nueva instancia**.

1. Consulte la salida de hello de dispositivo y aplicaciones de back-end.

    ![Ejecutar aplicaciones de hello tooschedule trabajos][img-schedulejobs]

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha utilizado un trabajo tooschedule un dispositivo de tooa método directo y actualización de Hola de las propiedades del doble del dispositivo de Hola.

toocontinue introducción con patrones de la administración de centro de IoT y el dispositivo como el remoto a través de la actualización de firmware de aire hello, leer [Tutorial: cómo toodo un firmware actualizar][lnk-fwupdate].

toocontinue Introducción a centro de IoT, consulte [introducción con borde IoT][lnk-iot-edge].

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
