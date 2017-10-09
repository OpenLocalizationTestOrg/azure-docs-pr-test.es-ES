---
title: "aaaSet el almacén de claves de Azure para máquinas virtuales Linux | Documentos de Microsoft"
description: "Cómo tooset el almacén de claves para su uso con una máquina virtual de Azure Resource Manager con Hola CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a><span data-ttu-id="a4269-103">Cómo tooset el almacén de claves para máquinas virtuales con Hola 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a4269-103">How tooset up Key Vault for virtual machines with hello Azure CLI 2.0</span></span>

<span data-ttu-id="a4269-104">En la pila del Administrador de recursos de Azure hello, secretos/certificados se modelan como recursos proporcionados por el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="a4269-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="a4269-105">toolearn más información acerca del almacén de claves de Azure, consulte [¿qué es el almacén de claves de Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="a4269-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="a4269-106">En orden para toobe de almacén de claves que se utiliza con máquinas virtuales del Administrador de recursos de Azure, Hola *EnabledForDeployment* propiedad en el almacén de claves se debe establecer tootrue.</span><span class="sxs-lookup"><span data-stu-id="a4269-106">In order for Key Vault toobe used with Azure Resource Manager VMs, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="a4269-107">Este artículo muestra cómo tooset el almacén de claves para su uso con Azure máquinas virtuales (VM) mediante Hola 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4269-107">This article shows you how tooset up Key Vault for use with Azure virtual machines (VMs) using hello Azure CLI 2.0.</span></span> <span data-ttu-id="a4269-108">También puede realizar estos pasos con hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a4269-108">You can also perform these steps with hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="a4269-109">tooperform estos pasos, necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="a4269-109">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="a4269-110">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="a4269-110">Create a Key Vault</span></span>
<span data-ttu-id="a4269-111">Crear un almacén de claves y asignar la directiva de implementación de hello con [crear az keyvault](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="a4269-111">Create a key vault and assign hello deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="a4269-112">Hello en el ejemplo siguiente se crea un almacén de claves denominado `myKeyVault` en hello `myResourceGroup` grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="a4269-112">hello following example creates a key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="a4269-113">Actualización de un almacén de claves para su uso con VM</span><span class="sxs-lookup"><span data-stu-id="a4269-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="a4269-114">Establecer directiva de implementación de hello en un almacén de claves existente con [actualización de keyvault az](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="a4269-114">Set hello deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="a4269-115">las actualizaciones siguientes Hola Hola almacén de claves denominado `myKeyVault` en hello `myResourceGroup` grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="a4269-115">hello following updates hello key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="a4269-116">Usar plantillas tooset el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="a4269-116">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="a4269-117">Cuando se usa una plantilla, deberá hello tooset `enabledForDeployment` propiedad demasiado`true` para el recurso de almacén de claves de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="a4269-117">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource as follows:</span></span>

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="a4269-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a4269-118">Next steps</span></span>
<span data-ttu-id="a4269-119">Para otras opciones que puede configurar al crear un almacén de claves mediante plantillas, consulte [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)(Creación de un almacén de claves).</span><span class="sxs-lookup"><span data-stu-id="a4269-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
