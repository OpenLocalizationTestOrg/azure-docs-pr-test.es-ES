---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure equilibra la carga de varios sitios Web con hello CLI de Azure | Documentos de Microsoft
description: "Ejemplo de secuencia de comandos CLI Azure - toohello de varios sitios Web se equilibra la carga misma máquina virtual"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Equilibrio de carga entre varios sitios web

Este ejemplo de script crea una red virtual con dos máquinas virtuales que son miembros de un conjunto de disponibilidad. Un equilibrador de carga dirige el tráfico de dos direcciones IP toohello dos las máquinas virtuales. Después de ejecutar script de Hola, podría implementar toohello de software de servidor web las máquinas virtuales y hospedar varios sitios web, cada uno con su propia dirección IP.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siga los comandos del toocreate un grupo de recursos de red virtual, equilibrador de carga y todos ellos relacionados con recursos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Crea una red virtual y una subred de Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Crea una dirección IP pública con una dirección IP estática y un nombre DNS asociado. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Crea una instancia de Azure Load Balancer. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Crea un sondeo de equilibrador de carga. Un sondeo del equilibrador de carga es toomonitor usado en cada máquina virtual en el conjunto de equilibrador de carga de Hola. Si ninguna máquina virtual deja de estar accesible, el tráfico no es toohello enrutado máquina virtual. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Crea una regla de equilibrador de carga. En este ejemplo, se crea una regla para el puerto 80. Como el tráfico HTTP llega al equilibrador de carga de hello, es tooport enrutado 80 una de las máquinas virtuales de hello en el conjunto de equilibrador de carga de Hola. |
| [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | Crear una dirección IP de front-end para hello equilibrador de carga. |
| [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | Crea un grupo de direcciones de back-end. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Crea una tarjeta de red virtual y lo adjunta toohello de red virtual y subred. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Crea un conjunto de disponibilidad. Conjuntos de disponibilidad de garantizan la disponibilidad de las aplicaciones repartir hello las máquinas virtuales entre recursos físicos de forma que si se produce el error, no se realiza el conjunto completo de Hola. |
| [az network nic ip-config create](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | Crea una configuración IP. Debe tener la característica de hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic habilitado para esta suscripción. Una sola configuración puede designarse como configuración IP primaria de Hola por NIC, con hello: marca de convertir en principal. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG. Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos CLI red Hola [documentación de introducción a las redes Azure](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
