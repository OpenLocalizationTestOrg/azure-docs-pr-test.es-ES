---
title: 'secuencia de comandos CLI aaaAzure de ejemplo: crear una red para aplicaciones de varios niveles | Documentos de Microsoft'
description: "Ejemplo de script de CLI de Azure: crear una red virtual para aplicaciones de niveles múltiples."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a>Creación de una red para aplicaciones de niveles múltiples

Este ejemplo de script crea una red virtual con subredes de front-end y back-end. Subred de tráfico toohello front-end es tooHTTP limitado y SSH, al tráfico toohello subred back-end es tooMySQL limitado, puerto 3306. Después de ejecutar script de Hola, tendrá dos máquinas virtuales, uno en cada subred que se pueden implementar el servidor web y el software MySQL.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Script de ejemplo


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toocreate un grupo de recursos, redes virtuales y grupos de seguridad de red. Cada comando de la tabla de hello vincula documentación específica del toocommand.

| Comando | Notas |
|---|---|
| [az group create](/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az network vnet create](/cli/azure/network/vnet#create) | Crea una subred de front-end y una red virtual de Azure. |
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | Crea una subred de back-end. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Crea un Hola de tooaccess VM pública para la dirección IP de hello Internet. |
| [az network nic create](/cli/azure/network/nic#create) | Crea las interfaces de red virtual y los asocia subredes de la red virtual toohello front-end y back-end. |
| [az network nsg create](/cli/azure/network/nsg#create) | Crea grupos de seguridad de red (NSG) que son subredes de front-end y back-end de toohello asociado. |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) |Crea reglas NSG que permiten o bloquear subredes toospecific de puertos específicos. |
| [az vm create](/cli/azure/vm#create) | Crea las máquinas virtuales y adjunta un tooeach NIC virtual. Este comando también especifica toouse de imagen de máquina virtual de Hola y credenciales administrativas. |
| [az group delete](/cli/azure/group#delete) | Elimina un grupo de recursos y todos los recursos que contiene. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos CLI red Hola [documentación de introducción a las redes Azure](../cli-samples.md)
