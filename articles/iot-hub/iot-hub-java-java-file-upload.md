---
title: Carga de archivos desde dispositivos a Azure IoT Hub con Java | Microsoft Docs
description: "Cómo cargar archivos de un dispositivo a la nube mediante el SDK de dispositivo IoT de Azure para Java. Los archivos cargados se almacenan en un contenedor de blobs de Azure Storage."
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
ms.openlocfilehash: c917a3b3e16f1e84f202d6c87a04faf642266701
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub"></a><span data-ttu-id="0b786-104">Carga de archivos de un dispositivo a la nube con IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0b786-104">Upload files from your device to the cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="0b786-105">Este tutorial se basa en el código del tutorial sobre el [envío de mensajes de la nube a un dispositivo con IoT Hub](iot-hub-java-java-c2d.md) para mostrar cómo se usan las [funcionalidades de carga de archivos de IoT Hub](iot-hub-devguide-file-upload.md) para cargar un archivo en [Azure Blob Storage](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="0b786-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial to show you how to use the [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) to upload a file to [Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="0b786-106">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="0b786-106">The tutorial shows you how to:</span></span>

- <span data-ttu-id="0b786-107">Proporcionar un dispositivo de forma segura con un identificador URI de blob de Azure para cargar un archivo.</span><span class="sxs-lookup"><span data-stu-id="0b786-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="0b786-108">Usar las notificaciones de carga de archivo de IoT Hub para desencadenar el procesamiento del archivo en el back-end de aplicación.</span><span class="sxs-lookup"><span data-stu-id="0b786-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="0b786-109">Los tutoriales [Introducción a Iot Hub](iot-hub-java-java-getstarted.md) y [Envío de mensajes de nube a dispositivo con IoT Hub](iot-hub-java-java-c2d.md) muestran cómo usar la funcionalidad básica de mensajería de dispositivo a nube y de nube a dispositivo de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0b786-109">The [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="0b786-110">En el [tutorial de procesamiento de mensajes de dispositivo a nube](iot-hub-java-java-process-d2c.md) se describe una forma de almacenar de manera confiable los mensajes enviados del dispositivo a la nube en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="0b786-110">The [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="0b786-111">Sin embargo, en algunos casos no se pueden asignar fácilmente los datos de que los dispositivos envían en los mensajes de dispositivo a nube con un tamaño relativamente reducido que acepta el Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0b786-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="0b786-112">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0b786-112">For example:</span></span>

* <span data-ttu-id="0b786-113">Archivos grandes con imágenes</span><span class="sxs-lookup"><span data-stu-id="0b786-113">Large files that contain images</span></span>
* <span data-ttu-id="0b786-114">Vídeos</span><span class="sxs-lookup"><span data-stu-id="0b786-114">Videos</span></span>
* <span data-ttu-id="0b786-115">Datos de vibración muestreados con alta frecuencia</span><span class="sxs-lookup"><span data-stu-id="0b786-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="0b786-116">Algún tipo de datos de procesamiento previo.</span><span class="sxs-lookup"><span data-stu-id="0b786-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="0b786-117">Dichos archivos se suelen procesar por lotes en la nube mediante herramientas como [Azure Data Factory](../data-factory/index.md) o la pila [Hadoop](../hdinsight/index.md).</span><span class="sxs-lookup"><span data-stu-id="0b786-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/index.md) or the [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="0b786-118">Cuando necesite cargar archivos desde un dispositivo, todavía puede usar la seguridad y confiabilidad de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0b786-118">When you need to upland files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="0b786-119">Al final de este tutorial, ejecutará dos aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="0b786-119">At the end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="0b786-120">**simulated-device**, una versión modificada de la aplicación que creó en el tutorial [Envío de mensajes de nube a dispositivo con IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="0b786-120">**simulated-device**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="0b786-121">Esta aplicación carga un archivo en el almacenamiento mediante un identificador URI de SAS proporcionado por el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0b786-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="0b786-122">**read-file-upload-notification**, que recibe notificaciones de carga de archivos de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0b786-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="0b786-123">IoT Hub admite muchas plataformas de dispositivos y lenguajes (incluido C, .NET y JavaScript), mediante los SDK de dispositivo IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="0b786-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="0b786-124">Consulte el [Centro para desarrolladores de IoT de Azure] para obtener instrucciones paso a paso sobre cómo conectar el dispositivo al Centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="0b786-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="0b786-125">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0b786-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="0b786-126">La versión más reciente de [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="0b786-126">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="0b786-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="0b786-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="0b786-128">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="0b786-128">An active Azure account.</span></span> <span data-ttu-id="0b786-129">(En caso de no tener ninguna, puede crear una [cuenta gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="0b786-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="0b786-130">Carga de un archivo desde una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="0b786-130">Upload a file from a device app</span></span>

<span data-ttu-id="0b786-131">En esta sección, modificará la aplicación de dispositivo que creó en [Envío de mensajes de nube a dispositivo con IoT Hub](iot-hub-java-java-c2d.md) para cargar un archivo en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0b786-131">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) to upload a file to IoT hub.</span></span>

1. <span data-ttu-id="0b786-132">Copie un archivo de imagen a la carpeta `simulated-device` llámelo `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="0b786-132">Copy an image file to the `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="0b786-133">Con un editor de texto, abra el archivo `simulated-device\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="0b786-133">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="0b786-134">Agregue la declaración de variable a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="0b786-134">Add the variable declaration to the **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="0b786-135">Para procesar mensajes de devolución de llamada de estado de carga de archivos, agregue la siguiente clase anidada a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="0b786-135">To process file upload status callback messages, add the following nested class to the **App** class:</span></span>

    ```java
    // Define a callback method to print status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to file upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="0b786-136">Para cargar imágenes en IoT Hub, agregue el método siguiente a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="0b786-136">To upload images to IoT Hub, add the following method to the **App** class to upload images to IoT Hub:</span></span>

    ```java
    // Use IoT Hub to upload a file asynchronously to Azure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="0b786-137">Modifique el método **principal** para llamar al método **uploadFile** tal como se muestra en el fragmento de código siguiente:</span><span class="sxs-lookup"><span data-stu-id="0b786-137">Modify the **main** method to call the **uploadFile** method as shown in the following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get the filename and start the upload.
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

1. <span data-ttu-id="0b786-138">Use el siguiente comando para compilar la aplicación **simulated-device** y busque errores:</span><span class="sxs-lookup"><span data-stu-id="0b786-138">Use the following command to build the **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="0b786-139">Recepción de una notificación de carga de archivos</span><span class="sxs-lookup"><span data-stu-id="0b786-139">Receive a file upload notification</span></span>

<span data-ttu-id="0b786-140">En esta sección, se crea una aplicación de consola de Java que recibe mensajes de notificación de carga de archivos de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0b786-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="0b786-141">Necesita la cadena de conexión **iothubowner** para que IoT Hub complete esta sección.</span><span class="sxs-lookup"><span data-stu-id="0b786-141">You need the **iothubowner** connection string for your IoT Hub to complete this section.</span></span> <span data-ttu-id="0b786-142">Puede encontrar la cadena de conexión en [Azure Portal](https://portal.azure.com/) o en la hoja **Directiva de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="0b786-142">You can find the connection string in the [Azure portal](https://portal.azure.com/) on the **Shared access policy** blade.</span></span>

1. <span data-ttu-id="0b786-143">Cree un proyecto de Maven denominado **read-file-upload-notification** mediante el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="0b786-143">Create a Maven project called **read-file-upload-notification** using the following command at your command prompt.</span></span> <span data-ttu-id="0b786-144">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="0b786-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="0b786-145">En el símbolo del sistema, vaya a la carpeta `read-file-upload-notification` nueva.</span><span class="sxs-lookup"><span data-stu-id="0b786-145">At your command prompt, navigate to the new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="0b786-146">Con un editor de texto, abra el archivo `pom.xml` de la carpeta `read-file-upload-notification` y agregue la dependencia siguiente al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="0b786-146">Using a text editor, open the `pom.xml` file in the `read-file-upload-notification` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="0b786-147">Esto le permite usar el paquete **iothub-java-service-client** en la aplicación para comunicarse con el servicio IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="0b786-147">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="0b786-148">Puede comprobar la versión más reciente de **iot-service-client** mediante la [funcionalidad de búsqueda de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="0b786-148">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="0b786-149">Guarde y cierre el archivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="0b786-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="0b786-150">Con un editor de texto, abra el archivo `read-file-upload-notification\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="0b786-150">Using a text editor, open the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="0b786-151">Agregue las siguientes instrucciones **import** al archivo:</span><span class="sxs-lookup"><span data-stu-id="0b786-151">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="0b786-152">Agregue las siguientes variables de nivel de clase a la clase **App** :</span><span class="sxs-lookup"><span data-stu-id="0b786-152">Add the following class-level variables to the **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="0b786-153">Para imprimir la información acerca de la carga de archivos en la consola, agregue la siguiente clase anidada para la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="0b786-153">To print information about the file upload to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Create a thread to receive file upload notifications.
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

1. <span data-ttu-id="0b786-154">Para iniciar el subproceso que realiza escuchas para las notificaciones de carga de archivos, agregue el código siguiente al método **principal**:</span><span class="sxs-lookup"><span data-stu-id="0b786-154">To start the thread that listens for file upload notifications, add the following code to the **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from the ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start the thread to receive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER to exit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="0b786-155">Guarde y cierre el archivo `read-file-upload-notification\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="0b786-155">Save and close the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="0b786-156">Use el siguiente comando para compilar la aplicación **read-file-upload-notification** y busque errores:</span><span class="sxs-lookup"><span data-stu-id="0b786-156">Use the following command to build the **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-the-applications"></a><span data-ttu-id="0b786-157">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="0b786-157">Run the applications</span></span>

<span data-ttu-id="0b786-158">Ahora está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0b786-158">Now you are ready to run the applications.</span></span>

<span data-ttu-id="0b786-159">En la carpeta `read-file-upload-notification` del símbolo del sistema, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0b786-159">At a command prompt in the `read-file-upload-notification` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="0b786-160">En la carpeta `simulated-device` del símbolo del sistema, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0b786-160">At a command prompt in the `simulated-device` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="0b786-161">En la captura de pantalla siguiente se muestra la salida de la aplicación **simulated-device**:</span><span class="sxs-lookup"><span data-stu-id="0b786-161">The following screenshot shows the output from the **simulated-device** app:</span></span>

![Salida de la aplicación simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="0b786-163">En la captura de pantalla siguiente se muestra la salida de la aplicación **read-file-upload-notification**:</span><span class="sxs-lookup"><span data-stu-id="0b786-163">The following screenshot shows the output from the **read-file-upload-notification** app:</span></span>

![Salida de la aplicación read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="0b786-165">Puede usar el portal para ver el archivo cargado en el contenedor de almacenamiento que configuró:</span><span class="sxs-lookup"><span data-stu-id="0b786-165">You can use the portal to view the uploaded file in the storage container you configured:</span></span>

![Archivo cargado](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="0b786-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b786-167">Next steps</span></span>

<span data-ttu-id="0b786-168">En este tutorial ha aprendido a usar la funcionalidad de carga de archivos de IoT Hub para simplificar la carga de archivos desde los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="0b786-168">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="0b786-169">Puede continuar explorando las características y los escenarios del centro de IoT con los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="0b786-169">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="0b786-170">[Creación de un centro de IoT mediante programación][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="0b786-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="0b786-171">[Introducción al SDK de C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="0b786-171">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="0b786-172">[SDK de IoT de Azure][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="0b786-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="0b786-173">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="0b786-173">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0b786-174">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="0b786-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Centro para desarrolladores de IoT de Azure]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


