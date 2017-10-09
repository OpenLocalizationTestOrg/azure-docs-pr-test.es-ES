---
title: aaaConnect aplicaciones tooAzure base de datos de MySQL | Documentos de Microsoft
description: "Este documento enumera las cadenas de conexión de hello admitida actualmente para las aplicaciones tooconnect con base de datos de Azure de MySQL, incluidos ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python y Ruby."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: bbcb2c0ddb4f8e5c225ebef53781e073f5c7b1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a>Cómo tooconnect tooAzure de las aplicaciones de base de datos de MySQL
Este documento enumera los tipos de cadena de conexión de Hola que son admitidos por base de datos de MySQL, junto con ejemplos y plantillas. Puede tener distintos parámetros y configuraciones en la cadena de conexión.

- certificado de hello tooobtain, consulte [cómo tooconfigure SSL](./howto-configure-ssl.md).
- {su_host} = <servername>.mysql.database.azure.com
- {su_usuario}@{nombredeservidor} = formato de userID para una autenticación correcta.  Utiliza simplemente Hola userID provocará Hola autenticación toofail.

## <a name="adonet"></a>ADO.NET
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

En este ejemplo, es el nombre del servidor de hello `myserver4demo`, nombre de base de datos es `wpdb`, nombre de usuario es `WPAdmin`, y la contraseña es `mypassword!2`. A continuación, debe tener la cadena de conexión de hello:

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a>JDBC
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a>Node.js
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a>ODBC
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a>PHP
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a>Python
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a>Ruby
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a>Obtener detalles de la cadena de conexión de Hola de hello portal de Azure
Hola [portal de Azure](https://portal.azure.com), vaya tooyour base de datos de MySQL server y, a continuación, haga clic en **las cadenas de conexión** tooget la cadena de lista para la instancia: ![panel de las cadenas de conexión de Hola Hola Portal de Azure](./media/howto-connection-strings/connection-strings-on-portal.png)

cadena de Hello proporciona detalles como controlador de hello, servidor y otros parámetros de conexión de base de datos. Modifique estos ejemplos con sus propios parámetros, como un nombre de base de datos, una contraseña, etc. A continuación, puede usar este servidor de cadena tooconnect toohello desde su código y aplicaciones.

## <a name="next-steps"></a>Pasos siguientes
- Para más información sobre las bibliotecas de conexión, consulte [Conceptos: bibliotecas de conexiones](./concepts-connection-libraries.md).
