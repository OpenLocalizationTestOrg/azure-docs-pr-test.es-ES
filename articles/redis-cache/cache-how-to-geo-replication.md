---
title: "aaaHow tooconfigure replicación geográfica para caché en Redis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooreplicate instancias de la memoria caché en Redis de Azure regiones geográficas."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 375643dc-dbac-4bab-8004-d9ae9570440d
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: sdanie
ms.openlocfilehash: edcd6f202b51055d1a4e47ecaf11f9977d50aa81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-geo-replication-for-azure-redis-cache"></a>¿Cómo tooconfigure replicación geográfica para caché en Redis de Azure

La replicación geográfica proporciona un mecanismo para vincular dos instancias de Azure Redis Cache de nivel Premium. Una memoria caché se designa como caché primaria vinculada de Hola y Hola otro como caché secundaria vinculado de Hola. caché secundaria vinculado de Hello pasa a ser de solo lectura, y datos de caché principal toohello escrito es replican toohello secundario vinculado caché. Esta funcionalidad puede ser tooreplicate usa una memoria caché en regiones de Azure. Este artículo proporciona una guía tooconfiguring replicación geográfica para las instancias de caché en Redis de Azure de nivel Premium.

## <a name="geo-replication-prerequisites"></a>Requisitos previos de la replicación geográfica

debe cumplirse tooconfigure replicación geográfica entre dos cachés, Hola siguiendo los requisitos previos:

- Ambas debe ser cachés de [nivel Premium](cache-premium-tier-intro.md).
- Las memorias caché deben estar en hello misma suscripción de Azure.
- caché secundaria vinculado de Hola debe o bien ser Hola mismo nivel o un mayor nivel de precios que Hola principal vinculado la memoria caché de precios.
- Si Hola principal vinculado en caché tiene habilitada de agrupación en clústeres, caché secundaria vinculado de hello debe tener habilitado con hello de agrupación en clústeres mismo número de particiones que caché primaria vinculada de Hola.
- Ambas cachés deben estar creadas y en ejecución.
- La persistencia no debe estar habilitada en ninguna de las cachés.
- Replicación geográfica entre las memorias caché de Hola que se admite la misma red virtual. También se admite la replicación geográfica entre las memorias caché en redes virtuales diferentes, como redes virtuales Hola dos están configuradas de manera que los recursos en redes virtuales Hola son tooreach pueda entre sí a través de las conexiones TCP.

Después de configurar la replicación geográfica, hello las restricciones siguientes aplican tooyour par de caché vinculado:

- caché secundaria vinculado de Hello es de solo lectura; puede leer de él, pero no se puede escribir cualquier tooit de datos. 
- Se quita cualquier dato que estaba en caché de hello secundaria vinculado antes de que se agregó el vínculo de Hola. Si hello replicación geográfica es posteriormente, se elimina sin embargo, Hola replica datos permanecen en memoria caché vinculado secundaria Hola.
- No se puede iniciar un [la operación de escalado](cache-how-to-scale.md) en cualquier caché o [cambiar Hola número de particiones](cache-how-to-premium-clustering.md) si hello en caché tiene habilitada de agrupación en clústeres.
- No puede habilitar la persistencia en ninguna de las cachés.
- Puede usar [exportar](cache-how-to-import-export-data.md#export) con cualquier caché, pero sólo puede [importación](cache-how-to-import-export-data.md#import) en hello principal vinculado caché.
- No se puede eliminar caché vinculado o grupo de recursos de Hola que los contiene, hasta que quite el vínculo de replicación geográfica de Hola. Para obtener más información, vea [¿por qué operación Hola producirá un error cuando se ha intentado toodelete mi caché vinculado?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- Si dos cachés de Hola se encuentran en regiones diferentes, los costos de salida de red aplicarán toohello datos que se replican a través de la caché de las regiones toohello secundaria vinculado. ¿Para obtener más información, vea [cuánto cuesta tooreplicate Mis datos en regiones de Azure?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- No hay ninguna caché vinculado secundaria de toohello de conmutación automática por error si la caché principal de hello (y su réplica) dejan de funcionar. En las aplicaciones de cliente de orden toofailover, necesitaría toomanually Quitar vínculo de replicación geográfica de Hola y punto toohello de las aplicaciones de cliente de Hola de caché que antes era caché secundaria vinculado de Hola. ¿Para obtener más información, vea [cómo funciona la caché vinculado secundaria toohello la conmutación por error?](#how-does-failing-over-to-the-secondary-linked-cache-work)

## <a name="add-a-geo-replication-link"></a>Agregar un vínculo de replicación geográfica

1. toolink dos premium almacena en caché juntos para la replicación geográfica, haga clic en **georreplicación** en el menú de recursos de hello del caché Hola pensado como Hola principal vinculado almacenar en caché y, a continuación, haga clic en **vínculo de replicación Agregar caché**de hello **georreplicación** hoja.

    ![Agregar vínculo](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. Haga clic en nombre de Hola de hello deseado caché secundaria de hello **cachés compatibles** lista. Si la memoria caché deseada no se muestra en la lista de hello, compruebe que hello [requisitos previos de replicación geográfica](#geo-replication-prerequisites) para hello deseado caché secundaria se cumplen. toofilter Hola cachés por región, haga clic en la región deseada de hello en hello mapa toodisplay solo las cachés de hello **cachés compatibles** lista.

    ![Cachés compatibles de replicación geográfica](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    También puede iniciar Hola vinculación proceso o ver detalles acerca de la memoria caché secundaria de hello utilizando el menú contextual de Hola.

    ![Menú contextual de replicación geográfica](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. Haga clic en **vínculo** toolink Hola dos cachés juntos y comenzar el proceso de replicación de Hola.

    ![Vincular cachés](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. También puede ver progreso de hello del proceso de replicación de hello en hello **georreplicación** hoja.

    ![Estado de la vinculación](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    También puede ver Hola vinculación de estado de hello **Introducción** hoja para ambos cachés de hello principal y secundaria.

    ![Estado de cachés](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    Una vez completado el proceso de replicación de hello, Hola **vincular estado** cambia demasiado**correcto**.

    ![Estado de cachés](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    Durante el proceso de vinculación de hello, caché primaria vinculada de hello sigue estando disponible para su uso pero caché vinculado de hello secundaria no está disponible hasta que se complete el proceso de vinculación de Hola.

## <a name="remove-a-geo-replication-link"></a>Quitar un vínculo de replicación geográfica

1. tooremove Hola vínculo entre dos cachés y Detener replicación geográfica, haga clic en **desvincular cachés** de hello **georreplicación** hoja.
    
    ![Desvincular cachés](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    Cuando se completa el proceso de desvinculación de hello, caché secundaria Hola está disponible para las lecturas y escribe.

>[!NOTE]
>Cuando se quita el vínculo de replicación geográfica de hello, Hola los datos replicados de hello principal caché vinculado permanece en memoria caché secundaria de Hola.
>
>

## <a name="geo-replication-faq"></a>Preguntas más frecuentes sobre la replicación geográfica

- [¿Puedo usar la replicación geográfica con una caché de nivel Estándar o Básico?](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [¿Está disponible para su uso durante la vinculación de Hola o proceso desvinculando mi caché?](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [¿Puedo vincular más de dos cachés?](#can-i-link-more-than-two-caches-together)
- [¿Puedo vincular dos cachés de distintas suscripciones de Azure?](#can-i-link-two-caches-from-different-azure-subscriptions)
- [¿Puedo vincular dos cachés de tamaños distintos?](#can-i-link-two-caches-with-different-sizes)
- [¿Puedo usar la replicación geográfica con agrupación en clústeres habilitada?](#can-i-use-geo-replication-with-clustering-enabled)
- [¿Puedo usar la replicación geográfica con cachés en una VNET?](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [¿Puedo usar PowerShell o CLI de Azure toomanage replicación geográfica?](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [¿Cuánto cuesta tooreplicate Mis datos en regiones de Azure?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [¿Por qué operación Hola produjo un error cuando se ha intentado toodelete mi caché vinculado?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [¿Qué región se debe usar para la caché vinculada secundaria?](#what-region-should-i-use-for-my-secondary-linked-cache)
- [¿Cómo funciona la caché vinculado secundaria toohello la conmutación por error?](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a>¿Puedo usar la replicación geográfica con una caché de nivel Estándar o Básico?

No, la replicación geográfica solo está disponible para las cachés de nivel Premium.

### <a name="is-my-cache-available-for-use-during-hello-linking-or-unlinking-process"></a>¿Está disponible para su uso durante la vinculación de Hola o proceso desvinculando mi caché?

- Al vincular dos cachés juntos para la replicación geográfica, caché primaria vinculada de hello sigue estando disponible para su uso pero caché vinculado de hello secundaria no está disponible hasta que se complete el proceso de vinculación de Hola.
- Al quitar el vínculo de replicación geográfica de hello entre dos cachés, ambos cachés siguen estando disponibles para su uso.

### <a name="can-i-link-more-than-two-caches-together"></a>¿Puedo vincular más de dos cachés?

No, solo puede vincular dos cachés cuando se usa la replicación geográfica.

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a>¿Puedo vincular dos cachés de distintas suscripciones de Azure?

Las memorias caché no, ambas deben estar en hello misma suscripción de Azure.

### <a name="can-i-link-two-caches-with-different-sizes"></a>¿Puedo vincular dos cachés de tamaños distintos?

Sí, siempre que sea mayor que la caché principal vinculado de hello caché secundaria vinculado de Hola.

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a>¿Puedo usar la replicación geográfica con agrupación en clústeres habilitada?

Sí, siempre que las memorias caché tengan Hola mismo número de particiones.

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a>¿Puedo usar la replicación geográfica con cachés en una VNET?

Sí, se admite la replicación geográfica de cachés en VNET. 

- Replicación geográfica entre las memorias caché de Hola que se admite la misma red virtual.
- También se admite la replicación geográfica entre las memorias caché en redes virtuales diferentes, como redes virtuales Hola dos están configuradas de manera que los recursos en redes virtuales Hola son tooreach pueda entre sí a través de las conexiones TCP.

### <a name="can-i-use-powershell-or-azure-cli-toomanage-geo-replication"></a>¿Puedo usar PowerShell o CLI de Azure toomanage replicación geográfica?

En este momento sólo se pueden administrar utilizando la replicación geográfica Hola portal de Azure.

### <a name="how-much-does-it-cost-tooreplicate-my-data-across-azure-regions"></a>¿Cuánto cuesta tooreplicate Mis datos en regiones de Azure?

Cuando se utiliza la replicación geográfica, datos de caché principal vinculado de hello están caché replicada toohello secundarias vinculada. Si vincula Hola dos cachés están en hello misma región de Azure, no hay ningún cargo por transferencia de datos de Hola. Si hello dos vinculado cachés están en diferentes regiones de Azure, hello cargo de transferencia de datos de replicación geográfica es costos de ancho de banda de Hola de replicación que toohello datos de otra región de Azure. Para más información, consulte [Detalles de precios de ancho de banda](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="why-did-hello-operation-fail-when-i-tried-toodelete-my-linked-cache"></a>¿Por qué operación Hola produjo un error cuando se ha intentado toodelete mi caché vinculado?

Cuando dos cachés están vinculadas entre sí, no se puede eliminar el grupo de recursos de memoria caché o hello incluidos en ellos hasta que quite el vínculo de replicación geográfica de Hola. Si trata de grupo de recursos de hello toodelete que contiene uno o ambos de hello vinculado cachés, hello otros recursos en el grupo de recursos de Hola se eliminan, pero grupo de recursos de hello permanece en Hola `deleting` estado y los vinculan las memorias caché de grupo de recursos de Hola permanecen en hello `running` estado. eliminación de hello toocomplete del grupo de recursos de Hola y Hola vinculado memorias caché dentro de él, romper el vínculo de replicación geográfica de hello tal y como se describe en [quitar un vínculo de replicación geográfica](#remove-a-geo-replication-link).

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a>¿Qué región se debe usar para la caché vinculada secundaria?

En general, se recomienda para su tooexist de caché en hello misma región de Azure como aplicación Hola que tiene acceso a él. Si la aplicación tiene una región principal y de reserva, las cachés principal y secundaria deben existir en esas mismas regiones. Para más información sobre regiones emparejadas, consulte el artículo sobre [procedimientos recomendados: regiones emparejadas de Azure](../best-practices-availability-paired-regions.md).

### <a name="how-does-failing-over-toohello-secondary-linked-cache-work"></a>¿Cómo funciona la caché vinculado secundaria toohello la conmutación por error?

En la versión inicial de saludo de la replicación geográfica, caché en Redis de Azure no admite conmutación por error automática en regiones de Azure. La replicación geográfica se usa principalmente en un escenario de recuperación ante desastres. En un escenario de recuperación distater, los clientes deberían actualizar la pila de toda la aplicación hello en una región de copia de seguridad de manera coordinada en lugar de permitir que los componentes de aplicaciones individuales a decidir cuándo tooswitch tootheir copias de seguridad por sí solas. Esto es especialmente relevante tooRedis. Una de las principales ventajas de Hola de Redis es que es un almacén de latencia muy baja. Si Redis utilizado por una aplicación conmuta por error tooa otra región de Azure pero no a nivel de proceso de hello, Hola agrega tiempo de viaje de ida y vuelta tendría un efecto notable en el rendimiento. Por este motivo, nos gustaría tooavoid Redis errores sobre automáticamente debido a problemas de disponibilidad de tootransient.

Actualmente, conmutación por error de tooinitiate hello, necesita tooremove Hola replicación geográfica vincular Hola portal de Azure y, a continuación, cambie el extremo de conexión de hello en el cliente de Redis Hola desde secundario de hello principal caché vinculado toohello (anteriormente vinculado) caché. Cuando Hola se desasoció dos cachés, réplica de Hola se convierte en normal nuevo caché de lectura y escritura y acepta solicitudes directamente desde los clientes de Redis.


## <a name="next-steps"></a>Pasos siguientes

Obtener más información sobre hello [nivel Premium de caché de Redis de Azure](cache-premium-tier-intro.md).

