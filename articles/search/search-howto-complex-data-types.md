---
title: "tipos de datos complejos de aaaHow toomodel en búsqueda de Azure | Documentos de Microsoft"
description: "Las estructuras de datos jerárquicas o anidadas se pueden modelar en un índice de Azure Search mediante conjuntos de filas aplanados y el tipo de datos Collections."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a>Cómo tipos de datos complejos toomodel en búsqueda de Azure
Conjuntos de datos externos utilizan toopopulate un índice de búsqueda de Azure a veces incluyen jerárquicas o anidados subestructuras a las que no se dividen perfectamente en un conjunto de filas tabular. Algunos ejemplos de estas estructuras son varias ubicaciones y números de teléfono de un solo cliente, varios tamaños y colores de un único SKU, varios autores de un único libro, etc. En términos de modelado, podría ver estas estructuras denominada tooas *tipos de datos complejos*, *compuestos de tipos de datos*, *tipos de datos compuestos*, o *agregado tipos de datos*, tooname un menor número.

Tipos de datos complejos no se admiten de forma nativa en búsqueda de Azure, pero una solución probada incluye un proceso de dos pasos de reducción de la estructura de Hola y, a continuación, usar un **colección** estructura interior de tooreconstitute Hola de tipo de datos. Seguir técnica de hello descrita en este artículo permite toobe contenido Hola buscada, por facetas, filtrar y ordenar.

## <a name="example-of-a-complex-data-structure"></a>Ejemplo de una estructura de datos complejos
Por lo general, los datos de saludo en cuestión residen como un conjunto de documentos JSON o XML, o como elementos en un almacén NoSQL como base de datos de Azure Cosmos. Estructuralmente, desafío Hola proviene de tener varios elementos secundarios que necesitan toobe buscar y filtrar.  Como punto de partida para ilustrar la solución de hello, tomar Hola siguiendo el documento JSON que enumera un conjunto de contactos como un ejemplo:

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

Mientras que los campos de Hola denomina 'id', 'name' y 'company' pueden asignarse fácilmente uno a uno como campos dentro de un índice de búsqueda de Azure, campo de hello 'ubicaciones' contiene una matriz de ubicaciones, tener tanto un conjunto de Id. de ubicación, así como descripciones de ubicación. Dado que la búsqueda de Azure no tiene un tipo de datos que es compatible con esto, debemos un toomodel de manera diferente este en búsqueda de Azure. 

> [!NOTE]
> Esta técnica se describe también por Kirk Evans en una entrada de blog [indizar documentos con búsqueda de Azure](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), que muestra una técnica denominada "sin formato Hola data", mediante el cual tendría un campo denominado `locationsID` y `locationsDescription` que son [colecciones](https://msdn.microsoft.com/library/azure/dn798938.aspx) (o una matriz de cadenas).   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a>Parte 1: Aplanar matriz hello en campos individuales
toocreate un índice de búsqueda de Azure que dé cabida a este conjunto de datos, crear campos individuales para subestructura anidada hello: `locationsID` y `locationsDescription` con un tipo de datos de [colecciones](https://msdn.microsoft.com/library/azure/dn798938.aspx) (o una matriz de cadenas). En estos campos que indiza los valores de hello '1' y '2' hello `locationsID` field para valores de hello y John Smith '3' & '4' en hello `locationsID` field para Jen Campbell.  

Los datos en Azure Search tendrían el siguiente aspecto: 

![datos de ejemplo, 2 filas](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a>Parte 2: Agregar un campo de la colección en la definición del índice Hola
En el esquema de índice de hello, definiciones de campo de hello podrían ser ejemplo toothis similar.

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a>Validar los comportamientos de búsqueda y, opcionalmente, extender índice Hola
Suponiendo el índice de hello creado y datos Hola cargado, ahora puede probar ejecución de consultas de búsqueda en tooverify de solución de hello en Hola conjunto de datos. Cada campo **collection** debería tener las propiedades **searchable**, **filterable** y **facetable**. Debe ser capaz de toorun consultas como:

* Buscar todas las personas que trabajan en hello "Adventureworks" oficina central".
* Obtener un recuento del número de Hola de personas que trabajan en una oficina.  
* De personas de Hola que trabajan en una oficina, muestran qué otras oficinas funcionan junto con un número de personas de hello en cada ubicación.  

Donde se encuentra esta técnica alejados es cuando se necesita una búsqueda que combina el Id. de ubicación de hello así como descripción de la ubicación de hello toodo. Por ejemplo:

* Buscar todas las personas cuya ubicación es Home Office y su identificador de ubicación es 4.  

Si recuerda el contenido original de hello tenía el siguiente aspecto:

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

Sin embargo, ahora que hemos separado datos hello en campos independientes, tenemos ninguna manera de saber si Hola oficina doméstica para Jen Campbell relaciona demasiado`locationsID 3` o `locationsID 4`.  

toohandle este caso, definir otro campo en el índice de Hola que combina todos los datos de hello en una sola colección.  En nuestro ejemplo, llamaremos a este campo `locationsCombined` y se separarán contenido Hola con un `||` aunque puede elegir cualquier separador que cree que sería un conjunto único de caracteres para su contenido. Por ejemplo: 

![datos de ejemplo, 2 filas con separador](./media/search-howto-complex-data-types/sample-data-2.png)

Con este campo `locationsCombined` , ahora podemos dar cabida a más consultas, por ejemplo:

* Mostrar el número de personas que trabajan en la ubicación 'Home Office' con un identificador de ubicación '4'.  
* Buscar las personas que trabajan en la ubicación 'Home Office' con un identificador de ubicación '4'. 

## <a name="limitations"></a>Limitaciones
Esta técnica es útil para diversos escenarios, pero no es aplicable en todos los casos.  Por ejemplo:

1. Si no tiene un conjunto estático de campos en el tipo de datos complejos y no había ninguna manera toomap todos los posibles Hola tipos tooa único campo. 
2. Actualizar objetos de hello anidada requiere algunos toodetermine trabajo adicional exactamente lo que debe toobe actualizado en el índice de búsqueda de Azure Hola

## <a name="sample-code"></a>Código de ejemplo
Puede ver un ejemplo sobre cómo tooindex un datos JSON complejos definidos en búsqueda de Azure y realizar un número de consultas sobre este conjunto de datos en este [repositorio de GitHub](https://github.com/liamca/AzureSearchComplexTypes).

## <a name="next-step"></a>Paso siguiente
[Voto de compatibilidad nativa con tipos de datos complejos](https://feedback.azure.com/forums/263029-azure-search) en hello UserVoice de búsqueda de Azure página y proporcionar cualquier entrada adicional que quiere que nos tooconsider con respecto a la implementación de características. Puede ponerse en contacto con toome directamente en Twitter en @liamca.

