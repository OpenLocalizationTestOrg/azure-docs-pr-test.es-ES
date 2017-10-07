---
title: "aaaHow toouse caché en Redis de Azure con Node.js | Documentos de Microsoft"
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
ms.openlocfilehash: dc8732041d2c4e5793e684e0c80b87a1c9d17f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a><span data-ttu-id="d842b-103">Cómo toouse caché de Redis de Azure con Node.js</span><span class="sxs-lookup"><span data-stu-id="d842b-103">How toouse Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d842b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d842b-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="d842b-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d842b-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="d842b-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="d842b-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="d842b-107">Java</span><span class="sxs-lookup"><span data-stu-id="d842b-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="d842b-108">Python</span><span class="sxs-lookup"><span data-stu-id="d842b-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="d842b-109">Azure le permite de caché en Redis acceder tooa dedicado Redis caché segura, administrada por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d842b-109">Azure Redis Cache gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="d842b-110">Se puede obtener acceso a su caché desde cualquier aplicación dentro de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d842b-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="d842b-111">Este tema muestra cómo se inicia tooget con caché en Redis de Azure con Node.js.</span><span class="sxs-lookup"><span data-stu-id="d842b-111">This topic shows you how tooget started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="d842b-112">Para obtener otro ejemplo de uso de Caché en Redis de Azure con Node.js, consulte [Creación de una aplicación de chat Node.js con Socket.IO en un sitio web de Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="d842b-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d842b-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d842b-113">Prerequisites</span></span>
<span data-ttu-id="d842b-114">Instale [node_redis](https://github.com/mranney/node_redis):</span><span class="sxs-lookup"><span data-stu-id="d842b-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="d842b-115">En este tutorial se usa [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="d842b-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="d842b-116">Para obtener ejemplos del uso de otros clientes de Node.js, consulte la documentación de individuales de Hola para clientes de Node.js Hola enumerados en [Node.js Redis clientes](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="d842b-116">For examples of using other Node.js clients, see hello individual documentation for hello Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="d842b-117">Crear una caché de Redis en Azure</span><span class="sxs-lookup"><span data-stu-id="d842b-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="d842b-118">Recuperar claves de acceso y nombre de host de Hola</span><span class="sxs-lookup"><span data-stu-id="d842b-118">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="d842b-119">Conectarse de forma segura mediante SSL de caché de toohello</span><span class="sxs-lookup"><span data-stu-id="d842b-119">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="d842b-120">Hola la compilación más reciente de [node_redis](https://github.com/mranney/node_redis) proporcionan compatibilidad para la conexión tooAzure caché en Redis mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="d842b-120">hello latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="d842b-121">Hola de ejemplo siguiente muestra cómo usar caché en Redis de tooAzure de tooconnect Hola punto de conexión SSL de 6380.</span><span class="sxs-lookup"><span data-stu-id="d842b-121">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="d842b-122">Reemplace `<name>` con el nombre de saludo de la memoria caché y `<key>` con cualquiera su clave principal o secundaria como se describe en Hola anterior [recuperar claves de acceso y nombre de host de hello](#retrieve-the-host-name-and-access-keys) sección.</span><span class="sxs-lookup"><span data-stu-id="d842b-122">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="d842b-123">puerto no SSL de Hello está deshabilitado para las nuevas instancias de caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="d842b-123">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="d842b-124">Si usas otro cliente que no es compatible con SSL, vea [cómo tooenable Hola puerto no SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="d842b-124">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="d842b-125">Agregar algo toohello almacenar en caché y recuperarlos</span><span class="sxs-lookup"><span data-stu-id="d842b-125">Add something toohello cache and retrieve it</span></span>
<span data-ttu-id="d842b-126">Hola siguiente ejemplo se muestra cómo tooconnect tooan Redis de Azure, almacenar en caché la instancia y almacena y recuperar un elemento de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="d842b-126">hello following example shows you how tooconnect tooan Azure Redis Cache instance, and store and retrieve an item from hello cache.</span></span> <span data-ttu-id="d842b-127">Para obtener más ejemplos del uso de Redis con hello [node_redis](https://github.com/mranney/node_redis) cliente, consulte [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="d842b-127">For more examples of using Redis with hello [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="d842b-128">Salida:</span><span class="sxs-lookup"><span data-stu-id="d842b-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="d842b-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d842b-129">Next steps</span></span>
* <span data-ttu-id="d842b-130">[Habilitar los diagnósticos de caché](cache-how-to-monitor.md#enable-cache-diagnostics) para que pueda [monitor](cache-how-to-monitor.md) Hola estado de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="d842b-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span>
* <span data-ttu-id="d842b-131">Lectura Hola oficial [Redis documentación](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="d842b-131">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>

