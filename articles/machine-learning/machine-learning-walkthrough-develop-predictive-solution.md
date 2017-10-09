---
title: "solución de predicción aaaA de riesgo de crédito con aprendizaje automático | Documentos de Microsoft"
description: "Un tutorial detallado que muestra cómo toocreate una solución de análisis predictivos de crédito evaluación de riesgos en estudio de aprendizaje automático de Azure."
keywords: "riesgo de crédito, solución de análisis predictivo, evaluación de riesgos"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a>Tutorial: Desarrollo de una solución de análisis predictiva para la evaluación del riesgo de crédito en Aprendizaje automático de Azure

En este tutorial, echamos un vistazo extendido en proceso de Hola de desarrollar una solución de análisis predictivos en estudio de aprendizaje automático. Se desarrolla un modelo simple estudio de aprendizaje automático y, a continuación, implementarlo como un servicio web de aprendizaje automático de Azure donde modelo Hola puede realizar predicciones con los nuevos datos. 

En este tutorial, se presupone que usó Machine Learning Studio con anterioridad al menos una vez y que tiene ciertos conocimientos sobre los conceptos de aprendizaje automático. Pero no se asume de que sea un experto.

Si nunca ha utilizado **estudio de aprendizaje automático de Azure** antes, puede querer toostart con el tutorial de hello, [crear su primer ciencia de datos experimentar en estudio de aprendizaje automático de Azure](machine-learning-create-experiment.md). Este tutorial le guiará por estudio de aprendizaje automático para hello primera vez. Muestra conceptos básicos de Hola de módulos de cómo toodrag y colocar en el experimento, conéctelos, ejecute el experimento de Hola y examine los resultados de Hola. Otra herramienta que puede resultar útil para obtener una introducción es un diagrama que ofrezca una visión general de las capacidades de Hola de estudio de aprendizaje automático. Puede descargarlo e imprimirlo desde aquí: [Diagrama de información general de las funcionalidades de Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
 
Si es nuevo campo toohello de máquina de aprendizaje en general, hay una serie de vídeos que podría ser útil tooyou. Se llama [ciencia de datos para principiantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) y puede ofrecerle un aprendizaje de toomachine introducción excelente utilizando lenguaje cotidiano y conceptos.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a>problema de Hola

Supongamos que necesita toopredict riesgo del crédito de un individuo en función de información de Hola que le proporcionaron en una solicitud de crédito.  

La evaluación de riesgos de un crédito es un problema complejo, pero podemos simplificarlo un poco para usarlo en este tutorial. La usaremos como ejemplo de cómo puede crear una solución de análisis predictivo con Microsoft Azure Machine Learning. toodo, utilizamos estudio de aprendizaje automático de Azure y un servicio web de aprendizaje automático.  

## <a name="hello-solution"></a>solución de Hola

En este detallado tutorial, comenzamos con datos de riesgo de crédito y desarrollaremos y entrenaremos un modelo predictivo según esos datos. A continuación, implementamos modelo Hola como un servicio web para que pueda usar por otros usuarios para la evaluación del riesgo de crédito.

toocreate esta solución de evaluación del riesgo de crédito, se siguen estos pasos:  

1. [Creación de un área de trabajo de Aprendizaje automático](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Carga de los datos existentes](machine-learning-walkthrough-2-upload-data.md)
3. [Creación de un experimento](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Entrenar y evaluar modelos de Hola](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Implementar el servicio web de Hola](machine-learning-walkthrough-5-publish-web-service.md)
6. [Servicio web de acceso Hola](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> Puede encontrar una copia de trabajo del experimento de Hola que desarrollamos en este tutorial Hola [Cortana Intelligence galería](https://gallery.cortanaintelligence.com). Vaya demasiado**[Tutorial: predicción de riesgo de crédito](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  y haga clic en **abierta en Studio** toodownload una copia del experimento de hello en el área de trabajo de estudio de aprendizaje automático.
> 
> En este tutorial se basa en una versión simplificada del experimento de ejemplo de Hola, [clasificación binaria: predicción de riesgo de crédito](http://go.microsoft.com/fwlink/?LinkID=525270), que también están disponibles en hello [galería](http://gallery.cortanaintelligence.com/).
