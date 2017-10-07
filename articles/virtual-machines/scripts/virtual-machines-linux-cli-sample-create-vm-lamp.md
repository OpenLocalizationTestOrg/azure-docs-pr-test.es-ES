---
title: 'Ejemplo de secuencia de comandos de CLI: aaaAzure implementar Hola pila LAMP en un conjunto de escala de Load-Balanced virtual Machin | Documentos de Microsoft'
description: "Usar un script personalizado extensión toodeploy hello pila LAMP en una carga = escala de máquina virtual con equilibrio establecida en Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>Implementar pila LAMP de hello en un conjunto de escala con equilibrio de carga de máquina virtual

Este ejemplo crea un conjunto de escalas de máquina virtual y aplica una extensión que se ejecuta una pila de luz de secuencia de comandos personalizada toodeploy hello en cada máquina virtual en el conjunto de escalas de Hola.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>Conectar

Utilice este toosee código cómo establecen tooconnect tooyour máquinas virtuales y la escala.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Ejecute hello después el grupo de recursos de comando tooremove hello, conjunto de escalas de Hola y las máquinas virtuales y todos ellos relacionados con recursos.

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toocreate un grupo de recursos, máquina virtual, conjunto de disponibilidad, equilibrador de carga y todos los recursos relacionados. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az vmss create](https://docs.microsoft.com/cli/azure/vmss#create) | Crea un conjunto de escalado de máquinas virtuales. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Agrega un punto de conexión de carga equilibrada. |
| [az vmss extension set](https://docs.microsoft.com/cli/azure/vmss/extension#set) | Crear la extensión de Hola que se ejecuta un script personalizado hello en la implementación de una máquina virtual |
| [az vmss update-instances](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Ejecutar script personalizado de hello en instancias de máquina virtual de Hola que se implementaron antes de que se aplicó la extensión de hello toohello conjunto de escala. |
| [az vmss scale](https://docs.microsoft.com/cli/azure/vmss#scale) | Escalar verticalmente la escala de hello establecida mediante la adición de más instancias de máquina virtual. secuencia de comandos personalizada Hello se ejecuta en estas cuando se implementan. |
| [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Obtener direcciones IP de Hola de hello VM creadas en el ejemplo de Hola. |
| [az network lb show](https://docs.microsoft.com/cli/azure/network/lb#show) | Obtener back-end y front-end de hello puertos utilizados por el equilibrador de carga de Hola. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
