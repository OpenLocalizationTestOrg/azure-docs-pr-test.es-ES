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
# <a name="how-toouse-azure-redis-cache-with-java"></a>Cómo toouse caché de Redis de Azure con Java
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure proporciona de caché en Redis acceso tooa dedicado Redis caché, administrada por Microsoft. Se puede obtener acceso a su caché desde cualquier aplicación dentro de Microsoft Azure.

Este tema muestra cómo se inicia tooget con caché en Redis de Azure con Java.

## <a name="prerequisites"></a>Requisitos previos
[Jedis](https://github.com/xetorthio/jedis) - Cliente de Java para Redis

Este tutorial usa Jedis, pero puede usar cualquier cliente de Java enumerado en [http://redis.io/clients](http://redis.io/clients).

## <a name="create-a-redis-cache-on-azure"></a>Crear una caché de Redis en Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Recuperar claves de acceso y nombre de host de Hola
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Conectarse de forma segura mediante SSL de caché de toohello
Hola la compilación más reciente de [jedis](https://github.com/xetorthio/jedis) proporcionan compatibilidad para la conexión tooAzure caché en Redis mediante SSL. Hola de ejemplo siguiente muestra cómo usar caché en Redis de tooAzure de tooconnect Hola punto de conexión SSL de 6380. Reemplace `<name>` con el nombre de saludo de la memoria caché y `<key>` con cualquiera su clave principal o secundaria como se describe en Hola anterior [recuperar claves de acceso y nombre de host de hello](#retrieve-the-host-name-and-access-keys) sección.

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> puerto no SSL de Hello está deshabilitado para las nuevas instancias de caché en Redis de Azure. Si usas otro cliente que no es compatible con SSL, vea [cómo tooenable Hola puerto no SSL](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Agregar algo toohello almacenar en caché y recuperarlos
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


## <a name="next-steps"></a>Pasos siguientes
* [Habilitar los diagnósticos de caché](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) para que pueda [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) Hola estado de la memoria caché.
* Lectura Hola oficial [Redis documentación](http://redis.io/documentation).
