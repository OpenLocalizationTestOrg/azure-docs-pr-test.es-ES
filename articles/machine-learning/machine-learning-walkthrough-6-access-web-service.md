---
title: "Paso 6: Acceder al servicio Web de aprendizaje de máquina Hola | Documentos de Microsoft"
description: "Paso 6 del programa Hola a desarrollar un solución de predicción Tutorial: obtener acceso a un servicio Web de aprendizaje de máquina de Azure activo."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a>Tutorial paso 6: Hola de acceso servicio web de aprendizaje automático de Azure

Éste es Hola último paso del tutorial de hello, [desarrollar una solución de análisis predictivos en aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Creación de un área de trabajo de Aprendizaje automático](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Carga de los datos existentes](machine-learning-walkthrough-2-upload-data.md)
3. [Crear un experimento nuevo](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Entrenar y evaluar modelos de Hola](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Implementar el servicio Web de Hola](machine-learning-walkthrough-5-publish-web-service.md)
6. **Acceder al servicio Web Hola**

- - -
En el paso anterior de hello en este tutorial se implementa un servicio web que usa nuestro modelo de predicción de riesgo de crédito. Ahora los usuarios son toosend capaz de datos tooit y reciban los resultados. 

Hola servicio Web es un servicio web de Azure que puede recibir y devolver datos mediante las API de REST de una de dos maneras:  

* **Solicitud/respuesta** : usuario Hola envía uno o más filas de crédito toohello de datos de servicio mediante un protocolo HTTP y Hola servicio responde con uno o varios conjuntos de resultados.
* **Ejecución por lotes** : usuario Hola almacena uno o más filas de datos de crédito en un Azure blob y, a continuación, envía el servicio de toohello de ubicación de blob de Hola. puntuaciones de servicio de Hello que todas las filas de datos de Hola Hola blob de entrada, almacenes de hello da como resultado otro blob y devuelve Hola dirección URL de ese contenedor.  

Hola tooaccess de manera más rápida y sencilla un servicio web de clásico es a través de hello [Azure ML solicitudes y respuestas Web del servicio de aplicaciones](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) o [plantilla de aplicación Web de Azure ML lote ejecución servicio](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).

Estas plantillas de aplicación web pueden compilar una aplicación web personalizada que reconoce los datos de entrada del servicio web y lo que devolverá. Todo lo que necesita toodo es proporcionar datos y servicio web de acceso tooyour y plantilla de Hola Hola rest.

Para obtener más información sobre el uso de plantillas de aplicación web de hello, consulte [consumir un servicio Web de aprendizaje de máquina de Azure con una plantilla de aplicación web](machine-learning-consume-web-service-with-web-app-template.md).

También puede desarrollar un servicio web de aplicación personalizada tooaccess hello mediante código de inicio que se proporcionan en R, C# y lenguajes de programación Python.

Puede encontrar detalles completos en [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).

