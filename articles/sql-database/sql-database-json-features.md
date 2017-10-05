---
title: "Características de JSON en Azure SQL Database | Microsoft Docs"
description: "Base de datos SQL de Azure permite analizar datos, consultarlos y darles formato en notación de objetos JavaScript (JSON)."
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
ms.openlocfilehash: 883e661107dd838f5c381cdef2c7f891b9a9389c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="a576a-103">Introducción a las características de JSON en Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="a576a-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="a576a-104">Base de datos SQL de Azure permite analizar y consultar datos representados en formato de notación de objetos JavaScript [(JSON)](http://www.json.org/) , y exportar los datos relacionales como texto JSON.</span><span class="sxs-lookup"><span data-stu-id="a576a-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="a576a-105">JSON es un formato de datos conocido que se usa para intercambiar datos en aplicaciones web y móviles modernas.</span><span class="sxs-lookup"><span data-stu-id="a576a-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="a576a-106">JSON también se utiliza para almacenar datos semiestructurados en archivos de registro o en bases de datos NoSQL como [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="a576a-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="a576a-107">Muchos servicios web REST devuelven resultados con formato de texto JSON o aceptan datos con ese formato.</span><span class="sxs-lookup"><span data-stu-id="a576a-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="a576a-108">La mayoría de los servicios de Azure, como [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/) y [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/), tienen puntos de conexión REST que devuelven o consumen JSON.</span><span class="sxs-lookup"><span data-stu-id="a576a-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="a576a-109">Base de datos SQL de Azure permite trabajar fácilmente con datos JSON e integrar su base de datos con servicios modernos.</span><span class="sxs-lookup"><span data-stu-id="a576a-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="a576a-110">Información general</span><span class="sxs-lookup"><span data-stu-id="a576a-110">Overview</span></span>
<span data-ttu-id="a576a-111">Base de datos SQL de Azure proporciona las siguientes funciones para trabajar con datos JSON:</span><span class="sxs-lookup"><span data-stu-id="a576a-111">Azure SQL Database provides the following functions for working with JSON data:</span></span>

![Funciones JSON](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="a576a-113">Si tiene texto JSON, puede extraer datos de JSON o comprobar que el formato JSON sea correcto con las funciones integradas [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx) y [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span><span class="sxs-lookup"><span data-stu-id="a576a-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using the built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="a576a-114">La función [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) le permite actualizar valores dentro del texto JSON.</span><span class="sxs-lookup"><span data-stu-id="a576a-114">The [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="a576a-115">Para consultas y análisis más avanzados, la función [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) puede transformar una matriz de objetos JSON en un conjunto de filas.</span><span class="sxs-lookup"><span data-stu-id="a576a-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="a576a-116">Se puede ejecutar cualquier consulta SQL en el conjunto de resultados devuelto.</span><span class="sxs-lookup"><span data-stu-id="a576a-116">Any SQL query can be executed on the returned result set.</span></span> <span data-ttu-id="a576a-117">Por último, hay una cláusula [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) que permite dar formato de texto JSON a los datos almacenados en las tablas relacionales.</span><span class="sxs-lookup"><span data-stu-id="a576a-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="a576a-118">Aplicación del formato JSON a datos relacionales</span><span class="sxs-lookup"><span data-stu-id="a576a-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="a576a-119">Si tiene un servicio web que toma datos del nivel de base de datos y proporciona una respuesta en formato JSON o marcos JavaScript del lado cliente o bibliotecas que aceptan datos con formato JSON, puede dar formato JSON al contenido de la base de datos directamente en una consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="a576a-119">If you have a web service that takes data from the database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="a576a-120">Ya no tiene que escribir código de aplicación para dar formato JSON a los resultados de Base de datos SQL de Azure ni incluir una biblioteca de serialización de JSON para convertir los resultados tabulares de la consulta y después serializar los objetos en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a576a-120">You no longer have to write application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library to convert tabular query results and then serialize objects to JSON format.</span></span> <span data-ttu-id="a576a-121">En su lugar, puede usar la cláusula FOR JSON para dar formato JSON a resultados de consultas SQL en Base de datos SQL de Azure y usarlos directamente en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a576a-121">Instead, you can use the FOR JSON clause to format SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="a576a-122">En el ejemplo siguiente, se aplica el formato JSON a las filas de la tabla Sales.Customers mediante la cláusula FOR JSON:</span><span class="sxs-lookup"><span data-stu-id="a576a-122">In the following example, rows from the Sales.Customer table are formatted as JSON by using the FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="a576a-123">La cláusula FOR JSON PATH da formato de texto JSON a los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="a576a-123">The FOR JSON PATH clause formats the results of the query as JSON text.</span></span> <span data-ttu-id="a576a-124">Los nombres de columna se utilizan como claves, mientras que los valores de celda se generan como valores JSON:</span><span class="sxs-lookup"><span data-stu-id="a576a-124">Column names are used as keys, while the cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="a576a-125">Se da al conjunto de resultados formato de matriz JSON, donde cada fila tiene formato de objeto JSON independiente.</span><span class="sxs-lookup"><span data-stu-id="a576a-125">The result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="a576a-126">PATH indica que puede personalizar el formato de salida de su resultado JSON utilizando la notación de puntos en los alias de columna.</span><span class="sxs-lookup"><span data-stu-id="a576a-126">PATH indicates that you can customize the output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="a576a-127">La consulta siguiente cambia el nombre de la clave "CustomerName" en el formato JSON de salida y coloca los números de teléfono y fax en el subobjeto "Contact":</span><span class="sxs-lookup"><span data-stu-id="a576a-127">The following query changes the name of the "CustomerName" key in the output JSON format, and puts phone and fax numbers in the "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="a576a-128">La salida de esta consulta tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="a576a-128">The output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="a576a-129">En este ejemplo, se devuelve un único objeto JSON en lugar de una matriz al especificarse la opción [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx).</span><span class="sxs-lookup"><span data-stu-id="a576a-129">In this example we returned a single JSON object instead of an array by specifying the [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="a576a-130">Puede usar esta opción si sabe que va a devolver un solo objeto como resultado de la consulta.</span><span class="sxs-lookup"><span data-stu-id="a576a-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="a576a-131">El valor principal de la cláusula FOR JSON es que permite devolver datos jerárquicos complejos desde la base de datos con formato de objetos o matrices JSON anidados.</span><span class="sxs-lookup"><span data-stu-id="a576a-131">The main value of the FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="a576a-132">En el ejemplo siguiente se muestra cómo incluir pedidos (Orders) que pertenecen a un cliente (Customer) como una matriz anidada de pedidos:</span><span class="sxs-lookup"><span data-stu-id="a576a-132">The following example shows how to include Orders that belong to the Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="a576a-133">En lugar de enviar consultas diferentes para obtener los datos del cliente y después recuperar una lista de pedidos relacionados, puede obtener todos los datos necesarios con una única consulta, como se muestra en la siguiente salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a576a-133">Instead of sending separate queries to get Customer data and then to fetch a list of related Orders, you can get all the necessary data with a single query, as shown in the following sample output:</span></span>

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

## <a name="working-with-json-data"></a><span data-ttu-id="a576a-134">Trabajo con datos JSON</span><span class="sxs-lookup"><span data-stu-id="a576a-134">Working with JSON data</span></span>
<span data-ttu-id="a576a-135">Si no tiene datos con una estructura estricta, si tiene subobjetos complejos, matrices o datos jerárquicos, o si sus estructuras de datos evolucionan con el tiempo, el formato JSON puede ayudarlo a representar cualquier estructura de datos compleja.</span><span class="sxs-lookup"><span data-stu-id="a576a-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, the JSON format can help you to represent any complex data structure.</span></span>

<span data-ttu-id="a576a-136">JSON es un formato de texto que se puede usar como cualquier otro tipo de cadena en Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="a576a-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="a576a-137">Puede enviar o almacenar datos JSON como un tipo NVARCHAR estándar:</span><span class="sxs-lookup"><span data-stu-id="a576a-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

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

<span data-ttu-id="a576a-138">Los datos JSON usados en este ejemplo se representan mediante el tipo NVARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="a576a-138">The JSON data used in this example is represented by using the NVARCHAR(MAX) type.</span></span> <span data-ttu-id="a576a-139">Se puede insertar JSON en esta tabla o proporcionarlo como argumento del procedimiento almacenado mediante sintaxis estándar de Transact-SQL, tal como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a576a-139">JSON can be inserted into this table or provided as an argument of the stored procedure using standard Transact-SQL syntax as shown in the following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="a576a-140">Cualquier lenguaje del lado cliente o biblioteca que funcione con datos de cadena en Base de datos SQL de Azure también funciona con datos JSON.</span><span class="sxs-lookup"><span data-stu-id="a576a-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="a576a-141">JSON se puede almacenar en cualquier tabla que admita el tipo NVARCHAR, como una tabla con optimización para memoria o una tabla con versiones del sistema.</span><span class="sxs-lookup"><span data-stu-id="a576a-141">JSON can be stored in any table that supports the NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="a576a-142">JSON no introduce ninguna restricción en el código del lado cliente ni en el nivel de base de datos.</span><span class="sxs-lookup"><span data-stu-id="a576a-142">JSON does not introduce any constraint either in the client-side code or in the database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="a576a-143">Consulta de datos JSON</span><span class="sxs-lookup"><span data-stu-id="a576a-143">Querying JSON data</span></span>
<span data-ttu-id="a576a-144">Si tiene datos con formato JSON almacenados en tablas SQL de Azure, las funciones JSON permiten usarlos en cualquier consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="a576a-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="a576a-145">Las funciones JSON que están disponibles en Base de datos SQL de Azure permiten tratar los datos con formato JSON como cualquier otro tipo de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a576a-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="a576a-146">Puede extraer fácilmente valores del texto JSON y usar datos JSON en cualquier consulta:</span><span class="sxs-lookup"><span data-stu-id="a576a-146">You can easily extract values from the JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="a576a-147">La función JSON_VALUE extrae un valor del texto JSON almacenado en la columna Data.</span><span class="sxs-lookup"><span data-stu-id="a576a-147">The JSON_VALUE function extracts a value from JSON text stored in the Data column.</span></span> <span data-ttu-id="a576a-148">Esta función usa una ruta de acceso de estilo JavaScript para hacer referencia a un valor en el texto JSON para extraerlo.</span><span class="sxs-lookup"><span data-stu-id="a576a-148">This function uses a JavaScript-like path to reference a value in JSON text to extract.</span></span> <span data-ttu-id="a576a-149">El valor extraído se puede usar en cualquier parte de la consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="a576a-149">The extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="a576a-150">La función JSON_QUERY es similar a JSON_VALUE.</span><span class="sxs-lookup"><span data-stu-id="a576a-150">The JSON_QUERY function is similar to JSON_VALUE.</span></span> <span data-ttu-id="a576a-151">A diferencia de JSON_VALUE, esta función extrae subobjetos complejos, como matrices u objetos ubicados en texto JSON.</span><span class="sxs-lookup"><span data-stu-id="a576a-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="a576a-152">La función JSON_MODIFY permite especificar la ruta de acceso del valor en el texto JSON que debe actualizarse, así como un nuevo valor que sobrescribirá el anterior.</span><span class="sxs-lookup"><span data-stu-id="a576a-152">The JSON_MODIFY function lets you specify the path of the value in the JSON text that should be updated, as well as a new value that will overwrite the old one.</span></span> <span data-ttu-id="a576a-153">De esta forma, puede actualizar fácilmente el texto JSON sin volver a analizar la estructura completa.</span><span class="sxs-lookup"><span data-stu-id="a576a-153">This way you can easily update JSON text without reparsing the entire structure.</span></span>

<span data-ttu-id="a576a-154">Dado que JSON se almacena en texto estándar, no existe ninguna garantía de que los valores almacenados en las columnas de texto tengan el formato correcto.</span><span class="sxs-lookup"><span data-stu-id="a576a-154">Since JSON is stored in a standard text, there are no guarantees that the values stored in text columns are properly formatted.</span></span> <span data-ttu-id="a576a-155">Puede comprobar que el texto almacenado en la columna JSON tenga un formato correcto con las restricciones CHECK estándar de Base de datos SQL de Azure y la función ISJSON:</span><span class="sxs-lookup"><span data-stu-id="a576a-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and the ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="a576a-156">Si el texto de entrada tiene un formato JSON correcto, la función ISJSON devuelve el valor 1.</span><span class="sxs-lookup"><span data-stu-id="a576a-156">If the input text is properly formatted JSON, the ISJSON function returns the value 1.</span></span> <span data-ttu-id="a576a-157">Con cada inserción o actualización de la columna JSON, esta restricción comprobará que el nuevo valor de texto no tenga un formato JSON incorrecto.</span><span class="sxs-lookup"><span data-stu-id="a576a-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="a576a-158">Transformación de JSON en formato tabular</span><span class="sxs-lookup"><span data-stu-id="a576a-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="a576a-159">Base de datos SQL de Azure también permite transformar las colecciones JSON en formato tabular y cargar o consultar datos JSON.</span><span class="sxs-lookup"><span data-stu-id="a576a-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="a576a-160">OPENJSON es una función de valores de tabla que analiza texto JSON, busca una matriz de objetos JSON, itera en los elementos de la matriz y devuelve en el resultado de salida una fila para cada elemento de la matriz.</span><span class="sxs-lookup"><span data-stu-id="a576a-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through the elements of the array, and returns one row in the output result for each element of the array.</span></span>

![JSON tabular](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="a576a-162">En el ejemplo anterior, se puede especificar dónde ubicar la matriz JSON que se debe abrir (en la ruta de acceso $.Orders), qué columnas se deben devolver como resultado y dónde encontrar los valores JSON que se devolverán como celdas.</span><span class="sxs-lookup"><span data-stu-id="a576a-162">In the example above, we can specify where to locate the JSON array that should be opened (in the $.Orders path), what columns should be returned as result, and where to find the JSON values that will be returned as cells.</span></span>

<span data-ttu-id="a576a-163">Se puede transformar una matriz JSON de la variable @orders en un conjunto de filas, analizar este conjunto de resultados o insertar filas en una tabla estándar:</span><span class="sxs-lookup"><span data-stu-id="a576a-163">We can transform a JSON array in the @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

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
<span data-ttu-id="a576a-164">La colección de pedidos con formato de matriz JSON que se proporciona como parámetro del procedimiento almacenado se puede analizar e insertar en la tabla Orders.</span><span class="sxs-lookup"><span data-stu-id="a576a-164">The collection of orders formatted as a JSON array and provided as a parameter to the stored procedure can be parsed and inserted into the Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a576a-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a576a-165">Next steps</span></span>
<span data-ttu-id="a576a-166">Para aprender a integrar JSON en la aplicación, consulte estos recursos:</span><span class="sxs-lookup"><span data-stu-id="a576a-166">To learn how to integrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="a576a-167">Blog de TechNet</span><span class="sxs-lookup"><span data-stu-id="a576a-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="a576a-168">Documentación de MSDN</span><span class="sxs-lookup"><span data-stu-id="a576a-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="a576a-169">Vídeo de Channel 9</span><span class="sxs-lookup"><span data-stu-id="a576a-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="a576a-170">Para más información sobre diversos escenarios para integrar JSON en su aplicación, vea las demostraciones en este [vídeo de Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) o busque un escenario que coincida con su caso de uso en las [publicaciones del blog sobre JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="a576a-170">To learn about various scenarios for integrating JSON into your application, see the demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

