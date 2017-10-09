---
title: "¿aaaHow tooquery datos del gráfico en la base de datos de Azure Cosmos? | Microsoft Docs"
description: "Obtenga información acerca de los datos del gráfico tooquery en la base de datos de Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a>Azure Cosmos DB: Cómo Hola tooquery con API Graph (versión preliminar)?

base de datos de Azure Cosmos Hello [API Graph](graph-introduction.md) (vista previa) es compatible con [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) consultas. Este artículo proporciona ejemplos de documentos y consultas tooget que se inició. Se proporciona una referencia detallada de Gremlin en hello [compatibilidad Gremlin](gremlin-support.md) artículo.

En este artículo se trata Hola siguientes tareas: 

> [!div class="checklist"]
> * Consulta de datos con Gremlin

## <a name="prerequisites"></a>Requisitos previos

Para estos toowork consultas, debe tener una cuenta de base de datos de Azure Cosmos y tener datos de gráfico en el contenedor de Hola. ¿No tiene nada de lo anterior? Hola completa [inicio rápido de 5 minutos](create-graph-dotnet.md) o hello [tutorial de programadores](tutorial-query-graph.md) toocreate una cuenta y rellenar la base de datos. Puede ejecutar hello las siguientes consultas con hello [biblioteca de .NET de base de datos de Azure Cosmos graph](graph-sdk-dotnet.md), [consola Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), o el controlador Gremlin favoritos.

## <a name="count-vertices-in-hello-graph"></a>Recuento de vértices en el gráfico de Hola

Hola siguiente fragmento de código muestra cómo toocount Hola número de vértices en el gráfico de hello:

```
g.V().count()
```

## <a name="filters"></a>Filtros

Puede realizar filtros utilizando del Gremlin `has` y `hasLabel` los pasos y combinarlos con `and`, `or`, y `not` toobuild los filtros más complejos. Azure Cosmos DB proporciona indexación independiente del esquema de todas las propiedades de los vértices y grados para consultas rápidas:

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>Proyección

Puede proyectar ciertas propiedades de resultados de la consulta de hello mediante hello `values` paso:

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>Búsqueda de bordes y vértices relacionados

Hasta ahora, solo hemos visto operadores de consulta que funcionan en cualquier base de datos. Gráficos son rápidos y eficaces para las operaciones de recorrido cuando necesite toonavigate toorelated bordes y vértices. Encontremos a todos los amigos de Thomas. Hacer esto mediante el uso del Gremlin `outE` paso toofind Hola todos los out-bordes de Thomas, a continuación, recorrer toohello vértices respecto a los bordes del Gremlin `inV` paso:

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

realiza la siguiente consulta de Hello toofind de dos saltos todos "Amigos de amigos" de Thomas, mediante una llamada a `outE` y `inV` dos veces. 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

Puede crear consultas más complejas e implementar lógica de cruce seguro de gráfico eficaz mediante Gremlin, filtro de combinación incluido Hola de expresiones, realizar el bucle con `loop` paso y la implementación de navegación condicional mediante hello `choose` paso. Obtenga más información sobre lo que puede hacer con [Compatibilidad con Gremlin](gremlin-support.md).

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello:

> [!div class="checklist"]
> * Ha aprendido cómo tooquery mediante Graph 

Ahora puede continuar toohello siguiente tutorial toolearn cómo toodistribute los datos globales.

> [!div class="nextstepaction"]
> [Distribución de datos global](tutorial-global-distribution-documentdb.md)