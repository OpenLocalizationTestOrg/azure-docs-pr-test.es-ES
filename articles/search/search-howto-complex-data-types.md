---
title: Modelado de tipos de datos complejos en Azure Search | Microsoft Docs
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
ms.openlocfilehash: d576fd7bb267ae7a100589413185b595e3b2be42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-model-complex-data-types-in-azure-search"></a><span data-ttu-id="77987-103">Modelado de tipos de datos complejos en Azure Search</span><span class="sxs-lookup"><span data-stu-id="77987-103">How to model complex data types in Azure Search</span></span>
<span data-ttu-id="77987-104">Los conjuntos de datos externos usados para rellenar un índice de Azure Search a veces incluyen subestructuras jerárquicas o anidadas que no se dividen perfectamente en un conjunto de filas tabular.</span><span class="sxs-lookup"><span data-stu-id="77987-104">External datasets used to populate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="77987-105">Algunos ejemplos de estas estructuras son varias ubicaciones y números de teléfono de un solo cliente, varios tamaños y colores de un único SKU, varios autores de un único libro, etc.</span><span class="sxs-lookup"><span data-stu-id="77987-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="77987-106">En términos de modelado, puede que vea referirse a estas estructuras como *tipos de datos complejos*, *tipos de datos compuestos* o *tipos de datos agregados*, por nombrar algunos. **</span><span class="sxs-lookup"><span data-stu-id="77987-106">In modeling terms, you might see these structures referred to as *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, to name a few.</span></span>

<span data-ttu-id="77987-107">Los tipos de datos complejos no se admiten de forma nativa en Azure Search, pero existe una solución probada que consiste en seguir un proceso en dos pasos para aplanar la estructura y, a continuación, utilizar un tipo de datos **Collection** para reconstituir la estructura interior.</span><span class="sxs-lookup"><span data-stu-id="77987-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening the structure and then using a **Collection** data type to reconstitute the interior structure.</span></span> <span data-ttu-id="77987-108">La técnica descrita en este artículo permite buscar, buscar con facetas, filtrar y ordenar el contenido.</span><span class="sxs-lookup"><span data-stu-id="77987-108">Following the technique described in this article allows the content to be searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="77987-109">Ejemplo de una estructura de datos complejos</span><span class="sxs-lookup"><span data-stu-id="77987-109">Example of a complex data structure</span></span>
<span data-ttu-id="77987-110">Normalmente, los datos en cuestión residen como un conjunto de documentos JSON o XML o como elementos en un almacén de NoSQL, por ejemplo, Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="77987-110">Typically, the data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="77987-111">Estructuralmente, la dificultad radica en tener varios elementos secundarios que se deben buscar y filtrar.</span><span class="sxs-lookup"><span data-stu-id="77987-111">Structurally, the challenge stems from having multiple child items that need to be searched and filtered.</span></span>  <span data-ttu-id="77987-112">Como punto de partida para ilustrar la solución alternativa, tome como ejemplo el siguiente documento JSON que enumera un conjunto de contactos:</span><span class="sxs-lookup"><span data-stu-id="77987-112">As a starting point for illustrating the workaround, take the following JSON document that lists a set of contacts as an example:</span></span>

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

<span data-ttu-id="77987-113">Mientras que los campos 'id', 'name' y 'company' se pueden asignar fácilmente uno a uno como campos en un índice de Azure Search, el campo 'locations' contiene una matriz de ubicaciones, con un conjunto de identificadores de ubicación así como descripciones de ubicación.</span><span class="sxs-lookup"><span data-stu-id="77987-113">While the fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, the ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="77987-114">Como Azure Search no tiene un tipo de datos que admita esto, necesitamos una manera diferente de modelarlo Azure Search.</span><span class="sxs-lookup"><span data-stu-id="77987-114">Given that Azure Search does not have a data type that supports this, we need a different way to model this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="77987-115">En su entrada de blog [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/) (Indexación de DocumentDB con Azure Search), Kirk Evans muestra una técnica llamada "aplanamiento de los datos", según la cual tendría dos campos llamados `locationsID` y `locationsDescription`, ambos [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (o una matriz de cadenas).</span><span class="sxs-lookup"><span data-stu-id="77987-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening the data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-the-array-into-individual-fields"></a><span data-ttu-id="77987-116">Parte 1: Aplanar la matriz en campos individuales</span><span class="sxs-lookup"><span data-stu-id="77987-116">Part 1: Flatten the array into individual fields</span></span>
<span data-ttu-id="77987-117">Para crear un índice de Azure Search que dé cabida a este conjunto de datos, cree campos individuales para la subestructura anidada: `locationsID` y `locationsDescription` con un tipo de datos [collection](https://msdn.microsoft.com/library/azure/dn798938.aspx) (o una matriz de cadenas).</span><span class="sxs-lookup"><span data-stu-id="77987-117">To create an Azure Search index that accommodates this dataset, create individual fields for the nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="77987-118">En estos campos, los valores '1' y '2' se indizan en el campo `locationsID` para John Smith y los valores '3' y '4' en el campo `locationsID` para Jen Campbell.</span><span class="sxs-lookup"><span data-stu-id="77987-118">In these fields you would index the values ‘1’ and ‘2’ into the `locationsID` field for John Smith and the values ‘3’ & ‘4’ into the `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="77987-119">Los datos en Azure Search tendrían el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="77987-119">Your data within Azure Search would look like this:</span></span> 

![datos de ejemplo, 2 filas](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-the-index-definition"></a><span data-ttu-id="77987-121">Parte 2: Agregar un campo de colección en la definición del índice</span><span class="sxs-lookup"><span data-stu-id="77987-121">Part 2: Add a collection field in the index definition</span></span>
<span data-ttu-id="77987-122">En el esquema de índice, las definiciones de campo podrían ser similares a las de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="77987-122">In the index schema, the field definitions might look similar to this example.</span></span>

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

## <a name="validate-search-behaviors-and-optionally-extend-the-index"></a><span data-ttu-id="77987-123">Validación de los comportamientos de búsqueda y extensión opcional del índice</span><span class="sxs-lookup"><span data-stu-id="77987-123">Validate search behaviors and optionally extend the index</span></span>
<span data-ttu-id="77987-124">Suponiendo que ha creado el índice y cargado los datos, ahora puede probar la solución para comprobar la ejecución de la consulta de búsqueda en el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="77987-124">Assuming you created the index and loaded the data, you can now test the solution to verify search query execution against the dataset.</span></span> <span data-ttu-id="77987-125">Cada campo **collection** debería tener las propiedades **searchable**, **filterable** y **facetable**.</span><span class="sxs-lookup"><span data-stu-id="77987-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="77987-126">Debe poder ejecutar consultas como estas:</span><span class="sxs-lookup"><span data-stu-id="77987-126">You should be able to run queries like:</span></span>

* <span data-ttu-id="77987-127">Buscar todas las personas que trabajan en ‘Adventureworks Headquarters’.</span><span class="sxs-lookup"><span data-stu-id="77987-127">Find all people who work at the ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="77987-128">Obtener el número de personas que trabajan en ‘Home Office’.</span><span class="sxs-lookup"><span data-stu-id="77987-128">Get a count of the number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="77987-129">De las personas que trabajan en ‘Home Office’, mostrar con qué otras oficinas trabajan, además del número de personas en cada ubicación.</span><span class="sxs-lookup"><span data-stu-id="77987-129">Of the people who work at a ‘Home Office’, show what other offices they work along with a count of the people in each location.</span></span>  

<span data-ttu-id="77987-130">Esta técnica no funciona correctamente cuando se necesita realizar una búsqueda que combina el identificador de ubicación y la descripción de la ubicación.</span><span class="sxs-lookup"><span data-stu-id="77987-130">Where this technique falls apart is when you need to do a search that combines both the location id as well as the location description.</span></span> <span data-ttu-id="77987-131">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="77987-131">For example:</span></span>

* <span data-ttu-id="77987-132">Buscar todas las personas cuya ubicación es Home Office y su identificador de ubicación es 4.</span><span class="sxs-lookup"><span data-stu-id="77987-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="77987-133">Si recuerda, el contenido original tenía el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="77987-133">If you recall the original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="77987-134">Sin embargo, ahora que hemos separado los datos en campos independientes, no hay ninguna manera de saber si la ubicación Home Office de Jen Campbell está relacionada con `locationsID 3` o `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="77987-134">However, now that we have separated the data into separate fields, we have no way of knowing if the Home Office for Jen Campbell relates to `locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="77987-135">En este caso, defina otro campo en el índice que combine todos los datos en una sola colección.</span><span class="sxs-lookup"><span data-stu-id="77987-135">To handle this case, define another field in the index that combines all of the data into a single collection.</span></span>  <span data-ttu-id="77987-136">En nuestro ejemplo, llamaremos a este campo `locationsCombined` y separaremos el contenido con un `||`, aunque puede elegir cualquier separador que piense que sería un conjunto único de caracteres para su contenido.</span><span class="sxs-lookup"><span data-stu-id="77987-136">For our example, we will call this field `locationsCombined` and we will separate the content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="77987-137">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="77987-137">For example:</span></span> 

![datos de ejemplo, 2 filas con separador](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="77987-139">Con este campo `locationsCombined` , ahora podemos dar cabida a más consultas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="77987-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="77987-140">Mostrar el número de personas que trabajan en la ubicación 'Home Office' con un identificador de ubicación '4'.</span><span class="sxs-lookup"><span data-stu-id="77987-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="77987-141">Buscar las personas que trabajan en la ubicación 'Home Office' con un identificador de ubicación '4'.</span><span class="sxs-lookup"><span data-stu-id="77987-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="77987-142">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="77987-142">Limitations</span></span>
<span data-ttu-id="77987-143">Esta técnica es útil para diversos escenarios, pero no es aplicable en todos los casos.</span><span class="sxs-lookup"><span data-stu-id="77987-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="77987-144">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="77987-144">For example:</span></span>

1. <span data-ttu-id="77987-145">Si no tiene un conjunto de campos estático en el tipo de datos complejos y no hay manera de asignar todos los tipos posibles a un único campo.</span><span class="sxs-lookup"><span data-stu-id="77987-145">If you do not have a static set of fields in your complex data type and there was no way to map all the possible types to a single field.</span></span> 
2. <span data-ttu-id="77987-146">Actualizar los objetos anidados requiere trabajo adicional para determinar exactamente lo que hay que actualizar en el índice de Azure Search.</span><span class="sxs-lookup"><span data-stu-id="77987-146">Updating the nested objects requires some extra work to determine exactly what needs to be updated in the Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="77987-147">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="77987-147">Sample code</span></span>
<span data-ttu-id="77987-148">En este [repositorio de GitHub](https://github.com/liamca/AzureSearchComplexTypes)puede ver un ejemplo de cómo indizar un conjunto de datos JSON complejo en Azure Search y realizar diversas consultas sobre este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="77987-148">You can see an example on how to index a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="77987-149">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="77987-149">Next step</span></span>
<span data-ttu-id="77987-150">[Vote a favor de la compatibilidad nativa con tipos de datos complejos](https://feedback.azure.com/forums/263029-azure-search) en la página UserVoice de Azure Search y díganos qué le gustaría que tuviéramos en cuenta para la implementación de la característica.</span><span class="sxs-lookup"><span data-stu-id="77987-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on the Azure Search UserVoice page and provide any additional input that you’d like us to consider regarding feature implementation.</span></span> <span data-ttu-id="77987-151">Puede ponerse en contacto conmigo directamente en Twitter en @liamca.</span><span class="sxs-lookup"><span data-stu-id="77987-151">You can also reach out to me directly on Twitter at @liamca.</span></span>

