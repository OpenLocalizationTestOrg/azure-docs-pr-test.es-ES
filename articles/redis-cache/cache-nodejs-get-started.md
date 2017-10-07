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
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a>Cómo toouse caché de Redis de Azure con Node.js
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure le permite de caché en Redis acceder tooa dedicado Redis caché segura, administrada por Microsoft. Se puede obtener acceso a su caché desde cualquier aplicación dentro de Microsoft Azure.

Este tema muestra cómo se inicia tooget con caché en Redis de Azure con Node.js. Para obtener otro ejemplo de uso de Caché en Redis de Azure con Node.js, consulte [Creación de una aplicación de chat Node.js con Socket.IO en un sitio web de Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).

## <a name="prerequisites"></a>Requisitos previos
Instale [node_redis](https://github.com/mranney/node_redis):

    npm install redis

En este tutorial se usa [node_redis](https://github.com/mranney/node_redis). Para obtener ejemplos del uso de otros clientes de Node.js, consulte la documentación de individuales de Hola para clientes de Node.js Hola enumerados en [Node.js Redis clientes](http://redis.io/clients#nodejs).

## <a name="create-a-redis-cache-on-azure"></a>Crear una caché de Redis en Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Recuperar claves de acceso y nombre de host de Hola
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Conectarse de forma segura mediante SSL de caché de toohello
Hola la compilación más reciente de [node_redis](https://github.com/mranney/node_redis) proporcionan compatibilidad para la conexión tooAzure caché en Redis mediante SSL. Hola de ejemplo siguiente muestra cómo usar caché en Redis de tooAzure de tooconnect Hola punto de conexión SSL de 6380. Reemplace `<name>` con el nombre de saludo de la memoria caché y `<key>` con cualquiera su clave principal o secundaria como se describe en Hola anterior [recuperar claves de acceso y nombre de host de hello](#retrieve-the-host-name-and-access-keys) sección.

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> puerto no SSL de Hello está deshabilitado para las nuevas instancias de caché en Redis de Azure. Si usas otro cliente que no es compatible con SSL, vea [cómo tooenable Hola puerto no SSL](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Agregar algo toohello almacenar en caché y recuperarlos
Hola siguiente ejemplo se muestra cómo tooconnect tooan Redis de Azure, almacenar en caché la instancia y almacena y recuperar un elemento de caché de Hola. Para obtener más ejemplos del uso de Redis con hello [node_redis](https://github.com/mranney/node_redis) cliente, consulte [http://redis.js.org/](http://redis.js.org/).

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

Salida:

    OK
    value


## <a name="next-steps"></a>Pasos siguientes
* [Habilitar los diagnósticos de caché](cache-how-to-monitor.md#enable-cache-diagnostics) para que pueda [monitor](cache-how-to-monitor.md) Hola estado de la memoria caché.
* Lectura Hola oficial [Redis documentación](http://redis.io/documentation).

