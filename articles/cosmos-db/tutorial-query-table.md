---
title: "¿aaaHow tooquery los datos de tabla en la base de datos de Azure Cosmos? | Microsoft Docs"
description: "Obtenga información acerca de los datos de la tabla en la base de datos de Azure Cosmos tooquery"
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a>Azure Cosmos DB: Cómo Hola tooquery datos de la tabla mediante el uso de API de tabla (vista previa)?

base de datos de Azure Cosmos Hello [API de tabla](table-introduction.md) (vista previa) es compatible con OData y [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) consultas en los datos de clave/valor (tabla).  

En este artículo se trata Hola siguientes tareas: 

> [!div class="checklist"]
> * Consultar datos con hello API de tabla

consultas de este artículo Hello usar Hola según muestra `People` tabla:

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

Dado que base de datos de Azure Cosmos es compatible con hello las API de almacenamiento de tabla de Azure, vea [consultar tablas y entidades] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) para obtener más información sobre cómo Hola tooquery mediante el uso de API de la tabla. 

Para obtener más información sobre las capacidades de premium de Hola que ofrece la base de datos de Azure Cosmos, consulte [base de datos de Azure Cosmos: API de tabla](table-introduction.md) y [desarrollar con hello API de tabla en .NET](tutorial-develop-table-dotnet.md). 

## <a name="prerequisites"></a>Requisitos previos

Para estos toowork consultas, debe tener una cuenta de base de datos de Azure Cosmos y tener datos de la entidad en el contenedor de Hola. ¿No tiene nada de lo anterior? Hola completa [inicio rápido de cinco minutos](https://aka.ms/acdbtnetqs) o hello [tutorial de programadores](https://aka.ms/acdbtabletut) toocreate una cuenta y rellenar la base de datos.

## <a name="query-on-partitionkey-and-rowkey"></a>Consultas en PartitionKey y RowKey
Dado que las propiedades PartitionKey y RowKey de hello forman la clave principal de una entidad, puede usar Hola después de la entidad de una sintaxis especial tooidentify hello: 

**Consultar**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**Resultados**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

Como alternativa, puede especificar estas propiedades como parte del programa Hola `$filter` opción, como se muestra en los pasos de la sección de Hola. Tenga en cuenta que los nombres de propiedad de clave de Hola y valores constantes distinguen mayúsculas de minúsculas. Hola PartitionKey y RowKey propiedades son de tipo String. 

## <a name="query-by-using-an-odata-filter"></a>Consultas mediante un filtro de OData
Al construir una cadena de filtro, tenga en cuenta estas reglas: 

* Usar operadores lógicos Hola definidos por la especificación de Protocolo OData toocompare un valor de propiedad tooa Hola. Tenga en cuenta que no se puede comparar un valor dinámico de tooa de propiedad. Un lado de la expresión de hello debe ser una constante. 
* nombre de la propiedad de Hello, operador y valor constante deben estar separados por espacios codificados de dirección URL. Para codificar un espacio con codificación URL se usa `%20`. 
* Todas las partes de la cadena de filtro de hello distinguen mayúsculas de minúsculas. 
* valor constante de Hello debe ser de hello como propiedad Hola para resultados válidos de hello filtro tooreturn de tipo de datos mismas. Para obtener más información acerca de los tipos de propiedad admitidos, consulte [Hola de entender el modelo de datos del servicio de tabla](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model). 

Esta es una consulta de ejemplo que muestra cómo toofilter por Hola PartitionKey y propiedades de correo electrónico mediante el uso de una OData `$filter`.

**Consultar**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

Para obtener más información sobre cómo tooconstruct filtrar expresiones para diversos tipos de datos, vea [consultar tablas y entidades](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).

**Resultados**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>Consultas con LINQ 
También puede consultar mediante el uso de LINQ, que traduce las expresiones de consulta OData correspondientes toohello. Este es un ejemplo de cómo toobuild consultas mediante Hola .NET SDK:

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello:

> [!div class="checklist"]
> * Aprender cómo tooquery mediante el uso de Hola API de tabla (vista previa) 

Ahora puede continuar toohello siguiente tutorial toolearn cómo toodistribute los datos globales.

> [!div class="nextstepaction"]
> [Distribución de datos global](tutorial-global-distribution-documentdb.md)
