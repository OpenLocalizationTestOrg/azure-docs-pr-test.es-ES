---
title: "Creación de un equilibrador de carga con conexión a Internet: plantilla de Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo crear un equilibrador de carga orientado a Internet en el Administrador de recursos mediante una plantilla"
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
ms.openlocfilehash: d829000e63515814b192f3f8256e3b8637bb3a34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="d5ea2-103">Creación de un equilibrador de carga orientado a Internet mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="d5ea2-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5ea2-104">Portal</span><span class="sxs-lookup"><span data-stu-id="d5ea2-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="d5ea2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5ea2-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="d5ea2-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d5ea2-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="d5ea2-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="d5ea2-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d5ea2-108">Este artículo trata sobre el modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="d5ea2-109">También puede [obtener información sobre cómo crear un equilibrador de carga orientado a Internet mediante el modelo de implementación clásica](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d5ea2-109">You can also [Learn how to create an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="d5ea2-110">Implementar la plantilla por medio de un solo clic para implementar</span><span class="sxs-lookup"><span data-stu-id="d5ea2-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="d5ea2-111">La plantilla de ejemplo disponible en el repositorio público usa un archivo de parámetros que contiene los valores predeterminados utilizados para generar el escenario descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="d5ea2-112">Para implementar esta plantilla mediante el método de hacer clic para implementar, siga [esta plantilla](http://go.microsoft.com/fwlink/?LinkId=544801), haga clic en **Implementar en Azure**, reemplace los valores de parámetro predeterminados si es necesario y siga las instrucciones del portal.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-112">To deploy this template using click to deploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="d5ea2-113">Implementación de la plantilla mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5ea2-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="d5ea2-114">Para implementar la plantilla que descargó con PowerShell, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="d5ea2-115">Si es la primera vez que usa Azure PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) y siga las instrucciones hasta el final para iniciar sesión en Azure y seleccionar su suscripción.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="d5ea2-116">Ejecute el cmdlet **New-AzureRmResourceGroupDeployment** para crear un grupo de recursos mediante esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-116">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="d5ea2-117">Implementación la plantilla ARM mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d5ea2-117">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="d5ea2-118">Para implementar la plantilla ARM mediante la CLI de Azure, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-118">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="d5ea2-119">Si nunca ha usado la CLI de Azure, consulte [Instalación y configuración de la CLI de Azure](../cli-install-nodejs.md) y siga las instrucciones hasta el punto donde deba seleccionar su cuenta y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-119">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d5ea2-120">Ejecute el comando **azure config mode** para cambiar al modo de Administrador de recursos, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-120">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="d5ea2-121">Este es el resultado esperado del comando anterior:</span><span class="sxs-lookup"><span data-stu-id="d5ea2-121">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="d5ea2-122">En el explorador, navegue a la [plantilla de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copie el contenido del archivo json y péguelo en un archivo nuevo del equipo.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-122">From your browser, navigate to [the Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy the contents of the json file and paste into a new file in your computer.</span></span> <span data-ttu-id="d5ea2-123">En este escenario, deberá copiar los valores siguientes en un archivo denominado **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-123">For this scenario, you would be copying the values below to a file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="d5ea2-124">Ejecute el cmdlet **azure group deployment create** para implementar el nuevo equilibrador de carga mediante la plantilla y los archivos de parámetros que ha descargado y modificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-124">Run the **azure group deployment create** cmdlet to deploy the new load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="d5ea2-125">En la lista que se muestra en la salida se explican los parámetros utilizados.</span><span class="sxs-lookup"><span data-stu-id="d5ea2-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="d5ea2-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5ea2-126">Next steps</span></span>

[<span data-ttu-id="d5ea2-127">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="d5ea2-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="d5ea2-128">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d5ea2-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d5ea2-129">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d5ea2-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
