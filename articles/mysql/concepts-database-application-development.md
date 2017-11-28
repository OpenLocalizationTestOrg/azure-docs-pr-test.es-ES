---
title: "información general sobre el desarrollo de aplicaciones de aaaDatabase de base de datos de Azure para MySQL | Documentos de Microsoft"
description: "Presenta consideraciones de diseño que debería seguir un programador al escribir aplicaciones código tooconnect tooAzure base de datos de MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="344e0-103">Introducción al desarrollo de aplicaciones para Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="344e0-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="344e0-104">En este artículo se describe las consideraciones de diseño que debería seguir un programador al escribir aplicaciones código tooconnect tooAzure base de datos de MySQL</span><span class="sxs-lookup"><span data-stu-id="344e0-104">This article discusses design considerations that a developer should follow when writing application code tooconnect tooAzure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="344e0-105">Encontrará un tutorial que se muestra cómo toocreate un servidor, se crea un firewall basado en servidor, ver propiedades del servidor, crea base de datos, conectarse y consulta mediante el área de trabajo y mysql.exe, [diseñar la primera base de datos de MySQL de Azure](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="344e0-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="344e0-106">Plataforma y lenguaje</span><span class="sxs-lookup"><span data-stu-id="344e0-106">Language and platform</span></span>
<span data-ttu-id="344e0-107">Existen ejemplos de código para diferentes lenguajes de programación y plataformas.</span><span class="sxs-lookup"><span data-stu-id="344e0-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="344e0-108">Puede encontrar vínculos toohello ejemplos de código en: [bibliotecas de conectividad usan tooconnect tooAzure base de datos de MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="344e0-108">You can find links toohello code samples at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="344e0-109">Herramientas</span><span class="sxs-lookup"><span data-stu-id="344e0-109">Tools</span></span>
<span data-ttu-id="344e0-110">Base de datos de Azure para MySQL usa la versión de comunidad de MySQL hello, compatible con MySQL de herramientas de administración habituales, tales como las utilidades de Workbench o MySQL como mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)y otros.</span><span class="sxs-lookup"><span data-stu-id="344e0-110">Azure Database for MySQL uses hello MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="344e0-111">También puede usar Hola portal de Azure, CLI de Azure y las API de REST toointeract con el servicio de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="344e0-111">You can also use hello Azure portal, Azure CLI, and REST APIs toointeract with hello database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="344e0-112">Limitaciones de recursos</span><span class="sxs-lookup"><span data-stu-id="344e0-112">Resource limitations</span></span>
<span data-ttu-id="344e0-113">La base de datos de MySQL Azure administra Hola recursos disponibles tooa server mediante dos mecanismos diferentes:</span><span class="sxs-lookup"><span data-stu-id="344e0-113">Azure MySQL Database manages hello resources available tooa server using two different mechanisms:</span></span> 
- <span data-ttu-id="344e0-114">Gobierno de recursos</span><span class="sxs-lookup"><span data-stu-id="344e0-114">Resources Governance</span></span> 
- <span data-ttu-id="344e0-115">Aplicación de límites</span><span class="sxs-lookup"><span data-stu-id="344e0-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="344e0-116">Seguridad</span><span class="sxs-lookup"><span data-stu-id="344e0-116">Security</span></span>
<span data-ttu-id="344e0-117">La base de datos MySQL de Azure proporciona recursos para limitar el acceso, proteger los datos, configurar usuarios y roles y supervisar las actividades en una base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="344e0-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="344e0-118">Autenticación</span><span class="sxs-lookup"><span data-stu-id="344e0-118">Authentication</span></span>
<span data-ttu-id="344e0-119">La base de datos MySQL de Azure admite la autenticación de servidor de usuarios e inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="344e0-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="344e0-120">Resistencia</span><span class="sxs-lookup"><span data-stu-id="344e0-120">Resiliency</span></span>
<span data-ttu-id="344e0-121">Cuando se produce un error transitorio al conectar tooMySQL base de datos, el código debe reintentar la llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="344e0-121">When a transient error occurs while connecting tooMySQL Database, your code should retry hello call.</span></span> <span data-ttu-id="344e0-122">Te recomendamos que uses Hola Reintentar lógica de interrupción lógica, por lo que no desborda Hola base de datos de SQL con varios clientes reintentando simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="344e0-122">We recommend hello retry logic use back off logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="344e0-123">Ejemplos de código: para los ejemplos de código que muestran la lógica de reintento, vea los ejemplos para el idioma de Hola de su elección en: [bibliotecas de conectividad usan tooconnect tooAzure base de datos de MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="344e0-123">Code samples: For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="344e0-124">Administración de conexiones</span><span class="sxs-lookup"><span data-stu-id="344e0-124">Managing Connections</span></span>
<span data-ttu-id="344e0-125">Las conexiones de base de datos son un recurso limitado, por lo que te recomendamos que uses significativo de conexiones al obtener acceso a la base de datos de MySQL tooachieve un mejor rendimiento.</span><span class="sxs-lookup"><span data-stu-id="344e0-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database tooachieve better performance.</span></span>
- <span data-ttu-id="344e0-126">Base de datos Access hello mediante la agrupación de conexiones o conexiones persistentes.</span><span class="sxs-lookup"><span data-stu-id="344e0-126">Access hello database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="344e0-127">Base de datos de Hola de Access mediante el uso de la duración de derivación.</span><span class="sxs-lookup"><span data-stu-id="344e0-127">Access hello database by using short connection life span.</span></span> 
- <span data-ttu-id="344e0-128">Lógica de reintento de uso en la aplicación en el momento de Hola de intento de conexión de hello, toocatch errores debido a las conexiones tooconcurrent ha alcanzado el máximo de hello permitido.</span><span class="sxs-lookup"><span data-stu-id="344e0-128">Use retry logic in your application at hello point of hello connection attempt, toocatch failures due tooconcurrent connections have reached hello maximum allowed.</span></span> <span data-ttu-id="344e0-129">Hola lógica de reintento, establezca un breve retraso y, a continuación, espere durante un tiempo aleatorio antes de intentos de conexión adicionales de Hola.</span><span class="sxs-lookup"><span data-stu-id="344e0-129">In hello retry logic, set a short delay, and then wait for a random time before hello additional connection attempts.</span></span>
