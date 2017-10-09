---
title: "aaaRedeploy máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Cómo emite máquinas virtuales de Linux tooredeploy en conexión de SSH de toomitigate de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a><span data-ttu-id="e5b01-103">Volver a implementar la máquina virtual de Linux toonew nodos de Azure</span><span class="sxs-lookup"><span data-stu-id="e5b01-103">Redeploy Linux virtual machine toonew Azure node</span></span>
<span data-ttu-id="e5b01-104">Si se enfrentan dificultades en la solución de problemas de SSH o aplicación tener acceso a la máquina virtual de Linux de tooa (VM) en Azure, volver a implementar Hola VM puede ayudar.</span><span class="sxs-lookup"><span data-stu-id="e5b01-104">If you face difficulties troubleshooting SSH or application access tooa Linux virtual machine (VM) in Azure, redeploying hello VM may help.</span></span> <span data-ttu-id="e5b01-105">Cuando se vuelve a implementar una máquina virtual, se desplaza Hola VM tooa nuevo nodo dentro de hello infraestructura de Azure y, a continuación, enciende.</span><span class="sxs-lookup"><span data-stu-id="e5b01-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="e5b01-106">Se conservan todas las opciones de configuración y los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="e5b01-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="e5b01-107">Este artículo muestra cómo tooredeploy una máquina virtual mediante la CLI de Azure o hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b01-107">This article shows you how tooredeploy a VM using Azure CLI or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="e5b01-108">Después de volver a implementar una máquina virtual, se perderá disco temporal de Hola y direcciones IP dinámicas asociadas con la interfaz de red virtual se actualizan.</span><span class="sxs-lookup"><span data-stu-id="e5b01-108">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="e5b01-109">Puede volver a implementar una máquina virtual mediante una de las siguientes opciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5b01-109">You can redeploy a VM using one of hello following options.</span></span> <span data-ttu-id="e5b01-110">Solo necesita toochoose una opción tooredeploy la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="e5b01-110">You only need toochoose one option tooredeploy your VM:</span></span>

- [<span data-ttu-id="e5b01-111">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e5b01-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="e5b01-112">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e5b01-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="e5b01-113">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e5b01-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="e5b01-114">Usar hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e5b01-114">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="e5b01-115">Hola de instalación más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e5b01-115">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e5b01-116">Vuelva a implementar la máquina virtual con [az vm redeploy](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="e5b01-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="e5b01-117">Después de nuevas implementaciones de ejemplo de Hola Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e5b01-117">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="e5b01-118">Usar hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e5b01-118">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="e5b01-119">Instalar hello [más reciente Azure CLI 1.0](../../cli-install-nodejs.md), inicie sesión en tooan cuenta de Azure y asegúrese de que está en modo de administrador de recursos (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="e5b01-119">Install hello [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in tooan Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="e5b01-120">Después de nuevas implementaciones de ejemplo de Hola Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e5b01-120">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="e5b01-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5b01-121">Next steps</span></span>
<span data-ttu-id="e5b01-122">Si tiene problemas para conectarse tooyour VM, puede buscar ayuda específica en [solucionar problemas de conexión de SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [detallan los pasos para solucionar problemas de SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5b01-122">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e5b01-123">También puede leer sobre la [solución de problemas de aplicaciones](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) si no puede acceder a una aplicación que se ejecuta en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e5b01-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

