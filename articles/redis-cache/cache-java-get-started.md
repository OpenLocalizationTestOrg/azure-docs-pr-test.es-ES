---
title: "aaaHow toouse caché en Redis de Azure con Java | Documentos de Microsoft"
description: "Introducción a Caché en Redis de Azure usando Java"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/13/2017
ms.author: sdanie
ms.openlocfilehash: 7768e879d71f61585b59cf4bd6634ba3f12e001d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-java"></a><span data-ttu-id="907ab-103">Cómo toouse caché de Redis de Azure con Java</span><span class="sxs-lookup"><span data-stu-id="907ab-103">How toouse Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="907ab-104">.NET</span><span class="sxs-lookup"><span data-stu-id="907ab-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="907ab-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="907ab-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="907ab-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="907ab-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="907ab-107">Java</span><span class="sxs-lookup"><span data-stu-id="907ab-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="907ab-108">Python</span><span class="sxs-lookup"><span data-stu-id="907ab-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="907ab-109">Azure proporciona de caché en Redis acceso tooa dedicado Redis caché, administrada por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="907ab-109">Azure Redis Cache gives you access tooa dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="907ab-110">Se puede obtener acceso a su caché desde cualquier aplicación dentro de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="907ab-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="907ab-111">Este tema muestra cómo se inicia tooget con caché en Redis de Azure con Java.</span><span class="sxs-lookup"><span data-stu-id="907ab-111">This topic shows you how tooget started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="907ab-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="907ab-112">Prerequisites</span></span>
<span data-ttu-id="907ab-113">[Jedis](https://github.com/xetorthio/jedis) - Cliente de Java para Redis</span><span class="sxs-lookup"><span data-stu-id="907ab-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="907ab-114">Este tutorial usa Jedis, pero puede usar cualquier cliente de Java enumerado en [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="907ab-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="907ab-115">Crear una caché de Redis en Azure</span><span class="sxs-lookup"><span data-stu-id="907ab-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="907ab-116">Recuperar claves de acceso y nombre de host de Hola</span><span class="sxs-lookup"><span data-stu-id="907ab-116">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="907ab-117">Conectarse de forma segura mediante SSL de caché de toohello</span><span class="sxs-lookup"><span data-stu-id="907ab-117">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="907ab-118">Hola la compilación más reciente de [jedis](https://github.com/xetorthio/jedis) proporcionan compatibilidad para la conexión tooAzure caché en Redis mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="907ab-118">hello latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="907ab-119">Hola de ejemplo siguiente muestra cómo usar caché en Redis de tooAzure de tooconnect Hola punto de conexión SSL de 6380.</span><span class="sxs-lookup"><span data-stu-id="907ab-119">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="907ab-120">Reemplace `<name>` con el nombre de saludo de la memoria caché y `<key>` con cualquiera su clave principal o secundaria como se describe en Hola anterior [recuperar claves de acceso y nombre de host de hello](#retrieve-the-host-name-and-access-keys) sección.</span><span class="sxs-lookup"><span data-stu-id="907ab-120">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="907ab-121">puerto no SSL de Hello está deshabilitado para las nuevas instancias de caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="907ab-121">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="907ab-122">Si usas otro cliente que no es compatible con SSL, vea [cómo tooenable Hola puerto no SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="907ab-122">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="907ab-123">Agregar algo toohello almacenar en caché y recuperarlos</span><span class="sxs-lookup"><span data-stu-id="907ab-123">Add something toohello cache and retrieve it</span></span>
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a><span data-ttu-id="907ab-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="907ab-124">Next steps</span></span>
* <span data-ttu-id="907ab-125">[Habilitar los diagnósticos de caché](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) para que pueda [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) Hola estado de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="907ab-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello health of your cache.</span></span>
* <span data-ttu-id="907ab-126">Lectura Hola oficial [Redis documentación](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="907ab-126">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>
