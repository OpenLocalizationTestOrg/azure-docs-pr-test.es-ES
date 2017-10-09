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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a>Cargar archivos desde su dispositivo toohello la nube con el centro de IoT

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Este tutorial se basa en el código de hello de hello [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-java-java-c2d.md) tooshow tutorial cómo hello toouse [archivo capacidades de carga del centro de IoT](iot-hub-devguide-file-upload.md) tooupload un archivo demasiado[ Almacenamiento de blobs de Azure](../storage/index.md). Hola tutorial le muestra cómo para:

- Proporcionar un dispositivo de forma segura con un identificador URI de blob de Azure para cargar un archivo.
- Usar hello centro de IoT archivo carga notificaciones tootrigger procesar el archivo de hello en el back-end de aplicación.

Hola [empezar a trabajar con el centro de IoT](iot-hub-java-java-getstarted.md) y [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-java-java-c2d.md) los tutoriales muestra hello dispositivo a la nube y en la nube al dispositivo funcionalidad de mensajería básica de centro de IoT. Hola [mensajes proceso dispositivo a la nube](iot-hub-java-java-process-d2c.md) tutorial describe una manera tooreliably almacenar dispositivo a la nube mensajes en el almacenamiento de blobs de Azure. Sin embargo, en algunos escenarios no se puede asignar fácilmente datos Hola que los dispositivos de envío en hello relativamente pequeño dispositivo a la nube los mensajes que acepta el centro de IoT. Por ejemplo:

* Archivos grandes con imágenes
* Vídeos
* Datos de vibración muestreados con alta frecuencia
* Algún tipo de datos de procesamiento previo.

Estos archivos suelen ser lote procesado en la nube de hello con herramientas como [Data Factory de Azure](../data-factory/index.md) o hello [Hadoop](../hdinsight/index.md) pila. Cuando necesite tooupland archivos desde un dispositivo, todavía puede usar seguridad de Hola y la confiabilidad del centro de IoT.

Al final de Hola de este tutorial, ejecutar dos aplicaciones de consola de Java:

* **dispositivo simulado**, una versión modificada de la aplicación hello creado en el tutorial de hello [mensajes de envío en la nube al dispositivo con el centro de IoT]. Esta aplicación carga una toostorage de archivo mediante un URI de SAS proporcionados por el centro de IoT.
* **read-file-upload-notification**, que recibe notificaciones de carga de archivos de IoT Hub.

> [!NOTE]
> IoT Hub admite muchas plataformas de dispositivos y lenguajes (incluido C, .NET y JavaScript), mediante los SDK de dispositivo IoT de Azure. Consulte toohello [Centro para desarrolladores de Azure IoT] para obtener instrucciones paso a paso sobre cómo tooconnect su centro de IoT tooAzure de dispositivo.

toocomplete este tutorial, necesita Hola siguientes:

* Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Una cuenta de Azure activa. (En caso de no tener ninguna, puede crear una [cuenta gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos).

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Carga de un archivo desde una aplicación de dispositivo

En esta sección, se modifica Hola del dispositivo que creó en [enviar mensajes en la nube al dispositivo con el centro de IoT](iot-hub-java-java-c2d.md) tooupload un concentrador de tooIoT de archivo.

1. Copiar un toohello del archivo de imagen `simulated-device` carpeta y cambie su nombre `myimage.png`.

1. Con un editor de texto, abra hello `simulated-device\src\main\java\com\mycompany\app\App.java` archivo.

1. Agregar toohello de declaración de variable de hello **aplicación** clase:

    ```java
    private static String fileName = "myimage.png";
    ```

1. tooprocess mensajes de devolución de llamada de estado de carga de archivos, agregue la siguiente Hola anidados clase toohello **aplicación** clase:

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. tooupload imágenes tooIoT concentrador, agregar Hola siguiendo el método toohello **aplicación** tooupload clase imágenes tooIoT concentrador:

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

1. Modificar hello **principal** Hola de método toocall **uploadFile** método tal como se muestra en el siguiente fragmento de código de hello:

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

1. Siguiente Hola de uso del comando hello toobuild **dispositivo simulado** aplicación y busque errores:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a>Recepción de una notificación de carga de archivos

En esta sección, se crea una aplicación de consola de Java que recibe mensajes de notificación de carga de archivos de IoT Hub.

Necesita hello **iothubowner** cadena de conexión de su centro de IoT toocomplete en esta sección. Puede encontrar la cadena de conexión de Hola Hola [portal de Azure](https://portal.azure.com/) en hello **la directiva de acceso compartido** hoja.

1. Cree un proyecto de Maven denominado **-archivo-cargar-notificación de lectura de** mediante el siguiente comando en el símbolo del sistema de Hola. Observe que este es un comando único y largo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. En el símbolo del sistema, navegue toohello nueva `read-file-upload-notification` carpeta.

1. Con un editor de texto, abra hello `pom.xml` archivo Hola `read-file-upload-notification` carpeta y agregue Hola después dependencia toohello **dependencias** nodo. Agregar dependencia Hola permite hello toouse **el centro de IOT java servicio cliente** paquete en su toocommunicate de aplicación con el servicio del centro de IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Puede comprobar la versión más reciente de Hola de **cliente del servicio de iot** con [búsqueda Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Guarde y cierre hello `pom.xml` archivo.

1. Con un editor de texto, abra hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` archivo.

1. Agregue los siguiente hello **importar** archivo toohello de instrucciones:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase:

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. tooprint información acerca de la consola de toohello de carga de archivo hello, agregue el siguiente de hello anidados clase toohello **aplicación** clase:

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

1. subproceso de hello toostart que realiza escuchas para las notificaciones de carga de archivos, agregar Hola después código toohello **principal** método:

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

1. Guarde y cierre hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` archivo.

1. Siguiente Hola de uso del comando hello toobuild **-archivo-cargar-notificación de lectura de** aplicación y busque errores:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Ejecutar aplicaciones de Hola

Ahora está listo toorun aplicaciones de Hola.

En un símbolo del sistema en hello `read-file-upload-notification` carpeta, ejecute el siguiente comando de hello:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

En un símbolo del sistema en hello `simulated-device` carpeta, ejecute el siguiente comando de hello:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Hello captura de pantalla siguiente muestra la salida de hello de hello **dispositivo simulado** aplicación:

![Salida de la aplicación simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

Hello captura de pantalla siguiente muestra la salida de hello de hello **-archivo-cargar-notificación de lectura de** aplicación:

![Salida de la aplicación read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

Se puede utilizar hello tooview portal Hola cargado archivo contenedor de almacenamiento de Hola que configuró:

![Archivo cargado](media/iot-hub-java-java-upload/uploaded-file.png)

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


