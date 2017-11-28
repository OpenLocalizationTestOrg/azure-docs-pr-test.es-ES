---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure cifrar una VM de Linux | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: cifrado de una máquina virtual Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 1e455da4a8ea6d75b6d0d74b338d2e4d84973413
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="966e0-103">Cifrado de una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="966e0-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="966e0-104">Este script crea un almacén Azure Key Vault seguro, claves de cifrado, una entidad de servicio de Azure Active Directory y una máquina virtual (VM) Linux.</span><span class="sxs-lookup"><span data-stu-id="966e0-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="966e0-105">Hola VM, a continuación, se cifra mediante la clave de cifrado de Hola desde el almacén de claves y credenciales de servicio principal.</span><span class="sxs-lookup"><span data-stu-id="966e0-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="966e0-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="966e0-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="966e0-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="966e0-107">Clean up deployment</span></span> 

<span data-ttu-id="966e0-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="966e0-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="966e0-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="966e0-109">Script explanation</span></span>

<span data-ttu-id="966e0-110">Esta secuencia de comandos usa Hola después comandos toocreate una recurso grupo, almacén de claves de Azure, servicio principal, máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="966e0-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="966e0-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="966e0-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="966e0-112">Comando</span><span class="sxs-lookup"><span data-stu-id="966e0-112">Command</span></span> | <span data-ttu-id="966e0-113">Notas</span><span class="sxs-lookup"><span data-stu-id="966e0-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="966e0-114">az group create</span><span class="sxs-lookup"><span data-stu-id="966e0-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="966e0-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="966e0-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="966e0-116">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="966e0-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="966e0-117">Crea un almacén de claves de Azure toostore proteger los datos, como las claves de cifrado.</span><span class="sxs-lookup"><span data-stu-id="966e0-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="966e0-118">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="966e0-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="966e0-119">Crea una clave de cifrado en el almacén Key Vault.</span><span class="sxs-lookup"><span data-stu-id="966e0-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="966e0-120">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="966e0-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="966e0-121">Crea un servicio de Azure Active Directory principal toosecurely autenticar y acceso tooencryption teclas de control.</span><span class="sxs-lookup"><span data-stu-id="966e0-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="966e0-122">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="966e0-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="966e0-123">Establece permisos en toogrant de almacén de claves de hello claves de tooencryption de acceso principal de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="966e0-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="966e0-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="966e0-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="966e0-125">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="966e0-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="966e0-126">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="966e0-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="966e0-127">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="966e0-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="966e0-128">Habilita el cifrado en una máquina virtual usando las credenciales de entidad de seguridad de servicio de Hola y clave de cifrado.</span><span class="sxs-lookup"><span data-stu-id="966e0-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="966e0-129">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="966e0-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="966e0-130">Muestra el estado de Hola de hello proceso de cifrado de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="966e0-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="966e0-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="966e0-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="966e0-132">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="966e0-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="966e0-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="966e0-133">Next steps</span></span>

<span data-ttu-id="966e0-134">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="966e0-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="966e0-135">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="966e0-135">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
