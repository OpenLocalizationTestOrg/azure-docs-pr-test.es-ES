---
title: Almacenamiento de datos no estructurados mediante Azure Functions y Cosmos DB
description: Almacenamiento de datos no estructurados mediante Azure Functions y Cosmos DB
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, procesamiento de eventos, Cosmos DB, proceso dinámico, arquitectura sin servidor"
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7c18676ff94ec7da17094abc5f33fb3c6a79895f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a><span data-ttu-id="7f5a1-104">Almacenamiento de datos no estructurados mediante Azure Functions y Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7f5a1-104">Store unstructured data using Azure Functions and Cosmos DB</span></span>

<span data-ttu-id="7f5a1-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) es una excelente manera de almacenar datos no estructurados y JSON.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way to store unstructured and JSON data.</span></span> <span data-ttu-id="7f5a1-106">En combinación con Azure Functions, Cosmos DB facilita y agiliza el almacenamiento de datos con mucho menos código que el necesario para almacenar datos en una base de datos relacional.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-106">Combined with Azure Functions, Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.</span></span>

<span data-ttu-id="7f5a1-107">En Azure Functions, los enlaces de entrada y salida proporcionan una manera declarativa de conectarse a los datos de servicio externos desde su función.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-107">In Azure Functions, input and output bindings provide a declarative way to connect to external service data from your function.</span></span> <span data-ttu-id="7f5a1-108">En este tema, aprenda a actualizar una función de C# existente para agregar un enlace de salida que almacene los datos no estructurados en un documento de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-108">In this topic, learn how to update an existing C# function to add an output binding that stores unstructured data in a Cosmos DB document.</span></span> 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a><span data-ttu-id="7f5a1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7f5a1-110">Prerequisites</span></span>

<span data-ttu-id="7f5a1-111">Para completar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="7f5a1-111">To complete this tutorial:</span></span>

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a><span data-ttu-id="7f5a1-112">Adición de un enlace de salida</span><span class="sxs-lookup"><span data-stu-id="7f5a1-112">Add an output binding</span></span>

1. <span data-ttu-id="7f5a1-113">Expanda su Function App y su función.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-113">Expand both your function app and your function.</span></span>

1. <span data-ttu-id="7f5a1-114">Seleccione **Integrar** y **+ Nueva salida**, que se encuentra en la parte superior derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-114">Select **Integrate** and **+ New Output**, which is at the top right of the page.</span></span> <span data-ttu-id="7f5a1-115">Elija **Azure Cosmos DB** y haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-115">Choose **Azure Cosmos DB**, and click **Select**.</span></span>

    ![Adición de un nuevo enlace de salida de Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. <span data-ttu-id="7f5a1-117">Use la configuración de **salida de Azure Cosmos DB**, tal y como se especifica en la tabla:</span><span class="sxs-lookup"><span data-stu-id="7f5a1-117">Use the **Azure Cosmos DB output** settings as specified in the table:</span></span> 

    ![Configuración del enlace de salida de Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | <span data-ttu-id="7f5a1-119">Configuración</span><span class="sxs-lookup"><span data-stu-id="7f5a1-119">Setting</span></span>      | <span data-ttu-id="7f5a1-120">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="7f5a1-120">Suggested value</span></span>  | <span data-ttu-id="7f5a1-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="7f5a1-121">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="7f5a1-122">**Nombre del parámetro de documento**</span><span class="sxs-lookup"><span data-stu-id="7f5a1-122">**Document parameter name**</span></span> | <span data-ttu-id="7f5a1-123">taskDocument</span><span class="sxs-lookup"><span data-stu-id="7f5a1-123">taskDocument</span></span> | <span data-ttu-id="7f5a1-124">Nombre que hace referencia al objeto de Cosmos DB en el código.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-124">Name that refers to the Cosmos DB object in code.</span></span> |
    | <span data-ttu-id="7f5a1-125">**Nombre de la base de datos**</span><span class="sxs-lookup"><span data-stu-id="7f5a1-125">**Database name**</span></span> | <span data-ttu-id="7f5a1-126">taskDatabase</span><span class="sxs-lookup"><span data-stu-id="7f5a1-126">taskDatabase</span></span> | <span data-ttu-id="7f5a1-127">Nombre de la base de datos para guardar documentos.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-127">Name of database to save documents.</span></span> |
    | <span data-ttu-id="7f5a1-128">**Nombre de colección**</span><span class="sxs-lookup"><span data-stu-id="7f5a1-128">**Collection name**</span></span> | <span data-ttu-id="7f5a1-129">TaskCollection</span><span class="sxs-lookup"><span data-stu-id="7f5a1-129">TaskCollection</span></span> | <span data-ttu-id="7f5a1-130">Nombre de colección de bases de datos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-130">Name of collection of Cosmos DB databases.</span></span> |
    | <span data-ttu-id="7f5a1-131">**Si es true, crea la base de datos y la colección de Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="7f5a1-131">**If true, creates the Cosmos DB database and collection**</span></span> | <span data-ttu-id="7f5a1-132">Activado</span><span class="sxs-lookup"><span data-stu-id="7f5a1-132">Checked</span></span> | <span data-ttu-id="7f5a1-133">La colección no existe, por lo que se crea.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-133">The collection doesn't already exist, so create it.</span></span> |

4. <span data-ttu-id="7f5a1-134">Seleccione **Nuevo** junto a la etiqueta **Conexión al documento de Cosmos DB** y elija **+ Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-134">Select **New** next to the **Cosmos DB document connection** label, and select **+ Create new**.</span></span> 

5. <span data-ttu-id="7f5a1-135">Use la configuración de **Nueva cuenta** tal y como se especifica en la tabla:</span><span class="sxs-lookup"><span data-stu-id="7f5a1-135">Use the **New account** settings as specified in the table:</span></span> 

    ![Configuración de la conexión de Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | <span data-ttu-id="7f5a1-137">Configuración</span><span class="sxs-lookup"><span data-stu-id="7f5a1-137">Setting</span></span>      | <span data-ttu-id="7f5a1-138">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="7f5a1-138">Suggested value</span></span>  | <span data-ttu-id="7f5a1-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="7f5a1-139">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="7f5a1-140">**Id**</span><span class="sxs-lookup"><span data-stu-id="7f5a1-140">**ID**</span></span> | <span data-ttu-id="7f5a1-141">Nombre de base de datos</span><span class="sxs-lookup"><span data-stu-id="7f5a1-141">Name of database</span></span> | <span data-ttu-id="7f5a1-142">Identificador único para la base de datos de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7f5a1-142">Unique ID for the Cosmos DB database</span></span>  |
    | <span data-ttu-id="7f5a1-143">**API**</span><span class="sxs-lookup"><span data-stu-id="7f5a1-143">**API**</span></span> | <span data-ttu-id="7f5a1-144">SQL (DocumentDB)</span><span class="sxs-lookup"><span data-stu-id="7f5a1-144">SQL (DocumentDB)</span></span> | <span data-ttu-id="7f5a1-145">Seleccione la API de base de datos de documentos.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-145">Select the document database API.</span></span>  |
    | <span data-ttu-id="7f5a1-146">**Suscripción**</span><span class="sxs-lookup"><span data-stu-id="7f5a1-146">**Subscription**</span></span> | <span data-ttu-id="7f5a1-147">Suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="7f5a1-147">Azure Subscription</span></span> | <span data-ttu-id="7f5a1-148">Suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="7f5a1-148">Azure Subscription</span></span>  |
    | <span data-ttu-id="7f5a1-149">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="7f5a1-149">**Resource Group**</span></span> | <span data-ttu-id="7f5a1-150">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7f5a1-150">myResourceGroup</span></span> |  <span data-ttu-id="7f5a1-151">Use el grupo de recursos existente que contiene la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-151">Use the existing resource group that contains your function app.</span></span> |
    | <span data-ttu-id="7f5a1-152">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="7f5a1-152">**Location**</span></span>  | <span data-ttu-id="7f5a1-153">WestEurope</span><span class="sxs-lookup"><span data-stu-id="7f5a1-153">WestEurope</span></span> | <span data-ttu-id="7f5a1-154">Seleccione una ubicación cerca de la aplicación de función o de otras aplicaciones que usen los documentos almacenados.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-154">Select a location near to either your function app or to other apps that use the stored documents.</span></span>  |

6. <span data-ttu-id="7f5a1-155">Haga clic en **Aceptar** para crear la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-155">Click **OK** to create the database.</span></span> <span data-ttu-id="7f5a1-156">La operación de creación de la base de datos puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-156">It may take a few minutes to create the database.</span></span> <span data-ttu-id="7f5a1-157">Después de crear la base de datos, la cadena de conexión de base de datos se almacena como una configuración de aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-157">After the database is created, the database connection string is stored as a function app setting.</span></span> <span data-ttu-id="7f5a1-158">El nombre de esta configuración de aplicación se inserta en la **conexión de la cuenta de Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-158">The name of this app setting is inserted in **Cosmos DB account connection**.</span></span> 
 
8. <span data-ttu-id="7f5a1-159">Después de establece la cadena de conexión, seleccione **Guardar** para crear el enlace.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-159">After the connection string is set, select **Save** to create the binding.</span></span>

## <a name="update-the-function-code"></a><span data-ttu-id="7f5a1-160">Actualización del código de la función</span><span class="sxs-lookup"><span data-stu-id="7f5a1-160">Update the function code</span></span>

<span data-ttu-id="7f5a1-161">Reemplace el código existente de la función de C# por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="7f5a1-161">Replace the existing C# function code with the following code:</span></span>

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
<span data-ttu-id="7f5a1-162">Este ejemplo de código lee las cadenas de consulta de la solicitud HTTP y las asigna a los campos del objeto `taskDocument`.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-162">This code sample reads the HTTP Request query strings and assigns them to fields in the `taskDocument` object.</span></span> <span data-ttu-id="7f5a1-163">El enlace `taskDocument` envía los datos del objeto desde este parámetro de enlace para almacenarlos en la base de datos de documentos enlazada.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-163">The `taskDocument` binding sends the object data from this binding parameter to be stored in the bound document database.</span></span> <span data-ttu-id="7f5a1-164">La base de datos se crea la primera vez que se ejecuta la función.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-164">The database is created the first time the function runs.</span></span>

## <a name="test-the-function-and-database"></a><span data-ttu-id="7f5a1-165">Prueba de la función y la base de datos</span><span class="sxs-lookup"><span data-stu-id="7f5a1-165">Test the function and database</span></span>

1. <span data-ttu-id="7f5a1-166">Expanda la ventana derecha y seleccione **Probar**.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-166">Expand the right window and select **Test**.</span></span> <span data-ttu-id="7f5a1-167">En **Consulta**, haga clic en **+ Agregar parámetro** y agregue los siguientes parámetros a la cadena de consulta:</span><span class="sxs-lookup"><span data-stu-id="7f5a1-167">Under **Query**, click **+ Add parameter** and add the following parameters to the query string:</span></span>

    + `name`
    + `task`
    + `duedate`

2. <span data-ttu-id="7f5a1-168">Haga clic en **Ejecutar** y compruebe que se devuelve un estado 200.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-168">Click **Run** and verify that a 200 status is returned.</span></span>

    ![Configuración del enlace de salida de Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. <span data-ttu-id="7f5a1-170">En el lado izquierdo de Azure Portal, expanda la barra de iconos, escriba `cosmos` en el campo de búsqueda y seleccione **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-170">On the left side of the Azure portal, expand the icon bar, type `cosmos` in the search field, and select **Azure Cosmos DB**.</span></span>

    ![Búsqueda del servicio Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. <span data-ttu-id="7f5a1-172">Seleccione la base de datos que creó y luego seleccione **Explorador de datos**.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-172">Select the database you created, then select **Data Explorer**.</span></span> <span data-ttu-id="7f5a1-173">Expanda los nodos de **Colecciones**, seleccione el nuevo documento y confirme que el documento contiene los valores de la cadena de consulta, junto con algunos metadatos adicionales.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-173">Expand the **Collections** nodes, select the new document, and confirm that the document contains your query string values, along with some additional metadata.</span></span> 

    ![Comprobación de la entrada de Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

<span data-ttu-id="7f5a1-175">Ha agregado correctamente un enlace al desencadenador HTTP que almacena datos no estructurados en una base de datos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7f5a1-175">You have successfully added a binding to your HTTP trigger that stores unstructured data in a Cosmos DB database.</span></span>

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="7f5a1-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f5a1-176">Next steps</span></span>

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="7f5a1-177">Para más información sobre el enlace a una base de datos de la base de datos de Cosmos, consulte [Enlaces de Cosmos DB en Azure Functions](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="7f5a1-177">For more information about binding to a Cosmos DB database, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>
