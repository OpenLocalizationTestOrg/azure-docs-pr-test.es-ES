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
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a>Cosmos Azure DB: Tutorial de aplicación de consola C++ para hello API de documentos
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 
 

Tutorial de C++ de bienvenida toohello de hello API de documentos de base de datos de Azure Cosmos están aprobados SDK para C++. Al terminar este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y realiza consultas en ellos, incluida una base de datos de C++.

Describiremos:

* Creación y conexión de cuenta de base de datos de Azure Cosmos tooan
* Configuración de la aplicación
* Creación de una base de datos Azure Cosmos DB en C++
* Creación de una colección
* Creación de documentos JSON
* Consultar la colección de Hola
* Sustitución de un documento
* Eliminación de un documento
* Eliminar base de datos de base de datos de C++ Azure Cosmos Hola

¿No tiene tiempo? ¡No se preocupe! está disponible en la solución completa de Hello [GitHub](https://github.com/stalker314314/DocumentDBCpp). Vea [obtener la solución completa de hello](#GetSolution) para obtener instrucciones rápidas.

Después de haber completado el tutorial de C++ de hello, por favor, use Hola botones de voto final Hola de esta página toogive nos comentarios. 

Si desea que nos toocontact directamente, cree libre tooinclude dirección de su correo electrónico en sus comentarios o [llegar aquí toous](https://www.research.net/r/8BKRJ3Z). 

Comencemos.

## <a name="prerequisites-for-hello-c-tutorial"></a>Requisitos previos para el tutorial de hello C++
Asegúrese de que tiene Hola siguientes:

* Una cuenta de Azure activa. Si no tiene una, puede registrarse para obtener una [prueba gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio](https://www.visualstudio.com/downloads/), con componentes del lenguaje C++ Hola instalados.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Paso 1: Creación de una cuenta de Azure Cosmos DB
Vamos a crear una cuenta de Azure Cosmos DB. Si ya tiene una cuenta que desee toouse, puede pasar demasiado[la instalación de la aplicación de C++](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupC++"></a>Paso 2: Configuración de la aplicación de C++
1. Abra Visual Studio y, a continuación, en hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**. 
2. Hola **nuevo proyecto** ventana, en hello **instalado** panel, expanda **Visual C++**, haga clic en **Win32**y, a continuación, haga clic en  **Aplicación de consola Win32**. Asigne un nombre hello proyecto hellodocumentdb y, a continuación, haga clic en **Aceptar**. 
   
    ![Captura de pantalla del Asistente para proyecto nuevo de Hola](media/documentdb-cpp-get-started/hello.png)
3. Cuando se inicia el Asistente para aplicaciones Win32 de hello, haga clic en **finalizar**.
4. Una vez que se ha creado el proyecto de hello, abra el Administrador de paquetes de NuGet Hola haciendo clic en hello **hellodocumentdb** proyecto **el Explorador de soluciones** y haga clic en **administrar paquetes de NuGet**. 
   
    ![Captura de pantalla muestra administrar paquetes de NuGet en el menú de proyecto Hola](media/documentdb-cpp-get-started/nuget.png)
5. Hola **NuGet: hellodocumentdb** , haga clic en **examinar**y, a continuación, busque *documentdbcpp*. En los resultados de hello, seleccione DocumentDbCPP, como se muestra en la siguiente captura de pantalla de Hola. Este paquete instala las referencias tooC ++ SDK de REST, que es una dependencia de hello DocumentDbCPP.  
   
    ![Paquete de captura de pantalla mostrando hello DocumentDbCpp resaltado](media/documentdb-cpp-get-started/cpp.png)
   
    Una vez que los paquetes de saludo se han agregado tooyour proyecto, se está escribiendo código todos los toostart de conjunto.   

## <a id="Config"></a>Paso 3: Copia de los detalles de la conexión de Azure Portal para la base de datos de Azure Cosmos DB
Mostrar [portal de Azure](https://portal.azure.com) y atravesar la cuenta de base de datos de base de datos de Azure Cosmos toohello que ha creado. Necesitamos Hola URI y la clave principal de Hola desde el portal de Azure en hello siguiente paso tooestablish una conexión desde el fragmento de código de C++. 

![Azure Cosmos URI de base de datos y las claves de hello portal de Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <a id="Connect"></a>Paso 4: Conectar la cuenta de base de datos de Azure Cosmos tooan
1. Hola después de código fuente de tooyour encabezados y los espacios de nombres, después de agregar `#include "stdafx.h"`.
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. A continuación, agregue código tooyour main (función) siguiente de Hola y reemplaza configuración de la cuenta de hello y toomatch de clave principal de la configuración de base de datos de Azure Cosmos del paso 3. 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    Ahora que tiene el cliente de documentos de hello código tooinitialize hello, echemos un vistazo a trabajar con los recursos de base de datos de Azure Cosmos.

## <a id="CreateDBColl"></a>Paso 5: Creación de una base de datos de C++ y una colección
Antes de que llevamos a cabo este paso, veamos cómo interactúan los documentos, colección y una base de datos para quienes están tooAzure nueva base de datos de Cosmos. Una [base de datos](documentdb-resources.md#databases) es un contenedor lógico de almacenamiento de documentos en varias colecciones. A [colección](documentdb-resources.md#collections) es un contenedor de documentos JSON y Hola asociados lógica de la aplicación de JavaScript. Puede obtener más información acerca de modelo de recursos jerárquica de base de datos de Azure Cosmos de Hola y conceptos de [modelo de base de datos de Azure Cosmos jerárquica de recursos y conceptos](documentdb-resources.md).

toocreate una base de datos y una colección correspondiente agregan Hola siguiente código toohello final de la función principal. Esto crea una base de datos denominada 'FamilyRegistry' y una colección denominada 'FamilyCollection' con configuración de cliente de hello declarado en el paso anterior de Hola.

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <a id="CreateDoc"></a>Paso 6: Creación de un documento
Los [documentos](documentdb-resources.md#documents) son contenido JSON definido por el usuario (arbitrario). Ahora puede insertar un documento en Azure Cosmos DB. Puede crear un documento mediante la copia de hello siguiente código en extremo Hola de función principal de Hola. 

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

toosummarize, este código crea una base de datos de la base de datos de Azure Cosmos, colección y documentos, que puede consultar en Document Explorer en el portal de Azure. 

![Tutorial de C++: diagrama que ilustra la relación jerárquica de hello entre la cuenta de hello, base de datos de hello, colección Hola y Hola documentos](media/documentdb-cpp-get-started/docs.png)

## <a id="QueryDB"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB
Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones. Hello código de ejemplo siguiente muestra una consulta realizada mediante sintaxis SQL que puede ejecutar en documentos de Hola que se creó en el paso anterior de Hola.

función Hello tarda argumentos Hola identificador único o Id. de recurso para la recopilación de hello junto con el cliente de documento de Hola y de base de datos de Hola. Agregue este código antes de la función principal.

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

## <a id="Replace"></a>Paso 8: Reemplazo de un documento
Base de datos de Azure Cosmos admite reemplazando documentos JSON, como se muestra en el siguiente código de hello. Agregue este código después de la función de hello executesimplequery.

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

## <a id="Delete"></a>Paso 9: Eliminación de un documento
Azure Cosmos DB es compatible con la eliminación de documentos JSON, puede hacerlo mediante la copia y pegado de hello siguiente código después de la función de hello replacedocument. 

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

## <a id="DeleteDB"></a>Paso 10: Eliminación de una base de datos
Eliminar base de datos de hello creado quita la base de datos de Hola y todos los recursos secundarios (colecciones, documentos, etcetera).

Copie y pegue Hola siguiente fragmento de código (limpieza de función) después de la base de datos de hello deletedocument función tooremove hello y todos los recursos secundarios de Hola.

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Run"></a>Paso 11: Ejecución de la aplicación C++
Se ha agregado código toocreate, consultar, modificar y eliminar distintos recursos de base de datos de Azure Cosmos.  Permítanos ahora conecte esto agregando llamadas toothese diferentes funciones de la función main en hellodocumentdb.cpp junto con algunos mensajes de diagnóstico.

Puede hacerlo mediante la sustitución Hola main (función) de la aplicación con el siguiente código de hello. Este escrituras por hello account_configuration_uri y primary_key ha copiado en el código de hello en el paso 3, por lo que esa línea o copia valores de hello en vuelva a guardar desde el portal de Hola. 

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

Ahora debería ser capaz de toobuild y ejecute el código en Visual Studio presionando F5 u o bien en ventana de terminal de hello localizando aplicación hello y ejecuta Hola ejecutable. 

Debería ver la salida de hello de la aplicación iniciada get. salida de Hello debe coincidir con la siguiente captura de pantalla de Hola.

![Salida de la aplicación de C++ de Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

¡Enhorabuena! Ha completado el tutorial de C++ de Hola y tienen su primera aplicación de consola de base de datos de Azure Cosmos!

## <a id="GetSolution"></a>Obtener Hola completa C++ solución del tutorial
solución GetStarted de hello toobuild que contiene todos los ejemplos de hello en este artículo, necesita siguiente de hello:

* [Cuenta de Azure Cosmos DB][create-account].
* Hola [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solución disponible en GitHub.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[supervisar una cuenta de base de datos de Azure Cosmos](monitor-accounts.md).
* Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).
* Obtener más información sobre el modelo de programación de Hola Hola sección desarrollar de hello [página de documentación de la base de datos de Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account


