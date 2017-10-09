---
<span data-ttu-id="11a3f-101">título: aaa "API de documentos de base de datos de Azure Cosmos: sintaxis SQL | Descripción de Microsoft Docs": hacer referencia a documentación de hello lenguaje de consulta SQL de API de Azure Cosmos DB documentos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-101">title: aaa"Azure Cosmos DB DocumentDB API: SQL syntax | Microsoft Docs" description: Reference documentation for hello Azure Cosmos DB DocumentDB API SQL query language.</span></span>
<span data-ttu-id="11a3f-102">servicios: cosmos db autor: mimig1 manager: editor de jhubbard: mimig documentationcenter: ''</span><span class="sxs-lookup"><span data-stu-id="11a3f-102">services: cosmos-db author: mimig1 manager: jhubbard editor: mimig documentationcenter: ''</span></span>

<span data-ttu-id="11a3f-103">MS.AssetId: ms.service: cosmos db ms.workload: ms.tgt_pltfrm de servicios de datos: na ms.devlang: na ms.topic: referencia ms.date: 06/13/2017 ms.author: mimig</span><span class="sxs-lookup"><span data-stu-id="11a3f-103">ms.assetid: ms.service: cosmos-db ms.workload: data-services ms.tgt_pltfrm: na ms.devlang: na ms.topic: reference ms.date: 06/13/2017 ms.author: mimig</span></span>

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="11a3f-104">API de DocumentDB de Azure Cosmos DB: referencia de sintaxis SQL</span><span class="sxs-lookup"><span data-stu-id="11a3f-104">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="11a3f-105">Hola API de documentos de base de datos de Azure Cosmos admite consultas documentos mediante una instancia de SQL (lenguaje de consulta estructurado) familiar gramática similar en documentos JSON jerárquicos sin necesidad de esquema explícito o la creación de índices secundarios.</span><span class="sxs-lookup"><span data-stu-id="11a3f-105">hello Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="11a3f-106">En este tema se proporciona documentación de referencia de lenguaje de consulta SQL de la API de documentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-106">This topic provides reference documentation for hello DocumentDB API SQL query language.</span></span>

<span data-ttu-id="11a3f-107">Para ver un tutorial de hello lenguaje de consulta SQL de la API de documentos, consulte [consultas SQL para la API de documentos de base de datos de Azure Cosmos](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="11a3f-107">For a walkthrough of hello DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="11a3f-108">También le invitamos hello toovisit [Query Playground](http://www.documentdb.com/sql/demo) donde puede probar la base de datos de Azure Cosmos y ejecutar consultas SQL contra nuestro conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-108">We also invite you toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="11a3f-109">Consulta SELECT</span><span class="sxs-lookup"><span data-stu-id="11a3f-109">SELECT query</span></span>  
<span data-ttu-id="11a3f-110">Recupera documentos JSON de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-110">Retrieves JSON documents from hello database.</span></span> <span data-ttu-id="11a3f-111">Es compatible con la evaluación de expresiones, las proyecciones, el filtrado y las combinaciones.</span><span class="sxs-lookup"><span data-stu-id="11a3f-111">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="11a3f-112">convenciones de Hello utilizadas para describir las instrucciones SELECT de Hola se tabulan en hello sección de convenciones de sintaxis.</span><span class="sxs-lookup"><span data-stu-id="11a3f-112">hello conventions used for describing hello SELECT statements are tabulated in hello Syntax conventions section.</span></span>  
  
<span data-ttu-id="11a3f-113">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-113">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="11a3f-114">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="11a3f-114">**Remarks**</span></span>  
  
 <span data-ttu-id="11a3f-115">Consulte las siguientes secciones para más información sobre las cláusulas:</span><span class="sxs-lookup"><span data-stu-id="11a3f-115">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="11a3f-116">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="11a3f-116">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="11a3f-117">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="11a3f-117">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="11a3f-118">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="11a3f-118">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="11a3f-119">Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="11a3f-119">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="11a3f-120">cláusulas de Hello en la instrucción SELECT de Hola se deben ordenar como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="11a3f-120">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="11a3f-121">Se puede omitir cualquiera de las cláusulas opcionales de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-121">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="11a3f-122">Pero cuando se usan cláusulas opcionales, deben aparecer en el orden correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-122">But when optional clauses are used, they must appear in hello right order.</span></span>  
  
<span data-ttu-id="11a3f-123">**Orden de procesamiento lógico de la instrucción SELECT de Hola**</span><span class="sxs-lookup"><span data-stu-id="11a3f-123">**Logical Processing Order of hello SELECT statement**</span></span>  
  
<span data-ttu-id="11a3f-124">orden de Hello en el que se procesan las cláusulas es:</span><span class="sxs-lookup"><span data-stu-id="11a3f-124">hello order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="11a3f-125">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="11a3f-125">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="11a3f-126">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="11a3f-126">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="11a3f-127">Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="11a3f-127">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="11a3f-128">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="11a3f-128">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="11a3f-129">Tenga en cuenta que esto es diferente del orden de hello en que aparecen en la sintaxis de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-129">Note that this is different from hello order in which they appear in hello syntax.</span></span> <span data-ttu-id="11a3f-130">Hola ordenación es tal que todos los símbolos nuevos introducidos por una cláusula procesada son visibles y pueden utilizarse en las cláusulas procesadas posteriormente.</span><span class="sxs-lookup"><span data-stu-id="11a3f-130">hello ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="11a3f-131">Por ejemplo, las cláusulas WHERE y SELECT pueden acceder a los alias declarados en una cláusula FROM.</span><span class="sxs-lookup"><span data-stu-id="11a3f-131">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="11a3f-132">**Comentarios y caracteres de espacio en blanco**</span><span class="sxs-lookup"><span data-stu-id="11a3f-132">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="11a3f-133">Todos los caracteres de espacio en blanco que no forman parte de una cadena entrecomillada o identificador entrecomillado no forman parte de la gramática del lenguaje de Hola y se omiten durante el análisis.</span><span class="sxs-lookup"><span data-stu-id="11a3f-133">All white space characters which are not part of a quoted string or quoted identifier are not part of hello language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="11a3f-134">lenguaje de consulta de Hello admite comentarios de estilo de T-SQL como</span><span class="sxs-lookup"><span data-stu-id="11a3f-134">hello query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="11a3f-135">Instrucción SQL `-- comment text [newline]`.</span><span class="sxs-lookup"><span data-stu-id="11a3f-135">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="11a3f-136">Mientras que los comentarios y espacios en blanco no tiene importancia en la gramática de hello, deben ser tokens tooseparate usado.</span><span class="sxs-lookup"><span data-stu-id="11a3f-136">While whitespace characters and comments do not have any significance in hello grammar, they must be used tooseparate tokens.</span></span> <span data-ttu-id="11a3f-137">Por ejemplo: `-1e5` es un token de un solo número, mientras que `: – 1 e5` es un token de menos seguido por el número 1 y el identificador e5.</span><span class="sxs-lookup"><span data-stu-id="11a3f-137">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="11a3f-138"><a name="bk_select_query"></a> Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="11a3f-138"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="11a3f-139">cláusulas de Hello en la instrucción SELECT de Hola se deben ordenar como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="11a3f-139">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="11a3f-140">Se puede omitir cualquiera de las cláusulas opcionales de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-140">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="11a3f-141">Pero cuando se usan cláusulas opcionales, deben aparecer en el orden correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-141">But when optional clauses are used, they must appear in hello right order.</span></span>  

<span data-ttu-id="11a3f-142">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-142">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="11a3f-143">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-143">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="11a3f-144">Establece propiedades o el valor toobe seleccionado para el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="11a3f-144">Properties or value toobe selected for hello result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="11a3f-145">Especifica que se debe recuperar el valor de hello sin realizar ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="11a3f-145">Specifies that hello value should be retrieved without making any changes.</span></span> <span data-ttu-id="11a3f-146">En concreto si valor Hola procesado es un objeto, se recuperarán todas las propiedades.</span><span class="sxs-lookup"><span data-stu-id="11a3f-146">Specifically if hello processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="11a3f-147">Especifica la lista de Hola de toobe de propiedades que se recuperan.</span><span class="sxs-lookup"><span data-stu-id="11a3f-147">Specifies hello list of properties toobe retrieved.</span></span> <span data-ttu-id="11a3f-148">Cada valor devuelto será un objeto con propiedades de hello especificadas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-148">Each returned value will be an object with hello properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="11a3f-149">Especifica que se debe recuperar el valor JSON de hello en lugar del objeto JSON completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-149">Specifies that hello JSON value should be retrieved instead of hello complete JSON object.</span></span> <span data-ttu-id="11a3f-150">Esto, a diferencia `<property_list>` no ajusta el valor de hello proyectada en un objeto.</span><span class="sxs-lookup"><span data-stu-id="11a3f-150">This, unlike `<property_list>` does not wrap hello projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="11a3f-151">Calcula la expresión que representa Hola valor toobe.</span><span class="sxs-lookup"><span data-stu-id="11a3f-151">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="11a3f-152">Consulte la sección [Expresiones escalares](#bk_scalar_expressions) para más información.</span><span class="sxs-lookup"><span data-stu-id="11a3f-152">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="11a3f-153">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="11a3f-153">**Remarks**</span></span>  
  
<span data-ttu-id="11a3f-154">Hola `SELECT *` sintaxis sólo es válida si la cláusula FROM ha declarado exactamente un alias.</span><span class="sxs-lookup"><span data-stu-id="11a3f-154">hello `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="11a3f-155">`SELECT *` proporciona una proyección de identidad, que puede resultar útil si no se necesitan proyecciones.</span><span class="sxs-lookup"><span data-stu-id="11a3f-155">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="11a3f-156">SELECT * solo es válida si se especifica cláusula FROM y se introdujo solo un origen de entrada.</span><span class="sxs-lookup"><span data-stu-id="11a3f-156">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="11a3f-157">Tenga en cuenta que `SELECT <select_list>` y `SELECT *` son código sintáctico y pueden expresarse también mediante instrucciones SELECT sencillas, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="11a3f-157">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="11a3f-158">equivale a:</span><span class="sxs-lookup"><span data-stu-id="11a3f-158">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="11a3f-159">equivale a:</span><span class="sxs-lookup"><span data-stu-id="11a3f-159">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="11a3f-160">**Consulte también**</span><span class="sxs-lookup"><span data-stu-id="11a3f-160">**See Also**</span></span>  
  
[<span data-ttu-id="11a3f-161">Expresiones escalares</span><span class="sxs-lookup"><span data-stu-id="11a3f-161">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="11a3f-162">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="11a3f-162">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="11a3f-163"><a name="bk_from_clause"></a> Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="11a3f-163"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="11a3f-164">Especifica el origen de Hola o los orígenes combinados.</span><span class="sxs-lookup"><span data-stu-id="11a3f-164">Specifies hello source or joined sources.</span></span> <span data-ttu-id="11a3f-165">Hola FROM cláusula es opcional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-165">hello FROM clause is optional.</span></span> <span data-ttu-id="11a3f-166">Si no se especifica, las demás cláusulas se continuarán ejecutando como si la cláusula FROM proporcionara un documento único.</span><span class="sxs-lookup"><span data-stu-id="11a3f-166">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="11a3f-167">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-167">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="11a3f-168">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-168">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="11a3f-169">Especifica un origen de datos, con o sin alias.</span><span class="sxs-lookup"><span data-stu-id="11a3f-169">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="11a3f-170">Si no se especifica, se inferirán de hello `<collection_expression>` con las siguientes reglas:</span><span class="sxs-lookup"><span data-stu-id="11a3f-170">If alias is not specified, it will be inferred from hello `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="11a3f-171">Si expresión de hello es un collection_name, se utilizará collection_name como alias.</span><span class="sxs-lookup"><span data-stu-id="11a3f-171">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="11a3f-172">Si la expresión de hello es `<collection_expression>`, entonces se usará property_name y, a continuación, property_name como alias.</span><span class="sxs-lookup"><span data-stu-id="11a3f-172">If hello expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="11a3f-173">Si expresión de hello es un collection_name, se utilizará collection_name como alias.</span><span class="sxs-lookup"><span data-stu-id="11a3f-173">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="11a3f-174">AS `input_alias`.</span><span class="sxs-lookup"><span data-stu-id="11a3f-174">AS `input_alias`</span></span>  
  
<span data-ttu-id="11a3f-175">Especifica que hello `input_alias` es un conjunto de valores devueltos por hello subyacente de la expresión de colección.</span><span class="sxs-lookup"><span data-stu-id="11a3f-175">Specifies that hello `input_alias` is a set of values returned by hello underlying collection expression.</span></span>  
 
<span data-ttu-id="11a3f-176">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="11a3f-176">`input_alias` IN</span></span>  
  
<span data-ttu-id="11a3f-177">Especifica que hello `input_alias` debe representar el conjunto de Hola de valores obtenidos por recorrer en iteración todos los elementos de la matriz de cada matriz devuelta por hello subyacente de la expresión de colección.</span><span class="sxs-lookup"><span data-stu-id="11a3f-177">Specifies that hello `input_alias` should represent hello set of values obtained by iterating over all array elements of each array returned by hello underlying collection expression.</span></span> <span data-ttu-id="11a3f-178">Se omite cualquier valor que la expresión de colección subyacente devuelva que no sea una matriz.</span><span class="sxs-lookup"><span data-stu-id="11a3f-178">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="11a3f-179">Especifica Hola colección expresión toobe usa documentos de hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="11a3f-179">Specifies hello collection expression toobe used tooretrieve hello documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="11a3f-180">Especifica que debe recuperarse ese documento de Hola de forma predeterminada, colección actualmente conectada.</span><span class="sxs-lookup"><span data-stu-id="11a3f-180">Specifies that document should be retrieved from hello default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="11a3f-181">Especifica que debe recuperarse ese documento de colección de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="11a3f-181">Specifies that document should be retrieved from hello provided collection.</span></span> <span data-ttu-id="11a3f-182">Hola nombre de colección de hello debe coincidir con hello de colección de hello conectado actualmente.</span><span class="sxs-lookup"><span data-stu-id="11a3f-182">hello name of hello collection must match hello name of hello collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="11a3f-183">Especifica que debe recuperarse ese documento de hello otro origen definido por el alias de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="11a3f-183">Specifies that document should be retrieved from hello other source defined by hello provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="11a3f-184">Especifica que debe recuperarse ese documento accediendo hello `property_name` especifica el elemento de matriz de propiedad o array_index para todos los documentos recuperados por expresión de colección.</span><span class="sxs-lookup"><span data-stu-id="11a3f-184">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="11a3f-185">Especifica que debe recuperarse ese documento accediendo hello `property_name` especifica el elemento de matriz de propiedad o array_index para todos los documentos recuperados por expresión de colección.</span><span class="sxs-lookup"><span data-stu-id="11a3f-185">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="11a3f-186">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="11a3f-186">**Remarks**</span></span>  
  
<span data-ttu-id="11a3f-187">Todos los alias proporcionados o deducidos en hello `<from_source>(`s) deben ser únicos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-187">All aliases provided or inferred in hello `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="11a3f-188">Hola sintaxis `<collection_expression>.`property_name es Hola igual que `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="11a3f-188">hello Syntax `<collection_expression>.`property_name is hello same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="11a3f-189">Sin embargo, pueden utilizarse esta última sintaxis de hello si un nombre de propiedad contiene un carácter no son identificadores.</span><span class="sxs-lookup"><span data-stu-id="11a3f-189">However, hello latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="11a3f-190">**Manejo de situaciones en las que faltan propiedades o elementos de matriz o en las que hay valores sin definir**</span><span class="sxs-lookup"><span data-stu-id="11a3f-190">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="11a3f-191">Si una expresión de colección accede a propiedades o elementos de matriz y el valor no existe, ese valor se omitirá y no se seguirá procesando.</span><span class="sxs-lookup"><span data-stu-id="11a3f-191">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="11a3f-192">**Ámbito de contexto de la expresión de la colección**</span><span class="sxs-lookup"><span data-stu-id="11a3f-192">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="11a3f-193">El ámbito de las expresiones de colección puede ser de colección o de documento:</span><span class="sxs-lookup"><span data-stu-id="11a3f-193">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="11a3f-194">Una expresión es de ámbito de la colección, si hello origen subyacente de la expresión de colección de hello es ROOT o `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="11a3f-194">An expression is collection-scoped, if hello underlying source of hello collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="11a3f-195">Este tipo de expresión representa un conjunto de documentos directamente recuperados de la colección de hello directamente y no es dependiente del procesamiento de Hola de otras expresiones de la colección.</span><span class="sxs-lookup"><span data-stu-id="11a3f-195">Such an expression represents a set of documents retrieved from hello collection directly, and is not dependent on hello processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="11a3f-196">Una expresión es de ámbito de documento, si hello origen subyacente de la expresión de colección de hello es `input_alias` presentada anteriormente en la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-196">An expression is document-scoped, if hello underlying source of hello collection expression is `input_alias` introduced earlier in hello query.</span></span> <span data-ttu-id="11a3f-197">Dicha expresión representa un conjunto de documentos obtenidos al evaluar la expresión de colección hello en el ámbito de Hola de cada documento que pertenece el conjunto de toohello asociado a la colección de alias de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-197">Such an expression represents a set of documents obtained by evaluating hello collection expression in hello scope of each document belonging toohello set associated with hello aliased collection.</span></span>  <span data-ttu-id="11a3f-198">conjunto resultante de Hello será una unión de los conjuntos obtenidos mediante la evaluación de expresión de colección de Hola para cada uno de los documentos de Hola Hola subyacente conjunto.</span><span class="sxs-lookup"><span data-stu-id="11a3f-198">hello resulting set will be a union of sets obtained by evaluating hello collection expression for each of hello documents in hello underlying set.</span></span>  
  
<span data-ttu-id="11a3f-199">**Combinaciones**</span><span class="sxs-lookup"><span data-stu-id="11a3f-199">**Joins**</span></span>  
  
<span data-ttu-id="11a3f-200">En la versión actual de hello, base de datos de Azure Cosmos admite combinaciones internas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-200">In hello current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="11a3f-201">Las funcionalidades de combinación adicionales estarán disponibles próximamente.</span><span class="sxs-lookup"><span data-stu-id="11a3f-201">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="11a3f-202">Conjuntos de resultados de combinaciones internas en un producto cruzado completado de hello participan en la combinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-202">Inner joins result in a complete cross product of hello sets participating in hello join.</span></span> <span data-ttu-id="11a3f-203">resultado de Hello de una combinación de N es un conjunto de tuplas de N elementos, donde cada valor de tupla Hola está asociado con un alias de hello establecer participan en la combinación de Hola y son accesibles mediante una referencia a ese alias en otras cláusulas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-203">hello result of an N-way join is a set of N-element tuples, where each value in hello tuple is associated with hello aliased set participating in hello join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="11a3f-204">evaluación de saludo de combinación de hello depende de ámbito de contexto de Hola de hello participa conjuntos:</span><span class="sxs-lookup"><span data-stu-id="11a3f-204">hello evaluation of hello join depends on hello context scope of hello participating sets:</span></span>  
  
-  <span data-ttu-id="11a3f-205">La combinación entre un conjunto de ámbito de colección A y otro B da como resultado un producto cruzado de todos los elementos de los conjuntos A y B.</span><span class="sxs-lookup"><span data-stu-id="11a3f-205">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="11a3f-206">La combinación entre un conjunto A y un conjunto de ámbito de documento B da como resultado una unión de todos los conjuntos obtenidos de la evaluación de B para cada documento del conjunto A.</span><span class="sxs-lookup"><span data-stu-id="11a3f-206">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="11a3f-207">En la versión actual de hello, se admite un máximo de una expresión de ámbito de la colección por el procesador de consultas de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-207">In hello current release, a maximum of one collection-scoped expression is supported by hello query processor.</span></span>  
  
<span data-ttu-id="11a3f-208">**Ejemplos de combinaciones:**</span><span class="sxs-lookup"><span data-stu-id="11a3f-208">**Examples of joins:**</span></span>  
  
<span data-ttu-id="11a3f-209">Echemos un vistazo a Hola siguiente cláusula FROM:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="11a3f-209">Let's look at hello following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="11a3f-210">Los orígenes definirán `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="11a3f-210">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="11a3f-211">Esta cláusula FROM devuelve un conjunto de N tuplas (tupla con N valores).</span><span class="sxs-lookup"><span data-stu-id="11a3f-211">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="11a3f-212">Cada tupla tiene valores generados por sus respectivos conjuntos en iteración de todos los alias de colección.</span><span class="sxs-lookup"><span data-stu-id="11a3f-212">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="11a3f-213">*Ejemplo de COMBINACIÓN 1, con 2 orígenes:*</span><span class="sxs-lookup"><span data-stu-id="11a3f-213">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="11a3f-214">`<from_source1>` tendrá ámbito de colección y representa el conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="11a3f-214">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="11a3f-215">`<from_source2>` tendrá ámbito de documento, hará referencia a input_alias1 y representará los conjuntos:</span><span class="sxs-lookup"><span data-stu-id="11a3f-215">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="11a3f-216">{1, 2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-216">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="11a3f-217">{3} para `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-217">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="11a3f-218">{4, 5} para `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-218">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="11a3f-219">Hola de cláusula `<from_source1> JOIN <from_source2>` dará como resultado Hola siguientes tuplas:</span><span class="sxs-lookup"><span data-stu-id="11a3f-219">hello FROM clause `<from_source1> JOIN <from_source2>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="11a3f-220">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="11a3f-220">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="11a3f-221">*Ejemplo de COMBINACIÓN 2, con 3 orígenes:*</span><span class="sxs-lookup"><span data-stu-id="11a3f-221">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="11a3f-222">`<from_source1>` tendrá ámbito de colección y representa el conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="11a3f-222">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="11a3f-223">`<from_source2>` tendrá ámbito de documento, hará referencia a `input_alias1` y representará los conjuntos:</span><span class="sxs-lookup"><span data-stu-id="11a3f-223">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="11a3f-224">{1, 2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-224">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="11a3f-225">{3} para `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-225">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="11a3f-226">{4, 5} para `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-226">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="11a3f-227">`<from_source3>` tendrá ámbito de documento, hará referencia a `input_alias2` y representará los conjuntos:</span><span class="sxs-lookup"><span data-stu-id="11a3f-227">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="11a3f-228">{100, 200} para `input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-228">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="11a3f-229">{300} para `input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-229">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="11a3f-230">Hola de cláusula `<from_source1> JOIN <from_source2> JOIN <from_source3>` dará como resultado Hola siguientes tuplas:</span><span class="sxs-lookup"><span data-stu-id="11a3f-230">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="11a3f-231">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="11a3f-231">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="11a3f-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="11a3f-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="11a3f-233">Falta de tuplas para otros valores de `input_alias1`, `input_alias2`, para qué hello `<from_source3>` no devolvió ningún valor.</span><span class="sxs-lookup"><span data-stu-id="11a3f-233">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which hello `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="11a3f-234">*Ejemplo de COMBINACIÓN 3, con 3 orígenes:*</span><span class="sxs-lookup"><span data-stu-id="11a3f-234">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="11a3f-235"><from_source1> tendrá ámbito de colección y representa el conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="11a3f-235">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="11a3f-236">`<from_source1>` tendrá ámbito de colección y representa el conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="11a3f-236">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="11a3f-237"><from_source2> tendrá ámbito de documento, hará referencia a input_alias1 y representará los conjuntos:</span><span class="sxs-lookup"><span data-stu-id="11a3f-237">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="11a3f-238">{1, 2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-238">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="11a3f-239">{3} para `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-239">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="11a3f-240">{4, 5} para `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-240">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="11a3f-241">Permiten `<from_source3>` con demasiado el ámbito`input_alias1` y representa conjuntos:</span><span class="sxs-lookup"><span data-stu-id="11a3f-241">Let `<from_source3>` be scoped too`input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="11a3f-242">{100, 200} para `input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-242">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="11a3f-243">{300} para `input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="11a3f-243">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="11a3f-244">Hola de cláusula `<from_source1> JOIN <from_source2> JOIN <from_source3>` dará como resultado Hola siguientes tuplas:</span><span class="sxs-lookup"><span data-stu-id="11a3f-244">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="11a3f-245">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="11a3f-245">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="11a3f-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300), (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="11a3f-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="11a3f-247">Esto da como resultado un producto cruzado entre `<from_source2>` y `<from_source3>` porque ambos son toohello ámbito mismo `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="11a3f-247">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped toohello same `<from_source1>`.</span></span>  <span data-ttu-id="11a3f-248">Esto dio como resultado 4 (2 x 2) tuplas con valor A, 0 tuplas con valor B (1 x 0) y 2 (2 x 1) tuplas con valor C.</span><span class="sxs-lookup"><span data-stu-id="11a3f-248">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="11a3f-249">**Consulte también**</span><span class="sxs-lookup"><span data-stu-id="11a3f-249">**See also**</span></span>  
  
 [<span data-ttu-id="11a3f-250">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="11a3f-250">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="11a3f-251"><a name="bk_where_clause"></a> Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="11a3f-251"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="11a3f-252">Especifica la condición de búsqueda de Hola para documentos de hello devuelto por la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-252">Specifies hello search condition for hello documents returned by hello query.</span></span>  
  
 <span data-ttu-id="11a3f-253">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-253">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="11a3f-254">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-254">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="11a3f-255">Especifica Hola condición toobe cumplido para hello documentos toobe devuelto.</span><span class="sxs-lookup"><span data-stu-id="11a3f-255">Specifies hello condition toobe met for hello documents toobe returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="11a3f-256">Calcula la expresión que representa Hola valor toobe.</span><span class="sxs-lookup"><span data-stu-id="11a3f-256">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="11a3f-257">Vea hello [expresiones escalares](#bk_scalar_expressions) sección para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="11a3f-257">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="11a3f-258">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="11a3f-258">**Remarks**</span></span>  
  
 <span data-ttu-id="11a3f-259">En orden para hello toobe documento devuelve una expresión especificada como condición de filtro debe evaluarse tootrue.</span><span class="sxs-lookup"><span data-stu-id="11a3f-259">In order for hello document toobe returned an expression specified as filter condition must evaluate tootrue.</span></span> <span data-ttu-id="11a3f-260">Solo un valor booleano true cumplirá la condición de hello, cualquier otro valor: sin definir, null, false, número, matriz u objeto no cumplirá la condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-260">Only Boolean value true will satisfy hello condition, any other value: undefined, null, false, Number, Array or Object will not satisfy hello condition.</span></span>  
  
##  <span data-ttu-id="11a3f-261"><a name="bk_orderby_clause"></a> Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="11a3f-261"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="11a3f-262">Especifica Hola orden de clasificación de resultados devueltos por la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-262">Specifies hello sorting order for results returned by hello query.</span></span>  
  
 <span data-ttu-id="11a3f-263">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-263">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="11a3f-264">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-264">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="11a3f-265">Especifica una propiedad o una expresión en la que del conjunto de resultados de consulta de hello toosort.</span><span class="sxs-lookup"><span data-stu-id="11a3f-265">Specifies a property or expression on which toosort hello query result set.</span></span> <span data-ttu-id="11a3f-266">Se puede especificar una columna de ordenación como alias de nombre o de columna.</span><span class="sxs-lookup"><span data-stu-id="11a3f-266">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="11a3f-267">Se pueden especificar varias columnas de ordenación.</span><span class="sxs-lookup"><span data-stu-id="11a3f-267">Multiple sort columns can be specified.</span></span> <span data-ttu-id="11a3f-268">Los nombres de columna deben ser únicos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-268">Column names must be unique.</span></span> <span data-ttu-id="11a3f-269">secuencia de Hola Hola de columnas de ordenación en la cláusula ORDER BY Hola define la organización de Hola Hola ordenado de conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="11a3f-269">hello sequence of hello sort columns in hello ORDER BY clause defines hello organization of hello sorted result set.</span></span> <span data-ttu-id="11a3f-270">Es decir, conjunto de resultados de Hola se ordena por la primera propiedad de hello y, a continuación, esa lista ordenada se ordena por la segunda propiedad de Hola y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="11a3f-270">That is, hello result set is sorted by hello first property and then that ordered list is sorted by hello second property, and so on.</span></span>  
  
     <span data-ttu-id="11a3f-271">nombres de columna de Hello hace referencia en la cláusula ORDER BY Hola deben corresponderse tooeither una columna de hello seleccione lista o tooa columna definida en la tabla especificada en la cláusula FROM de hello sin ambigüedades.</span><span class="sxs-lookup"><span data-stu-id="11a3f-271">hello column names referenced in hello ORDER BY clause must correspond tooeither a column in hello select list or tooa column defined in a table specified in hello FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="11a3f-272">Especifica una propiedad única o una expresión en qué conjunto de resultados de consulta de hello toosort.</span><span class="sxs-lookup"><span data-stu-id="11a3f-272">Specifies a single property or expression on which toosort hello query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="11a3f-273">Vea hello [expresiones escalares](#bk_scalar_expressions) sección para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="11a3f-273">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="11a3f-274">Especifica que los valores de hello en la columna especificada de Hola se deben ordenar en orden ascendente o descendente.</span><span class="sxs-lookup"><span data-stu-id="11a3f-274">Specifies that hello values in hello specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="11a3f-275">ASC ordena del valor de toohighest de valor más bajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-275">ASC sorts from hello lowest value toohighest value.</span></span> <span data-ttu-id="11a3f-276">DESC ordena del valor de toolowest de valor más alto.</span><span class="sxs-lookup"><span data-stu-id="11a3f-276">DESC sorts from highest value toolowest value.</span></span> <span data-ttu-id="11a3f-277">ASC es el criterio de ordenación predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-277">ASC is hello default sort order.</span></span> <span data-ttu-id="11a3f-278">Valores NULL se tratan como valores de hello más bajos posibles.</span><span class="sxs-lookup"><span data-stu-id="11a3f-278">Null values are treated as hello lowest possible values.</span></span>  
  
 <span data-ttu-id="11a3f-279">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="11a3f-279">**Remarks**</span></span>  
  
 <span data-ttu-id="11a3f-280">Durante la gramática de consulta de hello permite varios pedidos por propiedades, tiempo de ejecución de consulta de base de datos de Azure Cosmos de hello admite ordenación únicamente en una sola propiedad y únicamente en los nombres de propiedad, es decir, no en las propiedades calculadas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-280">While hello query grammar supports multiple order by properties, hello Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="11a3f-281">Ordenar también requiere que Hola directiva de indexación incluye un índice de intervalo para la propiedad de Hola y Hola especificado tipo, con una precisión máxima de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-281">Sorting also requires that hello indexing policy includes a range index for hello property and hello specified type, with hello maximum precision.</span></span> <span data-ttu-id="11a3f-282">Consulte toohello documentación para obtener más detalles de la directiva de indización.</span><span class="sxs-lookup"><span data-stu-id="11a3f-282">Refer toohello indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="11a3f-283"><a name="bk_scalar_expressions"></a> Expresiones escalares</span><span class="sxs-lookup"><span data-stu-id="11a3f-283"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="11a3f-284">Una expresión escalar es una combinación de símbolos y operadores que se pueden evalúan tooobtain un valor único.</span><span class="sxs-lookup"><span data-stu-id="11a3f-284">A scalar expression is a combination of symbols and operators that can be evaluated tooobtain a single value.</span></span> <span data-ttu-id="11a3f-285">Las expresiones simples pueden ser constantes, referencias de propiedad, referencias de elementos de matriz, referencias de alias o llamadas de función.</span><span class="sxs-lookup"><span data-stu-id="11a3f-285">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="11a3f-286">Las expresiones simples se pueden combinar en expresiones complejas con operadores.</span><span class="sxs-lookup"><span data-stu-id="11a3f-286">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="11a3f-287">Para más información sobre los valores que puede tener una expresión escalar, consulte la sección [Constantes](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="11a3f-287">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="11a3f-288">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-288">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="11a3f-289">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-289">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="11a3f-290">Representa un valor constante.</span><span class="sxs-lookup"><span data-stu-id="11a3f-290">Represents a constant value.</span></span> <span data-ttu-id="11a3f-291">Consulte la sección [Constantes](#bk_constants) para más información.</span><span class="sxs-lookup"><span data-stu-id="11a3f-291">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="11a3f-292">Representa un valor definido por hello `input_alias` introducidas en hello `FROM` cláusula.</span><span class="sxs-lookup"><span data-stu-id="11a3f-292">Represents a value defined by hello `input_alias` introduced in hello `FROM` clause.</span></span>  
    <span data-ttu-id="11a3f-293">Este valor se garantiza toonot ser **indefinido** :**indefinido** se omiten los valores de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-293">This value is guaranteed toonot be **undefined** –**undefined** values in hello input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="11a3f-294">Representa un valor de propiedad de Hola de un objeto.</span><span class="sxs-lookup"><span data-stu-id="11a3f-294">Represents a value of hello property of an object.</span></span> <span data-ttu-id="11a3f-295">Si no existe ninguna propiedad de Hola o propiedad que se hace referencia en un valor que no es un objeto y luego Hola expresión, se evalúa como demasiado**indefinido** valor.</span><span class="sxs-lookup"><span data-stu-id="11a3f-295">If hello property does not exist or property is referenced on a value which is not an object, then hello expression evaluates too**undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="11a3f-296">Representa un valor de propiedad de hello con nombre `property_name` o elemento de matriz con el índice `array_index` de una matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-296">Represents a value of hello property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="11a3f-297">Si no existe el índice de propiedad o matriz de Hola o índice de la propiedad/matriz Hola se hace referencia en un valor que no es una matriz de objetos, a continuación, Hola expresión se evalúa como el valor de tooundefined.</span><span class="sxs-lookup"><span data-stu-id="11a3f-297">If hello property/array index does not exist or hello property/array index is referenced on a value which is not an object/array, then hello expression evaluates tooundefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="11a3f-298">Representa un operador que sea tooa aplicado un solo valor.</span><span class="sxs-lookup"><span data-stu-id="11a3f-298">Represents an operator that is applied tooa single value.</span></span> <span data-ttu-id="11a3f-299">Consulte la sección [Operadores](#bk_operators) para más información.</span><span class="sxs-lookup"><span data-stu-id="11a3f-299">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="11a3f-300">Representa un operador que es tener valores tootwo aplicada.</span><span class="sxs-lookup"><span data-stu-id="11a3f-300">Represents an operator that is applied tootwo values.</span></span> <span data-ttu-id="11a3f-301">Consulte la sección [Operadores](#bk_operators) para más información.</span><span class="sxs-lookup"><span data-stu-id="11a3f-301">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="11a3f-302">Representa un valor definido por el resultado de una llamada de función.</span><span class="sxs-lookup"><span data-stu-id="11a3f-302">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="11a3f-303">Función escalar definida por el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-303">Name of hello user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="11a3f-304">Nombre de función escalar integrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-304">Name of hello built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="11a3f-305">Representa un valor obtenido al crear un objeto con propiedades especificadas y sus valores.</span><span class="sxs-lookup"><span data-stu-id="11a3f-305">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="11a3f-306">Representa un valor obtenido al crear una matriz con valores especificados como elementos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-306">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="11a3f-307">Representa un valor de nombre de parámetro especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-307">Represents a value of hello specified parameter name.</span></span> <span data-ttu-id="11a3f-308">Nombres de parámetro deben tener un único @ como primer carácter de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-308">Parameter names must have a single @ as hello first character.</span></span>  
  
 <span data-ttu-id="11a3f-309">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="11a3f-309">**Remarks**</span></span>  
  
 <span data-ttu-id="11a3f-310">Todos los argumentos deben estar definidos al llamar a una función escalar incorporada o definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="11a3f-310">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="11a3f-311">Si alguno de los argumentos de hello no está definido, no se llamará función hello y Hola resultado será indefinido.</span><span class="sxs-lookup"><span data-stu-id="11a3f-311">If any of hello arguments is undefined, hello function will not be called and hello result will be undefined.</span></span>  
  
 <span data-ttu-id="11a3f-312">Cuando se crea un objeto, cualquier propiedad que se asigna el valor no definido se omite y no se incluyen en hello creado el objeto.</span><span class="sxs-lookup"><span data-stu-id="11a3f-312">When creating an object, any property that is assigned undefined value will be skipped and not included in hello created object.</span></span>  
  
 <span data-ttu-id="11a3f-313">Cuando se asigna la creación de una matriz, cualquier valor del elemento que **indefinido** valor se omite y no se incluyen en el objeto Hola creado.</span><span class="sxs-lookup"><span data-stu-id="11a3f-313">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in hello created object.</span></span> <span data-ttu-id="11a3f-314">Esto hará que tootake de elemento de Hola a continuación definida su lugar como dicha matriz Hola creado no tenga índices omitidos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-314">This will cause hello next defined element tootake its place in such a way that hello created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="11a3f-315"><a name="bk_operators"></a> Operadores</span><span class="sxs-lookup"><span data-stu-id="11a3f-315"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="11a3f-316">Esta sección describe los operadores de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="11a3f-316">This section describes hello supported operators.</span></span> <span data-ttu-id="11a3f-317">Cada operador puede ser tooexactly asignado una categoría.</span><span class="sxs-lookup"><span data-stu-id="11a3f-317">Each operator can be assigned tooexactly one category.</span></span>  
  
 <span data-ttu-id="11a3f-318">Consulte la siguiente tabla, **Categorías de operadores**, para más información acerca del control de los valores **undefined**, los requisitos de tipo de valores de entrada y el control de los valores con tipos no coincidentes.</span><span class="sxs-lookup"><span data-stu-id="11a3f-318">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="11a3f-319">**Categorías de operadores:**</span><span class="sxs-lookup"><span data-stu-id="11a3f-319">**Operator categories:**</span></span>  
  
|<span data-ttu-id="11a3f-320">**Categoría**</span><span class="sxs-lookup"><span data-stu-id="11a3f-320">**Category**</span></span>|<span data-ttu-id="11a3f-321">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="11a3f-321">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="11a3f-322">**aritméticos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-322">**arithmetic**</span></span>|<span data-ttu-id="11a3f-323">El operador espera que las entradas toobe números.</span><span class="sxs-lookup"><span data-stu-id="11a3f-323">Operator expects input(s) toobe Number(s).</span></span> <span data-ttu-id="11a3f-324">La salida también es un número.</span><span class="sxs-lookup"><span data-stu-id="11a3f-324">Output is also a Number.</span></span> <span data-ttu-id="11a3f-325">Si se cumple alguna de las entradas de hello **indefinido** o es de tipo que no sea resultado de número, a continuación, hello **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="11a3f-325">If any of hello inputs is **undefined** or type other than Number then hello result is **undefined**.</span></span>|  
|<span data-ttu-id="11a3f-326">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="11a3f-326">**bitwise**</span></span>|<span data-ttu-id="11a3f-327">El operador espera que las entradas entero con signo de 32 bits de toobe números.</span><span class="sxs-lookup"><span data-stu-id="11a3f-327">Operator expects input(s) toobe 32-bit signed integer Number(s).</span></span> <span data-ttu-id="11a3f-328">La salida también es un número entero con signo de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="11a3f-328">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="11a3f-329">Los valores que no sean enteros se redondean.</span><span class="sxs-lookup"><span data-stu-id="11a3f-329">Any non-integer value will be rounded.</span></span> <span data-ttu-id="11a3f-330">Los valores positivos se redondean a la baja y los negativos, a la alta.</span><span class="sxs-lookup"><span data-stu-id="11a3f-330">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="11a3f-331">Se convertirá cualquier valor que está fuera del intervalo de entero de 32 bits de hello, aprovechando los últimos 32 bits de sus dos notaciones de complementos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-331">Any value that is outside of hello 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="11a3f-332">Si se cumple alguna de las entradas de hello **indefinido** o tipo que no sea número, entonces el resultado de hello es **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="11a3f-332">If any of hello inputs is **undefined** or type other than Number, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="11a3f-333">**Nota:** Hola anteriormente el comportamiento es compatible con el comportamiento del operador bit a bit de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="11a3f-333">**Note:** hello above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="11a3f-334">**lógicos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-334">**logical**</span></span>|<span data-ttu-id="11a3f-335">El operador espera que las entradas toobe booleanas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-335">Operator expects input(s) toobe Boolean(s).</span></span> <span data-ttu-id="11a3f-336">La salida también es un booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-336">Output is also a Boolean.</span></span><br /><span data-ttu-id="11a3f-337">Si se cumple alguna de las entradas de hello **indefinido** o tipo que no sea un valor booleano, será el resultado de hello **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="11a3f-337">If any of hello inputs is **undefined** or type other than Boolean, then hello result will be **undefined**.</span></span>|  
|<span data-ttu-id="11a3f-338">**de comparación**</span><span class="sxs-lookup"><span data-stu-id="11a3f-338">**comparison**</span></span>|<span data-ttu-id="11a3f-339">El operador espera que las entradas toohave Hola mismo tipo y no sean sin definir.</span><span class="sxs-lookup"><span data-stu-id="11a3f-339">Operator expects input(s) toohave hello same type and not be undefined.</span></span> <span data-ttu-id="11a3f-340">La salida es un booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-340">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="11a3f-341">Si se cumple alguna de las entradas de hello **indefinido** u Hola entradas tienen tipos diferentes, el resultado de hello es **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="11a3f-341">If any of hello inputs is **undefined** or hello inputs have different types, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="11a3f-342">Consulte la tabla **Ordenación de los valores para la comparación** para conocer los detalles de ordenación de los valores.</span><span class="sxs-lookup"><span data-stu-id="11a3f-342">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="11a3f-343">**cadena**</span><span class="sxs-lookup"><span data-stu-id="11a3f-343">**string**</span></span>|<span data-ttu-id="11a3f-344">El operador espera que las entradas toobe cadenas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-344">Operator expects input(s) toobe String(s).</span></span> <span data-ttu-id="11a3f-345">La salida también es una cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-345">Output is also a String.</span></span><br /><span data-ttu-id="11a3f-346">Si se cumple alguna de las entradas de hello **indefinido** o es de tipo que no sea resultado de cadena, a continuación, hello **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="11a3f-346">If any of hello inputs is **undefined** or type other than String then hello result is **undefined**.</span></span>|  
  
 <span data-ttu-id="11a3f-347">**Operadores unarios:**</span><span class="sxs-lookup"><span data-stu-id="11a3f-347">**Unary operators:**</span></span>  
  
|<span data-ttu-id="11a3f-348">**Name**</span><span class="sxs-lookup"><span data-stu-id="11a3f-348">**Name**</span></span>|<span data-ttu-id="11a3f-349">**Operador**</span><span class="sxs-lookup"><span data-stu-id="11a3f-349">**Operator**</span></span>|<span data-ttu-id="11a3f-350">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="11a3f-350">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="11a3f-351">**aritméticos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-351">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="11a3f-352">Devuelve el valor número Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-352">Returns hello number value.</span></span><br /><br /> <span data-ttu-id="11a3f-353">Negativos bit a bit.</span><span class="sxs-lookup"><span data-stu-id="11a3f-353">Bitwise negation.</span></span> <span data-ttu-id="11a3f-354">Devuelve el valor numérico negativo.</span><span class="sxs-lookup"><span data-stu-id="11a3f-354">Returns negated number value.</span></span>|  
|<span data-ttu-id="11a3f-355">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="11a3f-355">**bitwise**</span></span>|~|<span data-ttu-id="11a3f-356">Complemento de uno.</span><span class="sxs-lookup"><span data-stu-id="11a3f-356">Ones' complement.</span></span> <span data-ttu-id="11a3f-357">Devuelve un complemento de un valor numérico.</span><span class="sxs-lookup"><span data-stu-id="11a3f-357">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="11a3f-358">**lógicos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-358">**Logical**</span></span>|<span data-ttu-id="11a3f-359">**NOT**</span><span class="sxs-lookup"><span data-stu-id="11a3f-359">**NOT**</span></span>|<span data-ttu-id="11a3f-360">Negación.</span><span class="sxs-lookup"><span data-stu-id="11a3f-360">Negation.</span></span> <span data-ttu-id="11a3f-361">Devuelve el valor booleano negativo.</span><span class="sxs-lookup"><span data-stu-id="11a3f-361">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="11a3f-362">**Operadores binarios:**</span><span class="sxs-lookup"><span data-stu-id="11a3f-362">**Binary operators:**</span></span>  
  
|<span data-ttu-id="11a3f-363">**Name**</span><span class="sxs-lookup"><span data-stu-id="11a3f-363">**Name**</span></span>|<span data-ttu-id="11a3f-364">**Operador**</span><span class="sxs-lookup"><span data-stu-id="11a3f-364">**Operator**</span></span>|<span data-ttu-id="11a3f-365">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="11a3f-365">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="11a3f-366">**aritméticos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-366">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="11a3f-367">Suma.</span><span class="sxs-lookup"><span data-stu-id="11a3f-367">Addition.</span></span><br /><br /> <span data-ttu-id="11a3f-368">Resta.</span><span class="sxs-lookup"><span data-stu-id="11a3f-368">Subtraction.</span></span><br /><br /> <span data-ttu-id="11a3f-369">Multiplicación.</span><span class="sxs-lookup"><span data-stu-id="11a3f-369">Multiplication.</span></span><br /><br /> <span data-ttu-id="11a3f-370">División.</span><span class="sxs-lookup"><span data-stu-id="11a3f-370">Division.</span></span><br /><br /> <span data-ttu-id="11a3f-371">Modulación.</span><span class="sxs-lookup"><span data-stu-id="11a3f-371">Modulation.</span></span>|  
|<span data-ttu-id="11a3f-372">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="11a3f-372">**bitwise**</span></span>|<span data-ttu-id="11a3f-373">&#124;</span><span class="sxs-lookup"><span data-stu-id="11a3f-373">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="11a3f-374">OR bit a bit.</span><span class="sxs-lookup"><span data-stu-id="11a3f-374">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="11a3f-375">AND bit a bit.</span><span class="sxs-lookup"><span data-stu-id="11a3f-375">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="11a3f-376">XOR bit a bit.</span><span class="sxs-lookup"><span data-stu-id="11a3f-376">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="11a3f-377">Desplazamiento a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="11a3f-377">Left Shift.</span></span><br /><br /> <span data-ttu-id="11a3f-378">Desplazamiento a la derecha.</span><span class="sxs-lookup"><span data-stu-id="11a3f-378">Right Shift.</span></span><br /><br /> <span data-ttu-id="11a3f-379">Desplazamiento a la derecha con relleno de ceros.</span><span class="sxs-lookup"><span data-stu-id="11a3f-379">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="11a3f-380">**lógicos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-380">**logical**</span></span>|<span data-ttu-id="11a3f-381">**AND**</span><span class="sxs-lookup"><span data-stu-id="11a3f-381">**AND**</span></span><br /><br /> <span data-ttu-id="11a3f-382">**O bien**</span><span class="sxs-lookup"><span data-stu-id="11a3f-382">**OR**</span></span>|<span data-ttu-id="11a3f-383">Conjunción lógica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-383">Logical conjunction.</span></span> <span data-ttu-id="11a3f-384">Devuelve **true** si ambos argumentos son **true**, devuelve **false** en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="11a3f-384">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="11a3f-385">Conjunción lógica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-385">Logical conjunction.</span></span> <span data-ttu-id="11a3f-386">Devuelve **true** si ambos argumentos son **true**, devuelve **false** en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="11a3f-386">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="11a3f-387">**de comparación**</span><span class="sxs-lookup"><span data-stu-id="11a3f-387">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="11a3f-388">**!=, &lt;&gt;**</span><span class="sxs-lookup"><span data-stu-id="11a3f-388">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="11a3f-389">**??**</span><span class="sxs-lookup"><span data-stu-id="11a3f-389">**??**</span></span>|<span data-ttu-id="11a3f-390">Igual a.</span><span class="sxs-lookup"><span data-stu-id="11a3f-390">Equals.</span></span> <span data-ttu-id="11a3f-391">Devuelve **true** si ambos argumentos son iguales, en caso contrario, devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="11a3f-391">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="11a3f-392">Diferente de.</span><span class="sxs-lookup"><span data-stu-id="11a3f-392">Not equal to.</span></span> <span data-ttu-id="11a3f-393">Devuelve **true** si ambos argumentos no son iguales, en caso contrario, devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="11a3f-393">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="11a3f-394">Mayor que.</span><span class="sxs-lookup"><span data-stu-id="11a3f-394">Greater Than.</span></span> <span data-ttu-id="11a3f-395">Devuelve **true** si el primer argumento es mayor que otra de Hola, devolver **false** en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="11a3f-395">Returns **true** if first argument is greater than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="11a3f-396">Mayor o igual que.</span><span class="sxs-lookup"><span data-stu-id="11a3f-396">Greater Than or Equal To.</span></span> <span data-ttu-id="11a3f-397">Devuelve **true** si el primer argumento es mayor o igual a otra toohello, devolver **false** en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="11a3f-397">Returns **true** if first argument is greater than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="11a3f-398">Menor que.</span><span class="sxs-lookup"><span data-stu-id="11a3f-398">Less Than.</span></span> <span data-ttu-id="11a3f-399">Devuelve **true** si el primer argumento es menor que otra de Hola, devolver **false** en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="11a3f-399">Returns **true** if first argument is less than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="11a3f-400">Menor o igual que.</span><span class="sxs-lookup"><span data-stu-id="11a3f-400">Less Than or Equal To.</span></span> <span data-ttu-id="11a3f-401">Devuelve **true** si el primer argumento es menor o igual toohello segundo uno, devuelto **false** en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="11a3f-401">Returns **true** if first argument is less than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="11a3f-402">Fusionar.</span><span class="sxs-lookup"><span data-stu-id="11a3f-402">Coalesce.</span></span> <span data-ttu-id="11a3f-403">Devuelve Hola segundo argumento si Hola primer argumento es un **indefinido** valor.</span><span class="sxs-lookup"><span data-stu-id="11a3f-403">Returns hello second argument if hello first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="11a3f-404">**String**</span><span class="sxs-lookup"><span data-stu-id="11a3f-404">**String**</span></span>|<span data-ttu-id="11a3f-405">**&amp;#124;&amp;#124;**</span><span class="sxs-lookup"><span data-stu-id="11a3f-405">**&#124;&#124;**</span></span>|<span data-ttu-id="11a3f-406">Concatenación.</span><span class="sxs-lookup"><span data-stu-id="11a3f-406">Concatenation.</span></span> <span data-ttu-id="11a3f-407">Devuelve una concatenación de ambos argumentos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-407">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="11a3f-408">**Operadores ternarios:**</span><span class="sxs-lookup"><span data-stu-id="11a3f-408">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="11a3f-409">Operador ternario</span><span class="sxs-lookup"><span data-stu-id="11a3f-409">Ternary operator</span></span>|<span data-ttu-id="11a3f-410">?</span><span class="sxs-lookup"><span data-stu-id="11a3f-410">?</span></span>|<span data-ttu-id="11a3f-411">Devuelve Hola segundo argumento si Hola primer argumento se evalúa demasiado**true**; devuelve el tercer argumento de hello en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="11a3f-411">Returns hello second argument if hello first argument evaluates too**true**; return hello third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="11a3f-412">**Ordenación de los valores para la comparación**</span><span class="sxs-lookup"><span data-stu-id="11a3f-412">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="11a3f-413">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="11a3f-413">**Type**</span></span>|<span data-ttu-id="11a3f-414">**Orden de los valores**</span><span class="sxs-lookup"><span data-stu-id="11a3f-414">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="11a3f-415">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="11a3f-415">**Undefined**</span></span>|<span data-ttu-id="11a3f-416">No comparables.</span><span class="sxs-lookup"><span data-stu-id="11a3f-416">Not comparable.</span></span>|  
|<span data-ttu-id="11a3f-417">**Null**</span><span class="sxs-lookup"><span data-stu-id="11a3f-417">**Null**</span></span>|<span data-ttu-id="11a3f-418">Valor único: **null**</span><span class="sxs-lookup"><span data-stu-id="11a3f-418">Single value: **null**</span></span>|  
|<span data-ttu-id="11a3f-419">**Number**</span><span class="sxs-lookup"><span data-stu-id="11a3f-419">**Number**</span></span>|<span data-ttu-id="11a3f-420">Número real natural.</span><span class="sxs-lookup"><span data-stu-id="11a3f-420">Natural real number.</span></span><br /><br /> <span data-ttu-id="11a3f-421">El valor de infinito negativo es menor que cualquier otro valor numérico.</span><span class="sxs-lookup"><span data-stu-id="11a3f-421">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="11a3f-422">El valor de infinito positivo es mayor que cualquier otro valor numérico. El valor **NaN** no es comparable.</span><span class="sxs-lookup"><span data-stu-id="11a3f-422">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="11a3f-423">La comparación con **NaN** dará como resultado el valor **undefined**.</span><span class="sxs-lookup"><span data-stu-id="11a3f-423">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="11a3f-424">**String**</span><span class="sxs-lookup"><span data-stu-id="11a3f-424">**String**</span></span>|<span data-ttu-id="11a3f-425">Orden lexicográfico.</span><span class="sxs-lookup"><span data-stu-id="11a3f-425">Lexicographical order.</span></span>|  
|<span data-ttu-id="11a3f-426">**Array**</span><span class="sxs-lookup"><span data-stu-id="11a3f-426">**Array**</span></span>|<span data-ttu-id="11a3f-427">Ningún orden, pero equitativo.</span><span class="sxs-lookup"><span data-stu-id="11a3f-427">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="11a3f-428">**Object**</span><span class="sxs-lookup"><span data-stu-id="11a3f-428">**Object**</span></span>|<span data-ttu-id="11a3f-429">Ningún orden, pero equitativo.</span><span class="sxs-lookup"><span data-stu-id="11a3f-429">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="11a3f-430">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="11a3f-430">**Remarks**</span></span>  
  
 <span data-ttu-id="11a3f-431">En la base de datos de Azure Cosmos, tipos de Hola de valores a menudo no se conocen hasta que realmente se recuperan de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-431">In Azure Cosmos DB, hello types of values are often not known until they are actually retrieved from hello database.</span></span> <span data-ttu-id="11a3f-432">En orden toosupport una ejecución eficaz de las consultas, la mayoría de los operadores de hello tiene estrictos requisitos de tipos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-432">In order toosupport efficient execution of queries, most of hello operators have strict type requirements.</span></span> <span data-ttu-id="11a3f-433">Además, los operadores por sí mismos no realizan conversiones implícitas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-433">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="11a3f-434">Esto significa que una consulta como: seleccione * FROM ROOT r WHERE r.Age = 21 solo devolverá documentos con la propiedad Age igual toohello número 21.</span><span class="sxs-lookup"><span data-stu-id="11a3f-434">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal toohello number 21.</span></span> <span data-ttu-id="11a3f-435">Documentos con la propiedad Age igual toohello cadena "21" u Hola "0021" no coincidirán, como expresión de Hola "21" = 21 se evalúa como tooundefined.</span><span class="sxs-lookup"><span data-stu-id="11a3f-435">Documents with property Age equal toohello string "21" or hello string "0021" will not match, as hello expression "21" = 21 evaluates tooundefined.</span></span> <span data-ttu-id="11a3f-436">Esto permite un mejor uso de índices, porque búsqueda Hola de un valor específico (es decir, el número 21) es más rápido que busque un número indefinido de coincidencias posibles (es decir, el número 21 o las cadenas "21", "021", "21.0"...).</span><span class="sxs-lookup"><span data-stu-id="11a3f-436">This allows for a better use of indexes, because hello lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="11a3f-437">Esto difiere de la evaluación de los distintos tipos de valores de los operadores en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="11a3f-437">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="11a3f-438">**Comparación e igualdad de objetos y matrices**</span><span class="sxs-lookup"><span data-stu-id="11a3f-438">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="11a3f-439">La comparación de valores de Array u Object mediante los operadores de intervalo (>, > =, <, < =) dará como resultado undefined, ya que no hay orden definido en los valores de Object o Array.</span><span class="sxs-lookup"><span data-stu-id="11a3f-439">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="11a3f-440">Sin embargo, se admite con operadores de igualdad y desigualdad (=,! =, <>) y los valores se compararán estructuralmente.</span><span class="sxs-lookup"><span data-stu-id="11a3f-440">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="11a3f-441">Las matrices son iguales si ambas tienen el mismo número de elementos y los elementos de las posiciones coincidentes también son iguales.</span><span class="sxs-lookup"><span data-stu-id="11a3f-441">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="11a3f-442">Si compara cualquier par de elementos da como resultado sin definir, resultado de hello de comparación de la matriz es indefinido.</span><span class="sxs-lookup"><span data-stu-id="11a3f-442">If comparing any pair of elements results in undefined, hello result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="11a3f-443">Los objetos son iguales si tienen las mismas propiedades definidas y si los valores de las propiedades coincidentes también son iguales.</span><span class="sxs-lookup"><span data-stu-id="11a3f-443">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="11a3f-444">Si compara cualquier par de valores de propiedad da como resultado sin definir, resultado de hello de comparación de objetos es indefinido.</span><span class="sxs-lookup"><span data-stu-id="11a3f-444">If comparing any pair of property values results in undefined, hello result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="11a3f-445"><a name="bk_constants"></a> Constantes</span><span class="sxs-lookup"><span data-stu-id="11a3f-445"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="11a3f-446">Una constante, también conocida como valor literal o escalar, es un símbolo que representa un valor de datos específicos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-446">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="11a3f-447">formato de Hola de una constante depende de tipo de datos de hello del valor de Hola que representa.</span><span class="sxs-lookup"><span data-stu-id="11a3f-447">hello format of a constant depends on hello data type of hello value it represents.</span></span>  
  
 <span data-ttu-id="11a3f-448">**Tipos de datos escalares admitidos:**</span><span class="sxs-lookup"><span data-stu-id="11a3f-448">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="11a3f-449">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="11a3f-449">**Type**</span></span>|<span data-ttu-id="11a3f-450">**Orden de los valores**</span><span class="sxs-lookup"><span data-stu-id="11a3f-450">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="11a3f-451">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="11a3f-451">**Undefined**</span></span>|<span data-ttu-id="11a3f-452">Valor único: **undefined**</span><span class="sxs-lookup"><span data-stu-id="11a3f-452">Single value: **undefined**</span></span>|  
|<span data-ttu-id="11a3f-453">**Null**</span><span class="sxs-lookup"><span data-stu-id="11a3f-453">**Null**</span></span>|<span data-ttu-id="11a3f-454">Valor único: **null**</span><span class="sxs-lookup"><span data-stu-id="11a3f-454">Single value: **null**</span></span>|  
|<span data-ttu-id="11a3f-455">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="11a3f-455">**Boolean**</span></span>|<span data-ttu-id="11a3f-456">Valores: **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="11a3f-456">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="11a3f-457">**Number**</span><span class="sxs-lookup"><span data-stu-id="11a3f-457">**Number**</span></span>|<span data-ttu-id="11a3f-458">Número de punto flotante de precisión doble, estándar IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="11a3f-458">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="11a3f-459">**String**</span><span class="sxs-lookup"><span data-stu-id="11a3f-459">**String**</span></span>|<span data-ttu-id="11a3f-460">Secuencia de cero o más caracteres Unicode.</span><span class="sxs-lookup"><span data-stu-id="11a3f-460">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="11a3f-461">Las cadenas deben ir entre comillas sencillas o dobles.</span><span class="sxs-lookup"><span data-stu-id="11a3f-461">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="11a3f-462">**Array**</span><span class="sxs-lookup"><span data-stu-id="11a3f-462">**Array**</span></span>|<span data-ttu-id="11a3f-463">Secuencia de cero o más elementos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-463">A sequence of zero or more elements.</span></span> <span data-ttu-id="11a3f-464">Cada elemento puede ser un valor de cualquier tipo de datos escalar, excepto Undefined.</span><span class="sxs-lookup"><span data-stu-id="11a3f-464">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="11a3f-465">**Object**</span><span class="sxs-lookup"><span data-stu-id="11a3f-465">**Object**</span></span>|<span data-ttu-id="11a3f-466">Conjunto desordenado de cero o más pares nombre/valor.</span><span class="sxs-lookup"><span data-stu-id="11a3f-466">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="11a3f-467">Nombre es una cadena Unicode, el valor puede ser de cualquier tipo de datos escalar, excepto **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="11a3f-467">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="11a3f-468">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-468">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="11a3f-469">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-469">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="11a3f-470">Representa un valor sin definir de tipo Undefined.</span><span class="sxs-lookup"><span data-stu-id="11a3f-470">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="11a3f-471">Representa el valor **null** de tipo **Null**.</span><span class="sxs-lookup"><span data-stu-id="11a3f-471">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="11a3f-472">Representa la constante de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-472">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="11a3f-473">Representa el valor **false** de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-473">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="11a3f-474">Representa el valor **true** de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-474">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="11a3f-475">Representa una constante.</span><span class="sxs-lookup"><span data-stu-id="11a3f-475">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="11a3f-476">Los literales decimales son números representados mediante notación decimal o científica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-476">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="11a3f-477">Los literales hexadecimales son números representados mediante el prefijo "0x-" seguido de uno o más dígitos hexadecimales.</span><span class="sxs-lookup"><span data-stu-id="11a3f-477">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="11a3f-478">Representa una constante de tipo cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-478">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="11a3f-479">Los literales de cadena son cadenas Unicode representadas por una secuencia de cero o varios caracteres Unicode o secuencias de escape.</span><span class="sxs-lookup"><span data-stu-id="11a3f-479">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="11a3f-480">Los literales de cadena se encierran entre comillas simples (apóstrofo: ') o comillas dobles (comillas: ").</span><span class="sxs-lookup"><span data-stu-id="11a3f-480">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="11a3f-481">Se permiten las secuencias de escape siguientes:</span><span class="sxs-lookup"><span data-stu-id="11a3f-481">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="11a3f-482">**Secuencia de escape**</span><span class="sxs-lookup"><span data-stu-id="11a3f-482">**Escape sequence**</span></span>|<span data-ttu-id="11a3f-483">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="11a3f-483">**Description**</span></span>|<span data-ttu-id="11a3f-484">**Carácter Unicode**</span><span class="sxs-lookup"><span data-stu-id="11a3f-484">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="11a3f-485">\\'</span><span class="sxs-lookup"><span data-stu-id="11a3f-485">\\'</span></span>|<span data-ttu-id="11a3f-486">apóstrofo (')</span><span class="sxs-lookup"><span data-stu-id="11a3f-486">apostrophe (')</span></span>|<span data-ttu-id="11a3f-487">U + 0027</span><span class="sxs-lookup"><span data-stu-id="11a3f-487">U+0027</span></span>|  
|<span data-ttu-id="11a3f-488">\\"</span><span class="sxs-lookup"><span data-stu-id="11a3f-488">\\"</span></span>|<span data-ttu-id="11a3f-489">comillas dobles (")</span><span class="sxs-lookup"><span data-stu-id="11a3f-489">quotation mark (")</span></span>|<span data-ttu-id="11a3f-490">U + 0022</span><span class="sxs-lookup"><span data-stu-id="11a3f-490">U+0022</span></span>|  
|\\\|<span data-ttu-id="11a3f-491">barra inclinada inversa (\\)</span><span class="sxs-lookup"><span data-stu-id="11a3f-491">reverse solidus (\\)</span></span>|<span data-ttu-id="11a3f-492">U + 005C</span><span class="sxs-lookup"><span data-stu-id="11a3f-492">U+005C</span></span>|  
|\\/|<span data-ttu-id="11a3f-493">barra inclinada (/)</span><span class="sxs-lookup"><span data-stu-id="11a3f-493">solidus (/)</span></span>|<span data-ttu-id="11a3f-494">U + 002F</span><span class="sxs-lookup"><span data-stu-id="11a3f-494">U+002F</span></span>|  
|<span data-ttu-id="11a3f-495">\b</span><span class="sxs-lookup"><span data-stu-id="11a3f-495">\b</span></span>|<span data-ttu-id="11a3f-496">retroceso</span><span class="sxs-lookup"><span data-stu-id="11a3f-496">backspace</span></span>|<span data-ttu-id="11a3f-497">U + 0008</span><span class="sxs-lookup"><span data-stu-id="11a3f-497">U+0008</span></span>|  
|<span data-ttu-id="11a3f-498">\f</span><span class="sxs-lookup"><span data-stu-id="11a3f-498">\f</span></span>|<span data-ttu-id="11a3f-499">avance de página</span><span class="sxs-lookup"><span data-stu-id="11a3f-499">form feed</span></span>|<span data-ttu-id="11a3f-500">U + 000C</span><span class="sxs-lookup"><span data-stu-id="11a3f-500">U+000C</span></span>|  
|\n|<span data-ttu-id="11a3f-501">avance de línea</span><span class="sxs-lookup"><span data-stu-id="11a3f-501">line feed</span></span>|<span data-ttu-id="11a3f-502">U + 000A</span><span class="sxs-lookup"><span data-stu-id="11a3f-502">U+000A</span></span>|  
|<span data-ttu-id="11a3f-503">\r</span><span class="sxs-lookup"><span data-stu-id="11a3f-503">\r</span></span>|<span data-ttu-id="11a3f-504">retorno de carro</span><span class="sxs-lookup"><span data-stu-id="11a3f-504">carriage return</span></span>|<span data-ttu-id="11a3f-505">U + 000D</span><span class="sxs-lookup"><span data-stu-id="11a3f-505">U+000D</span></span>|  
|<span data-ttu-id="11a3f-506">\t</span><span class="sxs-lookup"><span data-stu-id="11a3f-506">\t</span></span>|<span data-ttu-id="11a3f-507">tabulador</span><span class="sxs-lookup"><span data-stu-id="11a3f-507">tab</span></span>|<span data-ttu-id="11a3f-508">U + 0009</span><span class="sxs-lookup"><span data-stu-id="11a3f-508">U+0009</span></span>|  
|<span data-ttu-id="11a3f-509">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="11a3f-509">\uXXXX</span></span>|<span data-ttu-id="11a3f-510">Carácter Unicode definidos por 4 dígitos hexadecimales.</span><span class="sxs-lookup"><span data-stu-id="11a3f-510">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="11a3f-511">U + XXXX</span><span class="sxs-lookup"><span data-stu-id="11a3f-511">U+XXXX</span></span>|  
  
##  <span data-ttu-id="11a3f-512"><a name="bk_query_perf_guidelines"></a> Guías de rendimiento de las consultas</span><span class="sxs-lookup"><span data-stu-id="11a3f-512"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="11a3f-513">En orden para un toobe consulta ejecutado eficazmente para una colección de gran tamaño, debe utilizar filtros que pueden obtenerse a través de uno o más índices.</span><span class="sxs-lookup"><span data-stu-id="11a3f-513">In order for a query toobe executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="11a3f-514">Hola después de filtros se considerará de búsqueda del índice:</span><span class="sxs-lookup"><span data-stu-id="11a3f-514">hello following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="11a3f-515">Utilice el operador de igualdad (=) con expresiones de ruta de acceso de documentos y constantes.</span><span class="sxs-lookup"><span data-stu-id="11a3f-515">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="11a3f-516">Utilice los operadores de intervalo (<, \<=, >, >=) con expresiones de ruta de acceso de documentos y constantes numéricas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-516">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="11a3f-517">Expresión de ruta de acceso de documento indica cualquier expresión que identifica una ruta de acceso constante en documentos de Hola de colección de la base de datos de hello al que hace referencia.</span><span class="sxs-lookup"><span data-stu-id="11a3f-517">Document path expression stands for any expression which identifies a constant path in hello documents from hello referenced database collection.</span></span>  
  
 <span data-ttu-id="11a3f-518">**Expresión de ruta de acceso de documento**</span><span class="sxs-lookup"><span data-stu-id="11a3f-518">**Document path expression**</span></span>  
  
 <span data-ttu-id="11a3f-519">Las expresiones de ruta de acceso de documento son expresiones que evalúan la ruta de una propiedad o un indexador de matrices en un documento procedente de la colección de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-519">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="11a3f-520">Esta ruta de acceso puede ser usado tooidentify Hola ubicación de valores que se hace referencia en un filtro directamente dentro de los documentos de hello en la colección de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-520">This path can be used tooidentify hello location of values referenced in a filter directly within hello documents in hello database collection.</span></span>  
  
 <span data-ttu-id="11a3f-521">Para que una expresión toobe considera una expresión de ruta de acceso del documento, debe:</span><span class="sxs-lookup"><span data-stu-id="11a3f-521">For an expression toobe considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="11a3f-522">Referencia Hola raíz directamente.</span><span class="sxs-lookup"><span data-stu-id="11a3f-522">Reference hello collection root directly.</span></span>  
  
2.  <span data-ttu-id="11a3f-523">Hacer referencia al indexador de matrices de propiedad o constantes de alguna expresión de ruta de acceso de documento.</span><span class="sxs-lookup"><span data-stu-id="11a3f-523">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="11a3f-524">Hacer referencia a un alias, que represente alguna expresión de ruta de acceso de documento.</span><span class="sxs-lookup"><span data-stu-id="11a3f-524">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="11a3f-525">**Convenciones de sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-525">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="11a3f-526">Hello en la tabla siguiente describe la sintaxis de toodescribe de hello convenciones utilizadas en la referencia del lenguaje de consulta de API de documentos Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-526">hello following table describes hello conventions used toodescribe syntax in hello DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="11a3f-527">**Convención**</span><span class="sxs-lookup"><span data-stu-id="11a3f-527">**Convention**</span></span>|<span data-ttu-id="11a3f-528">**Se usa para**</span><span class="sxs-lookup"><span data-stu-id="11a3f-528">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="11a3f-529">MAYÚSCULAS</span><span class="sxs-lookup"><span data-stu-id="11a3f-529">UPPERCASE</span></span>|<span data-ttu-id="11a3f-530">Palabras clave sin distinción entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-530">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="11a3f-531">minúsculas</span><span class="sxs-lookup"><span data-stu-id="11a3f-531">lowercase</span></span>|<span data-ttu-id="11a3f-532">Palabras clave con distinción entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-532">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="11a3f-533">\<noterminal&gt;</span><span class="sxs-lookup"><span data-stu-id="11a3f-533">\<nonterminal></span></span>|<span data-ttu-id="11a3f-534">Elemento no terminal, se define por separado.</span><span class="sxs-lookup"><span data-stu-id="11a3f-534">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="11a3f-535">\<noterminal&gt; ::=</span><span class="sxs-lookup"><span data-stu-id="11a3f-535">\<nonterminal> ::=</span></span>|<span data-ttu-id="11a3f-536">Definición de la sintaxis de elemento no Terminal de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-536">Syntax definition of hello nonterminal.</span></span>|  
    |<span data-ttu-id="11a3f-537">otro_terminal</span><span class="sxs-lookup"><span data-stu-id="11a3f-537">other_terminal</span></span>|<span data-ttu-id="11a3f-538">Terminal (token), se describe detalladamente en palabras.</span><span class="sxs-lookup"><span data-stu-id="11a3f-538">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="11a3f-539">identificador</span><span class="sxs-lookup"><span data-stu-id="11a3f-539">identifier</span></span>|<span data-ttu-id="11a3f-540">Identificador.</span><span class="sxs-lookup"><span data-stu-id="11a3f-540">Identifier.</span></span> <span data-ttu-id="11a3f-541">Solo admite los caracteres siguientes:, a-z, A-Z, 0-9 _El primer carácter no puede ser un dígito.</span><span class="sxs-lookup"><span data-stu-id="11a3f-541">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="11a3f-542">"cadena"</span><span class="sxs-lookup"><span data-stu-id="11a3f-542">"string"</span></span>|<span data-ttu-id="11a3f-543">Cadena entrecomillada.</span><span class="sxs-lookup"><span data-stu-id="11a3f-543">Quoted string.</span></span> <span data-ttu-id="11a3f-544">Permite cualquier cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-544">Allows any valid string.</span></span> <span data-ttu-id="11a3f-545">Vea la descripción de string_literal.</span><span class="sxs-lookup"><span data-stu-id="11a3f-545">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="11a3f-546">'símbolo'</span><span class="sxs-lookup"><span data-stu-id="11a3f-546">'symbol'</span></span>|<span data-ttu-id="11a3f-547">Símbolo literal que forma parte de la sintaxis de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-547">Literal symbol which is part of hello syntax.</span></span>|  
    |<span data-ttu-id="11a3f-548">&#124; (barra vertical)</span><span class="sxs-lookup"><span data-stu-id="11a3f-548">&#124; (vertical bar)</span></span>|<span data-ttu-id="11a3f-549">Alternativas para los elementos de la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="11a3f-549">Alternatives for syntax items.</span></span> <span data-ttu-id="11a3f-550">Puede usar solo uno de los elementos de hello especificados.</span><span class="sxs-lookup"><span data-stu-id="11a3f-550">You can use only one of hello items specified.</span></span>|  
    |<span data-ttu-id="11a3f-551">[] /(corchetes)</span><span class="sxs-lookup"><span data-stu-id="11a3f-551">[ ] /(brackets)</span></span>|<span data-ttu-id="11a3f-552">Los corchetes contienen uno o varios elementos opcionales.</span><span class="sxs-lookup"><span data-stu-id="11a3f-552">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="11a3f-553">[, ...n]</span><span class="sxs-lookup"><span data-stu-id="11a3f-553">[ ,...n ]</span></span>|<span data-ttu-id="11a3f-554">Indica Hola anterior elemento se puede repetir n número de veces.</span><span class="sxs-lookup"><span data-stu-id="11a3f-554">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="11a3f-555">Hola elementos se separan por comas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-555">hello occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="11a3f-556">[ ...n]</span><span class="sxs-lookup"><span data-stu-id="11a3f-556">[ ...n ]</span></span>|<span data-ttu-id="11a3f-557">Indica Hola anterior elemento se puede repetir n número de veces.</span><span class="sxs-lookup"><span data-stu-id="11a3f-557">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="11a3f-558">elementos de Hola se separan mediante espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="11a3f-558">hello occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="11a3f-559"><a name="bk_built_in_functions"></a> Funciones integradas</span><span class="sxs-lookup"><span data-stu-id="11a3f-559"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="11a3f-560">Azure Cosmos DB proporciona muchas funciones de SQL integradas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-560">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="11a3f-561">categorías de Hola de funciones integradas se enumeran a continuación.</span><span class="sxs-lookup"><span data-stu-id="11a3f-561">hello categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="11a3f-562">Función</span><span class="sxs-lookup"><span data-stu-id="11a3f-562">Function</span></span>|<span data-ttu-id="11a3f-563">Descripción</span><span class="sxs-lookup"><span data-stu-id="11a3f-563">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="11a3f-564">Funciones matemáticas</span><span class="sxs-lookup"><span data-stu-id="11a3f-564">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="11a3f-565">Hola funciones matemáticas cada realizan un cálculo, normalmente basado en valores de entrada que se proporcionan como argumentos y devuelven un valor numérico.</span><span class="sxs-lookup"><span data-stu-id="11a3f-565">hello mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="11a3f-566">Funciones de comprobación de tipos</span><span class="sxs-lookup"><span data-stu-id="11a3f-566">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="11a3f-567">funciones de comprobación de tipo Hello permiten a tipo de hello toocheck de una expresión dentro de las consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="11a3f-567">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="11a3f-568">Funciones de cadena</span><span class="sxs-lookup"><span data-stu-id="11a3f-568">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="11a3f-569">funciones de cadena de Hello realizan una operación sobre un valor de cadena de entrada y devuelven una cadena, valor numérico o booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-569">hello string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="11a3f-570">Funciones de matriz</span><span class="sxs-lookup"><span data-stu-id="11a3f-570">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="11a3f-571">funciones de matriz de Hello realizan una operación en un valor de matriz de entrada y devuelven numérico, un valor booleano o de matriz.</span><span class="sxs-lookup"><span data-stu-id="11a3f-571">hello array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="11a3f-572">Funciones espaciales</span><span class="sxs-lookup"><span data-stu-id="11a3f-572">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="11a3f-573">funciones espaciales Hola realizan una operación sobre un valor de entrada de objeto espacial y devuelven un valor numérico o booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-573">hello spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="11a3f-574"><a name="bk_mathematical_functions"></a> Funciones matemáticas</span><span class="sxs-lookup"><span data-stu-id="11a3f-574"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="11a3f-575">Hello siguientes funciones realizan un cálculo, normalmente basado en valores de entrada que se proporcionan como argumentos y devuelven un valor numérico.</span><span class="sxs-lookup"><span data-stu-id="11a3f-575">hello following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="11a3f-576">ABS</span><span class="sxs-lookup"><span data-stu-id="11a3f-576">ABS</span></span>](#bk_abs)|[<span data-ttu-id="11a3f-577">ACOS</span><span class="sxs-lookup"><span data-stu-id="11a3f-577">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="11a3f-578">ASIN</span><span class="sxs-lookup"><span data-stu-id="11a3f-578">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="11a3f-579">ATAN</span><span class="sxs-lookup"><span data-stu-id="11a3f-579">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="11a3f-580">ATN2</span><span class="sxs-lookup"><span data-stu-id="11a3f-580">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="11a3f-581">CEILING</span><span class="sxs-lookup"><span data-stu-id="11a3f-581">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="11a3f-582">COS</span><span class="sxs-lookup"><span data-stu-id="11a3f-582">COS</span></span>](#bk_cos)|[<span data-ttu-id="11a3f-583">COT</span><span class="sxs-lookup"><span data-stu-id="11a3f-583">COT</span></span>](#bk_cot)|[<span data-ttu-id="11a3f-584">DEGREES</span><span class="sxs-lookup"><span data-stu-id="11a3f-584">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="11a3f-585">EXP</span><span class="sxs-lookup"><span data-stu-id="11a3f-585">EXP</span></span>](#bk_exp)|[<span data-ttu-id="11a3f-586">FLOOR</span><span class="sxs-lookup"><span data-stu-id="11a3f-586">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="11a3f-587">LOG</span><span class="sxs-lookup"><span data-stu-id="11a3f-587">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="11a3f-588">LOG10</span><span class="sxs-lookup"><span data-stu-id="11a3f-588">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="11a3f-589">PI</span><span class="sxs-lookup"><span data-stu-id="11a3f-589">PI</span></span>](#bk_pi)|[<span data-ttu-id="11a3f-590">POWER</span><span class="sxs-lookup"><span data-stu-id="11a3f-590">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="11a3f-591">RADIANS</span><span class="sxs-lookup"><span data-stu-id="11a3f-591">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="11a3f-592">ROUND</span><span class="sxs-lookup"><span data-stu-id="11a3f-592">ROUND</span></span>](#bk_round)|[<span data-ttu-id="11a3f-593">SIN</span><span class="sxs-lookup"><span data-stu-id="11a3f-593">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="11a3f-594">SQRT</span><span class="sxs-lookup"><span data-stu-id="11a3f-594">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="11a3f-595">SQUARE</span><span class="sxs-lookup"><span data-stu-id="11a3f-595">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="11a3f-596">SIGN</span><span class="sxs-lookup"><span data-stu-id="11a3f-596">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="11a3f-597">TAN</span><span class="sxs-lookup"><span data-stu-id="11a3f-597">TAN</span></span>](#bk_tan)|[<span data-ttu-id="11a3f-598">TRUNC</span><span class="sxs-lookup"><span data-stu-id="11a3f-598">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="11a3f-599"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="11a3f-599"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="11a3f-600">Devuelve Hola valor absoluto (positivo) de hello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-600">Returns hello absolute (positive) value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-601">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-601">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-602">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-602">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-603">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-603">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-604">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-604">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-605">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-605">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-606">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-606">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-607">Hello en el ejemplo siguiente se muestra los resultados de Hola de usar la función hello ABS en tres números distintos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-607">hello following example shows hello results of using hello ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="11a3f-608">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-608">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="11a3f-609"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="11a3f-609"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="11a3f-610">Ángulo de hello devuelve, en radianes, cuyo coseno es Hola expresión numérica especificada; También se denomina arco coseno.</span><span class="sxs-lookup"><span data-stu-id="11a3f-610">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="11a3f-611">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-611">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-612">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-612">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-613">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-613">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-614">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-614">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-615">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-615">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-616">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-616">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-617">Hello en el ejemplo siguiente se devuelve Hola ACOS de -1.</span><span class="sxs-lookup"><span data-stu-id="11a3f-617">hello following example returns hello ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="11a3f-618">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-618">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="11a3f-619"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="11a3f-619"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="11a3f-620">Ángulo de hello devuelve, en radianes, cuyo seno es hello especifica expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-620">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="11a3f-621">También se denomina arcoseno.</span><span class="sxs-lookup"><span data-stu-id="11a3f-621">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="11a3f-622">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-622">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-623">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-624">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-625">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-625">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-626">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-627">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-627">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-628">Hello en el ejemplo siguiente se devuelve Hola ASIN de -1.</span><span class="sxs-lookup"><span data-stu-id="11a3f-628">hello following example returns hello ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="11a3f-629">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-629">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="11a3f-630"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="11a3f-630"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="11a3f-631">Ángulo de hello devuelve, en radianes, cuya tangente es hello especifica expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-631">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="11a3f-632">También se denomina arcotangente.</span><span class="sxs-lookup"><span data-stu-id="11a3f-632">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="11a3f-633">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-633">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-634">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-635">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-636">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-636">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-637">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-638">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-638">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-639">Hola siguiente ejemplo devuelve Hola ATAN de hello valor especificado.</span><span class="sxs-lookup"><span data-stu-id="11a3f-639">hello following example returns hello ATAN of hello specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="11a3f-640">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-640">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="11a3f-641"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="11a3f-641"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="11a3f-642">Devuelve el valor de entidad de seguridad de Hola de hello arco tangente de y/x x, expresado en radianes.</span><span class="sxs-lookup"><span data-stu-id="11a3f-642">Returns hello principal value of hello arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="11a3f-643">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-643">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-644">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-644">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-645">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-645">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-646">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-646">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-647">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-647">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-648">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-648">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-649">Hello en el ejemplo siguiente se calcula hello ATN2 para hello especificado x e y componentes.</span><span class="sxs-lookup"><span data-stu-id="11a3f-649">hello following example calculates hello ATN2 for hello specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="11a3f-650">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-650">Here is hello result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="11a3f-651"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="11a3f-651"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="11a3f-652">Devuelve Hola valor entero más pequeño mayor o igual a, Hola expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="11a3f-652">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-653">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-653">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-654">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-654">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-655">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-655">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-656">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-656">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-657">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-657">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-658">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-658">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-659">Hola siguiente ejemplo muestra numéricos positivos, negativos y valores cero con Hola función CEILING.</span><span class="sxs-lookup"><span data-stu-id="11a3f-659">hello following example shows positive numeric, negative, and zero values with hello CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="11a3f-660">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-660">Here is hello result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="11a3f-661"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="11a3f-661"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="11a3f-662">Devuelve Hola coseno trigonométrico Hola especifica el ángulo, en radianes, en hello expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="11a3f-662">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="11a3f-663">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-663">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-664">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-664">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-665">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-665">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-666">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-666">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-667">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-667">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-668">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-668">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-669">Hola siguiente ejemplo calcula Hola COS de hello especifica el ángulo.</span><span class="sxs-lookup"><span data-stu-id="11a3f-669">hello following example calculates hello COS of hello specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="11a3f-670">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-670">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="11a3f-671"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="11a3f-671"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="11a3f-672">Devuelve Hola cotangente trigonométrica Hola especifica el ángulo, en radianes, en hello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-672">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-673">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-673">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-674">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-674">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-675">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-675">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-676">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-676">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-677">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-677">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-678">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-678">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-679">Hola siguiente ejemplo calcula Hola COT del ángulo especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-679">hello following example calculates hello COT of hello specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="11a3f-680">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-680">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="11a3f-681"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="11a3f-681"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="11a3f-682">Devuelve Hola ángulo correspondiente en grados para un ángulo especificado en radianes.</span><span class="sxs-lookup"><span data-stu-id="11a3f-682">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="11a3f-683">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-683">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-684">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-684">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-685">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-685">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-686">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-686">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-687">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-687">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-688">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-688">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-689">Hello en el ejemplo siguiente se devuelve Hola número de grados en un ángulo de PI/2 radianes.</span><span class="sxs-lookup"><span data-stu-id="11a3f-689">hello following example returns hello number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="11a3f-690">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-690">Here is hello result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="11a3f-691"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="11a3f-691"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="11a3f-692">Devuelve Hola mayor entero menor o igual toohello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-692">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-693">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-693">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-694">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-694">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-695">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-695">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-696">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-696">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-697">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-697">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-698">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-698">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-699">Hola siguiente ejemplo muestra numéricos positivos, negativos y cero valores con Hola FLOOR (función).</span><span class="sxs-lookup"><span data-stu-id="11a3f-699">hello following example shows positive numeric, negative, and zero values with hello FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="11a3f-700">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-700">Here is hello result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="11a3f-701"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="11a3f-701"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="11a3f-702">Devuelve Hola valor exponencial de hello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-702">Returns hello exponential value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-703">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-703">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-704">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-704">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-705">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-705">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-706">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-706">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-707">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-707">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-708">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="11a3f-708">**Remarks**</span></span>  
  
 <span data-ttu-id="11a3f-709">constante de Hello **e** (2,718281 …) es Hola base de los logaritmos naturales.</span><span class="sxs-lookup"><span data-stu-id="11a3f-709">hello constant **e** (2.718281…), is hello base of natural logarithms.</span></span>  
  
 <span data-ttu-id="11a3f-710">Hello exponente de un número es constante de hello **e** genera potencia de toohello de número de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-710">hello exponent of a number is hello constant **e** raised toohello power of hello number.</span></span> <span data-ttu-id="11a3f-711">Por ejemplo EXP(1,0) = e^1,0 = 2,718 281 828 459 05 y EXP(10) = e^10 = 22 026,465 794 806 7.</span><span class="sxs-lookup"><span data-stu-id="11a3f-711">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="11a3f-712">Hola valor exponencial del logaritmo natural de Hola de un número es el número de hello propio: EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="11a3f-712">hello exponential of hello natural logarithm of a number is hello number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="11a3f-713">Logaritmo natural de Hola de hello exponencial de un número es el número de hello propio: LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="11a3f-713">And hello natural logarithm of hello exponential of a number is hello number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="11a3f-714">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-714">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-715">Hello en el ejemplo siguiente se declara una variable y devuelve el valor exponencial de saludo de la variable especificada de hello (10).</span><span class="sxs-lookup"><span data-stu-id="11a3f-715">hello following example declares a variable and returns hello exponential value of hello specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="11a3f-716">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-716">Here is hello result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="11a3f-717">Hello en el ejemplo siguiente se devuelve Hola valor exponencial del logaritmo natural de Hola de 20 y el logaritmo natural de Hola de hello exponencial de 20.</span><span class="sxs-lookup"><span data-stu-id="11a3f-717">hello following example returns hello exponential value of hello natural logarithm of 20 and hello natural logarithm of hello exponential of 20.</span></span> <span data-ttu-id="11a3f-718">Dado que estas funciones son funciones inversas entre sí, valor devuelto de hello con redondeo para matemáticas en ambos casos son 20 de punto flotante.</span><span class="sxs-lookup"><span data-stu-id="11a3f-718">Because these functions are inverse functions of one another, hello return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="11a3f-719">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-719">Here is hello result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="11a3f-720"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="11a3f-720"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="11a3f-721">Devuelve el logaritmo de natural de Hola de hello especificado expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-721">Returns hello natural logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-722">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-722">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="11a3f-723">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-723">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-724">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-724">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="11a3f-725">Argumento numérico opcional que establece base logaritmo Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-725">Optional numeric argument that sets hello base for hello logarithm.</span></span>  
  
 <span data-ttu-id="11a3f-726">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-726">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-727">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-727">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-728">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="11a3f-728">**Remarks**</span></span>  
  
 <span data-ttu-id="11a3f-729">De forma predeterminada, LOG() devuelve el logaritmo natural de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-729">By default, LOG() returns hello natural logarithm.</span></span> <span data-ttu-id="11a3f-730">Puede cambiar Hola base del valor de hello logaritmo tooanother mediante el uso del parámetro base opcional Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-730">You can change hello base of hello logarithm tooanother value by using hello optional base parameter.</span></span>  
  
 <span data-ttu-id="11a3f-731">logaritmo natural de Hello es Hola logaritmo toohello base **e**, donde **e** es un too2.718281828 aproximadamente igual constante irracional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-731">hello natural logarithm is hello logarithm toohello base **e**, where **e** is an irrational constant approximately equal too2.718281828.</span></span>  
  
 <span data-ttu-id="11a3f-732">logaritmo natural de Hola de hello exponencial de un número es el número de hello propio: LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="11a3f-732">hello natural logarithm of hello exponential of a number is hello number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="11a3f-733">Hola valor exponencial del logaritmo natural de Hola de un número es el número de hello propio: EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="11a3f-733">And hello exponential of hello natural logarithm of a number is hello number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="11a3f-734">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-734">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-735">Hello en el ejemplo siguiente se declara una variable y devuelve Hola logaritmo valor de la variable especificada de hello (10).</span><span class="sxs-lookup"><span data-stu-id="11a3f-735">hello following example declares a variable and returns hello logarithm value of hello specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="11a3f-736">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-736">Here is hello result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="11a3f-737">Hello en el ejemplo siguiente se calcula Hola registro exponente Hola de un número.</span><span class="sxs-lookup"><span data-stu-id="11a3f-737">hello following example calculates hello LOG for hello exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="11a3f-738">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-738">Here is hello result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="11a3f-739"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="11a3f-739"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="11a3f-740">Devuelve el logaritmo de base 10 de Hola de hello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-740">Returns hello base-10 logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-741">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-741">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-742">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-742">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-743">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-743">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-744">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-744">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-745">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-745">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-746">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="11a3f-746">**Remarks**</span></span>  
  
 <span data-ttu-id="11a3f-747">Hola LOG10 y funciones POWER están relacionada inversamente tooone otro.</span><span class="sxs-lookup"><span data-stu-id="11a3f-747">hello LOG10 and POWER functions are inversely related tooone another.</span></span> <span data-ttu-id="11a3f-748">Por ejemplo, 10 ^ LOG10 (n) = n.</span><span class="sxs-lookup"><span data-stu-id="11a3f-748">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="11a3f-749">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-749">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-750">Hello en el ejemplo siguiente se declara una variable y devuelve Hola LOG10 valor de la variable especificada de hello (100).</span><span class="sxs-lookup"><span data-stu-id="11a3f-750">hello following example declares a variable and returns hello LOG10 value of hello specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="11a3f-751">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-751">Here is hello result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="11a3f-752"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="11a3f-752"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="11a3f-753">Devuelve Hola valor constante de PI.</span><span class="sxs-lookup"><span data-stu-id="11a3f-753">Returns hello constant value of PI.</span></span>  
  
 <span data-ttu-id="11a3f-754">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-754">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="11a3f-755">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-755">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-756">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-756">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-757">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-757">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-758">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-758">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-759">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-759">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-760">Hello en el ejemplo siguiente se devuelve el valor de Hola de PI.</span><span class="sxs-lookup"><span data-stu-id="11a3f-760">hello following example returns hello value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="11a3f-761">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-761">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="11a3f-762"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="11a3f-762"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="11a3f-763">Devuelve Hola valo Hola especificado expresión toohello potencia especificada.</span><span class="sxs-lookup"><span data-stu-id="11a3f-763">Returns hello value of hello specified expression toohello specified power.</span></span>  
  
 <span data-ttu-id="11a3f-764">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-764">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="11a3f-765">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-765">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-766">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-766">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="11a3f-767">Es Hola power toowhich tooraise `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="11a3f-767">Is hello power toowhich tooraise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="11a3f-768">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-768">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-769">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-770">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-770">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-771">Hola de ejemplo siguiente se muestra cómo elevar números toohello potencia de 3 (Hola cubo del número de hello).</span><span class="sxs-lookup"><span data-stu-id="11a3f-771">hello following example demonstrates raising a number toohello power of 3 (hello cube of hello number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="11a3f-772">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-772">Here is hello result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="11a3f-773"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="11a3f-773"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="11a3f-774">Devuelve radianes cuando se especifica una expresión numérica en grados.</span><span class="sxs-lookup"><span data-stu-id="11a3f-774">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="11a3f-775">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-775">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-776">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-777">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-777">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-778">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-778">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-779">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-779">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-780">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-780">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-781">Hello en el ejemplo siguiente se toma unos ángulos como entrada y devuelve sus correspondientes valores en radianes.</span><span class="sxs-lookup"><span data-stu-id="11a3f-781">hello following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="11a3f-782">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-782">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="11a3f-783"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="11a3f-783"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="11a3f-784">Devuelve un valor numérico, redondeado toohello valor de entero más cercano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-784">Returns a numeric value, rounded toohello closest integer value.</span></span>  
  
 <span data-ttu-id="11a3f-785">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-785">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-786">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-786">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-787">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-787">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-788">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-788">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-789">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-789">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-790">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-790">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-791">Hello en el ejemplo siguiente se redondea Hola después toohello números positivos y negativos al entero más próximo.</span><span class="sxs-lookup"><span data-stu-id="11a3f-791">hello following example rounds hello following positive and negative numbers toohello nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="11a3f-792">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-792">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="11a3f-793"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="11a3f-793"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="11a3f-794">Devuelve Hola positivo (+ 1), cero (0), o signo negativo (-1) de hello especificado expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-794">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-795">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-795">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-796">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-796">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-797">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-797">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-798">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-798">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-799">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-799">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-800">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-800">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-801">Hello en el ejemplo siguiente se devuelve valores de inicio de sesión de Hola de números de-2 too2.</span><span class="sxs-lookup"><span data-stu-id="11a3f-801">hello following example returns hello SIGN values of numbers from -2 too2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="11a3f-802">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-802">Here is hello result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="11a3f-803"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="11a3f-803"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="11a3f-804">Devuelve Hola seno trigonométrico Hola especifica el ángulo, en radianes, en hello expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="11a3f-804">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="11a3f-805">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-805">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-806">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-806">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-807">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-807">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-808">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-808">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-809">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-809">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-810">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-810">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-811">Hola siguiente ejemplo calcula Hola seno del ángulo especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-811">hello following example calculates hello SIN of hello specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="11a3f-812">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-812">Here is hello result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="11a3f-813"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="11a3f-813"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="11a3f-814">Devuelve Hola cuadrado raíz de hello especifica el valor numérico.</span><span class="sxs-lookup"><span data-stu-id="11a3f-814">Returns hello square root of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="11a3f-815">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-815">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-816">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-816">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-817">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-817">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-818">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-818">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-819">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-819">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-820">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-820">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-821">Hello en el ejemplo siguiente se devuelve raíces cuadradas de Hola de números 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="11a3f-821">hello following example returns hello square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="11a3f-822">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-822">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="11a3f-823"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="11a3f-823"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="11a3f-824">Hola devuelve cuadrado de hello especifica el valor numérico.</span><span class="sxs-lookup"><span data-stu-id="11a3f-824">Returns hello square of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="11a3f-825">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-825">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-826">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-826">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-827">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-827">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-828">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-828">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-829">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-829">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-830">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-830">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-831">Hello en el ejemplo siguiente se devuelve cuadrados Hola de números 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="11a3f-831">hello following example returns hello squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="11a3f-832">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-832">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="11a3f-833"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="11a3f-833"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="11a3f-834">Tangente de hello devuelve de hello especifica el ángulo, en radianes, en hello expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="11a3f-834">Returns hello tangent of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="11a3f-835">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-835">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-836">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-836">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-837">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-837">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-838">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-838">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-839">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-839">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-840">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-840">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-841">Hello en el ejemplo siguiente se calcula tangente de Hola de PI () / 2.</span><span class="sxs-lookup"><span data-stu-id="11a3f-841">hello following example calculates hello tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="11a3f-842">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-842">Here is hello result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="11a3f-843"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="11a3f-843"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="11a3f-844">Devuelve un valor numérico, el valor entero más cercano de toohello truncado.</span><span class="sxs-lookup"><span data-stu-id="11a3f-844">Returns a numeric value, truncated toohello closest integer value.</span></span>  
  
 <span data-ttu-id="11a3f-845">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-845">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="11a3f-846">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-846">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="11a3f-847">Es una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-847">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-848">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-848">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-849">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-849">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-850">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-850">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-851">Hola de ejemplo siguiente trunca Hola siguientes números positivos y negativos toohello valor entero más cercano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-851">hello following example truncates hello following positive and negative numbers toohello nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="11a3f-852">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-852">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="11a3f-853"><a name="bk_type_checking_functions"></a> Funciones de comprobación de tipos</span><span class="sxs-lookup"><span data-stu-id="11a3f-853"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="11a3f-854">Hello siguientes funciones admiten la comprobación de tipos contra valores de entrada y devuelven un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-854">hello following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="11a3f-855">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="11a3f-855">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="11a3f-856">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="11a3f-856">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="11a3f-857">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="11a3f-857">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="11a3f-858">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="11a3f-858">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="11a3f-859">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="11a3f-859">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="11a3f-860">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="11a3f-860">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="11a3f-861">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="11a3f-861">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="11a3f-862">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="11a3f-862">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="11a3f-863"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="11a3f-863"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="11a3f-864">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es una matriz.</span><span class="sxs-lookup"><span data-stu-id="11a3f-864">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span>  
  
 <span data-ttu-id="11a3f-865">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-865">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="11a3f-866">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-866">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="11a3f-867">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-867">Is any valid expression.</span></span>  
  
 <span data-ttu-id="11a3f-868">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-868">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-869">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-869">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-870">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-870">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-871">Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_ARRAY.</span><span class="sxs-lookup"><span data-stu-id="11a3f-871">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="11a3f-872">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-872">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="11a3f-873"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="11a3f-873"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="11a3f-874">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-874">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="11a3f-875">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-875">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="11a3f-876">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-876">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="11a3f-877">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-877">Is any valid expression.</span></span>  
  
 <span data-ttu-id="11a3f-878">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-878">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-879">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-879">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-880">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-880">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-881">Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_BOOL.</span><span class="sxs-lookup"><span data-stu-id="11a3f-881">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="11a3f-882">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-882">Here is hello result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="11a3f-883"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="11a3f-883"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="11a3f-884">Devuelve un valor booleano que indica si la propiedad de Hola se ha asignado un valor.</span><span class="sxs-lookup"><span data-stu-id="11a3f-884">Returns a Boolean indicating if hello property has been assigned a value.</span></span>  
  
 <span data-ttu-id="11a3f-885">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-885">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="11a3f-886">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-886">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="11a3f-887">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-887">Is any valid expression.</span></span>  
  
 <span data-ttu-id="11a3f-888">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-888">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-889">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-889">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-890">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-890">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-891">Hola siguiendo en el ejemplo se comprueba presencia de Hola de una propiedad dentro de hello había especificado documento JSON.</span><span class="sxs-lookup"><span data-stu-id="11a3f-891">hello following example checks for hello presence of a property within hello specified JSON document.</span></span> <span data-ttu-id="11a3f-892">Hola primero devuelve true, ya que "a" está presente, pero Hola segundo devuelve false porque "b" no está presente.</span><span class="sxs-lookup"><span data-stu-id="11a3f-892">hello first returns true since "a" is present, but hello second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="11a3f-893">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-893">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="11a3f-894"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="11a3f-894"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="11a3f-895">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es null.</span><span class="sxs-lookup"><span data-stu-id="11a3f-895">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span>  
  
 <span data-ttu-id="11a3f-896">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-896">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="11a3f-897">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="11a3f-898">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="11a3f-899">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-899">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-900">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-901">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-901">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-902">Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="11a3f-902">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="11a3f-903">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-903">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="11a3f-904"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="11a3f-904"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="11a3f-905">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un número.</span><span class="sxs-lookup"><span data-stu-id="11a3f-905">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span>  
  
 <span data-ttu-id="11a3f-906">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-906">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="11a3f-907">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-907">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="11a3f-908">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-908">Is any valid expression.</span></span>  
  
 <span data-ttu-id="11a3f-909">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-909">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-910">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-910">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-911">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-911">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-912">Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="11a3f-912">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="11a3f-913">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-913">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="11a3f-914"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="11a3f-914"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="11a3f-915">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="11a3f-915">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="11a3f-916">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-916">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="11a3f-917">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-917">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="11a3f-918">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-918">Is any valid expression.</span></span>  
  
 <span data-ttu-id="11a3f-919">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-919">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-920">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-920">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-921">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-921">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-922">Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_OBJECT.</span><span class="sxs-lookup"><span data-stu-id="11a3f-922">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="11a3f-923">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-923">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="11a3f-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="11a3f-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="11a3f-925">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un tipo primitivo (cadena, booleano, numérico o null).</span><span class="sxs-lookup"><span data-stu-id="11a3f-925">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="11a3f-926">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-926">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="11a3f-927">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-927">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="11a3f-928">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-928">Is any valid expression.</span></span>  
  
 <span data-ttu-id="11a3f-929">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-929">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-930">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-930">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-931">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-931">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-932">Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_PRIMITIVE.</span><span class="sxs-lookup"><span data-stu-id="11a3f-932">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="11a3f-933">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-933">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="11a3f-934"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="11a3f-934"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="11a3f-935">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es una cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-935">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span>  
  
 <span data-ttu-id="11a3f-936">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-936">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="11a3f-937">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-937">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="11a3f-938">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-938">Is any valid expression.</span></span>  
  
 <span data-ttu-id="11a3f-939">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-939">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-940">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-940">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-941">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-941">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-942">Hello en el ejemplo siguiente se comprueba objetos de JSON Boolean, number, string, null, objeto, matriz y tipos sin definir mediante Hola función IS_STRING.</span><span class="sxs-lookup"><span data-stu-id="11a3f-942">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="11a3f-943">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-943">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="11a3f-944"><a name="bk_string_functions"></a> Funciones de cadena</span><span class="sxs-lookup"><span data-stu-id="11a3f-944"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="11a3f-945">Hola siguientes funciones escalares realizan una operación sobre un valor de cadena de entrada y devuelven una cadena, valor numérico o booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-945">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="11a3f-946">CONCAT</span><span class="sxs-lookup"><span data-stu-id="11a3f-946">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="11a3f-947">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="11a3f-947">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="11a3f-948">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="11a3f-948">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="11a3f-949">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="11a3f-949">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="11a3f-950">LEFT</span><span class="sxs-lookup"><span data-stu-id="11a3f-950">LEFT</span></span>](#bk_left)|[<span data-ttu-id="11a3f-951">LENGTH</span><span class="sxs-lookup"><span data-stu-id="11a3f-951">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="11a3f-952">LOWER</span><span class="sxs-lookup"><span data-stu-id="11a3f-952">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="11a3f-953">LTRIM</span><span class="sxs-lookup"><span data-stu-id="11a3f-953">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="11a3f-954">REPLACE</span><span class="sxs-lookup"><span data-stu-id="11a3f-954">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="11a3f-955">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="11a3f-955">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="11a3f-956">REVERSE</span><span class="sxs-lookup"><span data-stu-id="11a3f-956">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="11a3f-957">RIGHT</span><span class="sxs-lookup"><span data-stu-id="11a3f-957">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="11a3f-958">RTRIM</span><span class="sxs-lookup"><span data-stu-id="11a3f-958">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="11a3f-959">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="11a3f-959">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="11a3f-960">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="11a3f-960">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="11a3f-961">UPPER</span><span class="sxs-lookup"><span data-stu-id="11a3f-961">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="11a3f-962"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="11a3f-962"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="11a3f-963">Devuelve una cadena que es el resultado de hello de concatenar dos o más valores de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-963">Returns a string that is hello result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="11a3f-964">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-964">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="11a3f-965">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-965">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-966">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-966">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-967">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-967">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-968">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-968">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-969">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-969">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-970">Hola siguiendo en el ejemplo se devuelve una cadena concatenada de Hola de hello valores especificados.</span><span class="sxs-lookup"><span data-stu-id="11a3f-970">hello following example returns hello concatenated string of hello specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="11a3f-971">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-971">Here is hello result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="11a3f-972"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="11a3f-972"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="11a3f-973">Devuelve un valor booleano que indica si primera expresión de cadena hello contiene hello en segundo lugar.</span><span class="sxs-lookup"><span data-stu-id="11a3f-973">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span>  
  
 <span data-ttu-id="11a3f-974">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-974">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="11a3f-975">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-975">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-976">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-976">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-977">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-977">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-978">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-978">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-979">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-979">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-980">Hello en el ejemplo siguiente se comprueba si "abc" contiene "ab" y contiene "d".</span><span class="sxs-lookup"><span data-stu-id="11a3f-980">hello following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="11a3f-981">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-981">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="11a3f-982"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="11a3f-982"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="11a3f-983">Devuelve un valor booleano que indica si primera expresión de cadena Hola termina con hello en segundo lugar.</span><span class="sxs-lookup"><span data-stu-id="11a3f-983">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span>  
  
 <span data-ttu-id="11a3f-984">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-984">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="11a3f-985">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-985">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-986">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-986">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-987">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-987">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-988">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-988">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-989">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-989">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-990">Hello en el ejemplo siguiente se devuelve Hola "abc" termina con "b" y "bc".</span><span class="sxs-lookup"><span data-stu-id="11a3f-990">hello following example returns hello "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="11a3f-991">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-991">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="11a3f-992"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="11a3f-992"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="11a3f-993">Devuelve Hola a partir de la posición de la primera aparición de hello de la segunda expresión de cadena Hola dentro de la primera expresión de cadena especificada de hello, o -1 si no se encuentra la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-993">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>  
  
 <span data-ttu-id="11a3f-994">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-994">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="11a3f-995">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-995">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-996">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-996">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-997">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-997">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-998">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-998">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-999">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-999">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1000">Hello en el ejemplo siguiente se devuelve el índice de Hola de varias subcadenas dentro de "abc".</span><span class="sxs-lookup"><span data-stu-id="11a3f-1000">hello following example returns hello index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="11a3f-1001">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1001">Here is hello result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="11a3f-1002"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="11a3f-1002"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="11a3f-1003">Devuelve Hola parte izquierda de una cadena con hello especificada número de caracteres.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1003">Returns hello left part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="11a3f-1004">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1004">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="11a3f-1005">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1005">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1006">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1006">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="11a3f-1007">Es cualquier expresión numérica válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1007">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-1008">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1008">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1009">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1009">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1010">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1010">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1011">Hello en el ejemplo siguiente se devuelve Hola izquierda de "abc" para distintos valores de longitud.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1011">hello following example returns hello left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="11a3f-1012">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1012">Here is hello result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="11a3f-1013"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="11a3f-1013"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="11a3f-1014">Devuelve el número de caracteres de Hola Hola especificado expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1014">Returns hello number of characters of hello specified string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1015">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1015">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="11a3f-1016">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1016">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1017">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1017">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1018">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1018">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1019">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1019">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1020">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1020">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1021">Hello en el ejemplo siguiente se devuelve Hola longitud de una cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1021">hello following example returns hello length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="11a3f-1022">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1022">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="11a3f-1023"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="11a3f-1023"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="11a3f-1024">Devuelve una expresión de cadena después de convertir toolowercase de datos de caracteres en mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1024">Returns a string expression after converting uppercase character data toolowercase.</span></span>  
  
 <span data-ttu-id="11a3f-1025">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1025">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="11a3f-1026">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1026">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1027">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1027">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1028">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1028">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1029">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1029">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1030">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1030">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1031">Hola siguiente ejemplo se muestra cómo toouse inferior en una consulta.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1031">hello following example shows how toouse LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="11a3f-1032">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1032">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="11a3f-1033"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="11a3f-1033"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="11a3f-1034">Devuelve una expresión de cadena después de quitar los espacios en blanco iniciales.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1034">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="11a3f-1035">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1035">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="11a3f-1036">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1036">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1037">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1037">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1038">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1038">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1039">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1039">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1040">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1040">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1041">Hola siguiente ejemplo se muestra cómo toouse LTRIM dentro de una consulta.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1041">hello following example shows how toouse LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="11a3f-1042">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1042">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="11a3f-1043"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="11a3f-1043"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="11a3f-1044">Reemplaza todas las apariciones de un valor de cadena especificado por otro valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1044">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="11a3f-1045">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1045">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="11a3f-1046">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1046">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1047">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1047">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1048">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1048">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1049">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1049">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1050">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1050">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1051">Hola de ejemplo siguiente muestra cómo reemplazar el toouse en una consulta.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1051">hello following example shows how toouse REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="11a3f-1052">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1052">Here is hello result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="11a3f-1053"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="11a3f-1053"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="11a3f-1054">Repite un valor de cadena un número especificado de veces.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1054">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="11a3f-1055">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1055">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="11a3f-1056">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1056">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1057">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1057">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="11a3f-1058">Es cualquier expresión numérica válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1058">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-1059">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1059">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1060">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1060">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1061">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1061">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1062">Hola de ejemplo siguiente muestra cómo REPLICAR toouse en una consulta.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1062">hello following example shows how toouse REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="11a3f-1063">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1063">Here is hello result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="11a3f-1064"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="11a3f-1064"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="11a3f-1065">Devuelve Hola invirtiendo el orden de un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1065">Returns hello reverse order of a string value.</span></span>  
  
 <span data-ttu-id="11a3f-1066">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1066">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="11a3f-1067">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1067">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1068">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1068">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1069">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1069">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1070">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1070">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1071">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1071">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1072">Hola de ejemplo siguiente muestra cómo toouse INVERTIR en una consulta.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1072">hello following example shows how toouse REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="11a3f-1073">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1073">Here is hello result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="11a3f-1074"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="11a3f-1074"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="11a3f-1075">Hola devuelve parte derecha de una cadena con hello del número de caracteres especificado.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1075">Returns hello right part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="11a3f-1076">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1076">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="11a3f-1077">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1077">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1078">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1078">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="11a3f-1079">Es cualquier expresión numérica válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1079">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-1080">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1080">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1081">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1081">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1082">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1082">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1083">Hello en el ejemplo siguiente se devuelve Hola la parte derecha de "abc" para distintos valores de longitud.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1083">hello following example returns hello right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="11a3f-1084">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1084">Here is hello result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="11a3f-1085"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="11a3f-1085"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="11a3f-1086">Devuelve una expresión de cadena después de quitar los espacios en blanco finales.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1086">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="11a3f-1087">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1087">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="11a3f-1088">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1088">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1089">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1089">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1090">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1090">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1091">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1091">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1092">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1092">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1093">Hola siguiente ejemplo se muestra cómo toouse RTRIM dentro de una consulta.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1093">hello following example shows how toouse RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="11a3f-1094">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1094">Here is hello result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="11a3f-1095"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="11a3f-1095"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="11a3f-1096">Devuelve un valor booleano que indica si primera expresión de cadena Hola empieza por hello en segundo lugar.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1096">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span>  
  
 <span data-ttu-id="11a3f-1097">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1097">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="11a3f-1098">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1098">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1099">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1099">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1100">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1100">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1101">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1101">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-1102">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1102">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1103">Hello el ejemplo siguiente se comprueba si hello cadena "abc" comienza con "b" y "a".</span><span class="sxs-lookup"><span data-stu-id="11a3f-1103">hello following example checks if hello string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="11a3f-1104">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1104">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="11a3f-1105"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="11a3f-1105"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="11a3f-1106">Devuelve parte de una expresión de cadena a partir de hello especifica la posición de base cero del carácter y continúa toohello especifica la longitud o toohello final de cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1106">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span>  
  
 <span data-ttu-id="11a3f-1107">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1107">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="11a3f-1108">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1108">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1109">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1109">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="11a3f-1110">Es cualquier expresión numérica válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1110">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-1111">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1111">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1112">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1112">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1113">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1113">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1114">Hello en el ejemplo siguiente se devuelve Hola subcadena de "abc" comienza en 1 y una longitud de 1 carácter.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1114">hello following example returns hello substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="11a3f-1115">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1115">Here is hello result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="11a3f-1116"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="11a3f-1116"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="11a3f-1117">Devuelve una expresión de cadena después de convertir toouppercase de datos de carácter en minúscula.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1117">Returns a string expression after converting lowercase character data toouppercase.</span></span>  
  
 <span data-ttu-id="11a3f-1118">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1118">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="11a3f-1119">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1119">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="11a3f-1120">Es cualquier expresión de cadena válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1120">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1121">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1121">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1122">Devuelve una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1122">Returns a string expression.</span></span>  
  
 <span data-ttu-id="11a3f-1123">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1123">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1124">Hola siguiente ejemplo se muestra cómo toouse superior en una consulta</span><span class="sxs-lookup"><span data-stu-id="11a3f-1124">hello following example shows how toouse UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="11a3f-1125">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1125">Here is hello result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="11a3f-1126"><a name="bk_array_functions"></a> Funciones de matriz</span><span class="sxs-lookup"><span data-stu-id="11a3f-1126"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="11a3f-1127">Hola siguientes funciones escalares realiza una operación sobre un valor de entrada de matriz y devolución numérico, booleano o matriz.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1127">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="11a3f-1128">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="11a3f-1128">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="11a3f-1129">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="11a3f-1129">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="11a3f-1130">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="11a3f-1130">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="11a3f-1131">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="11a3f-1131">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="11a3f-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="11a3f-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="11a3f-1133">Devuelve una matriz que es el resultado de hello de concatenar dos o más valores de la matriz.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1133">Returns an array that is hello result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="11a3f-1134">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1134">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="11a3f-1135">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1135">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="11a3f-1136">Es cualquier expresión de matriz válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1136">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="11a3f-1137">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1137">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1138">Devuelve una expresión de matriz.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1138">Returns an array expression.</span></span>  
  
 <span data-ttu-id="11a3f-1139">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1139">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1140">Hola después ejemplo cómo tooconcatenate dos matrices.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1140">hello following example how tooconcatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="11a3f-1141">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1141">Here is hello result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="11a3f-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="11a3f-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="11a3f-1143">Devuelve un valor booleano que indica si la matriz de hello contiene Hola valor especificado.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1143">Returns a Boolean indicating whether hello array contains hello specified value.</span></span>  
  
 <span data-ttu-id="11a3f-1144">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1144">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="11a3f-1145">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1145">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="11a3f-1146">Es cualquier expresión de matriz válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1146">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="11a3f-1147">Es cualquier expresión válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1147">Is any valid expression.</span></span>  
  
 <span data-ttu-id="11a3f-1148">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1148">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1149">Devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1149">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="11a3f-1150">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1150">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1151">Hola siguiente ejemplo de cómo toocheck pertenencia a una matriz usar ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1151">hello following example how toocheck for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="11a3f-1152">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1152">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="11a3f-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="11a3f-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="11a3f-1154">Devuelve el número de elementos de Hola Hola especifica la expresión de matriz.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1154">Returns hello number of elements of hello specified array expression.</span></span>  
  
 <span data-ttu-id="11a3f-1155">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1155">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="11a3f-1156">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1156">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="11a3f-1157">Es cualquier expresión de matriz válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1157">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="11a3f-1158">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1158">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1159">Devuelve una expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1159">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-1160">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1160">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1161">Hola después ejemplo cómo tooget Hola longitud de una matriz usar ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1161">hello following example how tooget hello length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="11a3f-1162">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1162">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="11a3f-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="11a3f-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="11a3f-1164">Devuelve parte de una expresión de matriz.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1164">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="11a3f-1165">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1165">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="11a3f-1166">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1166">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="11a3f-1167">Es cualquier expresión de matriz válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1167">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="11a3f-1168">Es cualquier expresión numérica válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1168">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="11a3f-1169">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1169">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1170">Devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1170">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="11a3f-1171">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1171">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1172">Hola siguiente ejemplo de cómo tooget una parte de una matriz usar ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1172">hello following example how tooget a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="11a3f-1173">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1173">Here is hello result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="11a3f-1174"><a name="bk_spatial_functions"></a> Funciones espaciales</span><span class="sxs-lookup"><span data-stu-id="11a3f-1174"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="11a3f-1175">Hola siguientes funciones escalares realizan una operación sobre un valor de entrada de objeto espacial y devuelven un valor numérico o booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1175">hello following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="11a3f-1176">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="11a3f-1176">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="11a3f-1177">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="11a3f-1177">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="11a3f-1178">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="11a3f-1178">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="11a3f-1179">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="11a3f-1179">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="11a3f-1180">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="11a3f-1180">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="11a3f-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="11a3f-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="11a3f-1182">Devuelve la distancia de hello entre expresiones de punto de GeoJSON, polígono o LineString Hola dos.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1182">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="11a3f-1183">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1183">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="11a3f-1184">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1184">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="11a3f-1185">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1185">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="11a3f-1186">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1186">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1187">Devuelve una expresión numérica que contiene la distancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1187">Returns a numeric expression containing hello distance.</span></span> <span data-ttu-id="11a3f-1188">Esto se expresa en metros Hola predeterminado sistema de referencia.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1188">This is expressed in meters for hello default reference system.</span></span>  
  
 <span data-ttu-id="11a3f-1189">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1189">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1190">Hola siguiente ejemplo se muestra cómo tooreturn todos los documentos de familia que están dentro de 30 km de hello especificado ubicación mediante la función integrada de hello ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1190">hello following example shows how tooreturn all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> <span data-ttu-id="11a3f-1191">.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1191">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="11a3f-1192">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1192">Here is hello result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="11a3f-1193"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="11a3f-1193"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="11a3f-1194">Devuelve una expresión booleana que indica si hello GeoJSON el objeto (punto, polígono o LineString) especificado en el primer argumento de hello es dentro de hello GeoJSON (punto, polígono o LineString) en el segundo argumento de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1194">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument is within hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="11a3f-1195">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1195">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="11a3f-1196">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1196">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="11a3f-1197">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="11a3f-1198">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1198">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="11a3f-1199">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1199">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1200">Devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1200">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="11a3f-1201">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1201">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1202">Hola de ejemplo siguiente muestra cómo toofind familia de todos los documentos dentro de un polígono con ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1202">hello following example shows how toofind all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="11a3f-1203">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1203">Here is hello result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="11a3f-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="11a3f-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="11a3f-1205">Devuelve una expresión booleana que indica si el objeto de la GeoJSON de hello (punto, polígono o LineString) especificado en el primer argumento de hello superpuesto hello GeoJSON (punto, polígono o LineString) en el segundo argumento de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1205">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument intersects hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="11a3f-1206">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1206">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="11a3f-1207">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1207">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="11a3f-1208">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="11a3f-1209">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1209">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="11a3f-1210">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1210">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1211">Devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1211">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="11a3f-1212">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1212">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1213">Hola siguiente ejemplo se muestra cómo toofind todas las áreas que forma una intersección con Hola especificado polígono.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1213">hello following example shows how toofind all areas that intersects with hello given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="11a3f-1214">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1214">Here is hello result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="11a3f-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="11a3f-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="11a3f-1216">Devuelve un valor booleano que indica si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1216">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="11a3f-1217">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1217">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="11a3f-1218">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1218">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="11a3f-1219">Es cualquier expresión válida de objeto de tipo Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1219">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="11a3f-1220">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1220">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1221">Devuelve una expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1221">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="11a3f-1222">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1222">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1223">Hola siguiente ejemplo se muestra cómo toocheck si un punto es válido utilizando ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1223">hello following example shows how toocheck if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="11a3f-1224">Por ejemplo, este punto tiene un valor de latitud que no está en el intervalo válido de Hola de valores [-90, 90], Hola por lo que la consulta devuelve false.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1224">For example, this point has a latitude value that's not in hello valid range of values [-90, 90], so hello query returns false.</span></span>  
  
 <span data-ttu-id="11a3f-1225">Para los polígonos, hello GeoJSON especificación requiere que debe ser proporcionado de par de coordenadas última Hola Hola igual como hello en primer lugar, toocreate una forma cerrada.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1225">For polygons, hello GeoJSON specification requires that hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span> <span data-ttu-id="11a3f-1226">El orden de los puntos dentro de un polígono debe especificarse siguiendo el sentido contrario al de las agujas del reloj.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1226">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="11a3f-1227">Un polígono especificado en el orden de las agujas del reloj representa inverso de Hola de región de hello dentro de él.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1227">A polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="11a3f-1228">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1228">Here is hello result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="11a3f-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="11a3f-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="11a3f-1230">Devuelve un valor JSON que contiene un valor booleano si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida y si no es válido, además Hola motivo como un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1230">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="11a3f-1231">**Sintaxis**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1231">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="11a3f-1232">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1232">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="11a3f-1233">Es cualquier expresión válida de objeto Point o Polygon de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1233">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="11a3f-1234">**Tipos de valor devuelto**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1234">**Return Types**</span></span>  
  
 <span data-ttu-id="11a3f-1235">Devuelve un valor JSON que contiene un valor booleano si Hola especifica el punto de GeoJSON o expresión de polígono es válida y, si no es válido, además Hola motivo como un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1235">Returns a JSON value containing a Boolean value if hello specified GeoJSON point or polygon expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="11a3f-1236">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="11a3f-1236">**Examples**</span></span>  
  
 <span data-ttu-id="11a3f-1237">Hola siguiente ejemplo de cómo toocheck validez (con detalles) mediante ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1237">hello following example how toocheck validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="11a3f-1238">Este es el conjunto de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3f-1238">Here is hello result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="11a3f-1239">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="11a3f-1239">Next steps</span></span>  
 <span data-ttu-id="11a3f-1240">[Sintaxis SQL y consulta SQL para Azure Cosmos DB](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="11a3f-1240">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="11a3f-1241">Documentación sobre Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="11a3f-1241">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
