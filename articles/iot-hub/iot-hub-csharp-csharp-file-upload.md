---
title: archivos de aaaUpload desde dispositivos tooAzure centro de IoT con. NET | Documentos de Microsoft
description: "¿Cómo tooupload archivos desde una dispositivo toohello la nube mediante dispositivos de IoT de Azure SDK para. NET. Los archivos cargados se almacenan en un contenedor de blobs de Azure Storage."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: elioda
ms.openlocfilehash: 07d555f6ba8b067bbd3233bc8eebaa220ad2388b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a>Cargar archivos desde su dispositivo toohello la nube con el centro de IoT con .NET

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Este tutorial se basa en el código de hello de hello [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-csharp-csharp-c2d.md) tooshow tutorial también cómo toouse Hola capacidades de carga de archivos del centro de IoT. En él se muestra cómo realizar las siguientes acciones:

- Proporcionar un dispositivo de forma segura con un identificador URI de blob de Azure para cargar un archivo.
- Usar hello centro de IoT archivo carga notificaciones tootrigger procesar el archivo de hello en el back-end de aplicación.

Hola [empezar a trabajar con el centro de IoT](iot-hub-csharp-csharp-getstarted.md) y [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-csharp-csharp-c2d.md) los tutoriales muestra hello dispositivo a la nube y en la nube al dispositivo funcionalidad de mensajería básica de centro de IoT. Hola [mensajes proceso dispositivo a la nube](iot-hub-csharp-csharp-process-d2c.md) tutorial describe una manera tooreliably almacenar dispositivo a la nube mensajes en el almacenamiento de blobs de Azure. Sin embargo, en algunos escenarios no se puede asignar fácilmente datos Hola que los dispositivos de envío en hello relativamente pequeño dispositivo a la nube los mensajes que acepta el centro de IoT. Por ejemplo:

* Archivos grandes con imágenes
* Vídeos
* Datos de vibración muestreados con alta frecuencia
* Cierto tipo de datos procesados previamente

Estos archivos suelen ser lote procesado en la nube de hello con herramientas como [Data Factory de Azure](../data-factory/index.md) o hello [Hadoop](../hdinsight/index.md) pila. Si necesita archivos tooupload desde un dispositivo, todavía puede usar seguridad hello y la confiabilidad del centro de IoT.

Al final de Hola de este tutorial, ejecutar dos aplicaciones de consola. NET:

* **SimulatedDevice**, una versión modificada de la aplicación hello creado en hello [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-csharp-csharp-c2d.md) tutorial. Esta aplicación carga una toostorage de archivo mediante un URI de SAS proporcionados por el centro de IoT.
* **ReadFileUploadNotification**, que recibe notificaciones de carga de archivos del Centro de IoT.

> [!NOTE]
> El Centro de IoT admite muchas plataformas de dispositivos y lenguajes (incluido C, Java y JavaScript), mediante los SDK de dispositivo IoT de Azure. Consulte toohello [Centro para desarrolladores de Azure IoT] para obtener instrucciones paso a paso sobre cómo tooconnect su centro de IoT tooAzure de dispositivo.

toocomplete este tutorial, necesita Hola siguientes:

* Visual Studio 2015 o Visual Studio 2017
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Carga de un archivo desde una aplicación de dispositivo

En esta sección, se modifica Hola del dispositivo que creó en [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-csharp-csharp-c2d.md) mensajes de nube al dispositivo tooreceive Hola centro de IoT.

1. En Visual Studio, haga clic en hello **SimulatedDevice** proyecto de equipo y haga clic en **agregar**y, a continuación, haga clic en **elemento existente**. Navegar por el archivo de imagen tooan e incluirla en el proyecto. Este tutorial se da por supuesto que se denomina imagen hello `image.jpg`.

1. Haga doble clic en la imagen de hello y, a continuación, haga clic en **propiedades**. Asegúrese de que **copiar tooOutput directorio** se establece demasiado**copiar siempre**.

    ![][1]

1. Hola **Program.cs** , agregue Hola siguiendo las instrucciones en la parte superior de hello del archivo hello:

    ```csharp
    using System.IO;
    ```

1. Agregar Hola siguiendo el método toohello **programa** clase:

    ```csharp
    private static async void SendToBlobAsync()
    {
        string fileName = "image.jpg";
        Console.WriteLine("Uploading file: {0}", fileName);
        var watch = System.Diagnostics.Stopwatch.StartNew();

        using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
        {
            await deviceClient.UploadToBlobAsync(fileName, sourceData);
        }

        watch.Stop();
        Console.WriteLine("Time tooupload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    Hola `UploadToBlobAsync` método toma en nombre de archivo de Hola y origen de la secuencia de hello archivo toobe cargado y controla Hola carga toostorage. aplicación de consola de Hello muestra hello duración del archivo de hello tooupload.

1. Agregar Hola siguiente método Hola **Main** método, justo antes de hello `Console.ReadLine()` línea:

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> Por simplificar, este tutorial no implementa ninguna directiva de reintentos. En el código de producción, debe implementar directivas de reintento (por ejemplo, retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios].

## <a name="receive-a-file-upload-notification"></a>Recepción de una notificación de carga de archivos

En esta sección, se escribe una aplicación de consola de .NET que recibe mensajes de notificación de carga de archivos de IoT Hub.

1. En la solución de Visual Studio actual hello, crear un proyecto de Windows de Visual C# mediante hello **aplicación de consola** plantilla de proyecto. Proyecto de hello Name **ReadFileUploadNotification**.

    ![Nuevo proyecto en Visual Studio][2]

1. En el Explorador de soluciones, haga clic en hello **ReadFileUploadNotification** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .

1. Hola **Administrador de paquetes de NuGet** ventana, busque **Microsoft.Azure.Devices**, haga clic en **instalar**y acepte los términos de Hola de uso.

    Esta acción descarga, se instala y se agrega una referencia toohello [paquete de NuGet del SDK de servicios de Azure IoT] en hello **ReadFileUploadNotification** proyecto.

1. Hola **Program.cs** , agregue Hola siguiendo las instrucciones en la parte superior de hello del archivo hello:

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. Agregar Hola después campos toohello **programa** clase. Sustituir el valor de marcador de posición de hello con la cadena de conexión de base de datos central de hello IoT desde [empezar a trabajar con el centro de IoT]:

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. Agregar Hola siguiendo el método toohello **programa** clase:

    ```csharp
    private async static void ReceiveFileUploadNotificationAsync()
    {
        var notificationReceiver = serviceClient.GetFileNotificationReceiver();

        Console.WriteLine("\nReceiving file upload notification from service");
        while (true)
        {
            var fileUploadNotification = await notificationReceiver.ReceiveAsync();
            if (fileUploadNotification == null) continue;

            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
            Console.ResetColor();

            await notificationReceiver.CompleteAsync(fileUploadNotification);
        }
    }
    ```

    Tenga en cuenta este patrón de recepción es Hola mismos mensajes de nube al dispositivo tooreceive usa uno de aplicación de dispositivo de hello.

1. Por último, agregue Hola después líneas toohello **Main** método:

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Ejecutar aplicaciones de Hola

Ahora está listo toorun aplicaciones de Hola.

1. Desde Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio**. Seleccione **proyectos de inicio múltiples**, a continuación, seleccione hello **iniciar** acción para **ReadFileUploadNotification** y **SimulatedDevice**.

1. Presione **F5**. Deberían iniciarse las dos aplicaciones. Debería ver carga Hola completado en la aplicación de una única consola y mensaje de notificación de carga de hello recibido por Hola otra aplicación de consola. Puede usar hello [portal de Azure] o toocheck del explorador de servidores de Visual Studio para la presencia de Hola de Hola cargado el archivo en su cuenta de almacenamiento de Azure.

    ![][50]

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo toouse Hola carga capacidades de centro de IoT toosimplify archivo cargas de dispositivos. Puede seguir tooexplore IoT hub características y escenarios con hello siguientes artículos:

* [Creación de un centro de IoT mediante programación][lnk-create-hub]
* [Introducción tooC SDK][lnk-c-sdk]
* [SDK de IoT de Azure][lnk-sdks]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Simular un dispositivo con IoT Edge][lnk-iotedge]

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

[portal de Azure]: https://portal.azure.com/

[Centro para desarrolladores de Azure IoT]: http://www.azure.com/develop/iot

[control de errores transitorios]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[paquete de NuGet del SDK de servicios de Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
