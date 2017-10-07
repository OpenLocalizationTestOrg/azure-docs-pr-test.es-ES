---
title: aaaWorking con fechas en la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo toowork con las fechas en la base de datos de Azure Cosmos."
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a>Trabajo con fechas en Azure Cosmos DB
Azure Cosmos DB proporciona flexibilidad de esquema e indexación completa mediante un modelo de datos [JSON](http://www.json.org) nativo. Todos los recursos de Azure Cosmos DB, incluidas las bases de datos, las colecciones, los documentos y los procedimientos almacenados están modelados y almacenados como documentos JSON. Como requisito para ser portátil, JSON (y Azure Cosmos DB) solo admite un pequeño conjunto de tipos básicos: cadena, número, booleano, matriz, objeto y null. Sin embargo, JSON es flexible y permitir a los desarrolladores y marcos de trabajo toorepresent tipos más complejos con estas primitivas y creándolos a como objetos o matrices. 

En tipos básicos de suma toohello, muchas aplicaciones necesitan hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) escriba toorepresent fechas y las marcas de tiempo. Este artículo describe cómo los desarrolladores pueden almacenar, recuperar y consultar las fechas en la base de datos de Azure Cosmos con hello .NET SDK.

## <a name="storing-datetimes"></a>Almacenamiento de valores DateTime
De forma predeterminada, Hola [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md) serializa los valores de fecha y hora como [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) cadenas. Mayoría de las aplicaciones puede utilizar representación de cadena de saludo predeterminado de fecha y hora para hello siguientes motivos:

* Se pueden comparar cadenas y Hola relativa de ordenación de los valores de fecha y hora de Hola se conserva cuando están toostrings transformado. 
* Este enfoque no requiere ninguna personalización del código o de los atributos para la conversión de JSON.
* las fechas de Hello tal como se almacena en JSON son humanas legible.
* Este enfoque puede aprovechar el índice de Azure Cosmos DB para aumentar el rendimiento de las consultas.

Por ejemplo, Hola siguientes almacenes de fragmento de código una `Order` objeto que contiene dos propiedades de fecha y hora - `ShipDate` y `OrderDate` como un documento utilizando Hola .NET SDK:

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

Este documento se almacena en Azure Cosmos DB de la manera siguiente:

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

Como alternativa, puede almacenar fechas y horas como las marcas de hora de Unix, es decir, como un número que representa el número de Hola de segundos transcurridos desde el 1 de enero de 1970. La propiedad Timestamp (`_ts`) interna de Azure Cosmos DB sigue este enfoque. Puede usar hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) clase tooserialize fechas y horas como números. 

## <a name="indexing-datetimes-for-range-queries"></a>Indexación de valores DateTime para consultas de rango
Las consultas de rango son comunes con valores DateTime. Por ejemplo, si necesita toofind todas las órdenes creadas desde ayer, o buscar todos los pedidos enviados en hello últimos cinco minutos, deberá tooperform consultas por rango. tooexecute estas consultas de forma eficaz, debe configurar la colección para la indización de intervalo en cadenas.

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

Puede aprender más acerca de cómo tooconfigure directivas en la indización [directivas de indización de base de datos de Azure Cosmos](indexing-policies.md).

## <a name="querying-datetimes-in-linq"></a>Consulta de valores DateTimes en LINQ
Hola documentos .NET SDK automáticamente permite consultar los datos almacenados en la base de datos de Azure Cosmos mediante LINQ. Por ejemplo, hello fragmento de código siguiente muestra una consulta LINQ que ordena los filtros que se enviaron en hello últimos tres días.

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

Puede aprender más acerca consulta hello y lenguaje LINQ proveedor de SQL de Azure Cosmos DB en [consultar Cosmos DB](documentdb-sql-query.md).

En este artículo, explicamos cómo toostore, indizar y consultar las fechas y horas en la base de datos de Azure Cosmos.

## <a name="next-steps"></a>Pasos siguientes
* Descargue y ejecute hello [ejemplos en GitHub de código](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)
* Obtener más información en [Consulta de API de DocumentDB](documentdb-sql-query.md)
* Obtener más información sobre [Directivas de indexación de Azure Cosmos DB](indexing-policies.md)
