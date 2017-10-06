---
title: propiedades de gemelas los dispositivos aaaUse centro de IoT de Azure (nodo/.NET) | Documentos de Microsoft
description: "Cómo los dispositivos del centro de IoT de Azure toouse gemelos tooconfigure dispositivos. Utilice hello servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que se modifica una configuración de dispositivo mediante un doble de dispositivo y el dispositivo de hello IoT de Azure SDK para Node.js tooimplement una aplicación de dispositivo simulado."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>Usar propiedades deseadas tooconfigure dispositivos
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Al final de Hola de este tutorial, tendrá dos aplicaciones de consola:

* **SimulateDeviceConfiguration.js**, una aplicación de dispositivo simulado que espera una actualización de la configuración deseada e informa del estado de Hola de un proceso de actualización de configuración simulada.
* **SetDesiredConfigurationAndQuery**, una aplicación de back-end. NET, que establece Hola la configuración en un dispositivo deseado y consultas Hola el proceso de actualización de configuración.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.
> 
> 

toocomplete este tutorial necesita Hola siguiente:

* Visual Studio 2015 o Visual Studio 2017.
* Node.js versión 0.10.x, o posteriores.
* Una cuenta de Azure activa. Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.

Si ha seguido hello [empezar a trabajar con: los gemelos de dispositivo] [ lnk-twin-tutorial] tutorial, ya tiene un centro de IoT y una identidad de dispositivo llama **myDeviceId**. En ese caso, puede omitir toohello [aplicación de dispositivo simulado de hello crear] [ lnk-how-to-configure-createapp] sección.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Crear aplicación de dispositivo simulado de hello
En esta sección, creará una aplicación de consola de Node.js que conecta el concentrador de tooyour como **myDeviceId**, espera a que una actualización de la configuración deseada y, a continuación, informa de las actualizaciones en el proceso de actualización de configuración de Hola simulada.

1. Cree una nueva carpeta vacía denominada **simulatedeviceconfiguration**. Hola **simulatedeviceconfiguration** carpeta, cree un nuevo archivo package.json mediante el siguiente comando en el símbolo del sistema de Hola. Acepte todos los valores predeterminados de Hola.
   
    ```
    npm init
    ```
1. En el símbolo del sistema en hello **simulatedeviceconfiguration** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** y **azure iot dispositivo-mqtt**paquetes:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. Con un editor de texto, cree un nuevo **SimulateDeviceConfiguration.js** archivo Hola **simulatedeviceconfiguration** carpeta.
1. Agregar Hola después código toohello **SimulateDeviceConfiguration.js** archivo y sustituya hello **{cadena de conexión de dispositivo}** marcador de posición con la cadena de conexión de dispositivo Hola copió cuando se crea hello **myDeviceId** identidad del dispositivo:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    Hola **cliente** objeto expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del dispositivo de Hola. Este código inicializa hello **cliente** objeto, recupera Hola gemelas de dispositivo para **myDeviceId**y, a continuación, se adjunta un controlador de actualización de hello en *deseado propiedades*. controlador de Hello comprueba que hay es una solicitud de cambio de la configuración real mediante la comparación de hello configIds, a continuación, invoca un método que inicia el cambio de configuración de Hola.
   
    Tenga en cuenta que para hello simplificar, este código usa el valor predeterminado codificado de forma rígida para la configuración inicial de Hola. Una aplicación real probablemente cargaría esa configuración desde un almacenamiento local.
   
   > [!IMPORTANT]
   > Los eventos de cambio de propiedad deseados siempre se emiten una vez en la conexión de dispositivo. Asegúrese de que toocheck que hay un cambio real en hello las propiedades adecuadas antes de realizar cualquier acción.
   > 
   > 
1. Agregar Hola siguientes métodos antes de hello `client.open()` invocación:
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    Hola **initConfigChange** método actualizaciones Hola notificado propiedades Hola dispositivo local gemelas objeto con la configuración de hello actualizan solicitud y establece el estado de Hola demasiado**pendiente**, a continuación, Hola de actualizaciones gemelos de dispositivo en el servicio de Hola. Después de actualizar correctamente los gemelos de dispositivo de hello, simula un proceso de ejecución prolongada que finaliza en la ejecución de Hola de **completeConfigChange**. Este método actualiza las propiedades del incluido local Hola establecer el estado de hello demasiado**correcto** y quitar hello **pendingConfig** objeto. A continuación, actualiza a gemelas de dispositivo de hello en el servicio de Hola.
   
    Tenga en cuenta que, ancho de banda toosave, indica que se actualizan propiedades especificando solo Hola propiedades toobe modificado (denominado **revisión** Hola por encima del código), en lugar de reemplazar todo el documento Hola.
   
   > [!NOTE]
   > Este tutorial no simula ningún comportamiento de las actualizaciones de configuración simultáneas. Algunos procesos de actualización de la configuración podrían ser capaz de tooaccommodate cambios de configuración de destino mientras se ejecuta la actualización de hello, algunas pueden disponer de tooqueue ellos así como algunos pudieron rechazar ellos con una condición de error. Asegúrese de tooconsider seguro Hola comportamiento deseado para el proceso de configuración específica y cómo agregar lógica adecuada de hello antes de iniciar el cambio de configuración de Hola.
   > 
   > 
1. Ejecute la aplicación de dispositivo de hello:
   
        node SimulateDeviceConfiguration.js
   
    Debe aparecer un mensaje Hola `retrieved device twin`. Mantenga la aplicación hello ejecutando.

## <a name="create-hello-service-app"></a>Crear aplicación de servicio de hello
En esta sección, aprenderá a crear una aplicación de consola .NET que hello las actualizaciones *deseado propiedades* en hello dispositivo gemelas asociada **myDeviceId** con un nuevo objeto de configuración de telemetría. A continuación, consulta: los gemelos de dispositivo de hello almacenados en el centro de IoT de Hola y muestra diferenciar hello en hello deseado y notifica las configuraciones de dispositivo de Hola.

1. En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto. Proyecto de hello Name **SetDesiredConfigurationAndQuery**.
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]
1. En el Explorador de soluciones, haga clic en hello **SetDesiredConfigurationAndQuery** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .
1. Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso. Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. Agregar Hola después campos toohello **programa** clase. Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Agregar Hola siguiendo el método toohello **programa** clase:
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    Hola **registro** objeto expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del servicio de Hola. Este código inicializa hello **registro** objeto, recupera Hola gemelas de dispositivo para **myDeviceId**y, a continuación, actualiza sus propiedades deseados con un nuevo objeto de configuración de telemetría.
    Después de eso, consulta: los gemelos de dispositivo de hello almacenados en el centro de IoT Hola cada 10 segundos y copias fotográficas Hola deseado y notifica las configuraciones de telemetría. Consulte toohello [lenguaje de consultas del centro de IoT] [ lnk-query] toolearn cómo toogenerate enriquecido informes en todos los dispositivos.
   
   > [!IMPORTANT]
   > Esta aplicación consulta IoT Hub cada 10 segundos con fines ilustrativos. Use consultas toogenerate orientadas al usuario informes a través de varios dispositivos y no toodetect cambios. Si la solución requiere notificaciones en tiempo real de eventos de dispositivo, use [notificaciones gemelas][lnk-twin-notifications].
   > 
   > 
1. Por último, agregue Hola después líneas toohello **Main** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. Hola el Explorador de soluciones, abra hello **proyectos de inicio establecido...**  y asegúrese de que hello **acción** para **SetDesiredConfigurationAndQuery** proyecto es **iniciar**. Compile la solución de Hola.
1. Con **SimulateDeviceConfiguration.js** ejecutando, ejecute la aplicación de .NET de Hola desde Visual Studio mediante **F5** y debería ver Hola notificado configuración cambia de **correcto** demasiado**pendiente** demasiado**correcto** nuevo con activo nuevo Hola enviar frecuencia de cinco minutos en lugar de 24 horas.

 ![Dispositivo configurado correctamente][img-deviceconfigured]
   
   > [!IMPORTANT]
   > Hay un retraso de tooa minuto entre la operación de informe de dispositivo de Hola y el resultado de la consulta de Hola. Se trata de tooenable Hola consulta infraestructura toowork a gran escala. tooretrieve vistas coherentes de doble de un único dispositivo usan hello **getDeviceTwin** método Hola **registro** clase.
   > 
   > 

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, establezca una configuración deseada como *deseado propiedades* de solución de hello back-end y escribió una toodetect de aplicación de dispositivo que cambian y simular un proceso de actualización de varios pasos reporting su estado a través de hello notificado Propiedades.

Hola de uso después cómo toolearn de recursos para:

* enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT] [ lnk-iothub-getstarted] tutorial,
* programar o realizar operaciones en conjuntos grandes de dispositivos Consulte hello [programación y los trabajos de difusión] [ lnk-schedule-jobs] tutorial.
* controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario), con hello [usar métodos directos] [ lnk-methods-tutorial] tutorial.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
