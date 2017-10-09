---
title: Bibliotecas de conexiones de Azure Database for PostgreSQL | Microsoft Docs
description: "Este artículo describen varias bibliotecas y controladores que los desarrolladores pueden utilizar al codificar aplicaciones tooconnect y consulta de base de datos de Azure para PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/15/2017
ms.openlocfilehash: 1f7234499d8abe37f8de9008e3158765b1fb0bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connection-libraries-for-azure-database-for-postgresql"></a>Bibliotecas de conexiones de Azure Database for PostgreSQL
Este tema enumeran las bibliotecas y los controladores para su uso por los desarrolladores para programar aplicaciones tooconnect y consulta de base de datos de Azure para PostgreSQL.

## <a name="client-interfaces"></a>Interfaces de cliente
La mayoría lenguaje bibliotecas tooconnect tooPostgreSQL cliente-servidor son proyectos externos y se distribuyen de forma independiente. Estas se admiten en plataformas Windows, Linux y Mac. Se enumeran algunos de los controladores de cliente popular de hello:

| **Lenguaje** | **Interfaz de cliente** | **Información adicional** | **Descargar** |
|--------------|----------------------------------------------------------------|-------------------------------------|--------------------------------------------------------------------|
| Python | [psycopg](http://initd.org/psycopg/) | Compatible con API 2.0 de BD | [Descargar](http://initd.org/psycopg/download/) |
| PHP | [php-pgsql](https://php.net/manual/en/book.pgsql.php) | Extensión de base de datos | [Instalación](https://secure.php.net/manual/en/pgsql.installation.php) |
| Node.js | [Paquete de Pg npm](https://www.npmjs.com/package/pg) | Cliente sin bloqueo de JavaScript puro | [Instalación](https://www.npmjs.com/package/pg) |
| Java | [JDBC](http://jdbc.postgresql.org/) | Controlador JDBC tipo 4 | [Descargar](https://jdbc.postgresql.org/download.html)  |
| Ruby | [Pg gem](https://deveiate.org/code/pg/) | Interfaz Ruby | [Descargar](https://rubygems.org/downloads/pg-0.20.0.gem) |
| Go | [Package pq](https://godoc.org/github.com/lib/pq) | Controlador de Postgres de Go puro | [Instalación](https://github.com/lib/pq/blob/master/README.md) |
| C\#/ .NET | [Npgsql](http://www.npgsql.org/) | Proveedor de datos de ADO.NET | [Descargar](https://www.microsoft.com/net/) |
| ODBC | [psqlODBC](https://odbc.postgresql.org/) | Controlador ODBC | [Descargar](http://www.postgresql.org/ftp/odbc/versions/) |
| C | [libpq](https://www.postgresql.org/docs/9.6/static/libpq.html) | Interfaz de idioma C principal | Se incluye |
| C++ | [libpqxx](http://pqxx.org/) | Interfaz de C++ de nuevo estilo | [Descargar](http://pqxx.org/download/software/) |

## <a name="next-steps"></a>Pasos siguientes
Leer estos tutoriales sobre cómo tooconnect y consulta Azure base de datos PostgreSQL mediante el lenguaje seleccionado:

[Python](./connect-python.md) | [Node.JS](./connect-nodejs.md) | [.NET (C#)](./connect-csharp.md)
