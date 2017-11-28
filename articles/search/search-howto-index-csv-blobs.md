---
title: "aaaIndexing CSV blobs con el indizador de búsqueda de Azure blob | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooindex CSV blobs con búsqueda de Azure"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: ed3c9cff-1946-4af2-a05a-5e0b3d61eb25
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 12/15/2016
ms.author: eugenesh
ms.openlocfilehash: f2b1ce824e62c5b3f6155c6e88887897cf1a8eae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a>Indexación de blobs CSV con el indexador de blobs de Búsqueda de Azure
De forma predeterminada, el [indexador de blobs de Búsqueda de Azure](search-howto-indexing-azure-blob-storage.md) analiza los blobs de texto delimitados como un único fragmento de texto. Sin embargo, con los blobs que contiene datos CSV, a menudo desea tootreat cada línea en el blob de hello como documentos independientes. Por ejemplo, dada Hola siguiente texto delimitado por: 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

es recomendable tooparse en 2 documentos, cada una que contiene "id" y "datePublished", "tags" campos.

En este artículo, aprenderá cómo tooparse CSV blobs con un indizador de búsqueda de Azure blob. 

> [!IMPORTANT]
> Actualmente, la versión de esta funcionalidad es una versión preliminar. Está disponible únicamente en la API de REST de hello mediante versión **vista previa 2015-02-28**. Por favor, recuerde que las versiones preliminares de las API están pensadas para realizar pruebas y evaluar, y no deben usarse en entornos de producción. 
> 
> 

## <a name="setting-up-csv-indexing"></a>Configuración de la indexación de CSV
los blobs CSV tooindex, crear o actualizar una definición de indizador con hello `delimitedText` modo de análisis:  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

Para obtener más detalles sobre Hola crear API de indizador, visite [crear indizador](search-api-indexers-2015-02-28-preview.md#create-indexer).

`firstLineContainsHeaders`indica que la primera línea de (no están en blanco) Hola de cada blob contiene encabezados.
Si blobs no contienen una línea de encabezado inicial, encabezados de hello deben especificarse en la configuración de indizador de hello: 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

Actualmente, la codificación UTF-8 de hello solo se admite. Además, solo Hola coma `','` se admite el carácter como delimitador de Hola. Si necesita compatibilidad con otras codificaciones o delimitadores, háganoslo saber en [nuestro sitio web de UserVoice](https://feedback.azure.com/forums/263029-azure-search).

> [!IMPORTANT]
> Cuando se utiliza texto hello delimitada análisis modo, búsqueda de Azure, se da por supuesto que todos los blobs en el origen de datos será CSV. Si necesita toosupport una combinación de CSV y no CSV blobs de hello mismo origen de datos, por favor, hacernos saber en [nuestro sitio UserVoice](https://feedback.azure.com/forums/263029-azure-search).
> 
> 

## <a name="request-examples"></a>Ejemplos de solicitud
Al reunir estos todos juntos, estos son ejemplos de carga completa de Hola. 

Origen de datos: 

    POST https://[service name].search.windows.net/datasources?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

Indexador:

    POST https://[service name].search.windows.net/indexers?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a>Ayúdenos a mejorar Búsqueda de Azure
Si dispone de las solicitudes de características o ideas para mejoras, póngase en contacto toous en nuestra [sitio UserVoice](https://feedback.azure.com/forums/263029-azure-search/).

