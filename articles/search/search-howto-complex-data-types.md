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
# <a name="how-toomodel-complex-data-types-in-azure-search"></a><span data-ttu-id="140ac-103">Cómo tipos de datos complejos toomodel en búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="140ac-103">How toomodel complex data types in Azure Search</span></span>
<span data-ttu-id="140ac-104">Conjuntos de datos externos utilizan toopopulate un índice de búsqueda de Azure a veces incluyen jerárquicas o anidados subestructuras a las que no se dividen perfectamente en un conjunto de filas tabular.</span><span class="sxs-lookup"><span data-stu-id="140ac-104">External datasets used toopopulate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="140ac-105">Algunos ejemplos de estas estructuras son varias ubicaciones y números de teléfono de un solo cliente, varios tamaños y colores de un único SKU, varios autores de un único libro, etc.</span><span class="sxs-lookup"><span data-stu-id="140ac-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="140ac-106">En términos de modelado, podría ver estas estructuras denominada tooas *tipos de datos complejos*, *compuestos de tipos de datos*, *tipos de datos compuestos*, o *agregado tipos de datos*, tooname un menor número.</span><span class="sxs-lookup"><span data-stu-id="140ac-106">In modeling terms, you might see these structures referred tooas *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, tooname a few.</span></span>

<span data-ttu-id="140ac-107">Tipos de datos complejos no se admiten de forma nativa en búsqueda de Azure, pero una solución probada incluye un proceso de dos pasos de reducción de la estructura de Hola y, a continuación, usar un **colección** estructura interior de tooreconstitute Hola de tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="140ac-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening hello structure and then using a **Collection** data type tooreconstitute hello interior structure.</span></span> <span data-ttu-id="140ac-108">Seguir técnica de hello descrita en este artículo permite toobe contenido Hola buscada, por facetas, filtrar y ordenar.</span><span class="sxs-lookup"><span data-stu-id="140ac-108">Following hello technique described in this article allows hello content toobe searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="140ac-109">Ejemplo de una estructura de datos complejos</span><span class="sxs-lookup"><span data-stu-id="140ac-109">Example of a complex data structure</span></span>
<span data-ttu-id="140ac-110">Por lo general, los datos de saludo en cuestión residen como un conjunto de documentos JSON o XML, o como elementos en un almacén NoSQL como base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="140ac-110">Typically, hello data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="140ac-111">Estructuralmente, desafío Hola proviene de tener varios elementos secundarios que necesitan toobe buscar y filtrar.</span><span class="sxs-lookup"><span data-stu-id="140ac-111">Structurally, hello challenge stems from having multiple child items that need toobe searched and filtered.</span></span>  <span data-ttu-id="140ac-112">Como punto de partida para ilustrar la solución de hello, tomar Hola siguiendo el documento JSON que enumera un conjunto de contactos como un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="140ac-112">As a starting point for illustrating hello workaround, take hello following JSON document that lists a set of contacts as an example:</span></span>

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

<span data-ttu-id="140ac-113">Mientras que los campos de Hola denomina 'id', 'name' y 'company' pueden asignarse fácilmente uno a uno como campos dentro de un índice de búsqueda de Azure, campo de hello 'ubicaciones' contiene una matriz de ubicaciones, tener tanto un conjunto de Id. de ubicación, así como descripciones de ubicación.</span><span class="sxs-lookup"><span data-stu-id="140ac-113">While hello fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, hello ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="140ac-114">Dado que la búsqueda de Azure no tiene un tipo de datos que es compatible con esto, debemos un toomodel de manera diferente este en búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="140ac-114">Given that Azure Search does not have a data type that supports this, we need a different way toomodel this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="140ac-115">Esta técnica se describe también por Kirk Evans en una entrada de blog [indizar documentos con búsqueda de Azure](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), que muestra una técnica denominada "sin formato Hola data", mediante el cual tendría un campo denominado `locationsID` y `locationsDescription` que son [colecciones](https://msdn.microsoft.com/library/azure/dn798938.aspx) (o una matriz de cadenas).</span><span class="sxs-lookup"><span data-stu-id="140ac-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening hello data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a><span data-ttu-id="140ac-116">Parte 1: Aplanar matriz hello en campos individuales</span><span class="sxs-lookup"><span data-stu-id="140ac-116">Part 1: Flatten hello array into individual fields</span></span>
<span data-ttu-id="140ac-117">toocreate un índice de búsqueda de Azure que dé cabida a este conjunto de datos, crear campos individuales para subestructura anidada hello: `locationsID` y `locationsDescription` con un tipo de datos de [colecciones](https://msdn.microsoft.com/library/azure/dn798938.aspx) (o una matriz de cadenas).</span><span class="sxs-lookup"><span data-stu-id="140ac-117">toocreate an Azure Search index that accommodates this dataset, create individual fields for hello nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="140ac-118">En estos campos que indiza los valores de hello '1' y '2' hello `locationsID` field para valores de hello y John Smith '3' & '4' en hello `locationsID` field para Jen Campbell.</span><span class="sxs-lookup"><span data-stu-id="140ac-118">In these fields you would index hello values ‘1’ and ‘2’ into hello `locationsID` field for John Smith and hello values ‘3’ & ‘4’ into hello `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="140ac-119">Los datos en Azure Search tendrían el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="140ac-119">Your data within Azure Search would look like this:</span></span> 

![datos de ejemplo, 2 filas](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a><span data-ttu-id="140ac-121">Parte 2: Agregar un campo de la colección en la definición del índice Hola</span><span class="sxs-lookup"><span data-stu-id="140ac-121">Part 2: Add a collection field in hello index definition</span></span>
<span data-ttu-id="140ac-122">En el esquema de índice de hello, definiciones de campo de hello podrían ser ejemplo toothis similar.</span><span class="sxs-lookup"><span data-stu-id="140ac-122">In hello index schema, hello field definitions might look similar toothis example.</span></span>

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

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a><span data-ttu-id="140ac-123">Validar los comportamientos de búsqueda y, opcionalmente, extender índice Hola</span><span class="sxs-lookup"><span data-stu-id="140ac-123">Validate search behaviors and optionally extend hello index</span></span>
<span data-ttu-id="140ac-124">Suponiendo el índice de hello creado y datos Hola cargado, ahora puede probar ejecución de consultas de búsqueda en tooverify de solución de hello en Hola conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="140ac-124">Assuming you created hello index and loaded hello data, you can now test hello solution tooverify search query execution against hello dataset.</span></span> <span data-ttu-id="140ac-125">Cada campo **collection** debería tener las propiedades **searchable**, **filterable** y **facetable**.</span><span class="sxs-lookup"><span data-stu-id="140ac-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="140ac-126">Debe ser capaz de toorun consultas como:</span><span class="sxs-lookup"><span data-stu-id="140ac-126">You should be able toorun queries like:</span></span>

* <span data-ttu-id="140ac-127">Buscar todas las personas que trabajan en hello "Adventureworks" oficina central".</span><span class="sxs-lookup"><span data-stu-id="140ac-127">Find all people who work at hello ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="140ac-128">Obtener un recuento del número de Hola de personas que trabajan en una oficina.</span><span class="sxs-lookup"><span data-stu-id="140ac-128">Get a count of hello number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="140ac-129">De personas de Hola que trabajan en una oficina, muestran qué otras oficinas funcionan junto con un número de personas de hello en cada ubicación.</span><span class="sxs-lookup"><span data-stu-id="140ac-129">Of hello people who work at a ‘Home Office’, show what other offices they work along with a count of hello people in each location.</span></span>  

<span data-ttu-id="140ac-130">Donde se encuentra esta técnica alejados es cuando se necesita una búsqueda que combina el Id. de ubicación de hello así como descripción de la ubicación de hello toodo.</span><span class="sxs-lookup"><span data-stu-id="140ac-130">Where this technique falls apart is when you need toodo a search that combines both hello location id as well as hello location description.</span></span> <span data-ttu-id="140ac-131">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="140ac-131">For example:</span></span>

* <span data-ttu-id="140ac-132">Buscar todas las personas cuya ubicación es Home Office y su identificador de ubicación es 4.</span><span class="sxs-lookup"><span data-stu-id="140ac-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="140ac-133">Si recuerda el contenido original de hello tenía el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="140ac-133">If you recall hello original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="140ac-134">Sin embargo, ahora que hemos separado datos hello en campos independientes, tenemos ninguna manera de saber si Hola oficina doméstica para Jen Campbell relaciona demasiado`locationsID 3` o `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="140ac-134">However, now that we have separated hello data into separate fields, we have no way of knowing if hello Home Office for Jen Campbell relates too`locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="140ac-135">toohandle este caso, definir otro campo en el índice de Hola que combina todos los datos de hello en una sola colección.</span><span class="sxs-lookup"><span data-stu-id="140ac-135">toohandle this case, define another field in hello index that combines all of hello data into a single collection.</span></span>  <span data-ttu-id="140ac-136">En nuestro ejemplo, llamaremos a este campo `locationsCombined` y se separarán contenido Hola con un `||` aunque puede elegir cualquier separador que cree que sería un conjunto único de caracteres para su contenido.</span><span class="sxs-lookup"><span data-stu-id="140ac-136">For our example, we will call this field `locationsCombined` and we will separate hello content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="140ac-137">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="140ac-137">For example:</span></span> 

![datos de ejemplo, 2 filas con separador](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="140ac-139">Con este campo `locationsCombined` , ahora podemos dar cabida a más consultas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="140ac-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="140ac-140">Mostrar el número de personas que trabajan en la ubicación 'Home Office' con un identificador de ubicación '4'.</span><span class="sxs-lookup"><span data-stu-id="140ac-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="140ac-141">Buscar las personas que trabajan en la ubicación 'Home Office' con un identificador de ubicación '4'.</span><span class="sxs-lookup"><span data-stu-id="140ac-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="140ac-142">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="140ac-142">Limitations</span></span>
<span data-ttu-id="140ac-143">Esta técnica es útil para diversos escenarios, pero no es aplicable en todos los casos.</span><span class="sxs-lookup"><span data-stu-id="140ac-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="140ac-144">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="140ac-144">For example:</span></span>

1. <span data-ttu-id="140ac-145">Si no tiene un conjunto estático de campos en el tipo de datos complejos y no había ninguna manera toomap todos los posibles Hola tipos tooa único campo.</span><span class="sxs-lookup"><span data-stu-id="140ac-145">If you do not have a static set of fields in your complex data type and there was no way toomap all hello possible types tooa single field.</span></span> 
2. <span data-ttu-id="140ac-146">Actualizar objetos de hello anidada requiere algunos toodetermine trabajo adicional exactamente lo que debe toobe actualizado en el índice de búsqueda de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="140ac-146">Updating hello nested objects requires some extra work toodetermine exactly what needs toobe updated in hello Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="140ac-147">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="140ac-147">Sample code</span></span>
<span data-ttu-id="140ac-148">Puede ver un ejemplo sobre cómo tooindex un datos JSON complejos definidos en búsqueda de Azure y realizar un número de consultas sobre este conjunto de datos en este [repositorio de GitHub](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="140ac-148">You can see an example on how tooindex a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="140ac-149">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="140ac-149">Next step</span></span>
<span data-ttu-id="140ac-150">[Voto de compatibilidad nativa con tipos de datos complejos](https://feedback.azure.com/forums/263029-azure-search) en hello UserVoice de búsqueda de Azure página y proporcionar cualquier entrada adicional que quiere que nos tooconsider con respecto a la implementación de características.</span><span class="sxs-lookup"><span data-stu-id="140ac-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on hello Azure Search UserVoice page and provide any additional input that you’d like us tooconsider regarding feature implementation.</span></span> <span data-ttu-id="140ac-151">Puede ponerse en contacto con toome directamente en Twitter en @liamca.</span><span class="sxs-lookup"><span data-stu-id="140ac-151">You can also reach out toome directly on Twitter at @liamca.</span></span>

