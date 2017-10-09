---
title: archivos de aaaUpload desde dispositivos tooAzure centro de IoT con Java | Documentos de Microsoft
description: "¿Cómo tooupload archivos desde una dispositivo toohello la nube mediante dispositivos de IoT de Azure SDK para Java. Los archivos cargados se almacenan en un contenedor de blobs de Azure Storage."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: e305fe61bf7ca0aeb2c092bc2c7efebdc78d4f68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a><span data-ttu-id="03ee5-104">Cargar archivos desde su dispositivo toohello la nube con el centro de IoT</span><span class="sxs-lookup"><span data-stu-id="03ee5-104">Upload files from your device toohello cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="03ee5-105">Este tutorial se basa en el código de hello de hello [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-java-java-c2d.md) tooshow tutorial cómo hello toouse [archivo capacidades de carga del centro de IoT](iot-hub-devguide-file-upload.md) tooupload un archivo demasiado[ Almacenamiento de blobs de Azure](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="03ee5-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial tooshow you how toouse hello [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) tooupload a file too[Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="03ee5-106">Hola tutorial le muestra cómo para:</span><span class="sxs-lookup"><span data-stu-id="03ee5-106">hello tutorial shows you how to:</span></span>

- <span data-ttu-id="03ee5-107">Proporcionar un dispositivo de forma segura con un identificador URI de blob de Azure para cargar un archivo.</span><span class="sxs-lookup"><span data-stu-id="03ee5-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="03ee5-108">Usar hello centro de IoT archivo carga notificaciones tootrigger procesar el archivo de hello en el back-end de aplicación.</span><span class="sxs-lookup"><span data-stu-id="03ee5-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="03ee5-109">Hola [empezar a trabajar con el centro de IoT](iot-hub-java-java-getstarted.md) y [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-java-java-c2d.md) los tutoriales muestra hello dispositivo a la nube y en la nube al dispositivo funcionalidad de mensajería básica de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="03ee5-109">hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="03ee5-110">Hola [mensajes proceso dispositivo a la nube](iot-hub-java-java-process-d2c.md) tutorial describe una manera tooreliably almacenar dispositivo a la nube mensajes en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="03ee5-110">hello [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="03ee5-111">Sin embargo, en algunos escenarios no se puede asignar fácilmente datos Hola que los dispositivos de envío en hello relativamente pequeño dispositivo a la nube los mensajes que acepta el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="03ee5-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="03ee5-112">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="03ee5-112">For example:</span></span>

* <span data-ttu-id="03ee5-113">Archivos grandes con imágenes</span><span class="sxs-lookup"><span data-stu-id="03ee5-113">Large files that contain images</span></span>
* <span data-ttu-id="03ee5-114">Vídeos</span><span class="sxs-lookup"><span data-stu-id="03ee5-114">Videos</span></span>
* <span data-ttu-id="03ee5-115">Datos de vibración muestreados con alta frecuencia</span><span class="sxs-lookup"><span data-stu-id="03ee5-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="03ee5-116">Algún tipo de datos de procesamiento previo.</span><span class="sxs-lookup"><span data-stu-id="03ee5-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="03ee5-117">Estos archivos suelen ser lote procesado en la nube de hello con herramientas como [Data Factory de Azure](../data-factory/index.md) o hello [Hadoop](../hdinsight/index.md) pila.</span><span class="sxs-lookup"><span data-stu-id="03ee5-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="03ee5-118">Cuando necesite tooupland archivos desde un dispositivo, todavía puede usar seguridad de Hola y la confiabilidad del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="03ee5-118">When you need tooupland files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="03ee5-119">Al final de Hola de este tutorial, ejecutar dos aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="03ee5-119">At hello end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="03ee5-120">**dispositivo simulado**, una versión modificada de la aplicación hello creado en el tutorial de hello [mensajes de envío en la nube al dispositivo con el centro de IoT].</span><span class="sxs-lookup"><span data-stu-id="03ee5-120">**simulated-device**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="03ee5-121">Esta aplicación carga una toostorage de archivo mediante un URI de SAS proporcionados por el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="03ee5-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="03ee5-122">**read-file-upload-notification**, que recibe notificaciones de carga de archivos de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="03ee5-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="03ee5-123">IoT Hub admite muchas plataformas de dispositivos y lenguajes (incluido C, .NET y JavaScript), mediante los SDK de dispositivo IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="03ee5-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="03ee5-124">Consulte toohello [Centro para desarrolladores de Azure IoT] para obtener instrucciones paso a paso sobre cómo tooconnect su centro de IoT tooAzure de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="03ee5-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="03ee5-125">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="03ee5-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="03ee5-126">Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="03ee5-126">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="03ee5-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="03ee5-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="03ee5-128">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="03ee5-128">An active Azure account.</span></span> <span data-ttu-id="03ee5-129">(En caso de no tener ninguna, puede crear una [cuenta gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="03ee5-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="03ee5-130">Carga de un archivo desde una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="03ee5-130">Upload a file from a device app</span></span>

<span data-ttu-id="03ee5-131">En esta sección, se modifica Hola del dispositivo que creó en [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-java-java-c2d.md) tooupload un concentrador de tooIoT de archivo.</span><span class="sxs-lookup"><span data-stu-id="03ee5-131">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tooupload a file tooIoT hub.</span></span>

1. <span data-ttu-id="03ee5-132">Copiar un toohello del archivo de imagen `simulated-device` carpeta y cambie su nombre `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="03ee5-132">Copy an image file toohello `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="03ee5-133">Con un editor de texto, abra hello `simulated-device\src\main\java\com\mycompany\app\App.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="03ee5-133">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="03ee5-134">Agregar toohello de declaración de variable de hello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="03ee5-134">Add hello variable declaration toohello **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="03ee5-135">tooprocess mensajes de devolución de llamada de estado de carga de archivos, agregue la siguiente Hola anidados clase toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="03ee5-135">tooprocess file upload status callback messages, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="03ee5-136">tooupload imágenes tooIoT concentrador, agregar Hola siguiendo el método toohello **aplicación** tooupload clase imágenes tooIoT concentrador:</span><span class="sxs-lookup"><span data-stu-id="03ee5-136">tooupload images tooIoT Hub, add hello following method toohello **App** class tooupload images tooIoT Hub:</span></span>

    ```java
    // Use IoT Hub tooupload a file asynchronously tooAzure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="03ee5-137">Modificar hello **principal** Hola de método toocall **uploadFile** método tal como se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="03ee5-137">Modify hello **main** method toocall hello **uploadFile** method as shown in hello following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get hello filename and start hello upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. <span data-ttu-id="03ee5-138">Siguiente Hola de uso del comando hello toobuild **dispositivo simulado** aplicación y busque errores:</span><span class="sxs-lookup"><span data-stu-id="03ee5-138">Use hello following command toobuild hello **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="03ee5-139">Recepción de una notificación de carga de archivos</span><span class="sxs-lookup"><span data-stu-id="03ee5-139">Receive a file upload notification</span></span>

<span data-ttu-id="03ee5-140">En esta sección, se crea una aplicación de consola de Java que recibe mensajes de notificación de carga de archivos de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="03ee5-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="03ee5-141">Necesita hello **iothubowner** cadena de conexión de su centro de IoT toocomplete en esta sección.</span><span class="sxs-lookup"><span data-stu-id="03ee5-141">You need hello **iothubowner** connection string for your IoT Hub toocomplete this section.</span></span> <span data-ttu-id="03ee5-142">Puede encontrar la cadena de conexión de Hola Hola [portal de Azure](https://portal.azure.com/) en hello **la directiva de acceso compartido** hoja.</span><span class="sxs-lookup"><span data-stu-id="03ee5-142">You can find hello connection string in hello [Azure portal](https://portal.azure.com/) on hello **Shared access policy** blade.</span></span>

1. <span data-ttu-id="03ee5-143">Cree un proyecto de Maven denominado **-archivo-cargar-notificación de lectura de** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="03ee5-143">Create a Maven project called **read-file-upload-notification** using hello following command at your command prompt.</span></span> <span data-ttu-id="03ee5-144">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="03ee5-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="03ee5-145">En el símbolo del sistema, navegue toohello nueva `read-file-upload-notification` carpeta.</span><span class="sxs-lookup"><span data-stu-id="03ee5-145">At your command prompt, navigate toohello new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="03ee5-146">Con un editor de texto, abra hello `pom.xml` archivo Hola `read-file-upload-notification` carpeta y agregue Hola después dependencia toohello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="03ee5-146">Using a text editor, open hello `pom.xml` file in hello `read-file-upload-notification` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="03ee5-147">Agregar dependencia Hola permite hello toouse **el centro de IOT java servicio cliente** paquete en su toocommunicate de aplicación con el servicio del centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="03ee5-147">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="03ee5-148">Puede comprobar la versión más reciente de Hola de **cliente del servicio de iot** con [búsqueda Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="03ee5-148">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="03ee5-149">Guarde y cierre hello `pom.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="03ee5-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="03ee5-150">Con un editor de texto, abra hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="03ee5-150">Using a text editor, open hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="03ee5-151">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="03ee5-151">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="03ee5-152">Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="03ee5-152">Add hello following class-level variables toohello **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="03ee5-153">tooprint información acerca de la consola de toohello de carga de archivo hello, agregue el siguiente de hello anidados clase toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="03ee5-153">tooprint information about hello file upload toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Create a thread tooreceive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="03ee5-154">subproceso de hello toostart que realiza escuchas para las notificaciones de carga de archivos, agregar Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="03ee5-154">toostart hello thread that listens for file upload notifications, add hello following code toohello **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from hello ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start hello thread tooreceive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER tooexit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="03ee5-155">Guarde y cierre hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="03ee5-155">Save and close hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="03ee5-156">Siguiente Hola de uso del comando hello toobuild **-archivo-cargar-notificación de lectura de** aplicación y busque errores:</span><span class="sxs-lookup"><span data-stu-id="03ee5-156">Use hello following command toobuild hello **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="03ee5-157">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="03ee5-157">Run hello applications</span></span>

<span data-ttu-id="03ee5-158">Ahora está listo toorun aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="03ee5-158">Now you are ready toorun hello applications.</span></span>

<span data-ttu-id="03ee5-159">En un símbolo del sistema en hello `read-file-upload-notification` carpeta, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="03ee5-159">At a command prompt in hello `read-file-upload-notification` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="03ee5-160">En un símbolo del sistema en hello `simulated-device` carpeta, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="03ee5-160">At a command prompt in hello `simulated-device` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="03ee5-161">Hello captura de pantalla siguiente muestra la salida de hello de hello **dispositivo simulado** aplicación:</span><span class="sxs-lookup"><span data-stu-id="03ee5-161">hello following screenshot shows hello output from hello **simulated-device** app:</span></span>

![Salida de la aplicación simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="03ee5-163">Hello captura de pantalla siguiente muestra la salida de hello de hello **-archivo-cargar-notificación de lectura de** aplicación:</span><span class="sxs-lookup"><span data-stu-id="03ee5-163">hello following screenshot shows hello output from hello **read-file-upload-notification** app:</span></span>

![Salida de la aplicación read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="03ee5-165">Se puede utilizar hello tooview portal Hola cargado archivo contenedor de almacenamiento de Hola que configuró:</span><span class="sxs-lookup"><span data-stu-id="03ee5-165">You can use hello portal tooview hello uploaded file in hello storage container you configured:</span></span>

![Archivo cargado](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="03ee5-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03ee5-167">Next steps</span></span>

<span data-ttu-id="03ee5-168">En este tutorial, ha aprendido cómo toouse Hola carga capacidades de centro de IoT toosimplify archivo cargas de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="03ee5-168">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="03ee5-169">Puede seguir tooexplore IoT hub características y escenarios con hello siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="03ee5-169">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="03ee5-170">[Creación de un centro de IoT mediante programación][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="03ee5-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="03ee5-171">[Introducción tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="03ee5-171">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="03ee5-172">[SDK de IoT de Azure][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="03ee5-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="03ee5-173">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="03ee5-173">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="03ee5-174">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="03ee5-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Centro para desarrolladores de Azure IoT]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


