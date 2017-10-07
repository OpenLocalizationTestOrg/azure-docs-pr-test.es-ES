---
title: "aaaCreate un índice de búsqueda de Azure | Microsoft Azure | Servicio de búsqueda de nube hospedada"
description: "¿Qué es un índice de Búsqueda de Azure y cómo se usa?"
services: search
documentationcenter: 
author: ashmaka
ms.assetid: a395e166-bf2e-4fca-8bfc-116a46c5f7b1
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: c01cc654ff91427c8f1569b2f5b060a0a0f044c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index"></a>Creación de un índice de Búsqueda de Azure
> [!div class="op_single_selector"]
> * [Información general](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

## <a name="what-is-an-index"></a>¿Qué es un índice?
Un *índice* es un almacenamiento persistente de *documentos* y otras construcciones usadas por el servicio Azure Search. Un documento es una sola unidad de datos habilitada para búsquedas. Por ejemplo, un minorista de comercio electrónico podría tener un documento para cada objeto que vende, una organización de noticias puede tener un documento para cada artículo, etc. Asignar estos equivalentes de base de datos conocidos de conceptos toomore: una *índice* es conceptualmente similar tooa *tabla*, y *documentos* son bastante equivalentes demasiado*filas* en una tabla.

Cuando se agreguen/cargar documentos y enviar consultas de búsqueda tooAzure búsqueda, se envía el índice específico de tooa de solicitudes en el servicio búsqueda.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Tipos de campo y atributos en un índice de Búsqueda de Azure
Tal y como define el esquema, debe especificar el nombre hello, tipo y atributos de cada campo en el índice. tipo de campo de Hello clasifica los datos de Hola que se almacenan en ese campo. Atributos se establecen en campos individuales toospecify cómo se utiliza el campo de Hola. Hello en las tablas siguientes enumerar los tipos de Hola y los atributos que puede especificar.

### <a name="field-types"></a>Tipos de campo
| Tipo | Description |
| --- | --- |
| *Edm.String* |Texto que opcionalmente se puede acortar para búsquedas de texto completo (separación de palabras, lematización, etc.). |
| *Collection(Edm.String)* |Una lista de cadenas que opcionalmente se pueden acortar para búsquedas de texto completo. No hay ningún límite superior teórico en número de Hola de elementos de una colección, pero toocollections aplica el límite superior de hello de 16 MB en el tamaño de carga. |
| *Edm.Boolean* |Contiene valores true/false. |
| *Edm.Int32* |Valores enteros de 32 bits. |
| *Edm.Int64* |Valores enteros de 64 bits. |
| *Edm.Double* |Datos numéricos de precisión doble. |
| *Edm.DateTimeOffset* |Los valores de hora representados en formato OData V4 Hola de fecha (p. ej. `yyyy-MM-ddTHH:mm:ss.fffZ` o `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`). |
| *Edm.GeographyPoint* |Un punto que representa una ubicación geográfica en el mundo Hola. |

Puede encontrar información más detallada sobre los [tipos de datos de Azure Search admitidos aquí](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types).

### <a name="field-attributes"></a>Atributos de campo
| Atributo | Description |
| --- | --- |
| *Clave* |Una cadena que proporciona el identificador único de Hola de cada documento que se utiliza para buscar documentos. Todos los índices deben tener una clave. Sólo un campo puede ser la clave de Hola y su tipo se debe establecer tooEdm.String. |
| *Retrievable* |Establece si el campo se puede devolver en un resultado de búsqueda. |
| *Filterable* |Permite Hola campo toobe utilizado en las consultas de filtro. |
| *Sortable* |Permite que una consulta los resultados de búsqueda de toosort mediante este campo. |
| *Facetable* |Permite un toobe campo utilizado en un [la navegación por facetas](search-faceted-navigation.md) estructura para el usuario autodirigido filtrado. Normalmente campos que contienen valores repetitivos que se puede usar toogroup varios documentos juntos (por ejemplo, varios documentos que se encuentran en una única marca o categoría de servicio) funcionan mejor como facetas. |
| *Searchable* |Marcas de Hola campo como buscar por texto completo. |

Puede encontrar información más detallada sobre los [atributos de índice de Azure Search aquí](https://docs.microsoft.com/rest/api/searchservice/Create-Index).

## <a name="guidance-for-defining-an-index-schema"></a>Guía para definir un esquema de índice
Al diseñar el índice, tómese su tiempo en hello planeación Fase toothink a través de cada decisión. Es importante mantener sus necesidades de negocio y experiencia de usuario de búsqueda en cuenta al diseñar el índice como cada campo debe estar asignado hello [atributos propios](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Cambiar un índice después de su implementación implica volver a generar y cargar los datos de Hola.

Si los requisitos de almacenamiento de datos cambian con el tiempo, puede aumentar o disminuir la capacidad agregando o quitando particiones. Para más información, consulte [Administración del servicio de búsqueda en Azure](search-manage.md) o [Límites de servicio](search-limits-quotas-capacity.md).

