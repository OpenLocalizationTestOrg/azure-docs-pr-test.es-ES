---
title: "aaa \"consultar un índice (portal - búsqueda de Azure) | Documentos de Microsoft\""
description: "Emitir una consulta de búsqueda en el Explorador de búsqueda del Portal de Azure Hola."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a>Consultar un índice de búsqueda de Azure mediante el Explorador de búsqueda en hello Portal de Azure
> [!div class="op_single_selector"]
> * [Información general](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Este artículo muestra cómo tooquery una búsqueda de Azure INDICE mediante **buscar en el explorador** Hola portal de Azure. Puede usar Buscar en el explorador toosubmit simple o completo Lucene consulta cadenas tooany índice existente en el servicio.

## <a name="open-hello-service-dashboard"></a>Panel de servicio de hello abierto
1. Haga clic en **todos los recursos** en la barra de salto de hello en la parte izquierda de Hola de hello [portal de Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).
2. Seleccione el servicio Azure Search.

## <a name="select-an-index"></a>Seleccionar un índice

Índice de hello seleccione le gustaría toosearch de hello **índices** icono.

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>Abrir el Explorador de búsqueda

Haga clic en hello barra de búsqueda de búsqueda del explorador mosaico tooslide Hola abierto y panel de resultados.

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>Inicio de la búsqueda

Al utilizar Hola buscar en el explorador, se puede especificar [parámetros de consulta](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) consulta de hello tooformulate.

1. En **Cadena de consulta**, escriba una consulta y pulse **Buscar**. 

   cadena de consulta de Hola se analiza automáticamente en la solicitud correcta de hello URL toosubmit una solicitud HTTP en hello API de REST de búsqueda de Azure.   
   
   Puede usar cualquier válido simple o completo Lucene sintaxis toocreate Hola solicitud de consulta. Hola `*` carácter es búsqueda vacía o sin especificar tooan equivalente que devuelve todos los documentos sin ningún orden determinado.

2. En **resultados**, resultados de la consulta se presentan en JSON sin formato, carga toohello idénticos que se devuelve en un cuerpo de respuesta HTTP al emitir solicitudes mediante programación.

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>Pasos siguientes

Hola recursos siguientes proporciona ejemplos y la información de la sintaxis de consulta adicionales.

 + [Sintaxis de consulta simplificada](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Sintaxis de consulta de Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Ejemplos de sintaxis de consulta de Lucene para la creación de consultas en Azure Search](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [OData Expression Syntax for Azure Search](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) (Sintaxis de expresiones de OData en Azure Search) 