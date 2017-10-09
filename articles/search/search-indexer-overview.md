---
title: "aaaIndexers en búsqueda de Azure | Documentos de Microsoft"
description: "Rastreo de la base de datos SQL de Azure, base de datos de Azure Cosmos o datos de búsqueda de tooextract de almacenamiento de Azure y rellenar un índice de búsqueda de Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 6a816252ec5d6032491a12651c05cb1fe77d3d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="indexers-in-azure-search"></a>Indexadores de Búsqueda de Azure
> [!div class="op_single_selector"]
>
> * [Información general](search-indexer-overview.md)
> * [Portal](search-import-data-portal.md)
> * [SQL de Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Azure Cosmos DB](search-howto-index-documentdb.md)
> * [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md)
> * [Azure Table Storage](search-howto-indexing-azure-tables.md)
>
>

Un **indizador** en búsqueda de Azure es un rastreador (crawler) que extrae datos de búsqueda y los metadatos de un origen de datos externo y rellena un índice basado en asignaciones de campo a otro entre el índice de Hola y el origen de datos. Este enfoque es a veces tooas que se hace referencia un modelo de extracción de' ' porque extrae los datos de servicio Hola sin necesidad de toowrite cualquier código que inserta el índice de tooan de datos.

Puede utilizar un indizador como Hola único medio para la recopilación de datos o usar una combinación de técnicas que incluyen el uso de Hola de un indizador para cargar solo algunos de los campos de hello en el índice.

Puede ejecutar los indexadores a petición o con una programación de actualización periódica de datos que se ejecuta con una frecuencia de incluso cada quince minutos. Actualizaciones más frecuentes requieren un modelo de inserción que actualiza simultáneamente los datos en Búsqueda de Azure y su origen de datos externo.

## <a name="approaches-for-creating-and-managing-indexers"></a>Enfoques para crear y administrar indexadores
Los indexadores disponibles con carácter general, como Azure SQL o Azure Cosmos DB, pueden crearse y administrarse mediante estos métodos:

* [Portal &gt; Asistente para la importación de datos ](search-get-started-portal.md)
* [API de REST de servicio](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a>Pasos básicos de configuración
Los indizadores pueden ofrecer características que son origen de datos de toohello único. En este sentido, algunos aspectos de la configuración de orígenes de datos o indexadores varían según el tipo de indexador. Sin embargo, todos los indizadores compartan Hola misma composición básica y los requisitos. Pasos que son comunes tooall más adelante se explican los indizadores.

### <a name="step-1-create-an-index"></a>Paso 1: Creación de un índice
Un indizador que se automatizará algunos procesos de recopilación de tareas toodata relacionados, pero crear un índice no es uno de ellos. Como requisito previo, debe tener un índice predefinido con campos que coincidan con los del origen de datos externo. Para más información sobre la estructura de un índice, consulte [Crear índice (API de REST de servicios de búsqueda de Azure)](https://msdn.microsoft.com/library/azure/dn798941.aspx).

### <a name="step-2-create-a-data-source"></a>Paso 2: Creación de un origen de datos
Un indexador extrae datos de un **origen de datos** que contiene información, por ejemplo, una cadena de conexión. Actualmente se admite los siguientes orígenes de datos de hello:

* [Base de datos SQL de Azure o SQL Server en una máquina virtual de Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Almacenamiento de blobs de Azure](search-howto-indexing-azure-blob-storage.md), tooextract texto de PDF, documentos de Office, HTML o XML que se utiliza
* [Azure Table Storage](search-howto-indexing-azure-tables.md)

Orígenes de datos se configura y se administran independientemente de los indizadores de Hola que utilizarlos, lo que significa que un origen de datos puede usarse en varios tooload indizadores de más de un índice a la vez.

### <a name="step-3create-and-schedule-hello-indexer"></a>Paso 3: crear y programar indizador Hola
definición de indizador de Hello es una construcción de especificación de índice de hello, origen de datos y una programación. Un indizador que puede hacer referencia a un origen de datos de otro servicio, siempre que ese origen de datos sea de hello misma suscripción. Para más información sobre la estructura de un indexador, consulte [Crear el indizador (API de REST de servicios de búsqueda de Azure)](https://msdn.microsoft.com/library/azure/dn946899.aspx).

## <a name="next-steps"></a>Pasos siguientes
Ahora que tiene la idea básica de hello, Hola siguiente paso es tooreview requisitos y tipo de origen de datos de tareas tooeach específico.

* [Base de datos SQL de Azure o SQL Server en una máquina virtual de Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Almacenamiento de blobs de Azure](search-howto-indexing-azure-blob-storage.md), tooextract texto de PDF, documentos de Office, HTML o XML que se utiliza
* [Azure Table Storage](search-howto-indexing-azure-tables.md)
* [Indización de blobs CSV mediante el indizador de búsqueda de Azure Blob Hola](search-howto-index-csv-blobs.md)
* [Indexación de blobs JSON con el indexador de blobs de Azure Search](search-howto-index-json-blobs.md)
