---
title: "aaaHow tooadminister caché en Redis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo reiniciar como tareas de administración de tooperform y programar actualizaciones para caché en Redis de Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a>Cómo tooadminister Redis de Azure almacenan en caché
Este tema describe cómo tareas como administración de tooperform [reiniciar](#reboot) y [programar actualizaciones](#schedule-updates) para las instancias de caché en Redis de Azure.

## <a name="reboot"></a>Reboot
Hola **reiniciar** hoja permite tooreboot uno o varios nodos de la memoria caché. Esta capacidad de reinicio permite que se tootest la aplicación para proporcionar resistencia si se produce un error de un nodo de caché.

![Reboot](./media/cache-administration/redis-cache-administration-reboot.png)

Seleccione tooreboot de nodos de Hola y haga clic en **reiniciar**.

![Reboot](./media/cache-administration/redis-cache-reboot.png)

Si tiene una caché premium con clúster habilitado, puede seleccionar qué particiones de hello caché tooreboot.

![Reboot](./media/cache-administration/redis-cache-reboot-cluster.png)

tooreboot uno o varios nodos de la memoria caché, seleccione los nodos de hello deseado y haga clic en **reiniciar**. Si tiene una caché premium con clúster habilitado, seleccione tooreboot de particiones de hello deseado y, a continuación, haga clic en **reiniciar**. Después de unos minutos, Hola reinicio de los nodos seleccionados y son volver a conectarse más tarde unos minutos.

impacto de Hello en las aplicaciones de cliente varía en función de qué nodos que se reinicie.

* **Master** : al nodo maestro hello es reiniciado, Azure Redis Cache se produce un error en el nodo de la réplica de toohello y promociona toomaster. Durante esta conmutación por error, puede haber un breve intervalo en el que las conexiones puedan realizarse toohello caché.
* **Esclavo** : cuando se reinicia el nodo esclavo hello, normalmente no hay ningún cliente de toocache de impacto.
* **Maestro y esclavo** : cuando se reinician ambos nodos de memoria caché, se pierden todos los datos en hello caché y las conexiones toohello errores de la memoria caché hasta que el nodo principal de hello vuelve a conectarse. Si ha configurado [persistencia de los datos](cache-how-to-premium-persistence.md), copia de seguridad más reciente de Hola se restaura cuando caché Hola se pone en línea, pero se perderán las escrituras de caché que se produjeron después de la copia de seguridad más reciente de Hola.
* **La caché de nodos de una prima con clúster habilitado** : al reiniciar uno o más nodos de una caché premium con el clúster está habilitada, Hola comportamiento para hello seleccionado nodos Hola igual como cuando reinicie correspondiente Hola o nodos de no agrupado memoria caché.

> [!IMPORTANT]
> El reinicio ahora está disponible para todos los planes de tarifas.
> 
> 

## <a name="reboot-faq"></a>Preguntas más frecuentes sobre el reinicio
* [Qué nodo ¿reiniciar tootest mi aplicación?](#which-node-should-i-reboot-to-test-my-application)
* [¿Se puede reiniciar los conexiones de cliente de hello caché tooclear?](#can-i-reboot-the-cache-to-clear-client-connections)
* [¿Se pierden los datos de mi memoria caché si reinicio?](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [¿Puedo reiniciar la caché con PowerShell, CLI u otras herramientas de administración?](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [¿Los precios de capas pueden usar la funcionalidad de reinicio de hello?](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a>Qué nodo ¿reiniciar tootest mi aplicación?
resistencia de hello tootest de la aplicación frente a errores del nodo principal de hello de la memoria caché, reinicio hello **Master** nodo. resistencia de hello tootest de la aplicación frente a errores de nodo secundario de hello, reinicio hello **esclavo** nodo. resistencia de hello tootest de la aplicación frente a errores del total de memoria caché de hello, reinicie **ambos** nodos.

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a>¿Se puede reiniciar los conexiones de cliente de hello caché tooclear?
Sí, si reinicia caché Hola que se borran todas las conexiones de cliente. Reiniciar el sistema puede resultar útil en caso de hello donde todas las conexiones de cliente se agotan debido a errores de lógica de tooa o un error de aplicación de cliente de Hola. Cada nivel de precios tiene distintos [límites de conexión de cliente](cache-configure.md#default-redis-server-configuration) para Hola diversos tamaños y cuando se alcanzan estos límites, no se aceptan más conexiones de cliente. Reiniciar el sistema de caché de hello proporciona un tooclear de manera todas las conexiones de cliente.

> [!IMPORTANT]
> Si reinicia las conexiones de cliente de caché tooclear, StackExchange.Redis vuelve a conectarse automáticamente cuando se vuelve a estar conectado nodo de Redis Hola. Si no se resuelve el problema subyacente hello, las conexiones de cliente de hello pueden seguir toobe ha consumido.
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a>¿Se pierden los datos de mi memoria caché si reinicio?
Si reinicia ambas hello **Master** y **esclavo** nodos, se pierden todos los datos en memoria caché de hello (o en esa partición si utilizas una caché premium con clúster habilitado). Si ha configurado [persistencia de los datos](cache-how-to-premium-persistence.md), copia de seguridad más reciente de Hola se restaurará cuando caché Hola se pone en línea, pero se perderán las escrituras de caché que se han producido después de que se realizó la copia de seguridad de Hola.

Si reinicia solo uno de los nodos de hello, datos no se pierde por lo general, pero todavía puede ser. Por ejemplo, si se reinicia el nodo principal de hello y una memoria caché de escritura está en curso, datos de Hola de escritura de caché de hello es perdido. Otro escenario de pérdida de datos sería si un nodo de reinicio y Hola otro nodo ocurre toogo hacia abajo debido a error de tooa en hello mismo tiempo. ¿Para obtener más información sobre las posibles causas de pérdida de datos, vea [qué datos toomy problema en Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a>¿Puedo reiniciar la caché con PowerShell, CLI u otras herramientas de administración?
Sí, para PowerShell instrucciones consulte [tooreboot una caché de Redis](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a>¿Los precios de capas pueden usar la funcionalidad de reinicio de hello?
El reinicio está disponible para todos los planes de tarifas.

## <a name="schedule-updates"></a>Programar actualizaciones
Hola **programar actualizaciones** hoja permite toodesignate una ventana de mantenimiento de su caché de nivel Premium. Cuando se especifica la ventana de mantenimiento de hello, se realizan las actualizaciones de servidor Redis durante este período. 

> [!NOTE] 
> ventana de mantenimiento de Hola aplica solo las actualizaciones de servidor de tooRedis y tooany Azure actualiza o actualiza el sistema de operativo toohello de máquinas virtuales de Hola que hospedan la memoria caché de Hola.
> 
> 

![Programar actualizaciones](./media/cache-administration/redis-schedule-updates.png)

toospecify una ventana de mantenimiento, los días de hello deseado y especifique la hora de inicio de ventana de mantenimiento de Hola para cada día y haga clic en **Aceptar**. Tenga en cuenta que es hora de ventana de mantenimiento de hello en UTC. 

> [!NOTE]
> ventana de mantenimiento de Hello predeterminado para las actualizaciones es de cinco horas. Este valor no es configurable de hello portal de Azure, pero puede configurarlo en PowerShell mediante hello `MaintenanceWindow` parámetro de hello [AzureRmRedisCacheScheduleEntry New](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet. Para obtener más información, consulte [¿Se pueden administrar las actualizaciones programadas con PowerShell, CLI u otras herramientas de administración?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)
> 
> 

## <a name="schedule-updates-faq"></a>Preguntas más frecuentes sobre la programación de actualizaciones
* [¿Cuándo las actualizaciones se producen si no se usa Hola programación actualizaciones característica?](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [¿Qué tipo de actualizaciones se realizan durante el saludo programado una ventana de mantenimiento?](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [¿Se pueden administrar las actualizaciones programadas con PowerShell, CLI u otras herramientas de administración?](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [¿Los precios de capas pueden usar la funcionalidad de las actualizaciones de programación de hello?](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a>¿Cuándo las actualizaciones se producen si no se usa Hola programación actualizaciones característica?
Si no especifica un período de mantenimiento, las actualizaciones pueden realizarse en cualquier momento.

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a>¿Qué tipo de actualizaciones se realizan durante el saludo programado una ventana de mantenimiento?
Redis solo servidor se realizan las actualizaciones durante la ventana de mantenimiento programada Hola. ventana de mantenimiento de Hello no aplica la actualización de tooAzure o actualiza el sistema operativo de la VM de toohello.

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a>¿Se pueden administrar las actualizaciones programadas con PowerShell, CLI u otras herramientas de administración?
Sí, puede administrar las actualizaciones programadas con hello siguientes cmdlets de PowerShell:

* [Get-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [New-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [Remove-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a>¿Los precios de capas pueden usar la funcionalidad de las actualizaciones de programación de hello?
Hola **programar actualizaciones** característica solo está disponible en premium Hola nivel de precios.

## <a name="next-steps"></a>Pasos siguientes
* Explore más características del [nivel premium de Azure Redis Cache](cache-premium-tier-intro.md) .

