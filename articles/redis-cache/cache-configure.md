---
title: "aaaHow tooconfigure caché en Redis de Azure | Documentos de Microsoft"
description: "Comprender la configuración de Redis Hola predeterminada para caché en Redis de Azure y obtenga información acerca de cómo tooconfigure su Redis de Azure, instancias de caché"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a>Cómo tooconfigure Redis de Azure almacenan en caché
Este tema describe cómo Hola tooreview y actualización de configuración para las instancias de caché en Redis de Azure y la configuración del servidor de Redis portadas Hola predeterminado para instancias de caché en Redis de Azure.

> [!NOTE]
> Para obtener más información sobre cómo configurar y usar las características de caché premium, consulte [cómo persistencia tooconfigure](cache-how-to-premium-persistence.md), [cómo tooconfigure clústeres](cache-how-to-premium-clustering.md), y [cómo son compatibles con tooconfigure red Virtual ](cache-how-to-premium-vnet.md).
> 
> 

## <a name="configure-redis-cache-settings"></a>Configuración de opciones de la memoria caché en Redis
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Configuración de caché en Redis de Azure se ven y se configuran en hello **caché en Redis** hoja con la opción hello **menú recursos**.

![Caché en Redis - Configuración](./media/cache-configure/redis-cache-settings.png)

Puede ver y configurar Hola después de la configuración mediante hello **menú recursos**.

* [Información general](#overview)
* [Registro de actividad](#activity-log)
* [Control de acceso (IAM)](#access-control-iam)
* [Etiquetas](#tags)
* [Diagnóstico y solución de problemas](#diagnose-and-solve-problems)
* [Configuración](#settings)
    * [Claves de acceso](#access-keys)
    * [Configuración avanzada](#advanced-settings)
    * [Asesor de caché en Redis](#redis-cache-advisor)
    * [Escala](#scale)
    * [Tamaño del Clúster en Redis](#cluster-size)
    * [Persistencia de datos de Redis](#redis-data-persistence)
    * [Programación de actualizaciones](#schedule-updates)
    * [Replicación geográfica](#geo-replication)
    * [Virtual Network](#virtual-network)
    * [Firewall](#firewall)
    * [Propiedades](#properties)
    * [Bloqueos](#locks)
    * [Script de automatización](#automation-script)
* [Administración](#administration)
    * [Importación de datos](#importexport)
    * [Exportación de datos](#importexport)
    * [Reboot](#reboot)
* [Supervisión](#monitoring)
    * [Métricas de Redis](#redis-metrics)
    * [Reglas de alertas](#alert-rules)
    * [Diagnóstico](#diagnostics)
* [Configuración de soporte técnico y solución de problemas](#support-amp-troubleshooting-settings)
    * [Estado de los recursos](#resource-health)
    * [Nueva solicitud de soporte técnico](#new-support-request)


## <a name="overview"></a>Información general

**Información general** proporciona también con información básica sobre la memoria caché, como el nombre, puertos, plan de tarifa y las métricas de la caché seleccionada.

### <a name="activity-log"></a>Registro de actividades

Haga clic en **registro de actividad** tooview acciones realizan en la memoria caché. También puede usar filtrado tooexpand esta tooinclude ver otros recursos. Para obtener más información sobre cómo trabajar con los registros de auditoría, consulte [Operaciones de auditoría con Resource Manager](../azure-resource-manager/resource-group-audit.md). Para obtener más información sobre la supervisión de eventos de Caché en Redis de Azure, consulte [Operaciones y alertas](cache-how-to-monitor.md#operations-and-alerts).

### <a name="access-control-iam"></a>Control de acceso (IAM)

Hola **(de índices IAM) de control de acceso** sección proporciona compatibilidad para control de acceso basado en roles (RBAC) en hello Azure toohelp portal las organizaciones a cumplir sus requisitos de administración de acceso sencilla y precisa. Para obtener más información, consulte [el control de acceso basada en roles en el portal de Azure hello](../active-directory/role-based-access-control-configure.md).

### <a name="tags"></a>Etiquetas

Hola **etiquetas** sección le ayudará a organizar los recursos. Para obtener más información, consulte [mediante etiquetas tooorganize los recursos de Azure](../azure-resource-manager/resource-group-using-tags.md).


### <a name="diagnose-and-solve-problems"></a>Diagnosticar y solucionar problemas

Haga clic en **diagnosticar y resolver problemas** toobe proporcionada con problemas comunes y estrategias para resolverlos.



## <a name="settings"></a>Settings
Hola **configuración** sección permite tooaccess y configurar Hola después de la configuración de la memoria caché.

* [Claves de acceso](#access-keys)
* [Configuración avanzada](#advanced-settings)
* [Asesor de caché en Redis](#redis-cache-advisor)
* [Escala](#scale)
* [Tamaño del Clúster en Redis](#cluster-size)
* [Persistencia de datos de Redis](#redis-data-persistence)
* [Programación de actualizaciones](#schedule-updates)
* [Replicación geográfica](#geo-replication)
* [Virtual Network](#virtual-network)
* [Firewall](#firewall)
* [Propiedades](#properties)
* [Bloqueos](#locks)
* [Script de automatización](#automation-script)



### <a name="access-keys"></a>Claves de acceso
Haga clic en **las claves de acceso** acceso hello tooview o volver a generar las claves de la memoria caché. Estas teclas se utilizan los clientes de hello tooyour caché de conexión.

![Caché en Redis - Claves de acceso](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a>Configuración avanzada
Hello siguiente se configura en hello **configuración avanzada** hoja.

* [Puertos de acceso](#access-ports)
* [Directivas de memoria](#memory-policies)
* [Notificaciones de espacio de claves (configuración avanzada)](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a>Puertos de acceso
El acceso no SSL está deshabilitado de forma predeterminada para las nuevas cachés. tooenable Hola sin SSL de puerto, haga clic en **No** para **permitir el acceso sólo a través de SSL** en hello **configuración avanzada** hoja y, a continuación, haga clic en **guardar**.

![Caché en Redis - Puertos de acceso](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a>Directivas de memoria
Hola **directiva Maxmemory**, **reservado maxmemory**, y **reservado maxfragmentationmemory** configuración en hello **Configuraciónavanzada**hoja configurar directivas de memoria de Hola para caché de Hola.

![Caché en Redis - Directiva Maxmemory](./media/cache-configure/redis-cache-maxmemory-policy.png)

**Directiva MaxMemory** configura la directiva de expulsión de Hola para caché de Hola y le permite toochoose de hello las siguientes directivas de expulsión:

* `volatile-lru`-Éste es el predeterminado de Hola.
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

Para más información sobre las directivas `maxmemory`, consulte [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies) (Directivas de expulsión).

Hola **reservado maxmemory** configura cantidad Hola de memoria en MB que se reserva para las operaciones de caché no es como la replicación durante la conmutación por error. Este valor permite toohave una experiencia más coherente de servidor de Redis cuando varía la carga. Este valor debe establecerse más alto para cargas de trabajo con muchas operaciones de escritura. Cuando se reserva memoria para dichas operaciones, no está disponible para el almacenamiento de datos en caché.

Hola **maxfragmentationmemory reservadas** configura cantidad Hola de memoria en MB que está reservada tooaccommodate fragmentación de memoria. Este valor permite toohave una experiencia más coherente de servidor de Redis cuando Hola caché está llena o la proporción de fragmentación de hello y toofull cierre también es alta. Cuando se reserva memoria para dichas operaciones, no está disponible para el almacenamiento de datos en caché.

Una cuestión que hay tooconsider al elegir un nuevo valor de reserva de memoria (**reservado maxmemory** o **reservado maxfragmentationmemory**) es cómo este cambio puede afectar a una caché que ya se está ejecutando con grandes cantidades de datos en ella. Por ejemplo, si tienen una memoria caché de 53 GB con 49 GB de datos, cambiar Hola reserva valor too8 GB, Esto quitará la memoria disponible max Hola para sistema Hola hacia abajo too45 GB. Si el valor actual `used_memory` o su `used_memory_rss` valores son mayores que el nuevo límite de Hola de 45 GB, a continuación, sistema de hello tendrá datos tooevict hasta que `used_memory` y `used_memory_rss` están por debajo de 45 GB. La expulsión puede aumentar la carga del servidor y la fragmentación de memoria. Para más información sobre las métricas de caché como `used_memory` y `used_memory_rss`, vea [Métricas disponibles e intervalos de informes](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).

> [!IMPORTANT]
> Hola **reservado maxmemory** y **reservado maxfragmentationmemory** configuraciones solo están disponibles para el nivel Standard y Premium almacena en caché.
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a>Notificaciones de espacio de claves (configuración avanzada)
Redis keyspace las notificaciones están configuradas en hello **configuración avanzada** hoja. Notificaciones de Keyspace permiten a los clientes tooreceive notificaciones cuando se producen determinados eventos.

![Caché en Redis - Configuración avanzada](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> Keyspace hello y notificaciones **eventos keyspace notificar** configuración solo están disponibles para las memorias caché Standard y Premium.
> 
> 

Para obtener más información, vea [Notificaciones de espacio de claves de Redis](http://redis.io/topics/notifications). Ejemplo de código, vea hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) archivo Hola [Hola a todos](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) ejemplo.


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a>Asesor de caché en Redis
Hola **Asesor de caché de Redis** hoja muestra recomendaciones para la memoria caché. Durante las operaciones normales, no se muestra ninguna recomendación. 

![Recomendaciones](./media/cache-configure/redis-cache-no-recommendations.png)

Si las condiciones se producen durante las operaciones de saludo de la memoria caché como mayor uso de memoria, ancho de banda de red o de carga del servidor, se muestra una alerta en hello **caché en Redis** hoja.

![Recomendaciones](./media/cache-configure/redis-cache-recommendations-alert.png)

Puede encontrar información adicional en hello **recomendaciones** hoja.

![Recomendaciones](./media/cache-configure/redis-cache-recommendations.png)

Puede supervisar estas métricas en hello [gráficos de supervisión](cache-how-to-monitor.md#monitoring-charts) y [gráficos de uso](cache-how-to-monitor.md#usage-charts) secciones de hello **caché en Redis** hoja.

Cada plan de tarifa tiene distintos límites para las conexiones de cliente, memoria y ancho de banda. Si la caché se aproxima a la capacidad máxima para estas métricas durante un período prolongado, se crea una recomendación. Para obtener más información acerca de las métricas de Hola y límites revisados hello **recomendaciones** herramienta, vea hello en la tabla siguiente:

| Métrica de Caché en Redis | Más información |
| --- | --- |
| Uso de ancho de banda de red |[Rendimiento de la caché: ancho de banda disponible](cache-faq.md#cache-performance) |
| Clientes conectados |[Configuración predeterminada del servidor Redis: maxclients](#maxclients) |
| Carga de servidor |[Gráficos de uso: carga del servidor Redis](cache-how-to-monitor.md#usage-charts) |
| Uso de la memoria |[Rendimiento y tamaño de la memoria caché](cache-faq.md#cache-performance) |

tooupgrade la memoria caché, haga clic en **actualizar ahora** hello toochange nivel de precios y [escala](#scale) la memoria caché. Para más información sobre cómo elegir un plan de tarifa, consulte [¿Qué oferta y tamaño de Redis Caché debo utilizar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)


### <a name="scale"></a>Escala
Haga clic en **escala** tooview o cambiar Hola tarifa de la memoria caché. Para obtener más información sobre cómo ampliar, consulte [cómo tooScale Redis de Azure almacenan en caché](cache-how-to-scale.md).

![Nivel de precios de Caché en Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a>Tamaño del Clúster en Redis
Haga clic en **tamaño de clúster de Redis (vista previa)** toochange el tamaño del clúster de Hola para una ejecución premium de caché con clúster habilitado.

> [!NOTE]
> Tenga en cuenta que mientras hello Azure Redis caché Premium nivel ha sido liberado tooGeneral disponibilidad, la característica de tamaño de clúster Redis Hola está actualmente en vista previa.
> 
> 

![Tamaño del Clúster en Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

tamaño de clúster de toochange hello, utilice el control deslizante de Hola o escriba un número entre 1 y 10 en hello **número de particiones** cuadro de texto y haga clic en **Aceptar** toosave.

> [!IMPORTANT]
> La agrupación en clústeres de Redis solo está disponible para las memorias cachés premium. Para obtener más información, consulte [cómo tooconfigure agrupación en clústeres para una caché en Redis de Azure Premium](cache-how-to-premium-clustering.md).
> 
> 


### <a name="redis-data-persistence"></a>Persistencia de datos de Redis
Haga clic en **Redis persistencia de los datos** tooenable, deshabilitar o configurar la persistencia de datos de la memoria caché premium. Azure Redis Cache ofrece persistencia de Redis mediante [persistencia de RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) o [persistencia de AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).

Para obtener más información, consulte [cómo persistencia tooconfigure para una caché de Redis de Azure Premium](cache-how-to-premium-persistence.md).


> [!IMPORTANT]
> La persistencia de los datos en Redis solo está disponible para las memorias cachés premium. 
> 
> 

### <a name="schedule-updates"></a>Programar actualizaciones
Hola **programar actualizaciones** hoja permite toodesignate una ventana de mantenimiento para las actualizaciones de servidor de Redis para la memoria caché. 

> [!IMPORTANT]
> ventana de mantenimiento de Hola aplica solo las actualizaciones de servidor de tooRedis y tooany Azure actualiza o actualiza el sistema de operativo toohello de máquinas virtuales de Hola que hospedan la memoria caché de Hola.
> 
> 

![Programar actualizaciones](./media/cache-configure/redis-schedule-updates.png)

toospecify una ventana de mantenimiento, los días de hello deseado y especifique la hora de inicio de ventana de mantenimiento de Hola para cada día y haga clic en **Aceptar**. Tenga en cuenta que es hora de ventana de mantenimiento de hello en UTC. 

> [!IMPORTANT]
> Hola **programar actualizaciones** funcionalidad solo está disponible para las cachés de nivel Premium. Para más información e instrucciones, consulte [Administración de la Caché en Redis de Azure - Programación de actualizaciones](cache-administration.md#schedule-updates).
> 
> 

### <a name="geo-replication"></a>Replicación geográfica

Hola **georreplicación** hoja proporciona un mecanismo para vincular dos instancias de caché en Redis de Azure de nivel Premium. Una memoria caché se designa como caché primaria vinculada de Hola y Hola otro como caché secundaria vinculado de Hola. caché secundaria vinculado de Hello pasa a ser de solo lectura, y datos de caché principal toohello escrito es replican toohello secundario vinculado caché. Esta funcionalidad puede ser tooreplicate usa una memoria caché en regiones de Azure.

> [!IMPORTANT]
> La **replicación geográfica** solo está disponible para las cachés de nivel Premium. Para obtener más información e instrucciones, consulte [cómo tooconfigure replicación geográfica para caché en Redis de Azure](cache-how-to-geo-replication.md).
> 
> 

### <a name="virtual-network"></a>Virtual Network
Hola **red Virtual** sección le permite la configuración de red virtual de hello tooconfigure de la memoria caché. Para obtener información sobre cómo crear una caché premium con red virtual admiten y actualizar su configuración, consulte [cómo tooconfigure admite la red Virtual para una caché de Redis de Azure Premium](cache-how-to-premium-vnet.md).

> [!IMPORTANT]
> La configuración de red virtual solo está disponible para las memorias cachés premium que se configuraron con la compatibilidad de la red virtual durante la creación de la memoria caché. 
> 
> 

### <a name="firewall"></a>Firewall

Haga clic en **Firewall** tooview y configurar las reglas de firewall para la caché en Redis de Azure Premium.

![Firewall](./media/cache-configure/redis-firewall-rules.png)

Puede especificar las reglas de firewall con un intervalo de direcciones IP de inicio y finalización. Cuando se configuran las reglas de firewall, solo las conexiones de cliente de hello especifican intervalos de direcciones IP pueden conectar toohello caché. Cuando se guarda una regla de firewall no hay un breve retraso antes de regla de hello es efectivo. Normalmente, este retraso es inferior a un minuto.

> [!IMPORTANT]
> Siempre se permiten las conexiones de los sistemas de supervisión de Azure Redis Cache, incluso si se configuran reglas de firewall.
> 
> El reinicio solo está disponible para las memorias caché de nivel Premium.
> 
> 

### <a name="properties"></a>Propiedades
Haga clic en **propiedades** tooview información acerca de la memoria caché, incluidos los puertos y el extremo de la memoria caché de Hola.

![Caché en Redis - Propiedades](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a>Bloqueos
Hola **bloquea** sección le permite toolock una suscripción, el grupo de recursos o recursos tooprevent otros usuarios de su organización accidentalmente eliminen o modifiquen los recursos críticos. Para obtener más información, consulte [Bloqueo de recursos con el Administrador de recursos de Azure](../azure-resource-manager/resource-group-lock-resources.md).

### <a name="automation-script"></a>Script de automatización

Haga clic en **script de automatización** toobuild y exportar una plantilla de los recursos implementados para futuras implementaciones. Para más información sobre cómo trabajar con plantillas, consulte [Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="administration-settings"></a>Configuración de administración
Hola configuración Hola **administración** sección le permiten hello tooperform después de las tareas administrativas de la memoria caché. 

![Administración](./media/cache-configure/redis-cache-administration.png)

* [Importación de datos](#importexport)
* [Exportación de datos](#importexport)
* [Reboot](#reboot)


### <a name="importexport"></a>Importación/Exportación
Importación y exportación es una operación de administración de datos de caché en Redis de Azure, que le permite tooimport y exportar datos en memoria caché de hello al importar y exportar una instantánea de base de datos de caché de Redis (RDB) de un blob en páginas tooa caché premium en una cuenta de almacenamiento de Azure. Importación y exportación permite toomigrate entre distintas instancias de caché en Redis de Azure o rellenar Hola caché con los datos antes de su uso.

Importación puede ser toobring usado Redis compatible RDB archivos desde cualquier servidor de Redis que se ejecute en cualquier nube o el entorno, incluidos Redis que se ejecutan en Linux, Windows o cualquier proveedor de nube, como Amazon Web Services y otros. Importación de datos es un toocreate fácilmente una memoria caché con datos rellenadas previamente. Durante el proceso de importación de hello, caché en Redis de Azure carga archivos RDB Hola del almacenamiento de Azure en la memoria y, a continuación, inserta las claves de hello en memoria caché de Hola.

Exportación permite datos de hello tooexport almacenados en caché en Redis de Azure tooRedis compatible RDB archivos. Puede usar estos datos de toomove característica de una caché en Redis de Azure instancia tooanother o un servidor de Redis tooanother. Durante el proceso de exportación de hello, se crea un archivo temporal en hello VM que hosts Hola instancia del servidor de caché en Redis de Azure y archivo hello toohello cargado designado de la cuenta de almacenamiento. Cuando se completa la operación de exportación de hello con estado de éxito o error, se elimina el archivo temporal de Hola.

> [!IMPORTANT]
> Importación/Exportación solo está disponible para las memorias caché de nivel premium. Para más información e instrucciones, consulte [Importación y exportación de datos en la Caché en Redis de Azure](cache-how-to-import-export-data.md).
> 
> 

### <a name="reboot"></a>Reboot
Hola **reiniciar** hoja permite nodos de hello tooreboot de la memoria caché. Esta capacidad de reinicio permite que se tootest la aplicación para proporcionar resistencia si se produce un error de un nodo de caché.

![Reboot](./media/cache-configure/redis-cache-reboot.png)

Si tiene una caché premium con clúster habilitado, puede seleccionar qué particiones de hello caché tooreboot.

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

tooreboot uno o varios nodos de la memoria caché, seleccione los nodos de hello deseado y haga clic en **reiniciar**. Si tiene una caché premium con clúster habilitado, seleccione tooreboot de las particiones de hello y, a continuación, haga clic en **reiniciar**. Después de unos minutos, Hola reinicio de los nodos seleccionados y son volver a conectarse más tarde unos minutos.

> [!IMPORTANT]
> El reinicio ahora está disponible para todos los planes de tarifas. Para más información e instrucciones, consulte [Administración de Caché en Redis de Azure - Reboot](cache-administration.md#reboot).
> 
> 


## <a name="monitoring"></a>Supervisión

Hola **supervisión** sección le permite tooconfigure diagnósticos y supervisión de la memoria caché de Redis. Para obtener más información sobre la supervisión de la caché de Redis de Azure y diagnósticos, vea [cómo toomonitor Redis de Azure almacenan en caché](cache-how-to-monitor.md).

![Diagnóstico](./media/cache-configure/redis-cache-diagnostics.png)

* [Métricas de Redis](#redis-metrics)
* [Reglas de alertas](#alert-rules)
* [Diagnóstico](#diagnostics)

### <a name="redis-metrics"></a>Caché en Redis
Haga clic en **Redis métricas** demasiado[ver las métricas](cache-how-to-monitor.md#view-cache-metrics) de la memoria caché.

### <a name="alert-rules"></a>Las reglas de alertas

Haga clic en **reglas de alerta** alertas tooconfigure según las métricas de caché en Redis. Para obtener más información, consulte [Alerts](cache-how-to-monitor.md#alerts) (Alertas).

### <a name="diagnostics"></a>Diagnóstico

De manera predeterminada, en Azure Monitor las métricas de caché se [almacenan durante 30 días](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) y después se eliminan. toopersist las métricas de memoria caché durante más de 30 días, haga clic en ejecutar **diagnósticos** demasiado[Configurar cuenta de almacenamiento de hello](cache-how-to-monitor.md#export-cache-metrics) usar diagnósticos de caché toostore.

>[!NOTE]
>En suma tooarchiving su toostorage de métricas de caché, también puede [transmitirlos tooan concentrador de eventos o enviarlos tooLog análisis](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

## <a name="support--troubleshooting-settings"></a>Configuración de soporte técnico y solución de problemas
Hola configuración Hola **soporte técnico y solución de problemas** sección proporcionan opciones para resolver problemas con la memoria caché.

![Soporte y solución de problemas](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [Estado de los recursos](#resource-health)
* [Nueva solicitud de soporte técnico](#new-support-request)

### <a name="resource-health"></a>Estado de los recursos
**estado de los recursos** supervisa el recurso e indica si se ejecuta del modo previsto. Para obtener más información acerca de hello servicio de mantenimiento de recursos de Azure, consulte [información general de mantenimiento de recursos de Azure](../resource-health/resource-health-overview.md).

> [!NOTE]
> Estado del recurso es tooreport actualmente, no en estado de Hola de instancias de caché en Redis de Azure hospedados en una red virtual. Para más información, consulte [¿Funcionarán todas las características al alojar una caché en una red virtual?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)
> 
> 

### <a name="new-support-request"></a>Nueva solicitud de soporte
Haga clic en **nueva solicitud de soporte técnico** tooopen una solicitud de soporte técnico de la memoria caché.





## <a name="default-redis-server-configuration"></a>Configuración predeterminada del servidor Redis
Nuevas instancias de caché en Redis de Azure se configuran con hello después de valores de configuración de Redis predeterminados.

> [!NOTE]
> no se puede cambiar la configuración de Hello en esta sección con hello `StackExchange.Redis.IServer.ConfigSet` método. Si se llama a este método con uno de los comandos de hello en esta sección, se produce un siguiente toohello similar de excepción:  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> Los valores que se pueden configurables como **directiva de memoria máximo**, son configurables a través del portal de Azure de Hola o herramientas de administración de línea de comandos como PowerShell o CLI de Azure.
> 
> 

| Configuración | Valor predeterminado | Descripción |
| --- | --- | --- |
| `databases` |16 |número predeterminado de Hola de bases de datos es 16, pero se puede configurar un diferentes hello en función de número de tarifa. <sup>1</sup> base de datos de hello predeterminada es DB 0, puede seleccionar uno diferente según la por conexión mediante `connection.GetDatabase(dbid)` donde `dbid` es un número entre `0` y `databases - 1`. |
| `maxclients` |Depende de nivel de precios de hello<sup>2</sup> |Es Hola número máximo de clientes conectados permitido en hello mismo tiempo. Cuando se alcanza el límite de hello Redis cierra todas las conexiones nuevas de hello, devolver un error de 'número máximo de clientes alcanzada'. |
| `maxmemory-policy` |`volatile-lru` |Directiva MaxMemory es la configuración de hello para el modo en que Redis selecciona qué tooremove cuando `maxmemory` (tamaño de Hola de oferta seleccionado cuando creó la caché de hello de la caché de Hola) se alcanza. No tiene valor predeterminado de Hola de caché en Redis de Azure es configuración `volatile-lru`, lo que elimina las claves de hello con una expiración definida mediante un algoritmo LRU. Este valor se puede configurar en hello portal de Azure. Para más información, vea [Directivas de memoria](#memory-policies). |
| `maxmemory-samples` |3 |memoria de toosave, LRU y algoritmos TTL mínimo son aproximados algoritmos en lugar de algoritmos precisos. De forma predeterminada, Redis comprobaciones tres claves y recoge Hola uno que se utilizó menos recientemente. |
| `lua-time-limit` |5.000 |Tiempo máximo de ejecución de un script Lua en milisegundos. Si se alcanza el tiempo de ejecución máximo de hello, Redis registra que sigue en ejecución después de hello máxima permitida de una secuencia de comandos y tooreply tooqueries inicia con un error. |
| `lua-event-limit` |500 |Tamaño máximo de la cola de eventos de script. |
| `client-output-buffer-limit``normalclient-output-buffer-limit``pubsub` |0 0 032mb 8mb 60 |Hello límites de búfer de salida de cliente se pueden utilizar tooforce desconexión de los clientes que son no leyendo los datos del servidor de hello lo suficientemente rápido por algún motivo (un motivo habitual es que un cliente de Pub/Sub no puede consumir mensajes tan rápido como Hola Editor los crea). Para más información, vea [http://redis.io/topics/clients](http://redis.io/topics/clients). |

<a name="databases"></a>
<sup>1</sup>límite de Hola para `databases` es diferente para cada caché en Redis de Azure nivel de precios y se puede establecer al crear la memoria caché. Si no hay ningún `databases` configuración se especifica durante la creación de la memoria caché, valor predeterminado de hello es 16.

* Cachés Basic y Standard
  * C0 caché (250 MB) - seguridad too16 bases de datos
  * C1 caché (1 GB) - seguridad too16 bases de datos
  * C2 caché (2,5 GB) - seguridad too16 bases de datos
  * C3 caché (6 GB) - seguridad too16 bases de datos
  * C4 (13 GB) de memoria caché - seguridad too32 bases de datos
  * C5 caché (26 GB) - seguridad too48 bases de datos
  * C6 (53 GB) de memoria caché - seguridad too64 bases de datos
* Cachés Premium
  * P1 (6 GB - 60 GB) - seguridad too16 bases de datos
  * P2 (13 GB a 130 GB) - seguridad too32 bases de datos
  * P3 (26 GB - 260 GB) - seguridad too48 bases de datos
  * P4 (53 GB - 530 GB) - seguridad too64 bases de datos
  * Todas las memorias caché premium con clúster de Redis habilitado - Redis clúster solo admite el uso de la base de datos 0 tan Hola `databases` limitar para cualquier caché premium con clúster de Redis habilitada es efectivamente hello y 1 [seleccione](http://redis.io/commands/select) comando no se admite. Para obtener más información, vea [¿necesito toomake cualquier toouse de aplicación de cliente de cambios toomy de agrupación en clústeres?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)

Para obtener más información sobre las bases de datos, consulte el artículo [¿Cuáles son las bases de datos de Redis?](cache-faq.md#what-are-redis-databases)

> [!NOTE]
> Hola `databases` configuración se puede configurar durante la creación de cachés como solo con PowerShell, CLI u otros clientes de administración. Para ver un ejemplo de configuración de `databases` al crear la memoria caché mediante PowerShell, consulte [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).
> 
> 

<a name="maxclients"></a>
<sup>2</sup>`maxclients` es diferente en cada plan de tarifa de Azure Redis Cache.

* Cachés Basic y Standard
  * C0 caché (250 MB), las conexiones de too256
  * C1 caché (1 GB) - seguridad too1, 000 conexiones
  * C2 caché (2,5 GB) - seguridad too2, 000 conexiones
  * C3 caché (6 GB) - seguridad too5, 000 conexiones
  * C4 (13 GB) de memoria caché - seguridad too10, 000 conexiones
  * C5 caché (26 GB) - seguridad too15, 000 conexiones
  * C6 (53 GB) de memoria caché - seguridad too20, 000 conexiones
* Cachés Premium
  * P1 (6 GB - 60 GB) - seguridad too7, conexiones a 500
  * P2 (13 GB a 130 GB) - seguridad too15, 000 conexiones
  * P3 (26 GB - 260 GB) - seguridad too30, 000 conexiones
  * P4 (53 GB - 530 GB) - seguridad too40, 000 conexiones

> [!NOTE]
> Aunque cada tamaño de caché permite *hasta* un cierto número de conexiones, cada tooRedis de conexión tiene sobrecarga asociado. Un ejemplo de dicha sobrecarga podría ser el uso de memoria y CPU como resultado del cifrado TLS/SSL. límite máximo de conexiones de Hola para un tamaño de caché especificado supone una caché con poca carga. Si carga de sobrecarga de conexión *más* carga de las operaciones de cliente supera la capacidad para el sistema de Hola, caché Hola puede experimentar problemas de capacidad, incluso si no ha superado el límite de conexiones de hello para el tamaño actual de la caché de Hola.
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a>No se admiten comandos de Redis en Caché en Redis de Azure
> [!IMPORTANT]
> Porque la configuración y administración de instancias de caché de Redis de Azure está administrado por Microsoft, hello siguientes están deshabilitados. Si intentas tooinvoke usarlas, recibirá un mensaje de error similar demasiado`"(error) ERR unknown command"`.
> 
> * BGREWRITEAOF
> * BGSAVE
> * CONFIG
> * DEBUG
> * MIGRATE
> * Guardar
> * SHUTDOWN
> * SLAVEOF
> * CLÚSTER: los comandos de escritura del clúster están deshabilitados, pero se permiten los comandos de solo lectura del clúster.
> 
> 

Para más información sobre los comandos de Redis, vea [http://redis.io/commands](http://redis.io/commands).

## <a name="redis-console"></a>Consola de Redis
Forma segura puede emitir comandos tooyour instancias de caché en Redis de Azure con hello **Redis consola**, que está disponible en el portal de Azure para todos los niveles de caché de Hola.

> [!IMPORTANT]
> - Hello Redis consola no funciona con [VNET](cache-how-to-premium-vnet.md). Cuando la memoria caché forma parte de una red virtual, solo los clientes de hello red virtual pueden tener acceso a memoria caché de Hola. Dado que Redis consola se ejecuta en el explorador local, que se encuentra fuera de la red virtual de hello, no puede conectarse tooyour caché.
> - No se admiten todos los comandos de Redis en Azure Redis Cache. Para obtener una lista de comandos de Redis que se deshabilitan para caché en Redis de Azure, vea Hola anterior [Redis comandos no admitidos en caché en Redis de Azure](#redis-commands-not-supported-in-azure-redis-cache) sección. Para más información sobre los comandos de Redis, vea [http://redis.io/commands](http://redis.io/commands).
> 
> 

Hola tooaccess Redis consola, haga clic en **consola** de hello **caché en Redis** hoja.

![Consola de Redis](./media/cache-configure/redis-console-menu.png)

comandos de tooissue en una instancia de la memoria caché, simplemente Hola de tipo deseado comando en la consola de Hola.

![Consola de Redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a>Redis consola con una prima con hello en clúster caché

Al usar Hola consola Redis con un elevado en el clúster de caché, puede emitir tooa sola partición de memoria caché de Hola de comandos. tooissue una partición específica de comando tooa, primero conectarse toohello de partición deseada haciendo clic en él en el selector de la partición de Hola.

![Consola de Redis](./media/cache-configure/redis-console-premium-cluster.png)

Si intentas tooaccess una clave que se almacena en una partición diferente de Hola particiones conectado, recibirá un toohello similar de mensaje de error siguiente mensaje.

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

En el ejemplo anterior de hello, partición 1 es la partición seleccionada de hello, pero `myKey` se encuentra en la partición 0, tal como se indica por hello `(shard 0)` parte del mensaje de error de saludo. En este ejemplo, tooaccess `myKey`, seleccione usando la partición 0 Hola selector de partición y, a continuación, comando hello deseado de problema.


## <a name="move-your-cache-tooa-new-subscription"></a>Mover la nueva suscripción de caché tooa
Puede mover la nueva suscripción de caché tooa haciendo clic en **mover**.

![Traslado de Caché en Redis](./media/cache-configure/redis-cache-move.png)

Para obtener información acerca de cómo mover los recursos de tooanother de grupo de recursos y de tooanother de una suscripción, vea [Mover grupo de recursos de toonew de recursos o suscripción](../azure-resource-manager/resource-group-move-resources.md).

## <a name="next-steps"></a>Pasos siguientes
* Para más información sobre cómo trabajar con los comandos de Redis, consulte [¿Cómo puedo ejecutar comandos de Redis?](cache-faq.md#how-can-i-run-redis-commands).

