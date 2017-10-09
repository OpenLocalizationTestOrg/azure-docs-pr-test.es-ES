---
title: aaaStore datos no estructurados mediante funciones de Azure y base de datos de Cosmos
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
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a>Almacenamiento de datos no estructurados mediante Azure Functions y Cosmos DB

[Base de datos de Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) es una excelente manera toostore no estructurado y datos JSON. En combinación con Azure Functions, Cosmos DB facilita y agiliza el almacenamiento de datos con mucho menos código que el necesario para almacenar datos en una base de datos relacional.

En las funciones de Azure, los enlaces de entrada y salidos proporcionan una manera declarativa tooconnect tooexternal servicio de datos de la función. En este tema, aprenderá cómo tooupdate una existente C# función tooadd un enlace de salida que almacena los datos no estructurados en un documento de la base de datos de Cosmos. 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a>Adición de un enlace de salida

1. Expanda su Function App y su función.

1. Seleccione **integrar** y **+ nueva salida**, que se encuentra en hello parte superior derecha de la página de Hola. Elija **Azure Cosmos DB** y haga clic en **Seleccionar**.

    ![Adición de un nuevo enlace de salida de Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. Hola de uso **salida de la base de datos de Azure Cosmos** configuración como se especifica en la tabla de hello: 

    ![Configuración del enlace de salida de Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | Configuración      | Valor sugerido  | Descripción                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **Nombre del parámetro de documento** | taskDocument | Nombre que hace referencia el objeto de base de datos de Cosmos toohello en el código. |
    | **Nombre de la base de datos** | taskDatabase | Nombre de base de datos toosave documentos. |
    | **Nombre de colección** | TaskCollection | Nombre de colección de bases de datos de Cosmos DB. |
    | **Si es true, crea la colección y base de datos de base de datos de Cosmos Hola** | Activado | colección de Hello no ya existen, por lo que cree. |

4. Seleccione **New** toohello siguiente **conexión a BD de Cosmos documento** etiqueta y elija **+ crear nuevo**. 

5. Hola de uso **nueva cuenta** configuración como se especifica en la tabla de hello: 

    ![Configuración de la conexión de Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | Configuración      | Valor sugerido  | Descripción                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **Id** | Nombre de base de datos | Identificador único para la base de datos de base de datos de Cosmos Hola  |
    | **API** | SQL (DocumentDB) | Seleccione la API de bases de datos del documento de Hola.  |
    | **Suscripción** | Suscripción de Azure | Suscripción de Azure  |
    | **Grupo de recursos** | myResourceGroup |  Utilice Hola grupo de recursos existente que contiene la aplicación de la función. |
    | **Ubicación**  | WestEurope | Seleccione la aplicación de la función de un lugar próximo tooeither o tooother aplicaciones que usan Hola documentos almacenados.  |

6. Haga clic en **Aceptar** base de datos de toocreate Hola. Puede tardar unos base de datos de Hola de toocreate minutos. Después de crea la base de datos de hello, cadena de conexión de base de datos de Hola se almacena como una configuración de aplicación de la función. nombre de Hola de esta configuración de la aplicación se inserta en **conexión de la cuenta de base de datos de Cosmos**. 
 
8. Después de establece la cadena de conexión de hello, seleccione **guardar** enlace de hello toocreate.

## <a name="update-hello-function-code"></a>Actualizar código de función de Hola

Reemplace Hola existente C# código de la función con el siguiente código de hello:

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
Este ejemplo de código lee las cadenas de consulta de hello solicitud HTTP y les asigna toofields Hola `taskDocument` objeto. Hola `taskDocument` enlace envía datos de objeto de Hola desde este toobe de parámetro de enlace en base de datos de documento enlazado Hola. Hola crear base de datos Hola primera vez que se ejecuta la función hello.

## <a name="test-hello-function-and-database"></a>Función de prueba hello y base de datos

1. Expanda la ventana derecha de Hola y seleccione **prueba**. En **consulta**, haga clic en **+ Agregar parámetro** y agregue Hola después de la cadena de consulta de parámetros toohello:

    + `name`
    + `task`
    + `duedate`

2. Haga clic en **Ejecutar** y compruebe que se devuelve un estado 200.

    ![Configuración del enlace de salida de Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. En hello parte izquierda de hello portal de Azure, expanda la barra de iconos de hello, tipo `cosmos` Hola buscar el campo y, a continuación, seleccione **base de datos de Azure Cosmos**.

    ![Busque Hola servicio base de datos de Cosmos](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. A continuación, seleccione la base de datos de hello seleccione creado, **Explorador de datos**. Expanda hello **colecciones** nodos, seleccione Nuevo documento de Hola y confirmar ese documento hello contiene los valores de cadena de consulta, junto con algunos metadatos adicionales. 

    ![Comprobación de la entrada de Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

Ha agregado correctamente un desencadenador HTTP de tooyour de enlace que almacena los datos no estructurados en una base de datos de la base de datos de Cosmos.

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

Para obtener más información acerca de la base de datos de enlace tooa Cosmos DB, vea [enlaces de base de datos de Azure funciones Cosmos](functions-bindings-documentdb.md).
