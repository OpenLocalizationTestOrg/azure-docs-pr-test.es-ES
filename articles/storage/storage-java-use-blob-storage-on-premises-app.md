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
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="0c782-104">Aplicación local con almacenamiento en blobs</span><span class="sxs-lookup"><span data-stu-id="0c782-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="0c782-105">Información general</span><span class="sxs-lookup"><span data-stu-id="0c782-105">Overview</span></span>
<span data-ttu-id="0c782-106">Hello en el ejemplo siguiente se muestra cómo puede usar el almacenamiento de Azure para almacenar imágenes en Azure.</span><span class="sxs-lookup"><span data-stu-id="0c782-106">hello following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="0c782-107">código de Hello en este artículo es para una aplicación de consola que carga una imagen tooAzure y, a continuación, crea un archivo HTML que muestra la imagen de hello en el explorador.</span><span class="sxs-lookup"><span data-stu-id="0c782-107">hello code in this article is for a console application that uploads an image tooAzure, and then creates an HTML file that displays hello image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c782-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0c782-108">Prerequisites</span></span>
* <span data-ttu-id="0c782-109">Un kit para desarrolladores de Java (JDK) v 1.6 o posteriores instalado.</span><span class="sxs-lookup"><span data-stu-id="0c782-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="0c782-110">Hello Azure SDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="0c782-110">hello Azure SDK is installed.</span></span>
* <span data-ttu-id="0c782-111">Hola JAR Hola para bibliotecas de Azure para Java y cualquier dependencia aplicable archivos JAR, se instala y está en la ruta de acceso de compilación de hello utilizado por el compilador de Java.</span><span class="sxs-lookup"><span data-stu-id="0c782-111">hello JAR for hello Azure Libraries for Java, and any applicable dependency JARs, are installed and are in hello build path used by your Java compiler.</span></span> <span data-ttu-id="0c782-112">Para obtener información acerca de cómo instalar Hola bibliotecas de Azure para Java, consulte [descarga hello Azure SDK para Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0c782-112">For information about installing hello Azure Libraries for Java, see [Download hello Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="0c782-113">Una cuenta de almacenamiento configurada en Azure.</span><span class="sxs-lookup"><span data-stu-id="0c782-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="0c782-114">Hello nombre de cuenta y clave de cuenta de almacenamiento de Hola se utilizará por código de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="0c782-114">hello account name and account key for hello storage account will be used by hello code in this article.</span></span> <span data-ttu-id="0c782-115">Vea [cómo tooCreate una cuenta de almacenamiento](storage-create-storage-account.md#create-a-storage-account) para obtener información acerca de cómo crear una cuenta de almacenamiento, y [visualizar y copiar claves de acceso de almacenamiento](storage-create-storage-account.md#view-and-copy-storage-access-keys) para obtener información acerca de cómo recuperar la clave de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="0c782-115">See [How tooCreate a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving hello account key.</span></span>
* <span data-ttu-id="0c782-116">Ha creado un archivo de imagen local con el nombre almacenado en c: de ruta de acceso de hello\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="0c782-116">You have created a local image file named stored at hello path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="0c782-117">O bien, modificar el **FileInputStream** constructor en el ejemplo de Hola toouse un nombre de ruta de acceso y de otra imagen.</span><span class="sxs-lookup"><span data-stu-id="0c782-117">Alternatively, modify the **FileInputStream** constructor in hello example toouse a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a><span data-ttu-id="0c782-118">tooupload de almacenamiento de blobs de Azure toouse un archivo</span><span class="sxs-lookup"><span data-stu-id="0c782-118">toouse Azure blob storage tooupload a file</span></span>
<span data-ttu-id="0c782-119">A continuación se presenta un procedimiento paso a paso.</span><span class="sxs-lookup"><span data-stu-id="0c782-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="0c782-120">Si desea que tooskip con antelación, todo código de hello se presenta más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="0c782-120">If you'd like tooskip ahead, hello entire code is presented later in this article.</span></span>

<span data-ttu-id="0c782-121">Comienzo del código de hello mediante la inclusión de importaciones para clases de almacenamiento de Azure principales de hello, clases de cliente de hello blobs de Azure, las clases de E/S de Java de Hola y Hola **URISyntaxException** clase.</span><span class="sxs-lookup"><span data-stu-id="0c782-121">Begin hello code by including imports for hello Azure core storage classes, hello Azure blob client classes, hello Java IO classes, and hello **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="0c782-122">Declarar una clase denominada **StorageSample**e incluyen el corchete de apertura de hello, **{**.</span><span class="sxs-lookup"><span data-stu-id="0c782-122">Declare a class named **StorageSample**, and include hello open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="0c782-123">Dentro de hello **StorageSample** clase, declare una variable de cadena que contendrá el protocolo de extremo de Hola de forma predeterminada, el nombre de cuenta de almacenamiento y su clave de acceso de almacenamiento, como se especifica en la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0c782-123">Within hello **StorageSample** class, declare a string variable that will contain hello default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="0c782-124">Reemplace los valores de marcador de posición de hello **su\_cuenta\_nombre** y **su\_cuenta\_clave** con su propio nombre de cuenta y la clave de cuenta, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="0c782-124">Replace hello placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="0c782-125">Agregue la declaración para **principal**, incluyen un **intente** bloquear e incluya el corchete de apertura necesarios de hello, **{**.</span><span class="sxs-lookup"><span data-stu-id="0c782-125">Add in your declaration for **main**, include a **try** block, and include hello necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="0c782-126">Declarar variables de hello después del tipo (Hola son descripciones de cómo se utilizan en este ejemplo):</span><span class="sxs-lookup"><span data-stu-id="0c782-126">Declare variables of hello following type (hello descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="0c782-127">**CloudStorageAccount**: Hola tooinitialize usado cuenta objeto con el nombre de la cuenta de almacenamiento de Azure y la clave y el toocreate el objeto de cliente de blob.</span><span class="sxs-lookup"><span data-stu-id="0c782-127">**CloudStorageAccount**: Used tooinitialize hello account object with your Azure storage account name and key, and toocreate the blob client object.</span></span>
* <span data-ttu-id="0c782-128">**CloudBlobClient**: utiliza el servicio de blob de tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="0c782-128">**CloudBlobClient**: Used tooaccess hello blob service.</span></span>
* <span data-ttu-id="0c782-129">**CloudBlobContainer**: toocreate usa un contenedor de blobs, enumerar los blobs en un contenedor hello y delete Hola contenedor.</span><span class="sxs-lookup"><span data-stu-id="0c782-129">**CloudBlobContainer**: Used toocreate a blob container, list the blobs in hello container, and delete hello container.</span></span>
* <span data-ttu-id="0c782-130">**CloudBlockBlob**: tooupload usa un contenedor de toothe del archivo de imagen local.</span><span class="sxs-lookup"><span data-stu-id="0c782-130">**CloudBlockBlob**: Used tooupload a local image file toothe container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="0c782-131">Asignar un valor toohello **cuenta** variable.</span><span class="sxs-lookup"><span data-stu-id="0c782-131">Assign a value toohello **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="0c782-132">Asignar un valor toohello **serviceClient** variable.</span><span class="sxs-lookup"><span data-stu-id="0c782-132">Assign a value toohello **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="0c782-133">Asignar un valor toohello **contenedor** variable.</span><span class="sxs-lookup"><span data-stu-id="0c782-133">Assign a value toohello **container** variable.</span></span> <span data-ttu-id="0c782-134">Nos pondremos en un contenedor de tooa referencia denominado **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="0c782-134">We'll get a reference tooa container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="0c782-135">Crear contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c782-135">Create hello container.</span></span> <span data-ttu-id="0c782-136">Este método creará el contenedor de hello si no existe (y devolver **true**).</span><span class="sxs-lookup"><span data-stu-id="0c782-136">This method will create hello container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="0c782-137">Si existe el contenedor de hello, devolverá **false**.</span><span class="sxs-lookup"><span data-stu-id="0c782-137">If hello container does exist, it will return **false**.</span></span> <span data-ttu-id="0c782-138">Una alternativa demasiado**createIfNotExists** es hello **crear** método (que se devolverá un error si ya existe el contenedor de hello).</span><span class="sxs-lookup"><span data-stu-id="0c782-138">An alternative too**createIfNotExists** is hello **create** method (which will return an error if hello container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="0c782-139">Establecer el acceso anónimo para el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c782-139">Set anonymous access for hello container.</span></span>

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="0c782-140">Obtener un blob en bloques toohello referencia, que representará el blob de hello en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0c782-140">Get a reference toohello block blob, which will represent hello blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="0c782-141">Hola de uso **archivo** constructor tooget un archivo de referencia toohello creada localmente que va a cargar.</span><span class="sxs-lookup"><span data-stu-id="0c782-141">Use hello **File** constructor tooget a reference toohello locally created file that you will upload.</span></span> <span data-ttu-id="0c782-142">Asegúrese de que ha creado este archivo antes de ejecutar código de hello.</span><span class="sxs-lookup"><span data-stu-id="0c782-142">Ensure you have created this file before running hello code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="0c782-143">Cargando archivo local de Hola a través de una llamada toohello **CloudBlockBlob.upload** método.</span><span class="sxs-lookup"><span data-stu-id="0c782-143">Upload hello local file through a call toohello **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="0c782-144">Hola primera toohello parámetro **CloudBlockBlob.upload** método es un **FileInputStream** ese archivo local de Hola de representa será cargado tooAzure almacenamiento del objeto.</span><span class="sxs-lookup"><span data-stu-id="0c782-144">hello first parameter toohello **CloudBlockBlob.upload** method is a **FileInputStream** object that represents hello local file that will be uploaded tooAzure storage.</span></span> <span data-ttu-id="0c782-145">Hola segundo parámetro es tamaño hello, en bytes, del archivo hello.</span><span class="sxs-lookup"><span data-stu-id="0c782-145">hello second parameter is hello size, in bytes, of hello file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="0c782-146">Llamar a una función auxiliar denominada **MakeHTMLPage**, página toomake una HTML básica que contiene un  **&lt;imagen&gt;**  elemento con blob toohello de conjunto de origen de Hola que se encuentra ahora en Azure cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0c782-146">Call a helper function named **MakeHTMLPage**, toomake a basic HTML page that contains an **&lt;image&gt;** element with hello source set toohello blob that is now in your Azure storage account.</span></span> <span data-ttu-id="0c782-147">Hola código para **MakeHTMLPage** se explicará más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="0c782-147">hello code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="0c782-148">Imprimir un mensaje de estado e información sobre Hola creada la página HTML.</span><span class="sxs-lookup"><span data-stu-id="0c782-148">Print out a status message and information about hello created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

<span data-ttu-id="0c782-149">Hola cerrar **intente** bloque insertando un corchete de cierre: **}**</span><span class="sxs-lookup"><span data-stu-id="0c782-149">Close hello **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="0c782-150">Identificador hello siguientes excepciones:</span><span class="sxs-lookup"><span data-stu-id="0c782-150">Handle hello following exceptions:</span></span>

* <span data-ttu-id="0c782-151">**FileNotFoundException**: Hola puede producir **FileInputStream** o **clase FileOutputStream** constructores.</span><span class="sxs-lookup"><span data-stu-id="0c782-151">**FileNotFoundException**: Can be thrown by hello **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="0c782-152">**StorageException**: biblioteca de almacenamiento de Azure cliente hello puede producir.</span><span class="sxs-lookup"><span data-stu-id="0c782-152">**StorageException**: Can be thrown by hello Azure client storage library.</span></span>
* <span data-ttu-id="0c782-153">**URISyntaxException**: Hola puede producir **ListBlobItem.getUri** método.</span><span class="sxs-lookup"><span data-stu-id="0c782-153">**URISyntaxException**: Can be thrown by hello **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="0c782-154">**Exception**: control de una excepción genérica.</span><span class="sxs-lookup"><span data-stu-id="0c782-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="0c782-155">Cierre **main** mediante la inserción de un corchete de cierre: **}**.</span><span class="sxs-lookup"><span data-stu-id="0c782-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="0c782-156">Crear un método denominado **MakeHTMLPage** página toocreate una HTML básica.</span><span class="sxs-lookup"><span data-stu-id="0c782-156">Create a method named **MakeHTMLPage** toocreate a basic HTML page.</span></span> <span data-ttu-id="0c782-157">Este método tiene un parámetro de tipo **CloudBlobContainer**, que será usado tooiterate a través de la lista de Hola de blobs cargados.</span><span class="sxs-lookup"><span data-stu-id="0c782-157">This method has a parameter of type **CloudBlobContainer**, which will be used tooiterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="0c782-158">Este método producirá excepciones de tipo **FileNotFoundException**, que puede producir hello **clase FileOutputStream** constructor, y **URISyntaxException**, lo que puede se produce por hello **ListBlobItem.getUri** método.</span><span class="sxs-lookup"><span data-stu-id="0c782-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by hello **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by hello **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="0c782-159">Incluya el corchete de apertura, **{**.</span><span class="sxs-lookup"><span data-stu-id="0c782-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="0c782-160">Cree un archivo local llamado **index.html**.</span><span class="sxs-lookup"><span data-stu-id="0c782-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="0c782-161">Escribir en el archivo local toohello, agregar Hola  **&lt;html&gt;**,  **&lt;encabezado&gt;**, y  **&lt;cuerpo&gt;**  elementos.</span><span class="sxs-lookup"><span data-stu-id="0c782-161">Write toohello local file, adding in hello **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="0c782-162">Recorrer en iteración la lista de Hola de blobs cargados.</span><span class="sxs-lookup"><span data-stu-id="0c782-162">Iterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="0c782-163">Para cada blob, en la página de hello HTML crear un  **&lt;img&gt;**  elemento que tiene su **src** atributo enviado al URI de blob de Hola Hola tal como existe en su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0c782-163">For each blob, in hello HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to hello URI of hello blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="0c782-164">Aunque ha agregado una sola imagen en este ejemplo, si agregara más, este código iteraría todas ellas.</span><span class="sxs-lookup"><span data-stu-id="0c782-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="0c782-165">Para simplificar, en este ejemplo se asume que cada blob cargado es una imagen.</span><span class="sxs-lookup"><span data-stu-id="0c782-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="0c782-166">Si ha actualizado blobs que no sean imágenes o blobs de página en lugar de blobs en bloques, ajustar el código de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0c782-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust hello code as needed.</span></span>

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="0c782-167">Hola cerrar  **&lt;cuerpo&gt;**  hello y elemento  **&lt;html&gt;**  elemento.</span><span class="sxs-lookup"><span data-stu-id="0c782-167">Close hello **&lt;body&gt;** element and hello **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="0c782-168">Archivo local Hola cerrar.</span><span class="sxs-lookup"><span data-stu-id="0c782-168">Close hello local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="0c782-169">Cierre **MakeHTMLPage** mediante la inserción de un corchete de cierre: **}**.</span><span class="sxs-lookup"><span data-stu-id="0c782-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="0c782-170">Cierre **StorageSample** mediante la inserción de un corchete de cierre: **}**.</span><span class="sxs-lookup"><span data-stu-id="0c782-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="0c782-171">Hola aquí te mostramos código completo de hello en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0c782-171">hello following is hello complete code for this example.</span></span> <span data-ttu-id="0c782-172">Recuerde que los valores de marcador de posición de hello toomodify **su\_cuenta\_nombre** y **su\_cuenta\_clave** toouse su nombre de cuenta y la cuenta la clave, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="0c782-172">Remember toomodify hello placeholder values **your\_account\_name** and **your\_account\_key** toouse your account name and account key, respectively.</span></span>

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

<span data-ttu-id="0c782-173">En suma toouploading su almacenamiento tooAzure del archivo de imagen local, código de ejemplo de Hola crea un namedindex.html de archivos local, que puede abrir en el explorador toosee la imagen cargada.</span><span class="sxs-lookup"><span data-stu-id="0c782-173">In addition toouploading your local image file tooAzure storage, hello example code creates a local file namedindex.html, which you can open in your browser toosee your uploaded image.</span></span>

<span data-ttu-id="0c782-174">Dado que el código de hello contiene el nombre de cuenta y la clave de cuenta, asegúrese de que el código fuente sea seguro.</span><span class="sxs-lookup"><span data-stu-id="0c782-174">Because hello code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="toodelete-a-container"></a><span data-ttu-id="0c782-175">toodelete un contenedor</span><span class="sxs-lookup"><span data-stu-id="0c782-175">toodelete a container</span></span>
<span data-ttu-id="0c782-176">Dado que se le cobra por almacenamiento, quizá prefiera toodelete el **gettingstarted** contenedor una vez que haya experimentar con este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0c782-176">Because you are charged for storage, you may want toodelete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="0c782-177">toodelete un contenedor, use hello **CloudBlobContainer.delete** método.</span><span class="sxs-lookup"><span data-stu-id="0c782-177">toodelete a container, use hello **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="0c782-178">Hola toocall **CloudBlobContainer.delete** /método siguiente, el proceso de Hola de inicialización de **CloudStorageAccount**, **ClodBlobClient**, y  **CloudBlobContainer** objetos es Hola mismo tal y como se muestra para la **createIfNotExist** método.</span><span class="sxs-lookup"><span data-stu-id="0c782-178">toocall hello **CloudBlobContainer.delete** method, hello process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is hello same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="0c782-179">Hello aquí te mostramos un ejemplo completo que eliminaciones Hola contenedor denominado **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="0c782-179">hello following is a complete example that deletes hello container named **gettingstarted**.</span></span>

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

<span data-ttu-id="0c782-180">Para obtener información general de los otros métodos y clases de almacenamiento de blobs, vea [cómo toouse almacenamiento de blobs desde Java](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0c782-180">For an overview of other blob storage classes and methods, see [How toouse Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c782-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0c782-181">Next steps</span></span>
<span data-ttu-id="0c782-182">Siga estos toolearn de vínculos más información acerca de las tareas más complejas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0c782-182">Follow these links toolearn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="0c782-183">SDK de almacenamiento de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="0c782-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="0c782-184">Referencia del SDK de cliente de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="0c782-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="0c782-185">API de REST de servicios de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0c782-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="0c782-186">Blog del equipo de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="0c782-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

