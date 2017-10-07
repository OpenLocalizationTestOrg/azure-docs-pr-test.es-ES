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
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Servicios web Azure Machine Learning: Implementación y consumo
Puede usar flujos de trabajo de aprendizaje automático de aprendizaje automático de Azure toodeploy y modelos como servicios web. Estos servicios web, a continuación, pueden ser modelos de aprendizaje automático de hello toocall usado desde aplicaciones sobre predicciones de hello Internet toodo en tiempo real o en modo por lotes. Dado que los servicios web Hola son RESTful, puede llamarlos desde diversos lenguajes y plataformas, como .NET y Java, programación y aplicaciones, como Excel.

las secciones siguientes se Hola proporcionan vínculos toowalkthroughs, código y documentación toohelp ayudarán a comenzar.

## <a name="deploy-a-web-service"></a>Implementación de un servicio web
### <a name="with-azure-machine-learning-studio"></a>Con Azure Machine Learning Studio
Estudio de aprendizaje automático y el portal de servicios Web de Microsoft Azure Machine Learning Hola ayudan a implementar y administrar un servicio web sin escribir código.

Hello vínculos siguientes proporcionan información general acerca de cómo toodeploy un nuevo servicio web:

* Para obtener información general sobre cómo toodeploy un nuevo servicio web que se basa en el Administrador de recursos de Azure, vea [implementar un nuevo servicio web](machine-learning-webservice-deploy-a-web-service.md).
* Para ver un tutorial sobre cómo toodeploy un servicio web, consulte [implementar un servicio web de aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md).
* Para ver un tutorial completo sobre cómo toocreate e implementar un servicio web, consulte [tutorial paso 1: crear un área de trabajo de aprendizaje automático](machine-learning-walkthrough-1-create-ml-workspace.md).
* Para obtener ejemplos específicos de la implementación de un servicio web, consulte:

  * [Tutorial paso 5: Implementar el servicio web de aprendizaje automático de Azure de Hola](machine-learning-walkthrough-5-publish-web-service.md)
  * [Cómo toodeploy una web service toomultiple regiones](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>Con API de proveedor de recursos de servicios web (API de Azure Resource Manager)
proveedor de recursos de aprendizaje automático de Azure de Hola para servicios web habilita la implementación y administración de servicios web mediante llamadas a la API de REST. Para información más detallada, consulte la referencia [Servicio web Machine Learning (REST)](/rest/api/machinelearning/index).

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>Con cmdlets de PowerShell
El proveedor de recursos de Azure Machine Learning para servicios web permite la implementación y administración de servicios web mediante los cmdlets de PowerShell.

cmdlets de hello toouse, antes deben iniciar sesión en tooyour cuenta de Azure desde dentro del entorno de PowerShell de hello mediante el uso de hello [AzureRmAccount agregar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. Si no está familiarizado con el funcionamiento de los comandos toocall PowerShell que se basan en el Administrador de recursos, consulte [con Azure PowerShell con el Administrador de recursos de Azure](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

tooexport experimentar la predicción, use [este código de ejemplo](https://github.com/ritwik20/AzureML-WebServices). Después de crear el archivo .exe de Hola desde el código de hello, puede escribir:

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Ejecuta la aplicación hello, crea una plantilla JSON de servicio web. toouse Hola plantilla toodeploy un servicio web, debe agregar Hola siguiente información:

* Nombre y clave de la cuenta de almacenamiento

    Puede obtener el nombre de cuenta de almacenamiento de Hola y la clave desde cualquier hello [portal de Azure](https://portal.azure.com/) o hello [portal de Azure clásico](http://manage.windowsazure.com/).
* Identificador del plan de compromiso

    Puede obtener identificador de plan de Hola de hello [servicios Web de Azure Machine Learning](https://services.azureml.net) portal inicio de sesión y haga clic en un nombre de plan.

Agregar plantilla JSON toohello como elementos secundarios de hello *propiedades* nodo Hola de mismo nivel como hello *MachineLearningWorkspace* nodo.

Este es un ejemplo:

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

Vea Hola siguientes artículos y código de ejemplo para obtener más detalles:

* [cmdlets de Aprendizaje automático de Azure](https://msdn.microsoft.com/library/azure/mt767952.aspx) en MSDN
* [Tutorial](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) de ejemplo en GitHub

## <a name="consume-hello-web-services"></a>Consumir servicios web de Hola
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a>De hello Azure Machine Learning servicios de interfaz de usuario Web (prueba)
Puede probar el servicio web del portal de servicios Web de Azure Machine Learning Hola. Esto incluye pruebas de servicio de respuesta de solicitud de hello (RR) y de interfaces de servicio de ejecución por lotes (BES).

* [Implementación de servicios web nuevos](machine-learning-webservice-deploy-a-web-service.md)
* [Implementar un servicio web de Aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md)
* [Tutorial paso 5: Implementar el servicio web de aprendizaje automático de Azure de Hola](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>Desde Excel
Puede descargar una plantilla de Excel que consume el servicio web de hello:

* [Consumo de un servicio web Azure Machine Learning desde Excel](machine-learning-consuming-from-excel.md)
* [Complemento de Excel para Servicios web Azure Machine Learning](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>Desde un cliente basado en REST
Los servicios web Azure Machine Learning son API de RESTful. Puede utilizar estas API desde varias plataformas, como. NET, Python, R, Java, Hola etc. **Consume** página para el servicio web en hello [portal de servicios Web de Microsoft Azure Machine Learning](https://services.azureml.net) tiene ejemplo código que puede ayudarle a empezar a trabajar. Para obtener más información, consulte [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).
