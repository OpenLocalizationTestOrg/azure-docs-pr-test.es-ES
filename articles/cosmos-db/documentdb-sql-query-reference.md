---
title: 'API de DocumentDB de Azure Cosmos DB: sintaxis SQL | Microsoft Docs'
description: "Documentación de referencia para el lenguaje de consulta SQL de la API de DocumentDB de Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 06/13/2017
ms.author: mimig
ms.openlocfilehash: 63b2d20c74df4fd6173994ee1a727594ba8afba3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="97819-103">API de DocumentDB de Azure Cosmos DB: referencia de sintaxis SQL</span><span class="sxs-lookup"><span data-stu-id="97819-103">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="97819-104">La API de DocumentDB de Azure Cosmos DB admite consultar documentos mediante una instancia de SQL (lenguaje de consulta estructurado) familiar, como gramática, en documentos JSON jerárquicos sin necesidad de esquemas explícitos ni de índices secundarios.</span><span class="sxs-lookup"><span data-stu-id="97819-104">The Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="97819-105">En este tema se ofrece documentación de referencia para el lenguaje de consulta SQL de la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="97819-105">This topic provides reference documentation for the DocumentDB API SQL query language.</span></span>

<span data-ttu-id="97819-106">Para ver un tutorial del lenguaje de consulta SQL de la API de DocumentDB, consulte [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md) (Consultas SQL para la API de DocumentDB de Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="97819-106">For a walkthrough of the DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="97819-107">Le invitamos a visitar también [Query Playground](http://www.documentdb.com/sql/demo), donde puede probar Azure Cosmos DB y ejecutar consultas SQL en nuestro conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="97819-107">We also invite you to visit the [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="97819-108">Consulta SELECT</span><span class="sxs-lookup"><span data-stu-id="97819-108">SELECT query</span></span>  
<span data-ttu-id="97819-109">Recupera documentos JSON de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="97819-109">Retrieves JSON documents from the database.</span></span> <span data-ttu-id="97819-110">Es compatible con la evaluación de expresiones, las proyecciones, el filtrado y las combinaciones.</span><span class="sxs-lookup"><span data-stu-id="97819-110">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="97819-111">Las convenciones que se usan para describir las instrucciones SELECT se tabulan en la sección de convenciones de sintaxis.</span><span class="sxs-lookup"><span data-stu-id="97819-111">The conventions used for describing the SELECT statements are tabulated in the Syntax conventions section.</span></span>  
  
<span data-ttu-id="97819-112">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-112">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="97819-113">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="97819-113">**Remarks**</span></span>  
  
 <span data-ttu-id="97819-114">Consulte las siguientes secciones para más información sobre las cláusulas:</span><span class="sxs-lookup"><span data-stu-id="97819-114">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="97819-115">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="97819-115">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="97819-116">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="97819-116">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="97819-117">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="97819-117">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="97819-118">Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="97819-118">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="97819-119">Las cláusulas de la instrucción SELECT se deben ordenar como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="97819-119">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="97819-120">Se puede omitir cualquiera de las cláusulas opcionales.</span><span class="sxs-lookup"><span data-stu-id="97819-120">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="97819-121">Pero cuando se usen, deben aparecer en el orden correcto.</span><span class="sxs-lookup"><span data-stu-id="97819-121">But when optional clauses are used, they must appear in the right order.</span></span>  
  
<span data-ttu-id="97819-122">**Orden de procesamiento lógico de la instrucción SELECT**</span><span class="sxs-lookup"><span data-stu-id="97819-122">**Logical Processing Order of the SELECT statement**</span></span>  
  
<span data-ttu-id="97819-123">El orden en que se procesan las cláusulas es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-123">The order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="97819-124">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="97819-124">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="97819-125">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="97819-125">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="97819-126">Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="97819-126">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="97819-127">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="97819-127">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="97819-128">Tenga en cuenta que difiere del orden en que aparecen en la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="97819-128">Note that this is different from the order in which they appear in the syntax.</span></span> <span data-ttu-id="97819-129">La ordenación es tal que todos los símbolos nuevos introducidos por una cláusula procesada son visibles y pueden utilizarse en las cláusulas que se procesen después.</span><span class="sxs-lookup"><span data-stu-id="97819-129">The ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="97819-130">Por ejemplo, las cláusulas WHERE y SELECT pueden acceder a los alias declarados en una cláusula FROM.</span><span class="sxs-lookup"><span data-stu-id="97819-130">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="97819-131">**Comentarios y caracteres de espacio en blanco**</span><span class="sxs-lookup"><span data-stu-id="97819-131">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="97819-132">Todos los caracteres de espacio en blanco que no formen parte de una cadena o identificador entrecomillados no forman parte de la gramática del lenguaje y se omiten durante el análisis.</span><span class="sxs-lookup"><span data-stu-id="97819-132">All white space characters which are not part of a quoted string or quoted identifier are not part of the language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="97819-133">El lenguaje de consulta admite comentarios del estilo de T-SQL como</span><span class="sxs-lookup"><span data-stu-id="97819-133">The query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="97819-134">Instrucción SQL `-- comment text [newline]`.</span><span class="sxs-lookup"><span data-stu-id="97819-134">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="97819-135">Aunque los comentarios y los caracteres de espacio en blanco no tienen significado en la gramática, deben utilizarse para separar tokens.</span><span class="sxs-lookup"><span data-stu-id="97819-135">While whitespace characters and comments do not have any significance in the grammar, they must be used to separate tokens.</span></span> <span data-ttu-id="97819-136">Por ejemplo: `-1e5` es un token de un solo número, mientras que `: – 1 e5` es un token de menos seguido por el número 1 y el identificador e5.</span><span class="sxs-lookup"><span data-stu-id="97819-136">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="97819-137"><a name="bk_select_query"></a> Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="97819-137"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="97819-138">Las cláusulas de la instrucción SELECT se deben ordenar como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="97819-138">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="97819-139">Se puede omitir cualquiera de las cláusulas opcionales.</span><span class="sxs-lookup"><span data-stu-id="97819-139">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="97819-140">Pero cuando se usen, deben aparecer en el orden correcto.</span><span class="sxs-lookup"><span data-stu-id="97819-140">But when optional clauses are used, they must appear in the right order.</span></span>  

<span data-ttu-id="97819-141">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-141">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="97819-142">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-142">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="97819-143">Propiedades o valor que se van a seleccionar para los resultados.</span><span class="sxs-lookup"><span data-stu-id="97819-143">Properties or value to be selected for the result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="97819-144">Especifica que se debe recuperar el valor sin cambios.</span><span class="sxs-lookup"><span data-stu-id="97819-144">Specifies that the value should be retrieved without making any changes.</span></span> <span data-ttu-id="97819-145">En particular, si el valor procesado es un objeto, se recuperarán todas las propiedades.</span><span class="sxs-lookup"><span data-stu-id="97819-145">Specifically if the processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="97819-146">Especifica la lista de propiedades que se recuperan.</span><span class="sxs-lookup"><span data-stu-id="97819-146">Specifies the list of properties to be retrieved.</span></span> <span data-ttu-id="97819-147">Los valores devueltos serán objetos con las propiedades especificadas.</span><span class="sxs-lookup"><span data-stu-id="97819-147">Each returned value will be an object with the properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="97819-148">Especifica que se debe recuperar el valor JSON en lugar del objeto JSON completo.</span><span class="sxs-lookup"><span data-stu-id="97819-148">Specifies that the JSON value should be retrieved instead of the complete JSON object.</span></span> <span data-ttu-id="97819-149">Esto, a diferencia de `<property_list>`, no encapsula el valor proyectado en un objeto.</span><span class="sxs-lookup"><span data-stu-id="97819-149">This, unlike `<property_list>` does not wrap the projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="97819-150">Expresión que representa el valor que hay que calcular.</span><span class="sxs-lookup"><span data-stu-id="97819-150">Expression representing the value to be computed.</span></span> <span data-ttu-id="97819-151">Consulte la sección [Expresiones escalares](#bk_scalar_expressions) para más información.</span><span class="sxs-lookup"><span data-stu-id="97819-151">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="97819-152">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="97819-152">**Remarks**</span></span>  
  
<span data-ttu-id="97819-153">La sintaxis `SELECT *` solo es válida si la cláusula FROM ha declarado exactamente un alias.</span><span class="sxs-lookup"><span data-stu-id="97819-153">The `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="97819-154">`SELECT *` proporciona una proyección de identidad, que puede resultar útil si no se necesitan proyecciones.</span><span class="sxs-lookup"><span data-stu-id="97819-154">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="97819-155">SELECT * solo es válida si se especifica cláusula FROM y se introdujo solo un origen de entrada.</span><span class="sxs-lookup"><span data-stu-id="97819-155">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="97819-156">Tenga en cuenta que `SELECT <select_list>` y `SELECT *` son código sintáctico y pueden expresarse también mediante instrucciones SELECT sencillas, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="97819-156">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="97819-157">equivale a:</span><span class="sxs-lookup"><span data-stu-id="97819-157">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="97819-158">equivale a:</span><span class="sxs-lookup"><span data-stu-id="97819-158">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="97819-159">**Consulte también**</span><span class="sxs-lookup"><span data-stu-id="97819-159">**See Also**</span></span>  
  
[<span data-ttu-id="97819-160">Expresiones escalares</span><span class="sxs-lookup"><span data-stu-id="97819-160">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="97819-161">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="97819-161">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="97819-162"><a name="bk_from_clause"></a> Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="97819-162"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="97819-163">Especifica el origen o la combinación de orígenes.</span><span class="sxs-lookup"><span data-stu-id="97819-163">Specifies the source or joined sources.</span></span> <span data-ttu-id="97819-164">La cláusula FROM es opcional.</span><span class="sxs-lookup"><span data-stu-id="97819-164">The FROM clause is optional.</span></span> <span data-ttu-id="97819-165">Si no se especifica, las demás cláusulas se continuarán ejecutando como si la cláusula FROM proporcionara un documento único.</span><span class="sxs-lookup"><span data-stu-id="97819-165">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="97819-166">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-166">**Syntax**</span></span>  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
<span data-ttu-id="97819-167">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-167">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="97819-168">Especifica un origen de datos, con o sin alias.</span><span class="sxs-lookup"><span data-stu-id="97819-168">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="97819-169">Si no se especifica, se deducirá de `<collection_expression>` con las siguientes reglas:</span><span class="sxs-lookup"><span data-stu-id="97819-169">If alias is not specified, it will be inferred from the `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="97819-170">Si la expresión es un nombre de colección, se utilizará collection_name como alias.</span><span class="sxs-lookup"><span data-stu-id="97819-170">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="97819-171">Si la expresión es `<collection_expression>`, se utilizará property_name como alias.</span><span class="sxs-lookup"><span data-stu-id="97819-171">If the expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="97819-172">Si la expresión es un nombre de colección, se utilizará collection_name como alias.</span><span class="sxs-lookup"><span data-stu-id="97819-172">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="97819-173">AS `input_alias`.</span><span class="sxs-lookup"><span data-stu-id="97819-173">AS `input_alias`</span></span>  
  
<span data-ttu-id="97819-174">Especifica que `input_alias` es un conjunto de valores que devuelve la expresión de la colección subyacente.</span><span class="sxs-lookup"><span data-stu-id="97819-174">Specifies that the `input_alias` is a set of values returned by the underlying collection expression.</span></span>  
 
<span data-ttu-id="97819-175">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="97819-175">`input_alias` IN</span></span>  
  
<span data-ttu-id="97819-176">Especifica que `input_alias` debe representar el conjunto de valores obtenidos al recorrer en iteración todos los elementos de las matrices que devuelve la expresión de la colección subyacente.</span><span class="sxs-lookup"><span data-stu-id="97819-176">Specifies that the `input_alias` should represent the set of values obtained by iterating over all array elements of each array returned by the underlying collection expression.</span></span> <span data-ttu-id="97819-177">Se omite cualquier valor que la expresión de colección subyacente devuelva que no sea una matriz.</span><span class="sxs-lookup"><span data-stu-id="97819-177">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="97819-178">Especifica la expresión de colección que se usará para recuperar los documentos.</span><span class="sxs-lookup"><span data-stu-id="97819-178">Specifies the collection expression to be used to retrieve the documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="97819-179">Especifica que debe recuperarse ese documento predeterminado de la colección actualmente conectada.</span><span class="sxs-lookup"><span data-stu-id="97819-179">Specifies that document should be retrieved from the default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="97819-180">Especifica que debe recuperarse ese documento de la colección indicada.</span><span class="sxs-lookup"><span data-stu-id="97819-180">Specifies that document should be retrieved from the provided collection.</span></span> <span data-ttu-id="97819-181">El nombre de la colección debe coincidir con el nombre de la colección conectada actualmente.</span><span class="sxs-lookup"><span data-stu-id="97819-181">The name of the collection must match the name of the collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="97819-182">Especifica que debe recuperarse ese documento desde otro origen que define el alias proporcionado.</span><span class="sxs-lookup"><span data-stu-id="97819-182">Specifies that document should be retrieved from the other source defined by the provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="97819-183">Especifica que debe recuperarse ese documento mediante el acceso a la propiedad `property_name` o el elemento de matriz array_index para todos los documentos que recupera una expresión de colección específica.</span><span class="sxs-lookup"><span data-stu-id="97819-183">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="97819-184">Especifica que debe recuperarse ese documento mediante el acceso a la propiedad `property_name` o el elemento de matriz array_index para todos los documentos que recupera una expresión de colección específica.</span><span class="sxs-lookup"><span data-stu-id="97819-184">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="97819-185">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="97819-185">**Remarks**</span></span>  
  
<span data-ttu-id="97819-186">Todos los alias proporcionados o deducidos en `<from_source>(` deben ser únicos.</span><span class="sxs-lookup"><span data-stu-id="97819-186">All aliases provided or inferred in the `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="97819-187">La sintaxis de property_name de `<collection_expression>.` es la misma que la de `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="97819-187">The Syntax `<collection_expression>.`property_name is the same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="97819-188">Sin embargo, esta última puede usarse si un nombre de propiedad contiene caracteres que no sean identificadores.</span><span class="sxs-lookup"><span data-stu-id="97819-188">However, the latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="97819-189">**Manejo de situaciones en las que faltan propiedades o elementos de matriz o en las que hay valores sin definir**</span><span class="sxs-lookup"><span data-stu-id="97819-189">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="97819-190">Si una expresión de colección accede a propiedades o elementos de matriz y el valor no existe, ese valor se omitirá y no se seguirá procesando.</span><span class="sxs-lookup"><span data-stu-id="97819-190">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="97819-191">**Ámbito de contexto de la expresión de la colección**</span><span class="sxs-lookup"><span data-stu-id="97819-191">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="97819-192">El ámbito de las expresiones de colección puede ser de colección o de documento:</span><span class="sxs-lookup"><span data-stu-id="97819-192">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="97819-193">Una expresión es de ámbito de colección si el origen subyacente de la expresión de colección es ROOT o `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="97819-193">An expression is collection-scoped, if the underlying source of the collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="97819-194">Este tipo de expresión representa un conjunto de documentos que se recuperan directamente de la colección y no dependen del procesamiento de otras expresiones de colección.</span><span class="sxs-lookup"><span data-stu-id="97819-194">Such an expression represents a set of documents retrieved from the collection directly, and is not dependent on the processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="97819-195">Una expresión es de ámbito de documento si el origen subyacente de la expresión de colección es el valor `input_alias` introducido anteriormente en la consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-195">An expression is document-scoped, if the underlying source of the collection expression is `input_alias` introduced earlier in the query.</span></span> <span data-ttu-id="97819-196">Esta expresión representa un conjunto de documentos obtenidos al evaluar la expresión de colección en el ámbito de cada documento perteneciente al conjunto asociado a la colección del alias.</span><span class="sxs-lookup"><span data-stu-id="97819-196">Such an expression represents a set of documents obtained by evaluating the collection expression in the scope of each document belonging to the set associated with the aliased collection.</span></span>  <span data-ttu-id="97819-197">El conjunto resultante será una unión de los conjuntos obtenidos al evaluar la expresión de colección para cada uno de los documentos del conjunto subyacente.</span><span class="sxs-lookup"><span data-stu-id="97819-197">The resulting set will be a union of sets obtained by evaluating the collection expression for each of the documents in the underlying set.</span></span>  
  
<span data-ttu-id="97819-198">**Combinaciones**</span><span class="sxs-lookup"><span data-stu-id="97819-198">**Joins**</span></span>  
  
<span data-ttu-id="97819-199">En la versión actual, Azure Cosmos DB admite combinaciones internas.</span><span class="sxs-lookup"><span data-stu-id="97819-199">In the current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="97819-200">Las funcionalidades de combinación adicionales estarán disponibles próximamente.</span><span class="sxs-lookup"><span data-stu-id="97819-200">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="97819-201">Las combinaciones internas derivan en un producto cruzado completo con los conjuntos participantes en la combinación.</span><span class="sxs-lookup"><span data-stu-id="97819-201">Inner joins result in a complete cross product of the sets participating in the join.</span></span> <span data-ttu-id="97819-202">El resultado de una combinación de N es un conjunto de tuplas de N elementos, donde cada valor de la tupla se asocia con el conjunto del alias participante en la combinación, accesible mediante una referencia a ese alias en otras cláusulas.</span><span class="sxs-lookup"><span data-stu-id="97819-202">The result of an N-way join is a set of N-element tuples, where each value in the tuple is associated with the aliased set participating in the join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="97819-203">La evaluación de la combinación depende del ámbito del contexto de los conjuntos participantes:</span><span class="sxs-lookup"><span data-stu-id="97819-203">The evaluation of the join depends on the context scope of the participating sets:</span></span>  
  
-  <span data-ttu-id="97819-204">La combinación entre un conjunto de ámbito de colección A y otro B da como resultado un producto cruzado de todos los elementos de los conjuntos A y B.</span><span class="sxs-lookup"><span data-stu-id="97819-204">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="97819-205">La combinación entre un conjunto A y un conjunto de ámbito de documento B da como resultado una unión de todos los conjuntos obtenidos de la evaluación de B para cada documento del conjunto A.</span><span class="sxs-lookup"><span data-stu-id="97819-205">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="97819-206">En la versión actual, el procesador de consultas admite un máximo de una expresión de ámbito de colección.</span><span class="sxs-lookup"><span data-stu-id="97819-206">In the current release, a maximum of one collection-scoped expression is supported by the query processor.</span></span>  
  
<span data-ttu-id="97819-207">**Ejemplos de combinaciones:**</span><span class="sxs-lookup"><span data-stu-id="97819-207">**Examples of joins:**</span></span>  
  
<span data-ttu-id="97819-208">Observemos la siguiente cláusula FROM: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="97819-208">Let's look at the following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="97819-209">Los orígenes definirán `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="97819-209">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="97819-210">Esta cláusula FROM devuelve un conjunto de N tuplas (tupla con N valores).</span><span class="sxs-lookup"><span data-stu-id="97819-210">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="97819-211">Cada tupla tiene valores generados por sus respectivos conjuntos en iteración de todos los alias de colección.</span><span class="sxs-lookup"><span data-stu-id="97819-211">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="97819-212">*Ejemplo de COMBINACIÓN 1, con 2 orígenes:*</span><span class="sxs-lookup"><span data-stu-id="97819-212">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="97819-213">`<from_source1>` tendrá ámbito de colección y representa el conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="97819-213">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="97819-214">`<from_source2>` tendrá ámbito de documento, hará referencia a input_alias1 y representará los conjuntos:</span><span class="sxs-lookup"><span data-stu-id="97819-214">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="97819-215">{1, 2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="97819-215">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="97819-216">{3} para `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="97819-216">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="97819-217">{4, 5} para `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="97819-217">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="97819-218">La cláusula FROM `<from_source1> JOIN <from_source2>` dará como resultado las siguientes tuplas:</span><span class="sxs-lookup"><span data-stu-id="97819-218">The FROM clause `<from_source1> JOIN <from_source2>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="97819-219">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="97819-219">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="97819-220">*Ejemplo de COMBINACIÓN 2, con 3 orígenes:*</span><span class="sxs-lookup"><span data-stu-id="97819-220">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="97819-221">`<from_source1>` tendrá ámbito de colección y representa el conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="97819-221">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="97819-222">`<from_source2>` tendrá ámbito de documento, hará referencia a `input_alias1` y representará los conjuntos:</span><span class="sxs-lookup"><span data-stu-id="97819-222">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="97819-223">{1, 2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="97819-223">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="97819-224">{3} para `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="97819-224">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="97819-225">{4, 5} para `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="97819-225">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="97819-226">`<from_source3>` tendrá ámbito de documento, hará referencia a `input_alias2` y representará los conjuntos:</span><span class="sxs-lookup"><span data-stu-id="97819-226">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="97819-227">{100, 200} para `input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="97819-227">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="97819-228">{300} para `input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="97819-228">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="97819-229">La cláusula FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` dará como resultado las siguientes tuplas:</span><span class="sxs-lookup"><span data-stu-id="97819-229">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="97819-230">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="97819-230">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="97819-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="97819-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="97819-232">Faltan tuplas para otros valores de `input_alias1` y `input_alias2`, para los cuales `<from_source3>` no devolvió ningún valor.</span><span class="sxs-lookup"><span data-stu-id="97819-232">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which the `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="97819-233">*Ejemplo de COMBINACIÓN 3, con 3 orígenes:*</span><span class="sxs-lookup"><span data-stu-id="97819-233">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="97819-234"><from_source1> tendrá ámbito de colección y representa el conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="97819-234">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="97819-235">`<from_source1>` tendrá ámbito de colección y representa el conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="97819-235">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="97819-236"><from_source2> tendrá ámbito de documento, hará referencia a input_alias1 y representará los conjuntos:</span><span class="sxs-lookup"><span data-stu-id="97819-236">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="97819-237">{1, 2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="97819-237">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="97819-238">{3} para `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="97819-238">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="97819-239">{4, 5} para `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="97819-239">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="97819-240">`<from_source3>` tendrá el ámbito `input_alias1` y representará los conjuntos:</span><span class="sxs-lookup"><span data-stu-id="97819-240">Let `<from_source3>` be scoped to `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="97819-241">{100, 200} para `input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="97819-241">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="97819-242">{300} para `input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="97819-242">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="97819-243">La cláusula FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` dará como resultado las siguientes tuplas:</span><span class="sxs-lookup"><span data-stu-id="97819-243">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="97819-244">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="97819-244">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="97819-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300), (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="97819-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="97819-246">Esto dio como resultado un producto cruzado entre `<from_source2>` y `<from_source3>`, ya que ambos tienen como ámbito el mismo `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="97819-246">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped to the same `<from_source1>`.</span></span>  <span data-ttu-id="97819-247">Esto dio como resultado 4 (2 x 2) tuplas con valor A, 0 tuplas con valor B (1 x 0) y 2 (2 x 1) tuplas con valor C.</span><span class="sxs-lookup"><span data-stu-id="97819-247">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="97819-248">**Consulte también**</span><span class="sxs-lookup"><span data-stu-id="97819-248">**See also**</span></span>  
  
 [<span data-ttu-id="97819-249">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="97819-249">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="97819-250"><a name="bk_where_clause"></a> Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="97819-250"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="97819-251">Especifica la condición de búsqueda para los documentos que devuelve la consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-251">Specifies the search condition for the documents returned by the query.</span></span>  
  
 <span data-ttu-id="97819-252">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-252">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="97819-253">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-253">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="97819-254">Especifica la condición que debe cumplirse para que se devuelvan los documentos.</span><span class="sxs-lookup"><span data-stu-id="97819-254">Specifies the condition to be met for the documents to be returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="97819-255">Expresión que representa el valor que hay que calcular.</span><span class="sxs-lookup"><span data-stu-id="97819-255">Expression representing the value to be computed.</span></span> <span data-ttu-id="97819-256">Consulte la sección [Expresiones escalares](#bk_scalar_expressions) para más información.</span><span class="sxs-lookup"><span data-stu-id="97819-256">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="97819-257">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="97819-257">**Remarks**</span></span>  
  
 <span data-ttu-id="97819-258">Para que el documento se devuelva, debe establecerse en true una expresión especificada como condición de filtro.</span><span class="sxs-lookup"><span data-stu-id="97819-258">In order for the document to be returned an expression specified as filter condition must evaluate to true.</span></span> <span data-ttu-id="97819-259">Solo un valor booleano true cumplirá la condición, los demás valores: undefined, null, false, número, matriz u objeto, no cumplirán la condición.</span><span class="sxs-lookup"><span data-stu-id="97819-259">Only Boolean value true will satisfy the condition, any other value: undefined, null, false, Number, Array or Object will not satisfy the condition.</span></span>  
  
##  <span data-ttu-id="97819-260"><a name="bk_orderby_clause"></a> Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="97819-260"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="97819-261">Especifica el criterio de ordenación para los resultados que devuelve la consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-261">Specifies the sorting order for results returned by the query.</span></span>  
  
 <span data-ttu-id="97819-262">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-262">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="97819-263">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-263">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="97819-264">Especifica una propiedad o una expresión para ordenar el conjunto de resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-264">Specifies a property or expression on which to sort the query result set.</span></span> <span data-ttu-id="97819-265">Se puede especificar una columna de ordenación como alias de nombre o de columna.</span><span class="sxs-lookup"><span data-stu-id="97819-265">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="97819-266">Se pueden especificar varias columnas de ordenación.</span><span class="sxs-lookup"><span data-stu-id="97819-266">Multiple sort columns can be specified.</span></span> <span data-ttu-id="97819-267">Los nombres de columna deben ser únicos.</span><span class="sxs-lookup"><span data-stu-id="97819-267">Column names must be unique.</span></span> <span data-ttu-id="97819-268">La secuencia de las columnas de ordenación en la cláusula ORDER BY define la organización del conjunto de resultados ordenado.</span><span class="sxs-lookup"><span data-stu-id="97819-268">The sequence of the sort columns in the ORDER BY clause defines the organization of the sorted result set.</span></span> <span data-ttu-id="97819-269">Es decir, el conjunto de resultados se ordena en función de la primera propiedad, esa lista ordenada se ordena en función de la segunda propiedad y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="97819-269">That is, the result set is sorted by the first property and then that ordered list is sorted by the second property, and so on.</span></span>  
  
     <span data-ttu-id="97819-270">Los nombres de columna indicados en la cláusula ORDER BY deben corresponderse con una columna de la lista seleccionada o con una que se defina en una tabla que se especifique en la cláusula FROM sin ambigüedades.</span><span class="sxs-lookup"><span data-stu-id="97819-270">The column names referenced in the ORDER BY clause must correspond to either a column in the select list or to a column defined in a table specified in the FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="97819-271">Especifica una propiedad o expresión únicas para ordenar el conjunto de resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-271">Specifies a single property or expression on which to sort the query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="97819-272">Consulte la sección [Expresiones escalares](#bk_scalar_expressions) para más información.</span><span class="sxs-lookup"><span data-stu-id="97819-272">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="97819-273">Especifica que los valores de la columna especificada se deben ordenar en orden ascendente o descendente.</span><span class="sxs-lookup"><span data-stu-id="97819-273">Specifies that the values in the specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="97819-274">ASC ordena los valores de menor a mayor.</span><span class="sxs-lookup"><span data-stu-id="97819-274">ASC sorts from the lowest value to highest value.</span></span> <span data-ttu-id="97819-275">DESC ordena los valores de mayor a menos.</span><span class="sxs-lookup"><span data-stu-id="97819-275">DESC sorts from highest value to lowest value.</span></span> <span data-ttu-id="97819-276">ASC es el criterio de ordenación predeterminado.</span><span class="sxs-lookup"><span data-stu-id="97819-276">ASC is the default sort order.</span></span> <span data-ttu-id="97819-277">Los valores null se tratan como valores mínimos.</span><span class="sxs-lookup"><span data-stu-id="97819-277">Null values are treated as the lowest possible values.</span></span>  
  
 <span data-ttu-id="97819-278">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="97819-278">**Remarks**</span></span>  
  
 <span data-ttu-id="97819-279">Aunque la gramática de consulta admite varias propiedades para order by, el tiempo de ejecución de consulta de Azure Cosmos DB admite solo la ordenación por una propiedad y únicamente según los nombres de propiedad, es decir, no según las propiedades calculadas.</span><span class="sxs-lookup"><span data-stu-id="97819-279">While the query grammar supports multiple order by properties, the Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="97819-280">La ordenación también requiere que la directiva de indexación incluya un índice de intervalo para la propiedad y el tipo especificado, con máxima precisión.</span><span class="sxs-lookup"><span data-stu-id="97819-280">Sorting also requires that the indexing policy includes a range index for the property and the specified type, with the maximum precision.</span></span> <span data-ttu-id="97819-281">Consulte la documentación de la directiva de indexación para más detalles.</span><span class="sxs-lookup"><span data-stu-id="97819-281">Refer to the indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="97819-282"><a name="bk_scalar_expressions"></a> Expresiones escalares</span><span class="sxs-lookup"><span data-stu-id="97819-282"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="97819-283">Una expresión escalar es una combinación de símbolos y operadores que se puede evaluar para obtener un solo valor.</span><span class="sxs-lookup"><span data-stu-id="97819-283">A scalar expression is a combination of symbols and operators that can be evaluated to obtain a single value.</span></span> <span data-ttu-id="97819-284">Las expresiones simples pueden ser constantes, referencias de propiedad, referencias de elementos de matriz, referencias de alias o llamadas de función.</span><span class="sxs-lookup"><span data-stu-id="97819-284">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="97819-285">Las expresiones simples se pueden combinar en expresiones complejas con operadores.</span><span class="sxs-lookup"><span data-stu-id="97819-285">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="97819-286">Para más información sobre los valores que puede tener una expresión escalar, consulte la sección [Constantes](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="97819-286">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="97819-287">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-287">**Syntax**</span></span>  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 <span data-ttu-id="97819-288">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-288">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="97819-289">Representa un valor constante.</span><span class="sxs-lookup"><span data-stu-id="97819-289">Represents a constant value.</span></span> <span data-ttu-id="97819-290">Consulte la sección [Constantes](#bk_constants) para más información.</span><span class="sxs-lookup"><span data-stu-id="97819-290">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="97819-291">Representa un valor definido por `input_alias`, introducido en la cláusula `FROM`.</span><span class="sxs-lookup"><span data-stu-id="97819-291">Represents a value defined by the `input_alias` introduced in the `FROM` clause.</span></span>  
    <span data-ttu-id="97819-292">Este valor nunca será **undefined**, los valores **undefined** se omiten de la entrada.</span><span class="sxs-lookup"><span data-stu-id="97819-292">This value is guaranteed to not be **undefined** –**undefined** values in the input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="97819-293">Representa un valor de propiedad de un objeto.</span><span class="sxs-lookup"><span data-stu-id="97819-293">Represents a value of the property of an object.</span></span> <span data-ttu-id="97819-294">Si la propiedad no existe o se hace referencia a ella con un valor que no es un objeto, la expresión se evalúa como valor **undefined**.</span><span class="sxs-lookup"><span data-stu-id="97819-294">If the property does not exist or property is referenced on a value which is not an object, then the expression evaluates to **undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="97819-295">Representa un valor de propiedad con nombre `property_name` o de elemento de matriz con el índice `array_index` de un objeto o matriz.</span><span class="sxs-lookup"><span data-stu-id="97819-295">Represents a value of the property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="97819-296">Si la propiedad no existe o se hace referencia a ella con un valor que no es un objeto, la expresión se evalúa como valor undefined.</span><span class="sxs-lookup"><span data-stu-id="97819-296">If the property/array index does not exist or the property/array index is referenced on a value which is not an object/array, then the expression evaluates to undefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="97819-297">Representa un operador que se aplica a un único valor.</span><span class="sxs-lookup"><span data-stu-id="97819-297">Represents an operator that is applied to a single value.</span></span> <span data-ttu-id="97819-298">Consulte la sección [Operadores](#bk_operators) para más información.</span><span class="sxs-lookup"><span data-stu-id="97819-298">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="97819-299">Representa un operador que se aplica a dos valores.</span><span class="sxs-lookup"><span data-stu-id="97819-299">Represents an operator that is applied to two values.</span></span> <span data-ttu-id="97819-300">Consulte la sección [Operadores](#bk_operators) para más información.</span><span class="sxs-lookup"><span data-stu-id="97819-300">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="97819-301">Representa un valor definido por el resultado de una llamada de función.</span><span class="sxs-lookup"><span data-stu-id="97819-301">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="97819-302">Función escalar definida por el nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="97819-302">Name of the user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="97819-303">Nombre de la función escalar incorporada.</span><span class="sxs-lookup"><span data-stu-id="97819-303">Name of the built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="97819-304">Representa un valor obtenido al crear un objeto con propiedades especificadas y sus valores.</span><span class="sxs-lookup"><span data-stu-id="97819-304">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="97819-305">Representa un valor obtenido al crear una matriz con valores especificados como elementos.</span><span class="sxs-lookup"><span data-stu-id="97819-305">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="97819-306">Representa un valor del nombre de parámetro especificado.</span><span class="sxs-lookup"><span data-stu-id="97819-306">Represents a value of the specified parameter name.</span></span> <span data-ttu-id="97819-307">Los nombres de parámetro deben tener un único @ como primer carácter.</span><span class="sxs-lookup"><span data-stu-id="97819-307">Parameter names must have a single @ as the first character.</span></span>  
  
 <span data-ttu-id="97819-308">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="97819-308">**Remarks**</span></span>  
  
 <span data-ttu-id="97819-309">Todos los argumentos deben estar definidos al llamar a una función escalar incorporada o definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="97819-309">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="97819-310">Si alguno de los argumentos no está definido, no se llamará a la función y el resultado será undefined.</span><span class="sxs-lookup"><span data-stu-id="97819-310">If any of the arguments is undefined, the function will not be called and the result will be undefined.</span></span>  
  
 <span data-ttu-id="97819-311">Al crear un objeto, se omitirá cualquier propiedad a la que se le haya asignado un valor undefined y no se incluirá en el objeto creado.</span><span class="sxs-lookup"><span data-stu-id="97819-311">When creating an object, any property that is assigned undefined value will be skipped and not included in the created object.</span></span>  
  
 <span data-ttu-id="97819-312">Al crear una matriz, se omitirá cualquier elemento al que se le haya asignado un valor **undefined** y no se incluirá en el objeto creado.</span><span class="sxs-lookup"><span data-stu-id="97819-312">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in the created object.</span></span> <span data-ttu-id="97819-313">Esto hará que el siguiente elemento definido ocupe su lugar de manera que la matriz creada no tenga índices omitidos.</span><span class="sxs-lookup"><span data-stu-id="97819-313">This will cause the next defined element to take its place in such a way that the created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="97819-314"><a name="bk_operators"></a> Operadores</span><span class="sxs-lookup"><span data-stu-id="97819-314"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="97819-315">En esta sección se describen los operadores compatibles.</span><span class="sxs-lookup"><span data-stu-id="97819-315">This section describes the supported operators.</span></span> <span data-ttu-id="97819-316">Cada operador puede asignarse exactamente a una categoría.</span><span class="sxs-lookup"><span data-stu-id="97819-316">Each operator can be assigned to exactly one category.</span></span>  
  
 <span data-ttu-id="97819-317">Consulte la siguiente tabla, **Categorías de operadores**, para más información acerca del control de los valores **undefined**, los requisitos de tipo de valores de entrada y el control de los valores con tipos no coincidentes.</span><span class="sxs-lookup"><span data-stu-id="97819-317">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="97819-318">**Categorías de operadores:**</span><span class="sxs-lookup"><span data-stu-id="97819-318">**Operator categories:**</span></span>  
  
|<span data-ttu-id="97819-319">**Categoría**</span><span class="sxs-lookup"><span data-stu-id="97819-319">**Category**</span></span>|<span data-ttu-id="97819-320">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="97819-320">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="97819-321">**aritméticos**</span><span class="sxs-lookup"><span data-stu-id="97819-321">**arithmetic**</span></span>|<span data-ttu-id="97819-322">El operador espera que las entradas sean números.</span><span class="sxs-lookup"><span data-stu-id="97819-322">Operator expects input(s) to be Number(s).</span></span> <span data-ttu-id="97819-323">La salida también es un número.</span><span class="sxs-lookup"><span data-stu-id="97819-323">Output is also a Number.</span></span> <span data-ttu-id="97819-324">Si alguna de las entradas es **undefined** o de un tipo que no sea un número, el resultado es **undefined**.</span><span class="sxs-lookup"><span data-stu-id="97819-324">If any of the inputs is **undefined** or type other than Number then the result is **undefined**.</span></span>|  
|<span data-ttu-id="97819-325">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="97819-325">**bitwise**</span></span>|<span data-ttu-id="97819-326">El operador espera que las entradas sean números enteros con signo de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="97819-326">Operator expects input(s) to be 32-bit signed integer Number(s).</span></span> <span data-ttu-id="97819-327">La salida también es un número entero con signo de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="97819-327">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="97819-328">Los valores que no sean enteros se redondean.</span><span class="sxs-lookup"><span data-stu-id="97819-328">Any non-integer value will be rounded.</span></span> <span data-ttu-id="97819-329">Los valores positivos se redondean a la baja y los negativos, a la alta.</span><span class="sxs-lookup"><span data-stu-id="97819-329">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="97819-330">Se convertirá cualquier valor que esté fuera del intervalo de enteros de 32 bits, aprovechando los últimos 32 bits de su notación de complemento a dos.</span><span class="sxs-lookup"><span data-stu-id="97819-330">Any value that is outside of the 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="97819-331">Si alguna de las entradas es **undefined** o de un tipo que no sea un número, el resultado es **undefined**.</span><span class="sxs-lookup"><span data-stu-id="97819-331">If any of the inputs is **undefined** or type other than Number, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="97819-332">**Nota:** El comportamiento anterior es compatible con el comportamiento del operador bit a bit de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="97819-332">**Note:** The above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="97819-333">**lógicos**</span><span class="sxs-lookup"><span data-stu-id="97819-333">**logical**</span></span>|<span data-ttu-id="97819-334">El operador espera que las entradas sean booleanos.</span><span class="sxs-lookup"><span data-stu-id="97819-334">Operator expects input(s) to be Boolean(s).</span></span> <span data-ttu-id="97819-335">La salida también es un booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-335">Output is also a Boolean.</span></span><br /><span data-ttu-id="97819-336">Si alguna de las entradas es **undefined** o de un tipo que no sea un booleano, el resultado es **undefined**.</span><span class="sxs-lookup"><span data-stu-id="97819-336">If any of the inputs is **undefined** or type other than Boolean, then the result will be **undefined**.</span></span>|  
|<span data-ttu-id="97819-337">**de comparación**</span><span class="sxs-lookup"><span data-stu-id="97819-337">**comparison**</span></span>|<span data-ttu-id="97819-338">El operador espera que las entradas sean del mismo tipo y sin valores undefined.</span><span class="sxs-lookup"><span data-stu-id="97819-338">Operator expects input(s) to have the same type and not be undefined.</span></span> <span data-ttu-id="97819-339">La salida es un booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-339">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="97819-340">Si alguna de las entradas es **undefined** o tienen distintos tipos, el resultado es **undefined**.</span><span class="sxs-lookup"><span data-stu-id="97819-340">If any of the inputs is **undefined** or the inputs have different types, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="97819-341">Consulte la tabla **Ordenación de los valores para la comparación** para conocer los detalles de ordenación de los valores.</span><span class="sxs-lookup"><span data-stu-id="97819-341">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="97819-342">**cadena**</span><span class="sxs-lookup"><span data-stu-id="97819-342">**string**</span></span>|<span data-ttu-id="97819-343">El operador espera que las entradas sean cadenas.</span><span class="sxs-lookup"><span data-stu-id="97819-343">Operator expects input(s) to be String(s).</span></span> <span data-ttu-id="97819-344">La salida también es una cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-344">Output is also a String.</span></span><br /><span data-ttu-id="97819-345">Si alguna de las entradas es **undefined** o de un tipo que no sea una cadena, el resultado es **undefined**.</span><span class="sxs-lookup"><span data-stu-id="97819-345">If any of the inputs is **undefined** or type other than String then the result is **undefined**.</span></span>|  
  
 <span data-ttu-id="97819-346">**Operadores unarios:**</span><span class="sxs-lookup"><span data-stu-id="97819-346">**Unary operators:**</span></span>  
  
|<span data-ttu-id="97819-347">**Name**</span><span class="sxs-lookup"><span data-stu-id="97819-347">**Name**</span></span>|<span data-ttu-id="97819-348">**Operador**</span><span class="sxs-lookup"><span data-stu-id="97819-348">**Operator**</span></span>|<span data-ttu-id="97819-349">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="97819-349">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="97819-350">**aritméticos**</span><span class="sxs-lookup"><span data-stu-id="97819-350">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="97819-351">Devuelve el valor numérico.</span><span class="sxs-lookup"><span data-stu-id="97819-351">Returns the number value.</span></span><br /><br /> <span data-ttu-id="97819-352">Negativos bit a bit.</span><span class="sxs-lookup"><span data-stu-id="97819-352">Bitwise negation.</span></span> <span data-ttu-id="97819-353">Devuelve el valor numérico negativo.</span><span class="sxs-lookup"><span data-stu-id="97819-353">Returns negated number value.</span></span>|  
|<span data-ttu-id="97819-354">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="97819-354">**bitwise**</span></span>|~|<span data-ttu-id="97819-355">Complemento de uno.</span><span class="sxs-lookup"><span data-stu-id="97819-355">Ones' complement.</span></span> <span data-ttu-id="97819-356">Devuelve un complemento de un valor numérico.</span><span class="sxs-lookup"><span data-stu-id="97819-356">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="97819-357">**lógicos**</span><span class="sxs-lookup"><span data-stu-id="97819-357">**Logical**</span></span>|<span data-ttu-id="97819-358">**NOT**</span><span class="sxs-lookup"><span data-stu-id="97819-358">**NOT**</span></span>|<span data-ttu-id="97819-359">Negación.</span><span class="sxs-lookup"><span data-stu-id="97819-359">Negation.</span></span> <span data-ttu-id="97819-360">Devuelve el valor booleano negativo.</span><span class="sxs-lookup"><span data-stu-id="97819-360">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="97819-361">**Operadores binarios:**</span><span class="sxs-lookup"><span data-stu-id="97819-361">**Binary operators:**</span></span>  
  
|<span data-ttu-id="97819-362">**Name**</span><span class="sxs-lookup"><span data-stu-id="97819-362">**Name**</span></span>|<span data-ttu-id="97819-363">**Operador**</span><span class="sxs-lookup"><span data-stu-id="97819-363">**Operator**</span></span>|<span data-ttu-id="97819-364">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="97819-364">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="97819-365">**aritméticos**</span><span class="sxs-lookup"><span data-stu-id="97819-365">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="97819-366">Suma.</span><span class="sxs-lookup"><span data-stu-id="97819-366">Addition.</span></span><br /><br /> <span data-ttu-id="97819-367">Resta.</span><span class="sxs-lookup"><span data-stu-id="97819-367">Subtraction.</span></span><br /><br /> <span data-ttu-id="97819-368">Multiplicación.</span><span class="sxs-lookup"><span data-stu-id="97819-368">Multiplication.</span></span><br /><br /> <span data-ttu-id="97819-369">División.</span><span class="sxs-lookup"><span data-stu-id="97819-369">Division.</span></span><br /><br /> <span data-ttu-id="97819-370">Modulación.</span><span class="sxs-lookup"><span data-stu-id="97819-370">Modulation.</span></span>|  
|<span data-ttu-id="97819-371">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="97819-371">**bitwise**</span></span>|<span data-ttu-id="97819-372">&#124;</span><span class="sxs-lookup"><span data-stu-id="97819-372">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="97819-373">OR bit a bit.</span><span class="sxs-lookup"><span data-stu-id="97819-373">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="97819-374">AND bit a bit.</span><span class="sxs-lookup"><span data-stu-id="97819-374">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="97819-375">XOR bit a bit.</span><span class="sxs-lookup"><span data-stu-id="97819-375">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="97819-376">Desplazamiento a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="97819-376">Left Shift.</span></span><br /><br /> <span data-ttu-id="97819-377">Desplazamiento a la derecha.</span><span class="sxs-lookup"><span data-stu-id="97819-377">Right Shift.</span></span><br /><br /> <span data-ttu-id="97819-378">Desplazamiento a la derecha con relleno de ceros.</span><span class="sxs-lookup"><span data-stu-id="97819-378">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="97819-379">**lógicos**</span><span class="sxs-lookup"><span data-stu-id="97819-379">**logical**</span></span>|<span data-ttu-id="97819-380">**AND**</span><span class="sxs-lookup"><span data-stu-id="97819-380">**AND**</span></span><br /><br /> <span data-ttu-id="97819-381">**O bien**</span><span class="sxs-lookup"><span data-stu-id="97819-381">**OR**</span></span>|<span data-ttu-id="97819-382">Conjunción lógica.</span><span class="sxs-lookup"><span data-stu-id="97819-382">Logical conjunction.</span></span> <span data-ttu-id="97819-383">Devuelve **true** si ambos argumentos son **true**, devuelve **false** en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="97819-383">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="97819-384">Conjunción lógica.</span><span class="sxs-lookup"><span data-stu-id="97819-384">Logical conjunction.</span></span> <span data-ttu-id="97819-385">Devuelve **true** si ambos argumentos son **true**, devuelve **false** en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="97819-385">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="97819-386">**de comparación**</span><span class="sxs-lookup"><span data-stu-id="97819-386">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="97819-387">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="97819-387">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="97819-388">**??**</span><span class="sxs-lookup"><span data-stu-id="97819-388">**??**</span></span>|<span data-ttu-id="97819-389">Igual a.</span><span class="sxs-lookup"><span data-stu-id="97819-389">Equals.</span></span> <span data-ttu-id="97819-390">Devuelve **true** si ambos argumentos son iguales, en caso contrario, devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="97819-390">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="97819-391">Diferente de.</span><span class="sxs-lookup"><span data-stu-id="97819-391">Not equal to.</span></span> <span data-ttu-id="97819-392">Devuelve **true** si ambos argumentos no son iguales, en caso contrario, devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="97819-392">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="97819-393">Mayor que.</span><span class="sxs-lookup"><span data-stu-id="97819-393">Greater Than.</span></span> <span data-ttu-id="97819-394">Devuelve **true** si el primer argumento es mayor que el segundo, en caso contrario, devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="97819-394">Returns **true** if first argument is greater than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="97819-395">Mayor o igual que.</span><span class="sxs-lookup"><span data-stu-id="97819-395">Greater Than or Equal To.</span></span> <span data-ttu-id="97819-396">Devuelve **true** si el primer argumento es mayor o igual que el segundo, en caso contrario, devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="97819-396">Returns **true** if first argument is greater than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="97819-397">Menor que.</span><span class="sxs-lookup"><span data-stu-id="97819-397">Less Than.</span></span> <span data-ttu-id="97819-398">Devuelve **true** si el primer argumento es menor que el segundo, en caso contrario, devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="97819-398">Returns **true** if first argument is less than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="97819-399">Menor o igual que.</span><span class="sxs-lookup"><span data-stu-id="97819-399">Less Than or Equal To.</span></span> <span data-ttu-id="97819-400">Devuelve **true** si el primer argumento es menor o igual que el segundo, en caso contrario, devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="97819-400">Returns **true** if first argument is less than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="97819-401">Fusionar.</span><span class="sxs-lookup"><span data-stu-id="97819-401">Coalesce.</span></span> <span data-ttu-id="97819-402">Devuelve el segundo argumento si el primero es un valor **undefined**.</span><span class="sxs-lookup"><span data-stu-id="97819-402">Returns the second argument if the first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="97819-403">**String**</span><span class="sxs-lookup"><span data-stu-id="97819-403">**String**</span></span>|<span data-ttu-id="97819-404">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="97819-404">**&#124;&#124;**</span></span>|<span data-ttu-id="97819-405">Concatenación.</span><span class="sxs-lookup"><span data-stu-id="97819-405">Concatenation.</span></span> <span data-ttu-id="97819-406">Devuelve una concatenación de ambos argumentos.</span><span class="sxs-lookup"><span data-stu-id="97819-406">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="97819-407">**Operadores ternarios:**</span><span class="sxs-lookup"><span data-stu-id="97819-407">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="97819-408">Operador ternario</span><span class="sxs-lookup"><span data-stu-id="97819-408">Ternary operator</span></span>|<span data-ttu-id="97819-409">?</span><span class="sxs-lookup"><span data-stu-id="97819-409">?</span></span>|<span data-ttu-id="97819-410">Devuelve el segundo argumento si el primero se evalúa como **true**, en caso contrario, devuelve el tercer argumento.</span><span class="sxs-lookup"><span data-stu-id="97819-410">Returns the second argument if the first argument evaluates to **true**; return the third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="97819-411">**Ordenación de los valores para la comparación**</span><span class="sxs-lookup"><span data-stu-id="97819-411">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="97819-412">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="97819-412">**Type**</span></span>|<span data-ttu-id="97819-413">**Orden de los valores**</span><span class="sxs-lookup"><span data-stu-id="97819-413">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="97819-414">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="97819-414">**Undefined**</span></span>|<span data-ttu-id="97819-415">No comparables.</span><span class="sxs-lookup"><span data-stu-id="97819-415">Not comparable.</span></span>|  
|<span data-ttu-id="97819-416">**Null**</span><span class="sxs-lookup"><span data-stu-id="97819-416">**Null**</span></span>|<span data-ttu-id="97819-417">Valor único: **null**</span><span class="sxs-lookup"><span data-stu-id="97819-417">Single value: **null**</span></span>|  
|<span data-ttu-id="97819-418">**Number**</span><span class="sxs-lookup"><span data-stu-id="97819-418">**Number**</span></span>|<span data-ttu-id="97819-419">Número real natural.</span><span class="sxs-lookup"><span data-stu-id="97819-419">Natural real number.</span></span><br /><br /> <span data-ttu-id="97819-420">El valor de infinito negativo es menor que cualquier otro valor numérico.</span><span class="sxs-lookup"><span data-stu-id="97819-420">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="97819-421">El valor de infinito positivo es mayor que cualquier otro valor numérico. El valor **NaN** no es comparable.</span><span class="sxs-lookup"><span data-stu-id="97819-421">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="97819-422">La comparación con **NaN** dará como resultado el valor **undefined**.</span><span class="sxs-lookup"><span data-stu-id="97819-422">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="97819-423">**String**</span><span class="sxs-lookup"><span data-stu-id="97819-423">**String**</span></span>|<span data-ttu-id="97819-424">Orden lexicográfico.</span><span class="sxs-lookup"><span data-stu-id="97819-424">Lexicographical order.</span></span>|  
|<span data-ttu-id="97819-425">**Array**</span><span class="sxs-lookup"><span data-stu-id="97819-425">**Array**</span></span>|<span data-ttu-id="97819-426">Ningún orden, pero equitativo.</span><span class="sxs-lookup"><span data-stu-id="97819-426">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="97819-427">**Object**</span><span class="sxs-lookup"><span data-stu-id="97819-427">**Object**</span></span>|<span data-ttu-id="97819-428">Ningún orden, pero equitativo.</span><span class="sxs-lookup"><span data-stu-id="97819-428">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="97819-429">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="97819-429">**Remarks**</span></span>  
  
 <span data-ttu-id="97819-430">En Azure Cosmos DB, a menudo no se conocen los tipos de los valores hasta que se recuperan de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="97819-430">In Azure Cosmos DB, the types of values are often not known until they are actually retrieved from the database.</span></span> <span data-ttu-id="97819-431">Para admitir la ejecución de consultas de forma eficaz, la mayoría de los operadores tienen requisitos de tipo estrictos.</span><span class="sxs-lookup"><span data-stu-id="97819-431">In order to support efficient execution of queries, most of the operators have strict type requirements.</span></span> <span data-ttu-id="97819-432">Además, los operadores por sí mismos no realizan conversiones implícitas.</span><span class="sxs-lookup"><span data-stu-id="97819-432">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="97819-433">Esto significa que una consulta como: SELECT * FROM ROOT r WHERE r.Age = 21 solo devolverá documentos con la propiedad Age igual al número 21.</span><span class="sxs-lookup"><span data-stu-id="97819-433">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal to the number 21.</span></span> <span data-ttu-id="97819-434">Los documentos con la propiedad Age igual a la cadena "21" o a la cadena "0021" no coincidirán, ya que la expresión "21" = 21 se cuenta como undefined.</span><span class="sxs-lookup"><span data-stu-id="97819-434">Documents with property Age equal to the string "21" or the string "0021" will not match, as the expression "21" = 21 evaluates to undefined.</span></span> <span data-ttu-id="97819-435">Esto permite un mejor uso de los índices, ya que la búsqueda de un valor específico (es decir, el número 21) es más rápida que la búsqueda de un número indefinido de coincidencias posibles (es decir, el número 21 o las cadenas "21", "021", "21,0", etc.).</span><span class="sxs-lookup"><span data-stu-id="97819-435">This allows for a better use of indexes, because the lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="97819-436">Esto difiere de la evaluación de los distintos tipos de valores de los operadores en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="97819-436">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="97819-437">**Comparación e igualdad de objetos y matrices**</span><span class="sxs-lookup"><span data-stu-id="97819-437">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="97819-438">La comparación de valores de Array u Object mediante los operadores de intervalo (>, > =, <, < =) dará como resultado undefined, ya que no hay orden definido en los valores de Object o Array.</span><span class="sxs-lookup"><span data-stu-id="97819-438">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="97819-439">Sin embargo, se admite con operadores de igualdad y desigualdad (=,! =, <>) y los valores se compararán estructuralmente.</span><span class="sxs-lookup"><span data-stu-id="97819-439">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="97819-440">Las matrices son iguales si ambas tienen el mismo número de elementos y los elementos de las posiciones coincidentes también son iguales.</span><span class="sxs-lookup"><span data-stu-id="97819-440">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="97819-441">Si la comparación de cualquier par de resultados de elementos es undefined, el resultado de la comparación de matrices es undefined.</span><span class="sxs-lookup"><span data-stu-id="97819-441">If comparing any pair of elements results in undefined, the result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="97819-442">Los objetos son iguales si tienen las mismas propiedades definidas y si los valores de las propiedades coincidentes también son iguales.</span><span class="sxs-lookup"><span data-stu-id="97819-442">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="97819-443">Si la comparación de cualquier par de valores de propiedad es undefined, el resultado de la comparación de objetos es undefined.</span><span class="sxs-lookup"><span data-stu-id="97819-443">If comparing any pair of property values results in undefined, the result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="97819-444"><a name="bk_constants"></a> Constantes</span><span class="sxs-lookup"><span data-stu-id="97819-444"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="97819-445">Una constante, también conocida como valor literal o escalar, es un símbolo que representa un valor de datos específicos.</span><span class="sxs-lookup"><span data-stu-id="97819-445">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="97819-446">El formato de una constante depende del tipo de datos del valor que representa.</span><span class="sxs-lookup"><span data-stu-id="97819-446">The format of a constant depends on the data type of the value it represents.</span></span>  
  
 <span data-ttu-id="97819-447">**Tipos de datos escalares admitidos:**</span><span class="sxs-lookup"><span data-stu-id="97819-447">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="97819-448">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="97819-448">**Type**</span></span>|<span data-ttu-id="97819-449">**Orden de los valores**</span><span class="sxs-lookup"><span data-stu-id="97819-449">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="97819-450">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="97819-450">**Undefined**</span></span>|<span data-ttu-id="97819-451">Valor único: **undefined**</span><span class="sxs-lookup"><span data-stu-id="97819-451">Single value: **undefined**</span></span>|  
|<span data-ttu-id="97819-452">**Null**</span><span class="sxs-lookup"><span data-stu-id="97819-452">**Null**</span></span>|<span data-ttu-id="97819-453">Valor único: **null**</span><span class="sxs-lookup"><span data-stu-id="97819-453">Single value: **null**</span></span>|  
|<span data-ttu-id="97819-454">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="97819-454">**Boolean**</span></span>|<span data-ttu-id="97819-455">Valores: **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="97819-455">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="97819-456">**Number**</span><span class="sxs-lookup"><span data-stu-id="97819-456">**Number**</span></span>|<span data-ttu-id="97819-457">Número de punto flotante de precisión doble, estándar IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="97819-457">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="97819-458">**String**</span><span class="sxs-lookup"><span data-stu-id="97819-458">**String**</span></span>|<span data-ttu-id="97819-459">Secuencia de cero o más caracteres Unicode.</span><span class="sxs-lookup"><span data-stu-id="97819-459">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="97819-460">Las cadenas deben ir entre comillas sencillas o dobles.</span><span class="sxs-lookup"><span data-stu-id="97819-460">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="97819-461">**Array**</span><span class="sxs-lookup"><span data-stu-id="97819-461">**Array**</span></span>|<span data-ttu-id="97819-462">Secuencia de cero o más elementos.</span><span class="sxs-lookup"><span data-stu-id="97819-462">A sequence of zero or more elements.</span></span> <span data-ttu-id="97819-463">Cada elemento puede ser un valor de cualquier tipo de datos escalar, excepto Undefined.</span><span class="sxs-lookup"><span data-stu-id="97819-463">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="97819-464">**Object**</span><span class="sxs-lookup"><span data-stu-id="97819-464">**Object**</span></span>|<span data-ttu-id="97819-465">Conjunto desordenado de cero o más pares nombre/valor.</span><span class="sxs-lookup"><span data-stu-id="97819-465">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="97819-466">Nombre es una cadena Unicode, el valor puede ser de cualquier tipo de datos escalar, excepto **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="97819-466">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="97819-467">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-467">**Syntax**</span></span>  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 <span data-ttu-id="97819-468">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-468">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="97819-469">Representa un valor sin definir de tipo Undefined.</span><span class="sxs-lookup"><span data-stu-id="97819-469">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="97819-470">Representa el valor **null** de tipo **Null**.</span><span class="sxs-lookup"><span data-stu-id="97819-470">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="97819-471">Representa la constante de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-471">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="97819-472">Representa el valor **false** de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-472">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="97819-473">Representa el valor **true** de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-473">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="97819-474">Representa una constante.</span><span class="sxs-lookup"><span data-stu-id="97819-474">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="97819-475">Los literales decimales son números representados mediante notación decimal o científica.</span><span class="sxs-lookup"><span data-stu-id="97819-475">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="97819-476">Los literales hexadecimales son números representados mediante el prefijo "0x-" seguido de uno o más dígitos hexadecimales.</span><span class="sxs-lookup"><span data-stu-id="97819-476">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="97819-477">Representa una constante de tipo cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-477">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="97819-478">Los literales de cadena son cadenas Unicode representadas por una secuencia de cero o varios caracteres Unicode o secuencias de escape.</span><span class="sxs-lookup"><span data-stu-id="97819-478">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="97819-479">Los literales de cadena se encierran entre comillas simples (apóstrofo: ') o comillas dobles (comillas: ").</span><span class="sxs-lookup"><span data-stu-id="97819-479">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="97819-480">Se permiten las secuencias de escape siguientes:</span><span class="sxs-lookup"><span data-stu-id="97819-480">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="97819-481">**Secuencia de escape**</span><span class="sxs-lookup"><span data-stu-id="97819-481">**Escape sequence**</span></span>|<span data-ttu-id="97819-482">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="97819-482">**Description**</span></span>|<span data-ttu-id="97819-483">**Carácter Unicode**</span><span class="sxs-lookup"><span data-stu-id="97819-483">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="97819-484">\\'</span><span class="sxs-lookup"><span data-stu-id="97819-484">\\'</span></span>|<span data-ttu-id="97819-485">apóstrofo (')</span><span class="sxs-lookup"><span data-stu-id="97819-485">apostrophe (')</span></span>|<span data-ttu-id="97819-486">U + 0027</span><span class="sxs-lookup"><span data-stu-id="97819-486">U+0027</span></span>|  
|<span data-ttu-id="97819-487">\\"</span><span class="sxs-lookup"><span data-stu-id="97819-487">\\"</span></span>|<span data-ttu-id="97819-488">comillas dobles (")</span><span class="sxs-lookup"><span data-stu-id="97819-488">quotation mark (")</span></span>|<span data-ttu-id="97819-489">U + 0022</span><span class="sxs-lookup"><span data-stu-id="97819-489">U+0022</span></span>|  
|\\\|<span data-ttu-id="97819-490">barra inclinada inversa (\\)</span><span class="sxs-lookup"><span data-stu-id="97819-490">reverse solidus (\\)</span></span>|<span data-ttu-id="97819-491">U + 005C</span><span class="sxs-lookup"><span data-stu-id="97819-491">U+005C</span></span>|  
|\\/|<span data-ttu-id="97819-492">barra inclinada (/)</span><span class="sxs-lookup"><span data-stu-id="97819-492">solidus (/)</span></span>|<span data-ttu-id="97819-493">U + 002F</span><span class="sxs-lookup"><span data-stu-id="97819-493">U+002F</span></span>|  
|<span data-ttu-id="97819-494">\b</span><span class="sxs-lookup"><span data-stu-id="97819-494">\b</span></span>|<span data-ttu-id="97819-495">retroceso</span><span class="sxs-lookup"><span data-stu-id="97819-495">backspace</span></span>|<span data-ttu-id="97819-496">U + 0008</span><span class="sxs-lookup"><span data-stu-id="97819-496">U+0008</span></span>|  
|<span data-ttu-id="97819-497">\f</span><span class="sxs-lookup"><span data-stu-id="97819-497">\f</span></span>|<span data-ttu-id="97819-498">avance de página</span><span class="sxs-lookup"><span data-stu-id="97819-498">form feed</span></span>|<span data-ttu-id="97819-499">U + 000C</span><span class="sxs-lookup"><span data-stu-id="97819-499">U+000C</span></span>|  
|\n|<span data-ttu-id="97819-500">avance de línea</span><span class="sxs-lookup"><span data-stu-id="97819-500">line feed</span></span>|<span data-ttu-id="97819-501">U + 000A</span><span class="sxs-lookup"><span data-stu-id="97819-501">U+000A</span></span>|  
|<span data-ttu-id="97819-502">\r</span><span class="sxs-lookup"><span data-stu-id="97819-502">\r</span></span>|<span data-ttu-id="97819-503">retorno de carro</span><span class="sxs-lookup"><span data-stu-id="97819-503">carriage return</span></span>|<span data-ttu-id="97819-504">U + 000D</span><span class="sxs-lookup"><span data-stu-id="97819-504">U+000D</span></span>|  
|<span data-ttu-id="97819-505">\t</span><span class="sxs-lookup"><span data-stu-id="97819-505">\t</span></span>|<span data-ttu-id="97819-506">tabulador</span><span class="sxs-lookup"><span data-stu-id="97819-506">tab</span></span>|<span data-ttu-id="97819-507">U + 0009</span><span class="sxs-lookup"><span data-stu-id="97819-507">U+0009</span></span>|  
|<span data-ttu-id="97819-508">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="97819-508">\uXXXX</span></span>|<span data-ttu-id="97819-509">Carácter Unicode definidos por 4 dígitos hexadecimales.</span><span class="sxs-lookup"><span data-stu-id="97819-509">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="97819-510">U + XXXX</span><span class="sxs-lookup"><span data-stu-id="97819-510">U+XXXX</span></span>|  
  
##  <span data-ttu-id="97819-511"><a name="bk_query_perf_guidelines"></a> Guías de rendimiento de las consultas</span><span class="sxs-lookup"><span data-stu-id="97819-511"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="97819-512">Para que una consulta se ejecute de forma eficaz con una colección extensa, debe utilizar filtros que puedan obtenerse a través de uno o más índices.</span><span class="sxs-lookup"><span data-stu-id="97819-512">In order for a query to be executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="97819-513">Para la búsqueda de índices, se considerarán los filtros siguientes:</span><span class="sxs-lookup"><span data-stu-id="97819-513">The following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="97819-514">Utilice el operador de igualdad (=) con expresiones de ruta de acceso de documentos y constantes.</span><span class="sxs-lookup"><span data-stu-id="97819-514">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="97819-515">Utilice los operadores de intervalo (<, \<=, >, >=) con expresiones de ruta de acceso de documentos y constantes numéricas.</span><span class="sxs-lookup"><span data-stu-id="97819-515">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="97819-516">Una expresión de ruta de acceso de documento es cualquier expresión que identifica una ruta de acceso constante en los documentos de la colección de la base de datos a la que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="97819-516">Document path expression stands for any expression which identifies a constant path in the documents from the referenced database collection.</span></span>  
  
 <span data-ttu-id="97819-517">**Expresión de ruta de acceso de documento**</span><span class="sxs-lookup"><span data-stu-id="97819-517">**Document path expression**</span></span>  
  
 <span data-ttu-id="97819-518">Las expresiones de ruta de acceso de documento son expresiones que evalúan la ruta de una propiedad o un indexador de matrices en un documento procedente de la colección de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="97819-518">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="97819-519">Esta ruta de acceso sirve para identificar directamente la ubicación de los valores a los que se hace referencia en un filtro en los documentos de la colección de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="97819-519">This path can be used to identify the location of values referenced in a filter directly within the documents in the database collection.</span></span>  
  
 <span data-ttu-id="97819-520">Para que una expresión se considere una expresión de ruta de acceso de documento, debe:</span><span class="sxs-lookup"><span data-stu-id="97819-520">For an expression to be considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="97819-521">Hacer referencia directamente a la raíz de la colección.</span><span class="sxs-lookup"><span data-stu-id="97819-521">Reference the collection root directly.</span></span>  
  
2.  <span data-ttu-id="97819-522">Hacer referencia al indexador de matrices de propiedad o constantes de alguna expresión de ruta de acceso de documento.</span><span class="sxs-lookup"><span data-stu-id="97819-522">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="97819-523">Hacer referencia a un alias, que represente alguna expresión de ruta de acceso de documento.</span><span class="sxs-lookup"><span data-stu-id="97819-523">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="97819-524">**Convenciones de sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-524">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="97819-525">En la tabla siguiente se indican las convenciones utilizadas para describir la sintaxis de las referencias del lenguaje de consulta de la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="97819-525">The following table describes the conventions used to describe syntax in the DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="97819-526">**Convención**</span><span class="sxs-lookup"><span data-stu-id="97819-526">**Convention**</span></span>|<span data-ttu-id="97819-527">**Se usa para**</span><span class="sxs-lookup"><span data-stu-id="97819-527">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="97819-528">MAYÚSCULAS</span><span class="sxs-lookup"><span data-stu-id="97819-528">UPPERCASE</span></span>|<span data-ttu-id="97819-529">Palabras clave sin distinción entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="97819-529">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="97819-530">minúsculas</span><span class="sxs-lookup"><span data-stu-id="97819-530">lowercase</span></span>|<span data-ttu-id="97819-531">Palabras clave con distinción entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="97819-531">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="97819-532">\<noterminal></span><span class="sxs-lookup"><span data-stu-id="97819-532">\<nonterminal></span></span>|<span data-ttu-id="97819-533">Elemento no terminal, se define por separado.</span><span class="sxs-lookup"><span data-stu-id="97819-533">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="97819-534">\<noterminal> ::=</span><span class="sxs-lookup"><span data-stu-id="97819-534">\<nonterminal> ::=</span></span>|<span data-ttu-id="97819-535">Definición de la sintaxis del elemento no terminal.</span><span class="sxs-lookup"><span data-stu-id="97819-535">Syntax definition of the nonterminal.</span></span>|  
    |<span data-ttu-id="97819-536">otro_terminal</span><span class="sxs-lookup"><span data-stu-id="97819-536">other_terminal</span></span>|<span data-ttu-id="97819-537">Terminal (token), se describe detalladamente en palabras.</span><span class="sxs-lookup"><span data-stu-id="97819-537">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="97819-538">identificador</span><span class="sxs-lookup"><span data-stu-id="97819-538">identifier</span></span>|<span data-ttu-id="97819-539">Identificador.</span><span class="sxs-lookup"><span data-stu-id="97819-539">Identifier.</span></span> <span data-ttu-id="97819-540">Solo admite los caracteres siguientes:, a-z, A-Z, 0-9 _El primer carácter no puede ser un dígito.</span><span class="sxs-lookup"><span data-stu-id="97819-540">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="97819-541">"cadena"</span><span class="sxs-lookup"><span data-stu-id="97819-541">"string"</span></span>|<span data-ttu-id="97819-542">Cadena entrecomillada.</span><span class="sxs-lookup"><span data-stu-id="97819-542">Quoted string.</span></span> <span data-ttu-id="97819-543">Permite cualquier cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-543">Allows any valid string.</span></span> <span data-ttu-id="97819-544">Vea la descripción de string_literal.</span><span class="sxs-lookup"><span data-stu-id="97819-544">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="97819-545">'símbolo'</span><span class="sxs-lookup"><span data-stu-id="97819-545">'symbol'</span></span>|<span data-ttu-id="97819-546">Símbolo literal que forma parte de la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="97819-546">Literal symbol which is part of the syntax.</span></span>|  
    |<span data-ttu-id="97819-547">&#124; (barra vertical)</span><span class="sxs-lookup"><span data-stu-id="97819-547">&#124; (vertical bar)</span></span>|<span data-ttu-id="97819-548">Alternativas para los elementos de la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="97819-548">Alternatives for syntax items.</span></span> <span data-ttu-id="97819-549">Puede usar solo uno de los elementos especificados.</span><span class="sxs-lookup"><span data-stu-id="97819-549">You can use only one of the items specified.</span></span>|  
    |<span data-ttu-id="97819-550">[] /(corchetes)</span><span class="sxs-lookup"><span data-stu-id="97819-550">[ ] /(brackets)</span></span>|<span data-ttu-id="97819-551">Los corchetes contienen uno o varios elementos opcionales.</span><span class="sxs-lookup"><span data-stu-id="97819-551">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="97819-552">[, ...n]</span><span class="sxs-lookup"><span data-stu-id="97819-552">[ ,...n ]</span></span>|<span data-ttu-id="97819-553">Indica que el elemento anterior se puede repetir un número n de veces.</span><span class="sxs-lookup"><span data-stu-id="97819-553">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="97819-554">Los elementos se separan por comas.</span><span class="sxs-lookup"><span data-stu-id="97819-554">The occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="97819-555">[ ...n]</span><span class="sxs-lookup"><span data-stu-id="97819-555">[ ...n ]</span></span>|<span data-ttu-id="97819-556">Indica que el elemento anterior se puede repetir un número n de veces.</span><span class="sxs-lookup"><span data-stu-id="97819-556">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="97819-557">Los elementos se separan por espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="97819-557">The occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="97819-558"><a name="bk_built_in_functions"></a> Funciones integradas</span><span class="sxs-lookup"><span data-stu-id="97819-558"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="97819-559">Azure Cosmos DB proporciona muchas funciones de SQL integradas.</span><span class="sxs-lookup"><span data-stu-id="97819-559">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="97819-560">Las categorías de las funciones integradas aparecen a continuación.</span><span class="sxs-lookup"><span data-stu-id="97819-560">The categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="97819-561">Función</span><span class="sxs-lookup"><span data-stu-id="97819-561">Function</span></span>|<span data-ttu-id="97819-562">Descripción</span><span class="sxs-lookup"><span data-stu-id="97819-562">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="97819-563">Funciones matemáticas</span><span class="sxs-lookup"><span data-stu-id="97819-563">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="97819-564">Las funciones matemáticas realizan un cálculo, basado normalmente en valores de entrada proporcionados como argumentos, y devuelven un valor numérico.</span><span class="sxs-lookup"><span data-stu-id="97819-564">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="97819-565">Funciones de comprobación de tipos</span><span class="sxs-lookup"><span data-stu-id="97819-565">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="97819-566">Las funciones de comprobación de tipos permiten comprobar el tipo de una expresión dentro de consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="97819-566">The type checking functions allow you to check the type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="97819-567">Funciones de cadena</span><span class="sxs-lookup"><span data-stu-id="97819-567">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="97819-568">Las siguientes funciones de cadena realizan una operación sobre un valor de entrada de cadena y devuelven una cadena, un valor numérico o un booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-568">The string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="97819-569">Funciones de matriz</span><span class="sxs-lookup"><span data-stu-id="97819-569">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="97819-570">Las siguientes funciones de matriz realizan una operación en un valor de entrada de matriz y devolver un valor numérico, booleano o de matriz.</span><span class="sxs-lookup"><span data-stu-id="97819-570">The array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="97819-571">Funciones espaciales</span><span class="sxs-lookup"><span data-stu-id="97819-571">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="97819-572">Las siguientes funciones espaciales realizan una operación en un valor de entrada de objeto espacial y devuelven un valor numérico o un booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-572">The spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="97819-573"><a name="bk_mathematical_functions"></a> Funciones matemáticas</span><span class="sxs-lookup"><span data-stu-id="97819-573"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="97819-574">Las siguientes funciones realizan un cálculo, basado normalmente en valores de entrada que se proporcionan como argumentos, y devuelven un valor numérico.</span><span class="sxs-lookup"><span data-stu-id="97819-574">The following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="97819-575">ABS</span><span class="sxs-lookup"><span data-stu-id="97819-575">ABS</span></span>](#bk_abs)|[<span data-ttu-id="97819-576">ACOS</span><span class="sxs-lookup"><span data-stu-id="97819-576">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="97819-577">ASIN</span><span class="sxs-lookup"><span data-stu-id="97819-577">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="97819-578">ATAN</span><span class="sxs-lookup"><span data-stu-id="97819-578">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="97819-579">ATN2</span><span class="sxs-lookup"><span data-stu-id="97819-579">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="97819-580">CEILING</span><span class="sxs-lookup"><span data-stu-id="97819-580">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="97819-581">COS</span><span class="sxs-lookup"><span data-stu-id="97819-581">COS</span></span>](#bk_cos)|[<span data-ttu-id="97819-582">COT</span><span class="sxs-lookup"><span data-stu-id="97819-582">COT</span></span>](#bk_cot)|[<span data-ttu-id="97819-583">DEGREES</span><span class="sxs-lookup"><span data-stu-id="97819-583">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="97819-584">EXP</span><span class="sxs-lookup"><span data-stu-id="97819-584">EXP</span></span>](#bk_exp)|[<span data-ttu-id="97819-585">FLOOR</span><span class="sxs-lookup"><span data-stu-id="97819-585">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="97819-586">LOG</span><span class="sxs-lookup"><span data-stu-id="97819-586">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="97819-587">LOG10</span><span class="sxs-lookup"><span data-stu-id="97819-587">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="97819-588">PI</span><span class="sxs-lookup"><span data-stu-id="97819-588">PI</span></span>](#bk_pi)|[<span data-ttu-id="97819-589">POWER</span><span class="sxs-lookup"><span data-stu-id="97819-589">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="97819-590">RADIANS</span><span class="sxs-lookup"><span data-stu-id="97819-590">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="97819-591">ROUND</span><span class="sxs-lookup"><span data-stu-id="97819-591">ROUND</span></span>](#bk_round)|[<span data-ttu-id="97819-592">SIN</span><span class="sxs-lookup"><span data-stu-id="97819-592">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="97819-593">SQRT</span><span class="sxs-lookup"><span data-stu-id="97819-593">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="97819-594">SQUARE</span><span class="sxs-lookup"><span data-stu-id="97819-594">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="97819-595">SIGN</span><span class="sxs-lookup"><span data-stu-id="97819-595">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="97819-596">TAN</span><span class="sxs-lookup"><span data-stu-id="97819-596">TAN</span></span>](#bk_tan)|[<span data-ttu-id="97819-597">TRUNC</span><span class="sxs-lookup"><span data-stu-id="97819-597">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="97819-598"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="97819-598"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="97819-599">Devuelve el valor absoluto (positivo) de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-599">Returns the absolute (positive) value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="97819-600">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-600">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-601">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-601">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-602">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-602">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-603">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-603">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-604">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-604">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-605">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-605">**Examples**</span></span>  
  
 <span data-ttu-id="97819-606">En el ejemplo siguiente se muestran los resultados de usar la función ABS en tres números distintos.</span><span class="sxs-lookup"><span data-stu-id="97819-606">The following example shows the results of using the ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="97819-607">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-607">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="97819-608"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="97819-608"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="97819-609">Devuelve el ángulo, en radianes, cuyo coseno es la expresión numérica especificada; también se denomina arcocoseno.</span><span class="sxs-lookup"><span data-stu-id="97819-609">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="97819-610">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-610">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-611">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-611">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-612">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-612">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-613">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-613">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-614">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-614">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-615">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-615">**Examples**</span></span>  
  
 <span data-ttu-id="97819-616">El siguiente ejemplo devuelve el arcocoseno de -1:</span><span class="sxs-lookup"><span data-stu-id="97819-616">The following example returns the ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="97819-617">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-617">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="97819-618"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="97819-618"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="97819-619">Devuelve el ángulo, en radianes, cuyo seno es la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-619">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="97819-620">También se denomina arcoseno.</span><span class="sxs-lookup"><span data-stu-id="97819-620">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="97819-621">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-621">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-622">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-622">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-623">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-623">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-624">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-624">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-625">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-625">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-626">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-626">**Examples**</span></span>  
  
 <span data-ttu-id="97819-627">El siguiente ejemplo devuelve el arcoseno de -1:</span><span class="sxs-lookup"><span data-stu-id="97819-627">The following example returns the ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="97819-628">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-628">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="97819-629"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="97819-629"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="97819-630">Devuelve el ángulo, en radianes, cuya tangente es la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-630">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="97819-631">También se denomina arcotangente.</span><span class="sxs-lookup"><span data-stu-id="97819-631">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="97819-632">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-632">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-633">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-633">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-634">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-634">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-635">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-635">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-636">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-636">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-637">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-637">**Examples**</span></span>  
  
 <span data-ttu-id="97819-638">El siguiente ejemplo devuelve la arcotangente del valor especificado.</span><span class="sxs-lookup"><span data-stu-id="97819-638">The following example returns the ATAN of the specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="97819-639">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-639">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="97819-640"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="97819-640"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="97819-641">Devuelve el valor principal de la arcotangente de y/x, expresado en radianes.</span><span class="sxs-lookup"><span data-stu-id="97819-641">Returns the principal value of the arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="97819-642">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-642">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="97819-643">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-643">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-644">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-644">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-645">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-645">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-646">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-646">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-647">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-647">**Examples**</span></span>  
  
 <span data-ttu-id="97819-648">En el siguiente ejemplo se calcula ATN2 para los componentes x e y especificados.</span><span class="sxs-lookup"><span data-stu-id="97819-648">The following example calculates the ATN2 for the specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="97819-649">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-649">Here is the result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="97819-650"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="97819-650"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="97819-651">Devuelve el valor entero más pequeño mayor o igual que la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-651">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span>  
  
 <span data-ttu-id="97819-652">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-652">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-653">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-653">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-654">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-654">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-655">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-655">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-656">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-656">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-657">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-657">**Examples**</span></span>  
  
 <span data-ttu-id="97819-658">En el ejemplo siguiente se muestran valores numéricos positivos, negativos y cero con la función CEILING.</span><span class="sxs-lookup"><span data-stu-id="97819-658">The following example shows positive numeric, negative, and zero values with the CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="97819-659">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-659">Here is the result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="97819-660"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="97819-660"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="97819-661">Devuelve el coseno trigonométrico del ángulo especificado, en radianes, en la expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-661">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="97819-662">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-662">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-663">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-663">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-664">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-664">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-665">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-665">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-666">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-666">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-667">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-667">**Examples**</span></span>  
  
 <span data-ttu-id="97819-668">En el ejemplo siguiente se calcula el coseno del ángulo especificado.</span><span class="sxs-lookup"><span data-stu-id="97819-668">The following example calculates the COS of the specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="97819-669">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-669">Here is the result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="97819-670"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="97819-670"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="97819-671">Devuelve la cotangente trigonométrica del ángulo especificado, en radianes, en la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-671">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span>  
  
 <span data-ttu-id="97819-672">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-672">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-673">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-673">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-674">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-674">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-675">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-675">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-676">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-676">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-677">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-677">**Examples**</span></span>  
  
 <span data-ttu-id="97819-678">En el ejemplo siguiente se calcula la cotangente del ángulo especificado.</span><span class="sxs-lookup"><span data-stu-id="97819-678">The following example calculates the COT of the specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="97819-679">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-679">Here is the result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="97819-680"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="97819-680"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="97819-681">Devuelve el ángulo correspondiente en grados de un ángulo especificado en radianes.</span><span class="sxs-lookup"><span data-stu-id="97819-681">Returns the corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="97819-682">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-682">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-683">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-683">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-684">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-684">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-685">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-685">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-686">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-686">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-687">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-687">**Examples**</span></span>  
  
 <span data-ttu-id="97819-688">En el ejemplo siguiente se devuelven los grados de un ángulo de pi/2 radianes.</span><span class="sxs-lookup"><span data-stu-id="97819-688">The following example returns the number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="97819-689">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-689">Here is the result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="97819-690"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="97819-690"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="97819-691">Devuelve el valor entero más grande menor o igual que la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-691">Returns the largest integer less than or equal to the specified numeric expression.</span></span>  
  
 <span data-ttu-id="97819-692">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-692">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-693">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-693">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-694">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-694">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-695">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-695">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-696">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-696">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-697">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-697">**Examples**</span></span>  
  
 <span data-ttu-id="97819-698">En el ejemplo siguiente se muestran valores numéricos positivos, negativos y cero con la función FLOOP.</span><span class="sxs-lookup"><span data-stu-id="97819-698">The following example shows positive numeric, negative, and zero values with the FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="97819-699">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-699">Here is the result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="97819-700"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="97819-700"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="97819-701">Devuelve el valor exponencial de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-701">Returns the exponential value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="97819-702">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-702">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-703">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-703">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-704">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-704">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-705">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-705">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-706">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-706">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-707">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="97819-707">**Remarks**</span></span>  
  
 <span data-ttu-id="97819-708">La constante **e** (2,718281 …) es la base de los logaritmos naturales.</span><span class="sxs-lookup"><span data-stu-id="97819-708">The constant **e** (2.718281…), is the base of natural logarithms.</span></span>  
  
 <span data-ttu-id="97819-709">El exponente de un número es la constante **e** elevada a la potencia del número.</span><span class="sxs-lookup"><span data-stu-id="97819-709">The exponent of a number is the constant **e** raised to the power of the number.</span></span> <span data-ttu-id="97819-710">Por ejemplo EXP(1,0) = e^1,0 = 2,718 281 828 459 05 y EXP(10) = e^10 = 22 026,465 794 806 7.</span><span class="sxs-lookup"><span data-stu-id="97819-710">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="97819-711">El valor exponencial del logaritmo natural de un número es el mismo número: EXP (LOG [n]) = n.</span><span class="sxs-lookup"><span data-stu-id="97819-711">The exponential of the natural logarithm of a number is the number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="97819-712">Y el logaritmo natural del valor exponencial de un número es el mismo número: LOG (EXP [n]) = n.</span><span class="sxs-lookup"><span data-stu-id="97819-712">And the natural logarithm of the exponential of a number is the number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="97819-713">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-713">**Examples**</span></span>  
  
 <span data-ttu-id="97819-714">En el ejemplo siguiente se declara una variable y se devuelve el valor exponencial de la variable especificada (10).</span><span class="sxs-lookup"><span data-stu-id="97819-714">The following example declares a variable and returns the exponential value of the specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="97819-715">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-715">Here is the result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="97819-716">En el ejemplo siguiente se devuelve el valor exponencial del logaritmo natural de 20 y el logaritmo natural del valor exponencial de 20.</span><span class="sxs-lookup"><span data-stu-id="97819-716">The following example returns the exponential value of the natural logarithm of 20 and the natural logarithm of the exponential of 20.</span></span> <span data-ttu-id="97819-717">Dado que estas funciones son inversas entre sí, el valor devuelto con redondeo para las operaciones matemáticas de punto flotante en ambos casos es 20.</span><span class="sxs-lookup"><span data-stu-id="97819-717">Because these functions are inverse functions of one another, the return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="97819-718">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-718">Here is the result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="97819-719"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="97819-719"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="97819-720">Devuelve el algoritmo natural de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-720">Returns the natural logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="97819-721">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-721">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="97819-722">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-722">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-723">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-723">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="97819-724">Argumento numérico opcional que establece la base del logaritmo.</span><span class="sxs-lookup"><span data-stu-id="97819-724">Optional numeric argument that sets the base for the logarithm.</span></span>  
  
 <span data-ttu-id="97819-725">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-725">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-726">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-726">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-727">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="97819-727">**Remarks**</span></span>  
  
 <span data-ttu-id="97819-728">De forma predeterminada, LOG() devuelve el logaritmo natural.</span><span class="sxs-lookup"><span data-stu-id="97819-728">By default, LOG() returns the natural logarithm.</span></span> <span data-ttu-id="97819-729">Puede cambiar la base del logaritmo a otro valor mediante el parámetro base opcional.</span><span class="sxs-lookup"><span data-stu-id="97819-729">You can change the base of the logarithm to another value by using the optional base parameter.</span></span>  
  
 <span data-ttu-id="97819-730">El logaritmo natural es el logaritmo en base **e**, donde **e** es una constante irracional aproximadamente igual a 2,718 281 828.</span><span class="sxs-lookup"><span data-stu-id="97819-730">The natural logarithm is the logarithm to the base **e**, where **e** is an irrational constant approximately equal to 2.718281828.</span></span>  
  
 <span data-ttu-id="97819-731">El logaritmo natural del valor exponencial de un número es el mismo número: LOG (EXP [n]) = n.</span><span class="sxs-lookup"><span data-stu-id="97819-731">The natural logarithm of the exponential of a number is the number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="97819-732">Y el valor exponencial del logaritmo natural de un número es el mismo número: EXP (LOG [n]) = n.</span><span class="sxs-lookup"><span data-stu-id="97819-732">And the exponential of the natural logarithm of a number is the number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="97819-733">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-733">**Examples**</span></span>  
  
 <span data-ttu-id="97819-734">En el ejemplo siguiente se declara una variable y se devuelve el valor logarítmico de la variable especificada (10).</span><span class="sxs-lookup"><span data-stu-id="97819-734">The following example declares a variable and returns the logarithm value of the specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="97819-735">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-735">Here is the result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="97819-736">En el ejemplo siguiente se calcula el logaritmo del exponente de un número.</span><span class="sxs-lookup"><span data-stu-id="97819-736">The following example calculates the LOG for the exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="97819-737">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-737">Here is the result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="97819-738"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="97819-738"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="97819-739">Devuelve el logaritmo de base 10 de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-739">Returns the base-10 logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="97819-740">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-740">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-741">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-741">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-742">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-742">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-743">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-743">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-744">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-744">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-745">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="97819-745">**Remarks**</span></span>  
  
 <span data-ttu-id="97819-746">Las funciones LOG10 y POWER tienen una relación inversa.</span><span class="sxs-lookup"><span data-stu-id="97819-746">The LOG10 and POWER functions are inversely related to one another.</span></span> <span data-ttu-id="97819-747">Por ejemplo, 10 ^ LOG10 (n) = n.</span><span class="sxs-lookup"><span data-stu-id="97819-747">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="97819-748">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-748">**Examples**</span></span>  
  
 <span data-ttu-id="97819-749">En el ejemplo siguiente se declara una variable y se devuelve el valor de LOG10 de la variable especificada (100).</span><span class="sxs-lookup"><span data-stu-id="97819-749">The following example declares a variable and returns the LOG10 value of the specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="97819-750">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-750">Here is the result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="97819-751"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="97819-751"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="97819-752">Devuelve el valor constante de PI.</span><span class="sxs-lookup"><span data-stu-id="97819-752">Returns the constant value of PI.</span></span>  
  
 <span data-ttu-id="97819-753">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-753">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="97819-754">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-754">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-755">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-755">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-756">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-756">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-757">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-757">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-758">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-758">**Examples**</span></span>  
  
 <span data-ttu-id="97819-759">El siguiente ejemplo devuelve el valor de pi.</span><span class="sxs-lookup"><span data-stu-id="97819-759">The following example returns the value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="97819-760">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-760">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="97819-761"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="97819-761"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="97819-762">Devuelve el valor de la expresión especificada a la potencia especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-762">Returns the value of the specified expression to the specified power.</span></span>  
  
 <span data-ttu-id="97819-763">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-763">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="97819-764">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-764">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-765">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-765">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="97819-766">Es la potencia a la que se eleva `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="97819-766">Is the power to which to raise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="97819-767">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-767">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-768">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-768">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-769">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-769">**Examples**</span></span>  
  
 <span data-ttu-id="97819-770">En el ejemplo siguiente se muestra cómo elevar un número a la potencia de 3 (el cubo del número).</span><span class="sxs-lookup"><span data-stu-id="97819-770">The following example demonstrates raising a number to the power of 3 (the cube of the number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="97819-771">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-771">Here is the result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="97819-772"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="97819-772"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="97819-773">Devuelve radianes cuando se especifica una expresión numérica en grados.</span><span class="sxs-lookup"><span data-stu-id="97819-773">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="97819-774">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-774">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-775">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-775">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-776">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-776">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-777">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-777">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-778">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-778">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-779">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-779">**Examples**</span></span>  
  
 <span data-ttu-id="97819-780">En el ejemplo siguiente se toman unos ángulos como entrada y se devuelven sus correspondientes valores en radianes.</span><span class="sxs-lookup"><span data-stu-id="97819-780">The following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="97819-781">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-781">Here is the result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="97819-782"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="97819-782"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="97819-783">Devuelve un valor numérico, redondeado al valor entero más cercano.</span><span class="sxs-lookup"><span data-stu-id="97819-783">Returns a numeric value, rounded to the closest integer value.</span></span>  
  
 <span data-ttu-id="97819-784">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-784">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-785">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-785">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-786">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-786">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-787">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-787">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-788">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-788">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-789">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-789">**Examples**</span></span>  
  
 <span data-ttu-id="97819-790">En el ejemplo siguiente se redondean los siguientes números positivos y negativos al entero más próximo.</span><span class="sxs-lookup"><span data-stu-id="97819-790">The following example rounds the following positive and negative numbers to the nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="97819-791">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-791">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="97819-792"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="97819-792"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="97819-793">Devuelve el signo positivo (+1), cero (0) o negativo (-1) de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-793">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="97819-794">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-794">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-795">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-795">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-796">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-796">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-797">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-797">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-798">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-798">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-799">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-799">**Examples**</span></span>  
  
 <span data-ttu-id="97819-800">En el ejemplo siguiente se devuelven los valores del signo de números entre -2 y 2.</span><span class="sxs-lookup"><span data-stu-id="97819-800">The following example returns the SIGN values of numbers from -2 to 2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="97819-801">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-801">Here is the result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="97819-802"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="97819-802"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="97819-803">Devuelve el seno trigonométrico del ángulo especificado, en radianes, en la expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-803">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="97819-804">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-804">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-805">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-805">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-806">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-806">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-807">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-807">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-808">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-808">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-809">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-809">**Examples**</span></span>  
  
 <span data-ttu-id="97819-810">En el ejemplo siguiente se calcula el seno del ángulo especificado.</span><span class="sxs-lookup"><span data-stu-id="97819-810">The following example calculates the SIN of the specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="97819-811">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-811">Here is the result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="97819-812"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="97819-812"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="97819-813">Devuelve la raíz cuadrada del valor numérico especificado.</span><span class="sxs-lookup"><span data-stu-id="97819-813">Returns the square root of the specified numeric value.</span></span>  
  
 <span data-ttu-id="97819-814">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-814">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-815">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-815">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-816">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-816">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-817">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-817">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-818">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-818">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-819">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-819">**Examples**</span></span>  
  
 <span data-ttu-id="97819-820">En el ejemplo siguiente se devuelven las raíces cuadradas de los números 1-3.</span><span class="sxs-lookup"><span data-stu-id="97819-820">The following example returns the square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="97819-821">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-821">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="97819-822"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="97819-822"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="97819-823">Devuelve el cuadrado del valor numérico especificado.</span><span class="sxs-lookup"><span data-stu-id="97819-823">Returns the square of the specified numeric value.</span></span>  
  
 <span data-ttu-id="97819-824">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-824">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-825">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-825">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-826">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-826">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-827">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-827">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-828">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-828">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-829">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-829">**Examples**</span></span>  
  
 <span data-ttu-id="97819-830">En el ejemplo siguiente se devuelven los cuadrados de los números 1-3.</span><span class="sxs-lookup"><span data-stu-id="97819-830">The following example returns the squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="97819-831">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-831">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="97819-832"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="97819-832"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="97819-833">Devuelve la tangente del ángulo especificado, en radianes, en la expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-833">Returns the tangent of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="97819-834">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-834">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-835">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-835">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-836">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-836">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-837">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-837">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-838">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-838">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-839">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-839">**Examples**</span></span>  
  
 <span data-ttu-id="97819-840">En el ejemplo siguiente se calcula la tangente de pi()/2.</span><span class="sxs-lookup"><span data-stu-id="97819-840">The following example calculates the tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="97819-841">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-841">Here is the result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="97819-842"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="97819-842"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="97819-843">Devuelve un valor numérico, truncado al valor entero más cercano.</span><span class="sxs-lookup"><span data-stu-id="97819-843">Returns a numeric value, truncated to the closest integer value.</span></span>  
  
 <span data-ttu-id="97819-844">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-844">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="97819-845">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-845">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="97819-846">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-846">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-847">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-847">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-848">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-848">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-849">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-849">**Examples**</span></span>  
  
 <span data-ttu-id="97819-850">En el ejemplo siguiente se truncan los siguientes números positivos y negativos al valor entero más próximo.</span><span class="sxs-lookup"><span data-stu-id="97819-850">The following example truncates the following positive and negative numbers to the nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="97819-851">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-851">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="97819-852"><a name="bk_type_checking_functions"></a> Funciones de comprobación de tipos</span><span class="sxs-lookup"><span data-stu-id="97819-852"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="97819-853">Las siguientes funciones admiten la comprobación de tipos de valores de entrada y devuelven un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-853">The following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="97819-854">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="97819-854">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="97819-855">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="97819-855">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="97819-856">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="97819-856">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="97819-857">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="97819-857">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="97819-858">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="97819-858">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="97819-859">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="97819-859">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="97819-860">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="97819-860">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="97819-861">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="97819-861">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="97819-862"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="97819-862"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="97819-863">Devuelve un valor booleano que indica si el tipo de la expresión especificada es una matriz.</span><span class="sxs-lookup"><span data-stu-id="97819-863">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span>  
  
 <span data-ttu-id="97819-864">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-864">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="97819-865">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-865">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="97819-866">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="97819-866">Is any valid expression.</span></span>  
  
 <span data-ttu-id="97819-867">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-867">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-868">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-868">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-869">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-869">**Examples**</span></span>  
  
 <span data-ttu-id="97819-870">En el ejemplo siguiente se comprueban objetos de los tipos JSON Boolean, number, string, null, object, array y undefined, mediante la función IS_ARRAY.</span><span class="sxs-lookup"><span data-stu-id="97819-870">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_ARRAY function.</span></span>  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="97819-871">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-871">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="97819-872"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="97819-872"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="97819-873">Devuelve un valor booleano que indica si el tipo de la expresión especificada es un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-873">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="97819-874">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-874">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="97819-875">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-875">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="97819-876">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="97819-876">Is any valid expression.</span></span>  
  
 <span data-ttu-id="97819-877">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-877">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-878">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-878">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-879">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-879">**Examples**</span></span>  
  
 <span data-ttu-id="97819-880">En el ejemplo siguiente se comprueban objetos de los tipos JSON Boolean, number, string, null, object, array y undefined, mediante la función IS_BOOL.</span><span class="sxs-lookup"><span data-stu-id="97819-880">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_BOOL function.</span></span>  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="97819-881">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-881">Here is the result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="97819-882"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="97819-882"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="97819-883">Devuelve un valor booleano que indica si se ha asignado un valor a la propiedad.</span><span class="sxs-lookup"><span data-stu-id="97819-883">Returns a Boolean indicating if the property has been assigned a value.</span></span>  
  
 <span data-ttu-id="97819-884">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-884">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="97819-885">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-885">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="97819-886">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="97819-886">Is any valid expression.</span></span>  
  
 <span data-ttu-id="97819-887">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-887">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-888">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-888">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-889">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-889">**Examples**</span></span>  
  
 <span data-ttu-id="97819-890">En el ejemplo siguiente se comprueba la presencia de una propiedad en el documento JSON especificado.</span><span class="sxs-lookup"><span data-stu-id="97819-890">The following example checks for the presence of a property within the specified JSON document.</span></span> <span data-ttu-id="97819-891">En el primer caso se devuelve true, ya que "a" está presente, pero en el segundo, false, ya que "b" no lo está.</span><span class="sxs-lookup"><span data-stu-id="97819-891">The first returns true since "a" is present, but the second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="97819-892">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-892">Here is the result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="97819-893"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="97819-893"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="97819-894">Devuelve un valor booleano que indica si el tipo de la expresión especificada es nulo.</span><span class="sxs-lookup"><span data-stu-id="97819-894">Returns a Boolean value indicating if the type of the specified expression is null.</span></span>  
  
 <span data-ttu-id="97819-895">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-895">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="97819-896">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-896">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="97819-897">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="97819-897">Is any valid expression.</span></span>  
  
 <span data-ttu-id="97819-898">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-898">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-899">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-899">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-900">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-900">**Examples**</span></span>  
  
 <span data-ttu-id="97819-901">En el ejemplo siguiente se comprueban objetos de los tipos JSON Boolean, number, string, null, object, array y undefined, mediante la función IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="97819-901">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="97819-902">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-902">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="97819-903"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="97819-903"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="97819-904">Devuelve un valor booleano que indica si el tipo de la expresión especificada es un número.</span><span class="sxs-lookup"><span data-stu-id="97819-904">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span>  
  
 <span data-ttu-id="97819-905">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-905">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="97819-906">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-906">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="97819-907">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="97819-907">Is any valid expression.</span></span>  
  
 <span data-ttu-id="97819-908">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-908">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-909">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-909">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-910">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-910">**Examples**</span></span>  
  
 <span data-ttu-id="97819-911">En el ejemplo siguiente se comprueban objetos de los tipos JSON Boolean, number, string, null, object, array y undefined, mediante la función IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="97819-911">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="97819-912">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-912">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="97819-913"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="97819-913"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="97819-914">Devuelve un valor booleano que indica si el tipo de la expresión especificada es un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="97819-914">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="97819-915">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-915">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="97819-916">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-916">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="97819-917">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="97819-917">Is any valid expression.</span></span>  
  
 <span data-ttu-id="97819-918">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-918">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-919">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-919">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-920">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-920">**Examples**</span></span>  
  
 <span data-ttu-id="97819-921">En el ejemplo siguiente se comprueban objetos de los tipos JSON Boolean, number, string, null, object, array y undefined, mediante la función IS_OBJECT.</span><span class="sxs-lookup"><span data-stu-id="97819-921">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_OBJECT function.</span></span>  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="97819-922">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-922">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="97819-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="97819-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="97819-924">Devuelve un valor booleano que indica si el tipo de la expresión especificada es primitivo (cadena, booleano, numérico o nulo).</span><span class="sxs-lookup"><span data-stu-id="97819-924">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="97819-925">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-925">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="97819-926">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-926">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="97819-927">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="97819-927">Is any valid expression.</span></span>  
  
 <span data-ttu-id="97819-928">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-928">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-929">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-929">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-930">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-930">**Examples**</span></span>  
  
 <span data-ttu-id="97819-931">En el ejemplo siguiente se comprueban los objetos de los tipos JSON Boolean, number, string, null, object, array y undefined, mediante la función IS_PRIMITIVE.</span><span class="sxs-lookup"><span data-stu-id="97819-931">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_PRIMITIVE function.</span></span>  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="97819-932">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-932">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="97819-933"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="97819-933"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="97819-934">Devuelve un valor booleano que indica si el tipo de la expresión especificada es una cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-934">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span>  
  
 <span data-ttu-id="97819-935">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-935">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="97819-936">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-936">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="97819-937">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="97819-937">Is any valid expression.</span></span>  
  
 <span data-ttu-id="97819-938">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-938">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-939">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-939">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-940">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-940">**Examples**</span></span>  
  
 <span data-ttu-id="97819-941">En el ejemplo siguiente se comprueban objetos de los tipos JSON Boolean, number, string, null, object, array y undefined, mediante la función IS_STRING.</span><span class="sxs-lookup"><span data-stu-id="97819-941">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_STRING function.</span></span>  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="97819-942">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-942">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="97819-943"><a name="bk_string_functions"></a> Funciones de cadena</span><span class="sxs-lookup"><span data-stu-id="97819-943"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="97819-944">Las siguientes funciones escalares realizan una operación sobre un valor de entrada de cadena y devuelven una cadena, un valor numérico o un booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-944">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="97819-945">CONCAT</span><span class="sxs-lookup"><span data-stu-id="97819-945">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="97819-946">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="97819-946">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="97819-947">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="97819-947">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="97819-948">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="97819-948">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="97819-949">LEFT</span><span class="sxs-lookup"><span data-stu-id="97819-949">LEFT</span></span>](#bk_left)|[<span data-ttu-id="97819-950">LENGTH</span><span class="sxs-lookup"><span data-stu-id="97819-950">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="97819-951">LOWER</span><span class="sxs-lookup"><span data-stu-id="97819-951">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="97819-952">LTRIM</span><span class="sxs-lookup"><span data-stu-id="97819-952">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="97819-953">REPLACE</span><span class="sxs-lookup"><span data-stu-id="97819-953">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="97819-954">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="97819-954">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="97819-955">REVERSE</span><span class="sxs-lookup"><span data-stu-id="97819-955">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="97819-956">RIGHT</span><span class="sxs-lookup"><span data-stu-id="97819-956">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="97819-957">RTRIM</span><span class="sxs-lookup"><span data-stu-id="97819-957">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="97819-958">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="97819-958">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="97819-959">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="97819-959">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="97819-960">UPPER</span><span class="sxs-lookup"><span data-stu-id="97819-960">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="97819-961"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="97819-961"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="97819-962">Devuelve una cadena que es el resultado de concatenar dos o más valores de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-962">Returns a string that is the result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="97819-963">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-963">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="97819-964">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-964">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-965">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-965">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-966">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-966">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-967">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-967">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-968">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-968">**Examples**</span></span>  
  
 <span data-ttu-id="97819-969">El siguiente ejemplo devuelve la cadena concatenada de los valores especificados.</span><span class="sxs-lookup"><span data-stu-id="97819-969">The following example returns the concatenated string of the specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="97819-970">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-970">Here is the result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="97819-971"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="97819-971"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="97819-972">Devuelve un valor booleano que indica si la primera expresión de cadena contiene la segunda.</span><span class="sxs-lookup"><span data-stu-id="97819-972">Returns a Boolean indicating whether the first string expression contains the second.</span></span>  
  
 <span data-ttu-id="97819-973">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-973">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="97819-974">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-974">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-975">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-975">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-976">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-976">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-977">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-977">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-978">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-978">**Examples**</span></span>  
  
 <span data-ttu-id="97819-979">En el ejemplo siguiente se comprueba si "abc" contiene "ab" y contiene "d".</span><span class="sxs-lookup"><span data-stu-id="97819-979">The following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="97819-980">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-980">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="97819-981"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="97819-981"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="97819-982">Devuelve un valor booleano que indica si la primera expresión de cadena finaliza con la segunda.</span><span class="sxs-lookup"><span data-stu-id="97819-982">Returns a Boolean indicating whether the first string expression ends with the second.</span></span>  
  
 <span data-ttu-id="97819-983">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-983">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="97819-984">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-984">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-985">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-985">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-986">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-986">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-987">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-987">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-988">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-988">**Examples**</span></span>  
  
 <span data-ttu-id="97819-989">El siguiente ejemplo devuelve las terminaciones "b" y "bc"de "abc".</span><span class="sxs-lookup"><span data-stu-id="97819-989">The following example returns the "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="97819-990">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-990">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="97819-991"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="97819-991"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="97819-992">Devuelve la posición inicial de la primera aparición de la expresión de la segunda cadena dentro de la primera expresión de cadena especificada, o -1 si no se encuentra la cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-992">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>  
  
 <span data-ttu-id="97819-993">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-993">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="97819-994">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-994">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-995">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-995">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-996">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-996">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-997">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-997">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-998">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-998">**Examples**</span></span>  
  
 <span data-ttu-id="97819-999">En el ejemplo siguiente se devuelve el índice de varias subcadenas dentro de "abc".</span><span class="sxs-lookup"><span data-stu-id="97819-999">The following example returns the index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="97819-1000">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1000">Here is the result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="97819-1001"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="97819-1001"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="97819-1002">Devuelve la parte izquierda de una cadena con el número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="97819-1002">Returns the left part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="97819-1003">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1003">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="97819-1004">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1004">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1005">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1005">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="97819-1006">Es cualquier expresión numérica válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1006">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="97819-1007">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1007">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1008">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1008">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-1009">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1009">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1010">En el ejemplo siguiente se devuelve la parte izquierda de "abc" para distintos valores de longitud.</span><span class="sxs-lookup"><span data-stu-id="97819-1010">The following example returns the left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="97819-1011">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1011">Here is the result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="97819-1012"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="97819-1012"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="97819-1013">Devuelve el número de caracteres de la expresión de cadena especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-1013">Returns the number of characters of the specified string expression.</span></span>  
  
 <span data-ttu-id="97819-1014">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1014">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="97819-1015">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1015">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1016">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1016">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-1017">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1017">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1018">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1018">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-1019">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1019">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1020">En el ejemplo siguiente se devuelve la longitud de una cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1020">The following example returns the length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="97819-1021">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1021">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="97819-1022"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="97819-1022"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="97819-1023">Devuelve una expresión de cadena después de convertir los datos de caracteres en mayúsculas a minúsculas.</span><span class="sxs-lookup"><span data-stu-id="97819-1023">Returns a string expression after converting uppercase character data to lowercase.</span></span>  
  
 <span data-ttu-id="97819-1024">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1024">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="97819-1025">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1025">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1026">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1026">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-1027">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1027">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1028">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1028">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-1029">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1029">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1030">En el ejemplo siguiente se muestra cómo utilizar LOWER en una consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-1030">The following example shows how to use LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="97819-1031">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1031">Here is the result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="97819-1032"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="97819-1032"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="97819-1033">Devuelve una expresión de cadena después de quitar los espacios en blanco iniciales.</span><span class="sxs-lookup"><span data-stu-id="97819-1033">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="97819-1034">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1034">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="97819-1035">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1035">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1036">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1036">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-1037">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1037">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1038">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1038">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-1039">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1039">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1040">En el ejemplo siguiente se muestra cómo utilizar LTRIM en una consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-1040">The following example shows how to use LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="97819-1041">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1041">Here is the result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="97819-1042"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="97819-1042"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="97819-1043">Reemplaza todas las apariciones de un valor de cadena especificado por otro valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1043">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="97819-1044">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1044">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="97819-1045">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1045">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1046">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1046">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-1047">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1047">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1048">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1048">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-1049">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1049">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1050">En el ejemplo siguiente se muestra cómo utilizar REPLACE en una consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-1050">The following example shows how to use REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="97819-1051">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1051">Here is the result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="97819-1052"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="97819-1052"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="97819-1053">Repite un valor de cadena un número especificado de veces.</span><span class="sxs-lookup"><span data-stu-id="97819-1053">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="97819-1054">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1054">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="97819-1055">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1055">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1056">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1056">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="97819-1057">Es cualquier expresión numérica válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1057">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="97819-1058">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1058">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1059">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1059">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-1060">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1060">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1061">En el ejemplo siguiente se muestra cómo utilizar REPLICATE en una consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-1061">The following example shows how to use REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="97819-1062">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1062">Here is the result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="97819-1063"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="97819-1063"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="97819-1064">Devuelve el orden inverso de un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1064">Returns the reverse order of a string value.</span></span>  
  
 <span data-ttu-id="97819-1065">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1065">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="97819-1066">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1066">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1067">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1067">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-1068">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1068">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1069">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1069">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-1070">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1070">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1071">En el ejemplo siguiente se muestra cómo utilizar REVERSE en una consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-1071">The following example shows how to use REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="97819-1072">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1072">Here is the result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="97819-1073"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="97819-1073"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="97819-1074">Devuelve la parte derecha de una cadena con el número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="97819-1074">Returns the right part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="97819-1075">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1075">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="97819-1076">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1076">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1077">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1077">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="97819-1078">Es cualquier expresión numérica válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1078">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="97819-1079">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1079">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1080">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1080">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-1081">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1081">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1082">En el ejemplo siguiente se devuelve la parte derecha de "abc" para distintos valores de longitud.</span><span class="sxs-lookup"><span data-stu-id="97819-1082">The following example returns the right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="97819-1083">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1083">Here is the result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="97819-1084"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="97819-1084"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="97819-1085">Devuelve una expresión de cadena después de quitar los espacios en blanco finales.</span><span class="sxs-lookup"><span data-stu-id="97819-1085">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="97819-1086">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1086">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="97819-1087">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1087">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1088">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1088">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-1089">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1089">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1090">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1090">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-1091">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1091">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1092">En el ejemplo siguiente se muestra cómo utilizar RTRIM en una consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-1092">The following example shows how to use RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="97819-1093">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1093">Here is the result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="97819-1094"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="97819-1094"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="97819-1095">Devuelve un valor booleano que indica si la primera expresión de cadena empieza con la segunda.</span><span class="sxs-lookup"><span data-stu-id="97819-1095">Returns a Boolean indicating whether the first string expression starts with the second.</span></span>  
  
 <span data-ttu-id="97819-1096">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1096">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="97819-1097">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1097">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1098">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1098">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-1099">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1099">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1100">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-1100">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-1101">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1101">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1102">En el ejemplo siguiente se comprueba si la cadena "abc" empieza por "b" y "a".</span><span class="sxs-lookup"><span data-stu-id="97819-1102">The following example checks if the string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="97819-1103">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1103">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="97819-1104"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="97819-1104"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="97819-1105">Devuelve parte de una expresión de cadena a partir de la posición de base cero del carácter especificado y continúa hasta la longitud especificada, o hasta el final de la cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1105">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span>  
  
 <span data-ttu-id="97819-1106">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1106">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="97819-1107">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1107">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1108">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1108">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="97819-1109">Es cualquier expresión numérica válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1109">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="97819-1110">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1110">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1111">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1111">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-1112">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1112">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1113">En el ejemplo siguiente se devuelve la subcadena de "abc" que empieza por 1 y tiene una longitud de 1 carácter.</span><span class="sxs-lookup"><span data-stu-id="97819-1113">The following example returns the substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="97819-1114">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1114">Here is the result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="97819-1115"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="97819-1115"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="97819-1116">Devuelve una expresión de cadena después de convertir datos de caracteres en minúsculas a mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="97819-1116">Returns a string expression after converting lowercase character data to uppercase.</span></span>  
  
 <span data-ttu-id="97819-1117">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1117">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="97819-1118">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1118">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="97819-1119">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1119">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="97819-1120">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1120">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1121">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1121">Returns a string expression.</span></span>  
  
 <span data-ttu-id="97819-1122">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1122">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1123">En el ejemplo siguiente se muestra cómo utilizar UPPER en una consulta.</span><span class="sxs-lookup"><span data-stu-id="97819-1123">The following example shows how to use UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="97819-1124">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1124">Here is the result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="97819-1125"><a name="bk_array_functions"></a> Funciones de matriz</span><span class="sxs-lookup"><span data-stu-id="97819-1125"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="97819-1126">Las siguientes funciones escalares realizan una operación en un valor de entrada de matriz y devuelven un valor numérico, booleano o de matriz.</span><span class="sxs-lookup"><span data-stu-id="97819-1126">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="97819-1127">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="97819-1127">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="97819-1128">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="97819-1128">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="97819-1129">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="97819-1129">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="97819-1130">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="97819-1130">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="97819-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="97819-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="97819-1132">Devuelve una matriz que es el resultado de concatenar dos o más valores de la matriz.</span><span class="sxs-lookup"><span data-stu-id="97819-1132">Returns an array that is the result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="97819-1133">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1133">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="97819-1134">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1134">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="97819-1135">Es cualquier expresión de matriz válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1135">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="97819-1136">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1136">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1137">Devuelve una expresión de matriz.</span><span class="sxs-lookup"><span data-stu-id="97819-1137">Returns an array expression.</span></span>  
  
 <span data-ttu-id="97819-1138">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1138">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1139">En el ejemplo siguiente se muestra cómo concatenar dos matrices.</span><span class="sxs-lookup"><span data-stu-id="97819-1139">The following example how to concatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="97819-1140">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1140">Here is the result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="97819-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="97819-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="97819-1142">Devuelve un valor booleano que indica si la matriz contiene el valor especificado.</span><span class="sxs-lookup"><span data-stu-id="97819-1142">Returns a Boolean indicating whether the array contains the specified value.</span></span>  
  
 <span data-ttu-id="97819-1143">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1143">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="97819-1144">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1144">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="97819-1145">Es cualquier expresión de matriz válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1145">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="97819-1146">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1146">Is any valid expression.</span></span>  
  
 <span data-ttu-id="97819-1147">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1147">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1148">Devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-1148">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="97819-1149">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1149">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1150">En el siguiente ejemplo se muestra cómo comprobar la pertenencia a una matriz con ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="97819-1150">The following example how to check for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="97819-1151">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1151">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="97819-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="97819-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="97819-1153">Devuelve el número de elementos de la expresión de matriz especificada.</span><span class="sxs-lookup"><span data-stu-id="97819-1153">Returns the number of elements of the specified array expression.</span></span>  
  
 <span data-ttu-id="97819-1154">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1154">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="97819-1155">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1155">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="97819-1156">Es cualquier expresión de matriz válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1156">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="97819-1157">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1157">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1158">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="97819-1158">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="97819-1159">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1159">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1160">En el siguiente ejemplo se muestra cómo obtener la longitud de una matriz con ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="97819-1160">The following example how to get the length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="97819-1161">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1161">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="97819-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="97819-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="97819-1163">Devuelve parte de una expresión de matriz.</span><span class="sxs-lookup"><span data-stu-id="97819-1163">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="97819-1164">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1164">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="97819-1165">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1165">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="97819-1166">Es cualquier expresión de matriz válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1166">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="97819-1167">Es cualquier expresión numérica válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1167">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="97819-1168">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1168">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1169">Devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-1169">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="97819-1170">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1170">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1171">En el siguiente ejemplo se muestra cómo obtener una parte de una matriz con ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="97819-1171">The following example how to get a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="97819-1172">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1172">Here is the result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="97819-1173"><a name="bk_spatial_functions"></a> Funciones espaciales</span><span class="sxs-lookup"><span data-stu-id="97819-1173"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="97819-1174">Las siguientes funciones escalares realizan una operación en un valor de entrada de objeto espacial y devuelven un valor numérico o un booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-1174">The following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="97819-1175">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="97819-1175">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="97819-1176">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="97819-1176">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="97819-1177">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="97819-1177">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="97819-1178">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="97819-1178">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="97819-1179">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="97819-1179">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="97819-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="97819-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="97819-1181">Devuelve la distancia entre dos expresiones Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="97819-1181">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="97819-1182">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1182">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="97819-1183">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1183">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="97819-1184">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="97819-1184">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="97819-1185">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1185">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1186">Devuelve una expresión numérica con la distancia,</span><span class="sxs-lookup"><span data-stu-id="97819-1186">Returns a numeric expression containing the distance.</span></span> <span data-ttu-id="97819-1187">que se expresa en metros para el sistema de referencia predeterminado.</span><span class="sxs-lookup"><span data-stu-id="97819-1187">This is expressed in meters for the default reference system.</span></span>  
  
 <span data-ttu-id="97819-1188">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1188">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1189">En el siguiente ejemplo se muestra cómo se devuelven todos los documentos de la familia en un radio de 30 km a partir de la ubicación especificada mediante la función integrada ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="97819-1189">The following example shows how to return all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> <span data-ttu-id="97819-1190">.</span><span class="sxs-lookup"><span data-stu-id="97819-1190">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="97819-1191">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1191">Here is the result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="97819-1192"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="97819-1192"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="97819-1193">Devuelve una expresión condicional que indica si el objeto de GeoJSON (Point, Polygon o LineString) especificado en el primer argumento se encuentra en el objeto de GeoJSON (Point, Polygon o LineString) del segundo.</span><span class="sxs-lookup"><span data-stu-id="97819-1193">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument is within the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="97819-1194">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1194">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="97819-1195">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1195">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="97819-1196">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="97819-1196">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="97819-1197">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="97819-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="97819-1198">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1198">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1199">Devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-1199">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="97819-1200">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1200">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1201">En el ejemplo siguiente se muestra cómo buscar todos los documentos de la familia en un polígono con ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="97819-1201">The following example shows how to find all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="97819-1202">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1202">Here is the result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="97819-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="97819-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="97819-1204">Devuelve una expresión condicional que indica si el objeto de GeoJSON (Point, Polygon o LineString) especificado en el primer argumento forma intersección con el objeto de GeoJSON (Point, Polygon o LineString) del segundo.</span><span class="sxs-lookup"><span data-stu-id="97819-1204">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument intersects the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="97819-1205">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1205">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="97819-1206">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1206">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="97819-1207">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="97819-1207">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="97819-1208">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="97819-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="97819-1209">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1209">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1210">Devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="97819-1210">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="97819-1211">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1211">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1212">En el siguiente ejemplo se muestra cómo buscar todas las áreas de intersección con el polígono indicado.</span><span class="sxs-lookup"><span data-stu-id="97819-1212">The following example shows how to find all areas that intersects with the given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="97819-1213">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1213">Here is the result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="97819-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="97819-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="97819-1215">Devuelve un valor booleano que indica si la expresión de Point, Polygon o LineString de GeoJSON especificada es válida.</span><span class="sxs-lookup"><span data-stu-id="97819-1215">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="97819-1216">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1216">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="97819-1217">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1217">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="97819-1218">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="97819-1218">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="97819-1219">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1219">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1220">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="97819-1220">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="97819-1221">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1221">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1222">En el ejemplo siguiente se muestra cómo comprobar si un punto es válido con ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="97819-1222">The following example shows how to check if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="97819-1223">Por ejemplo, este punto tiene un valor de latitud que no está en el intervalo válido de valores [-90, 90], por lo que la consulta devuelve false.</span><span class="sxs-lookup"><span data-stu-id="97819-1223">For example, this point has a latitude value that's not in the valid range of values [-90, 90], so the query returns false.</span></span>  
  
 <span data-ttu-id="97819-1224">Para los polígonos, la especificación de GeoJSON requiere que el último par de coordenadas indicado sea igual que el primero, para crear una forma cerrada.</span><span class="sxs-lookup"><span data-stu-id="97819-1224">For polygons, the GeoJSON specification requires that the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span> <span data-ttu-id="97819-1225">El orden de los puntos dentro de un polígono debe especificarse siguiendo el sentido contrario al de las agujas del reloj.</span><span class="sxs-lookup"><span data-stu-id="97819-1225">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="97819-1226">Un polígono cuyos puntos se hayan especificado en el sentido de las agujas del reloj representa el inverso de la región dentro de él.</span><span class="sxs-lookup"><span data-stu-id="97819-1226">A polygon specified in clockwise order represents the inverse of the region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="97819-1227">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1227">Here is the result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="97819-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="97819-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="97819-1229">Devuelve un valor JSON que contiene un valor booleano si la expresión de Point, Polygon o LineString de GeoJSON especificada es válida; si no es válida, devuelve también el motivo como un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1229">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="97819-1230">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="97819-1230">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="97819-1231">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="97819-1231">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="97819-1232">Es cualquier expresión válida de objeto Point o Polygon de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="97819-1232">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="97819-1233">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="97819-1233">**Return Types**</span></span>  
  
 <span data-ttu-id="97819-1234">Devuelve un valor JSON que contiene un valor booleano si la expresión de punto o polígono GeoJSON especificada es válida; si no es válida, devuelve también el motivo en forma de valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="97819-1234">Returns a JSON value containing a Boolean value if the specified GeoJSON point or polygon expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="97819-1235">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="97819-1235">**Examples**</span></span>  
  
 <span data-ttu-id="97819-1236">En el siguiente ejemplo se muestra cómo comprobar la validez (con detalles) mediante ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="97819-1236">The following example how to check validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="97819-1237">El conjunto de resultados es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="97819-1237">Here is the result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a polygon must have the same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="97819-1238">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97819-1238">Next steps</span></span>  
 <span data-ttu-id="97819-1239">[Sintaxis SQL y consulta SQL para Azure Cosmos DB](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="97819-1239">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="97819-1240">Documentación sobre Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="97819-1240">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
