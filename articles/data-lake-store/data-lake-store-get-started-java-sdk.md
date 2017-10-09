---
title: "las aplicaciones de Java SDK toodevelop Hola de aaaUse en el almacén de Azure Data Lake | Documentos de Microsoft"
description: "Usar una cuenta de almacén de Data Lake del SDK de Java de almacén de Azure Data Lake toocreate y realizar operaciones básicas en hello almacén de Data Lake"
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
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="888d4-103">Introducción al Almacén de Azure Data Lake mediante Java</span><span class="sxs-lookup"><span data-stu-id="888d4-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="888d4-104">Portal</span><span class="sxs-lookup"><span data-stu-id="888d4-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="888d4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="888d4-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="888d4-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="888d4-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="888d4-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="888d4-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="888d4-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="888d4-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="888d4-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="888d4-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="888d4-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="888d4-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="888d4-111">Python</span><span class="sxs-lookup"><span data-stu-id="888d4-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="888d4-112">Obtenga información acerca de cómo toouse Hola SDK de Java de almacén de Azure Data Lake tooperform las operaciones básicas, como crean carpetas, cargar y descargar archivos de datos, etcetera. Para más información sobre Data Lake, consulte [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="888d4-112">Learn how toouse hello Azure Data Lake Store Java SDK tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="888d4-113">Puede tener acceso a documentos de la API del SDK de Java de hello para el almacén de Azure Data Lake en [documentos de la API de Java de almacén de Azure datos Lake](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="888d4-113">You can access hello Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="888d4-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="888d4-114">Prerequisites</span></span>
* <span data-ttu-id="888d4-115">Kit de desarrollo de Java (JDK 7 o superior, con Java versión 1.7 o posterior).</span><span class="sxs-lookup"><span data-stu-id="888d4-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="888d4-116">Cuenta de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="888d4-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="888d4-117">Siga las instrucciones de hello en [empezar a trabajar con el almacén de Azure Data Lake con hello Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="888d4-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="888d4-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="888d4-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="888d4-119">Este tutorial usa Maven para crear las dependencias de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="888d4-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="888d4-120">Aunque es posible toobuild sin usar un sistema de compilación como Maven o Gradle, asegúrese de estos sistemas es mucho más fácil de dependencias de toomanage.</span><span class="sxs-lookup"><span data-stu-id="888d4-120">Although it is possible toobuild without using a build system like Maven or Gradle, these systems make is much easier toomanage dependencies.</span></span>
* <span data-ttu-id="888d4-121">(Opcional) Y un IDE como [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) o similar.</span><span class="sxs-lookup"><span data-stu-id="888d4-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="888d4-122">¿Cómo se puede autenticar mediante Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="888d4-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="888d4-123">En este tutorial se usa un tooretrieve secreto de Azure AD aplicación cliente un token de Azure Active Directory (autenticación de servicio a servicio).</span><span class="sxs-lookup"><span data-stu-id="888d4-123">In this tutorial we use a Azure AD application client secret tooretrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="888d4-124">Usamos este token toocreate un archivo de las operaciones de tooperform de objetos de almacén de Data Lake cliente y operaciones de directorio.</span><span class="sxs-lookup"><span data-stu-id="888d4-124">We use this token toocreate an Data Lake Store client object tooperform operations file and directory operations.</span></span> <span data-ttu-id="888d4-125">Para obtener instrucciones sobre cómo tooauthenticate con el almacén de Azure Data Lake Hola secreto del cliente, realizamos Hola siguiendo los pasos de alto nivel:</span><span class="sxs-lookup"><span data-stu-id="888d4-125">For instructions on how tooauthenticate with Azure Data Lake Store using hello client secret, we perform hello following high-level steps:</span></span>

1. <span data-ttu-id="888d4-126">Creación de una aplicación web de Azure AD</span><span class="sxs-lookup"><span data-stu-id="888d4-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="888d4-127">Recuperar Id. de cliente de hello, secreto del cliente y extremo de token para hello aplicación web de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="888d4-127">Retrieve hello client ID, client secret, and token endpoint for hello Azure AD web application.</span></span>
3. <span data-ttu-id="888d4-128">Configurar el acceso para la aplicación web de Azure AD de hello en hello almacén de Data Lake archivo o carpeta que desee tooaccess de hello aplicación Java que está creando.</span><span class="sxs-lookup"><span data-stu-id="888d4-128">Configure access for hello Azure AD web application on hello Data Lake Store file/folder that you want tooaccess from hello Java application you are creating.</span></span>

<span data-ttu-id="888d4-129">Para obtener instrucciones sobre cómo tooperform estos pasos, consulte [crear una aplicación de Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="888d4-129">For instructions on how tooperform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="888d4-130">Azure Active Directory proporciona que otras opciones también tooretrieve un token.</span><span class="sxs-lookup"><span data-stu-id="888d4-130">Azure Active Directory provides other options as well tooretrieve a token.</span></span> <span data-ttu-id="888d4-131">Puede elegir entre una serie de toosuit de mecanismos de autenticación diferentes su escenario, por ejemplo, una aplicación que se ejecuta en un explorador, una aplicación distribuida como una aplicación de escritorio o una aplicación de servidor que se ejecuta de forma local o en una virtual de Azure máquina.</span><span class="sxs-lookup"><span data-stu-id="888d4-131">You can pick from a number of different authentication mechanisms toosuit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="888d4-132">También puede elegir entre distintos tipos de credenciales, como contraseñas, certificados, autenticación en dos fases, etc. Además, Azure Active Directory permite toosynchronize los usuarios de Active Directory local con la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="888d4-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you toosynchronize your on-premises Active Directory users with hello cloud.</span></span> <span data-ttu-id="888d4-133">Para más detalles, consulte [Escenarios de autenticación para Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="888d4-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="888d4-134">Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="888d4-134">Create a Java application</span></span>
<span data-ttu-id="888d4-135">ejemplo de código de Hello disponible [en GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) le guía por el proceso de Hola de crear archivos en el almacén de hello, concatenación de archivos, descargar un archivo y eliminar algunos archivos de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="888d4-135">hello code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through hello process of creating files in hello store, concatenating files, downloading a file, and deleting some files in hello store.</span></span> <span data-ttu-id="888d4-136">En esta sección del artículo Hola le guían por partes principales de Hola de código de hello.</span><span class="sxs-lookup"><span data-stu-id="888d4-136">This section of hello article walk you through hello main parts of hello code.</span></span>

1. <span data-ttu-id="888d4-137">Crear un proyecto de Maven con [mvn Arquetipo](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) de Hola de línea de comandos o con el IDE.</span><span class="sxs-lookup"><span data-stu-id="888d4-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from hello command-line or using an IDE.</span></span> <span data-ttu-id="888d4-138">Para obtener instrucciones sobre cómo toocreate un Java proyecto usando IntelliJ, consulte [aquí](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="888d4-138">For instructions on how toocreate a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="888d4-139">Para obtener instrucciones sobre cómo toocreate un proyecto usando Eclipse, consulte [aquí](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="888d4-139">For instructions on how toocreate a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="888d4-140">Agregar Hola siguiendo las dependencias tooyour Maven **pom.xml** archivo.</span><span class="sxs-lookup"><span data-stu-id="888d4-140">Add hello following dependencies tooyour Maven **pom.xml** file.</span></span> <span data-ttu-id="888d4-141">Agregar Hola siguiente fragmento de texto entre hello  **\</version >** hello y etiqueta  **\</proyecto >** etiqueta:</span><span class="sxs-lookup"><span data-stu-id="888d4-141">Add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>
   
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
   
    <span data-ttu-id="888d4-142">Hola primera dependencia es toouse Hola SDK de almacén de Data Lake (`azure-data-lake-store-sdk`) del repositorio de maven Hola.</span><span class="sxs-lookup"><span data-stu-id="888d4-142">hello first dependency is toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) from hello maven repository.</span></span> <span data-ttu-id="888d4-143">Hola segunda dependencia (`slf4j-nop`) es toospecify qué toouse del marco de trabajo de registro para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="888d4-143">hello second dependency (`slf4j-nop`) is toospecify which logging framework toouse for this application.</span></span> <span data-ttu-id="888d4-144">usa Hello SDK de almacén de Data Lake [slf4j](http://www.slf4j.org/) fachada de registro, que permite elegir un número de marcos de registro populares, como log4j, Java, registro, logback, etc., o no existe ningún registro.</span><span class="sxs-lookup"><span data-stu-id="888d4-144">hello Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="888d4-145">En este ejemplo, se deshabilitará el registro, por lo tanto, usamos hello **slf4j-nop** enlace.</span><span class="sxs-lookup"><span data-stu-id="888d4-145">For this example, we will disable logging, hence we use hello **slf4j-nop** binding.</span></span> <span data-ttu-id="888d4-146">toouse otras opciones de registro de la aplicación, consulte [aquí](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="888d4-146">toouse other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-hello-application-code"></a><span data-ttu-id="888d4-147">Agregar código de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="888d4-147">Add hello application code</span></span>
<span data-ttu-id="888d4-148">Hay tres partes principales toohello código.</span><span class="sxs-lookup"><span data-stu-id="888d4-148">There are three main parts toohello code.</span></span>

1. <span data-ttu-id="888d4-149">Obtener token de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="888d4-149">Obtain hello Azure Active Directory token</span></span>
2. <span data-ttu-id="888d4-150">Utilice Hola token toocreate un cliente de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="888d4-150">Use hello token toocreate a Data Lake Store client.</span></span>
3. <span data-ttu-id="888d4-151">Usar operaciones de tooperform de cliente de almacén de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="888d4-151">Use hello Data Lake Store client tooperform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="888d4-152">Paso 1: Obtención de un token de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="888d4-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="888d4-153">Hola SDK de almacén de Data Lake proporciona métodos útiles que permiten administrar tokens de seguridad de hello necesarios tootalk toohello cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="888d4-153">hello Data Lake Store SDK provides convenient methods that let you manage hello security tokens needed tootalk toohello Data Lake Store account.</span></span> <span data-ttu-id="888d4-154">Sin embargo, Hola SDK no impone que utilizará estos métodos solamente.</span><span class="sxs-lookup"><span data-stu-id="888d4-154">However, hello SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="888d4-155">Puede usar alguna otra forma de obtener el símbolo (token), como el uso de hello [SDK de Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java), o su propio código personalizado.</span><span class="sxs-lookup"><span data-stu-id="888d4-155">You can use any other means of obtaining token as well, like using hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="888d4-156">Hola toouse SDK de almacén de Data Lake tooobtain símbolo (token) para la aplicación Web de Active Directory de hello que creó anteriormente, use uno de subclase de Hola de `AccessTokenProvider` (ejemplo de Hola siguiente utiliza `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="888d4-156">toouse hello Data Lake Store SDK tooobtain token for hello Active Directory Web application you created earlier, use one of hello subclasses of `AccessTokenProvider` (hello example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="888d4-157">Hola proveedor de tokens cachés Hola credenciales utilizan el token de hello tooobtain en la memoria y renueva automáticamente el token de hello si se trata de tooexpire.</span><span class="sxs-lookup"><span data-stu-id="888d4-157">hello token provider caches hello creds used tooobtain hello token in memory, and automatically renews hello token if it is about tooexpire.</span></span> <span data-ttu-id="888d4-158">Es posible toocreate su propia subclase de `AccessTokenProvider` para los tokens se obtienen mediante el código de cliente, pero por ahora vamos a simplemente use Hola uno se proporcionan en hello SDK.</span><span class="sxs-lookup"><span data-stu-id="888d4-158">It is possible toocreate your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use hello one provided in hello SDK.</span></span>

<span data-ttu-id="888d4-159">Reemplace **rellenar en aquí** con valores reales de Hola para hello aplicación Web de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="888d4-159">Replace **FILL-IN-HERE** with hello actual values for hello Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="888d4-160">Paso 2: Creación de un objeto de cliente de Azure Data Lake Store (ADLStoreClient)</span><span class="sxs-lookup"><span data-stu-id="888d4-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="888d4-161">Crear un [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) objeto requiere toospecify Hola almacén de Data Lake cuenta hello y nombre de proveedor de tokens que generó en el último paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="888d4-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you toospecify hello Data Lake Store account name and hello token provider you generated in hello last step.</span></span> <span data-ttu-id="888d4-162">Tenga en cuenta que Hola cuenta de almacén de Data Lake nombre necesita toobe un nombre de dominio completo.</span><span class="sxs-lookup"><span data-stu-id="888d4-162">Note that hello Data Lake Store account name needs toobe a fully qualified domain name.</span></span> <span data-ttu-id="888d4-163">Por ejemplo, reemplace **FILL-IN-HERE** por algo similar a **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="888d4-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a><span data-ttu-id="888d4-164">Paso 3: Usar operaciones de archivo y directorio de la tooperform del ADLStoreClient Hola</span><span class="sxs-lookup"><span data-stu-id="888d4-164">Step 3: Use hello ADLStoreClient tooperform file and directory operations</span></span>
<span data-ttu-id="888d4-165">código de Hello siguiente contiene fragmentos de código de ejemplo de algunas operaciones comunes.</span><span class="sxs-lookup"><span data-stu-id="888d4-165">hello code below contains example snippets of some common operations.</span></span> <span data-ttu-id="888d4-166">Puede mirar Hola completa [documentos de API de SDK de Java del almacén de datos Lake](https://azure.github.io/azure-data-lake-store-java/javadoc/) de hello **ADLStoreClient** objeto toosee otras operaciones.</span><span class="sxs-lookup"><span data-stu-id="888d4-166">You can look at hello full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of hello **ADLStoreClient** object toosee other operations.</span></span>

<span data-ttu-id="888d4-167">Tenga en cuenta que los archivos se leen y escribes mediante secuencias de Java estándar.</span><span class="sxs-lookup"><span data-stu-id="888d4-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="888d4-168">Esto significa que puede crear niveles en cualquiera de las secuencias de Java de Hola sobre hello que toobenefit de funcionalidad de Java estándar (por ejemplo, impresión flujos de salida con formato, o cualquiera de las secuencias de compresión o cifrado de Hola para una funcionalidad adicional en almacén de Data Lake se transmita por secuencias etcetera superior,.).</span><span class="sxs-lookup"><span data-stu-id="888d4-168">This means that you can layer any of hello Java streams on top of hello Data Lake Store streams toobenefit from standard Java functionality (e.g., Print streams for formatted output, or any of hello compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
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

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a><span data-ttu-id="888d4-169">Paso 4: Compilar y ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="888d4-169">Step 4: Build and run hello application</span></span>
1. <span data-ttu-id="888d4-170">toorun desde dentro de un IDE, buscar y presione hello **ejecutar** botón.</span><span class="sxs-lookup"><span data-stu-id="888d4-170">toorun from within an IDE, locate and press hello **Run** button.</span></span> <span data-ttu-id="888d4-171">toorun de Maven, use [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="888d4-171">toorun from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="888d4-172">un archivo jar independiente que se puede ejecutar desde jar de Hola de compilación de línea de comandos con todas las dependencias incluidas, con hello tooproduce [Maven ensamblado complemento](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="888d4-172">tooproduce a standalone jar that you can run from command-line build hello jar with all dependencies included, using hello [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="888d4-173">Hola pom.xml Hola [código fuente de ejemplo en github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) tiene un ejemplo de cómo toodo esto.</span><span class="sxs-lookup"><span data-stu-id="888d4-173">hello pom.xml in hello [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how toodo this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="888d4-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="888d4-174">Next steps</span></span>
* [<span data-ttu-id="888d4-175">Explorar JavaDoc para hello SDK de Java</span><span class="sxs-lookup"><span data-stu-id="888d4-175">Explore JavaDoc for hello Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="888d4-176">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="888d4-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="888d4-177">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="888d4-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="888d4-178">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="888d4-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

