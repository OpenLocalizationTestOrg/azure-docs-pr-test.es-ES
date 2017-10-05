---
title: "Creación de clústeres de Hadoop con plantillas - Azure HDInsight | Microsoft Docs"
description: "Aprenda a crear clústeres para HDInsight con plantillas de Resource Manager"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: b2cdc954530daea2a641599c946ce3787149e762
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="4211e-103">Creación de clústeres de Hadoop en HDInsight con plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4211e-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="4211e-104">En este artículo aprenderá varias formas de crear clústeres de Azure HDInsight mediante plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4211e-104">In this article, you learn several ways to create Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="4211e-105">Para obtener más información, consulte [Implementación de una aplicación con la plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4211e-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="4211e-106">Para obtener información sobre otras herramientas y características de creación de clústeres, haga clic en la selección de pestaña de la parte superior de esta página o consulte los [métodos de creación de clústeres](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="4211e-106">To learn about other cluster creation tools and features, click the tab selector on the top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4211e-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4211e-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="4211e-108">Para seguir las instrucciones de este artículo, necesitará:</span><span class="sxs-lookup"><span data-stu-id="4211e-108">To follow the instructions in this article, you'll need:</span></span>

* <span data-ttu-id="4211e-109">Una [suscripción de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4211e-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="4211e-110">Azure PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4211e-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="4211e-111">Plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4211e-111">Resource Manager templates</span></span>
<span data-ttu-id="4211e-112">Una plantilla de Resource Manager facilita la creación de los siguientes elementos de la aplicación en una única operación coordinada:</span><span class="sxs-lookup"><span data-stu-id="4211e-112">A Resource Manager template makes it easy to create the following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="4211e-113">Clústeres de HDInsight y sus recursos dependientes (por ejemplo, la cuenta de almacenamiento predeterminada)</span><span class="sxs-lookup"><span data-stu-id="4211e-113">HDInsight clusters and their dependent resources (such as the default storage account)</span></span>
* <span data-ttu-id="4211e-114">Otros recursos (por ejemplo, Azure SQL Database para usar Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="4211e-114">Other resources (such as Azure SQL Database to use Apache Sqoop)</span></span>

<span data-ttu-id="4211e-115">En la plantilla, se definen los recursos que son necesarios para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4211e-115">In the template, you define the resources that are needed for the application.</span></span> <span data-ttu-id="4211e-116">También se especifican los parámetros de implementación para introducir los valores para los diferentes entornos.</span><span class="sxs-lookup"><span data-stu-id="4211e-116">You also specify deployment parameters to input values for different environments.</span></span> <span data-ttu-id="4211e-117">La plantilla consta de JSON y expresiones que puede usar para generar valores para su implementación.</span><span class="sxs-lookup"><span data-stu-id="4211e-117">The template consists of JSON and expressions that you use to construct values for your deployment.</span></span>

<span data-ttu-id="4211e-118">Puede encontrar plantillas de HDInsight de ejemplo en [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="4211e-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="4211e-119">Utilice [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) multiplataforma con la [extensión de Resource Manager](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) o un editor de texto para guardar la plantilla en un archivo en su estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4211e-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with the [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor to save the template into a file on your workstation.</span></span> <span data-ttu-id="4211e-120">En este documento, puede obtener información sobre cómo llamar a la plantilla mediante distintos métodos.</span><span class="sxs-lookup"><span data-stu-id="4211e-120">You learn how to call the template by using different methods.</span></span>

<span data-ttu-id="4211e-121">Para más información sobre la plantilla de Resource Manager, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4211e-121">For more information about Resource Manager templates, see the following articles:</span></span>

* [<span data-ttu-id="4211e-122">Creación de plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4211e-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="4211e-123">Implementación de una aplicación con las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4211e-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="4211e-124">Generación de plantillas</span><span class="sxs-lookup"><span data-stu-id="4211e-124">Generate templates</span></span>

<span data-ttu-id="4211e-125">Con Azure Portal puede configurar todas las propiedades de un clúster y, luego, guardar la plantilla antes de la implementación.</span><span class="sxs-lookup"><span data-stu-id="4211e-125">By using the Azure portal, you can configure all the properties of a cluster and then save the template before deploying it.</span></span> <span data-ttu-id="4211e-126">De ese modo, puede volver a usar la plantilla posteriormente.</span><span class="sxs-lookup"><span data-stu-id="4211e-126">You can then reuse the template.</span></span>

<span data-ttu-id="4211e-127">**Para generar una plantilla con Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="4211e-127">**To generate a template by using the Azure portal**</span></span>

1. <span data-ttu-id="4211e-128">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4211e-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4211e-129">En el menú de la izquierda, haga clic en **Nuevo**, **Inteligencia y análisis** y, luego, en **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4211e-129">Click **New** on the left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="4211e-130">Siga las instrucciones para escribir las propiedades.</span><span class="sxs-lookup"><span data-stu-id="4211e-130">Follow the instructions to enter properties.</span></span> <span data-ttu-id="4211e-131">Puede usar la opción de **creación rápida** o la opción para **personalizar**.</span><span class="sxs-lookup"><span data-stu-id="4211e-131">You can use either the **Quick create** or the **Custom** option.</span></span>
4. <span data-ttu-id="4211e-132">En la pestaña **Resumen**, haga clic para **descargar la plantilla y los parámetros**:</span><span class="sxs-lookup"><span data-stu-id="4211e-132">On the **Summary** tab, click **Download template and parameters**:</span></span>

    ![HDInsight Hadoop crear clúster descarga plantilla de Resource Manager](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="4211e-134">Puede ver una lista del archivo de plantilla, el archivo de parámetros y los ejemplos de código usados para implementar la plantilla:</span><span class="sxs-lookup"><span data-stu-id="4211e-134">You see a list of the template file, parameters file, and code samples used to deploy the template:</span></span>

    ![HDInsight Hadoop crear clúster opciones de descarga de plantilla de Resource Manager](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="4211e-136">Aquí puede descargar la plantilla, guardarla en la biblioteca de plantillas o implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="4211e-136">From here, you can download the template, save it to your template library, or deploy the template.</span></span>

    <span data-ttu-id="4211e-137">Para tener acceso a una plantilla de la biblioteca, haga clic en **Más servicios** en el menú de la izquierda y, luego, en **Plantillas** (en la categoría **Otros**).</span><span class="sxs-lookup"><span data-stu-id="4211e-137">To access a template in your library, click **More services** from the left menu, and then click **Templates** (under the **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="4211e-138">El archivo de plantilla y el de parámetros se deben usar conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="4211e-138">The template and parameters file must be used together.</span></span> <span data-ttu-id="4211e-139">De lo contrario, podría obtener resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="4211e-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="4211e-140">Por ejemplo, el valor de la propiedad **clusterKind** siempre es **hadoop**, independientemente de lo que haya especificado antes de descargar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="4211e-140">For example, the default **clusterKind** property value is always **hadoop**, despite what you specify before you download the template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="4211e-141">Implementación con PowerShell</span><span class="sxs-lookup"><span data-stu-id="4211e-141">Deploy with PowerShell</span></span>

<span data-ttu-id="4211e-142">Este procedimiento permite crear el clúster de Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4211e-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="4211e-143">Guarde el archivo JSON en el [Apéndice](#appx-a-arm-template) de la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4211e-143">Save the JSON file in the [Appendix](#appx-a-arm-template) to your workstation.</span></span> <span data-ttu-id="4211e-144">En el script de PowerShell, el nombre de archivo es `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="4211e-144">In the PowerShell script, the file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="4211e-145">Si fuera necesario, establezca los parámetros y las variables.</span><span class="sxs-lookup"><span data-stu-id="4211e-145">Set the parameters and variables if needed.</span></span>
3. <span data-ttu-id="4211e-146">Ejecute la plantilla con el siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4211e-146">Run the template by using the following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect to Azure
        ####################################
        #region - Connect to Azure subscription
        Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and the dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="4211e-147">El script de PowerShell solo configura el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="4211e-147">The PowerShell script configures only the cluster name.</span></span> <span data-ttu-id="4211e-148">El nombre de la cuenta de almacenamiento está codificado en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="4211e-148">The storage account name is hard-coded in the template.</span></span> <span data-ttu-id="4211e-149">Se le pide que escriba la contraseña del usuario del clúster.</span><span class="sxs-lookup"><span data-stu-id="4211e-149">You are prompted to enter the cluster user password.</span></span> <span data-ttu-id="4211e-150">(El nombre de usuario predeterminado es **admin**). Se le pide también que escriba la contraseña del usuario SSH.</span><span class="sxs-lookup"><span data-stu-id="4211e-150">(The default username is **admin**.) You are also prompted to enter the SSH user password.</span></span> <span data-ttu-id="4211e-151">(El nombre predeterminado del usuario SSH es **sshuser**).</span><span class="sxs-lookup"><span data-stu-id="4211e-151">(The default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="4211e-152">Para obtener más información, consulte [Implementación con PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="4211e-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="4211e-153">Implementación con la CLI</span><span class="sxs-lookup"><span data-stu-id="4211e-153">Deploy with CLI</span></span>
<span data-ttu-id="4211e-154">El ejemplo siguiente utiliza la interfaz de la línea de comandos (CLI) de Azure.</span><span class="sxs-lookup"><span data-stu-id="4211e-154">The following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="4211e-155">En él, se crea un clúster y su contenedor y cuenta de almacenamiento dependientes mediante una llamada a una plantilla de Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="4211e-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="4211e-156">Se le solicitará que escriba:</span><span class="sxs-lookup"><span data-stu-id="4211e-156">You are prompted to enter:</span></span>
* <span data-ttu-id="4211e-157">El nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="4211e-157">The cluster name.</span></span>
* <span data-ttu-id="4211e-158">La contraseña de usuario del clúster.</span><span class="sxs-lookup"><span data-stu-id="4211e-158">The cluster user password.</span></span> <span data-ttu-id="4211e-159">(El nombre de usuario predeterminado es **admin**).</span><span class="sxs-lookup"><span data-stu-id="4211e-159">(The default username is **admin**.)</span></span>
* <span data-ttu-id="4211e-160">La contraseña del usuario SSH.</span><span class="sxs-lookup"><span data-stu-id="4211e-160">The SSH user password.</span></span> <span data-ttu-id="4211e-161">(El nombre predeterminado del usuario SSH es **sshuser**).</span><span class="sxs-lookup"><span data-stu-id="4211e-161">(The default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="4211e-162">El código siguiente proporciona los parámetros en línea:</span><span class="sxs-lookup"><span data-stu-id="4211e-162">The following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="4211e-163">Implementación con la API de REST</span><span class="sxs-lookup"><span data-stu-id="4211e-163">Deploy with the REST API</span></span>
<span data-ttu-id="4211e-164">Consulte [Implementación con la API de REST](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="4211e-164">See [Deploy with the REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="4211e-165">Implementación con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4211e-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="4211e-166">Use Visual Studio para crear un proyecto del grupo de recursos e implementarlo en Azure a través de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="4211e-166">Use Visual Studio to create a resource group project and deploy it to Azure through the user interface.</span></span> <span data-ttu-id="4211e-167">Seleccione el tipo de recursos que va a incluir en su proyecto.</span><span class="sxs-lookup"><span data-stu-id="4211e-167">You select the type of resources to include in your project.</span></span> <span data-ttu-id="4211e-168">Estos recursos se agregan automáticamente a la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4211e-168">Those resources are automatically added to the Resource Manager template.</span></span> <span data-ttu-id="4211e-169">El proyecto también ofrece un script de PowerShell para implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="4211e-169">The project also provides a PowerShell script to deploy the template.</span></span>

<span data-ttu-id="4211e-170">Para ver una introducción sobre el uso de Visual Studio con grupos de recursos, consulte [Creación e implementación de grupos de recursos de Azure mediante Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4211e-170">For an introduction to using Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="4211e-171">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="4211e-171">Troubleshoot</span></span>

<span data-ttu-id="4211e-172">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="4211e-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4211e-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4211e-173">Next steps</span></span>
<span data-ttu-id="4211e-174">En este artículo, ha aprendido varias maneras de crear un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4211e-174">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="4211e-175">Para obtener más información, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4211e-175">To learn more, see the following articles:</span></span>

* <span data-ttu-id="4211e-176">Para ver un ejemplo de cómo implementar los recursos mediante la biblioteca cliente de .NET, consulte [Deploy Azure resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)(Implementación de recursos de Azure mediante bibliotecas de .NET y una plantilla).</span><span class="sxs-lookup"><span data-stu-id="4211e-176">For an example of deploying resources through the .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="4211e-177">Para ver un ejemplo en profundidad de la implementación de una aplicación, consulte [Aprovisionamiento e implementación predecibles de microservicios en Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="4211e-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="4211e-178">Para obtener instrucciones sobre cómo implementar la solución en diferentes entornos, vea [Entornos de desarrollo y pruebas en Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="4211e-178">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="4211e-179">Para información sobre las secciones de la plantilla de Azure Resource Manager, consulte [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4211e-179">To learn about the sections of the Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="4211e-180">Para ver una lista de las funciones que puede usar en una plantilla de Azure Resource Manager, consulte [Funciones de la plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="4211e-180">For a list of the functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-to-create-a-hadoop-cluster"></a><span data-ttu-id="4211e-181">Apéndice: plantilla de Resource Manager para crear un clúster de Hadoop</span><span class="sxs-lookup"><span data-stu-id="4211e-181">Appendix: Resource Manager template to create a Hadoop cluster</span></span>
<span data-ttu-id="4211e-182">La siguiente plantilla de Azure Resource Manager crea un clúster de Hadoop basado en Linux con la cuenta de Azure Storage dependiente.</span><span class="sxs-lookup"><span data-stu-id="4211e-182">The following Azure Resource Manager template creates a Linux-based Hadoop cluster with the dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="4211e-183">El ejemplo incluye información de configuración de la tienda de Hive y Oozie Metastore.</span><span class="sxs-lookup"><span data-stu-id="4211e-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="4211e-184">Quite la sección o configúrela antes de usar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="4211e-184">Remove the section or configure the section before using the template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "The name of the HDInsight cluster to create."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used to remotely access the cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "The location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "The type of the HDInsight cluster to create."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "The number of nodes in the HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-to-create-a-spark-cluster"></a><span data-ttu-id="4211e-185">Apéndice: plantilla de Resource Manager para crear un clúster de Spark</span><span class="sxs-lookup"><span data-stu-id="4211e-185">Appendix: Resource Manager template to create a Spark cluster</span></span>

<span data-ttu-id="4211e-186">En esta sección se proporciona una plantilla de Resource Manager que se puede usar para crear un clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="4211e-186">This section provides a Resource Manager template that you can use to create an HDInsight Spark cluster.</span></span> <span data-ttu-id="4211e-187">Esta plantilla incluye configuraciones para `spark-defaults` y `spark-thrift-sparkconf` (para clústeres de Spark 1.6) y `spark2-defaults` y `spark2-thrift-sparkconf` (para clústeres de Spark 2).</span><span class="sxs-lookup"><span data-stu-id="4211e-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="4211e-188">Además, HDInsight calcula y establece configuraciones como `spark.executor.instances`, `spark.executor.memory` y `spark.executor.cores` en función del tamaño del clúster.</span><span class="sxs-lookup"><span data-stu-id="4211e-188">In addition to this, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on the cluster size.</span></span> 

<span data-ttu-id="4211e-189">Si se establece cualquier parámetro de una sección como parte de la propia plantilla, HDInsight no calcula ni establece los demás parámetros de la misma sección.</span><span class="sxs-lookup"><span data-stu-id="4211e-189">If you set any one parameter in a section as part of the template itself, HDInsight does not calculate and set the other parameters of the same section.</span></span> <span data-ttu-id="4211e-190">Por ejemplo, el parámetro `spark.executor.instances` está en la configuración `spark-defaults`.</span><span class="sxs-lookup"><span data-stu-id="4211e-190">For example, parameter `spark.executor.instances` is in the  `spark-defaults` configuration.</span></span> <span data-ttu-id="4211e-191">Si se establece otro parámetro (por ejemplo, `spark.yarn.exector.memoryOverhead`) en la configuración `spark-defaults`, HDInsight tampoco calcula ni establece el parámetro `spark.executor.instances`.</span><span class="sxs-lookup"><span data-stu-id="4211e-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in the `spark-defaults` configuration, HDInsight does not calculate and set the `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "The name of the HDInsight cluster to create."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "The location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "The number of nodes in the HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "The type of the HDInsight cluster to create."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used to remotely access the cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
