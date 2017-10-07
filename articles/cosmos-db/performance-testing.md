---
title: aaaAzure Cosmos DB escala y pruebas de rendimiento | Documentos de Microsoft
description: "Obtenga información acerca de cómo escalar tooperform y pruebas de rendimiento con base de datos de Azure Cosmos"
keywords: pruebas de rendimiento
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Pruebas de escala y rendimiento con Azure Cosmos DB
Las pruebas de escala y rendimiento representan un paso clave en el desarrollo de aplicaciones. Para muchas aplicaciones, el nivel de base de datos de hello tiene un impacto significativo en Hola el rendimiento general y la escalabilidad, y es, por tanto, un componente esencial del rendimiento de las pruebas. [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) está diseñado específicamente para el escalado flexible y un rendimiento predecible y, por lo tanto, supone una elección excelente para aplicaciones que necesitan un nivel de base de datos de alto rendimiento. 

Este artículo es una referencia para los desarrolladores que implementan conjuntos de pruebas de rendimiento para sus cargas de trabajo de Cosmos DB o evalúan Cosmos DB para escenarios de aplicaciones de alto rendimiento. Se centra principalmente en las pruebas de rendimiento aislado de base de datos de hello, pero también incluye prácticas recomendadas para las aplicaciones de producción.

Después de leer este artículo, será hello tooanswer pueda siguientes preguntas:   

* ¿Dónde puedo encontrar una aplicación cliente de .NET de ejemplo para pruebas de rendimiento de Azure Cosmos DB? 
* ¿Cómo se pueden alcanzar niveles de alto rendimiento con Cosmos DB desde mi aplicación cliente?

tooget a trabajar con código, descargue proyecto Hola de [ejemplo de pruebas de rendimiento de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark). 

> [!NOTE]
> objetivo de Hola de esta aplicación es toodemonstrate prácticas recomendadas para extraer un mejor rendimiento de la base de datos de Cosmos con un número reducido de equipos cliente. Esto no realizó la capacidad de toodemonstrate Hola máxima del servicio de hello, que puede escalar limitlessly.
> 
> 

Si está buscando tooimprove de opciones de configuración de cliente DB Cosmos rendimiento, consulte [sugerencias de rendimiento de base de datos de Azure Cosmos](performance-tips.md).

## <a name="run-hello-performance-testing-application"></a>Ejecutar la aplicación de prueba de rendimiento de Hola
Hola tooget de manera más rápida iniciado es toocompile y ejemplo de Hola ejecución .NET a continuación, como se describe en estos pasos Hola. También puede revisar el código fuente de hello e implementar aplicaciones de cliente propio de tooyour configuraciones similares.

**Paso 1:** proyecto Hola de descarga de [ejemplo de pruebas de rendimiento de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), o en el repositorio de GitHub de Hola de bifurcación.

**Paso 2:** modificar la configuración de Hola de EndpointUrl, AuthorizationKey, CollectionThroughput y DocumentTemplate (opcional) en un archivo App.config.

> [!NOTE]
> Antes de aprovisionar colecciones con un alto rendimiento, consulte toohello [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/) los costos de hello tooestimate por colección. Base de datos de Azure Cosmos facturas almacenamiento y rendimiento de forma independiente en concreto cada hora, por lo que puede ahorrar costos al eliminar o reducir el rendimiento de las colecciones de base de datos de Azure Cosmos Hola después de realizar pruebas.
> 
> 

**Paso 3:** compilar y ejecutar la aplicación de consola de hello desde línea de comandos de Hola. Obtendrá unos resultados similares a Hola siguientes:

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


**Paso 4 (si es necesario):** Hola rendimiento notificado (RU/s) de la herramienta de hello debe ser Hola igual o mayor que el rendimiento aprovisionado Hola de colección de Hola. De lo contrario, creciente hello DegreeOfParallelism en incrementos pequeños puede ayudarle a alcanzar el límite de Hola. Si meseta de rendimiento de Hola desde la aplicación cliente, iniciar varias instancias de la aplicación hello en Hola iguales o distintos equipos le ayudará a alcanzar el límite de hello aprovisionado en hello instancias diferentes. Si necesita ayuda con este paso, escriba un correo electrónico tooaskcosmosdb@microsoft.com o presentar una incidencia de soporte técnico de hello [Portal de Azure](https://portal.azure.com).

Una vez que tenga la aplicación hello ejecutando, puede probar diferentes [directivas de indexación](indexing-policies.md) y [niveles de coherencia](consistency-levels.md) toounderstand su impacto sobre el rendimiento y la latencia. También puede revisar el código fuente de hello e implementar las aplicaciones de producción o de conjuntos de pruebas propias de tooyour de configuraciones similares.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, vimos cómo puede realizar pruebas de rendimiento y escala con Cosmos DB usando una aplicación de consola .NET. Consulte toohello vínculos siguientes para obtener información adicional sobre cómo trabajar con la base de datos de Azure Cosmos.

* [Ejemplo de pruebas de rendimiento de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [Tooimprove de opciones de configuración de cliente rendimiento de base de datos de Azure Cosmos](performance-tips.md)
* [Creación de particiones en el servidor en Azure Cosmos DB](partition-data.md)


