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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a><span data-ttu-id="3d287-104">Cargar archivos desde su dispositivo toohello la nube con el centro de IoT con .NET</span><span class="sxs-lookup"><span data-stu-id="3d287-104">Upload files from your device toohello cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="3d287-105">Este tutorial se basa en el código de hello de hello [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-csharp-csharp-c2d.md) tooshow tutorial también cómo toouse Hola capacidades de carga de archivos del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="3d287-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial tooshow you how toouse hello file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="3d287-106">En él se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="3d287-106">It shows you how to:</span></span>

- <span data-ttu-id="3d287-107">Proporcionar un dispositivo de forma segura con un identificador URI de blob de Azure para cargar un archivo.</span><span class="sxs-lookup"><span data-stu-id="3d287-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="3d287-108">Usar hello centro de IoT archivo carga notificaciones tootrigger procesar el archivo de hello en el back-end de aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d287-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="3d287-109">Hola [empezar a trabajar con el centro de IoT](iot-hub-csharp-csharp-getstarted.md) y [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-csharp-csharp-c2d.md) los tutoriales muestra hello dispositivo a la nube y en la nube al dispositivo funcionalidad de mensajería básica de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="3d287-109">hello [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="3d287-110">Hola [mensajes proceso dispositivo a la nube](iot-hub-csharp-csharp-process-d2c.md) tutorial describe una manera tooreliably almacenar dispositivo a la nube mensajes en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d287-110">hello [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="3d287-111">Sin embargo, en algunos escenarios no se puede asignar fácilmente datos Hola que los dispositivos de envío en hello relativamente pequeño dispositivo a la nube los mensajes que acepta el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="3d287-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="3d287-112">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3d287-112">For example:</span></span>

* <span data-ttu-id="3d287-113">Archivos grandes con imágenes</span><span class="sxs-lookup"><span data-stu-id="3d287-113">Large files that contain images</span></span>
* <span data-ttu-id="3d287-114">Vídeos</span><span class="sxs-lookup"><span data-stu-id="3d287-114">Videos</span></span>
* <span data-ttu-id="3d287-115">Datos de vibración muestreados con alta frecuencia</span><span class="sxs-lookup"><span data-stu-id="3d287-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="3d287-116">Cierto tipo de datos procesados previamente</span><span class="sxs-lookup"><span data-stu-id="3d287-116">Some form of preprocessed data</span></span>

<span data-ttu-id="3d287-117">Estos archivos suelen ser lote procesado en la nube de hello con herramientas como [Data Factory de Azure](../data-factory/index.md) o hello [Hadoop](../hdinsight/index.md) pila.</span><span class="sxs-lookup"><span data-stu-id="3d287-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="3d287-118">Si necesita archivos tooupload desde un dispositivo, todavía puede usar seguridad hello y la confiabilidad del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="3d287-118">When you need tooupload files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="3d287-119">Al final de Hola de este tutorial, ejecutar dos aplicaciones de consola. NET:</span><span class="sxs-lookup"><span data-stu-id="3d287-119">At hello end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="3d287-120">**SimulatedDevice**, una versión modificada de la aplicación hello creado en hello [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-csharp-csharp-c2d.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="3d287-120">**SimulatedDevice**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="3d287-121">Esta aplicación carga una toostorage de archivo mediante un URI de SAS proporcionados por el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="3d287-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="3d287-122">**ReadFileUploadNotification**, que recibe notificaciones de carga de archivos del Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="3d287-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="3d287-123">El Centro de IoT admite muchas plataformas de dispositivos y lenguajes (incluido C, Java y JavaScript), mediante los SDK de dispositivo IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d287-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="3d287-124">Consulte toohello [Centro para desarrolladores de Azure IoT] para obtener instrucciones paso a paso sobre cómo tooconnect su centro de IoT tooAzure de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3d287-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="3d287-125">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="3d287-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="3d287-126">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3d287-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="3d287-127">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="3d287-127">An active Azure account.</span></span> <span data-ttu-id="3d287-128">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="3d287-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="3d287-129">Carga de un archivo desde una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="3d287-129">Upload a file from a device app</span></span>

<span data-ttu-id="3d287-130">En esta sección, se modifica Hola del dispositivo que creó en [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-csharp-csharp-c2d.md) mensajes de nube al dispositivo tooreceive Hola centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="3d287-130">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="3d287-131">En Visual Studio, haga clic en hello **SimulatedDevice** proyecto de equipo y haga clic en **agregar**y, a continuación, haga clic en **elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="3d287-131">In Visual Studio, right-click hello **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="3d287-132">Navegar por el archivo de imagen tooan e incluirla en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3d287-132">Navigate tooan image file and include it in your project.</span></span> <span data-ttu-id="3d287-133">Este tutorial se da por supuesto que se denomina imagen hello `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="3d287-133">This tutorial assumes hello image is named `image.jpg`.</span></span>

1. <span data-ttu-id="3d287-134">Haga doble clic en la imagen de hello y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="3d287-134">Right-click on hello image, and then click **Properties**.</span></span> <span data-ttu-id="3d287-135">Asegúrese de que **copiar tooOutput directorio** se establece demasiado**copiar siempre**.</span><span class="sxs-lookup"><span data-stu-id="3d287-135">Make sure that **Copy tooOutput Directory** is set too**Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="3d287-136">Hola **Program.cs** , agregue Hola siguiendo las instrucciones en la parte superior de hello del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="3d287-136">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="3d287-137">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="3d287-137">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="3d287-138">Hola `UploadToBlobAsync` método toma en nombre de archivo de Hola y origen de la secuencia de hello archivo toobe cargado y controla Hola carga toostorage.</span><span class="sxs-lookup"><span data-stu-id="3d287-138">hello `UploadToBlobAsync` method takes in hello file name and stream source of hello file toobe uploaded and handles hello upload toostorage.</span></span> <span data-ttu-id="3d287-139">aplicación de consola de Hello muestra hello duración del archivo de hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="3d287-139">hello console app displays hello time it takes tooupload hello file.</span></span>

1. <span data-ttu-id="3d287-140">Agregar Hola siguiente método Hola **Main** método, justo antes de hello `Console.ReadLine()` línea:</span><span class="sxs-lookup"><span data-stu-id="3d287-140">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="3d287-141">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="3d287-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="3d287-142">En el código de producción, debe implementar directivas de reintento (por ejemplo, retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios].</span><span class="sxs-lookup"><span data-stu-id="3d287-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="3d287-143">Recepción de una notificación de carga de archivos</span><span class="sxs-lookup"><span data-stu-id="3d287-143">Receive a file upload notification</span></span>

<span data-ttu-id="3d287-144">En esta sección, se escribe una aplicación de consola de .NET que recibe mensajes de notificación de carga de archivos de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3d287-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="3d287-145">En la solución de Visual Studio actual hello, crear un proyecto de Windows de Visual C# mediante hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="3d287-145">In hello current Visual Studio solution, create a Visual C# Windows project by using hello **Console Application** project template.</span></span> <span data-ttu-id="3d287-146">Proyecto de hello Name **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="3d287-146">Name hello project **ReadFileUploadNotification**.</span></span>

    ![Nuevo proyecto en Visual Studio][2]

1. <span data-ttu-id="3d287-148">En el Explorador de soluciones, haga clic en hello **ReadFileUploadNotification** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="3d287-148">In Solution Explorer, right-click hello **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="3d287-149">Hola **Administrador de paquetes de NuGet** ventana, busque **Microsoft.Azure.Devices**, haga clic en **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="3d287-149">In hello **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span>

    <span data-ttu-id="3d287-150">Esta acción descarga, se instala y se agrega una referencia toohello [paquete de NuGet del SDK de servicios de Azure IoT] en hello **ReadFileUploadNotification** proyecto.</span><span class="sxs-lookup"><span data-stu-id="3d287-150">This action downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package] in hello **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="3d287-151">Hola **Program.cs** , agregue Hola siguiendo las instrucciones en la parte superior de hello del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="3d287-151">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="3d287-152">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="3d287-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="3d287-153">Sustituir el valor de marcador de posición de hello con la cadena de conexión de base de datos central de hello IoT desde [empezar a trabajar con el centro de IoT]:</span><span class="sxs-lookup"><span data-stu-id="3d287-153">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="3d287-154">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="3d287-154">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="3d287-155">Tenga en cuenta este patrón de recepción es Hola mismos mensajes de nube al dispositivo tooreceive usa uno de aplicación de dispositivo de hello.</span><span class="sxs-lookup"><span data-stu-id="3d287-155">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>

1. <span data-ttu-id="3d287-156">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="3d287-156">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="3d287-157">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="3d287-157">Run hello applications</span></span>

<span data-ttu-id="3d287-158">Ahora está listo toorun aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d287-158">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="3d287-159">Desde Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio**.</span><span class="sxs-lookup"><span data-stu-id="3d287-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="3d287-160">Seleccione **proyectos de inicio múltiples**, a continuación, seleccione hello **iniciar** acción para **ReadFileUploadNotification** y **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="3d287-160">Select **Multiple startup projects**, then select hello **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="3d287-161">Presione **F5**.</span><span class="sxs-lookup"><span data-stu-id="3d287-161">Press **F5**.</span></span> <span data-ttu-id="3d287-162">Deberían iniciarse las dos aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3d287-162">Both applications should start.</span></span> <span data-ttu-id="3d287-163">Debería ver carga Hola completado en la aplicación de una única consola y mensaje de notificación de carga de hello recibido por Hola otra aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="3d287-163">You should see hello upload completed in one console app and hello upload notification message received by hello other console app.</span></span> <span data-ttu-id="3d287-164">Puede usar hello [portal de Azure] o toocheck del explorador de servidores de Visual Studio para la presencia de Hola de Hola cargado el archivo en su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d287-164">You can use hello [Azure portal] or Visual Studio Server Explorer toocheck for hello presence of hello uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="3d287-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3d287-165">Next steps</span></span>

<span data-ttu-id="3d287-166">En este tutorial, ha aprendido cómo toouse Hola carga capacidades de centro de IoT toosimplify archivo cargas de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3d287-166">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="3d287-167">Puede seguir tooexplore IoT hub características y escenarios con hello siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="3d287-167">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="3d287-168">[Creación de un centro de IoT mediante programación][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="3d287-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="3d287-169">[Introducción tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="3d287-169">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="3d287-170">[SDK de IoT de Azure][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="3d287-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="3d287-171">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="3d287-171">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3d287-172">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="3d287-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

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
