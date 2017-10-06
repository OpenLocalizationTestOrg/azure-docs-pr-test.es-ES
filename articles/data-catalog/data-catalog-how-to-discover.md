---
title: "orígenes de datos de aaaHow toodiscover en el catálogo de datos de Azure | Documentos de Microsoft"
description: "Este artículo resalta cómo toodiscover recursos de datos registrados con el catálogo de datos de Azure, incluidos la búsqueda y el filtrado y utilizando Hola visitarán resaltar las capacidades del portal del catálogo de datos de Azure de Hola."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 624834b8895dd50c8931c9d3e6f8dc217927c617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodiscover-data-sources-in-azure-data-catalog"></a>Cómo orígenes de datos de toodiscover en el catálogo de datos
## <a name="introduction"></a>Introducción
Azure Data Catalog es un servicio en la nube totalmente administrado que actúa como sistema de registro y de detección para orígenes de datos empresariales. En otras palabras, Data Catalog ayuda a los usuarios a detectar, comprender y usar orígenes de datos, así como a las organizaciones a obtener un mayor valor de sus datos. Después de un origen de datos está registrado con el catálogo de datos, sus metadatos se indizan por servicio de hello, por lo que puede buscar fácilmente datos de hello toodiscover que necesita.

## <a name="searching-and-filtering"></a>Búsqueda y filtrado
La detección en Azure Data Catalog usa dos mecanismos principales: la búsqueda y el filtrado.

La búsqueda es toobe diseñada intuitiva y eficaz. De forma predeterminada, los términos de búsqueda se comparan con cualquier propiedad de catálogo de hello, incluidas las anotaciones proporcionado por el usuario.

El filtrado está diseñado toocomplement buscar. Puede seleccionar características específicas como expertos, tipo de origen de datos, tipo de objeto y etiquetas. Puede ver solo los activos de datos coincidentes y restringir los activos de toomatching de resultados de búsqueda.

Mediante una combinación de búsqueda y filtrado, puede navegar rápidamente los orígenes de datos de Hola que se han registrado con orígenes de datos de catálogo de datos toodiscover Hola que necesita.

## <a name="search-syntax"></a>Sintaxis de búsqueda
Aunque la búsqueda de texto sin formato de hello predeterminada es sencillo e intuitivo, también puede utilizar sintaxis de búsqueda del catálogo de datos para un mayor control sobre los resultados de la búsqueda de Hola. Datos catálogo búsqueda admite Hola siguientes técnicas:

| Técnica | Uso | Ejemplo |
| --- | --- | --- |
| Búsqueda básica |Búsqueda básica que usa uno o varios términos de búsqueda. Los resultados son los activos que coincide con cualquier propiedad con uno o varios de los términos de hello especificados. |`sales data` |
| Ámbito de propiedad |Valor devuelto solo orígenes de datos donde se compara el término de búsqueda de hello con hello la propiedad especificada. |`name:finance` |
| Operadores booleanos |Se puede ampliar o reducir una búsqueda mediante operaciones booleanas. |`finance NOT corporate` |
| Agrupación con paréntesis |Utilice paréntesis toogroup partes de hello consulta tooachieve lógico de aislamiento, especialmente en combinación con los operadores booleanos. |`name:finance AND (tags:Q1 OR tags:Q2)` |
| Operadores de comparación |Use comparaciones distintas de la igualdad de propiedades que tengan tipos de datos numéricos y de fechas. |`modifiedTime > "11/05/2014"` |

Para obtener más información acerca de la búsqueda de catálogo de datos, vea hello [el catálogo de datos](https://msdn.microsoft.com/library/azure/mt267594.aspx) artículo.

## <a name="hit-highlighting"></a>Resaltado de referencias
Al ver los resultados de búsqueda, cualquiera muestran propiedades que coinciden con hello especificado términos de búsqueda (por ejemplo, nombre de recurso de datos de hello, descripción y las etiquetas) están resaltado toomake sea más fácil tooidentify ¿por qué se devolvió un recurso de datos determinado por una búsqueda determinada.

> [!NOTE]
> tooturn desactivar acierto resaltado, use hello **resaltar** portal del catálogo de datos de saludo de activación.
>
>

Al visualizar los resultados de la búsqueda, puede que no siempre sea evidente por qué se incluye un recurso de datos, incluso con el resaltado habilitado. Dado que se busca en todas las propiedades de forma predeterminada, es posible que se devuelva un recurso de datos debido a una coincidencia en una propiedad de nivel de columna. Y dado que varios usuarios pueden anotar los activos de datos registrada con sus propias etiquetas y descripciones, no todos los metadatos pueden mostrarse en la lista de Hola de resultados de la búsqueda.

En la vista de mosaico de Hola de forma predeterminada, cada icono que se muestra en los resultados de búsqueda de hello incluye un **coincide con el término de búsqueda de vista** icono, para que pueda ver rápidamente los número de Hola de coincidencias, su ubicación y toojump toothem si desea.

 ![Resaltado y coincidencias de búsqueda en el portal del catálogo de datos de Azure de Hola](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a>Resumen
Porque al registrar un origen de datos con copias de datos catálogo estructurales y descriptivos toohello servicio del catálogo del origen de los metadatos de los datos de hello, pasa a ser más fácil toodiscover hello origen de datos y comprender. Una vez que haya registrado un origen de datos, puede detectar mediante el filtrado y buscar desde el portal del catálogo de datos de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Para obtener detalles paso a paso acerca de cómo toodiscover orígenes de datos, vea [empezar a trabajar con el catálogo de datos](data-catalog-get-started.md).
