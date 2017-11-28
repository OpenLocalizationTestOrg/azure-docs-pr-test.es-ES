---
title: "clústeres de Hadoop aaaCreate mediante plantillas - HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate clústeres de HDInsight mediante plantillas de administrador de recursos"
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
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="c1398-103">Creación de clústeres de Hadoop en HDInsight con plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1398-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="c1398-104">En este artículo, aprenderá varias formas de clústeres de toocreate HDInsight de Azure con plantillas del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1398-104">In this article, you learn several ways toocreate Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="c1398-105">Para obtener más información, consulte [Implementación de una aplicación con la plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c1398-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="c1398-106">toolearn acerca de otras herramientas de creación de clúster y características, haga clic en Tabulador de hello en la parte superior de Hola de esta página o vea [métodos de creación de clúster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="c1398-106">toolearn about other cluster creation tools and features, click hello tab selector on hello top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1398-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c1398-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="c1398-108">instrucciones de hello toofollow en este artículo, necesitará:</span><span class="sxs-lookup"><span data-stu-id="c1398-108">toofollow hello instructions in this article, you'll need:</span></span>

* <span data-ttu-id="c1398-109">Una [suscripción de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c1398-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="c1398-110">Azure PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1398-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="c1398-111">Plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1398-111">Resource Manager templates</span></span>
<span data-ttu-id="c1398-112">Una plantilla de administrador de recursos facilita hello toocreate fácil después de la aplicación en una única operación coordinada:</span><span class="sxs-lookup"><span data-stu-id="c1398-112">A Resource Manager template makes it easy toocreate hello following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="c1398-113">Clústeres de HDInsight y sus recursos dependientes (como cuenta de almacenamiento predeterminada de hello)</span><span class="sxs-lookup"><span data-stu-id="c1398-113">HDInsight clusters and their dependent resources (such as hello default storage account)</span></span>
* <span data-ttu-id="c1398-114">Otros recursos (por ejemplo, toouse Sqoop Apache de base de datos de SQL Azure)</span><span class="sxs-lookup"><span data-stu-id="c1398-114">Other resources (such as Azure SQL Database toouse Apache Sqoop)</span></span>

<span data-ttu-id="c1398-115">En la plantilla de hello, definir recursos de Hola que sean necesarios para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c1398-115">In hello template, you define hello resources that are needed for hello application.</span></span> <span data-ttu-id="c1398-116">También especificar tooinput valores de parámetros de implementación para diferentes entornos.</span><span class="sxs-lookup"><span data-stu-id="c1398-116">You also specify deployment parameters tooinput values for different environments.</span></span> <span data-ttu-id="c1398-117">plantilla de Hello consta de JSON y expresiones que usan valores de tooconstruct para su implementación.</span><span class="sxs-lookup"><span data-stu-id="c1398-117">hello template consists of JSON and expressions that you use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="c1398-118">Puede encontrar plantillas de HDInsight de ejemplo en [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="c1398-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="c1398-119">Usar multiplataforma [código de Visual Studio](https://code.visualstudio.com/#alt-downloads) con hello [extensión del Administrador de recursos](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) o una plantilla de Hola de toosave de editor de texto en un archivo en la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c1398-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with hello [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor toosave hello template into a file on your workstation.</span></span> <span data-ttu-id="c1398-120">Obtenga información acerca cómo toocall Hola plantilla mediante diversos métodos.</span><span class="sxs-lookup"><span data-stu-id="c1398-120">You learn how toocall hello template by using different methods.</span></span>

<span data-ttu-id="c1398-121">Para obtener más información acerca de las plantillas de administrador de recursos, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="c1398-121">For more information about Resource Manager templates, see hello following articles:</span></span>

* [<span data-ttu-id="c1398-122">Creación de plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="c1398-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="c1398-123">Implementación de una aplicación con las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1398-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="c1398-124">Generación de plantillas</span><span class="sxs-lookup"><span data-stu-id="c1398-124">Generate templates</span></span>

<span data-ttu-id="c1398-125">Mediante el uso de hello portal de Azure, puede configurar todas las propiedades de Hola de un clúster y, a continuación, Guardar plantilla Hola antes de implementarla.</span><span class="sxs-lookup"><span data-stu-id="c1398-125">By using hello Azure portal, you can configure all hello properties of a cluster and then save hello template before deploying it.</span></span> <span data-ttu-id="c1398-126">A continuación, puede volver a usar plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-126">You can then reuse hello template.</span></span>

<span data-ttu-id="c1398-127">**toogenerate una plantilla mediante Hola portal de Azure**</span><span class="sxs-lookup"><span data-stu-id="c1398-127">**toogenerate a template by using hello Azure portal**</span></span>

1. <span data-ttu-id="c1398-128">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c1398-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c1398-129">Haga clic en **New** en el menú de la izquierda hello, haga clic en **Intelligence + análisis**y, a continuación, haga clic en **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c1398-129">Click **New** on hello left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="c1398-130">Siguen Hola instrucciones tooenter propiedades.</span><span class="sxs-lookup"><span data-stu-id="c1398-130">Follow hello instructions tooenter properties.</span></span> <span data-ttu-id="c1398-131">Puede usar cualquier hello **creación rápida** o hello **personalizado** opción.</span><span class="sxs-lookup"><span data-stu-id="c1398-131">You can use either hello **Quick create** or hello **Custom** option.</span></span>
4. <span data-ttu-id="c1398-132">En hello **resumen** , haga clic en **descargar la plantilla y los parámetros**:</span><span class="sxs-lookup"><span data-stu-id="c1398-132">On hello **Summary** tab, click **Download template and parameters**:</span></span>

    ![HDInsight Hadoop crear clúster descarga plantilla de Resource Manager](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="c1398-134">Ver una lista de archivo de plantilla de hello, archivo de parámetros y ejemplos que se utilizará toodeploy Hola plantilla:</span><span class="sxs-lookup"><span data-stu-id="c1398-134">You see a list of hello template file, parameters file, and code samples used toodeploy hello template:</span></span>

    ![HDInsight Hadoop crear clúster opciones de descarga de plantilla de Resource Manager](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="c1398-136">Desde aquí, puede descargar la plantilla de hello, guardar biblioteca de plantillas de tooyour o implementar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-136">From here, you can download hello template, save it tooyour template library, or deploy hello template.</span></span>

    <span data-ttu-id="c1398-137">tooaccess una plantilla en la biblioteca, haga clic en **más servicios** del menú izquierdo de hello y, a continuación, haga clic en **plantillas** (en hello **otros** categoría).</span><span class="sxs-lookup"><span data-stu-id="c1398-137">tooaccess a template in your library, click **More services** from hello left menu, and then click **Templates** (under hello **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="c1398-138">archivo de plantilla y los parámetros de Hello se debe usar conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="c1398-138">hello template and parameters file must be used together.</span></span> <span data-ttu-id="c1398-139">De lo contrario, podría obtener resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="c1398-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="c1398-140">Por ejemplo, Hola predeterminado **clusterKind** siempre es el valor de la propiedad **hadoop**, a pesar de lo que se especifique antes de descargar plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-140">For example, hello default **clusterKind** property value is always **hadoop**, despite what you specify before you download hello template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="c1398-141">Implementación con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1398-141">Deploy with PowerShell</span></span>

<span data-ttu-id="c1398-142">Este procedimiento permite crear el clúster de Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c1398-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="c1398-143">Guarde el archivo JSON de Hola Hola [apéndice](#appx-a-arm-template) tooyour estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c1398-143">Save hello JSON file in hello [Appendix](#appx-a-arm-template) tooyour workstation.</span></span> <span data-ttu-id="c1398-144">Hola script de PowerShell, nombre de archivo de hello es `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="c1398-144">In hello PowerShell script, hello file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="c1398-145">Establecer parámetros de Hola y variables si es necesario.</span><span class="sxs-lookup"><span data-stu-id="c1398-145">Set hello parameters and variables if needed.</span></span>
3. <span data-ttu-id="c1398-146">Plantilla de ejecución hello mediante Hola siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c1398-146">Run hello template by using hello following PowerShell script:</span></span>

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
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="c1398-147">Hola script de PowerShell configura sólo el nombre de clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-147">hello PowerShell script configures only hello cluster name.</span></span> <span data-ttu-id="c1398-148">nombre de cuenta de almacenamiento de Hello está codificado de forma rígida en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-148">hello storage account name is hard-coded in hello template.</span></span> <span data-ttu-id="c1398-149">Son la contraseña de usuario de clúster de hello tooenter solicitadas.</span><span class="sxs-lookup"><span data-stu-id="c1398-149">You are prompted tooenter hello cluster user password.</span></span> <span data-ttu-id="c1398-150">(nombre de usuario de hello predeterminada es **administración**.) También son contraseña de usuario SSH de hello tooenter solicitadas.</span><span class="sxs-lookup"><span data-stu-id="c1398-150">(hello default username is **admin**.) You are also prompted tooenter hello SSH user password.</span></span> <span data-ttu-id="c1398-151">(nombre de usuario SSH de hello predeterminada es **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="c1398-151">(hello default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="c1398-152">Para obtener más información, consulte [Implementación con PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="c1398-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="c1398-153">Implementación con la CLI</span><span class="sxs-lookup"><span data-stu-id="c1398-153">Deploy with CLI</span></span>
<span data-ttu-id="c1398-154">Hola según muestra usa la interfaz de línea de comandos (CLI) de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1398-154">hello following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="c1398-155">En él, se crea un clúster y su contenedor y cuenta de almacenamiento dependientes mediante una llamada a una plantilla de Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="c1398-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="c1398-156">Son tooenter solicitada:</span><span class="sxs-lookup"><span data-stu-id="c1398-156">You are prompted tooenter:</span></span>
* <span data-ttu-id="c1398-157">nombre del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-157">hello cluster name.</span></span>
* <span data-ttu-id="c1398-158">contraseña de usuario del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-158">hello cluster user password.</span></span> <span data-ttu-id="c1398-159">(nombre de usuario de hello predeterminada es **administración**.)</span><span class="sxs-lookup"><span data-stu-id="c1398-159">(hello default username is **admin**.)</span></span>
* <span data-ttu-id="c1398-160">contraseña de usuario SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-160">hello SSH user password.</span></span> <span data-ttu-id="c1398-161">(nombre de usuario SSH de hello predeterminada es **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="c1398-161">(hello default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="c1398-162">Hola siguiente código proporciona los parámetros de en línea:</span><span class="sxs-lookup"><span data-stu-id="c1398-162">hello following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="c1398-163">Implementar con hello API de REST</span><span class="sxs-lookup"><span data-stu-id="c1398-163">Deploy with hello REST API</span></span>
<span data-ttu-id="c1398-164">Vea [implementar con la API de REST de hello](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="c1398-164">See [Deploy with hello REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="c1398-165">Implementación con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c1398-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="c1398-166">Usar Visual Studio toocreate un proyecto del grupo de recursos e impleméntela tooAzure a través de la interfaz de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-166">Use Visual Studio toocreate a resource group project and deploy it tooAzure through hello user interface.</span></span> <span data-ttu-id="c1398-167">Seleccionar tipo de Hola de tooinclude de recursos en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="c1398-167">You select hello type of resources tooinclude in your project.</span></span> <span data-ttu-id="c1398-168">Estos recursos se agregan automáticamente toohello plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1398-168">Those resources are automatically added toohello Resource Manager template.</span></span> <span data-ttu-id="c1398-169">proyecto de Hello también proporciona una plantilla de Hola de toodeploy de script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1398-169">hello project also provides a PowerShell script toodeploy hello template.</span></span>

<span data-ttu-id="c1398-170">Para una introducción toousing Visual Studio con grupos de recursos, consulte [crear e implementar grupos de recursos de Azure a través de Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c1398-170">For an introduction toousing Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="c1398-171">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="c1398-171">Troubleshoot</span></span>

<span data-ttu-id="c1398-172">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="c1398-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1398-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1398-173">Next steps</span></span>
<span data-ttu-id="c1398-174">En este artículo, ha aprendido varias formas toocreate un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c1398-174">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="c1398-175">toolearn más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="c1398-175">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="c1398-176">Para obtener un ejemplo de la implementación de los recursos a través de la biblioteca de cliente de .NET de hello, consulte [implementar los recursos mediante el uso de bibliotecas de .NET y una plantilla de](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1398-176">For an example of deploying resources through hello .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="c1398-177">Para ver un ejemplo en profundidad de la implementación de una aplicación, consulte [Aprovisionamiento e implementación predecibles de microservicios en Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="c1398-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="c1398-178">Para obtener instrucciones sobre la implementación de los entornos de toodifferent de solución, vea [entornos de desarrollo y prueba en Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="c1398-178">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="c1398-179">toolearn acerca de las secciones de Hola de plantilla de hello Azure Resource Manager, consulte [crear plantillas](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c1398-179">toolearn about hello sections of hello Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c1398-180">Para obtener una lista de funciones de Hola pueden usar en una plantilla de Azure Resource Manager, consulte [funciones de plantilla](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="c1398-180">For a list of hello functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a><span data-ttu-id="c1398-181">Apéndice: El Administrador de recursos plantilla toocreate un clúster de Hadoop</span><span class="sxs-lookup"><span data-stu-id="c1398-181">Appendix: Resource Manager template toocreate a Hadoop cluster</span></span>
<span data-ttu-id="c1398-182">Hello siguiente plantilla de Azure Resource Manager crea un clúster de Hadoop basados en Linux con cuenta de almacenamiento de Azure dependientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-182">hello following Azure Resource Manager template creates a Linux-based Hadoop cluster with hello dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="c1398-183">El ejemplo incluye información de configuración de la tienda de Hive y Oozie Metastore.</span><span class="sxs-lookup"><span data-stu-id="c1398-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="c1398-184">Quitar sección Hola o configurar sección Hola antes de usar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-184">Remove hello section or configure hello section before using hello template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
            "description": "hello location where all azure resources will be deployed."
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
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
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

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a><span data-ttu-id="c1398-185">Apéndice: El Administrador de recursos plantilla toocreate un clúster Spark</span><span class="sxs-lookup"><span data-stu-id="c1398-185">Appendix: Resource Manager template toocreate a Spark cluster</span></span>

<span data-ttu-id="c1398-186">Esta sección proporciona una plantilla de administrador de recursos que puede usar un clúster de HDInsight Spark toocreate.</span><span class="sxs-lookup"><span data-stu-id="c1398-186">This section provides a Resource Manager template that you can use toocreate an HDInsight Spark cluster.</span></span> <span data-ttu-id="c1398-187">Esta plantilla incluye configuraciones para `spark-defaults` y `spark-thrift-sparkconf` (para clústeres de Spark 1.6) y `spark2-defaults` y `spark2-thrift-sparkconf` (para clústeres de Spark 2).</span><span class="sxs-lookup"><span data-stu-id="c1398-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="c1398-188">Además la toothis, HDInsight calcula y establece las configuraciones como `spark.executor.instances`, `spark.executor.memory`, y `spark.executor.cores` según el tamaño del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="c1398-188">In addition toothis, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on hello cluster size.</span></span> 

<span data-ttu-id="c1398-189">Si establece un parámetro en una sección como parte de la propia plantilla hello, HDInsight no calcular y establecer Hola otros parámetros de hello misma sección.</span><span class="sxs-lookup"><span data-stu-id="c1398-189">If you set any one parameter in a section as part of hello template itself, HDInsight does not calculate and set hello other parameters of hello same section.</span></span> <span data-ttu-id="c1398-190">Por ejemplo, el parámetro `spark.executor.instances` en hello `spark-defaults` configuración.</span><span class="sxs-lookup"><span data-stu-id="c1398-190">For example, parameter `spark.executor.instances` is in hello  `spark-defaults` configuration.</span></span> <span data-ttu-id="c1398-191">Si se establece otro parámetro (por ejemplo, `spark.yarn.exector.memoryOverhead`) en hello `spark-defaults` configuración, HDInsight no calcular y establecer hello `spark.executor.instances` parámetro también.</span><span class="sxs-lookup"><span data-stu-id="c1398-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configuration, HDInsight does not calculate and set hello `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
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
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
