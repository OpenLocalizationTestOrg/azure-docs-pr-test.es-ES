---
title: Bibliotecas de conexiones de Azure Database for PostgreSQL | Microsoft Docs
description: "En este artículo se describen varias bibliotecas y controladores que los desarrolladores pueden usar al codificar aplicaciones para conectarse a Azure Database for PostgreSQL y realizar ahí consultas."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/15/2017
ms.openlocfilehash: 1f99ef7fefb1ff9d35f564a1f0ad77c8dd64659e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connection-libraries-for-azure-database-for-postgresql"></a><span data-ttu-id="60a54-103">Bibliotecas de conexiones de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="60a54-103">Connection libraries for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="60a54-104">En este tema se enumeran las bibliotecas y los controladores que pueden usar los desarrolladores para programar aplicaciones para conectarse a Azure Database for PostgreSQL y realizar ahí consultas.</span><span class="sxs-lookup"><span data-stu-id="60a54-104">This topic lists libraries and drivers for use by developers for programming applications to connect and query Azure Database for PostgreSQL.</span></span>

## <a name="client-interfaces"></a><span data-ttu-id="60a54-105">Interfaces de cliente</span><span class="sxs-lookup"><span data-stu-id="60a54-105">Client interfaces</span></span>
<span data-ttu-id="60a54-106">La mayoría de bibliotecas de cliente de lenguajes para conectarse al servidor de PostgreSQL son proyectos externos y se distribuyen de manera independiente.</span><span class="sxs-lookup"><span data-stu-id="60a54-106">Most language client libraries to connect to PostgreSQL server are external projects, and are distributed independently.</span></span> <span data-ttu-id="60a54-107">Estas se admiten en plataformas Windows, Linux y Mac.</span><span class="sxs-lookup"><span data-stu-id="60a54-107">These are supported on Windows, Linux, and Mac platforms.</span></span> <span data-ttu-id="60a54-108">Se enumeran algunos de los controladores cliente más conocidos:</span><span class="sxs-lookup"><span data-stu-id="60a54-108">Some of the popular client drivers are listed:</span></span>

| <span data-ttu-id="60a54-109">**Lenguaje**</span><span class="sxs-lookup"><span data-stu-id="60a54-109">**Language**</span></span> | <span data-ttu-id="60a54-110">**Interfaz de cliente**</span><span class="sxs-lookup"><span data-stu-id="60a54-110">**Client interface**</span></span> | <span data-ttu-id="60a54-111">**Información adicional**</span><span class="sxs-lookup"><span data-stu-id="60a54-111">**Additional information**</span></span> | <span data-ttu-id="60a54-112">**Descargar**</span><span class="sxs-lookup"><span data-stu-id="60a54-112">**Download**</span></span> |
|--------------|----------------------------------------------------------------|-------------------------------------|--------------------------------------------------------------------|
| <span data-ttu-id="60a54-113">Python</span><span class="sxs-lookup"><span data-stu-id="60a54-113">Python</span></span> | [<span data-ttu-id="60a54-114">psycopg</span><span class="sxs-lookup"><span data-stu-id="60a54-114">psycopg</span></span>](http://initd.org/psycopg/) | <span data-ttu-id="60a54-115">Compatible con API 2.0 de BD</span><span class="sxs-lookup"><span data-stu-id="60a54-115">DB API 2.0-compliant</span></span> | [<span data-ttu-id="60a54-116">Descargar</span><span class="sxs-lookup"><span data-stu-id="60a54-116">Download</span></span>](http://initd.org/psycopg/download/) |
| <span data-ttu-id="60a54-117">PHP</span><span class="sxs-lookup"><span data-stu-id="60a54-117">PHP</span></span> | [<span data-ttu-id="60a54-118">php-pgsql</span><span class="sxs-lookup"><span data-stu-id="60a54-118">php-pgsql</span></span>](https://php.net/manual/en/book.pgsql.php) | <span data-ttu-id="60a54-119">Extensión de base de datos</span><span class="sxs-lookup"><span data-stu-id="60a54-119">Database extension</span></span> | [<span data-ttu-id="60a54-120">Instalación</span><span class="sxs-lookup"><span data-stu-id="60a54-120">Install</span></span>](https://secure.php.net/manual/en/pgsql.installation.php) |
| <span data-ttu-id="60a54-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="60a54-121">Node.js</span></span> | [<span data-ttu-id="60a54-122">Paquete de Pg npm</span><span class="sxs-lookup"><span data-stu-id="60a54-122">Pg npm package</span></span>](https://www.npmjs.com/package/pg) | <span data-ttu-id="60a54-123">Cliente sin bloqueo de JavaScript puro</span><span class="sxs-lookup"><span data-stu-id="60a54-123">Pure JavaScript non-blocking client</span></span> | [<span data-ttu-id="60a54-124">Instalación</span><span class="sxs-lookup"><span data-stu-id="60a54-124">Install</span></span>](https://www.npmjs.com/package/pg) |
| <span data-ttu-id="60a54-125">Java</span><span class="sxs-lookup"><span data-stu-id="60a54-125">Java</span></span> | [<span data-ttu-id="60a54-126">JDBC</span><span class="sxs-lookup"><span data-stu-id="60a54-126">JDBC</span></span>](http://jdbc.postgresql.org/) | <span data-ttu-id="60a54-127">Controlador JDBC tipo 4</span><span class="sxs-lookup"><span data-stu-id="60a54-127">Type 4 JDBC driver</span></span> | [<span data-ttu-id="60a54-128">Descargar</span><span class="sxs-lookup"><span data-stu-id="60a54-128">Download</span></span>](https://jdbc.postgresql.org/download.html)  |
| <span data-ttu-id="60a54-129">Ruby</span><span class="sxs-lookup"><span data-stu-id="60a54-129">Ruby</span></span> | [<span data-ttu-id="60a54-130">Pg gem</span><span class="sxs-lookup"><span data-stu-id="60a54-130">Pg gem</span></span>](https://deveiate.org/code/pg/) | <span data-ttu-id="60a54-131">Interfaz Ruby</span><span class="sxs-lookup"><span data-stu-id="60a54-131">Ruby Interface</span></span> | [<span data-ttu-id="60a54-132">Descargar</span><span class="sxs-lookup"><span data-stu-id="60a54-132">Download</span></span>](https://rubygems.org/downloads/pg-0.20.0.gem) |
| <span data-ttu-id="60a54-133">Go</span><span class="sxs-lookup"><span data-stu-id="60a54-133">Go</span></span> | [<span data-ttu-id="60a54-134">Package pq</span><span class="sxs-lookup"><span data-stu-id="60a54-134">Package pq</span></span>](https://godoc.org/github.com/lib/pq) | <span data-ttu-id="60a54-135">Controlador de Postgres de Go puro</span><span class="sxs-lookup"><span data-stu-id="60a54-135">Pure Go postgres driver</span></span> | [<span data-ttu-id="60a54-136">Instalación</span><span class="sxs-lookup"><span data-stu-id="60a54-136">Install</span></span>](https://github.com/lib/pq/blob/master/README.md) |
| <span data-ttu-id="60a54-137">C\#/ .NET</span><span class="sxs-lookup"><span data-stu-id="60a54-137">C\#/ .NET</span></span> | [<span data-ttu-id="60a54-138">Npgsql</span><span class="sxs-lookup"><span data-stu-id="60a54-138">Npgsql</span></span>](http://www.npgsql.org/) | <span data-ttu-id="60a54-139">Proveedor de datos de ADO.NET</span><span class="sxs-lookup"><span data-stu-id="60a54-139">ADO.NET Data Provider</span></span> | [<span data-ttu-id="60a54-140">Descargar</span><span class="sxs-lookup"><span data-stu-id="60a54-140">Download</span></span>](https://www.microsoft.com/net/) |
| <span data-ttu-id="60a54-141">ODBC</span><span class="sxs-lookup"><span data-stu-id="60a54-141">ODBC</span></span> | [<span data-ttu-id="60a54-142">psqlODBC</span><span class="sxs-lookup"><span data-stu-id="60a54-142">psqlODBC</span></span>](https://odbc.postgresql.org/) | <span data-ttu-id="60a54-143">Controlador ODBC</span><span class="sxs-lookup"><span data-stu-id="60a54-143">ODBC Driver</span></span> | [<span data-ttu-id="60a54-144">Descargar</span><span class="sxs-lookup"><span data-stu-id="60a54-144">Download</span></span>](http://www.postgresql.org/ftp/odbc/versions/) |
| <span data-ttu-id="60a54-145">C</span><span class="sxs-lookup"><span data-stu-id="60a54-145">C</span></span> | [<span data-ttu-id="60a54-146">libpq</span><span class="sxs-lookup"><span data-stu-id="60a54-146">libpq</span></span>](https://www.postgresql.org/docs/9.6/static/libpq.html) | <span data-ttu-id="60a54-147">Interfaz de idioma C principal</span><span class="sxs-lookup"><span data-stu-id="60a54-147">Primary C language interface</span></span> | <span data-ttu-id="60a54-148">Se incluye</span><span class="sxs-lookup"><span data-stu-id="60a54-148">Included</span></span> |
| <span data-ttu-id="60a54-149">C++</span><span class="sxs-lookup"><span data-stu-id="60a54-149">C++</span></span> | [<span data-ttu-id="60a54-150">libpqxx</span><span class="sxs-lookup"><span data-stu-id="60a54-150">libpqxx</span></span>](http://pqxx.org/) | <span data-ttu-id="60a54-151">Interfaz de C++ de nuevo estilo</span><span class="sxs-lookup"><span data-stu-id="60a54-151">New-style C++ interface</span></span> | [<span data-ttu-id="60a54-152">Descargar</span><span class="sxs-lookup"><span data-stu-id="60a54-152">Download</span></span>](http://pqxx.org/download/software/) |

## <a name="next-steps"></a><span data-ttu-id="60a54-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="60a54-153">Next steps</span></span>
<span data-ttu-id="60a54-154">Lea estos tutoriales rápidos sobre cómo conectarse a Azure Database for PostgreSQL y realizar consultas ahí mediante el lenguaje de su elección:</span><span class="sxs-lookup"><span data-stu-id="60a54-154">Read these quickstarts on how to connect and query Azure Database for PostgreSQL using your language of choice:</span></span>

<span data-ttu-id="60a54-155">[Python](./connect-python.md) | [Node.JS](./connect-nodejs.md) | [.NET (C#)](./connect-csharp.md)</span><span class="sxs-lookup"><span data-stu-id="60a54-155">[Python](./connect-python.md) | [Node.JS](./connect-nodejs.md) | [.NET (C#)](./connect-csharp.md)</span></span>