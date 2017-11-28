---
title: aaaCreate un equilibrador de carga interno - plantilla de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un interno cargar equilibrador utilizando una plantilla en el Administrador de recursos"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="017a9-103">Creación del equilibrador de carga interno con una plantilla</span><span class="sxs-lookup"><span data-stu-id="017a9-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="017a9-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="017a9-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="017a9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="017a9-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="017a9-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="017a9-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="017a9-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="017a9-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="017a9-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="017a9-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="017a9-109">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="017a9-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="017a9-110">Implementar la plantilla de hello mediante haga clic en toodeploy</span><span class="sxs-lookup"><span data-stu-id="017a9-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="017a9-111">plantilla de ejemplo Hola disponible en el repositorio público de hello usa un archivo de parámetros que contiene el escenario Hola predeterminada valores utilizados toogenerate Hola descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="017a9-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="017a9-112">toodeploy este uso de la plantilla, haga clic en toodeploy, siga [este vínculo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), haga clic en **implementar tooAzure**, reemplazar valores de parámetro predeterminados de hello si es necesario y siga las instrucciones de hello del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="017a9-112">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="017a9-113">Implementar la plantilla de hello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="017a9-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="017a9-114">plantilla de hello toodeploy que ha descargado con PowerShell, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="017a9-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="017a9-115">Si nunca ha usado PowerShell de Azure, consulte [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) y siga instrucciones de hello todos los toohello de manera Hola finalizar toosign en Azure y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="017a9-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="017a9-116">Descargue el disco local de hello parámetros archivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="017a9-116">Download hello parameters file tooyour local disk.</span></span>
3. <span data-ttu-id="017a9-117">Edite el archivo hello y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="017a9-117">Edit hello file and save it.</span></span>
4. <span data-ttu-id="017a9-118">Ejecute hello **New-AzureRmResourceGroupDeployment** toocreate cmdlet un grupo de recursos con Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="017a9-118">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="017a9-119">Implementar la plantilla de hello mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="017a9-119">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="017a9-120">plantilla de hello toodeploy mediante el uso de hello CLI de Azure, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="017a9-120">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="017a9-121">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="017a9-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="017a9-122">Ejecute hello **configuración azure modo** modo de administrador de tooResource de comandos tooswitch, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="017a9-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="017a9-123">Este es el resultado de hello esperada en comando hello anterior:</span><span class="sxs-lookup"><span data-stu-id="017a9-123">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="017a9-124">Abra el archivo de parámetros de hello, seleccione su contenido y guarde el archivo tooa en el equipo.</span><span class="sxs-lookup"><span data-stu-id="017a9-124">Open hello parameter file, select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="017a9-125">En este ejemplo, hemos guardado archivo de parámetros de hello demasiado*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="017a9-125">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="017a9-126">Ejecute hello **Crear implementación de grupo de azure** archivos de comandos toodeploy Hola nuevo equilibrador de carga interno mediante el uso de la plantilla de Hola y los parámetros que ha descargado y modificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="017a9-126">Run hello **azure group deployment create** command toodeploy hello new internal load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="017a9-127">lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.</span><span class="sxs-lookup"><span data-stu-id="017a9-127">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="017a9-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="017a9-128">Next steps</span></span>

[<span data-ttu-id="017a9-129">Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen</span><span class="sxs-lookup"><span data-stu-id="017a9-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="017a9-130">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="017a9-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

