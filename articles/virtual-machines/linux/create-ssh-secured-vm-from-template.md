---
title: aaaCreate una VM de Linux en Azure desde una plantilla | Documentos de Microsoft
description: "¿Cómo toouse Hola CLI de Azure 2.0 toocreate una VM de Linux desde una plantilla de administrador de recursos"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="da459-103">¿Cómo toocreate una máquina virtual de Linux con plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="da459-103">How toocreate a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="da459-104">Este artículo muestra cómo tooquickly implementar una máquina virtual de Linux (VM) con hello Azure CLI 2.0 y plantillas del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="da459-104">This article shows you how tooquickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and hello Azure CLI 2.0.</span></span> <span data-ttu-id="da459-105">También puede realizar estos pasos con hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="da459-105">You can also perform these steps with hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="da459-106">Introducción a las plantillas</span><span class="sxs-lookup"><span data-stu-id="da459-106">Templates overview</span></span>
<span data-ttu-id="da459-107">Plantillas de administrador de recursos de Azure son archivos JSON que definen la infraestructura de Hola y la configuración de la solución de Azure.</span><span class="sxs-lookup"><span data-stu-id="da459-107">Azure Resource Manager templates are JSON files that define hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="da459-108">Mediante una plantilla, puede implementar la solución repetidamente a lo largo del ciclo de vida y tener la seguridad de que los recursos se implementan de forma coherente.</span><span class="sxs-lookup"><span data-stu-id="da459-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="da459-109">toolearn más información acerca del formato de Hola de plantilla de Hola y cómo se crea, consulte [crear la primera plantilla de Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="da459-109">toolearn more about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="da459-110">Hola tooview sintaxis de JSON para los tipos de recursos, consulte [definir los recursos en las plantillas de Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="da459-110">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="da459-111">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="da459-111">Create resource group</span></span>
<span data-ttu-id="da459-112">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="da459-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="da459-113">Se debe crear un grupo de recursos antes de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da459-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="da459-114">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupVM* en hello *eastus* región:</span><span class="sxs-lookup"><span data-stu-id="da459-114">hello following example creates a resource group named *myResourceGroupVM* in hello *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="da459-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="da459-115">Create virtual machine</span></span>
<span data-ttu-id="da459-116">Hello en el ejemplo siguiente se crea una máquina virtual desde [esta plantilla de Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) con [Crear implementación de grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="da459-116">hello following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="da459-117">Proporcionar valor Hola de su propia clave pública SSH, como contenido de Hola de *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="da459-117">Provide hello value of your own SSH public key, such as hello contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="da459-118">Si necesita toocreate un par de claves de SSH, consulte [cómo toocreate y use un SSH par de claves para máquinas virtuales de Linux en Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="da459-118">If you need toocreate an SSH key pair, see [How toocreate and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="da459-119">En este ejemplo, especificó una plantilla almacenada en GitHub.</span><span class="sxs-lookup"><span data-stu-id="da459-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="da459-120">También puede descargar o crear una plantilla y especificar la ruta de acceso local de hello con hello mismo `--template-file` parámetro.</span><span class="sxs-lookup"><span data-stu-id="da459-120">You can also download or create a template and specify hello local path with hello same `--template-file` parameter.</span></span>

<span data-ttu-id="da459-121">tooSSH tooyour VM, obtener dirección IP pública de hello con [show de public-ip de red az](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="da459-121">tooSSH tooyour VM, obtain hello public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="da459-122">A continuación puede SSH tooyour VM como normal:</span><span class="sxs-lookup"><span data-stu-id="da459-122">You can then SSH tooyour VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="da459-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="da459-123">Next steps</span></span>
<span data-ttu-id="da459-124">En este ejemplo, creó una máquina virtual Linux básica.</span><span class="sxs-lookup"><span data-stu-id="da459-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="da459-125">Para obtener más plantillas de administrador de recursos que incluyen marcos de aplicaciones o crear entornos más complejos, examinar hello [Galería de plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="da459-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse hello [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>
