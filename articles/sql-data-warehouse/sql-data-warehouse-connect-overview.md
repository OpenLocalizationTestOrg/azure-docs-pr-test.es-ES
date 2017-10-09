---
title: aaaConnect tooAzure almacenamiento de datos SQL | Documentos de Microsoft
description: "Cómo cadena de conexión y el nombre de servidor hello toofind de su tooAzure almacenamiento de datos de SQL"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: e52872ca-ae74-4e25-9c56-d49c85c8d0f0
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: f15e098026afb7c5efbbbfaf62b681e8cd7936bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-sql-data-warehouse"></a>Conectar tooAzure almacenamiento de datos SQL
En este artículo le ayuda a obtener conectado tooSQL Data Warehouse Hola primera vez.

## <a name="find-your-server-name"></a>Búsqueda del nombre de servidor
Hola tooSQL de tooconnecting paso primer almacén de datos consiste en saber cómo toofind el nombre del servidor.  Por ejemplo, el nombre del servidor hello en el siguiente ejemplo de Hola es sample.database.windows.net. nombre de servidor completo de Hola toofind:

1. Vaya toohello [portal de Azure][Azure portal].
2. Haga clic en **Bases de datos SQL** 
3. Haga clic en la base de datos de hello a que desea tooconnect.
4. Busque el nombre completo del servidor de Hola.
   
    ![Nombre del servidor completo][1]

## <a name="supported-drivers-and-connection-strings"></a>Cadenas de conexión y controladores admitidos
Azure SQL Data Warehouse es compatible con [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] y [JDBC][JDBC]. Haga clic en uno de hello anterior versión más reciente de los controladores toofind hello y documentación. tooautomatically generar la cadena de conexión de hello para el controlador de Hola que usas para de hello Azure portal, puede hacer clic en hello **mostrar cadenas de conexión de base de datos** del anterior ejemplo de Hola.  Los siguientes son también algunos ejemplos del aspecto de una cadena de conexión para cada controlador.

> [!NOTE]
> Considere la posibilidad de establecer Hola conexión tiempo de espera too300 segundos tooallow su toosurvive conexión abreviada períodos de falta de disponibilidad.
> 
> 

### <a name="adonet-connection-string-example"></a>Ejemplo de cadena de conexión de ADO.NET
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a>Ejemplo de cadena de conexión de ODBC
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a>Ejemplo de cadena de conexión de PHP
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a>Ejemplo de cadena de conexión de JDBC
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a>Configuración de conexión
SQL Data Warehouse normaliza algunas opciones de configuración durante la conexión y la creación de objetos. Estas opciones de configuración no se pueden invalidar e incluyen:

| Configuración de base de datos | Valor |
|:--- |:--- |
| [ANSI_NULLS][ANSI_NULLS] |ACTIVAR |
| [QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS] |ACTIVAR |
| [DATEFORMAT][DATEFORMAT] |mdy |
| [DATEFIRST][DATEFIRST] |7 |

## <a name="next-steps"></a>Pasos siguientes
tooconnect y consultas con Visual Studio, vea [consulta con Visual Studio][Query with Visual Studio]. toolearn más información acerca de opciones de autenticación, vea [tooAzure almacenamiento de datos SQL de autenticación][Authentication tooAzure SQL Data Warehouse].

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx
[ANSI_NULLS]: https://msdn.microsoft.com/library/ms188048.aspx
[QUOTED_IDENTIFIERS]: https://msdn.microsoft.com/library/ms174393.aspx
[DATEFORMAT]: https://msdn.microsoft.com/library/ms189491.aspx
[DATEFIRST]: https://msdn.microsoft.com/library/ms181598.aspx

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->
[1]: media/sql-data-warehouse-connect-overview/get-server-name.png


