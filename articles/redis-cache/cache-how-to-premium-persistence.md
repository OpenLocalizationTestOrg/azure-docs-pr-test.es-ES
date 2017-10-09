---
title: "persistencia de los datos aaaHow tooconfigure para una caché de Redis de Azure Premium"
description: "Obtenga información acerca de cómo tooconfigure y administrar las instancias de caché en Redis de Azure de nivel Premium de persistencia de datos"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: sdanie
ms.openlocfilehash: 62feb6f5522e0270487f045eb303bf852434143d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-persistence-for-a-premium-azure-redis-cache"></a>¿Cómo tooconfigure persistencia de los datos de una caché en Redis de Azure Premium
Caché en Redis de Azure tiene ofertas de caché diferentes que proporcionan flexibilidad en la elección de Hola de tamaño de caché y las características, incluidas las características de nivel Premium como de agrupación en clústeres, la persistencia y la compatibilidad de red virtual. Este artículo describe cómo tooconfigure persistencia en un premium Redis de Azure caché de instancia.

Para obtener información sobre otras características de caché premium, consulte [nivel Premium de caché de Redis de Azure de introducción toohello](cache-premium-tier-intro.md).

## <a name="what-is-data-persistence"></a>¿Qué es la persistencia de datos?
[Redis persistencia](https://redis.io/topics/persistence) permite toopersist los datos almacenados en Redis. También puede tomar instantáneas y realizar copias de seguridad de los datos de hello, que puede cargar en el caso de un error de hardware. Se trata de una enorme ventaja con respecto a Basic o nivel estándar donde Hola a todos los datos se almacena en memoria y puede haber pérdida potencial de datos en caso de error donde los nodos de memoria caché están inactivos. 

Caché en Redis de Azure ofrece persistencia Redis con hello después de modelos:

* **Persistencia de RDB** -persistencia cuando RDB (base de datos de Redis) está configurada, Azure Redis Cache persiste una instantánea de memoria caché de Redis de hello en un formato binario toodisk tomando como base una frecuencia de copia de seguridad configurable de Redis. Si se produce un evento grave que deshabilita la caché de réplica y de saludo principal, se reconstruye caché hello mediante Hola la instantánea más reciente. Obtener más información sobre hello [ventajas](https://redis.io/topics/persistence#rdb-advantages) y [desventajas](https://redis.io/topics/persistence#rdb-disadvantages) de persistencia de RDB.
* **Persistencia de AOF** -persistencia cuando AOF (archivo solo anexar) está configurada, Azure Redis Cache guarda cada registro de tooa de operaciones de escritura que se ha guardado al menos una vez por segundo en una cuenta de almacenamiento de Azure. Si se produce un evento grave que deshabilita la caché de réplica y de saludo principal, se reconstruye caché hello mediante las operaciones de escritura de hello almacenado. Obtener más información sobre hello [ventajas](https://redis.io/topics/persistence#aof-advantages) y [desventajas](https://redis.io/topics/persistence#aof-disadvantages) de persistencia AOF.

Persistencia se configura de hello **nueva caché en Redis** hoja durante la creación de la memoria caché y en hello **menú recursos** Premium existente almacena en memoria caché.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Una vez se selecciona un plan de tarifa premium, haga clic en **Persistencia de Redis**.

![Persistencia de Redis][redis-cache-persistence]

Hello en los pasos en la sección siguiente Hola describe cómo tooconfigure Redis persistencia en la nueva caché premium. Una vez configurada la persistencia de Redis, haga clic en **crear** toocreate su premium nuevo la caché con Redis persistencia.

## <a name="enable-redis-persistence"></a>Habilitación de la persistencia de Redis

Redis se habilita la persistencia en hello **Redis persistencia de los datos** hoja seleccionando cualquiera **RDB** o **AOF** persistencia. Memoria caché de nuevo, esta hoja se tiene acceso durante el proceso de creación de la memoria caché de hello, como se describe en la sección anterior de Hola. Para las memorias caché existentes, Hola **Redis persistencia de los datos** hoja se obtiene acceso desde hello **menú recursos** de la memoria caché.

![Configuración de Redis][redis-cache-settings]


## <a name="configure-rdb-persistence"></a>Configuración de la persistencia de RDB

persistencia de RDB tooenable, haga clic en **RDB**. persistencia de RDB toodisable en una caché premium habilitados anteriormente, haga clic en **deshabilitado**.

![Persistencia de RDB en Redis][redis-cache-rdb-persistence]

intervalo copia de seguridad de saludo de tooconfigure, seleccione un **frecuencia de copia de seguridad** de lista desplegable de Hola. Las opciones disponibles son: **15 minutos**, **30 minutos**, **60 minutos**, **6 horas**, **12 horas** y **24 horas**. Este intervalo comienza a contar hacia abajo después de operación de copia de seguridad anterior de Hola se complete correctamente y cuando ha transcurrido se inicia una nueva copia de seguridad.

Haga clic en **cuenta de almacenamiento** tooselect Hola toouse de cuenta de almacenamiento y elija cualquiera hello **clave principal** o **clave secundaria** toouse de hello **almacenamiento Clave** lista desplegable. Debe elegir una cuenta de almacenamiento de hello misma región que la memoria caché de hello y un **almacenamiento Premium** cuenta se recomienda porque almacenamiento premium tiene un mayor rendimiento. 

> [!IMPORTANT]
> Si se vuelve a generar clave de almacenamiento de Hola para su cuenta de persistencia, debe volver a configurar clave deseado Hola Hola **clave de almacenamiento** lista desplegable.
> 
> 

Haga clic en **Aceptar** configuración de persistencia de toosave Hola.

siguiente copia de seguridad de Hello (o primera copia de seguridad para las cachés nuevas) se inicia una vez que transcurre el intervalo de frecuencia de copia de seguridad de saludo.

## <a name="configure-aof-persistence"></a>Configuración de la persistencia de AOF

persistencia de AOF tooenable, haga clic en **AOF**. persistencia de AOF toodisable en una caché premium habilitados anteriormente, haga clic en **deshabilitado**.

![Persistencia de AOF en Redis][redis-cache-aof-persistence]

persistencia de AOF tooconfigure, especifique un **primera cuenta de almacenamiento**. Esta cuenta de almacenamiento debe encontrarse en hello misma región que la memoria caché de hello y un **almacenamiento Premium** cuenta se recomienda porque almacenamiento premium tiene un mayor rendimiento. También puede configurar una cuenta de almacenamiento adicional denominada **Segunda cuenta de almacenamiento**. Si se configura una segunda cuenta de almacenamiento, hello escrituras toohello réplica caché se escriben toothis una segunda cuenta de almacenamiento. Para cada cuenta de almacenamiento configurada, elija cualquier hello **clave principal** o **clave secundaria** toouse de hello **clave de almacenamiento** lista desplegable. 

> [!IMPORTANT]
> Si se vuelve a generar clave de almacenamiento de Hola para su cuenta de persistencia, debe volver a configurar clave deseado Hola Hola **clave de almacenamiento** lista desplegable.
> 
> 

Cuando se habilita la persistencia de AOF, escribir la caché de toohello de operaciones se guardan toohello designado de la cuenta de almacenamiento (o cuentas si ha configurado una segunda cuenta de almacenamiento). En caso de hello de un error catastrófico que toma hacia abajo ambos Hola principal y caché de réplica, hello almacenado AOF registro es usan caché de hello toorebuild.

## <a name="persistence-faq"></a>P+F de persistencia
Hello lista siguiente contiene toocommonly respuestas preguntas más frecuentes sobre la persistencia de caché en Redis de Azure.

* [¿Puedo habilitar la persistencia en una memoria caché creada anteriormente?](#can-i-enable-persistence-on-a-previously-created-cache)
* [¿Se puede habilitar la persistencia AOF y RDB en hello mismo tiempo?](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [¿Qué modelo de persistencia debería elegir?](#which-persistence-model-should-i-choose)
* [¿Qué ocurre si he escalar tooa diferentes tamaños y se restaura una copia de seguridad realizada antes de la operación de escalado de hello?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a>Persistencia de RDB
* [¿Puedo cambiar frecuencia de copia de seguridad de hello RDB después de crear caché Hola?](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [¿Por qué si tengo una frecuencia de copia de seguridad de RDB de 60 minutos hay más de 60 minutos entre las copias de seguridad?](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [Copias de seguridad RDB antiguas toohello ¿qué ocurre cuando se realiza una copia de seguridad?](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a>Persistencia de AOF
* [¿Cuándo debo usar una segunda cuenta de almacenamiento?](#when-should-i-use-a-second-storage-account)
* [¿Afecta la persistencia de AOF a la productividad, la latencia o el rendimiento de la memoria caché?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [¿Cómo puedo quitar cuenta de almacenamiento de segundo de hello?](#how-can-i-remove-the-second-storage-account)
* [¿Qué es una reescritura y cómo afecta a la memoria caché?](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [¿Qué debo esperar al escalar una memoria caché con AOF habilitado?](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [¿Cómo se organizan los datos de AOF en el almacenamiento?](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a>¿Puedo habilitar la persistencia en una memoria caché creada anteriormente?
Sí, la persistencia de Redis puede configurarse tanto durante la creación de la memoria caché como en las memorias caché premium existente.

### <a name="can-i-enable-aof-and-rdb-persistence-at-hello-same-time"></a>¿Se puede habilitar la persistencia AOF y RDB en hello mismo tiempo?

No, puede habilitar solo RDB o AOF, pero no ambos al Hola mismo tiempo.

### <a name="which-persistence-model-should-i-choose"></a>¿Qué modelo de persistencia debería elegir?

Persistencia de AOF guarda cada registro de tooa de escritura, que tiene algún impacto en el rendimiento, en comparación con RDB persistencia que guarda las copias de seguridad en función de hello configurado intervalo de copia de seguridad, con un impacto mínimo en el rendimiento. Elija persistencia AOF si su objetivo principal es la pérdida de datos de toominimize y puede controlar una disminución del rendimiento de la memoria caché. Elija la persistencia de RDB si desea toomaintain un rendimiento óptimo en la memoria caché, pero todavía desea un mecanismo para la recuperación de datos.

* Obtener más información sobre hello [ventajas](https://redis.io/topics/persistence#rdb-advantages) y [desventajas](https://redis.io/topics/persistence#rdb-disadvantages) de persistencia de RDB.
* Obtener más información sobre hello [ventajas](https://redis.io/topics/persistence#aof-advantages) y [desventajas](https://redis.io/topics/persistence#aof-disadvantages) de persistencia AOF.

Para más información sobre el rendimiento al usar la persistencia de AOF, vea [¿Afecta la persistencia de AOF a la productividad, la latencia o el rendimiento de la memoria caché?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)

### <a name="what-happens-if-i-have-scaled-tooa-different-size-and-a-backup-is-restored-that-was-made-before-hello-scaling-operation"></a>¿Qué ocurre si he escalar tooa diferentes tamaños y se restaura una copia de seguridad realizada antes de la operación de escalado de hello?

Para la persistencia de RDB y AOF:

* Si ha escalado tooa mayor tamaño, no hay ningún impacto.
* Si ha escalado tooa menor tamaño, y tiene un personalizado [bases de datos](cache-configure.md#databases) establece que es mayor que hello [límite de bases de datos](cache-configure.md#databases) para el nuevo tamaño, no es restaurar datos en esas bases de datos. Para más información, consulte [¿Mi configuración de bases de datos personalizada se ve afectada durante el escalado?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)
* Si ha escalado tooa menor tamaño, y no hay espacio suficiente en hello menor tamaño toohold todos los datos de Hola desde la última copia de seguridad, clave de Hola se expulsen durante el proceso de restauración de Hola, normalmente mediante hello [allkeys lru](http://redis.io/topics/lru-cache) expulsión Directiva.

### <a name="can-i-change-hello-rdb-backup-frequency-after-i-create-hello-cache"></a>¿Puedo cambiar frecuencia de copia de seguridad de hello RDB después de crear caché Hola?
Sí, puede cambiar la frecuencia de copia de seguridad de hello para la persistencia de RDB en hello **Redis persistencia de los datos** hoja. Para instrucciones, vea [Configurar la persistencia de Redis](#configure-redis-persistence).

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a>¿Por qué si tengo una frecuencia de copia de seguridad de RDB de 60 minutos hay más de 60 minutos entre las copias de seguridad?
intervalo de frecuencia de copia de seguridad de persistencia de Hello RDB no se inicia hasta que el proceso de copia de seguridad anterior de Hola se ha completado correctamente. Si la frecuencia de copia de seguridad de hello es 60 minutos y tarda un toosuccessfully de 15 minutos de proceso de copia de seguridad completa, copia de seguridad siguiente hello no se inicia hasta 75 minutos después de hello hora de inicio de copia de seguridad anterior de Hola.

### <a name="what-happens-toohello-old-rdb-backups-when-a-new-backup-is-made"></a>Copias de seguridad RDB antiguas toohello ¿qué ocurre cuando se realiza una copia de seguridad?
Todas las copias de seguridad de persistencia de RDB excepto hello más reciente se eliminan automáticamente. Es posible que esta eliminación no se produzca inmediatamente pero las copias de seguridad anteriores no se guardan de manera indefinida.


### <a name="when-should-i-use-a-second-storage-account"></a>¿Cuándo debo usar una segunda cuenta de almacenamiento?

Debe usar una segunda cuenta de almacenamiento para la persistencia de AOF cuando crea que tiene mayor que las operaciones de conjunto esperado en la memoria caché de Hola.  Configuración de cuenta de almacenamiento secundaria Hola ayuda a garantizar que la memoria caché no alcanza los límites de ancho de banda de almacenamiento.

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a>¿Afecta la persistencia de AOF a la productividad, la latencia o el rendimiento de la memoria caché?

Persistencia AOF afecta al rendimiento por aproximadamente 15-20% al caché Hola está por debajo de la carga máxima (CPU y servidor de carga de ambos en un 90%). No debería haber problemas de latencia al caché Hola esté dentro de estos límites. Sin embargo, caché Hola alcanzará estos límites antes con AOF habilitado.

### <a name="how-can-i-remove-hello-second-storage-account"></a>¿Cómo puedo quitar cuenta de almacenamiento de segundo de hello?

Puede quitar la cuenta de almacenamiento secundaria de persistencia de hello AOF estableciendo la segunda cuenta de almacenamiento Hola Hola toobe mismo como primera cuenta de almacenamiento Hola. Para obtener instrucciones, vea [Configuración de la persistencia de AOF](#configure-aof-persistence).

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a>¿Qué es una reescritura y cómo afecta a la memoria caché?

Cuando el archivo de hello AOF pasa a ser lo suficientemente grande, una reescritura automáticamente se pone en cola en memoria caché de Hola. archivo AOF de hello Hello reescritura cambia de tamaño con el conjunto mínimo de hello operaciones necesarias toocreate Hola actual del conjunto de datos. Durante la reescribe, esperar límites de rendimiento de tooreach antes especialmente cuando se trabaja con grandes conjuntos de datos. Reescribe menor produce a menudo como archivo de hello AOF se vuelve mayor, pero tendrá una gran cantidad de tiempo cuando se produce.

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a>¿Qué debo esperar al escalar una memoria caché con AOF habilitado?

Si el archivo AOF de hello en tiempo de Hola de ajuste de escala es considerablemente grande, a continuación, espera hello tootake de operación de escalado más de lo esperado desde que se puede volver a cargar archivo hello una vez finalizada la escala.

Para obtener más información sobre cómo ampliar, consulte [¿qué ocurre si he escalar tooa diferentes tamaños y se restaura una copia de seguridad realizada antes de la operación de escalado de hello?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)

### <a name="how-is-my-aof-data-organized-in-storage"></a>¿Cómo se organizan los datos de AOF en el almacenamiento?

Datos almacenados en archivos AOF se dividen en varios blobs de página por el rendimiento del proceso de guardar Hola datos toostorage tooincrease del nodo. Hello siguiente tabla muestra cuántas blobs de página se utilizan para cada nivel de precios:

| Nivel Premium | Blobs |
|--------------|-------|
| P1           | 4 por partición    |
| P2           | 8 por partición    |
| P3           | 16 por partición   |
| P4           | 20 por partición   |

Cuando se habilita la agrupación en clústeres, cada partición de memoria caché de hello tiene su propio conjunto de blobs de página, como se indica en la tabla anterior de Hola. Por ejemplo, una caché P2 con tres particiones distribuye su archivo AOF entre 24 blobs en páginas (8 blobs por partición, con 3 particiones).

Después de una reescritura, hay dos conjuntos de archivos AOF en el almacenamiento. Reescribe se produce en segundo plano de Hola y anexa toohello primer conjunto de archivos, mientras que las operaciones de conjunto que se envían toohello caché durante la reescritura de hello anexan toohello segundo conjunto. Durante las operaciones de reescritura se almacena de forma temporal una copia de seguridad por si hubiera un error, pero se elimina inmediatamente después de que finalice la reescritura.


## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo toouse premium más características de caché.

* [Nivel de introducción toohello Premium de caché de Redis de Azure](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png
