---
title: "aplicación de aaaOn local con el almacenamiento de blobs (Java) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo una aplicación de consola que carga una imagen tooAzure y, a continuación, muestra toocreate Hola imagen en el explorador. Ejemplos de código en Java."
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a>Aplicación local con almacenamiento en blobs
## <a name="overview"></a>Información general
Hello en el ejemplo siguiente se muestra cómo puede usar el almacenamiento de Azure para almacenar imágenes en Azure. código de Hello en este artículo es para una aplicación de consola que carga una imagen tooAzure y, a continuación, crea un archivo HTML que muestra la imagen de hello en el explorador.

## <a name="prerequisites"></a>Requisitos previos
* Un kit para desarrolladores de Java (JDK) v 1.6 o posteriores instalado.
* Hello Azure SDK está instalado.
* Hola JAR Hola para bibliotecas de Azure para Java y cualquier dependencia aplicable archivos JAR, se instala y está en la ruta de acceso de compilación de hello utilizado por el compilador de Java. Para obtener información acerca de cómo instalar Hola bibliotecas de Azure para Java, consulte [descarga hello Azure SDK para Java](../java-download-azure-sdk.md).
* Una cuenta de almacenamiento configurada en Azure. Hello nombre de cuenta y clave de cuenta de almacenamiento de Hola se utilizará por código de hello en este artículo. Vea [cómo tooCreate una cuenta de almacenamiento](storage-create-storage-account.md#create-a-storage-account) para obtener información acerca de cómo crear una cuenta de almacenamiento, y [visualizar y copiar claves de acceso de almacenamiento](storage-create-storage-account.md#view-and-copy-storage-access-keys) para obtener información acerca de cómo recuperar la clave de la cuenta de hello.
* Ha creado un archivo de imagen local con el nombre almacenado en c: de ruta de acceso de hello\\myimages\\image1.jpg. O bien, modificar el **FileInputStream** constructor en el ejemplo de Hola toouse un nombre de ruta de acceso y de otra imagen.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a>tooupload de almacenamiento de blobs de Azure toouse un archivo
A continuación se presenta un procedimiento paso a paso. Si desea que tooskip con antelación, todo código de hello se presenta más adelante en este artículo.

Comienzo del código de hello mediante la inclusión de importaciones para clases de almacenamiento de Azure principales de hello, clases de cliente de hello blobs de Azure, las clases de E/S de Java de Hola y Hola **URISyntaxException** clase.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

Declarar una clase denominada **StorageSample**e incluyen el corchete de apertura de hello, **{**.

```java
public class StorageSample {
```

Dentro de hello **StorageSample** clase, declare una variable de cadena que contendrá el protocolo de extremo de Hola de forma predeterminada, el nombre de cuenta de almacenamiento y su clave de acceso de almacenamiento, como se especifica en la cuenta de almacenamiento de Azure. Reemplace los valores de marcador de posición de hello **su\_cuenta\_nombre** y **su\_cuenta\_clave** con su propio nombre de cuenta y la clave de cuenta, respectivamente.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

Agregue la declaración para **principal**, incluyen un **intente** bloquear e incluya el corchete de apertura necesarios de hello, **{**.

```java
    public static void main(String[] args)
    {
        try
        {
```

Declarar variables de hello después del tipo (Hola son descripciones de cómo se utilizan en este ejemplo):

* **CloudStorageAccount**: Hola tooinitialize usado cuenta objeto con el nombre de la cuenta de almacenamiento de Azure y la clave y el toocreate el objeto de cliente de blob.
* **CloudBlobClient**: utiliza el servicio de blob de tooaccess Hola.
* **CloudBlobContainer**: toocreate usa un contenedor de blobs, enumerar los blobs en un contenedor hello y delete Hola contenedor.
* **CloudBlockBlob**: tooupload usa un contenedor de toothe del archivo de imagen local.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

Asignar un valor toohello **cuenta** variable.

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

Asignar un valor toohello **serviceClient** variable.

```java
serviceClient = account.createCloudBlobClient();
```

Asignar un valor toohello **contenedor** variable. Nos pondremos en un contenedor de tooa referencia denominado **gettingstarted**.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

Crear contenedor de Hola. Este método creará el contenedor de hello si no existe (y devolver **true**). Si existe el contenedor de hello, devolverá **false**. Una alternativa demasiado**createIfNotExists** es hello **crear** método (que se devolverá un error si ya existe el contenedor de hello).

```java
container.createIfNotExists();
```

Establecer el acceso anónimo para el contenedor de Hola.

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Obtener un blob en bloques toohello referencia, que representará el blob de hello en el almacenamiento de Azure.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

Hola de uso **archivo** constructor tooget un archivo de referencia toohello creada localmente que va a cargar. Asegúrese de que ha creado este archivo antes de ejecutar código de hello.

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

Cargando archivo local de Hola a través de una llamada toohello **CloudBlockBlob.upload** método. Hola primera toohello parámetro **CloudBlockBlob.upload** método es un **FileInputStream** ese archivo local de Hola de representa será cargado tooAzure almacenamiento del objeto. Hola segundo parámetro es tamaño hello, en bytes, del archivo hello.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

Llamar a una función auxiliar denominada **MakeHTMLPage**, página toomake una HTML básica que contiene un  **&lt;imagen&gt;**  elemento con blob toohello de conjunto de origen de Hola que se encuentra ahora en Azure cuenta de almacenamiento. Hola código para **MakeHTMLPage** se explicará más adelante en este artículo.

```java
MakeHTMLPage(container);
```

Imprimir un mensaje de estado e información sobre Hola creada la página HTML.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

Hola cerrar **intente** bloque insertando un corchete de cierre: **}**

Identificador hello siguientes excepciones:

* **FileNotFoundException**: Hola puede producir **FileInputStream** o **clase FileOutputStream** constructores.
* **StorageException**: biblioteca de almacenamiento de Azure cliente hello puede producir.
* **URISyntaxException**: Hola puede producir **ListBlobItem.getUri** método.
* **Exception**: control de una excepción genérica.

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Cierre **main** mediante la inserción de un corchete de cierre: **}**.

Crear un método denominado **MakeHTMLPage** página toocreate una HTML básica. Este método tiene un parámetro de tipo **CloudBlobContainer**, que será usado tooiterate a través de la lista de Hola de blobs cargados. Este método producirá excepciones de tipo **FileNotFoundException**, que puede producir hello **clase FileOutputStream** constructor, y **URISyntaxException**, lo que puede se produce por hello **ListBlobItem.getUri** método. Incluya el corchete de apertura, **{**.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

Cree un archivo local llamado **index.html**.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Escribir en el archivo local toohello, agregar Hola  **&lt;html&gt;**,  **&lt;encabezado&gt;**, y  **&lt;cuerpo&gt;**  elementos.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

Recorrer en iteración la lista de Hola de blobs cargados. Para cada blob, en la página de hello HTML crear un  **&lt;img&gt;**  elemento que tiene su **src** atributo enviado al URI de blob de Hola Hola tal como existe en su cuenta de almacenamiento de Azure.
Aunque ha agregado una sola imagen en este ejemplo, si agregara más, este código iteraría todas ellas.

Para simplificar, en este ejemplo se asume que cada blob cargado es una imagen. Si ha actualizado blobs que no sean imágenes o blobs de página en lugar de blobs en bloques, ajustar el código de hello según sea necesario.

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

Hola cerrar  **&lt;cuerpo&gt;**  hello y elemento  **&lt;html&gt;**  elemento.

```java
stream.println("</body>");
stream.println("</html>");
```

Archivo local Hola cerrar.

```java
stream.close();
```

Cierre **MakeHTMLPage** mediante la inserción de un corchete de cierre: **}**.

Cierre **StorageSample** mediante la inserción de un corchete de cierre: **}**.

Hola aquí te mostramos código completo de hello en este ejemplo. Recuerde que los valores de marcador de posición de hello toomodify **su\_cuenta\_nombre** y **su\_cuenta\_clave** toouse su nombre de cuenta y la cuenta la clave, respectivamente.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

En suma toouploading su almacenamiento tooAzure del archivo de imagen local, código de ejemplo de Hola crea un namedindex.html de archivos local, que puede abrir en el explorador toosee la imagen cargada.

Dado que el código de hello contiene el nombre de cuenta y la clave de cuenta, asegúrese de que el código fuente sea seguro.

## <a name="toodelete-a-container"></a>toodelete un contenedor
Dado que se le cobra por almacenamiento, quizá prefiera toodelete el **gettingstarted** contenedor una vez que haya experimentar con este ejemplo. toodelete un contenedor, use hello **CloudBlobContainer.delete** método.

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

Hola toocall **CloudBlobContainer.delete** /método siguiente, el proceso de Hola de inicialización de **CloudStorageAccount**, **ClodBlobClient**, y  **CloudBlobContainer** objetos es Hola mismo tal y como se muestra para la **createIfNotExist** método. Hello aquí te mostramos un ejemplo completo que eliminaciones Hola contenedor denominado **gettingstarted**.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

Para obtener información general de los otros métodos y clases de almacenamiento de blobs, vea [cómo toouse almacenamiento de blobs desde Java](storage-java-how-to-use-blob-storage.md).

## <a name="next-steps"></a>Pasos siguientes
Siga estos toolearn de vínculos más información acerca de las tareas más complejas de almacenamiento.

* [SDK de almacenamiento de Azure para Java](https://github.com/azure/azure-storage-java)
* [Referencia del SDK de cliente de almacenamiento de Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API de REST de servicios de Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)

