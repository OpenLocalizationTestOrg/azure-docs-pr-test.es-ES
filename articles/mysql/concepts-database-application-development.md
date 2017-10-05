---
title: "Introducción al desarrollo de aplicaciones de base de datos de Azure Database for MySQL | Microsoft Docs"
description: "Se presentan las consideraciones de diseño que un desarrollador debe seguir al escribir código de aplicación para conectarse a Azure Database for MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 350dd775e172120d806d1193877a34d94f4d3f6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="c5c08-103">Introducción al desarrollo de aplicaciones para Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="c5c08-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="c5c08-104">En este artículo se describe las consideraciones de diseño que debería seguir un desarrollador al escribir código de aplicación para conectarse a Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="c5c08-104">This article discusses design considerations that a developer should follow when writing application code to connect to Azure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="c5c08-105">Para obtener un tutorial que muestre cómo crear un servidor, crear un firewall basado en servidor, ver propiedades de servidor, crear base de datos, conectarse y consultar mediante Workbench y mysql.exe, consulte [Design your first Azure MySQL database](tutorial-design-database-using-portal.md) (Diseño de la primera base de datos MySQL de Azure).</span><span class="sxs-lookup"><span data-stu-id="c5c08-105">For a tutorial showing you how to create a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="c5c08-106">Plataforma y lenguaje</span><span class="sxs-lookup"><span data-stu-id="c5c08-106">Language and platform</span></span>
<span data-ttu-id="c5c08-107">Existen ejemplos de código para diferentes lenguajes de programación y plataformas.</span><span class="sxs-lookup"><span data-stu-id="c5c08-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="c5c08-108">Puede encontrar vínculos a los ejemplos de código en: [Bibliotecas de conexiones usadas para conectarse a Azure Database for MySQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="c5c08-108">You can find links to the code samples at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="c5c08-109">Herramientas</span><span class="sxs-lookup"><span data-stu-id="c5c08-109">Tools</span></span>
<span data-ttu-id="c5c08-110">Azure Database for MySQL usa la versión de la comunidad de MySQL, compatible con herramientas de administración comunes de MySQL, como Workbench, o utilidades de MySQL como mysql.exe, [phpMyAdmin ](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql) y otras.</span><span class="sxs-lookup"><span data-stu-id="c5c08-110">Azure Database for MySQL uses the MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="c5c08-111">También puede usar el portal de Azure, la CLI de Azure y la API de REST para interactuar con el servicio de base de datos.</span><span class="sxs-lookup"><span data-stu-id="c5c08-111">You can also use the Azure portal, Azure CLI, and REST APIs to interact with the database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="c5c08-112">Limitaciones de recursos</span><span class="sxs-lookup"><span data-stu-id="c5c08-112">Resource limitations</span></span>
<span data-ttu-id="c5c08-113">La base de datos MySQL de Azure administra los recursos disponibles para un servidor mediante dos mecanismos diferentes:</span><span class="sxs-lookup"><span data-stu-id="c5c08-113">Azure MySQL Database manages the resources available to a server using two different mechanisms:</span></span> 
- <span data-ttu-id="c5c08-114">Gobierno de recursos</span><span class="sxs-lookup"><span data-stu-id="c5c08-114">Resources Governance</span></span> 
- <span data-ttu-id="c5c08-115">Aplicación de límites</span><span class="sxs-lookup"><span data-stu-id="c5c08-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="c5c08-116">Seguridad</span><span class="sxs-lookup"><span data-stu-id="c5c08-116">Security</span></span>
<span data-ttu-id="c5c08-117">La base de datos MySQL de Azure proporciona recursos para limitar el acceso, proteger los datos, configurar usuarios y roles y supervisar las actividades en una base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="c5c08-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="c5c08-118">Autenticación</span><span class="sxs-lookup"><span data-stu-id="c5c08-118">Authentication</span></span>
<span data-ttu-id="c5c08-119">La base de datos MySQL de Azure admite la autenticación de servidor de usuarios e inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="c5c08-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="c5c08-120">Resistencia</span><span class="sxs-lookup"><span data-stu-id="c5c08-120">Resiliency</span></span>
<span data-ttu-id="c5c08-121">Cuando se produce un error transitorio durante la conexión a la base de datos MySQL, el código debe reintentar la llamada.</span><span class="sxs-lookup"><span data-stu-id="c5c08-121">When a transient error occurs while connecting to MySQL Database, your code should retry the call.</span></span> <span data-ttu-id="c5c08-122">Recomendamos que en la lógica de reintento se haga uso de la lógica de interrupción; de este modo no se sobrecargará SQL Database con los reintentos de varios clientes a la vez.</span><span class="sxs-lookup"><span data-stu-id="c5c08-122">We recommend the retry logic use back off logic, so that it does not overwhelm the SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="c5c08-123">Ejemplos de código: para ver ejemplos de código que ilustran la lógica de reintento, consulte los del idioma de su elección en: [Bibliotecas de conexiones usadas para conectarse a Azure Database for MySQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="c5c08-123">Code samples: For code samples that illustrate retry logic, see samples for the language of your choice at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="c5c08-124">Administración de conexiones</span><span class="sxs-lookup"><span data-stu-id="c5c08-124">Managing Connections</span></span>
<span data-ttu-id="c5c08-125">Las conexiones de base de datos son un recurso limitado, por lo que recomendamos un uso razonable de conexiones al acceder a la base de datos MySQL con el fin de lograr un mejor rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c5c08-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database to achieve better performance.</span></span>
- <span data-ttu-id="c5c08-126">Acceda a la base de datos mediante la agrupación de conexiones o conexiones persistentes.</span><span class="sxs-lookup"><span data-stu-id="c5c08-126">Access the database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="c5c08-127">Acceda a la base de datos usando la duración de conexión corta.</span><span class="sxs-lookup"><span data-stu-id="c5c08-127">Access the database by using short connection life span.</span></span> 
- <span data-ttu-id="c5c08-128">Use la lógica de reintento en su aplicación en el momento del intento de conexión, para detectar errores debidos a conexiones simultáneas que hayan alcanzado el número máximo permitido.</span><span class="sxs-lookup"><span data-stu-id="c5c08-128">Use retry logic in your application at the point of the connection attempt, to catch failures due to concurrent connections have reached the maximum allowed.</span></span> <span data-ttu-id="c5c08-129">En la lógica de reintento, establezca un retraso breve y, a continuación, espere un tiempo aleatorio antes de los intentos de conexiones adicionales.</span><span class="sxs-lookup"><span data-stu-id="c5c08-129">In the retry logic, set a short delay, and then wait for a random time before the additional connection attempts.</span></span>