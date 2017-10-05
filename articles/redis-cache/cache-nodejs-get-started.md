---
title: Uso de Azure Redis Cache con Node.js | Microsoft Docs
description: "Introducción a Caché en Redis de Azure usando Node.js y node_redis."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: 530191637b1aa91ee1d7fe5b5bb032c60983f7dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-nodejs"></a><span data-ttu-id="c44bd-103">Uso de Caché en Redis de Azure con Node.js</span><span class="sxs-lookup"><span data-stu-id="c44bd-103">How to use Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c44bd-104">.NET</span><span class="sxs-lookup"><span data-stu-id="c44bd-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="c44bd-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c44bd-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="c44bd-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="c44bd-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="c44bd-107">Java</span><span class="sxs-lookup"><span data-stu-id="c44bd-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="c44bd-108">Python</span><span class="sxs-lookup"><span data-stu-id="c44bd-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="c44bd-109">Caché en Redis de Azure le proporciona acceso a una caché en Redis segura y dedicada, administrada por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c44bd-109">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="c44bd-110">Se puede obtener acceso a su caché desde cualquier aplicación dentro de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c44bd-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="c44bd-111">En este tema se explica cómo comenzar a usar Caché en Redis de Azure mediante Node.js.</span><span class="sxs-lookup"><span data-stu-id="c44bd-111">This topic shows you how to get started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="c44bd-112">Para obtener otro ejemplo de uso de Caché en Redis de Azure con Node.js, consulte [Creación de una aplicación de chat Node.js con Socket.IO en un sitio web de Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="c44bd-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c44bd-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c44bd-113">Prerequisites</span></span>
<span data-ttu-id="c44bd-114">Instale [node_redis](https://github.com/mranney/node_redis):</span><span class="sxs-lookup"><span data-stu-id="c44bd-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="c44bd-115">En este tutorial se usa [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="c44bd-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="c44bd-116">Para ver ejemplos del uso de otros clientes de Node.js, consulte la documentación individual de los clientes de Node.js, que encontrará en [clientes Redis de Node.js](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="c44bd-116">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="c44bd-117">Crear una caché de Redis en Azure</span><span class="sxs-lookup"><span data-stu-id="c44bd-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="c44bd-118">Recuperación del nombre de host y las claves de acceso</span><span class="sxs-lookup"><span data-stu-id="c44bd-118">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="c44bd-119">Conexión a la caché de forma segura mediante SSL</span><span class="sxs-lookup"><span data-stu-id="c44bd-119">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="c44bd-120">Las últimas compilaciones de [node_redis](https://github.com/mranney/node_redis) permiten conectarse a Azure Redis Cache mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="c44bd-120">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="c44bd-121">En el ejemplo siguiente se muestra cómo conectarse a Caché en Redis de Azure con el punto de conexión SSL de 6380.</span><span class="sxs-lookup"><span data-stu-id="c44bd-121">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="c44bd-122">Reemplace `<name>` por el nombre de la memoria caché y `<key>` por su clave principal o secundaria, tal como se ha descrito en la sección anterior, [Recuperación del nombre de host y las claves de acceso](#retrieve-the-host-name-and-access-keys).</span><span class="sxs-lookup"><span data-stu-id="c44bd-122">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="c44bd-123">El puerto no SSL está deshabilitado para instancias nuevas de Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="c44bd-123">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="c44bd-124">Si usa otro cliente incompatible con SSL, consulte [cómo habilitar el puerto no SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="c44bd-124">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="c44bd-125">Agregar algo a la memoria caché y recuperarlo</span><span class="sxs-lookup"><span data-stu-id="c44bd-125">Add something to the cache and retrieve it</span></span>
<span data-ttu-id="c44bd-126">En el ejemplo siguiente se muestra cómo conectarse a una instancia de Caché en Redis de Azure y almacenar y recuperar un elemento de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="c44bd-126">The following example shows you how to connect to an Azure Redis Cache instance, and store and retrieve an item from the cache.</span></span> <span data-ttu-id="c44bd-127">Para ver otros ejemplos sobre el uso de Redis con el cliente [node_redis](https://github.com/mranney/node_redis), consulte [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="c44bd-127">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="c44bd-128">Salida:</span><span class="sxs-lookup"><span data-stu-id="c44bd-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="c44bd-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c44bd-129">Next steps</span></span>
* <span data-ttu-id="c44bd-130">[Habilite los diagnósticos de cache](cache-how-to-monitor.md#enable-cache-diagnostics) para que pueda [supervisar](cache-how-to-monitor.md) el estado de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="c44bd-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span>
* <span data-ttu-id="c44bd-131">Lea la [documentación de Redis](http://redis.io/documentation)oficial.</span><span class="sxs-lookup"><span data-stu-id="c44bd-131">Read the official [Redis documentation](http://redis.io/documentation).</span></span>

