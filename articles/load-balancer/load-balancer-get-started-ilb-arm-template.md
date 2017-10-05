---
title: "Creación de un equilibrador de carga interno: plantilla de Azure | Microsoft Docs"
description: "Obtenga información sobre cómo crear un equilibrador de carga interno mediante una plantilla en el Administrador de recursos"
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
ms.openlocfilehash: 5e0278cf5c605298932d6ac55d147a1c43fd9d23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="df772-103">Creación del equilibrador de carga interno con una plantilla</span><span class="sxs-lookup"><span data-stu-id="df772-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="df772-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="df772-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="df772-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="df772-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="df772-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="df772-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="df772-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="df772-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="df772-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="df772-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="df772-109">En este artículo se describe el uso del modelo de implementación de Resource Manager, recomendado por Microsoft para la mayoría de las nuevas implementaciones en lugar del [modelo de implementación clásica](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="df772-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="df772-110">Implementar la plantilla por medio de un solo clic para implementar</span><span class="sxs-lookup"><span data-stu-id="df772-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="df772-111">La plantilla de ejemplo disponible en el repositorio público usa un archivo de parámetros que contiene los valores predeterminados utilizados para generar el escenario descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="df772-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="df772-112">Para implementar esta plantilla mediante el método de hacer clic para implementar, siga [esta plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), haga clic en **Implementar en Azure**, reemplace los valores de parámetro predeterminados si es necesario y siga las instrucciones del portal.</span><span class="sxs-lookup"><span data-stu-id="df772-112">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="df772-113">Implementación de la plantilla mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="df772-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="df772-114">Para implementar la plantilla que descargó con PowerShell, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="df772-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="df772-115">Si es la primera vez que usa Azure PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) y siga las instrucciones hasta el final para iniciar sesión en Azure y seleccionar su suscripción.</span><span class="sxs-lookup"><span data-stu-id="df772-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="df772-116">Descargue el archivo de parámetros en el disco local.</span><span class="sxs-lookup"><span data-stu-id="df772-116">Download the parameters file to your local disk.</span></span>
3. <span data-ttu-id="df772-117">Edite el archivo y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="df772-117">Edit the file and save it.</span></span>
4. <span data-ttu-id="df772-118">Ejecute el cmdlet **New-AzureRmResourceGroupDeployment** para crear un grupo de recursos mediante esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="df772-118">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="df772-119">Implementación la plantilla ARM mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="df772-119">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="df772-120">Para implementar la plantilla ARM mediante la CLI de Azure, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="df772-120">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="df772-121">Si nunca ha usado la CLI de Azure, consulte [Instalación y configuración de la CLI de Azure](../cli-install-nodejs.md) y siga las instrucciones hasta el punto donde deba seleccionar su cuenta y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="df772-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="df772-122">Ejecute el comando **azure config mode** para cambiar al modo de Administrador de recursos, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="df772-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="df772-123">Este es el resultado esperado del comando anterior:</span><span class="sxs-lookup"><span data-stu-id="df772-123">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="df772-124">Abra el archivo de parámetros, seleccione su contenido y guárdelo en un archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="df772-124">Open the parameter file, select its contents, and save it to a file in your computer.</span></span> <span data-ttu-id="df772-125">Para este ejemplo, guardamos el archivo de parámetros en *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="df772-125">For this example, we saved the parameters file to *parameters.json*.</span></span>
4. <span data-ttu-id="df772-126">Ejecute el comando **azure group deployment create** para implementar el nuevo equilibrador de carga interno mediante la plantilla y los archivos de parámetros que ha descargado y modificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="df772-126">Run the **azure group deployment create** command to deploy the new internal load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="df772-127">En la lista que se muestra en la salida se explican los parámetros utilizados.</span><span class="sxs-lookup"><span data-stu-id="df772-127">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="df772-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df772-128">Next steps</span></span>

[<span data-ttu-id="df772-129">Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen</span><span class="sxs-lookup"><span data-stu-id="df772-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="df772-130">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="df772-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

