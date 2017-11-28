---
title: Uso del SDK de Java para desarrollar aplicaciones en Azure Data Lake Store | Microsoft Docs
description: "Uso del SDK de Java de Azure Data Lake Store para crear una cuenta de Data Lake Store y realizar operaciones básicas en este"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: 91128b53a2f1cd3ddcbee5b07da0d67668944fb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="89ecb-103">Introducción al Almacén de Azure Data Lake mediante Java</span><span class="sxs-lookup"><span data-stu-id="89ecb-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89ecb-104">Portal</span><span class="sxs-lookup"><span data-stu-id="89ecb-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="89ecb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="89ecb-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="89ecb-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="89ecb-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="89ecb-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="89ecb-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="89ecb-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="89ecb-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="89ecb-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="89ecb-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="89ecb-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="89ecb-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="89ecb-111">Python</span><span class="sxs-lookup"><span data-stu-id="89ecb-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="89ecb-112">Aprenda a utilizar el SDK de Java de Azure Data Lake Store para realizar operaciones básicas como crear carpetas, cargar y descargar archivos de datos, etc. Para más información sobre Data Lake, consulte [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="89ecb-112">Learn how to use the Azure Data Lake Store Java SDK to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="89ecb-113">Puede acceder a los documentos de la API del SDK de Java para Azure Data Lake Store en los [documentos de la API de Java de Azure Data Lake Store](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="89ecb-113">You can access the Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89ecb-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="89ecb-114">Prerequisites</span></span>
* <span data-ttu-id="89ecb-115">Kit de desarrollo de Java (JDK 7 o superior, con Java versión 1.7 o posterior).</span><span class="sxs-lookup"><span data-stu-id="89ecb-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="89ecb-116">Cuenta de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="89ecb-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="89ecb-117">Siga las instrucciones que se describen en [Introducción al Almacén de Azure Data Lake mediante el Portal de Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="89ecb-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="89ecb-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="89ecb-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="89ecb-119">Este tutorial usa Maven para crear las dependencias de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="89ecb-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="89ecb-120">Aunque es posible generarlas sin utilizar un sistema como Maven o Gradle, estos sistemas facilitan mucho la administración de las dependencias.</span><span class="sxs-lookup"><span data-stu-id="89ecb-120">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span></span>
* <span data-ttu-id="89ecb-121">(Opcional) Y un IDE como [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) o similar.</span><span class="sxs-lookup"><span data-stu-id="89ecb-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="89ecb-122">¿Cómo se puede autenticar mediante Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89ecb-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="89ecb-123">En este tutorial, utilizamos un secreto de cliente de la aplicación de Azure AD para recuperar un token de Azure Active Directory (autenticación de servicio a servicio).</span><span class="sxs-lookup"><span data-stu-id="89ecb-123">In this tutorial we use a Azure AD application client secret to retrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="89ecb-124">Usamos este token para crear un objeto de cliente de Data Lake Store para llevar a cabo operaciones de archivos y directorios.</span><span class="sxs-lookup"><span data-stu-id="89ecb-124">We use this token to create an Data Lake Store client object to perform operations file and directory operations.</span></span> <span data-ttu-id="89ecb-125">Para ver instrucciones sobre cómo autenticar con Azure Data Lake Store mediante el secreto del cliente, realizamos los siguientes pasos de alto nivel:</span><span class="sxs-lookup"><span data-stu-id="89ecb-125">For instructions on how to authenticate with Azure Data Lake Store using the client secret, we perform the following high-level steps:</span></span>

1. <span data-ttu-id="89ecb-126">Creación de una aplicación web de Azure AD</span><span class="sxs-lookup"><span data-stu-id="89ecb-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="89ecb-127">Recupere el identificador de cliente, el secreto de cliente y el punto de conexión del token para la aplicación web de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89ecb-127">Retrieve the client ID, client secret, and token endpoint for the Azure AD web application.</span></span>
3. <span data-ttu-id="89ecb-128">Configure el acceso para la aplicación web de Azure AD en el archivo o carpeta Data Lake Store al que desee acceder desde la aplicación de Java que está creando.</span><span class="sxs-lookup"><span data-stu-id="89ecb-128">Configure access for the Azure AD web application on the Data Lake Store file/folder that you want to access from the Java application you are creating.</span></span>

<span data-ttu-id="89ecb-129">Para ver instrucciones sobre cómo realizar estos pasos, consulte [Creación de una aplicación de Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="89ecb-129">For instructions on how to perform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="89ecb-130">Azure Active Directory ofrece también otras opciones para recuperar un token.</span><span class="sxs-lookup"><span data-stu-id="89ecb-130">Azure Active Directory provides other options as well to retrieve a token.</span></span> <span data-ttu-id="89ecb-131">Puede elegir entre una serie de diferentes mecanismos de autenticación para adaptarlos a su escenario; por ejemplo, una aplicación que se ejecuta en un explorador, una aplicación distribuida como una aplicación de escritorio o una aplicación de servidor que se ejecuta de forma local o en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="89ecb-131">You can pick from a number of different authentication mechanisms to suit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="89ecb-132">También puede elegir entre distintos tipos de credenciales, como contraseñas, certificados, autenticación en dos fases, etc. Además, Azure Active Directory permite sincronizar los usuarios de Active Directory local con la nube.</span><span class="sxs-lookup"><span data-stu-id="89ecb-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you to synchronize your on-premises Active Directory users with the cloud.</span></span> <span data-ttu-id="89ecb-133">Para más detalles, consulte [Escenarios de autenticación para Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="89ecb-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="89ecb-134">Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="89ecb-134">Create a Java application</span></span>
<span data-ttu-id="89ecb-135">El ejemplo de código disponible [en GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) le guía a través del proceso de creación de archivos en el almacén, concatenación de archivos, descarga de un archivo y eliminación de algunos archivos en el almacén.</span><span class="sxs-lookup"><span data-stu-id="89ecb-135">The code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through the process of creating files in the store, concatenating files, downloading a file, and deleting some files in the store.</span></span> <span data-ttu-id="89ecb-136">Esta sección del artículo le guía a través de las principales partes del código.</span><span class="sxs-lookup"><span data-stu-id="89ecb-136">This section of the article walk you through the main parts of the code.</span></span>

1. <span data-ttu-id="89ecb-137">Cree un proyecto de Maven con [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) en la línea de comandos o mediante un IDE.</span><span class="sxs-lookup"><span data-stu-id="89ecb-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command-line or using an IDE.</span></span> <span data-ttu-id="89ecb-138">Para ver instrucciones sobre cómo crear un proyecto de Java mediante IntelliJ, consulte [este artículo](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="89ecb-138">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="89ecb-139">Para ver instrucciones sobre cómo crear un proyecto con Eclipse, consulte [este artículo](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="89ecb-139">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="89ecb-140">Agregue las siguientes dependencias a su archivo **pom.xml** de Maven.</span><span class="sxs-lookup"><span data-stu-id="89ecb-140">Add the following dependencies to your Maven **pom.xml** file.</span></span> <span data-ttu-id="89ecb-141">Agregue el siguiente fragmento de texto entre las etiquetas **\</version>** y **\</project>**:</span><span class="sxs-lookup"><span data-stu-id="89ecb-141">Add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span></span>
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    <span data-ttu-id="89ecb-142">La primera dependencia es el uso del SDK de Data Lake Store (`azure-data-lake-store-sdk`) desde el repositorio de maven.</span><span class="sxs-lookup"><span data-stu-id="89ecb-142">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span></span> <span data-ttu-id="89ecb-143">La segunda dependencia (`slf4j-nop`) consiste en especificar qué plataforma de registro se usará para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="89ecb-143">The second dependency (`slf4j-nop`) is to specify which logging framework to use for this application.</span></span> <span data-ttu-id="89ecb-144">El SDK de Data Lake Store usa la fachada de registro [slf4j](http://www.slf4j.org/), que permite elegir entre una serie de plataformas de registro populares, como log4j, registro de Java, logback, etc., o no registrarse.</span><span class="sxs-lookup"><span data-stu-id="89ecb-144">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="89ecb-145">En este ejemplo, se deshabilitará el registro; por tanto, usamos el enlace **slf4j-nop**.</span><span class="sxs-lookup"><span data-stu-id="89ecb-145">For this example, we will disable logging, hence we use the **slf4j-nop** binding.</span></span> <span data-ttu-id="89ecb-146">Para usar otras opciones de registro en su aplicación, consulte [este artículo](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="89ecb-146">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-the-application-code"></a><span data-ttu-id="89ecb-147">Revisión del código de la aplicación</span><span class="sxs-lookup"><span data-stu-id="89ecb-147">Add the application code</span></span>
<span data-ttu-id="89ecb-148">Hay tres partes principales en el código.</span><span class="sxs-lookup"><span data-stu-id="89ecb-148">There are three main parts to the code.</span></span>

1. <span data-ttu-id="89ecb-149">Obtener el token de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="89ecb-149">Obtain the Azure Active Directory token</span></span>
2. <span data-ttu-id="89ecb-150">Usar el token para crear a un cliente de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="89ecb-150">Use the token to create a Data Lake Store client.</span></span>
3. <span data-ttu-id="89ecb-151">Utilizar al cliente de Data Lake Store para realizar operaciones.</span><span class="sxs-lookup"><span data-stu-id="89ecb-151">Use the Data Lake Store client to perform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="89ecb-152">Paso 1: Obtención de un token de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="89ecb-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="89ecb-153">El SDK de Data Lake Store proporciona métodos útiles que permiten obtener los tokens de seguridad necesarios para comunicarse con la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="89ecb-153">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span></span> <span data-ttu-id="89ecb-154">Sin embargo, el SDK no obliga a que se usen solo estos métodos.</span><span class="sxs-lookup"><span data-stu-id="89ecb-154">However, the SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="89ecb-155">También puede usar cualquier otro medio de obtención del token, como el [SDK de Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java) o su propio código personalizado.</span><span class="sxs-lookup"><span data-stu-id="89ecb-155">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="89ecb-156">Para utilizar el SDK de Data Lake Store con el fin de obtener el token para la aplicación web de Active Directory que creó anteriormente, utilice una de las subclases de `AccessTokenProvider` (el ejemplo a continuación utiliza `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="89ecb-156">To use the Data Lake Store SDK to obtain token for the Active Directory Web application you created earlier, use one of the subclasses of `AccessTokenProvider` (the example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="89ecb-157">El proveedor de tokens almacena en caché las credenciales que se utilizan para obtener el token en la memoria y renueva el token de forma automática si está a punto de expirar.</span><span class="sxs-lookup"><span data-stu-id="89ecb-157">The token provider caches the creds used to obtain the token in memory, and automatically renews the token if it is about to expire.</span></span> <span data-ttu-id="89ecb-158">Puede crear sus propias subclases de `AccessTokenProvider` para que los tokens se obtengan mediante su código de cliente, pero por ahora vamos a usar simplemente el que se proporciona en el SDK.</span><span class="sxs-lookup"><span data-stu-id="89ecb-158">It is possible to create your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use the one provided in the SDK.</span></span>

<span data-ttu-id="89ecb-159">Reemplace **FILL-IN-HERE** por los valores reales de la aplicación web de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="89ecb-159">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="89ecb-160">Paso 2: Creación de un objeto de cliente de Azure Data Lake Store (ADLStoreClient)</span><span class="sxs-lookup"><span data-stu-id="89ecb-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="89ecb-161">La creación de un objeto [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) requiere que especifique el nombre de la cuenta de Data Lake Store y el proveedor de token que generó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="89ecb-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you to specify the Data Lake Store account name and the token provider you generated in the last step.</span></span> <span data-ttu-id="89ecb-162">Tenga en cuenta que el nombre de la cuenta de Data Lake Store debe ser un nombre de dominio completo.</span><span class="sxs-lookup"><span data-stu-id="89ecb-162">Note that the Data Lake Store account name needs to be a fully qualified domain name.</span></span> <span data-ttu-id="89ecb-163">Por ejemplo, reemplace **FILL-IN-HERE** por algo similar a **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="89ecb-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just the account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-the-adlstoreclient-to-perform-file-and-directory-operations"></a><span data-ttu-id="89ecb-164">Paso 3: Uso de ADLStoreClient para realizar operaciones de archivo y directorio</span><span class="sxs-lookup"><span data-stu-id="89ecb-164">Step 3: Use the ADLStoreClient to perform file and directory operations</span></span>
<span data-ttu-id="89ecb-165">El código siguiente contiene fragmentos de código de ejemplo de algunas operaciones comunes.</span><span class="sxs-lookup"><span data-stu-id="89ecb-165">The code below contains example snippets of some common operations.</span></span> <span data-ttu-id="89ecb-166">Puede buscar en todos los [documentos de la API de SDK de Java de Data Lake Store](https://azure.github.io/azure-data-lake-store-java/javadoc/) del objeto **ADLStoreClient** para ver otras operaciones.</span><span class="sxs-lookup"><span data-stu-id="89ecb-166">You can look at the full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of the **ADLStoreClient** object to see other operations.</span></span>

<span data-ttu-id="89ecb-167">Tenga en cuenta que los archivos se leen y escribes mediante secuencias de Java estándar.</span><span class="sxs-lookup"><span data-stu-id="89ecb-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="89ecb-168">Esto significa que puede crear niveles de cualquiera de las secuencias de Java sobre las secuencias de Data Lake Store para beneficiarse de la capacidad estándar de Java (por ejemplo, secuencias impresión para la salida con formato o cualquiera de las secuencias de compresión o cifrado para una capacidad adicional en la parte superior, etc.).</span><span class="sxs-lookup"><span data-stu-id="89ecb-168">This means that you can layer any of the Java streams on top of the Data Lake Store streams to benefit from standard Java functionality (e.g., Print streams for formatted output, or any of the compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is the same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append to file
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate the two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename the file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all the subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-the-application"></a><span data-ttu-id="89ecb-169">Paso 4: Compilación y ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="89ecb-169">Step 4: Build and run the application</span></span>
1. <span data-ttu-id="89ecb-170">Para ejecutarla desde un IDE, localícela y presione el botón **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="89ecb-170">To run from within an IDE, locate and press the **Run** button.</span></span> <span data-ttu-id="89ecb-171">Para ejecutarla desde Maven, utilice [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="89ecb-171">To run from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="89ecb-172">Para generar un archivo jar independiente que puede ejecutar desde la línea de comandos, genere el archivo jar con todas las dependencias incluidas mediante el [complemento de ensamblado de Maven](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="89ecb-172">To produce a standalone jar that you can run from command-line build the jar with all dependencies included, using the [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="89ecb-173">El archivo pom.xml en el [ejemplo de código fuente en github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) tiene un ejemplo de cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="89ecb-173">The pom.xml in the [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how to do this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89ecb-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89ecb-174">Next steps</span></span>
* [<span data-ttu-id="89ecb-175">Explorar JavaDoc para el SDK de Java</span><span class="sxs-lookup"><span data-stu-id="89ecb-175">Explore JavaDoc for the Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="89ecb-176">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="89ecb-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="89ecb-177">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="89ecb-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="89ecb-178">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="89ecb-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

