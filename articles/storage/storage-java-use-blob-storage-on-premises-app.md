---
title: "Aplicación local con Blob Storage (Java) | Microsoft Docs"
description: "Aprenda a crear una aplicación de consola que carga una imagen en Azure y, a continuación, muestra la imagen en el explorador. Ejemplos de código en Java."
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
ms.openlocfilehash: a172b881fa38a69f4510df94f5797b7a56940c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="5fb60-104">Aplicación local con almacenamiento en blobs</span><span class="sxs-lookup"><span data-stu-id="5fb60-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="5fb60-105">Información general</span><span class="sxs-lookup"><span data-stu-id="5fb60-105">Overview</span></span>
<span data-ttu-id="5fb60-106">El siguiente ejemplo muestra cómo se puede utilizar el almacenamiento de Azure para almacenar las imágenes en Azure.</span><span class="sxs-lookup"><span data-stu-id="5fb60-106">The following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="5fb60-107">El código en este artículo se destina a una aplicación de consola que carga una imagen en Azure y, a continuación, crea un archivo HTML que muestra la imagen en su explorador.</span><span class="sxs-lookup"><span data-stu-id="5fb60-107">The code in this article is for a console application that uploads an image to Azure, and then creates an HTML file that displays the image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fb60-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5fb60-108">Prerequisites</span></span>
* <span data-ttu-id="5fb60-109">Un kit para desarrolladores de Java (JDK) v 1.6 o posteriores instalado.</span><span class="sxs-lookup"><span data-stu-id="5fb60-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="5fb60-110">El SDK de Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="5fb60-110">The Azure SDK is installed.</span></span>
* <span data-ttu-id="5fb60-111">El archivo JAR de las Bibliotecas de Azure para Java (y cualquier JAR de dependencia correspondiente) instalado y en la ruta de acceso de compilación utilizada por el compilador de Java.</span><span class="sxs-lookup"><span data-stu-id="5fb60-111">The JAR for the Azure Libraries for Java, and any applicable dependency JARs, are installed and are in the build path used by your Java compiler.</span></span> <span data-ttu-id="5fb60-112">Para obtener información acerca de la instalación de bibliotecas de Azure para Java, consulte [Descarga del SDK de Azure para Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5fb60-112">For information about installing the Azure Libraries for Java, see [Download the Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="5fb60-113">Una cuenta de almacenamiento configurada en Azure.</span><span class="sxs-lookup"><span data-stu-id="5fb60-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="5fb60-114">El código en este artículo usará el nombre y la clave de cuenta para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5fb60-114">The account name and account key for the storage account will be used by the code in this article.</span></span> <span data-ttu-id="5fb60-115">Consulte [Crear una cuenta de almacenamiento](storage-create-storage-account.md#create-a-storage-account) para más información sobre la creación de una cuenta de almacenamiento y [Visualización y copia de las claves de acceso de almacenamiento](storage-create-storage-account.md#view-and-copy-storage-access-keys) para más información acerca de la recuperación de la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="5fb60-115">See [How to Create a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving the account key.</span></span>
* <span data-ttu-id="5fb60-116">Ha creado un archivo de imagen local con el nombre almacenado en la ruta de acceso c:\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="5fb60-116">You have created a local image file named stored at the path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="5fb60-117">También puede modificar el constructor **FileInputStream** en el ejemplo para usar una ruta de acceso de imagen y un nombre de archivo diferentes.</span><span class="sxs-lookup"><span data-stu-id="5fb60-117">Alternatively, modify the **FileInputStream** constructor in the example to use a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="to-use-azure-blob-storage-to-upload-a-file"></a><span data-ttu-id="5fb60-118">Para usar el almacenamiento de blobs de Azure para cargar un archivo</span><span class="sxs-lookup"><span data-stu-id="5fb60-118">To use Azure blob storage to upload a file</span></span>
<span data-ttu-id="5fb60-119">A continuación se presenta un procedimiento paso a paso.</span><span class="sxs-lookup"><span data-stu-id="5fb60-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="5fb60-120">Si desea omitir pasos, el código completo se presenta más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="5fb60-120">If you'd like to skip ahead, the entire code is presented later in this article.</span></span>

<span data-ttu-id="5fb60-121">Comience el código mediante la inclusión de importaciones para las clases de almacenamiento central de Azure, las clases de clientes de blob de Azure, las clases de Java IO y la clase **URISyntaxException** :</span><span class="sxs-lookup"><span data-stu-id="5fb60-121">Begin the code by including imports for the Azure core storage classes, the Azure blob client classes, the Java IO classes, and the **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="5fb60-122">Declare una clase llamada **StorageSample** e incluya el corchete de apertura, **{**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-122">Declare a class named **StorageSample**, and include the open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="5fb60-123">Dentro de la clase **StorageSample** , declare una variable de cadena que contendrá el protocolo de extremo predeterminado, el nombre de la cuenta de almacenamiento y la clave de acceso de almacenamiento, según lo especificado en su cuenta de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="5fb60-123">Within the **StorageSample** class, declare a string variable that will contain the default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="5fb60-124">Reemplace los valores de marcador de posición **your\_account\_name** y **your\_account\_key** por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="5fb60-124">Replace the placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="5fb60-125">Agregue su declaración de **main**, incluya un bloque **try** e incluya los corchetes de apertura necesarios, **{**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-125">Add in your declaration for **main**, include a **try** block, and include the necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="5fb60-126">Declare variables del siguiente tipo (las descripciones reflejan el uso que se les da en este ejemplo):</span><span class="sxs-lookup"><span data-stu-id="5fb60-126">Declare variables of the following type (the descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="5fb60-127">**CloudStorageAccount**: se utiliza para inicializar el objeto de cuenta con el nombre y la clave de la cuenta de Almacenamiento de Azure y para crear el objeto de cliente blob.</span><span class="sxs-lookup"><span data-stu-id="5fb60-127">**CloudStorageAccount**: Used to initialize the account object with your Azure storage account name and key, and to create the blob client object.</span></span>
* <span data-ttu-id="5fb60-128">**CloudBlobClient**: se utiliza para tener acceso al servicio BLOB.</span><span class="sxs-lookup"><span data-stu-id="5fb60-128">**CloudBlobClient**: Used to access the blob service.</span></span>
* <span data-ttu-id="5fb60-129">**CloudBlobContainer**: se utiliza para crear un contenedor de blobs, enumerar los blobs en el contenedor y eliminar el contenedor.</span><span class="sxs-lookup"><span data-stu-id="5fb60-129">**CloudBlobContainer**: Used to create a blob container, list the blobs in the container, and delete the container.</span></span>
* <span data-ttu-id="5fb60-130">**CloudBlockBlob**: se utiliza para cargar un archivo de imagen local al contenedor.</span><span class="sxs-lookup"><span data-stu-id="5fb60-130">**CloudBlockBlob**: Used to upload a local image file to the container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="5fb60-131">Asigne un valor a la variable **account** .</span><span class="sxs-lookup"><span data-stu-id="5fb60-131">Assign a value to the **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="5fb60-132">Asigne un valor a la variable **serviceClient** .</span><span class="sxs-lookup"><span data-stu-id="5fb60-132">Assign a value to the **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="5fb60-133">Asigne un valor a la variable **container** .</span><span class="sxs-lookup"><span data-stu-id="5fb60-133">Assign a value to the **container** variable.</span></span> <span data-ttu-id="5fb60-134">Obtendremos una referencia a un contenedor llamado **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-134">We'll get a reference to a container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="5fb60-135">Cree el contenedor.</span><span class="sxs-lookup"><span data-stu-id="5fb60-135">Create the container.</span></span> <span data-ttu-id="5fb60-136">Este método creará el contenedor si no existe (y devolverá **true**).</span><span class="sxs-lookup"><span data-stu-id="5fb60-136">This method will create the container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="5fb60-137">Si el contenedor existe, devolverá **false**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-137">If the container does exist, it will return **false**.</span></span> <span data-ttu-id="5fb60-138">Una alternativa a **createIfNotExist** es el método **create** (que devolverá un error si el contenedor ya existe).</span><span class="sxs-lookup"><span data-stu-id="5fb60-138">An alternative to **createIfNotExists** is the **create** method (which will return an error if the container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="5fb60-139">Configure el acceso anónimo para el contenedor.</span><span class="sxs-lookup"><span data-stu-id="5fb60-139">Set anonymous access for the container.</span></span>

```java
// Set anonymous access on the container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="5fb60-140">Obtenga una referencia al blob en bloque, el cual representará al blob en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="5fb60-140">Get a reference to the block blob, which will represent the blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="5fb60-141">Use el constructor **File** para obtener una referencia al archivo que se creó de manera local que va a cargar.</span><span class="sxs-lookup"><span data-stu-id="5fb60-141">Use the **File** constructor to get a reference to the locally created file that you will upload.</span></span> <span data-ttu-id="5fb60-142">Asegúrese de haber creado el archivo antes de ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="5fb60-142">Ensure you have created this file before running the code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="5fb60-143">Cargue el archivo local a través de una llamada al método **CloudBlockBlob.upload** .</span><span class="sxs-lookup"><span data-stu-id="5fb60-143">Upload the local file through a call to the **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="5fb60-144">El primer parámetro del método **CloudBlockBlob.upload** es un objeto **FileInputStream** que representa el archivo local que se cargará en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5fb60-144">The first parameter to the **CloudBlockBlob.upload** method is a **FileInputStream** object that represents the local file that will be uploaded to Azure storage.</span></span> <span data-ttu-id="5fb60-145">El segundo parámetro es el tamaño, en bytes, del archivo.</span><span class="sxs-lookup"><span data-stu-id="5fb60-145">The second parameter is the size, in bytes, of the file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="5fb60-146">Llame a una función auxiliar denominada **MakeHTMLPage** para crear una página HTML básica que contenga un elemento **&lt;image&gt;** con la fuente definida en el blob que se encuentra ahora en la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5fb60-146">Call a helper function named **MakeHTMLPage**, to make a basic HTML page that contains an **&lt;image&gt;** element with the source set to the blob that is now in your Azure storage account.</span></span> <span data-ttu-id="5fb60-147">El código de **MakeHTMLPage** se describirá más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="5fb60-147">The code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="5fb60-148">Imprima un mensaje de estado y la información sobre la página HTML creada.</span><span class="sxs-lookup"><span data-stu-id="5fb60-148">Print out a status message and information about the created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html to see the images stored in your storage account.");
```

<span data-ttu-id="5fb60-149">Cierre el bloque **try** mediante la inserción de un corchete de cierre: **}**</span><span class="sxs-lookup"><span data-stu-id="5fb60-149">Close the **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="5fb60-150">Controle las siguientes excepciones:</span><span class="sxs-lookup"><span data-stu-id="5fb60-150">Handle the following exceptions:</span></span>

* <span data-ttu-id="5fb60-151">**FileNotFoundException**: se puede mostrar mediante los constructores **FileInputStream** o **FileOutputStream**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-151">**FileNotFoundException**: Can be thrown by the **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="5fb60-152">**StorageException**: se puede mostrar mediante la biblioteca de almacenamiento del cliente de Azure.</span><span class="sxs-lookup"><span data-stu-id="5fb60-152">**StorageException**: Can be thrown by the Azure client storage library.</span></span>
* <span data-ttu-id="5fb60-153">**URISyntaxException**: se puede mostrar mediante el método **ListBlobItem.getUri**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-153">**URISyntaxException**: Can be thrown by the **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="5fb60-154">**Exception**: control de una excepción genérica.</span><span class="sxs-lookup"><span data-stu-id="5fb60-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="5fb60-155">Cierre **main** mediante la inserción de un corchete de cierre: **}**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="5fb60-156">Cree un método llamado **MakeHTMLPage** para crear una página HTML básica.</span><span class="sxs-lookup"><span data-stu-id="5fb60-156">Create a method named **MakeHTMLPage** to create a basic HTML page.</span></span> <span data-ttu-id="5fb60-157">Este método tiene un parámetro de tipo **CloudBlobContainer**, que se usará para iterar a través de la lista de blobs cargados.</span><span class="sxs-lookup"><span data-stu-id="5fb60-157">This method has a parameter of type **CloudBlobContainer**, which will be used to iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="5fb60-158">Este método mostrará excepciones de tipo **FileNotFoundException**, que se pueden mostrar mediante el constructor **FileOutputStream** y **URISyntaxException**, que se pueden mostrar a través del método **ListBlobItem.getUri**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by the **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by the **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="5fb60-159">Incluya el corchete de apertura, **{**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="5fb60-160">Cree un archivo local llamado **index.html**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="5fb60-161">Escriba en el archivo local y agregue los elementos **html&lt;&gt;**, **&lt;header&gt;** y **&lt;body&gt;**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-161">Write to the local file, adding in the **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="5fb60-162">Itere a través de la lista de blobs cargados.</span><span class="sxs-lookup"><span data-stu-id="5fb60-162">Iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="5fb60-163">Para cada blob, en la página HTML cree un elemento **&lt;img&gt;** que envió su atributo **src** al URI del blob, tal como existe en su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5fb60-163">For each blob, in the HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to the URI of the blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="5fb60-164">Aunque ha agregado una sola imagen en este ejemplo, si agregara más, este código iteraría todas ellas.</span><span class="sxs-lookup"><span data-stu-id="5fb60-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="5fb60-165">Para simplificar, en este ejemplo se asume que cada blob cargado es una imagen.</span><span class="sxs-lookup"><span data-stu-id="5fb60-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="5fb60-166">Si ha actualizado blobs aparte de imágenes o blobs de páginas en lugar de blobs en bloques, ajuste el código según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5fb60-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust the code as needed.</span></span>

```java
// Enumerate the uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in the HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="5fb60-167">Cierre el elemento **&lt;body&gt;** y el elemento **&lt;html&gt;**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-167">Close the **&lt;body&gt;** element and the **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="5fb60-168">Cierre el archivo local.</span><span class="sxs-lookup"><span data-stu-id="5fb60-168">Close the local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="5fb60-169">Cierre **MakeHTMLPage** mediante la inserción de un corchete de cierre: **}**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="5fb60-170">Cierre **StorageSample** mediante la inserción de un corchete de cierre: **}**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="5fb60-171">El siguiente es el código completo de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5fb60-171">The following is the complete code for this example.</span></span> <span data-ttu-id="5fb60-172">Recuerde modificar los valores de marcador de posición **your\_account\_name** and **your\_account\_key** para usar los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="5fb60-172">Remember to modify the placeholder values **your\_account\_name** and **your\_account\_key** to use your account name and account key, respectively.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior to running this sample.
// Alternatively, change the value used by the FileInputStream constructor
// to use a different image path and file that you have already created.
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

            // Set anonymous access on the container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point the image is uploaded.
            // Next, create an HTML page that lists all of the uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html to see the images stored in your storage account.");

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

    // Create an HTML page that can be used to display the uploaded images.
    // This example assumes all of the blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create the opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate the uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in the HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete the <html> element and close the file.
        stream.println("</html>");
        stream.close();
    }
}
```

<span data-ttu-id="5fb60-173">Además de subir el archivo de imagen local al almacenamiento de Azure, el código de ejemplo crea un archivo local namedindex.html, que se puede abrir en el explorador para ver la imagen cargada.</span><span class="sxs-lookup"><span data-stu-id="5fb60-173">In addition to uploading your local image file to Azure storage, the example code creates a local file namedindex.html, which you can open in your browser to see your uploaded image.</span></span>

<span data-ttu-id="5fb60-174">Debido a que el código contiene el nombre y la clave de la cuenta, asegúrese de que su código fuente sea seguro.</span><span class="sxs-lookup"><span data-stu-id="5fb60-174">Because the code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="to-delete-a-container"></a><span data-ttu-id="5fb60-175">Para eliminar un contenedor</span><span class="sxs-lookup"><span data-stu-id="5fb60-175">To delete a container</span></span>
<span data-ttu-id="5fb60-176">Debido a que se cobrará por el almacenamiento, es posible que desee eliminar el contenedor **gettingstarted** después de que haya terminado de experimentar con este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5fb60-176">Because you are charged for storage, you may want to delete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="5fb60-177">Para eliminar un contenedor, use el método **CloudBlobContainer.delete** :</span><span class="sxs-lookup"><span data-stu-id="5fb60-177">To delete a container, use the **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="5fb60-178">Para llamar al método **CloudBlobContainer.delete**, el proceso de inicialización de los objetos **CloudStorageAccount**, **ClodBlobClient** y **CloudBlobContainer** es el mismo que se muestra para el método **createIfNotExist**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-178">To call the **CloudBlobContainer.delete** method, the process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is the same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="5fb60-179">A continuación se expone un ejemplo completo que elimina el contenedor llamado **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="5fb60-179">The following is a complete example that deletes the container named **gettingstarted**.</span></span>

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

<span data-ttu-id="5fb60-180">Para ver información general de otras clases y métodos de almacenamiento de blobs, consulte [Uso del almacenamiento de blobs desde Java](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5fb60-180">For an overview of other blob storage classes and methods, see [How to use Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fb60-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5fb60-181">Next steps</span></span>
<span data-ttu-id="5fb60-182">Siga estos vínculos para obtener más información acerca de las tareas de almacenamiento más complejas.</span><span class="sxs-lookup"><span data-stu-id="5fb60-182">Follow these links to learn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="5fb60-183">SDK de almacenamiento de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="5fb60-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="5fb60-184">Referencia del SDK de cliente de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="5fb60-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="5fb60-185">API de REST de servicios de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5fb60-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="5fb60-186">Blog del equipo de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="5fb60-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

