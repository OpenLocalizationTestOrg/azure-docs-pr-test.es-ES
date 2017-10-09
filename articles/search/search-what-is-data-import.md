---
title: "carga aaaData en búsqueda de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooupload tooan de datos de índice de búsqueda de Azure."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a>Cargar datos tooAzure búsqueda
> [!div class="op_single_selector"]
> * [Información general](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Hay dos toopopulate de formas de un índice con los datos. primera opción de Hello es insertar manualmente los datos en índice de hello mediante Hola búsqueda de Azure [API de REST](search-import-data-rest-api.md) o [.NET SDK](search-import-data-dotnet.md). segunda opción de Hello es demasiado[seleccione un origen de datos admitidos](search-indexer-overview.md) tooyour indizar y permiten la búsqueda de Azure incorporar automáticamente los cambios de datos de Hola.

## <a name="push-data-tooan-index"></a>Índice de tooan de inserción de datos
Este enfoque refiere tooprogrammatically enviar su toomake de búsqueda de tooAzure de datos estén disponibles para las búsquedas. Para las aplicaciones con requisitos de una latencia muy baja (por ejemplo, si necesita buscar toobe operaciones sincronizada con las bases de datos de inventario dinámico), modelo de inserción de hello es la única opción.

Puede usar hello [API de REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) o [.NET SDK](search-import-data-dotnet.md) toopush índice de tooan de datos. Actualmente no hay ninguna compatibilidad de herramienta de inserción de datos mediante el portal de Hola.

Este enfoque es más flexible que el modelo de extracción de hello porque puede cargar documentos individualmente o en lotes (seguridad too1000 por lote o 16 MB, el límite ocurra primero). modelo de inserción de Hello también le permite tooupload documentos tooAzure búsqueda sin tener en cuenta que los datos son.

formato de datos de Hello reconocido por búsqueda de Azure es JSON, y todos los documentos en el conjunto de datos de hello deben tener campos que se asignan toofields definidos en el esquema de índice. 

## <a name="pull-data-into-an-index"></a>Extracción de datos e introducción en un índice
modelo de extracción de Hello rastrea un origen de datos admitidos y carga automáticamente los datos de hello en el índice. En Azure Search, esta funcionalidad se implementa mediante *indexadores*, que actualmente están disponibles para [Blob Storage](search-howto-indexing-azure-blob-storage.md), [Table Storage](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer), [Azure SQL Database y SQL Server en máquinas virtuales de Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 

Los indizadores conectan con un origen de datos de índice tooa (normalmente una tabla, vista o estructura equivalente) y asignan los campos de tooequivalent de campos de origen de índice de Hola. Durante la ejecución, el conjunto de filas de Hola se tooJSON transformado automáticamente y se carga en el índice especificado de Hola. Todos los indizadores admiten programación para que se puede especificar la frecuencia con datos de hello toobe actualizado. La mayoría de los indizadores proporcionan si el origen de datos de hello es compatible con el seguimiento de cambios. Seguimiento de cambios y eliminaciones tooexisting documentos además toorecognizing nuevos documentos, los indizadores eliminan la necesidad de hello tooactively administrar datos de hello en el índice. 

Funcionalidad de indizador se expone en hello [portal de Azure](search-import-data-portal.md), hello [API de REST](/rest/api/searchservice/Indexer-operations), hello y [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations). 

Un portal de hello toousing ventaja es que búsqueda de Azure normalmente va a generar un esquema de índice predeterminado leyendo Hola metadatos del conjunto de datos de origen de Hola. Puede modificar el índice generado Hola hasta que se procesa el índice de hello, después de que Hola se permiten modificaciones de esquema solo son aquellos que no requieren volver a indizar. Si los cambios de Hola que desee toomake impacto hello esquema directamente, necesitaría índice de hello toorebuild. 

Después de que se rellena el índice de hello, puede usar **buscar en el explorador** en la barra de comandos de portal de Hola como un paso de verificación.

## <a name="query-an-index-using-search-explorer"></a>Realización de consultas en un índice mediante el Explorador de búsqueda

Un tooperform de forma rápida una comprobación preliminar de carga de un documento hello es toouse **buscar en el explorador** en el portal de Hola. el Explorador de Hello permite consultar un índice sin necesidad de toowrite cualquier código. Hello experiencia de búsqueda se basa valores predeterminados, como hello [sintaxis simple](/rest/api/searchservice/simple-query-syntax-in-azure-search) y default [searchMode parámetro de consulta](/rest/api/searchservice/search-documents). Resultados se devuelven en JSON que puede inspeccionar todo el documento Hola.

> [!TIP]
> Numerosos [ejemplos de código de búsqueda de Azure](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) incluir conjuntos de datos incrustado o estén disponibles, inicia un tooget de manera sencilla de la oferta. portal de Hello también proporciona un indizador de ejemplo y un origen de datos que consta de un conjunto de datos pequeño inmobiliaria (denominada "realestate-us-sample"). Al ejecutar indizador preconfigurada de hello en el origen de datos de ejemplo de Hola, se crea un índice y se cargan con documentos que, a continuación, se pueden consultar en el Explorador de búsqueda o el código que se escribe.
