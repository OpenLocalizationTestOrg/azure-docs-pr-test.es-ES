---
title: "ejemplo de secuencia de comandos CLI aaaAzure - tráfico de red de VM de filtro | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: filtrar el tráfico de red de VM entrante y saliente."
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
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a>Filtrar el tráfico de red de VM entrante y saliente

Este ejemplo de script crea una red virtual con subredes de front-end y back-end. El tráfico de red entrante toohello la subred front-end es tooHTTP limitado, toohello Internet desde la subred de back-end de hello no se permite el tráfico de HTTPS y SSH, mientras saliente. Después de ejecutar el script de Hola, tendrá una máquina virtual con dos NIC. Cada NIC está conectado tooa otra subred.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

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
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) | Asocia los NSG toosubnets. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Crea un Hola de tooaccess VM pública para la dirección IP de hello Internet. |
| [az network nic create](/cli/azure/network/nic#create) | Crea las interfaces de red virtual y los asocia subredes de la red virtual toohello front-end y back-end. |
| [az network nsg create](/cli/azure/network/nsg#create) | Crea grupos de seguridad de red (NSG) que son subredes de front-end y back-end de toohello asociado. |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) |Crea reglas NSG que permiten o bloquear subredes toospecific de puertos específicos. |
| [az vm create](/cli/azure/vm#create) | Crea las máquinas virtuales y adjunta un tooeach NIC virtual. Este comando también especifica toouse de imagen de máquina virtual de Hola y credenciales administrativas. |
| [az group delete](/cli/azure/group#delete) | Elimina un grupo de recursos y todos los recursos que contiene. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos CLI red Hola [documentación de introducción a las redes Azure](../cli-samples.md)
