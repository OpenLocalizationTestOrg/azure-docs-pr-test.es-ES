---
title: "Caché en Redis de Azure mediante Azure CLI aaaManage | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall Hola CLI de Azure en cualquier plataforma, cómo toouse se tooconnect tooyour cuenta de Azure y cómo toocreate y administrar una caché en Redis de hello CLI de Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a>¿Cómo toocreate y administrar caché en Redis de Azure con hello Azure interfaz de línea de comandos (CLI de Azure)
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [CLI de Azure](cache-manage-cli.md)
>
>

Hola CLI de Azure es una excelente manera toomanage su infraestructura de Azure desde cualquier plataforma. Este artículo muestra cómo toocreate y administrar las instancias de caché en Redis de Azure con hello CLI de Azure.

> [!NOTE]
> En este artículo se aplica la versión anterior de tooa de CLI de Azure. Para los scripts de ejemplo de CLI de Azure 2.0 más recientes hello, consulte [ejemplos de caché Redis de Azure CLI](cli-samples.md).
> 
> 

## <a name="prerequisites"></a>Requisitos previos
toocreate y administrar instancias de caché en Redis de Azure mediante Azure CLI, debe completar pasos de Hola.

* Debe tener una cuenta de Azure. En caso de no tener ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/) en tan solo unos momentos.
* [Instalar hello Azure CLI](../cli-install-nodejs.md).
* Conectarse a la instalación de CLI de Azure con una cuenta personal de Azure, o con un trabajo o escuela cuenta de Azure e inicie sesión de hello CLI de Azure con hello `azure login` comando. toounderstand Hola diferencias y elegir, consulte [conectarse tooan suscripción de Azure desde hello Azure interfaz de línea de comandos (CLI de Azure)](../xplat-cli-connect.md).
* Antes de ejecutar cualquiera de hello después de comandos, cambie hello Azure CLI en modo de administrador de recursos mediante la ejecución de hello `azure config mode arm` comando. Para obtener más información, consulte [usar hello Azure CLI toomanage Azure y grupos de recursos](../xplat-cli-azure-resource-manager.md).

## <a name="redis-cache-properties"></a>Propiedades de caché en Redis
Hello siguientes propiedades se utilizan al crear y actualizar instancias de caché en Redis.

| Propiedad | Switch | Description |
| --- | --- | --- |
| name |-n,--name |Nombre del programa Hola a caché en Redis. |
| resource group |-g, --resource-group |Nombre del grupo de recursos de Hola. |
| location |-l, --location |Memoria caché de ubicación toocreate. |
| size |-z, --size |Tamaño de caché en Redis Hola. Valores válidos: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
| sku |-x, --sku |SKU de Redis. Debe ser uno de estos valores: [Basic, Standard, Premium] |
| EnableNonSslPort |-e, --enable-non-ssl-port |Propiedad EnableNonSslPort de hello caché en Redis. Agregar esta marca si desea tooenable hello no SSL puerto de la memoria caché |
| Configuración de Redis |-c, --redis-configuration |Configuración de Redis. Escriba una cadena con formato JSON de valores y claves de configuración aquí. Formato:"{"":"","":""}" |
| Configuración de Redis |-f, --redis-configuration-file |Configuración de Redis. Escriba la ruta de acceso de Hola de un archivo que contiene las claves de configuración y los valores aquí. Formato de entrada del archivo de hello: {"": "","": ""} |
| Número de particiones |-r, --shard-count |Número de particiones toocreate en una caché de clúster Premium con agrupación en clústeres. |
| Virtual Network |-v, --virtual-network |Cuando se hospeda la memoria caché en una red virtual, especifica Hola exacta ARM Id. de recurso de Hola Hola de toodeploy de red virtual redis caché en. Formato de ejemplo: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| key type |-t, --key-type |Tipo de clave toorenew. Valores válidos: [Primary, Secondary] |
| StaticIP |-p, --static-ip <static-ip> |Al hospedar la memoria caché en una red virtual, especifica una dirección IP única en la subred de Hola para caché de Hola. Si no se proporciona, se elige una automáticamente de la subred de Hola. |
| Subred |t, --subnet <subnet> |Al hospedar la memoria caché en una red virtual, especifica el nombre de Hola de subred de hello en la caché de hello toodeploy. |
| VirtualNetwork |-v, --virtual-network <virtual-network> |Cuando se hospeda la memoria caché en una red virtual, especifica Hola exacta ARM Id. de recurso de Hola Hola de toodeploy de red virtual redis caché en. Formato de ejemplo: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| Subscription |-s, --subscription |identificador de la suscripción de Hola. |

## <a name="see-all-redis-cache-commands"></a>Consulta de todos los comandos de caché en Redis
toosee todos los comandos de caché en Redis y sus parámetros, usar hello `azure rediscache -h` comando.

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a>Creación de una caché en Redis
toocreate una caché en Redis, utilice Hola siguiente comando:

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

Para obtener más información sobre este comando, ejecute hello `azure rediscache create -h` comando.

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a>Eliminación de una caché en Redis existente
toodelete una caché en Redis, utilice Hola siguiente comando:

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

Para obtener más información sobre este comando, ejecute hello `azure rediscache delete -h` comando.

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a>Lista de todas las memorias Redis Cache dentro de su suscripción o del grupo de recursos
toolist todas las cachés de Redis dentro de la suscripción o el grupo de recursos, utilice Hola comando siguiente:

    azure rediscache list [options]

Para obtener más información sobre este comando, ejecute hello `azure rediscache list -h` comando.

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a>Presentación de las propiedades de una caché en Redis existente
propiedades de tooshow de una caché de Redis existente, use Hola siguiente comando:

    azure rediscache show [--name <name> --resource-group <resource-group>]

Para obtener más información sobre este comando, ejecute hello `azure rediscache show -h` comando.

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a>Cambio de la configuración de una caché en Redis existente
configuración de toochange de una caché de Redis existente, use Hola siguiente comando:

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

Para obtener más información sobre este comando, ejecute hello `azure rediscache set -h` comando.

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a>Renovar la clave de autenticación de Hola para una caché en Redis existente
clave de autenticación de hello toorenew para una caché existente de Redis, Hola de uso siguiente comando:

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

Especifique `Primary` o `Secondary` para `key-type`.

Para obtener más información sobre este comando, ejecute hello `azure rediscache renew-key -h` comando.

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a>Lista de las claves principal y secundaria de una caché en Redis existente
claves principales y secundarios de toolist de una caché de Redis existente, use Hola siguiente comando:

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

Para obtener más información sobre este comando, ejecute hello `azure rediscache list-keys -h` comando.

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
