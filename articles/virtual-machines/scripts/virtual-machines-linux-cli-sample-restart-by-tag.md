---
title: "aaaAzure ejemplo de secuencia de comandos de CLI - reiniciar máquinas virtuales | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: reinicio de máquinas virtuales por etiqueta e identificador"
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
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a>Reinicio de máquinas virtuales

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

Este ejemplo muestra un par de maneras tooget algunas máquinas virtuales y reiniciarlas una vez.

Hola reinicia primero todas las máquinas virtuales de hello en el grupo de recursos de Hola.

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

segundo Hola obtiene Hello etiquetado máquinas virtuales con `az resouce list` filtra toohello recursos que son máquinas virtuales y se reinicia esas máquinas virtuales.

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

Este ejemplo funciona en un shell de Bash. Para opciones sobre cómo ejecutar las secuencias de comandos de CLI de Azure en el cliente de Windows, vea [ejecuta Hola CLI de Azure en Windows](../windows/cli-options.md).


## <a name="sample-script"></a>Script de ejemplo

ejemplo de Hola tiene tres secuencias de comandos.
Hola primero disposiciones hello las máquinas virtuales.
Utiliza la opción de no espera de Hola para que comandos de hello devuelva sin tener que esperar en cada toobe VM aprovisionado.
en segundo lugar Hola espera toobe de máquinas virtuales de hello aprovisionado por completo.
script tercer Hola reinicia todas las máquinas virtuales de hello aprovisionados y, a continuación, simplemente Hola etiqueta las máquinas virtuales.

### <a name="provision-hello-vms"></a>Hola aprovisionar máquinas virtuales

Este script crea un grupo de recursos y, a continuación, crea tres toorestart de máquinas virtuales.
Dos de ellos tienen etiqueta.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a>Esperar

Este script se comprueba en hello cada 20 segundos hasta que todas las tres máquinas virtuales se aprovisionan o uno de ellos se produce un error tooprovision en el estado de aprovisionamiento.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a>Reiniciar las máquinas virtuales de Hola

Esta secuencia de comandos reinicia todas las máquinas virtuales de hello en el grupo de recursos de hello y, a continuación, reinicia las máquinas virtuales Hola etiquetado.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser tooremove usa grupos de recursos de hello, máquinas virtuales y todos ellos relacionados con recursos.

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toocreate un grupo de recursos, máquina virtual, conjunto de disponibilidad, equilibrador de carga y todos los recursos relacionados. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Crea hello las máquinas virtuales.  |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | Usar con `--query` tooensure hello las máquinas virtuales se aprovisionan antes de reiniciar ellos y, a continuación, tooget Hola identificadores de hello las máquinas virtuales toorestart ellos. |
| [az resource list](https://docs.microsoft.com/cli/azure/vm#list) | Usar con `--query` tooget Hola identificadores de máquinas virtuales de hello con etiqueta de Hola. |
| [az vm restart](https://docs.microsoft.com/cli/azure/vm#list) | Reinicia las máquinas virtuales de Hola. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
