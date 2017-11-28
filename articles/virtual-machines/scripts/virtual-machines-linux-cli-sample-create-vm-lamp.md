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
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="a6810-103">Implementar pila LAMP de hello en un conjunto de escala con equilibrio de carga de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a6810-103">Deploy hello LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="a6810-104">Este ejemplo crea un conjunto de escalas de máquina virtual y aplica una extensión que se ejecuta una pila de luz de secuencia de comandos personalizada toodeploy hello en cada máquina virtual en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6810-104">This example creates a virtual machine scale set and applies an extension that runs a custom script toodeploy hello LAMP stack on each virtual machine in hello scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="a6810-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a6810-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="a6810-106">Conectar</span><span class="sxs-lookup"><span data-stu-id="a6810-106">Connect</span></span>

<span data-ttu-id="a6810-107">Utilice este toosee código cómo establecen tooconnect tooyour máquinas virtuales y la escala.</span><span class="sxs-lookup"><span data-stu-id="a6810-107">Use this code toosee how tooconnect tooyour VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a6810-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="a6810-108">Clean up deployment</span></span> 

<span data-ttu-id="a6810-109">Ejecute hello después el grupo de recursos de comando tooremove hello, conjunto de escalas de Hola y las máquinas virtuales y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="a6810-109">Run hello following command tooremove hello resource group, hello scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a6810-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="a6810-110">Script explanation</span></span>

<span data-ttu-id="a6810-111">Este script utiliza Hola después comandos toocreate un grupo de recursos, máquina virtual, conjunto de disponibilidad, equilibrador de carga y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="a6810-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="a6810-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="a6810-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a6810-113">Comando</span><span class="sxs-lookup"><span data-stu-id="a6810-113">Command</span></span> | <span data-ttu-id="a6810-114">Notas</span><span class="sxs-lookup"><span data-stu-id="a6810-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a6810-115">az group create</span><span class="sxs-lookup"><span data-stu-id="a6810-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a6810-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="a6810-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a6810-117">az vmss create</span><span class="sxs-lookup"><span data-stu-id="a6810-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="a6810-118">Crea un conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a6810-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="a6810-119">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="a6810-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="a6810-120">Agrega un punto de conexión de carga equilibrada.</span><span class="sxs-lookup"><span data-stu-id="a6810-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="a6810-121">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="a6810-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="a6810-122">Crear la extensión de Hola que se ejecuta un script personalizado hello en la implementación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a6810-122">Create hello extension that runs hello custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="a6810-123">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="a6810-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="a6810-124">Ejecutar script personalizado de hello en instancias de máquina virtual de Hola que se implementaron antes de que se aplicó la extensión de hello toohello conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="a6810-124">Run hello custom script on hello VM instances that were deployed before hello extension was applied toohello scale set.</span></span> |
| [<span data-ttu-id="a6810-125">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="a6810-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="a6810-126">Escalar verticalmente la escala de hello establecida mediante la adición de más instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a6810-126">Scale up hello scale set by adding more VM instances.</span></span> <span data-ttu-id="a6810-127">secuencia de comandos personalizada Hello se ejecuta en estas cuando se implementan.</span><span class="sxs-lookup"><span data-stu-id="a6810-127">hello custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="a6810-128">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="a6810-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="a6810-129">Obtener direcciones IP de Hola de hello VM creadas en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6810-129">Get hello IP addresses of hello VMs created by hello sample.</span></span> |
| [<span data-ttu-id="a6810-130">az network lb show</span><span class="sxs-lookup"><span data-stu-id="a6810-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="a6810-131">Obtener back-end y front-end de hello puertos utilizados por el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6810-131">Get hello frontend and backend ports used by hello load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a6810-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a6810-132">Next steps</span></span>

<span data-ttu-id="a6810-133">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6810-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a6810-134">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6810-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
