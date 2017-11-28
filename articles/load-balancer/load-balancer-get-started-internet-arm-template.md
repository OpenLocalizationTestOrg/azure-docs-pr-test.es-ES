---
title: "equilibrador de carga de una conexión a Internet de aaaCreate - plantilla de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de en el Administrador de recursos mediante una plantilla de equilibrador de carga de toocreate una conexión a Internet de forma"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="7e9ab-103">Creación de un equilibrador de carga orientado a Internet mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="7e9ab-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7e9ab-104">Portal</span><span class="sxs-lookup"><span data-stu-id="7e9ab-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="7e9ab-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e9ab-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="7e9ab-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7e9ab-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="7e9ab-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="7e9ab-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="7e9ab-108">Este artículo trata el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="7e9ab-109">También puede [Obtenga información acerca de cómo el equilibrador utilizando el modelo de implementación clásica de la carga de toocreate una conexión a Internet](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7e9ab-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="7e9ab-110">Implementar la plantilla de hello mediante haga clic en toodeploy</span><span class="sxs-lookup"><span data-stu-id="7e9ab-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="7e9ab-111">plantilla de ejemplo Hola disponible en el repositorio público de hello usa un archivo de parámetros que contiene el escenario Hola predeterminada valores utilizados toogenerate Hola descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="7e9ab-112">toodeploy este uso de la plantilla, haga clic en toodeploy, siga [este vínculo](http://go.microsoft.com/fwlink/?LinkId=544801), haga clic en **implementar tooAzure**, reemplazar valores de parámetro predeterminados de hello si es necesario y siga las instrucciones de hello del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-112">toodeploy this template using click toodeploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="7e9ab-113">Implementar la plantilla de hello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e9ab-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="7e9ab-114">plantilla de hello toodeploy que ha descargado con PowerShell, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="7e9ab-115">Si nunca ha usado PowerShell de Azure, consulte [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) y siga instrucciones de hello todos los toohello de manera Hola finalizar toosign en Azure y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="7e9ab-116">Ejecute hello **New-AzureRmResourceGroupDeployment** toocreate cmdlet un grupo de recursos con Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-116">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="7e9ab-117">Implementar la plantilla de hello mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7e9ab-117">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="7e9ab-118">plantilla de hello toodeploy mediante el uso de hello CLI de Azure, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-118">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="7e9ab-119">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-119">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="7e9ab-120">Ejecute hello **configuración azure modo** modo de administrador de tooResource de comandos tooswitch, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-120">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="7e9ab-121">Este es el resultado de hello esperada en comando hello anterior:</span><span class="sxs-lookup"><span data-stu-id="7e9ab-121">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="7e9ab-122">Desde el explorador, navegue demasiado[Hola plantilla de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copie el contenido de Hola de archivo json de hello y pegue en un archivo nuevo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-122">From your browser, navigate too[hello Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy hello contents of hello json file and paste into a new file in your computer.</span></span> <span data-ttu-id="7e9ab-123">En este escenario, podría copiar valores de hello a continuación con el nombre de archivo de tooa **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-123">For this scenario, you would be copying hello values below tooa file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="7e9ab-124">Ejecute hello **Crear implementación de grupo de azure** cmdlet toodeploy Hola nuevo equilibrador de carga mediante el uso de la plantilla de Hola y los parámetros de archivos que ha descargado y modificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-124">Run hello **azure group deployment create** cmdlet toodeploy hello new load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="7e9ab-125">lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.</span><span class="sxs-lookup"><span data-stu-id="7e9ab-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="7e9ab-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7e9ab-126">Next steps</span></span>

[<span data-ttu-id="7e9ab-127">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="7e9ab-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="7e9ab-128">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="7e9ab-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="7e9ab-129">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="7e9ab-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
