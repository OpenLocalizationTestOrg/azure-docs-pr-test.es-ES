---
title: "Ejemplo de secuencia de comandos de CLI - tooVMs de tráfico de equilibrio de carga para lograr alta disponibilidad aaaAzure | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos CLI Azure - tooVMs de tráfico de equilibrio de carga para lograr alta disponibilidad"
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
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Cargar tooVMs de tráfico de equilibrio de alta disponibilidad

Este ejemplo de secuencia de comandos crea todo lo necesario toorun varias máquinas virtuales de Ubuntu configurado en una alta disponibilidad y de carga equilibrada de configuración. Después de ejecutar script de Hola, tendrá tres máquinas virtuales, tooan Unidos a un conjunto de disponibilidad de Azure y es accesible a través de un equilibrador de carga de Azure. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toocreate un grupo de recursos, máquina virtual, conjunto de disponibilidad, equilibrador de carga y todos los recursos relacionados. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Crea una red virtual y una subred de Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Crea una dirección IP pública con una dirección IP estática y un nombre DNS asociado. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Crea una instancia de Azure Load Balancer. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Crea un sondeo de equilibrador de carga. Un sondeo del equilibrador de carga es toomonitor usado en cada máquina virtual en el conjunto de equilibrador de carga de Hola. Si ninguna máquina virtual deja de estar accesible, el tráfico no es toohello enrutado máquina virtual. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Crea una regla de equilibrador de carga. En este ejemplo, se crea una regla para el puerto 80. Como el tráfico HTTP llega al equilibrador de carga de hello, es tooport enrutado 80 una de las máquinas virtuales de hello en el conjunto de carga Equilibrada de Hola. |
| [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Crea una regla de traducción de direcciones de red (NAT) de Load Balancer.  Las reglas NAT asignan un puerto de puerto de tooa de equilibrador de carga de hello en una máquina virtual. En este ejemplo, se crea una regla NAT para SSH tráfico tooeach VM en el conjunto de equilibrador de carga de Hola.  |
| [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#create) | Crea un grupo de seguridad de red (NSG), que es un límite de seguridad entre Hola internet y hello las máquinas virtuales. |
| [az network nsg rule create](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Crea un tooallow de regla NSG el tráfico entrante. En este ejemplo, el puerto 22 está abierto al tráfico SSH. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Crea una tarjeta de red virtual y lo adjunta toohello de red virtual, subred y NSG. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Crea un conjunto de disponibilidad. Conjuntos de disponibilidad de garantizan la disponibilidad de las aplicaciones repartir hello las máquinas virtuales entre recursos físicos de forma que si se produce el error, no se realiza el conjunto completo de Hola. |
| [az vm create](/cli/azure/vm#create) | Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG. Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos de CLI de redes de Azure en hello [red Azure documentación](../cli-samples.md).
