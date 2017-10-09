---
title: tutorial de aaaC ++ de base de datos de Azure Cosmos | Documentos de Microsoft
description: "Tutorial de C++ que crea una aplicación de consola y una base de datos de C++ mediante un SDK aprobado para C++. Azure Cosmos DB es un servicio de base de datos de escala mundial."
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a><span data-ttu-id="de31c-104">Cosmos Azure DB: Tutorial de aplicación de consola C++ para hello API de documentos</span><span class="sxs-lookup"><span data-stu-id="de31c-104">Azure Cosmos DB: C++ console application tutorial for hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de31c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="de31c-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="de31c-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="de31c-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="de31c-107">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="de31c-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="de31c-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="de31c-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="de31c-109">Java</span><span class="sxs-lookup"><span data-stu-id="de31c-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="de31c-110">C++</span><span class="sxs-lookup"><span data-stu-id="de31c-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="de31c-111">Tutorial de C++ de bienvenida toohello de hello API de documentos de base de datos de Azure Cosmos están aprobados SDK para C++.</span><span class="sxs-lookup"><span data-stu-id="de31c-111">Welcome toohello C++ tutorial for hello Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="de31c-112">Al terminar este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y realiza consultas en ellos, incluida una base de datos de C++.</span><span class="sxs-lookup"><span data-stu-id="de31c-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="de31c-113">Describiremos:</span><span class="sxs-lookup"><span data-stu-id="de31c-113">We'll cover:</span></span>

* <span data-ttu-id="de31c-114">Creación y conexión de cuenta de base de datos de Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="de31c-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="de31c-115">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="de31c-115">Setting up your application</span></span>
* <span data-ttu-id="de31c-116">Creación de una base de datos Azure Cosmos DB en C++</span><span class="sxs-lookup"><span data-stu-id="de31c-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="de31c-117">Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="de31c-117">Creating a collection</span></span>
* <span data-ttu-id="de31c-118">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="de31c-118">Creating JSON documents</span></span>
* <span data-ttu-id="de31c-119">Consultar la colección de Hola</span><span class="sxs-lookup"><span data-stu-id="de31c-119">Querying hello collection</span></span>
* <span data-ttu-id="de31c-120">Sustitución de un documento</span><span class="sxs-lookup"><span data-stu-id="de31c-120">Replacing a document</span></span>
* <span data-ttu-id="de31c-121">Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="de31c-121">Deleting a document</span></span>
* <span data-ttu-id="de31c-122">Eliminar base de datos de base de datos de C++ Azure Cosmos Hola</span><span class="sxs-lookup"><span data-stu-id="de31c-122">Deleting hello C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="de31c-123">¿No tiene tiempo?</span><span class="sxs-lookup"><span data-stu-id="de31c-123">Don't have time?</span></span> <span data-ttu-id="de31c-124">¡No se preocupe!</span><span class="sxs-lookup"><span data-stu-id="de31c-124">Don't worry!</span></span> <span data-ttu-id="de31c-125">está disponible en la solución completa de Hello [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="de31c-125">hello complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="de31c-126">Vea [obtener la solución completa de hello](#GetSolution) para obtener instrucciones rápidas.</span><span class="sxs-lookup"><span data-stu-id="de31c-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="de31c-127">Después de haber completado el tutorial de C++ de hello, por favor, use Hola botones de voto final Hola de esta página toogive nos comentarios.</span><span class="sxs-lookup"><span data-stu-id="de31c-127">After you've completed hello C++ tutorial, please use hello voting buttons at hello bottom of this page toogive us feedback.</span></span> 

<span data-ttu-id="de31c-128">Si desea que nos toocontact directamente, cree libre tooinclude dirección de su correo electrónico en sus comentarios o [llegar aquí toous](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="de31c-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments or [reach out toous here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="de31c-129">Comencemos.</span><span class="sxs-lookup"><span data-stu-id="de31c-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-c-tutorial"></a><span data-ttu-id="de31c-130">Requisitos previos para el tutorial de hello C++</span><span class="sxs-lookup"><span data-stu-id="de31c-130">Prerequisites for hello C++ tutorial</span></span>
<span data-ttu-id="de31c-131">Asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="de31c-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="de31c-132">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="de31c-132">An active Azure account.</span></span> <span data-ttu-id="de31c-133">Si no tiene una, puede registrarse para obtener una [prueba gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de31c-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="de31c-134">[Visual Studio](https://www.visualstudio.com/downloads/), con componentes del lenguaje C++ Hola instalados.</span><span class="sxs-lookup"><span data-stu-id="de31c-134">[Visual Studio](https://www.visualstudio.com/downloads/), with hello C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="de31c-135">Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de31c-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="de31c-136">Vamos a crear una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de31c-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="de31c-137">Si ya tiene una cuenta que desee toouse, puede pasar demasiado[la instalación de la aplicación de C++](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="de31c-137">If you already have an account you want toouse, you can skip ahead too[Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="de31c-138"><a id="SetupC++"></a>Paso 2: Configuración de la aplicación de C++</span><span class="sxs-lookup"><span data-stu-id="de31c-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="de31c-139">Abra Visual Studio y, a continuación, en hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="de31c-139">Open Visual Studio, and then on hello **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="de31c-140">Hola **nuevo proyecto** ventana, en hello **instalado** panel, expanda **Visual C++**, haga clic en **Win32**y, a continuación, haga clic en  **Aplicación de consola Win32**.</span><span class="sxs-lookup"><span data-stu-id="de31c-140">In hello **New Project** window, in hello **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="de31c-141">Asigne un nombre hello proyecto hellodocumentdb y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="de31c-141">Name hello project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Captura de pantalla del Asistente para proyecto nuevo de Hola](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="de31c-143">Cuando se inicia el Asistente para aplicaciones Win32 de hello, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="de31c-143">When hello Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="de31c-144">Una vez que se ha creado el proyecto de hello, abra el Administrador de paquetes de NuGet Hola haciendo clic en hello **hellodocumentdb** proyecto **el Explorador de soluciones** y haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="de31c-144">Once hello project has been created, open hello NuGet package manager by right-clicking hello **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Captura de pantalla muestra administrar paquetes de NuGet en el menú de proyecto Hola](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="de31c-146">Hola **NuGet: hellodocumentdb** , haga clic en **examinar**y, a continuación, busque *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="de31c-146">In hello **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="de31c-147">En los resultados de hello, seleccione DocumentDbCPP, como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="de31c-147">In hello results, select DocumentDbCPP, as shown in hello following screenshot.</span></span> <span data-ttu-id="de31c-148">Este paquete instala las referencias tooC ++ SDK de REST, que es una dependencia de hello DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="de31c-148">This package installs references tooC++ REST SDK, which is a dependency for hello DocumentDbCPP.</span></span>  
   
    ![Paquete de captura de pantalla mostrando hello DocumentDbCpp resaltado](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="de31c-150">Una vez que los paquetes de saludo se han agregado tooyour proyecto, se está escribiendo código todos los toostart de conjunto.</span><span class="sxs-lookup"><span data-stu-id="de31c-150">Once hello packages have been added tooyour project, we are all set toostart writing some code.</span></span>   

## <span data-ttu-id="de31c-151"><a id="Config"></a>Paso 3: Copia de los detalles de la conexión de Azure Portal para la base de datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de31c-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="de31c-152">Mostrar [portal de Azure](https://portal.azure.com) y atravesar la cuenta de base de datos de base de datos de Azure Cosmos toohello que ha creado.</span><span class="sxs-lookup"><span data-stu-id="de31c-152">Bring up [Azure portal](https://portal.azure.com) and traverse toohello Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="de31c-153">Necesitamos Hola URI y la clave principal de Hola desde el portal de Azure en hello siguiente paso tooestablish una conexión desde el fragmento de código de C++.</span><span class="sxs-lookup"><span data-stu-id="de31c-153">We will need hello URI and hello primary key from Azure portal in hello next step tooestablish a connection from our C++ code snippet.</span></span> 

![Azure Cosmos URI de base de datos y las claves de hello portal de Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="de31c-155"><a id="Connect"></a>Paso 4: Conectar la cuenta de base de datos de Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="de31c-155"><a id="Connect"></a>Step 4: Connect tooan Azure Cosmos DB account</span></span>
1. <span data-ttu-id="de31c-156">Hola después de código fuente de tooyour encabezados y los espacios de nombres, después de agregar `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="de31c-156">Add hello following headers and namespaces tooyour source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="de31c-157">A continuación, agregue código tooyour main (función) siguiente de Hola y reemplaza configuración de la cuenta de hello y toomatch de clave principal de la configuración de base de datos de Azure Cosmos del paso 3.</span><span class="sxs-lookup"><span data-stu-id="de31c-157">Next add hello following code tooyour main function and replace hello account configuration and primary key toomatch your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="de31c-158">Ahora que tiene el cliente de documentos de hello código tooinitialize hello, echemos un vistazo a trabajar con los recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="de31c-158">Now that you have hello code tooinitialize hello documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="de31c-159"><a id="CreateDBColl"></a>Paso 5: Creación de una base de datos de C++ y una colección</span><span class="sxs-lookup"><span data-stu-id="de31c-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="de31c-160">Antes de que llevamos a cabo este paso, veamos cómo interactúan los documentos, colección y una base de datos para quienes están tooAzure nueva base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="de31c-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new tooAzure Cosmos DB.</span></span> <span data-ttu-id="de31c-161">Una [base de datos](documentdb-resources.md#databases) es un contenedor lógico de almacenamiento de documentos en varias colecciones.</span><span class="sxs-lookup"><span data-stu-id="de31c-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="de31c-162">A [colección](documentdb-resources.md#collections) es un contenedor de documentos JSON y Hola asociados lógica de la aplicación de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="de31c-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and hello associated JavaScript application logic.</span></span> <span data-ttu-id="de31c-163">Puede obtener más información acerca de modelo de recursos jerárquica de base de datos de Azure Cosmos de Hola y conceptos de [modelo de base de datos de Azure Cosmos jerárquica de recursos y conceptos](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="de31c-163">You can learn more about hello Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="de31c-164">toocreate una base de datos y una colección correspondiente agregan Hola siguiente código toohello final de la función principal.</span><span class="sxs-lookup"><span data-stu-id="de31c-164">toocreate a database and a corresponding collection add hello following code toohello end of your main function.</span></span> <span data-ttu-id="de31c-165">Esto crea una base de datos denominada 'FamilyRegistry' y una colección denominada 'FamilyCollection' con configuración de cliente de hello declarado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="de31c-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using hello client configuration you declared in hello previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="de31c-166"><a id="CreateDoc"></a>Paso 6: Creación de un documento</span><span class="sxs-lookup"><span data-stu-id="de31c-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="de31c-167">Los [documentos](documentdb-resources.md#documents) son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="de31c-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="de31c-168">Ahora puede insertar un documento en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de31c-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="de31c-169">Puede crear un documento mediante la copia de hello siguiente código en extremo Hola de función principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="de31c-169">You can create a document by copying hello following code into hello end of hello main function.</span></span> 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

<span data-ttu-id="de31c-170">toosummarize, este código crea una base de datos de la base de datos de Azure Cosmos, colección y documentos, que puede consultar en Document Explorer en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="de31c-170">toosummarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Tutorial de C++: diagrama que ilustra la relación jerárquica de hello entre la cuenta de hello, base de datos de hello, colección Hola y Hola documentos](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="de31c-172"><a id="QueryDB"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de31c-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="de31c-173">Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.</span><span class="sxs-lookup"><span data-stu-id="de31c-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="de31c-174">Hello código de ejemplo siguiente muestra una consulta realizada mediante sintaxis SQL que puede ejecutar en documentos de Hola que se creó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="de31c-174">hello following sample code shows a query made using SQL syntax that you can run against hello documents we created in hello previous step.</span></span>

<span data-ttu-id="de31c-175">función Hello tarda argumentos Hola identificador único o Id. de recurso para la recopilación de hello junto con el cliente de documento de Hola y de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="de31c-175">hello function takes in as arguments hello unique identifier or resource id for hello database and hello collection along with hello document client.</span></span> <span data-ttu-id="de31c-176">Agregue este código antes de la función principal.</span><span class="sxs-lookup"><span data-stu-id="de31c-176">Add this code before main function.</span></span>

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="de31c-177"><a id="Replace"></a>Paso 8: Reemplazo de un documento</span><span class="sxs-lookup"><span data-stu-id="de31c-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="de31c-178">Base de datos de Azure Cosmos admite reemplazando documentos JSON, como se muestra en el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="de31c-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in hello following code.</span></span> <span data-ttu-id="de31c-179">Agregue este código después de la función de hello executesimplequery.</span><span class="sxs-lookup"><span data-stu-id="de31c-179">Add this code after hello executesimplequery function.</span></span>

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <span data-ttu-id="de31c-180"><a id="Delete"></a>Paso 9: Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="de31c-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="de31c-181">Azure Cosmos DB es compatible con la eliminación de documentos JSON, puede hacerlo mediante la copia y pegado de hello siguiente código después de la función de hello replacedocument.</span><span class="sxs-lookup"><span data-stu-id="de31c-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting hello following code after hello replacedocument function.</span></span> 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="de31c-182"><a id="DeleteDB"></a>Paso 10: Eliminación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="de31c-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="de31c-183">Eliminar base de datos de hello creado quita la base de datos de Hola y todos los recursos secundarios (colecciones, documentos, etcetera).</span><span class="sxs-lookup"><span data-stu-id="de31c-183">Deleting hello created database removes hello database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="de31c-184">Copie y pegue Hola siguiente fragmento de código (limpieza de función) después de la base de datos de hello deletedocument función tooremove hello y todos los recursos secundarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="de31c-184">Copy and paste hello following code snippet (function cleanup) after hello deletedocument function tooremove hello database and all hello child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="de31c-185"><a id="Run"></a>Paso 11: Ejecución de la aplicación C++</span><span class="sxs-lookup"><span data-stu-id="de31c-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="de31c-186">Se ha agregado código toocreate, consultar, modificar y eliminar distintos recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="de31c-186">We have now added code toocreate, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="de31c-187">Permítanos ahora conecte esto agregando llamadas toothese diferentes funciones de la función main en hellodocumentdb.cpp junto con algunos mensajes de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="de31c-187">Let us now wire this up by adding calls toothese different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="de31c-188">Puede hacerlo mediante la sustitución Hola main (función) de la aplicación con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="de31c-188">You can do so by replacing hello main function of your application with hello following code.</span></span> <span data-ttu-id="de31c-189">Este escrituras por hello account_configuration_uri y primary_key ha copiado en el código de hello en el paso 3, por lo que esa línea o copia valores de hello en vuelva a guardar desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="de31c-189">This writes over hello account_configuration_uri and primary_key you copied into hello code in Step 3, so save that line or copy hello values in again from hello portal.</span></span> 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

<span data-ttu-id="de31c-190">Ahora debería ser capaz de toobuild y ejecute el código en Visual Studio presionando F5 u o bien en ventana de terminal de hello localizando aplicación hello y ejecuta Hola ejecutable.</span><span class="sxs-lookup"><span data-stu-id="de31c-190">You should now be able toobuild and run your code in Visual Studio by pressing F5 or alternatively in hello terminal window by locating hello application and running hello executable.</span></span> 

<span data-ttu-id="de31c-191">Debería ver la salida de hello de la aplicación iniciada get.</span><span class="sxs-lookup"><span data-stu-id="de31c-191">You should see hello output of your get started app.</span></span> <span data-ttu-id="de31c-192">salida de Hello debe coincidir con la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="de31c-192">hello output should match hello following screenshot.</span></span>

![Salida de la aplicación de C++ de Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="de31c-194">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="de31c-194">Congratulations!</span></span> <span data-ttu-id="de31c-195">Ha completado el tutorial de C++ de Hola y tienen su primera aplicación de consola de base de datos de Azure Cosmos!</span><span class="sxs-lookup"><span data-stu-id="de31c-195">You've completed hello C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="de31c-196"><a id="GetSolution"></a>Obtener Hola completa C++ solución del tutorial</span><span class="sxs-lookup"><span data-stu-id="de31c-196"><a id="GetSolution"></a>Get hello complete C++ tutorial solution</span></span>
<span data-ttu-id="de31c-197">solución GetStarted de hello toobuild que contiene todos los ejemplos de hello en este artículo, necesita siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="de31c-197">toobuild hello GetStarted solution that contains all hello samples in this article, you need hello following:</span></span>

* <span data-ttu-id="de31c-198">[Cuenta de Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="de31c-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="de31c-199">Hola [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solución disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="de31c-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de31c-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="de31c-200">Next steps</span></span>
* <span data-ttu-id="de31c-201">Obtenga información acerca de cómo demasiado[supervisar una cuenta de base de datos de Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="de31c-201">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="de31c-202">Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="de31c-202">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="de31c-203">Obtener más información sobre el modelo de programación de Hola Hola sección desarrollar de hello [página de documentación de la base de datos de Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="de31c-203">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


