---
title: "Servicios web Azure Machine Learning: Implementación y consumo | Microsoft Docs"
description: Recursos para implementar y consumir servicios web.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="6c7e9-103">Servicios web Azure Machine Learning: Implementación y consumo</span><span class="sxs-lookup"><span data-stu-id="6c7e9-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="6c7e9-104">Puede usar flujos de trabajo de aprendizaje automático de aprendizaje automático de Azure toodeploy y modelos como servicios web.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-104">You can use Azure Machine Learning toodeploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="6c7e9-105">Estos servicios web, a continuación, pueden ser modelos de aprendizaje automático de hello toocall usado desde aplicaciones sobre predicciones de hello Internet toodo en tiempo real o en modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-105">These web services can then be used toocall hello machine-learning models from applications over hello Internet toodo predictions in real time or in batch mode.</span></span> <span data-ttu-id="6c7e9-106">Dado que los servicios web Hola son RESTful, puede llamarlos desde diversos lenguajes y plataformas, como .NET y Java, programación y aplicaciones, como Excel.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-106">Because hello web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="6c7e9-107">las secciones siguientes se Hola proporcionan vínculos toowalkthroughs, código y documentación toohelp ayudarán a comenzar.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-107">hello next sections provide links toowalkthroughs, code, and documentation toohelp get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="6c7e9-108">Implementación de un servicio web</span><span class="sxs-lookup"><span data-stu-id="6c7e9-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="6c7e9-109">Con Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="6c7e9-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="6c7e9-110">Estudio de aprendizaje automático y el portal de servicios Web de Microsoft Azure Machine Learning Hola ayudan a implementar y administrar un servicio web sin escribir código.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-110">Machine Learning Studio and hello Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="6c7e9-111">Hello vínculos siguientes proporcionan información general acerca de cómo toodeploy un nuevo servicio web:</span><span class="sxs-lookup"><span data-stu-id="6c7e9-111">hello following links provide general Information about how toodeploy a new web service:</span></span>

* <span data-ttu-id="6c7e9-112">Para obtener información general sobre cómo toodeploy un nuevo servicio web que se basa en el Administrador de recursos de Azure, vea [implementar un nuevo servicio web](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="6c7e9-112">For an overview about how toodeploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="6c7e9-113">Para ver un tutorial sobre cómo toodeploy un servicio web, consulte [implementar un servicio web de aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="6c7e9-113">For a walkthrough about how toodeploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="6c7e9-114">Para ver un tutorial completo sobre cómo toocreate e implementar un servicio web, consulte [tutorial paso 1: crear un área de trabajo de aprendizaje automático](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="6c7e9-114">For a full walkthrough about how toocreate and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="6c7e9-115">Para obtener ejemplos específicos de la implementación de un servicio web, consulte:</span><span class="sxs-lookup"><span data-stu-id="6c7e9-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="6c7e9-116">Tutorial paso 5: Implementar el servicio web de aprendizaje automático de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="6c7e9-116">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="6c7e9-117">Cómo toodeploy una web service toomultiple regiones</span><span class="sxs-lookup"><span data-stu-id="6c7e9-117">How toodeploy a web service toomultiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="6c7e9-118">Con API de proveedor de recursos de servicios web (API de Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="6c7e9-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="6c7e9-119">proveedor de recursos de aprendizaje automático de Azure de Hola para servicios web habilita la implementación y administración de servicios web mediante llamadas a la API de REST.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-119">hello Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="6c7e9-120">Para información más detallada, consulte la referencia [Servicio web Machine Learning (REST)](/rest/api/machinelearning/index).</span><span class="sxs-lookup"><span data-stu-id="6c7e9-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="6c7e9-121">Con cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c7e9-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="6c7e9-122">El proveedor de recursos de Azure Machine Learning para servicios web permite la implementación y administración de servicios web mediante los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="6c7e9-123">cmdlets de hello toouse, antes deben iniciar sesión en tooyour cuenta de Azure desde dentro del entorno de PowerShell de hello mediante el uso de hello [AzureRmAccount agregar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-123">toouse hello cmdlets, you must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="6c7e9-124">Si no está familiarizado con el funcionamiento de los comandos toocall PowerShell que se basan en el Administrador de recursos, consulte [con Azure PowerShell con el Administrador de recursos de Azure](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="6c7e9-124">If you are unfamiliar with how toocall PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="6c7e9-125">tooexport experimentar la predicción, use [este código de ejemplo](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="6c7e9-125">tooexport your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="6c7e9-126">Después de crear el archivo .exe de Hola desde el código de hello, puede escribir:</span><span class="sxs-lookup"><span data-stu-id="6c7e9-126">After you create hello .exe file from hello code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="6c7e9-127">Ejecuta la aplicación hello, crea una plantilla JSON de servicio web.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-127">Running hello application creates a web service JSON template.</span></span> <span data-ttu-id="6c7e9-128">toouse Hola plantilla toodeploy un servicio web, debe agregar Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="6c7e9-128">toouse hello template toodeploy a web service, you must add hello following information:</span></span>

* <span data-ttu-id="6c7e9-129">Nombre y clave de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="6c7e9-129">Storage account name and key</span></span>

    <span data-ttu-id="6c7e9-130">Puede obtener el nombre de cuenta de almacenamiento de Hola y la clave desde cualquier hello [portal de Azure](https://portal.azure.com/) o hello [portal de Azure clásico](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="6c7e9-130">You can get hello storage account name and key from either hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="6c7e9-131">Identificador del plan de compromiso</span><span class="sxs-lookup"><span data-stu-id="6c7e9-131">Commitment plan ID</span></span>

    <span data-ttu-id="6c7e9-132">Puede obtener identificador de plan de Hola de hello [servicios Web de Azure Machine Learning](https://services.azureml.net) portal inicio de sesión y haga clic en un nombre de plan.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-132">You can get hello plan ID from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="6c7e9-133">Agregar plantilla JSON toohello como elementos secundarios de hello *propiedades* nodo Hola de mismo nivel como hello *MachineLearningWorkspace* nodo.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-133">Add them toohello JSON template as children of hello *Properties* node at hello same level as hello *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="6c7e9-134">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6c7e9-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="6c7e9-135">Vea Hola siguientes artículos y código de ejemplo para obtener más detalles:</span><span class="sxs-lookup"><span data-stu-id="6c7e9-135">See hello following articles and sample code for additional details:</span></span>

* <span data-ttu-id="6c7e9-136">[cmdlets de Aprendizaje automático de Azure](https://msdn.microsoft.com/library/azure/mt767952.aspx) en MSDN</span><span class="sxs-lookup"><span data-stu-id="6c7e9-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="6c7e9-137">[Tutorial](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) de ejemplo en GitHub</span><span class="sxs-lookup"><span data-stu-id="6c7e9-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-hello-web-services"></a><span data-ttu-id="6c7e9-138">Consumir servicios web de Hola</span><span class="sxs-lookup"><span data-stu-id="6c7e9-138">Consume hello web services</span></span>
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="6c7e9-139">De hello Azure Machine Learning servicios de interfaz de usuario Web (prueba)</span><span class="sxs-lookup"><span data-stu-id="6c7e9-139">From hello Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="6c7e9-140">Puede probar el servicio web del portal de servicios Web de Azure Machine Learning Hola.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-140">You can test your web service from hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="6c7e9-141">Esto incluye pruebas de servicio de respuesta de solicitud de hello (RR) y de interfaces de servicio de ejecución por lotes (BES).</span><span class="sxs-lookup"><span data-stu-id="6c7e9-141">This includes testing hello Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="6c7e9-142">Implementación de servicios web nuevos</span><span class="sxs-lookup"><span data-stu-id="6c7e9-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="6c7e9-143">Implementar un servicio web de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="6c7e9-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="6c7e9-144">Tutorial paso 5: Implementar el servicio web de aprendizaje automático de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="6c7e9-144">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="6c7e9-145">Desde Excel</span><span class="sxs-lookup"><span data-stu-id="6c7e9-145">From Excel</span></span>
<span data-ttu-id="6c7e9-146">Puede descargar una plantilla de Excel que consume el servicio web de hello:</span><span class="sxs-lookup"><span data-stu-id="6c7e9-146">You can download an Excel template that consumes hello web service:</span></span>

* [<span data-ttu-id="6c7e9-147">Consumo de un servicio web Azure Machine Learning desde Excel</span><span class="sxs-lookup"><span data-stu-id="6c7e9-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="6c7e9-148">Complemento de Excel para Servicios web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6c7e9-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="6c7e9-149">Desde un cliente basado en REST</span><span class="sxs-lookup"><span data-stu-id="6c7e9-149">From a REST-based client</span></span>
<span data-ttu-id="6c7e9-150">Los servicios web Azure Machine Learning son API de RESTful.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="6c7e9-151">Puede utilizar estas API desde varias plataformas, como. NET, Python, R, Java, Hola etc. **Consume** página para el servicio web en hello [portal de servicios Web de Microsoft Azure Machine Learning](https://services.azureml.net) tiene ejemplo código que puede ayudarle a empezar a trabajar.</span><span class="sxs-lookup"><span data-stu-id="6c7e9-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. hello **Consume** page for your web service on hello [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="6c7e9-152">Para obtener más información, consulte [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="6c7e9-152">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
