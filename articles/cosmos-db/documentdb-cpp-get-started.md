---
title: Tutorial de C++ para Azure Cosmos DB | Microsoft Docs
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
ms.openlocfilehash: 7d8de973765830ccd7983182bc1bb19b1e01e505
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-the-documentdb-api"></a><span data-ttu-id="06166-104">Cosmos Azure DB: tutorial de la aplicación de consola de C++ para la API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="06166-104">Azure Cosmos DB: C++ console application tutorial for the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="06166-105">.NET</span><span class="sxs-lookup"><span data-stu-id="06166-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="06166-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="06166-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="06166-107">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="06166-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="06166-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="06166-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="06166-109">Java</span><span class="sxs-lookup"><span data-stu-id="06166-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="06166-110">C++</span><span class="sxs-lookup"><span data-stu-id="06166-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="06166-111">Bienvenido al tutorial de C++ para el SDK aprobado de la API de DocumentDB de Azure Cosmos DB para C++.</span><span class="sxs-lookup"><span data-stu-id="06166-111">Welcome to the C++ tutorial for the Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="06166-112">Al terminar este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y realiza consultas en ellos, incluida una base de datos de C++.</span><span class="sxs-lookup"><span data-stu-id="06166-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="06166-113">Describiremos:</span><span class="sxs-lookup"><span data-stu-id="06166-113">We'll cover:</span></span>

* <span data-ttu-id="06166-114">Creación de una cuenta de Azure Cosmos DB y conexión a ella</span><span class="sxs-lookup"><span data-stu-id="06166-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="06166-115">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="06166-115">Setting up your application</span></span>
* <span data-ttu-id="06166-116">Creación de una base de datos Azure Cosmos DB en C++</span><span class="sxs-lookup"><span data-stu-id="06166-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="06166-117">Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="06166-117">Creating a collection</span></span>
* <span data-ttu-id="06166-118">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="06166-118">Creating JSON documents</span></span>
* <span data-ttu-id="06166-119">Consulta de la colección</span><span class="sxs-lookup"><span data-stu-id="06166-119">Querying the collection</span></span>
* <span data-ttu-id="06166-120">Sustitución de un documento</span><span class="sxs-lookup"><span data-stu-id="06166-120">Replacing a document</span></span>
* <span data-ttu-id="06166-121">Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="06166-121">Deleting a document</span></span>
* <span data-ttu-id="06166-122">Eliminación de la base de datos Azure Cosmos DB en C++</span><span class="sxs-lookup"><span data-stu-id="06166-122">Deleting the C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="06166-123">¿No tiene tiempo?</span><span class="sxs-lookup"><span data-stu-id="06166-123">Don't have time?</span></span> <span data-ttu-id="06166-124">¡No se preocupe!</span><span class="sxs-lookup"><span data-stu-id="06166-124">Don't worry!</span></span> <span data-ttu-id="06166-125">La solución completa está disponible en [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="06166-125">The complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="06166-126">Consulte [Obtención de la solución completa](#GetSolution) para obtener instrucciones rápidas.</span><span class="sxs-lookup"><span data-stu-id="06166-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="06166-127">Después de haber completado el tutorial de C++, use los botones de votación en la parte inferior de esta página para enviar comentarios.</span><span class="sxs-lookup"><span data-stu-id="06166-127">After you've completed the C++ tutorial, please use the voting buttons at the bottom of this page to give us feedback.</span></span> 

<span data-ttu-id="06166-128">Si quiere que nos pongamos en contacto directamente con usted, puede incluir su dirección de correo electrónico en los comentarios o, si lo prefiere, [puede ponerse usted en contacto con nosotros aquí](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="06166-128">If you'd like us to contact you directly, feel free to include your email address in your comments or [reach out to us here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="06166-129">Comencemos.</span><span class="sxs-lookup"><span data-stu-id="06166-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-c-tutorial"></a><span data-ttu-id="06166-130">Requisitos previos para el tutorial de C++</span><span class="sxs-lookup"><span data-stu-id="06166-130">Prerequisites for the C++ tutorial</span></span>
<span data-ttu-id="06166-131">Asegúrese de que dispone de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="06166-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="06166-132">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="06166-132">An active Azure account.</span></span> <span data-ttu-id="06166-133">Si no tiene una, puede registrarse para obtener una [prueba gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06166-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="06166-134">[Visual Studio](https://www.visualstudio.com/downloads/), con los componentes del lenguaje C++ instalados.</span><span class="sxs-lookup"><span data-stu-id="06166-134">[Visual Studio](https://www.visualstudio.com/downloads/), with the C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="06166-135">Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="06166-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="06166-136">Vamos a crear una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06166-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="06166-137">Si ya tiene una cuenta que desea usar, puede ir directamente a [Configuración de la aplicación de C++](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="06166-137">If you already have an account you want to use, you can skip ahead to [Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="06166-138"><a id="SetupC++"></a>Paso 2: Configuración de la aplicación de C++</span><span class="sxs-lookup"><span data-stu-id="06166-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="06166-139">Abra Visual Studio en el menú **Archivo**, haga clic en **Nuevo** y, a continuación, haga clic en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="06166-139">Open Visual Studio, and then on the **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="06166-140">En la ventana **Nuevo proyecto** del panel **Instalado** expanda **Visual C++**, haga clic en **Win32**, y luego en **Aplicación de consola Win32**.</span><span class="sxs-lookup"><span data-stu-id="06166-140">In the **New Project** window, in the **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="06166-141">Llame al proyecto hellodocumentdb y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="06166-141">Name the project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Captura de pantalla del Asistente para nuevo proyecto](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="06166-143">Cuando se inicie el Asistente para aplicaciones Win32, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="06166-143">When the Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="06166-144">Una vez creado el proyecto, abra el Administrador de paquetes de NuGet haciendo clic con el botón derecho en el proyecto **hellodocumentdb** en **el Explorador de soluciones** y luego haciendo clic en **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="06166-144">Once the project has been created, open the NuGet package manager by right-clicking the **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Captura de pantalla que muestra Administrar paquetes NuGet en el menú del proyecto](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="06166-146">En la pestaña **NuGet: hellodocumentdb** haga clic en **Examinar**, y, a continuación, busque *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="06166-146">In the **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="06166-147">En los resultados, seleccione DocumentDbCPP, tal como se muestra en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="06166-147">In the results, select DocumentDbCPP, as shown in the following screenshot.</span></span> <span data-ttu-id="06166-148">Este paquete instala las referencias a C++ REST SDK, que es una dependencia para DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="06166-148">This package installs references to C++ REST SDK, which is a dependency for the DocumentDbCPP.</span></span>  
   
    ![Captura de pantalla que muestra el paquete de DocumentDbCpp resaltado](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="06166-150">Una vez que los paquetes se han agregado al proyecto, ya está todo preparado para empezar a escribir código.</span><span class="sxs-lookup"><span data-stu-id="06166-150">Once the packages have been added to your project, we are all set to start writing some code.</span></span>   

## <span data-ttu-id="06166-151"><a id="Config"></a>Paso 3: Copia de los detalles de la conexión de Azure Portal para la base de datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="06166-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="06166-152">Abra [Azure Portal](https://portal.azure.com) y vaya hasta la cuenta de la base de datos de Azure Cosmos DB que ha creado.</span><span class="sxs-lookup"><span data-stu-id="06166-152">Bring up [Azure portal](https://portal.azure.com) and traverse to the Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="06166-153">Se necesitará el URI y la clave principal de Azure Portal en el paso siguiente para establecer una conexión desde el fragmento de código de C++.</span><span class="sxs-lookup"><span data-stu-id="06166-153">We will need the URI and the primary key from Azure portal in the next step to establish a connection from our C++ code snippet.</span></span> 

![Identificador URI y claves de Azure Cosmos DB en Azure Portal](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="06166-155"><a id="Connect"></a>Paso 4: Conexión a una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="06166-155"><a id="Connect"></a>Step 4: Connect to an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="06166-156">Agregue los siguientes encabezados y espacios de nombres al código fuente, después de `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="06166-156">Add the following headers and namespaces to your source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="06166-157">A continuación, agregue el código siguiente a la función principal y reemplace la configuración de la cuenta y la clave principal para que coincidan con la configuración de Azure Cosmos DB del paso 3.</span><span class="sxs-lookup"><span data-stu-id="06166-157">Next add the following code to your main function and replace the account configuration and primary key to match your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="06166-158">Ahora que tiene el código necesario para inicializar el cliente de DocumentDB, se explicará cómo usar los recursos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06166-158">Now that you have the code to initialize the documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="06166-159"><a id="CreateDBColl"></a>Paso 5: Creación de una base de datos de C++ y una colección</span><span class="sxs-lookup"><span data-stu-id="06166-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="06166-160">Antes realizar este paso, vamos a explicar la forma de interacción de las bases de datos, las colecciones y los documentos para aquellos que no estén familiarizados con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06166-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new to Azure Cosmos DB.</span></span> <span data-ttu-id="06166-161">Una [base de datos](documentdb-resources.md#databases) es un contenedor lógico de almacenamiento de documentos en varias colecciones.</span><span class="sxs-lookup"><span data-stu-id="06166-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="06166-162">Una [colección](documentdb-resources.md#collections) es un contenedor de documentos JSON y la lógica de aplicación de JavaScript asociada.</span><span class="sxs-lookup"><span data-stu-id="06166-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="06166-163">Para más información acerca del modelo jerárquico de recursos y de los conceptos de Azure Cosmos DB, consulte [Modelo jerárquico de recursos y conceptos básicos de DocumentDB](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="06166-163">You can learn more about the Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="06166-164">Para crear una base de datos y la colección correspondiente agregue el código siguiente al final de la función principal.</span><span class="sxs-lookup"><span data-stu-id="06166-164">To create a database and a corresponding collection add the following code to the end of your main function.</span></span> <span data-ttu-id="06166-165">Esto crea una base de datos denominada "FamilyRegistry" y una colección denominada "FamilyCollection" usando la configuración de cliente que declaró en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="06166-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using the client configuration you declared in the previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="06166-166"><a id="CreateDoc"></a>Paso 6: Creación de un documento</span><span class="sxs-lookup"><span data-stu-id="06166-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="06166-167">Los [documentos](documentdb-resources.md#documents) son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="06166-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="06166-168">Ahora puede insertar un documento en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06166-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="06166-169">Puede crear un documento copiando el código siguiente al final de la función principal.</span><span class="sxs-lookup"><span data-stu-id="06166-169">You can create a document by copying the following code into the end of the main function.</span></span> 

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

<span data-ttu-id="06166-170">En resumen, este código crea una base de datos, una colección y documentos de Azure Cosmos DB que se pueden consultar en el Explorador de documentos en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="06166-170">To summarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Tutorial C++: Diagrama que muestra la relación jerárquica entre la cuenta, la base de datos, la colección y los documentos](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="06166-172"><a id="QueryDB"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="06166-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="06166-173">Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.</span><span class="sxs-lookup"><span data-stu-id="06166-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="06166-174">El siguiente código de ejemplo muestra una consulta realizada mediante la sintaxis de SQL que se puede ejecutar en los documentos creados en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="06166-174">The following sample code shows a query made using SQL syntax that you can run against the documents we created in the previous step.</span></span>

<span data-ttu-id="06166-175">La función toma como argumentos el identificador único o identificador de recurso para la base de datos y la colección junto con el cliente de documento.</span><span class="sxs-lookup"><span data-stu-id="06166-175">The function takes in as arguments the unique identifier or resource id for the database and the collection along with the document client.</span></span> <span data-ttu-id="06166-176">Agregue este código antes de la función principal.</span><span class="sxs-lookup"><span data-stu-id="06166-176">Add this code before main function.</span></span>

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

## <span data-ttu-id="06166-177"><a id="Replace"></a>Paso 8: Reemplazo de un documento</span><span class="sxs-lookup"><span data-stu-id="06166-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="06166-178">Azure Cosmos DB admite la sustitución de documentos JSON, como se muestra en el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="06166-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in the following code.</span></span> <span data-ttu-id="06166-179">Agregue este código después de la función executesimplequery.</span><span class="sxs-lookup"><span data-stu-id="06166-179">Add this code after the executesimplequery function.</span></span>

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

## <span data-ttu-id="06166-180"><a id="Delete"></a>Paso 9: Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="06166-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="06166-181">Azure Cosmos DB admite la eliminación de documentos JSON, para lo que se puede copiar y pegar el código siguiente después de la función replacedocument.</span><span class="sxs-lookup"><span data-stu-id="06166-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting the following code after the replacedocument function.</span></span> 

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

## <span data-ttu-id="06166-182"><a id="DeleteDB"></a>Paso 10: Eliminación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="06166-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="06166-183">La eliminación de la base de datos creada quitará la base de datos y todos los recursos secundarios (colecciones, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="06166-183">Deleting the created database removes the database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="06166-184">Copie y pegue el siguiente fragmento de código (función cleanup) después de la función deletedocument para quitar la base de datos y todos los recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="06166-184">Copy and paste the following code snippet (function cleanup) after the deletedocument function to remove the database and all the child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="06166-185"><a id="Run"></a>Paso 11: Ejecución de la aplicación C++</span><span class="sxs-lookup"><span data-stu-id="06166-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="06166-186">Hemos agregado código para crear, consultar, modificar y eliminar distintos recursos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06166-186">We have now added code to create, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="06166-187">Vamos ahora a conectar esto mediante la adición de llamadas a estas distintas funciones desde la función principal en hellodocumentdb.cpp junto con algunos mensajes de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="06166-187">Let us now wire this up by adding calls to these different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="06166-188">Para ello, reemplace la función principal de la aplicación con el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="06166-188">You can do so by replacing the main function of your application with the following code.</span></span> <span data-ttu-id="06166-189">Con esto se sobrescriben los valores de account_configuration_uri y primary_key que copió en el código en el Paso 3, por lo que debe guardar esa línea o volver a copiar los valores desde el portal.</span><span class="sxs-lookup"><span data-stu-id="06166-189">This writes over the account_configuration_uri and primary_key you copied into the code in Step 3, so save that line or copy the values in again from the portal.</span></span> 

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

<span data-ttu-id="06166-190">Ahora podrá generar y ejecutar el código en Visual Studio presionando F5 o de forma alternativa en la ventana de terminal buscando la aplicación y ejecutando el archivo ejecutable.</span><span class="sxs-lookup"><span data-stu-id="06166-190">You should now be able to build and run your code in Visual Studio by pressing F5 or alternatively in the terminal window by locating the application and running the executable.</span></span> 

<span data-ttu-id="06166-191">Ahora debería ver la salida de la aplicación GetStarted.</span><span class="sxs-lookup"><span data-stu-id="06166-191">You should see the output of your get started app.</span></span> <span data-ttu-id="06166-192">El resultado debería coincidir con la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="06166-192">The output should match the following screenshot.</span></span>

![Salida de la aplicación de C++ de Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="06166-194">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="06166-194">Congratulations!</span></span> <span data-ttu-id="06166-195">Ha completado el tutorial de C++ y tiene la primera aplicación de consola de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06166-195">You've completed the C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="06166-196"><a id="GetSolution"></a> Obtención de la solución completa del tutorial de C++</span><span class="sxs-lookup"><span data-stu-id="06166-196"><a id="GetSolution"></a>Get the complete C++ tutorial solution</span></span>
<span data-ttu-id="06166-197">Para compilar la solución GetStarted que contiene todos los ejemplos de este artículo, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="06166-197">To build the GetStarted solution that contains all the samples in this article, you need the following:</span></span>

* <span data-ttu-id="06166-198">[Cuenta de Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="06166-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="06166-199">La solución [GetStarted](https://github.com/stalker314314/DocumentDBCpp) está disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="06166-199">The [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06166-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="06166-200">Next steps</span></span>
* <span data-ttu-id="06166-201">Información acerca de cómo [supervisar una cuenta de Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="06166-201">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="06166-202">Ejecute las consultas en nuestro conjunto de datos de ejemplo en el [área de consultas](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="06166-202">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="06166-203">Obtenga más información sobre el modelo de programación en la sección sobre desarrollo de la [página de documentación de Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="06166-203">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account

