---
title: "Conexión de aplicaciones a Azure Database for MySQL | Microsoft Docs"
description: "En este documento se enumeran todas las cadenas de conexión admitidas actualmente para que las aplicaciones se conecten con Azure Database for MySQL, incluidas ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python y Ruby."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: 2f40da41bcfda7e35f6fc63ead5d055246ab390c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-applications-to-azure-database-for-mysql"></a><span data-ttu-id="1c9cd-103">Conexión de aplicaciones a Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="1c9cd-103">How to connect applications to Azure Database for MySQL</span></span>
<span data-ttu-id="1c9cd-104">En este documento se enumeran todos los tipos de cadena de conexión admitidos en Azure Database for MySQL, junto con plantillas y ejemplos.</span><span class="sxs-lookup"><span data-stu-id="1c9cd-104">This document lists the connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="1c9cd-105">Puede tener distintos parámetros y configuraciones en la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="1c9cd-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="1c9cd-106">Para obtener el certificado, consulte [Configuración de SSL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="1c9cd-106">To obtain the certificate, see [How to configure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="1c9cd-107">{su_host} = <servername>.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="1c9cd-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="1c9cd-108">{su_usuario}@{nombredeservidor} = formato de userID para una autenticación correcta.</span><span class="sxs-lookup"><span data-stu-id="1c9cd-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="1c9cd-109">Usar solo userID hará que la autenticación presente un error.</span><span class="sxs-lookup"><span data-stu-id="1c9cd-109">Using just the userID will cause the authentication to fail.</span></span>

## <a name="adonet"></a><span data-ttu-id="1c9cd-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="1c9cd-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="1c9cd-111">En este ejemplo, el nombre del servidor es `myserver4demo`, el nombre de base de datos es `wpdb`, el nombre de usuario es `WPAdmin` y la contraseña es `mypassword!2`.</span><span class="sxs-lookup"><span data-stu-id="1c9cd-111">In this example, the server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="1c9cd-112">Entonces, la cadena de conexión debería ser:</span><span class="sxs-lookup"><span data-stu-id="1c9cd-112">Then, the connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="1c9cd-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="1c9cd-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="1c9cd-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="1c9cd-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="1c9cd-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="1c9cd-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="1c9cd-116">PHP</span><span class="sxs-lookup"><span data-stu-id="1c9cd-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="1c9cd-117">Python</span><span class="sxs-lookup"><span data-stu-id="1c9cd-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="1c9cd-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="1c9cd-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-the-connection-string-details-from-the-azure-portal"></a><span data-ttu-id="1c9cd-119">Obtención de los detalles de la cadena de conexión de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1c9cd-119">Get the connection string details from the Azure portal</span></span>
<span data-ttu-id="1c9cd-120">En [Azure Portal](https://portal.azure.com), vaya al servidor de Azure Database for MySQL y, luego, haga clic en **Cadenas de conexión** para obtener la lista de cadenas para la instancia: ![El panel Cadenas de conexión en Azure Portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="1c9cd-120">In the [Azure portal](https://portal.azure.com), go to your Azure Database for MySQL server, and then click **Connection strings** to get your string list for your instance: ![The Connection strings pane in the Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="1c9cd-121">La cadena proporciona detalles como el controlador, el servidor y otros parámetros de conexión de base de datos.</span><span class="sxs-lookup"><span data-stu-id="1c9cd-121">The string provides details such as the driver, server, and other database connection parameters.</span></span> <span data-ttu-id="1c9cd-122">Modifique estos ejemplos con sus propios parámetros, como un nombre de base de datos, una contraseña, etc.</span><span class="sxs-lookup"><span data-stu-id="1c9cd-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="1c9cd-123">Luego puede usar esta cadena para conectarse al servidor desde su código y sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1c9cd-123">You can then use this string to connect to the server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c9cd-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1c9cd-124">Next steps</span></span>
- <span data-ttu-id="1c9cd-125">Para más información sobre las bibliotecas de conexión, consulte [Conceptos: bibliotecas de conexiones](./concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="1c9cd-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
