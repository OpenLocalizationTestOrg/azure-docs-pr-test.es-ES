---
title: "aaaHow toouse caché en Redis de Azure con Python | Documentos de Microsoft"
description: "Introducción a Caché en Redis de Azure usando Python"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: 74c03eb4ce17ff3574595fd2bb37e399d71c6eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-python"></a>Cómo toouse caché de Redis de Azure con Python
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Este tema muestra cómo se inicia tooget con caché en Redis de Azure con Python.

## <a name="prerequisites"></a>Requisitos previos
Instale [redis-py](https://github.com/andymccurdy/redis-py).

## <a name="create-a-redis-cache-on-azure"></a>Crear una caché de Redis en Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Recuperar claves de acceso y nombre de host de Hola
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-hello-non-ssl-endpoint"></a>Habilitar el punto de conexión de hello sin SSL
Algunos clientes de Redis no son compatibles con SSL y por hello predeterminado [puerto no SSL está deshabilitado para las nuevas instancias de caché en Redis de Azure](cache-configure.md#access-ports). En tiempo de Hola de redactar este artículo, Hola [redis copiar](https://github.com/andymccurdy/redis-py) cliente no es compatible con SSL. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Agregar algo toohello almacenar en caché y recuperarlos
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


Reemplace `<name>` por el nombre de la memoria caché y `key` por la clave de acceso.

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
