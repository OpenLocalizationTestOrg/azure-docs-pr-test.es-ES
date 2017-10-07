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
# <a name="getting-started-with-json-features-in-azure-sql-database"></a>Introducción a las características de JSON en Base de datos SQL de Azure
Base de datos SQL de Azure permite analizar y consultar datos representados en formato de notación de objetos JavaScript [(JSON)](http://www.json.org/) , y exportar los datos relacionales como texto JSON.

JSON es un formato de datos conocido que se usa para intercambiar datos en aplicaciones web y móviles modernas. JSON también se utiliza para almacenar datos semiestructurados en archivos de registro o en bases de datos NoSQL como [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/). Muchos servicios web REST devuelven resultados con formato de texto JSON o aceptan datos con ese formato. La mayoría de los servicios de Azure, como [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/) y [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/), tienen puntos de conexión REST que devuelven o consumen JSON.

Base de datos SQL de Azure permite trabajar fácilmente con datos JSON e integrar su base de datos con servicios modernos.

## <a name="overview"></a>Información general
La base de datos de SQL Azure proporciona Hola siguientes funciones para trabajar con datos JSON:

![Funciones JSON](./media/sql-database-json-features/image_1.png)

Si tiene texto JSON, puede extraer datos de JSON o compruebe que JSON es el formato correcto mediante el uso de funciones integradas de hello [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), y [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) . Hola [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) función le permite actualizar el valor de texto JSON. Para consultas y análisis más avanzados, la función [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) puede transformar una matriz de objetos JSON en un conjunto de filas. Cualquier consulta SQL se puede ejecutar en hello devolvió un conjunto de resultados. Por último, hay una cláusula [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) que permite dar formato de texto JSON a los datos almacenados en las tablas relacionales.

## <a name="formatting-relational-data-in-json-format"></a>Aplicación del formato JSON a datos relacionales
Si tiene un servicio web que toma datos de base de datos de hello las capas y proporciona una respuesta en JSON de formato, o marcos de JavaScript de cliente o bibliotecas que aceptan datos con formato JSON, se puede dar formato al contenido de base de datos como JSON directamente en una consulta SQL. Ya no tiene código de aplicación de toowrite que da formato a los resultados de la base de datos de SQL de Azure como JSON, o incluye algunos resultados de consulta tabulares JSON tooconvert de biblioteca de serialización y, a continuación, serializar formato tooJSON de objetos. En su lugar, puede usar Hola de resultados de la consulta SQL de JSON cláusula tooformat como JSON en la base de datos de SQL Azure y usarlo directamente en la aplicación.

En el siguiente ejemplo de Hola, se da formato como JSON filas de la tabla Sales.Customer hello mediante el uso de hello cláusula FOR JSON:

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

cláusula FOR JSON PATH de Hello da formato a resultados de Hola de consulta de hello texto JSON. Nombres de columna se utilizan como claves, mientras que los valores de celda de Hola se generan como valores JSON:

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

conjunto de resultados de Hola se formatea como una matriz JSON donde cada fila se da formato como un objeto JSON independiente.

Ruta de acceso indica que puede personalizar Hola el formato de salida de los resultados de JSON usando la notación de puntos en los alias de columna. Hola después de consulta cambia Hola nombre de clave de "CustomerName" hello en formato JSON de salida de hello y coloca los números de teléfono y fax en subobjeto de Hola "Contacto":

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

salida de Hello de esta consulta tiene el siguiente aspecto:

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

En este ejemplo se devuelve un único objeto JSON en lugar de una matriz mediante la especificación de hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) opción. Puede usar esta opción si sabe que va a devolver un solo objeto como resultado de la consulta.

valor principal de Hola de hello cláusula FOR JSON es que le permite devolver datos jerárquicos complejos de la base de datos con formato de objetos JSON anidados o matrices. Hola el siguiente ejemplo se muestra cómo ordena tooinclude que pertenecen toohello al cliente como una matriz anidada de pedidos:

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

En lugar de enviar datos de los clientes tooget consultas independientes y, a continuación, toofetch una lista de pedidos relacionados, puede obtener todos los datos necesarios de hello con una sola consulta, como se muestra en la siguiente salida de ejemplo de Hola:

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

## <a name="working-with-json-data"></a>Trabajo con datos JSON
Si no tiene datos estructurados estrictamente, si tiene subobjetos complejas, matrices o datos jerárquicos, o si sus estructuras de datos evolucionan con el tiempo, formato JSON de hello puede ayudarle a toorepresent cualquier estructura de datos complejos.

JSON es un formato de texto que se puede usar como cualquier otro tipo de cadena en Base de datos SQL de Azure. Puede enviar o almacenar datos JSON como un tipo NVARCHAR estándar:

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

Hola datos JSON que se usan en este ejemplo se representa mediante el uso de tipo nvarchar (max) de Hola. JSON se puede insertar en esta tabla o proporcionarse como un argumento de procedimiento Hola almacenado mediante sintaxis de Transact-SQL estándar, como se muestra en el siguiente ejemplo de Hola:

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

Cualquier lenguaje del lado cliente o biblioteca que funcione con datos de cadena en Base de datos SQL de Azure también funciona con datos JSON. JSON se puede almacenar en cualquier tabla que admite el tipo NVARCHAR de hello, como una tabla optimizada en memoria o una tabla con control de versiones. JSON no incluye ninguna restricción en el código de cliente de Hola o de capa de base de datos de Hola.

## <a name="querying-json-data"></a>Consulta de datos JSON
Si tiene datos con formato JSON almacenados en tablas SQL de Azure, las funciones JSON permiten usarlos en cualquier consulta SQL.

Las funciones JSON que están disponibles en Base de datos SQL de Azure permiten tratar los datos con formato JSON como cualquier otro tipo de datos SQL. Fácilmente puede extraer valores de hello texto JSON y utilizar datos JSON en cualquier consulta:

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

Hola función JSON_VALUE extrae un valor de texto JSON almacenado en la columna de datos de Hola. Esta función usa un valor de ruta de acceso similar a JavaScript tooreference en tooextract de texto JSON. valor de Hello extraído se puede utilizar en cualquier parte de la consulta SQL.

Hola función JSON_QUERY es tooJSON_VALUE similar. A diferencia de JSON_VALUE, esta función extrae subobjetos complejos, como matrices u objetos ubicados en texto JSON.

función JSON_MODIFY de Hello le permite especificar la ruta Hola Hola del valor en texto JSON hello que debe actualizarse, así como un nuevo valor que se sobrescribirá Hola antiguo. De esta forma que puede actualizar fácilmente texto JSON sin volver a analizar estructura completa de Hola.

Dado que JSON se almacena en un texto estándar, no hay ninguna garantía de que los valores de hello almacenados en columnas de texto son el formato correcto. Puede comprobar que el texto almacenado en la columna JSON correctamente con formato estándar hello función ISJSON y restricciones de comprobación de base de datos de SQL Azure:

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

Si el formato del texto de entrada de hello es correcto JSON, Hola función ISJSON devuelve el valor de hello 1. Con cada inserción o actualización de la columna JSON, esta restricción comprobará que el nuevo valor de texto no tenga un formato JSON incorrecto.

## <a name="transforming-json-into-tabular-format"></a>Transformación de JSON en formato tabular
Base de datos SQL de Azure también permite transformar las colecciones JSON en formato tabular y cargar o consultar datos JSON.

OPENJSON es una función con valores de tabla que analiza el texto JSON, busca una matriz de objetos JSON, recorre en iteración los elementos de Hola de matriz de Hola y devuelve una fila de resultado de salida de hello para cada elemento de matriz de Hola.

![JSON tabular](./media/sql-database-json-features/image_2.png)

En el ejemplo de Hola anterior, podemos especificar donde toolocate Hola matriz JSON que se debería abrir (en hello $. Ruta de acceso de pedidos), qué columnas se deben devolver como resultado, y donde toofind Hola valores JSON que se devolverán como celdas.

Se puede transformar una matriz JSON en hello @orders variable en un conjunto de filas, analizar este conjunto de resultados, o insertar filas en una tabla estándar:

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
colección de Hola de pedidos formatea como una matriz JSON y proporcionado como un procedimiento almacenado de toohello de parámetro se pueden analizar e insertar en la tabla de pedidos de Hola.

## <a name="next-steps"></a>Pasos siguientes
toolearn cómo toointegrate JSON en la aplicación, consulte estos recursos:

* [Blog de TechNet](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [Documentación de MSDN](https://msdn.microsoft.com/library/dn921897.aspx)
* [Vídeo de Channel 9](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

toolearn sobre los distintos escenarios para integrar JSON en la aplicación, vea las demostraciones de hello en este [vídeo de Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) o buscar un escenario que coincida con el caso de uso en [las entradas de Blog de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).

