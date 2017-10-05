---
title: "Creación de una máquina virtual Linux mediante una plantilla de Azure con la CLI de Azure 1.0 | Microsoft Docs"
description: "En este artículo se explica cómo crear una máquina virtual Linux en Azure mediante una plantilla de Azure Resource Manager y la CLI de Azure 1.0."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 33d4aaa78fcdf3bd9e2e236606f2d3049f464a8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-vm-using-the-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="72c38-103">Procedimiento para crear una máquina virtual Linux mediante una plantilla de Azure Resource Manager y la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="72c38-103">How to create a Linux VM using the Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="72c38-104">En este artículo se muestra cómo implementar rápidamente una máquina virtual Linux con plantillas de Azure Resource Manager y la CLI de Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="72c38-104">This article shows you how to quickly deploy a Linux Virtual Machine using the Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="72c38-105">Este artículo requiere:</span><span class="sxs-lookup"><span data-stu-id="72c38-105">The article requires:</span></span>

* <span data-ttu-id="72c38-106">una cuenta de Azure ([obtenga aquí una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/));</span><span class="sxs-lookup"><span data-stu-id="72c38-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="72c38-107">la [CLI de Azure 1.0](../../cli-install-nodejs.md) en la que se inició sesión con `azure login`;</span><span class="sxs-lookup"><span data-stu-id="72c38-107">the [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="72c38-108">la CLI de Azure *debe estar en* el modo Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="72c38-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="72c38-109">También puede implementar rápidamente una plantilla de máquina virtual Linux mediante [Azure Portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72c38-109">You can also quickly deploy a Linux VM template by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="72c38-110">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="72c38-110">CLI versions to complete the task</span></span>
<span data-ttu-id="72c38-111">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="72c38-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="72c38-112">[CLI de Azure 1.0](#quick-command-summary): la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="72c38-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="72c38-113">[CLI de Azure 2.0](create-ssh-secured-vm-from-template.md): la CLI de última generación para el modelo de implementación de administración de recursos</span><span class="sxs-lookup"><span data-stu-id="72c38-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="72c38-114">Resumen rápido de comandos</span><span class="sxs-lookup"><span data-stu-id="72c38-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="72c38-115">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="72c38-115">Detailed Walkthrough</span></span>
<span data-ttu-id="72c38-116">Las plantillas permiten crear máquinas virtuales en Azure con la configuración que desea personalizar durante el inicio, por ejemplo, nombres de usuario y nombres de host.</span><span class="sxs-lookup"><span data-stu-id="72c38-116">Templates allow you to create VMs on Azure with settings that you want to customize during the launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="72c38-117">En este artículo, hemos iniciado una plantilla de Azure mediante una máquina virtual de Ubuntu junto con un grupo de seguridad de red (NSG) con el puerto 22 abierto para SSH.</span><span class="sxs-lookup"><span data-stu-id="72c38-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="72c38-118">Las plantillas de Azure Resource Manager son archivos JSON que se pueden usar para tareas sencillas y excepcionales, como iniciar una máquina virtual de Ubuntu, como lo hizo en este artículo.</span><span class="sxs-lookup"><span data-stu-id="72c38-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="72c38-119">Las plantillas de Azure también se pueden utilizar para crear configuraciones de Azure complejas de entornos completos como una pila de implementación de prueba, desarrollo o producción.</span><span class="sxs-lookup"><span data-stu-id="72c38-119">Azure Templates can also be used to construct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-the-linux-vm"></a><span data-ttu-id="72c38-120">Creación de la máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="72c38-120">Create the Linux VM</span></span>
<span data-ttu-id="72c38-121">El ejemplo de código siguiente muestra cómo llamar a `azure group create` para crear un grupo de recursos e implementar una máquina virtual Linux protegida por SSH al mismo tiempo mediante [esta plantilla de Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="72c38-121">The following code example shows how to call `azure group create` to create a resource group and deploy an SSH-secured Linux VM at the same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="72c38-122">En el ejemplo, recuerde que debe usar nombres que sean únicos en su entorno.</span><span class="sxs-lookup"><span data-stu-id="72c38-122">Remember that in your example you need to use names that are unique to your environment.</span></span> <span data-ttu-id="72c38-123">En este ejemplo se usa *myResourceGroup* como nombre del grupo de recursos, y *myVM* como nombre de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="72c38-123">This example uses *myResourceGroup* as the resource group name, and *myVM* as the VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="72c38-124">La salida debe tener un aspecto similar al siguiente bloque de salida:</span><span class="sxs-lookup"><span data-stu-id="72c38-124">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for the following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="72c38-125">Ese ejemplo implementó una máquina virtual mediante el parámetro `--template-uri` .</span><span class="sxs-lookup"><span data-stu-id="72c38-125">That example deployed a VM using the `--template-uri` parameter.</span></span>  <span data-ttu-id="72c38-126">Puede también descargar o crear una plantilla localmente y pasar la plantilla con el parámetro `--template-file` , indicando la ruta de acceso al archivo de plantilla como argumento.</span><span class="sxs-lookup"><span data-stu-id="72c38-126">You can also download or create a template locally and pass the template using the `--template-file` parameter with a path to the template file as an argument.</span></span> <span data-ttu-id="72c38-127">La CLI de Azure le pide que especifique los parámetros requeridos por la plantilla.</span><span class="sxs-lookup"><span data-stu-id="72c38-127">The Azure CLI prompts you for the parameters required by the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72c38-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72c38-128">Next steps</span></span>
<span data-ttu-id="72c38-129">Busque en la [galería de plantillas](https://azure.microsoft.com/documentation/templates/) para ver qué entornos de aplicación implementará después.</span><span class="sxs-lookup"><span data-stu-id="72c38-129">Search the [templates gallery](https://azure.microsoft.com/documentation/templates/) to discover what app frameworks to deploy next.</span></span>

