---
title: "características de JSON de la base de datos de SQL aaaAzure | Documentos de Microsoft"
description: "La base de datos de SQL Azure le permite tooparse, consulta y datos de formato de notación de JavaScript Object Notation (JSON)."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 55860105-2f5f-4b10-87a0-99faa32b5653
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.date: 11/15/2016
ms.author: jovanpop
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 30a31a1b01482ec276646b6fd6ca0c1f581168d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="e6b2c-103">Introducción a las características de JSON en Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="e6b2c-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="e6b2c-104">Base de datos SQL de Azure permite analizar y consultar datos representados en formato de notación de objetos JavaScript [(JSON)](http://www.json.org/) , y exportar los datos relacionales como texto JSON.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="e6b2c-105">JSON es un formato de datos conocido que se usa para intercambiar datos en aplicaciones web y móviles modernas.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="e6b2c-106">JSON también se utiliza para almacenar datos semiestructurados en archivos de registro o en bases de datos NoSQL como [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="e6b2c-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="e6b2c-107">Muchos servicios web REST devuelven resultados con formato de texto JSON o aceptan datos con ese formato.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="e6b2c-108">La mayoría de los servicios de Azure, como [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/) y [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/), tienen puntos de conexión REST que devuelven o consumen JSON.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="e6b2c-109">Base de datos SQL de Azure permite trabajar fácilmente con datos JSON e integrar su base de datos con servicios modernos.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="e6b2c-110">Información general</span><span class="sxs-lookup"><span data-stu-id="e6b2c-110">Overview</span></span>
<span data-ttu-id="e6b2c-111">La base de datos de SQL Azure proporciona Hola siguientes funciones para trabajar con datos JSON:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-111">Azure SQL Database provides hello following functions for working with JSON data:</span></span>

![Funciones JSON](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="e6b2c-113">Si tiene texto JSON, puede extraer datos de JSON o compruebe que JSON es el formato correcto mediante el uso de funciones integradas de hello [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), y [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e6b2c-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using hello built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="e6b2c-114">Hola [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) función le permite actualizar el valor de texto JSON.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="e6b2c-115">Para consultas y análisis más avanzados, la función [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) puede transformar una matriz de objetos JSON en un conjunto de filas.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="e6b2c-116">Cualquier consulta SQL se puede ejecutar en hello devolvió un conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-116">Any SQL query can be executed on hello returned result set.</span></span> <span data-ttu-id="e6b2c-117">Por último, hay una cláusula [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) que permite dar formato de texto JSON a los datos almacenados en las tablas relacionales.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="e6b2c-118">Aplicación del formato JSON a datos relacionales</span><span class="sxs-lookup"><span data-stu-id="e6b2c-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="e6b2c-119">Si tiene un servicio web que toma datos de base de datos de hello las capas y proporciona una respuesta en JSON de formato, o marcos de JavaScript de cliente o bibliotecas que aceptan datos con formato JSON, se puede dar formato al contenido de base de datos como JSON directamente en una consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-119">If you have a web service that takes data from hello database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="e6b2c-120">Ya no tiene código de aplicación de toowrite que da formato a los resultados de la base de datos de SQL de Azure como JSON, o incluye algunos resultados de consulta tabulares JSON tooconvert de biblioteca de serialización y, a continuación, serializar formato tooJSON de objetos.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-120">You no longer have toowrite application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library tooconvert tabular query results and then serialize objects tooJSON format.</span></span> <span data-ttu-id="e6b2c-121">En su lugar, puede usar Hola de resultados de la consulta SQL de JSON cláusula tooformat como JSON en la base de datos de SQL Azure y usarlo directamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-121">Instead, you can use hello FOR JSON clause tooformat SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="e6b2c-122">En el siguiente ejemplo de Hola, se da formato como JSON filas de la tabla Sales.Customer hello mediante el uso de hello cláusula FOR JSON:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-122">In hello following example, rows from hello Sales.Customer table are formatted as JSON by using hello FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="e6b2c-123">cláusula FOR JSON PATH de Hello da formato a resultados de Hola de consulta de hello texto JSON.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-123">hello FOR JSON PATH clause formats hello results of hello query as JSON text.</span></span> <span data-ttu-id="e6b2c-124">Nombres de columna se utilizan como claves, mientras que los valores de celda de Hola se generan como valores JSON:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-124">Column names are used as keys, while hello cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="e6b2c-125">conjunto de resultados de Hola se formatea como una matriz JSON donde cada fila se da formato como un objeto JSON independiente.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-125">hello result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="e6b2c-126">Ruta de acceso indica que puede personalizar Hola el formato de salida de los resultados de JSON usando la notación de puntos en los alias de columna.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-126">PATH indicates that you can customize hello output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="e6b2c-127">Hola después de consulta cambia Hola nombre de clave de "CustomerName" hello en formato JSON de salida de hello y coloca los números de teléfono y fax en subobjeto de Hola "Contacto":</span><span class="sxs-lookup"><span data-stu-id="e6b2c-127">hello following query changes hello name of hello "CustomerName" key in hello output JSON format, and puts phone and fax numbers in hello "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="e6b2c-128">salida de Hello de esta consulta tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-128">hello output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="e6b2c-129">En este ejemplo se devuelve un único objeto JSON en lugar de una matriz mediante la especificación de hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) opción.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-129">In this example we returned a single JSON object instead of an array by specifying hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="e6b2c-130">Puede usar esta opción si sabe que va a devolver un solo objeto como resultado de la consulta.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="e6b2c-131">valor principal de Hola de hello cláusula FOR JSON es que le permite devolver datos jerárquicos complejos de la base de datos con formato de objetos JSON anidados o matrices.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-131">hello main value of hello FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="e6b2c-132">Hola el siguiente ejemplo se muestra cómo ordena tooinclude que pertenecen toohello al cliente como una matriz anidada de pedidos:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-132">hello following example shows how tooinclude Orders that belong toohello Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="e6b2c-133">En lugar de enviar datos de los clientes tooget consultas independientes y, a continuación, toofetch una lista de pedidos relacionados, puede obtener todos los datos necesarios de hello con una sola consulta, como se muestra en la siguiente salida de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-133">Instead of sending separate queries tooget Customer data and then toofetch a list of related Orders, you can get all hello necessary data with a single query, as shown in hello following sample output:</span></span>

```
{
  "Name":"Nada Jovanovic",
  "Phone":"(215) 555-0100",
  "Fax":"(215) 555-0101",
  "Orders":[
    {"OrderID":382,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":395,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":1657,"OrderDate":"2013-01-31","ExpectedDeliveryDate":"2013-02-01"}
]
}
```

## <a name="working-with-json-data"></a><span data-ttu-id="e6b2c-134">Trabajo con datos JSON</span><span class="sxs-lookup"><span data-stu-id="e6b2c-134">Working with JSON data</span></span>
<span data-ttu-id="e6b2c-135">Si no tiene datos estructurados estrictamente, si tiene subobjetos complejas, matrices o datos jerárquicos, o si sus estructuras de datos evolucionan con el tiempo, formato JSON de hello puede ayudarle a toorepresent cualquier estructura de datos complejos.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, hello JSON format can help you toorepresent any complex data structure.</span></span>

<span data-ttu-id="e6b2c-136">JSON es un formato de texto que se puede usar como cualquier otro tipo de cadena en Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="e6b2c-137">Puede enviar o almacenar datos JSON como un tipo NVARCHAR estándar:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

```
CREATE TABLE Products (
  Id int identity primary key,
  Title nvarchar(200),
  Data nvarchar(max)
)
go
CREATE PROCEDURE InsertProduct(@title nvarchar(200), @json nvarchar(max))
AS BEGIN
    insert into Products(Title, Data)
    values(@title, @json)
END
```

<span data-ttu-id="e6b2c-138">Hola datos JSON que se usan en este ejemplo se representa mediante el uso de tipo nvarchar (max) de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-138">hello JSON data used in this example is represented by using hello NVARCHAR(MAX) type.</span></span> <span data-ttu-id="e6b2c-139">JSON se puede insertar en esta tabla o proporcionarse como un argumento de procedimiento Hola almacenado mediante sintaxis de Transact-SQL estándar, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-139">JSON can be inserted into this table or provided as an argument of hello stored procedure using standard Transact-SQL syntax as shown in hello following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="e6b2c-140">Cualquier lenguaje del lado cliente o biblioteca que funcione con datos de cadena en Base de datos SQL de Azure también funciona con datos JSON.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="e6b2c-141">JSON se puede almacenar en cualquier tabla que admite el tipo NVARCHAR de hello, como una tabla optimizada en memoria o una tabla con control de versiones.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-141">JSON can be stored in any table that supports hello NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="e6b2c-142">JSON no incluye ninguna restricción en el código de cliente de Hola o de capa de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-142">JSON does not introduce any constraint either in hello client-side code or in hello database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="e6b2c-143">Consulta de datos JSON</span><span class="sxs-lookup"><span data-stu-id="e6b2c-143">Querying JSON data</span></span>
<span data-ttu-id="e6b2c-144">Si tiene datos con formato JSON almacenados en tablas SQL de Azure, las funciones JSON permiten usarlos en cualquier consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="e6b2c-145">Las funciones JSON que están disponibles en Base de datos SQL de Azure permiten tratar los datos con formato JSON como cualquier otro tipo de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="e6b2c-146">Fácilmente puede extraer valores de hello texto JSON y utilizar datos JSON en cualquier consulta:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-146">You can easily extract values from hello JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="e6b2c-147">Hola función JSON_VALUE extrae un valor de texto JSON almacenado en la columna de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-147">hello JSON_VALUE function extracts a value from JSON text stored in hello Data column.</span></span> <span data-ttu-id="e6b2c-148">Esta función usa un valor de ruta de acceso similar a JavaScript tooreference en tooextract de texto JSON.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-148">This function uses a JavaScript-like path tooreference a value in JSON text tooextract.</span></span> <span data-ttu-id="e6b2c-149">valor de Hello extraído se puede utilizar en cualquier parte de la consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-149">hello extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="e6b2c-150">Hola función JSON_QUERY es tooJSON_VALUE similar.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-150">hello JSON_QUERY function is similar tooJSON_VALUE.</span></span> <span data-ttu-id="e6b2c-151">A diferencia de JSON_VALUE, esta función extrae subobjetos complejos, como matrices u objetos ubicados en texto JSON.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="e6b2c-152">función JSON_MODIFY de Hello le permite especificar la ruta Hola Hola del valor en texto JSON hello que debe actualizarse, así como un nuevo valor que se sobrescribirá Hola antiguo.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-152">hello JSON_MODIFY function lets you specify hello path of hello value in hello JSON text that should be updated, as well as a new value that will overwrite hello old one.</span></span> <span data-ttu-id="e6b2c-153">De esta forma que puede actualizar fácilmente texto JSON sin volver a analizar estructura completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-153">This way you can easily update JSON text without reparsing hello entire structure.</span></span>

<span data-ttu-id="e6b2c-154">Dado que JSON se almacena en un texto estándar, no hay ninguna garantía de que los valores de hello almacenados en columnas de texto son el formato correcto.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-154">Since JSON is stored in a standard text, there are no guarantees that hello values stored in text columns are properly formatted.</span></span> <span data-ttu-id="e6b2c-155">Puede comprobar que el texto almacenado en la columna JSON correctamente con formato estándar hello función ISJSON y restricciones de comprobación de base de datos de SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and hello ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="e6b2c-156">Si el formato del texto de entrada de hello es correcto JSON, Hola función ISJSON devuelve el valor de hello 1.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-156">If hello input text is properly formatted JSON, hello ISJSON function returns hello value 1.</span></span> <span data-ttu-id="e6b2c-157">Con cada inserción o actualización de la columna JSON, esta restricción comprobará que el nuevo valor de texto no tenga un formato JSON incorrecto.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="e6b2c-158">Transformación de JSON en formato tabular</span><span class="sxs-lookup"><span data-stu-id="e6b2c-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="e6b2c-159">Base de datos SQL de Azure también permite transformar las colecciones JSON en formato tabular y cargar o consultar datos JSON.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="e6b2c-160">OPENJSON es una función con valores de tabla que analiza el texto JSON, busca una matriz de objetos JSON, recorre en iteración los elementos de Hola de matriz de Hola y devuelve una fila de resultado de salida de hello para cada elemento de matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through hello elements of hello array, and returns one row in hello output result for each element of hello array.</span></span>

![JSON tabular](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="e6b2c-162">En el ejemplo de Hola anterior, podemos especificar donde toolocate Hola matriz JSON que se debería abrir (en hello $. Ruta de acceso de pedidos), qué columnas se deben devolver como resultado, y donde toofind Hola valores JSON que se devolverán como celdas.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-162">In hello example above, we can specify where toolocate hello JSON array that should be opened (in hello $.Orders path), what columns should be returned as result, and where toofind hello JSON values that will be returned as cells.</span></span>

<span data-ttu-id="e6b2c-163">Se puede transformar una matriz JSON en hello @orders variable en un conjunto de filas, analizar este conjunto de resultados, o insertar filas en una tabla estándar:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-163">We can transform a JSON array in hello @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

```
CREATE PROCEDURE InsertOrders(@orders nvarchar(max))
AS BEGIN

    insert into Orders(Number, Date, Customer, Quantity)
    select Number, Date, Customer, Quantity
    OPENJSON (@orders)
     WITH (
            Number varchar(200),
            Date datetime,
            Customer varchar(200),
            Quantity int
     )

END
```
<span data-ttu-id="e6b2c-164">colección de Hola de pedidos formatea como una matriz JSON y proporcionado como un procedimiento almacenado de toohello de parámetro se pueden analizar e insertar en la tabla de pedidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b2c-164">hello collection of orders formatted as a JSON array and provided as a parameter toohello stored procedure can be parsed and inserted into hello Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6b2c-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e6b2c-165">Next steps</span></span>
<span data-ttu-id="e6b2c-166">toolearn cómo toointegrate JSON en la aplicación, consulte estos recursos:</span><span class="sxs-lookup"><span data-stu-id="e6b2c-166">toolearn how toointegrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="e6b2c-167">Blog de TechNet</span><span class="sxs-lookup"><span data-stu-id="e6b2c-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="e6b2c-168">Documentación de MSDN</span><span class="sxs-lookup"><span data-stu-id="e6b2c-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="e6b2c-169">Vídeo de Channel 9</span><span class="sxs-lookup"><span data-stu-id="e6b2c-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="e6b2c-170">toolearn sobre los distintos escenarios para integrar JSON en la aplicación, vea las demostraciones de hello en este [vídeo de Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) o buscar un escenario que coincida con el caso de uso en [las entradas de Blog de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="e6b2c-170">toolearn about various scenarios for integrating JSON into your application, see hello demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

