---
title: "aaaRetrain un servicio web de aprendizaje automático de Azure nuevo con PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprogrammatically volver a entrenar un modelo y actualización hello web servicio toouse Hola recién entrenado en aprendizaje automático de Azure con los cmdlets de PowerShell de administración de aprendizaje de máquina de Hola."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="bdc94-103">Entrenar el modelo de un servicio web de nuevo en función de administrador de recursos con los cmdlets de PowerShell de administración de aprendizaje de máquina de Hola</span><span class="sxs-lookup"><span data-stu-id="bdc94-103">Retrain a New Resource Manager based web service using hello Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="bdc94-104">Al entrenar el modelo de un servicio web nuevo, se actualiza hello web predictivo servicio definición tooreference Hola nuevo modelo entrenado.</span><span class="sxs-lookup"><span data-stu-id="bdc94-104">When you retrain a New web service, you update hello predictive web service definition tooreference hello new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="bdc94-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bdc94-105">Prerequisites</span></span>
<span data-ttu-id="bdc94-106">Debe configurar un experimento de entrenamiento y predictivo tal como se muestra en los [modelos de reciclaje de Machine Learning mediante programación](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="bdc94-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bdc94-107">experimento predictivo Hola debe implementarse como una máquina de Azure Resource Manager (nuevo) en función, servicio web de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="bdc94-107">hello predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="bdc94-108">toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdc94-108">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="bdc94-109">Para obtener más información, consulte [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="bdc94-109">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="bdc94-110">Para obtener más información sobre la implementación de servicios web, vea el artículo sobre [implementación de un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="bdc94-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="bdc94-111">Este proceso requiere que haya instalado Hola Cmdlets de aprendizaje de máquina de Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc94-111">This process requires that you have installed hello Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="bdc94-112">Para obtener información de instalación de cmdlets de aprendizaje automático de hello, vea hello [Cmdlets de Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) referencia en MSDN.</span><span class="sxs-lookup"><span data-stu-id="bdc94-112">For information installing hello Machine Learning cmdlets, see hello [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="bdc94-113">Hola copiada siguiendo la información de hello reciclaje salida:</span><span class="sxs-lookup"><span data-stu-id="bdc94-113">Copied hello following information from hello retraining output:</span></span>

* <span data-ttu-id="bdc94-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="bdc94-114">BaseLocation</span></span>
* <span data-ttu-id="bdc94-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="bdc94-115">RelativeLocation</span></span>

<span data-ttu-id="bdc94-116">pasos de Hello que necesarios son:</span><span class="sxs-lookup"><span data-stu-id="bdc94-116">hello steps you take are:</span></span>

1. <span data-ttu-id="bdc94-117">Inicie sesión en tooyour cuenta de administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc94-117">Sign in tooyour Azure Resource Manager account.</span></span>
2. <span data-ttu-id="bdc94-118">Obtener la definición de servicio web de Hola</span><span class="sxs-lookup"><span data-stu-id="bdc94-118">Get hello web service definition</span></span>
3. <span data-ttu-id="bdc94-119">Exportar la definición del servicio Web de Hola como JSON</span><span class="sxs-lookup"><span data-stu-id="bdc94-119">Export hello Web Service Definition as JSON</span></span>
4. <span data-ttu-id="bdc94-120">Actualizar el blob de hello referencia toohello ilearner Hola JSON.</span><span class="sxs-lookup"><span data-stu-id="bdc94-120">Update hello reference toohello ilearner blob in hello JSON.</span></span>
5. <span data-ttu-id="bdc94-121">Importar Hola JSON en una definición de servicio Web</span><span class="sxs-lookup"><span data-stu-id="bdc94-121">Import hello JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="bdc94-122">Actualizar el servicio web de hello con la nueva definición del servicio Web</span><span class="sxs-lookup"><span data-stu-id="bdc94-122">Update hello web service with new Web Service Definition</span></span>

## <a name="sign-in-tooyour-azure-resource-manager-account"></a><span data-ttu-id="bdc94-123">Inicie sesión en tooyour cuenta de administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="bdc94-123">Sign in tooyour Azure Resource Manager account</span></span>
<span data-ttu-id="bdc94-124">En primer lugar debe iniciar sesión en la cuenta de Azure desde dentro del entorno de PowerShell de hello mediante hello tooyour [AzureRmAccount agregar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdc94-124">You must first sign in tooyour Azure account from within hello PowerShell environment using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition"></a><span data-ttu-id="bdc94-125">Obtener Hola definición del servicio Web</span><span class="sxs-lookup"><span data-stu-id="bdc94-125">Get hello Web Service Definition</span></span>
<span data-ttu-id="bdc94-126">A continuación, obtener Hola servicio Web por llamada hello [AzureRmMlWebService Get](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdc94-126">Next, get hello Web Service by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="bdc94-127">Hola definición del servicio Web es una representación interna de entrenado Hola del servicio web de hello y no es modificable directamente.</span><span class="sxs-lookup"><span data-stu-id="bdc94-127">hello Web Service Definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="bdc94-128">Asegúrese de que está recuperando Hola definición del servicio Web para el experimento de predicción y no el experimento de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="bdc94-128">Make sure that you are retrieving hello Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="bdc94-129">toodetermine el nombre de grupo de recursos de Hola de un servicio web existente, ejecute el cmdlet de Get-AzureRmMlWebService de hello sin ningún servicio web de parámetros toodisplay hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="bdc94-129">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="bdc94-130">Busque el servicio web de hello y, a continuación, examine su identificador de servicio web.</span><span class="sxs-lookup"><span data-stu-id="bdc94-130">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="bdc94-131">nombre de Hola Hola del grupo de recursos es el cuarto elemento de hello en el identificador hello, justo después de hello *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="bdc94-131">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="bdc94-132">En el siguiente ejemplo de Hola, nombre del grupo de recursos de hello es SouthCentralUS de MachineLearning de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bdc94-132">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="bdc94-133">O bien, toodetermine Hola nombre grupo de recursos de un servicio web existente, el portal de servicios Web de Microsoft Azure Machine Learning toohello de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="bdc94-133">Alternatively, toodetermine hello resource group name of an existing web service, log on toohello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="bdc94-134">Seleccione el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdc94-134">Select hello web service.</span></span> <span data-ttu-id="bdc94-135">nombre del grupo de recursos de Hello es quinto elemento de Hola de hello URL del servicio web de hello, justo después de hello *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="bdc94-135">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="bdc94-136">En el siguiente ejemplo de Hola, nombre del grupo de recursos de hello es SouthCentralUS de MachineLearning de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bdc94-136">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a><span data-ttu-id="bdc94-137">Exportar la definición del servicio Web de Hola como JSON</span><span class="sxs-lookup"><span data-stu-id="bdc94-137">Export hello Web Service Definition as JSON</span></span>
<span data-ttu-id="bdc94-138">toomodify Hola definición toohello entrenar modelo toouse recién Hola entrenado, primero debe usar hello [AzureRmMlWebService de exportación](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport de cmdlet tooa archivo de formato JSON.</span><span class="sxs-lookup"><span data-stu-id="bdc94-138">toomodify hello definition toohello trained model toouse hello newly Trained Model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a><span data-ttu-id="bdc94-139">Actualizar el blob de hello referencia toohello ilearner Hola JSON.</span><span class="sxs-lookup"><span data-stu-id="bdc94-139">Update hello reference toohello ilearner blob in hello JSON.</span></span>
<span data-ttu-id="bdc94-140">En los activos de hello, busque Hola [entrenado], actualización hello *uri* valor Hola *locationInfo* nodo con hello URI de blob de hello ilearner.</span><span class="sxs-lookup"><span data-stu-id="bdc94-140">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="bdc94-141">Hello URI generado por la combinación de hello *BaseLocation* hello y *RelativeLocation* de salida de hello de hello llamada reconversión BES.</span><span class="sxs-lookup"><span data-stu-id="bdc94-141">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span> <span data-ttu-id="bdc94-142">Esto actualiza Hola ruta de acceso tooreference Hola nuevo modelo entrenado.</span><span class="sxs-lookup"><span data-stu-id="bdc94-142">This updates hello path tooreference hello new trained model.</span></span>

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition"></a><span data-ttu-id="bdc94-143">Importar Hola JSON en una definición de servicio Web</span><span class="sxs-lookup"><span data-stu-id="bdc94-143">Import hello JSON into a Web Service Definition</span></span>
<span data-ttu-id="bdc94-144">Debe usar hello [AzureRmMlWebService de importación](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Hola modifica el archivo JSON en una definición de servicio Web que se puede usar tooupdate Hola definición del servicio Web.</span><span class="sxs-lookup"><span data-stu-id="bdc94-144">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition that you can use tooupdate hello Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a><span data-ttu-id="bdc94-145">Actualizar el servicio web de hello con la nueva definición del servicio Web</span><span class="sxs-lookup"><span data-stu-id="bdc94-145">Update hello web service with new Web Service Definition</span></span>
<span data-ttu-id="bdc94-146">Por último, utilice [AzureRmMlWebService actualización](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate Hola definición del servicio Web.</span><span class="sxs-lookup"><span data-stu-id="bdc94-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="bdc94-147">Resumen</span><span class="sxs-lookup"><span data-stu-id="bdc94-147">Summary</span></span>
<span data-ttu-id="bdc94-148">Con los cmdlets de administración de PowerShell de aprendizaje de máquina de hello, puede actualizar entrenado Hola de un servicio Web predictivos que permite escenarios como:</span><span class="sxs-lookup"><span data-stu-id="bdc94-148">Using hello Machine Learning PowerShell management cmdlets, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="bdc94-149">Reentrenamiento de modelos periódicos con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="bdc94-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="bdc94-150">Distribución de un modelo toocustomers con el objetivo de Hola de lo que permite volver a entrenar modelo hello mediante sus propios datos.</span><span class="sxs-lookup"><span data-stu-id="bdc94-150">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

