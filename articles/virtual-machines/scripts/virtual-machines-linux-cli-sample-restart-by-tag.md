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
# <a name="restart-vms"></a><span data-ttu-id="784d1-103">Reinicio de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="784d1-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="784d1-104">Este ejemplo muestra un par de maneras tooget algunas máquinas virtuales y reiniciarlas una vez.</span><span class="sxs-lookup"><span data-stu-id="784d1-104">This sample shows a couple of ways tooget some VMs and restart them.</span></span>

<span data-ttu-id="784d1-105">Hola reinicia primero todas las máquinas virtuales de hello en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="784d1-105">hello first restarts all hello VMs in hello resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="784d1-106">segundo Hola obtiene Hello etiquetado máquinas virtuales con `az resouce list` filtra toohello recursos que son máquinas virtuales y se reinicia esas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="784d1-106">hello second gets hello tagged VMs using `az resouce list` and filters toohello resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="784d1-107">Este ejemplo funciona en un shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="784d1-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="784d1-108">Para opciones sobre cómo ejecutar las secuencias de comandos de CLI de Azure en el cliente de Windows, vea [ejecuta Hola CLI de Azure en Windows](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="784d1-108">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="784d1-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="784d1-109">Sample script</span></span>

<span data-ttu-id="784d1-110">ejemplo de Hola tiene tres secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="784d1-110">hello sample has three scripts.</span></span>
<span data-ttu-id="784d1-111">Hola primero disposiciones hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="784d1-111">hello first one provisions hello virtual machines.</span></span>
<span data-ttu-id="784d1-112">Utiliza la opción de no espera de Hola para que comandos de hello devuelva sin tener que esperar en cada toobe VM aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="784d1-112">It uses hello no-wait option so hello command returns without waiting on each VM toobe provisioned.</span></span>
<span data-ttu-id="784d1-113">en segundo lugar Hola espera toobe de máquinas virtuales de hello aprovisionado por completo.</span><span class="sxs-lookup"><span data-stu-id="784d1-113">hello second waits for hello VMs toobe fully provisioned.</span></span>
<span data-ttu-id="784d1-114">script tercer Hola reinicia todas las máquinas virtuales de hello aprovisionados y, a continuación, simplemente Hola etiqueta las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="784d1-114">hello third script restarts all hello VMs that were provisioned, and then just hello tagged VMs.</span></span>

### <a name="provision-hello-vms"></a><span data-ttu-id="784d1-115">Hola aprovisionar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="784d1-115">Provision hello VMs</span></span>

<span data-ttu-id="784d1-116">Este script crea un grupo de recursos y, a continuación, crea tres toorestart de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="784d1-116">This script creates a resource group and then it creates three VMs toorestart.</span></span>
<span data-ttu-id="784d1-117">Dos de ellos tienen etiqueta.</span><span class="sxs-lookup"><span data-stu-id="784d1-117">Two of them are tagged.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a><span data-ttu-id="784d1-118">Esperar</span><span class="sxs-lookup"><span data-stu-id="784d1-118">Wait</span></span>

<span data-ttu-id="784d1-119">Este script se comprueba en hello cada 20 segundos hasta que todas las tres máquinas virtuales se aprovisionan o uno de ellos se produce un error tooprovision en el estado de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="784d1-119">This script checks on hello provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails tooprovision.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a><span data-ttu-id="784d1-120">Reiniciar las máquinas virtuales de Hola</span><span class="sxs-lookup"><span data-stu-id="784d1-120">Restart hello VMs</span></span>

<span data-ttu-id="784d1-121">Esta secuencia de comandos reinicia todas las máquinas virtuales de hello en el grupo de recursos de hello y, a continuación, reinicia las máquinas virtuales Hola etiquetado.</span><span class="sxs-lookup"><span data-stu-id="784d1-121">This script restarts all hello VMs in hello resource group, and then it restarts just hello tagged VMs.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="784d1-122">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="784d1-122">Clean up deployment</span></span> 

<span data-ttu-id="784d1-123">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser tooremove usa grupos de recursos de hello, máquinas virtuales y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="784d1-123">After hello script sample has been run, hello following command can be used tooremove hello resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="784d1-124">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="784d1-124">Script explanation</span></span>

<span data-ttu-id="784d1-125">Este script utiliza Hola después comandos toocreate un grupo de recursos, máquina virtual, conjunto de disponibilidad, equilibrador de carga y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="784d1-125">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="784d1-126">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="784d1-126">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="784d1-127">Comando</span><span class="sxs-lookup"><span data-stu-id="784d1-127">Command</span></span> | <span data-ttu-id="784d1-128">Notas</span><span class="sxs-lookup"><span data-stu-id="784d1-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="784d1-129">az group create</span><span class="sxs-lookup"><span data-stu-id="784d1-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="784d1-130">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="784d1-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="784d1-131">az vm create</span><span class="sxs-lookup"><span data-stu-id="784d1-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="784d1-132">Crea hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="784d1-132">Creates hello virtual machines.</span></span>  |
| [<span data-ttu-id="784d1-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="784d1-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="784d1-134">Usar con `--query` tooensure hello las máquinas virtuales se aprovisionan antes de reiniciar ellos y, a continuación, tooget Hola identificadores de hello las máquinas virtuales toorestart ellos.</span><span class="sxs-lookup"><span data-stu-id="784d1-134">Used with `--query` tooensure hello VMs are provisioned before restarting them, and then tooget hello IDs of hello VMs toorestart them.</span></span> |
| [<span data-ttu-id="784d1-135">az resource list</span><span class="sxs-lookup"><span data-stu-id="784d1-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="784d1-136">Usar con `--query` tooget Hola identificadores de máquinas virtuales de hello con etiqueta de Hola.</span><span class="sxs-lookup"><span data-stu-id="784d1-136">Used with `--query` tooget hello IDs of hello VMs using hello tag.</span></span> |
| [<span data-ttu-id="784d1-137">az vm restart</span><span class="sxs-lookup"><span data-stu-id="784d1-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="784d1-138">Reinicia las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="784d1-138">Restarts hello VMs.</span></span> |
| [<span data-ttu-id="784d1-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="784d1-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="784d1-140">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="784d1-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="784d1-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="784d1-141">Next steps</span></span>

<span data-ttu-id="784d1-142">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="784d1-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="784d1-143">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="784d1-143">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
