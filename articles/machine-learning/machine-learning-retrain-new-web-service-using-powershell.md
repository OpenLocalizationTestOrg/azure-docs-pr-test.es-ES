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
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a>Entrenar el modelo de un servicio web de nuevo en función de administrador de recursos con los cmdlets de PowerShell de administración de aprendizaje de máquina de Hola
Al entrenar el modelo de un servicio web nuevo, se actualiza hello web predictivo servicio definición tooreference Hola nuevo modelo entrenado.  

## <a name="prerequisites"></a>Requisitos previos
Debe configurar un experimento de entrenamiento y predictivo tal como se muestra en los [modelos de reciclaje de Machine Learning mediante programación](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> experimento predictivo Hola debe implementarse como una máquina de Azure Resource Manager (nuevo) en función, servicio web de aprendizaje. toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola. Para obtener más información, consulte [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Para obtener más información sobre la implementación de servicios web, vea el artículo sobre [implementación de un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

Este proceso requiere que haya instalado Hola Cmdlets de aprendizaje de máquina de Azure. Para obtener información de instalación de cmdlets de aprendizaje automático de hello, vea hello [Cmdlets de Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) referencia en MSDN.

Hola copiada siguiendo la información de hello reciclaje salida:

* BaseLocation
* RelativeLocation

pasos de Hello que necesarios son:

1. Inicie sesión en tooyour cuenta de administrador de recursos de Azure.
2. Obtener la definición de servicio web de Hola
3. Exportar la definición del servicio Web de Hola como JSON
4. Actualizar el blob de hello referencia toohello ilearner Hola JSON.
5. Importar Hola JSON en una definición de servicio Web
6. Actualizar el servicio web de hello con la nueva definición del servicio Web

## <a name="sign-in-tooyour-azure-resource-manager-account"></a>Inicie sesión en tooyour cuenta de administrador de recursos de Azure
En primer lugar debe iniciar sesión en la cuenta de Azure desde dentro del entorno de PowerShell de hello mediante hello tooyour [AzureRmAccount agregar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

## <a name="get-hello-web-service-definition"></a>Obtener Hola definición del servicio Web
A continuación, obtener Hola servicio Web por llamada hello [AzureRmMlWebService Get](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. Hola definición del servicio Web es una representación interna de entrenado Hola del servicio web de hello y no es modificable directamente. Asegúrese de que está recuperando Hola definición del servicio Web para el experimento de predicción y no el experimento de entrenamiento.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine el nombre de grupo de recursos de Hola de un servicio web existente, ejecute el cmdlet de Get-AzureRmMlWebService de hello sin ningún servicio web de parámetros toodisplay hello en su suscripción. Busque el servicio web de hello y, a continuación, examine su identificador de servicio web. nombre de Hola Hola del grupo de recursos es el cuarto elemento de hello en el identificador hello, justo después de hello *resourceGroups* elemento. En el siguiente ejemplo de Hola, nombre del grupo de recursos de hello es SouthCentralUS de MachineLearning de forma predeterminada.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

O bien, toodetermine Hola nombre grupo de recursos de un servicio web existente, el portal de servicios Web de Microsoft Azure Machine Learning toohello de inicio de sesión. Seleccione el servicio web de Hola. nombre del grupo de recursos de Hello es quinto elemento de Hola de hello URL del servicio web de hello, justo después de hello *resourceGroups* elemento. En el siguiente ejemplo de Hola, nombre del grupo de recursos de hello es SouthCentralUS de MachineLearning de forma predeterminada.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a>Exportar la definición del servicio Web de Hola como JSON
toomodify Hola definición toohello entrenar modelo toouse recién Hola entrenado, primero debe usar hello [AzureRmMlWebService de exportación](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport de cmdlet tooa archivo de formato JSON.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a>Actualizar el blob de hello referencia toohello ilearner Hola JSON.
En los activos de hello, busque Hola [entrenado], actualización hello *uri* valor Hola *locationInfo* nodo con hello URI de blob de hello ilearner. Hello URI generado por la combinación de hello *BaseLocation* hello y *RelativeLocation* de salida de hello de hello llamada reconversión BES. Esto actualiza Hola ruta de acceso tooreference Hola nuevo modelo entrenado.

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

## <a name="import-hello-json-into-a-web-service-definition"></a>Importar Hola JSON en una definición de servicio Web
Debe usar hello [AzureRmMlWebService de importación](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Hola modifica el archivo JSON en una definición de servicio Web que se puede usar tooupdate Hola definición del servicio Web.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a>Actualizar el servicio web de hello con la nueva definición del servicio Web
Por último, utilice [AzureRmMlWebService actualización](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate Hola definición del servicio Web.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a>Resumen
Con los cmdlets de administración de PowerShell de aprendizaje de máquina de hello, puede actualizar entrenado Hola de un servicio Web predictivos que permite escenarios como:

* Reentrenamiento de modelos periódicos con nuevos datos.
* Distribución de un modelo toocustomers con el objetivo de Hola de lo que permite volver a entrenar modelo hello mediante sus propios datos.

