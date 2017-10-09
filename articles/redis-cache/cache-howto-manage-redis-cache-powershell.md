---
title: "aaaManage caché en Redis de Azure con PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooperform las tareas administrativas para caché en Redis de Azure con Azure PowerShell."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a>Administración de Caché en Redis de Azure con Azure PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [CLI de Azure](cache-manage-cli.md)
> 
> 

Este tema muestra cómo tooperform comunes tareas como crear, actualizar y ampliar las instancias de caché en Redis de Azure, cómo tooregenerate teclas de acceso y cómo tooview información acerca de sus cachés. Para obtener una lista completa de cmdlets de PowerShell de caché en Redis de Azure, consulte [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

Para obtener más información sobre el modelo de implementación clásica de hello, consulte [Azure Resource Manager frente a la implementación clásica: comprender los modelos de implementación y Hola estado de los recursos](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).

## <a name="prerequisites"></a>Requisitos previos
Si ya ha instalado Azure PowerShell, debe tener la versión 1.0.0 (o posterior) de Azure PowerShell. Puede comprobar la versión de Hola de PowerShell de Azure que ha instalado con este comando en el símbolo del sistema de PowerShell de Azure de Hola.

    Get-Module azure | format-table version


En primer lugar, debe iniciar sesión en tooAzure con este comando.

    Login-AzureRmAccount

Especifique la dirección de correo electrónico de Hola de su cuenta de Azure y su contraseña en el cuadro de diálogo de hello en el inicio de sesión de Microsoft Azure.

A continuación, si tiene varias suscripciones de Azure, deberá tooset su suscripción de Azure. toosee una lista de las suscripciones actuales, ejecute este comando.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

suscripción de hello toospecify, ejecute el siguiente comando de Hola. En el siguiente ejemplo de Hola, es el nombre de la suscripción de hello `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

Para poder usar Windows PowerShell con el Administrador de recursos de Azure, necesita Hola siguiente:

* Windows PowerShell, versión 3.0 o 4.0. versión de hello toofind de Windows PowerShell, escriba:`$PSVersionTable` y comprobar el valor de Hola de `PSVersion` es 3.0 o 4.0. tooinstall una versión compatible, consulte [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) o [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

tooget ayuda detallada de cualquier cmdlet que se ven en este tutorial, use el cmdlet Get-Help de Hola.

    Get-Help <cmdlet-name> -Detailed

Por ejemplo, tooget ayuda para hello `New-AzureRmRedisCache` cmdlet, escriba:

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a>Cómo tooconnect tooother nubes
Hola predeterminado Azure entorno es `AzureCloud`, que representa Hola instancia global de nube de Azure. tooconnect tooa otra instancia, utilice hello `Add-AzureRmAccount` comando con hello `-Environment` o -`EnvironmentName` modificador de línea de comandos con el entorno deseado de Hola o nombre del entorno.

lista de hello toosee de entornos disponibles, ejecute hello `Get-AzureRmEnvironment` cmdlet.

### <a name="tooconnect-toohello-azure-government-cloud"></a>tooconnect toohello nube de la administración pública de Azure
tooconnect toohello nube de la administración pública de Azure, use uno de hello siga los comandos.

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

o

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

toocreate una memoria caché en hello Azure gobierno en la nube, use uno de hello ubicaciones siguientes.

* USGov Virginia
* USGov Iowa

Para obtener más información acerca de hello Azure gobierno en la nube, consulte [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) y [guía para desarrolladores de Microsoft Azure Government](../azure-government-developer-guide.md).

### <a name="tooconnect-toohello-azure-china-cloud"></a>tooconnect toohello Azure China en la nube
tooconnect toohello Azure China en la nube, use uno de hello siga los comandos.

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

o

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

toocreate una memoria caché en hello Azure China en la nube, use uno de hello ubicaciones siguientes.

* Este de China
* Norte de China

Para obtener más información acerca de la nube de Azure China hello, consulte [AzureChinaCloud de Azure operado por 21Vianet en China](http://www.windowsazure.cn/).

### <a name="tooconnect-toomicrosoft-azure-germany"></a>tooconnect tooMicrosoft Alemania de Azure
tooconnect tooMicrosoft Alemania de Azure, use uno de hello siga los comandos.

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


o

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

toocreate una memoria caché en Microsoft Azure en Alemania, utilice uno de hello ubicaciones siguientes.

* Centro de Alemania
* Noreste de Alemania

Para obtener más información acerca de Microsoft Azure Alemania, consulte [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).

### <a name="properties-used-for-azure-redis-cache-powershell"></a>Propiedades utilizadas para Caché en Redis de Azure con PowerShell
Hello en la tabla siguiente contiene las propiedades y las descripciones de parámetros utilizados con frecuencia al crear y administrar las instancias de caché en Redis de Azure con Azure PowerShell.

| Parámetro | Description | Valor predeterminado |
| --- | --- | --- |
| Nombre |Nombre de caché de Hola | |
| Ubicación |Ubicación de caché de Hola | |
| ResourceGroupName |Nombre de grupo de recursos en la caché de hello toocreate | |
| Tamaño |tamaño de Hola de caché de Hola. Los valores válidos son: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 MB, 1 GB, 2,5 GB, 6 GB, 13 GB, 26 GB, 53 GB |1 GB |
| ShardCount |número de Hola de particiones toocreate al crear una caché premium con clúster habilitado. Los valores válidos son: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 | |
| SKU |Especifica la SKU de la memoria caché de Hola Hola. Los valores válidos son: Básico, Estándar y Premium |Estándar |
| RedisConfiguration |Especifica la configuración de Redis. Para obtener más información acerca de cada opción, vea el siguiente hello [RedisConfiguration propiedades](#redisconfiguration-properties) tabla. | |
| EnableNonSslPort |Indica si está habilitado el puerto no SSL de Hola. |False |
| MaxMemoryPolicy |Este parámetro está en desuso; utilice RedisConfiguration en su lugar. | |
| StaticIP |Al hospedar la memoria caché en una red virtual, especifica una dirección IP única en la subred de Hola para caché de Hola. Si no se proporciona, se elige una automáticamente de la subred de Hola. | |
| Subred |Al hospedar la memoria caché en una red virtual, especifica el nombre de Hola de subred de hello en la caché de hello toodeploy. | |
| VirtualNetwork |Cuando se hospeda la memoria caché en una red virtual, especifica el identificador de recurso de Hola de Hola red virtual en la caché de hello toodeploy. | |
| KeyType |Especifica qué tecla de acceso tooregenerate cuando se renueva las claves de acceso. Los valores válidos son: primario, secundario | |

### <a name="redisconfiguration-properties"></a>Propiedades de RedisConfiguration
| Propiedad | Description | Planes de tarifa |
| --- | --- | --- |
| rdb-backup-enabled |Si [Persistencia de los datos en Redis](cache-how-to-premium-persistence.md) está habilitado |Solo Premium |
| rdb-storage-connection-string |Hola cuenta de almacenamiento de toohello de cadena de conexión para [Redis persistencia de datos](cache-how-to-premium-persistence.md) |Solo Premium |
| rdb-backup-frequency |Hola frecuencia de copia de seguridad para [Redis persistencia de datos](cache-how-to-premium-persistence.md) |Solo Premium |
| maxmemory-reserved |Configura hello [memoria reservada](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para procesos sin caché |Estándar y Premium |
| maxmemory-policy |Configura hello [directiva de expulsión](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para caché de Hola |Todos los planes de tarifa |
| notify-keyspace-events |Configura las [notificaciones de Keyspace](cache-configure.md#keyspace-notifications-advanced-settings) |Estándar y Premium |
| hash-max-ziplist-entries |Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños |Estándar y Premium |
| hash-max-ziplist-value |Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños |Estándar y Premium |
| set-max-intset-entries |Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños |Estándar y Premium |
| zset-max-ziplist-entries |Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños |Estándar y Premium |
| zset-max-ziplist-value |Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños |Estándar y Premium |
| bases de datos |Configura el número de Hola de bases de datos. Esta propiedad solo se puede configurar al crear la memoria caché. |Estándar y Premium |

## <a name="toocreate-a-redis-cache"></a>toocreate una caché en Redis
Se crean nuevas instancias de caché en Redis de Azure con hello [AzureRmRedisCache New](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.

> [!IMPORTANT]
> Hello primera vez que cree una caché de Redis en una suscripción mediante el portal de Azure, Hola portal Hola registra hello `Microsoft.Cache` espacio de nombres para esa suscripción. Si intenta toocreate Hola primero la caché en una suscripción mediante PowerShell en Redis, primero debe registrar ese espacio de nombres mediante el siguiente comando; de Hola en caso contrario cmdlets como `New-AzureRmRedisCache` y `Get-AzureRmRedisCache` producirá un error.
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

toosee una lista de parámetros disponibles y sus descripciones para `New-AzureRmRedisCache`, ejecute hello después del comando.

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

toocreate una memoria caché con los parámetros predeterminados, ejecute el siguiente comando de Hola.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

`ResourceGroupName`, `Name`, y `Location` son parámetros necesarios, pero el resto de hello son opcional y tienen valores predeterminados. Ejecuta el comando anterior Hola crea una instancia de caché de Redis de Azure de SKU estándar con el nombre especificado de hello, la ubicación y el grupo de recursos, que es de 1 GB de tamaño con el puerto no SSL de hello deshabilitado.

toocreate una caché premium, especifique un tamaño de P1 (6 GB - 60 GB), P2 (13 GB a 130 GB), P3 (26 GB - 260 GB), o P4 (53 GB - 530 GB). tooenable agrupación en clústeres, especifique un número de particiones con hello `ShardCount` parámetro. Hello en el ejemplo siguiente se crea una memoria caché premium de P1 con 3 particiones. Una memoria caché premium de P1 es 6 GB de tamaño y, puesto que se especifican tres particiones Hola tamaño total es 18 GB (3 x 6 GB).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

valores toospecify para hello `RedisConfiguration` parámetro, incluya valores de hello `{}` como clave y valor como pares `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`. Hello en el ejemplo siguiente se crea una caché de 1 GB estándar con `allkeys-random` notificaciones de keyspace y directivas de maxmemory configuradas con `KEA`. Para más información, consulte [Notificaciones de Keyspace (configuración avanzada)](cache-configure.md#keyspace-notifications-advanced-settings) y [Directivas de memoria](cache-configure.md#memory-policies).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a>bases de datos de tooconfigure Hola establecer durante la creación de cachés
Hola `databases` se puede configurar solo durante la creación de la memoria caché. Hello en el ejemplo siguiente se crea un P3 premium (26 GB) de memoria caché con 48 bases de datos mediante hello [AzureRmRedisCache New](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

Para obtener más información sobre hello `databases` propiedad, vea [configuración del servidor de caché en Redis de Azure predeterminado](cache-configure.md#default-redis-server-configuration). Para obtener más información acerca de cómo crear una memoria caché mediante hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, vea Hola anterior [toocreate una caché en Redis](#to-create-a-redis-cache) sección.

## <a name="tooupdate-a-redis-cache"></a>tooupdate una caché de Redis
Instancias de caché en Redis de Azure se actualizan utilizando hello [AzureRmRedisCache conjunto](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.

toosee una lista de parámetros disponibles y sus descripciones para `Set-AzureRmRedisCache`, ejecute hello después del comando.

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Hola `Set-AzureRmRedisCache` cmdlet puede ser propiedades tooupdate usado como `Size`, `Sku`, `EnableNonSslPort`, hello y `RedisConfiguration` valores. 

Hello siguiente comando actualizaciones Hola directiva maxmemory para hello caché en Redis denominado myCache.

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a>tooscale una caché de Redis
`Set-AzureRmRedisCache`puede ser tooscale usa una instancia de caché Redis de Azure cuando hello `Size`, `Sku`, o `ShardCount` propiedades se modifican. 

> [!NOTE]
> Escalar una memoria caché con PowerShell es asunto toohello mismos límites y directrices como escalar una memoria caché de Hola portal de Azure. Puede escalar tooa otro nivel de precios con hello siguiendo las restricciones.
> 
> * No se puede escalar de un plan de tarifa mayor nivel tooa menor nivel de precios.
> * No se puede escalar de un **Premium** caché hacia abajo tooa **estándar** o un **básica** memoria caché.
> * No se puede escalar de un **estándar** caché hacia abajo tooa **básica** memoria caché.
> * Puede escalar de un **básica** almacenar en caché tooa **estándar** caché pero no se puede cambiar el tamaño de hello en hello mismo tiempo. Si tiene un tamaño diferente, puede hacer un tamaño de toohello deseado de operación de escalado posteriores.
> * No se puede escalar de un **básica** almacenar en caché directamente tooa **Premium** memoria caché. Debe escalar **básica** demasiado**estándar** en una sola operación de escala y, a continuación, desde **estándar** demasiado**Premium** en una escala posteriores operación.
> * No se puede escalar de un tamaño mayor profundidad toohello **C0 (250 MB)** tamaño.
> 
> Para obtener más información, consulte [cómo tooScale Redis de Azure almacenan en caché](cache-how-to-scale.md).
> 
> 

Hello en el ejemplo siguiente se muestra cómo tooscale una memoria caché denominado `myCache` 2,5 GB de memoria caché de tooa. Tenga en cuenta que este comando funciona con una memoria caché básica o una estándar.

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Después de emite este comando, se devuelve el estado de Hola de caché de hello (toocalling similar `Get-AzureRmRedisCache`). Tenga en cuenta que hello `ProvisioningState` es `Scaling`.

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

Una vez completada la operación de escalado de hello, Hola `ProvisioningState` cambia demasiado`Succeeded`. Si necesita toomake una operación de escalado subsiguientes, como cambiar de tooStandard básico y, a continuación, cambiar tamaño de hello, debe esperar a que se ha completado la operación anterior de Hola o recibir un siguiente toohello de error similar.

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a>tooget información acerca de una caché de Redis
Puede recuperar información sobre una memoria caché mediante hello [AzureRmRedisCache Get](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.

toosee una lista de parámetros disponibles y sus descripciones para `Get-AzureRmRedisCache`, ejecute hello después del comando.

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

ejecutar tooreturn información acerca de todas las memorias caché en la suscripción actual de hello, `Get-AzureRmRedisCache` sin ningún parámetro.

    Get-AzureRmRedisCache

tooreturn información acerca de todas las memorias caché en un grupo de recursos específico, ejecute `Get-AzureRmRedisCache` con hello `ResourceGroupName` parámetro.

    Get-AzureRmRedisCache -ResourceGroupName myGroup

tooreturn información acerca de una memoria caché específica, ejecute `Get-AzureRmRedisCache` con hello `Name` parámetro que contiene el nombre de Hola de caché de Hola y Hola `ResourceGroupName` parámetro con el grupo de recursos de Hola que contiene esa memoria caché.

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a>teclas de acceso de hello tooretrieve para una caché de Redis
tooretrieve hello las teclas de acceso de la memoria caché, puede usar hello [AzureRmRedisCacheKey Get](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.

toosee una lista de parámetros disponibles y sus descripciones para `Get-AzureRmRedisCacheKey`, ejecute hello después del comando.

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Hola tooretrieve claves de la memoria caché, llamada hello `Get-AzureRmRedisCacheKey` nombre hello del grupo de recursos que contiene la caché de Hola Hola a cmdlet y pase nombre hello de la memoria caché.

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a>teclas de acceso de tooregenerate para su caché de Redis
tooregenerate hello las teclas de acceso de la memoria caché, puede usar hello [AzureRmRedisCacheKey New](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.

toosee una lista de parámetros disponibles y sus descripciones para `New-AzureRmRedisCacheKey`, ejecute hello después del comando.

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

clave primario o secundario de Hola de tooregenerate para la memoria caché, llamada hello `New-AzureRmRedisCacheKey` cmdlet y pase Hola nombre, grupo de recursos y especifique `Primary` o `Secondary` para hello `KeyType` parámetro. En el siguiente ejemplo de Hola, se vuelve a generar clave de acceso secundaria de Hola para una caché.

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a>toodelete una caché de Redis
toodelete una caché en Redis, usar hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.

toosee una lista de parámetros disponibles y sus descripciones para `Remove-AzureRmRedisCache`, ejecute hello después del comando.

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

En el siguiente ejemplo de Hola Hola caché denominado `myCache` se quita.

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a>tooimport una caché de Redis
Puede importar datos en una instancia de caché en Redis de Azure mediante hello `Import-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> Importación/Exportación solo está disponible para las memorias caché de [nivel premium](cache-premium-tier-intro.md) . Para más información e instrucciones sobre Importación/Exportación, consulte [Importación y exportación de datos en la Caché en Redis de Azure](cache-how-to-import-export-data.md).
> 
> 

toosee una lista de parámetros disponibles y sus descripciones para `Import-AzureRmRedisCache`, ejecute hello después del comando.

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello siguiente comando importa datos de blob de hello especificado por el identificador uri SAS de hello en caché en Redis de Azure.

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a>tooexport una caché de Redis
Puede exportar datos desde una instancia de caché en Redis de Azure mediante hello `Export-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> Importación/Exportación solo está disponible para las memorias caché de [nivel premium](cache-premium-tier-intro.md) . Para más información e instrucciones sobre Importación/Exportación, consulte [Importación y exportación de datos en la Caché en Redis de Azure](cache-how-to-import-export-data.md).
> 
> 

toosee una lista de parámetros disponibles y sus descripciones para `Export-AzureRmRedisCache`, ejecute hello después del comando.

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello siguiente comando exporta los datos de una instancia de caché en Redis de Azure en contenedor Hola especificado por el uri de SAS de Hola.

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a>tooreboot una caché de Redis
Puede reiniciar la instancia de caché en Redis de Azure con hello `Reset-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> El reinicio solo está disponible para las memorias caché de [nivel premium](cache-premium-tier-intro.md) . Para más información acerca de cómo reiniciar la caché, consulte [Administración de caché: reinicio](cache-administration.md#reboot).
> 
> 

toosee una lista de parámetros disponibles y sus descripciones para `Reset-AzureRmRedisCache`, ejecute hello después del comando.

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello siguiente comando reinicia ambos nodos de hello especificado caché.

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a>Pasos siguientes
toolearn más sobre el uso de Windows PowerShell con Azure, vea Hola recursos siguientes:

* [Documentación de cmdlet de caché en Redis de Azure en MSDN](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* [Cmdlets de Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkID=394765): obtener información sobre toouse Hola cmdlets en el módulo de Azure Resource Manager Hola.
* [Uso del recurso agrupa toomanage los recursos de Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): Obtenga información acerca de cómo toocreate y administrar grupos de recursos de hello portal de Azure.
* [Blog de Azure](http://blogs.msdn.com/windowsazure): obtenga información acerca de las nuevas características de Azure.
* [Blog de Windows PowerShell](http://blogs.msdn.com/powershell): obtenga información acerca de las nuevas características de Windows PowerShell.
* [Blog Blog](http://blogs.technet.com/b/heyscriptingguy/): obtener reales sugerencias y trucos de hello Comunidad de Windows PowerShell.

