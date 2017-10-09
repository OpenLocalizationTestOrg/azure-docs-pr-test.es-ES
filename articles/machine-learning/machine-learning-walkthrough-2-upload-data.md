---
title: 'Paso 2: Carga de datos en un experimento de Machine Learning | Microsoft Docs'
description: "Paso 2 del programa Hola a desarrollar un tutorial de solución de predicción: carga almacena datos públicos en estudio de aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a>Paso 2 del tutorial: Carga de los datos existentes en un experimento de Aprendizaje automático de Azure
Esto es Hola segundo paso del tutorial de hello, [desarrollar una solución de análisis predictivos en aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Creación de un área de trabajo de Aprendizaje automático](machine-learning-walkthrough-1-create-ml-workspace.md)
2. **Carga de los datos existentes**
3. [Crear un experimento nuevo](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Entrenar y evaluar modelos de Hola](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Implementar el servicio Web de Hola](machine-learning-walkthrough-5-publish-web-service.md)
6. [Acceder al servicio Web Hola](machine-learning-walkthrough-6-access-web-service.md)

- - -
toodevelop un modelo de predicción de riesgo de crédito, es necesario que los datos que podemos usar tootrain y, a continuación, probar el modelo de Hola. En este tutorial, usaremos Hola "Conjunto de datos UCI Statlog (datos de crédito alemana)" desde el repositorio de aprendizaje automático de UC Irvine Hola. Puede encontrarlo aquí:   
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a>

Vamos a usar con el nombre de archivo de hello **german.data**. Descargue este archivo tooyour el disco duro local.  

Hola **german.data** conjunto de datos contiene filas de 20 variables para los solicitantes de últimas 1000 de crédito. Estas 20 variables representan Hola del conjunto de características (hello *vector de característica*), que proporciona características de identificación de los candidatos de crédito. Una columna adicional en cada fila representa el riesgo de crédito calculados del solicitante de hello, con 700 candidatos identificados como un riesgo de crédito baja y 300 como un alto riesgo.

sitio Web UCI Hola proporciona una descripción de los atributos de Hola de vector de característica de Hola para estos datos. Entre estos figuran la información financiera, el historial crediticio, el estado de empleo e información personal. A cada solicitante se le ha dado una calificación binaria para indicar si son de riesgo de crédito alto o bajo. 

Usaremos esta tootrain un modelo de predicción de análisis de datos. Cuando hayamos terminados, nuestro modelo debe ser capaz de tooaccept un vector de característica para un nuevo individuo y predecir si es un riesgo de crédito baja o alta.  

Aquí hay un giro interesante. Hola descripción del conjunto de datos de hello en menciones de sitio Web de hello UCI lo que cuesta si se misclassify riesgo del crédito de una persona.
Si el modelo Hola predice un riesgo de crédito alta para un usuario que es realmente un riesgo de crédito baja, modelo de hello ha realizado una clasificaciones incorrectas.
Pero clasificaciones incorrectas inversa de hello son cinco veces más costoso institución financiera de toohello: si el modelo de hello predice un riesgo de crédito baja para un usuario que es realmente un riesgo de crédito alta.

Por lo tanto, es deseable tootrain nuestro modelo para que el costo de Hola de este último tipo de clasificaciones incorrectas es cinco veces mayor que clasifique mal Hola otra forma.
Toodo de una manera sencilla esto al modelo de hello en nuestro experimento de entrenamiento es duplicando (cinco veces) aquellas entradas que representan una persona con un riesgo de crédito alta. A continuación, si el modelo de hello misclassifies alguien como un riesgo de crédito baja cuando están realmente un alto riesgo, modelo Hola realiza esa misma clasificaciones de incorrectas cinco veces, una vez cada duplicado. Esto aumentará el costo de Hola de este error en los resultados de la formación de Hola.


## <a name="convert-hello-dataset-format"></a>Convertir el formato de conjunto de datos de Hola
Hola de conjunto de datos original utiliza un formato separado por el espacio en blanco. Estudio de aprendizaje automático funciona mejor con un archivo de valores separados por comas (CSV), por lo que se podrá convertir el conjunto de datos de hello reemplazando los espacios con comas.  

Estos datos no hay tooconvert de muchas maneras. Una manera es mediante el uso de hello siguiente comando de Windows PowerShell:   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

Otra forma es mediante el uso de comando de sed Hola Unix:  

    sed 's/ /,/g' german.data > german.csv  

En cualquier caso, hemos creado una versión separada por comas de los datos de hello en un archivo denominado **german.csv** que podemos usar en el experimento.

## <a name="upload-hello-dataset-toomachine-learning-studio"></a>Cargar el conjunto de datos de hello tooMachine estudio de aprendizaje
Una vez datos Hola formato tooCSV convertido, necesitamos tooupload en estudio de aprendizaje automático. 

1. Página principal de estudio de aprendizaje automático de hello abierto ([https://studio.azureml.net](https://studio.azureml.net)). 

2. Haga clic en el menú de hello ![menú][1] en la esquina superior izquierda de Hola de ventana hello, haga clic en **aprendizaje automático de Azure**, seleccione **Studio**e inicie sesión.

3. Haga clic en **+ nuevo** final Hola de ventana hello.

4. Seleccione **CONJUNTO DE DATOS**.

5. Seleccione **DE ARCHIVO LOCAL**.

    ![Adición de un conjunto de datos desde un archivo local][2]

6. Hola **cargar un nuevo conjunto de datos** cuadro de diálogo, haga clic en **examinar** y buscar hello **german.csv** archivo que ha creado.

7. Escriba un nombre para el conjunto de datos de Hola. En este tutorial, lo llamaremos "UCI German Credit Card Data".

8. Para el tipo de datos, seleccione **Archivo CSV genérico sin encabezado (.nh.csv)**.

9. Agregue una descripción si así lo desea.

10. Haga clic en hello **Aceptar** marca de verificación.  

    ![Carga el conjunto de datos de Hola][3]

Esto carga los datos de hello en un módulo de conjunto de datos que podemos usar en un experimento.

Puede administrar conjuntos de datos que ha cargado tooStudio haciendo clic en hello **conjuntos de datos** toohello de pestaña a la izquierda de la ventana de hello Studio.

![Administración de conjuntos de datos][4]

Para obtener más información sobre la importación de diversos tipos de datos a un experimento, consulte [Importar datos de entrenamiento en Azure Machine Learning Studio](machine-learning-data-science-import-data.md).

**Siguiente: [Crear un experimento nuevo](machine-learning-walkthrough-3-create-new-experiment.md)**

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
