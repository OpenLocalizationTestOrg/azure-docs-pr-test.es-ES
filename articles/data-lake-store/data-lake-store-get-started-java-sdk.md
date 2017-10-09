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
# <a name="get-started-with-azure-data-lake-store-using-java"></a>Introducción al Almacén de Azure Data Lake mediante Java
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK de Java](data-lake-store-get-started-java-sdk.md)
> * [API de REST](data-lake-store-get-started-rest-api.md)
> * [CLI de Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Obtenga información acerca de cómo toouse Hola SDK de Java de almacén de Azure Data Lake tooperform las operaciones básicas, como crean carpetas, cargar y descargar archivos de datos, etcetera. Para más información sobre Data Lake, consulte [Azure Data Lake Store](data-lake-store-overview.md).

Puede tener acceso a documentos de la API del SDK de Java de hello para el almacén de Azure Data Lake en [documentos de la API de Java de almacén de Azure datos Lake](https://azure.github.io/azure-data-lake-store-java/javadoc/).

## <a name="prerequisites"></a>Requisitos previos
* Kit de desarrollo de Java (JDK 7 o superior, con Java versión 1.7 o posterior).
* Cuenta de Azure Data Lake Store. Siga las instrucciones de hello en [empezar a trabajar con el almacén de Azure Data Lake con hello Azure Portal](data-lake-store-get-started-portal.md).
* [Maven](https://maven.apache.org/install.html). Este tutorial usa Maven para crear las dependencias de un proyecto. Aunque es posible toobuild sin usar un sistema de compilación como Maven o Gradle, asegúrese de estos sistemas es mucho más fácil de dependencias de toomanage.
* (Opcional) Y un IDE como [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) o similar.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>¿Cómo se puede autenticar mediante Azure Active Directory?
En este tutorial se usa un tooretrieve secreto de Azure AD aplicación cliente un token de Azure Active Directory (autenticación de servicio a servicio). Usamos este token toocreate un archivo de las operaciones de tooperform de objetos de almacén de Data Lake cliente y operaciones de directorio. Para obtener instrucciones sobre cómo tooauthenticate con el almacén de Azure Data Lake Hola secreto del cliente, realizamos Hola siguiendo los pasos de alto nivel:

1. Creación de una aplicación web de Azure AD
2. Recuperar Id. de cliente de hello, secreto del cliente y extremo de token para hello aplicación web de Azure AD.
3. Configurar el acceso para la aplicación web de Azure AD de hello en hello almacén de Data Lake archivo o carpeta que desee tooaccess de hello aplicación Java que está creando.

Para obtener instrucciones sobre cómo tooperform estos pasos, consulte [crear una aplicación de Active Directory](data-lake-store-authenticate-using-active-directory.md).

Azure Active Directory proporciona que otras opciones también tooretrieve un token. Puede elegir entre una serie de toosuit de mecanismos de autenticación diferentes su escenario, por ejemplo, una aplicación que se ejecuta en un explorador, una aplicación distribuida como una aplicación de escritorio o una aplicación de servidor que se ejecuta de forma local o en una virtual de Azure máquina. También puede elegir entre distintos tipos de credenciales, como contraseñas, certificados, autenticación en dos fases, etc. Además, Azure Active Directory permite toosynchronize los usuarios de Active Directory local con la nube de Hola. Para más detalles, consulte [Escenarios de autenticación para Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md). 

## <a name="create-a-java-application"></a>Creación de una aplicación Java
ejemplo de código de Hello disponible [en GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) le guía por el proceso de Hola de crear archivos en el almacén de hello, concatenación de archivos, descargar un archivo y eliminar algunos archivos de almacén de Hola. En esta sección del artículo Hola le guían por partes principales de Hola de código de hello.

1. Crear un proyecto de Maven con [mvn Arquetipo](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) de Hola de línea de comandos o con el IDE. Para obtener instrucciones sobre cómo toocreate un Java proyecto usando IntelliJ, consulte [aquí](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html). Para obtener instrucciones sobre cómo toocreate un proyecto usando Eclipse, consulte [aquí](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm). 
2. Agregar Hola siguiendo las dependencias tooyour Maven **pom.xml** archivo. Agregar Hola siguiente fragmento de texto entre hello  **\</version >** hello y etiqueta  **\</proyecto >** etiqueta:
   
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
   
    Hola primera dependencia es toouse Hola SDK de almacén de Data Lake (`azure-data-lake-store-sdk`) del repositorio de maven Hola. Hola segunda dependencia (`slf4j-nop`) es toospecify qué toouse del marco de trabajo de registro para esta aplicación. usa Hello SDK de almacén de Data Lake [slf4j](http://www.slf4j.org/) fachada de registro, que permite elegir un número de marcos de registro populares, como log4j, Java, registro, logback, etc., o no existe ningún registro. En este ejemplo, se deshabilitará el registro, por lo tanto, usamos hello **slf4j-nop** enlace. toouse otras opciones de registro de la aplicación, consulte [aquí](http://www.slf4j.org/manual.html#projectDep).

### <a name="add-hello-application-code"></a>Agregar código de la aplicación hello
Hay tres partes principales toohello código.

1. Obtener token de Azure Active Directory Hola
2. Utilice Hola token toocreate un cliente de almacén de Data Lake.
3. Usar operaciones de tooperform de cliente de almacén de Data Lake Hola.

#### <a name="step-1-obtain-an-azure-active-directory-token"></a>Paso 1: Obtención de un token de Azure Active Directory.
Hola SDK de almacén de Data Lake proporciona métodos útiles que permiten administrar tokens de seguridad de hello necesarios tootalk toohello cuenta de almacén de Data Lake. Sin embargo, Hola SDK no impone que utilizará estos métodos solamente. Puede usar alguna otra forma de obtener el símbolo (token), como el uso de hello [SDK de Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java), o su propio código personalizado.

Hola toouse SDK de almacén de Data Lake tooobtain símbolo (token) para la aplicación Web de Active Directory de hello que creó anteriormente, use uno de subclase de Hola de `AccessTokenProvider` (ejemplo de Hola siguiente utiliza `ClientCredsTokenProvider`). Hola proveedor de tokens cachés Hola credenciales utilizan el token de hello tooobtain en la memoria y renueva automáticamente el token de hello si se trata de tooexpire. Es posible toocreate su propia subclase de `AccessTokenProvider` para los tokens se obtienen mediante el código de cliente, pero por ahora vamos a simplemente use Hola uno se proporcionan en hello SDK.

Reemplace **rellenar en aquí** con valores reales de Hola para hello aplicación Web de Azure Active Directory.

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a>Paso 2: Creación de un objeto de cliente de Azure Data Lake Store (ADLStoreClient)
Crear un [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) objeto requiere toospecify Hola almacén de Data Lake cuenta hello y nombre de proveedor de tokens que generó en el último paso de Hola. Tenga en cuenta que Hola cuenta de almacén de Data Lake nombre necesita toobe un nombre de dominio completo. Por ejemplo, reemplace **FILL-IN-HERE** por algo similar a **mydatalakestore.azuredatalakestore.net**.

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a>Paso 3: Usar operaciones de archivo y directorio de la tooperform del ADLStoreClient Hola
código de Hello siguiente contiene fragmentos de código de ejemplo de algunas operaciones comunes. Puede mirar Hola completa [documentos de API de SDK de Java del almacén de datos Lake](https://azure.github.io/azure-data-lake-store-java/javadoc/) de hello **ADLStoreClient** objeto toosee otras operaciones.

Tenga en cuenta que los archivos se leen y escribes mediante secuencias de Java estándar. Esto significa que puede crear niveles en cualquiera de las secuencias de Java de Hola sobre hello que toobenefit de funcionalidad de Java estándar (por ejemplo, impresión flujos de salida con formato, o cualquiera de las secuencias de compresión o cifrado de Hola para una funcionalidad adicional en almacén de Data Lake se transmita por secuencias etcetera superior,.).

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

#### <a name="step-4-build-and-run-hello-application"></a>Paso 4: Compilar y ejecutar la aplicación hello
1. toorun desde dentro de un IDE, buscar y presione hello **ejecutar** botón. toorun de Maven, use [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).
2. un archivo jar independiente que se puede ejecutar desde jar de Hola de compilación de línea de comandos con todas las dependencias incluidas, con hello tooproduce [Maven ensamblado complemento](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html). Hola pom.xml Hola [código fuente de ejemplo en github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) tiene un ejemplo de cómo toodo esto.

## <a name="next-steps"></a>Pasos siguientes
* [Explorar JavaDoc para hello SDK de Java](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)
* [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

