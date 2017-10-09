---
title: aaaCreate una VM de Linux con una plantilla de Azure 1.0 de CLI de Azure | Documentos de Microsoft
description: Crear una VM de Linux en Azure con hello 1.0 de CLI de Azure y una plantilla de Azure Resource Manager.
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
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="b9390-103">¿Cómo toocreate una VM de Linux con hello Azure CLI 1.0 una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b9390-103">How toocreate a Linux VM using hello Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="b9390-104">Este artículo muestra cómo tooquickly implementar una máquina Virtual de Linux con hello 1.0 de CLI de Azure y una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b9390-104">This article shows you how tooquickly deploy a Linux Virtual Machine using hello Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="b9390-105">Hola artículo requiere:</span><span class="sxs-lookup"><span data-stu-id="b9390-105">hello article requires:</span></span>

* <span data-ttu-id="b9390-106">una cuenta de Azure ([obtenga aquí una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/));</span><span class="sxs-lookup"><span data-stu-id="b9390-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="b9390-107">Hola [Azure CLI 1.0](../../cli-install-nodejs.md) inició sesión `azure login`.</span><span class="sxs-lookup"><span data-stu-id="b9390-107">hello [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="b9390-108">Hola CLI de Azure *debe estar en* modo Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="b9390-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="b9390-109">Puede implementar rápidamente una plantilla de VM de Linux mediante el uso de hello [portal de Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b9390-109">You can also quickly deploy a Linux VM template by using hello [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b9390-110">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="b9390-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="b9390-111">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="b9390-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="b9390-112">[Azure 1.0 de CLI](#quick-command-summary) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="b9390-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b9390-113">[Azure 2.0 CLI](create-ssh-secured-vm-from-template.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="b9390-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="b9390-114">Resumen rápido de comandos</span><span class="sxs-lookup"><span data-stu-id="b9390-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b9390-115">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="b9390-115">Detailed Walkthrough</span></span>
<span data-ttu-id="b9390-116">Las plantillas permiten toocreate las máquinas virtuales en Azure con la configuración que desee toocustomize durante el inicio de hello, opciones, como nombres de usuario y los nombres de host.</span><span class="sxs-lookup"><span data-stu-id="b9390-116">Templates allow you toocreate VMs on Azure with settings that you want toocustomize during hello launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="b9390-117">En este artículo, hemos iniciado una plantilla de Azure mediante una máquina virtual de Ubuntu junto con un grupo de seguridad de red (NSG) con el puerto 22 abierto para SSH.</span><span class="sxs-lookup"><span data-stu-id="b9390-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="b9390-118">Las plantillas de Azure Resource Manager son archivos JSON que se pueden usar para tareas sencillas y excepcionales, como iniciar una máquina virtual de Ubuntu, como lo hizo en este artículo.</span><span class="sxs-lookup"><span data-stu-id="b9390-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="b9390-119">Plantillas de Azure también pueden ser configuraciones complejas de Azure usa tooconstruct de entornos completas como una pila de implementación de prueba, desarrollo o de producción.</span><span class="sxs-lookup"><span data-stu-id="b9390-119">Azure Templates can also be used tooconstruct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-hello-linux-vm"></a><span data-ttu-id="b9390-120">Crear hello VM de Linux</span><span class="sxs-lookup"><span data-stu-id="b9390-120">Create hello Linux VM</span></span>
<span data-ttu-id="b9390-121">Hola siguiendo el ejemplo de código muestra cómo toocall `azure group create` toocreate un recurso de grupo e implementar una VM de Linux protegidas mediante SSH en hello mismo tiempo, use [esta plantilla de Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b9390-121">hello following code example shows how toocall `azure group create` toocreate a resource group and deploy an SSH-secured Linux VM at hello same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="b9390-122">Recuerde que en el ejemplo, es preciso nombres toouse tooyour único entorno.</span><span class="sxs-lookup"><span data-stu-id="b9390-122">Remember that in your example you need toouse names that are unique tooyour environment.</span></span> <span data-ttu-id="b9390-123">Este ejemplo se utiliza *myResourceGroup* como nombre de grupo de recursos de hello, y *myVM* como nombre de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b9390-123">This example uses *myResourceGroup* as hello resource group name, and *myVM* as hello VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="b9390-124">salida de Hello debería ser similar Hola siguiente bloque de salida:</span><span class="sxs-lookup"><span data-stu-id="b9390-124">hello output should look like hello following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
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

<span data-ttu-id="b9390-125">En el ejemplo que se implementa una máquina virtual mediante hello `--template-uri` parámetro.</span><span class="sxs-lookup"><span data-stu-id="b9390-125">That example deployed a VM using hello `--template-uri` parameter.</span></span>  <span data-ttu-id="b9390-126">También puede descargar o crear una plantilla de forma local y pasar la plantilla de hello con hello `--template-file` parámetro con un archivo de plantilla de ruta de acceso toohello como un argumento.</span><span class="sxs-lookup"><span data-stu-id="b9390-126">You can also download or create a template locally and pass hello template using hello `--template-file` parameter with a path toohello template file as an argument.</span></span> <span data-ttu-id="b9390-127">Hola CLI de Azure le pide parámetros de hello requeridos por plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b9390-127">hello Azure CLI prompts you for hello parameters required by hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9390-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b9390-128">Next steps</span></span>
<span data-ttu-id="b9390-129">Hola de búsqueda [Galería de plantillas](https://azure.microsoft.com/documentation/templates/) toodiscover qué toodeploy de marcos de aplicación siguiente.</span><span class="sxs-lookup"><span data-stu-id="b9390-129">Search hello [templates gallery](https://azure.microsoft.com/documentation/templates/) toodiscover what app frameworks toodeploy next.</span></span>

