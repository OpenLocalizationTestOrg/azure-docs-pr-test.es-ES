---
title: "un modelo de aprendizaje automático de aaaRetrain | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooretrain un modelo y actualización hello Web servicio toouse Hola recién entrenado en aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a>Reciclaje de un modelo de Machine Learning
Como parte del proceso de Hola de puesta en marcha de modelos de aprendizaje automático en el aprendizaje automático de Azure, el modelo está entrenado y guardado. También, a continuación, utilizarlo toocreate un servicio Web predicative. Hola servicio Web, a continuación, puede utilizarse en sitios web, paneles y aplicaciones móviles. 

Los modelos que crea mediante Aprendizaje automático no suelen ser estáticos. Como los nuevos datos se convierte en disponibles o cuando consumidor Hola de hello API tiene su propio modelo de Hola de datos debe toobe volver a entrenar. 

El reentrenamiento puede producirse con frecuencia. Con función de la API mediante programación de reciclaje de hello, mediante programación puede que volver a entrenar modelo de hello utilizando el servicio de Web de Hola de API de reciclaje y actualización Hola con hello recién entrenado. 

Este documento describe Hola reciclaje de proceso y muestra cómo toouse Hola reciclaje API.

## <a name="why-retrain-defining-hello-problem"></a>¿Por qué volver a entrenar: definir el problema de Hola
Como parte del aprendizaje automático de hello proceso de entrenamiento, se entrena un modelo utilizando un conjunto de datos. Los modelos que crea mediante Aprendizaje automático no suelen ser estáticos. Como los nuevos datos se convierte en disponibles o cuando consumidor Hola de hello API tiene su propio modelo de Hola de datos debe toobe volver a entrenar.

En estos casos, una API de programación proporciona una manera cómoda de tooallow se o hello consumidor de su toocreate API un cliente que puede, de forma puntual o regular, volver a entrenar modelo hello mediante sus propios datos. A continuación, puede evaluar los resultados de Hola de reciclaje y actualizar hello Web servicio API toouse Hola recién entrenado.

> [!NOTE]
> Si tienes un experimento de aprendizaje existentes y el servicio Web nuevo, puede que desee toocheck out reciclaje una predicción Web existentes del servicio en lugar de la siguiente tutorial Hola mencionado en los pasos de la sección de Hola.
> 
> 

## <a name="end-to-end-workflow"></a>Flujo de trabajo de un extremo a otro
proceso de Hello implica Hola de los componentes siguientes: un experimento de entrenamiento y una predicción experimento publican como un servicio Web. tooenable reciclaje de un modelo entrenado, Hola experimento de entrenamiento debe publicarse como un servicio Web con salida de hello de un modelo entrenado. Esto permite toohello modelo de acceso de API de reciclaje. 

Hola pasos aplica tooboth nuevo y clásico servicios Web:

Crear servicio Web de predicción inicial de hello:

* Crear un experimento de entrenamiento
* Crear un experimento web predictivo
* Implementar un servicio web predictivo

Entrenar el modelo de servicio Web de hello:

* Actualizar tooallow de experimento de entrenamiento de reciclaje
* Implementar Hola reciclaje servicio web
* Usar Hola servicio de ejecución por lotes código tooretrain Hola modelo

Para ver un tutorial de hello pasos anteriores, consulte [aprendizaje automático de volver a entrenar modelos mediante programación](machine-learning-retrain-models-programmatically.md).

> [!NOTE] 
> toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola. Para obtener más información, vea [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Si ha implementado un servicio web clásico:

* Crear un nuevo extremo de servicio Web de predicción Hola
* Obtener la dirección URL de revisión de Hola y el código
* Use Hola URL PATCH toopoint Hola nuevo punto de conexión en hello volver a entrenar el modelo 

Para ver un tutorial de hello pasos anteriores, consulte [entrenar el modelo de un servicio Web clásico](machine-learning-retrain-a-classic-web-service.md).

Si experimenta dificultades reciclaje de un servicio Web clásico, consulte [solución de problemas de hello reciclaje de un servicio Web clásico de Azure Machine Learning](machine-learning-troubleshooting-retraining-models.md).

Si ha implementado un nuevo servicio web:

* Inicie sesión en tooyour cuenta de administrador de recursos de Azure
* Obtener la definición de servicio Web de Hola
* Exportar la definición del servicio Web de Hola como JSON
* Actualizar Hola referencia toohello `ilearner` blob Hola JSON
* Importar Hola JSON en una definición de servicio Web
* Actualizar el servicio Web de hello con la nueva definición del servicio Web

Para ver un tutorial de hello pasos anteriores, consulte [entrenar el modelo de un servicio Web nuevo mediante cmdlets de PowerShell de administración de aprendizaje de máquina de hello](machine-learning-retrain-new-web-service-using-powershell.md).

proceso de Hello para la configuración de reciclaje para un servicio Web clásico implica Hola pasos:

![Descripción del proceso de reentrenamiento][1]

proceso de Hello para la configuración de reciclaje para un servicio Web nuevo implica Hola pasos:

![Descripción del proceso de reentrenamiento][7]

## <a name="other-resources"></a>Otros recursos
* [Reciclaje y actualización de modelos de Azure Machine Learning con Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [Creación de varios modelos de Machine Learning y puntos de conexión de servicio web a partir de un experimento mediante PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md)
* Hola [AML reciclaje modelos utilizando API](https://www.youtube.com/watch?v=wwjglA8xllg) vídeo muestra cómo crean modelos de aprendizaje automático de tooretrain aprendizaje automático de Azure con hello las API de reciclaje y PowerShell.

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

