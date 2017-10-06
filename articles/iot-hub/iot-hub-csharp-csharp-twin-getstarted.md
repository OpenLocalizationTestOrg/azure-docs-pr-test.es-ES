---
title: "aaaGet partió gemelos de dispositivo del centro de IoT de Azure (.NET/.NET) | Documentos de Microsoft"
description: "¿Cómo toouse centro de IoT de Azure dispositivo: los gemelos tooadd etiquetas y, a continuación, utilice una consulta de centro de IoT. Usar dispositivos de IoT de Azure de hello SDK para hello servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que agrega etiquetas de Hola y ejecuta consultas del centro de IoT hello y aplicación de .NET tooimplement hello dispositivo simulado."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a>Introducción a los dispositivos gemelos (.NET/.NET)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Al final de Hola de este tutorial, tendrá estas aplicaciones de consola. NET:

* **CreateDeviceIdentity**, una aplicación de .NET que crea una identidad del dispositivo y la seguridad de clave tooconnect la aplicación de dispositivo simulado.
* **AddTagsAndQuery**, una aplicación .NET de back-end diseñada para ejecutarse desde el back-end, que agrega etiquetas y consulta dispositivos gemelos.
* **ReportConnectivity**, una aplicación de dispositivo de .NET que simula un dispositivo que conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente e informa acerca de su condición de conectividad.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.
> 
> 

toocomplete este tutorial necesita Hola siguiente:

* Visual Studio 2015 o Visual Studio 2017.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Si desea identidad del dispositivo toocreate hello mediante programación en su lugar, lea las secciones correspondientes de Hola Hola [conectar el centro de IoT de tooyour dispositivo simulado mediante .NET] [ lnk-device-identity-csharp] artículo.

## <a name="create-hello-service-app"></a>Crear aplicación de servicio de hello
En esta sección, creará una aplicación de consola de .NET (mediante C#) que agrega gemelas de dispositivo de toohello ubicación metadatos asociados a **myDeviceId**. A continuación, consulta: los gemelos de hello dispositivo almacenan en el centro de IoT Hola seleccionar dispositivos de hello ubicados en hello nos y los que informó de una conexión de telefonía móvil Hola, a continuación.

1. En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto. Proyecto de hello Name **AddTagsAndQuery**.
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]
1. En el Explorador de soluciones, haga clic en hello **AddTagsAndQuery** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .
1. Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar** y busque **microsoft.azure.devices**. Seleccione **instalar** tooinstall hello **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso. Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
   
        using Microsoft.Azure.Devices;
1. Agregar Hola después campos toohello **programa** clase. Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Agregar Hola siguiendo el método toohello **programa** clase:
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    Hola **RegistryManager** clase expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del servicio de Hola. código anterior Hola inicializa por primera vez hello **registryManager** objeto, a continuación, recupera Hola gemelas de dispositivo para **myDeviceId**y por último actualiza sus etiquetas con información de ubicación de hello deseado.
   
    Después de actualizar, se ejecutan dos consultas: Hola primero selecciona solo Hola dispositivo: los gemelos de dispositivos que se encuentran en hello **Redmond43** planta Hola segundo perfecciona Hola consulta tooselect solo Hola dispositivos y que también están conectados a través de red de telefonía móvil.
   
    Tenga en cuenta ese código Hola anterior, cuando crea hello **consulta** de objetos, especifica un número máximo de documentos devueltos. Hola **consulta** objeto contiene un **HasMoreResults** propiedad booleana que se puede usar hello tooinvoke **GetNextAsTwinAsync** métodos varias veces tooretrieve todos los resultados. Un método llamado **GetNextAsJson** está disponible para los resultados que no son dispositivos gemelos, por ejemplo, los resultados de consultas de agregación.
1. Por último, agregue Hola después líneas toohello **Main** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. Hola el Explorador de soluciones, abra hello **proyectos de inicio establecido...**  y asegúrese de que hello **acción** para **AddTagsAndQuery** proyecto es **iniciar**. Compile la solución de Hola.
1. Ejecutar esta aplicación con el botón secundario en hello **AddTagsAndQuery** proyecto y seleccione **depurar**, seguido de **Iniciar nueva instancia**. Debería ver un dispositivo en los resultados de Hola para hello formular de consulta para todos los dispositivos ubicados en **Redmond43** y ninguno para consulta de Hola que restringe Hola resultados toodevices que usan una red móvil.
   
    ![Resultados de consulta en ventana][img-addtagapp]

En la siguiente sección hello, crear una aplicación de dispositivo que contiene información de conectividad de Hola y cambios Hola resultado de consulta de hello en la sección anterior de Hola.

## <a name="create-hello-device-app"></a>Crear aplicación de dispositivo de hello
En esta sección, creará una aplicación de consola .NET que se conecta el concentrador de tooyour como **myDeviceId**y, a continuación, actualiza su información de Hola de toocontain propiedades notificado que está conectado mediante una red de telefonía móvil.

1. En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto. Proyecto de hello Name **ReportConnectivity**.
   
    ![Nueva aplicación para dispositivo de Windows clásico de Visual C#][img-createdeviceapp]
    
1. En el Explorador de soluciones, haga clic en hello **ReportConnectivity** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .
1. Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar** y busque **microsoft.azure.devices.client**. Seleccione **instalar** tooinstall hello **Microsoft.Azure.Devices.Client** empaquetar y acepte los términos de Hola de uso. Este procedimiento se descarga, se instala y se agrega una referencia toohello [dispositivos de IoT de Azure SDK] [ lnk-nuget-client-sdk] NuGet paquete y sus dependencias.
   
    ![Ventana del Administrador de paquetes NuGet: aplicación cliente][img-clientnuget]
1. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Agregar Hola después campos toohello **programa** clase. Reemplace el valor de marcador de posición de hello con cadena de conexión de dispositivo de Hola que anotó en la sección anterior de Hola.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Agregar Hola siguiendo el método toohello **programa** clase:

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    Hola **cliente** objeto expone todos los métodos de hello requieren toointeract con: los gemelos de dispositivo del dispositivo de Hola. Hola mostrado anteriormente, el código inicializa hello **cliente** objeto y, a continuación, recupera Hola dispositivo gemelas para **myDeviceId**.

1. Agregar Hola siguiendo el método toohello **programa** clase:
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   Hola código encima de las actualizaciones de **myDeviceId**del notificado propiedad con información de conectividad de Hola.

1. Por último, agregue Hola después líneas toohello **Main** método:
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. Hola el Explorador de soluciones, abra hello **proyectos de inicio establecido...**  y asegúrese de que hello **acción** para **ReportConnectivity** proyecto es **iniciar**. Compile la solución de Hola.
1. Ejecutar esta aplicación con el botón secundario en hello **ReportConnectivity** proyecto y seleccione **depurar**, seguido de **Iniciar nueva instancia**. Debería ver obtener Hola gemelas información y, a continuación, enviar conectividad como un *notificado propiedad*.
   
    ![Ejecute la conectividad de tooreport de aplicación de dispositivo][img-rundeviceapp]
    
    
1. Ahora que hello dispositivo había notificado su información de conectividad, debe aparecer en las dos consultas. Ejecute hello .NET **AddTagsAndQuery** Hola de toorun aplicación consulta de nuevo. Esta vez **myDeviceId** debe aparecer en los resultados de ambas consulta.
   
    ![Conectividad de dispositivo notificada correctamente][img-tagappsuccess]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Agrega los metadatos del dispositivo como etiquetas desde una aplicación de back-end y una información de conectividad del dispositivo de tooreport de aplicación de dispositivo simulado se escribió en gemelas de dispositivo de Hola. También habrá aprendido cómo tooquery esta información mediante el lenguaje de consulta de hello centro de IoT similar a SQL.

Hola de uso después cómo toolearn de recursos para:

* enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT] [ lnk-iothub-getstarted] tutorial,
* configurar dispositivos mediante propiedades que desee del doble del dispositivo con hello [uso deseado propiedades de dispositivos con tooconfigure] [ lnk-twin-how-to-configure] tutorial,
* controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario) con hello [usar métodos directos] [ lnk-methods-tutorial] tutorial.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

