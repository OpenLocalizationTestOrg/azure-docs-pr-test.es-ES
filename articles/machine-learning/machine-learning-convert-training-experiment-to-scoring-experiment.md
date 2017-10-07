---
title: "aaaHow tooprepare el modelo para la implementación en estudio de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Cómo tooprepare el modelo entrenado para la implementación como un servidor web service mediante la conversión de la formación de estudio de aprendizaje automático experimentar tooa predictivo experimento."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: garye
ms.openlocfilehash: d25bc68be63679a803bfc24a9e29e009a9263f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprepare-your-model-for-deployment-in-azure-machine-learning-studio"></a>Cómo tooprepare el modelo para la implementación en estudio de aprendizaje automático de Azure

Azure deja de estudio de aprendizaje automático que Hola herramientas que necesita toodevelop un modelo de análisis predictivo y, a continuación, hacer operativa mediante la implementación como un servicio web de Azure.

toodo esto, utilice Studio toocreate un experimento - llama un *experimento de entrenamiento* : donde entrenar, puntuación y editar el modelo. Cuando esté satisfecho, obtener su toodeploy listo del modelo mediante la conversión de su tooa de experimento de entrenamiento *experimento predictivo* que configuró tooscore datos de usuario.

Puede ver un ejemplo de este proceso en [Tutorial: Desarrollo de una solución de análisis predictivo para la evaluación del riesgo de crédito en Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

Este artículo le profundización en los detalles de Hola de cómo un experimento de entrenamiento se convierte en un experimento de predicción y cómo se implementa ese experimento de predicción. Al comprender estos detalles, puede obtener información sobre cómo tooconfigure su toomake modelo implementado lo más eficaz.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Información general 

proceso de Hola de convertir un experimento de entrenamiento experimento tooa predictivo implica tres pasos:

1. Reemplace máquina Hola módulos algoritmo con el modelo entrenado de aprendizaje.
2. Recortar Hola experimento tooonly los módulos que se necesitan para puntuar. Un experimento de entrenamiento incluye un número de módulos que son necesarios para el entrenamiento, pero no son necesarios cuando se entrena el modelo de Hola.
3. Definir cómo va a aceptar su modelo de datos de usuario del servicio web hello y qué datos se devolverán.

> [!TIP]
> En el experimento de entrenamiento, se ha interesado por el entrenamiento y la puntuación del modelo con la utilización de datos propios. Pero una vez implementado, los usuarios enviarán nuevo modelo de datos tooyour y devolverá los resultados de predicción. Por lo tanto, como para convertir su tooget de experimento predictivo tooa de experimento de entrenamiento está listo para la implementación, tenga en cuenta cómo se utilizarán modelo Hola por otros usuarios.
> 
> 

## <a name="set-up-web-service-button"></a>Botón Configurar servicio web
Después de ejecutar el experimento (haga clic en **ejecutar** final Hola del lienzo del experimento de hello), haga clic en hello **configurar el servicio de Web** botón (seleccione hello **predictivo servicio Web** opción). **Configurar el servicio de Web** lleva a cabo para Hola tres pasos de convertir el experimento de entrenamiento experimento tooa predicción:

1. Guarda el modelo entrenado en hello **modelos entrenados** sección de la paleta de módulo de hello (toohello a la izquierda del lienzo del experimento de hello). A continuación, reemplaza el algoritmo de aprendizaje de máquina de Hola y [entrenar modelo] [ train-model] módulos con hello guarda entrenados modelo.
2. Analiza el experimento y quita los módulos que ya se han usado solo para entrenamiento y que ya no son necesarios.
3. Inserta los módulos de _Entrada de servicio web_ y _Salida de servicio web_ en las ubicaciones predeterminadas del experimento (estos módulos aceptan y devuelven datos de usuario).

Por ejemplo, siguiente Hola experimentar trenes de un modelo de árbol de decisión impulsado de dos clases con datos del censo de ejemplo:

![experimento de entrenamiento][figure1]

módulos de Hello en este experimento llevan a cabo básicamente cuatro funciones diferentes:

![Funciones del módulo][figure2]

Al convertir este experimento de entrenamiento experimento tooa predictivo, algunos de estos módulos ya no son necesarios o ahora un propósito diferente:

* **Datos** -datos de hello en este conjunto de datos de ejemplo no se usa durante la puntuación: usuario Hola del servicio web de hello proporcionará hello toobe de datos con puntuación. Sin embargo, los metadatos de Hola desde este conjunto de datos, tales como tipos de datos, se usan por modelo entrenado Hola. Por ello, debe tookeep Hola conjunto de datos en el experimento de predicción de Hola para que pueda ofrecer estos metadatos.

* **Preparar el** , según los datos de usuario de Hola que se van a enviar para puntuar, estos módulos pueden o no ser necesario tooprocess los datos entrantes Hola. Hola **configurar el servicio de Web** botón no toque a estos: necesita toodecide cómo desea toohandle ellos.
  
    Por ejemplo, en este ejemplo de conjunto de datos de ejemplo de Hola puede tener valores que faltan, por lo que un [limpiar datos que faltan] [ clean-missing-data] módulo estaba incluido toodeal con ellos. Además, conjunto de datos de ejemplo de Hola incluye columnas que no son necesarios tootrain modelo de Hola. Por lo tanto un [seleccionar columnas de conjunto de datos] [ select-columns] módulo fue tooexclude incluye las columnas adicionales de Hola flujo de datos. Si sabe que se van a enviar para puntuar datos Hola a través de hello, servicio web no tendrán valores que faltan, puede quitar hello [limpiar datos que faltan] [ clean-missing-data] módulo. Sin embargo, puesto que de Hola [seleccionar columnas de conjunto de datos] [ select-columns] módulo le ayuda a definir Hola columnas de datos espera que entrenado hello, ese módulo debe tooremain.

* **Entrenar** -estos módulos son modelos de hello tootrain usado. Al hacer clic en **configurar el servicio de Web**, estos módulos se reemplazan con un solo módulo que contiene el modelo de hello realizar el entrenamiento. Este nuevo módulo se guarda en hello **modelos entrenados** sección de la paleta de módulo de Hola.

* **Puntuación** : en este ejemplo, hello [dividir datos] [ split] módulo es flujo de datos de uso toodivide hello en los datos de prueba y datos de entrenamiento. En el experimento de predicción de hello, nos estamos no entrenamiento, ya lo [dividir datos] [ split] se puede quitar. De forma similar, en segundo lugar Hola [puntuar modelo] [ score-model] hello y módulo [evaluar modelo] [ evaluate-model] módulo toocompare usado de resultados de prueba de Hola datos, por lo que estos módulos no son necesitan en hello predictivo experimentar. Hola restantes [puntuar modelo] [ score-model] módulo, sin embargo, es necesario tooreturn un resultado de puntuación a través del servicio web Hola.

Este es el aspecto de nuestro ejemplo después de hacer clic en **Configurar servicio web**:

![Experimento predictivo convertido][figure3]

Hola trabajo realizado por **configurar el servicio de Web** puede ser suficiente tooprepare su toobe experimento implementado como un servicio web. Sin embargo, puede que desee toodo algunos experimento tooyour específico de un trabajo adicional.

### <a name="adjust-input-and-output-modules"></a>Ajustar los módulos de entrada y salida
En el experimento de entrenamiento, usa un conjunto de datos de entrenamiento y, a continuación, ha Hola algunos tooget de procesamiento de datos en un formulario que Hola algoritmo de aprendizaje de máquina necesarios. Si los datos de hello esperados tooreceive a través del servicio web hello no necesitará este procesamiento, puede omitirlo: conectar la salida de hello de hello **el módulo de entrada de servicio Web** tooa módulo diferente en el experimento. datos del usuario de Hello ahora llegarán en el modelo de hello en esta ubicación.

Por ejemplo, de forma predeterminada **configurar el servicio de Web** coloca hello **Web proporcionados por el servicio** módulo en la parte superior de Hola de su flujo de datos, como se muestra en figura Hola anterior. Pero podemos posicionar manualmente hello **Web proporcionados por el servicio** más allá de los módulos de procesamiento de datos de hello:

![Entrada de servicio de web Hola móvil][figure4]

Hola datos de entrada proporcionado a través de hello web servicio ahora pasará directamente en el módulo de modelo de puntuación de hello sin ningún procesamiento previo.

De forma similar, de forma predeterminada **configurar el servicio de Web** coloca Hola módulo de salida de servicio Web final Hola de su flujo de datos. En este ejemplo, el servicio web de hello devolverá toohello salida de hello de usuario del programa Hola a [puntuar modelo] [ score-model] módulo, que incluye vector de datos de entrada completa de Hola y Hola resultados de puntuación.
Sin embargo, si prefiere tooreturn algo diferente, a continuación, puede agregar módulos adicionales antes de hello **Web resultado del servicio** módulo. 

Por ejemplo, tooreturn solo Hola los resultados de puntuación y no Hola todo vector de datos de entrada, agregar un [seleccionar columnas de conjunto de datos] [ select-columns] tooexclude módulo todas las columnas excepto Hola resultados de puntuación. A continuación, mueva hello **Web resultado del servicio** toohello salida del módulo de hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo. el experimento de Hello tiene el siguiente aspecto:

![Mover el resultado del servicio web Hola][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a>Agregar o quitar módulos de procesamiento de datos adicionales
Si hay más módulos en el experimento de los que sabe que se necesitarán durante la puntuación, se pueden eliminar. Por ejemplo, debido a que se mueve hello **Web proporcionados por el servicio** tooa módulo señalar después hello módulos de procesamiento de datos, se puede eliminar hello [limpiar datos que faltan] [ clean-missing-data] módulo desde la experimento de predicción de Hola.

Nuestro experimento predictivo tiene ahora el siguiente aspecto:

![Eliminación de módulos adicionales][figure6]


### <a name="add-optional-web-service-parameters"></a>Agregar parámetros de servicio web opcionales
En algunos casos, puede que desee tooallow usuario de Hola de su comportamiento de hello web toochange de servicio de los módulos cuando se tiene acceso al servicio de Hola. *Parámetros de servicio Web* le permiten toodo esto.

Un ejemplo común es configurar un [importar datos] [ import-data] módulo por lo que usuario Hola de hello implementa el servicio web puede especificar un origen de datos diferente cuando se accede al servicio web de Hola. También puede configurar el módulo [Exportar datos][export-data] para que se pueda especificar un destino diferente.

Puede definir parámetros de servicio web y asociarlos con uno o más parámetros de módulo, y puede especificar si son obligatorios u opcionales. usuario de Hello del servicio web de hello proporciona valores para estos parámetros cuando se tiene acceso al servicio de Hola y acciones de módulo de Hola se modifican en consecuencia.

Para obtener más información acerca de los parámetros de servicio Web y cómo toouse, vea [utilizando parámetros de servicio de Web de Azure Machine Learning][webserviceparameters].

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-hello-predictive-experiment-as-a-web-service"></a>Implementar experimento predictivo Hola como un servicio web
Ahora que se ha preparado suficientemente experimento predictivo hello, puede implementarlo como un servicio web de Azure. Con el servicio web de hello, los usuarios pueden enviar tooyour modelo de datos y modelo de hello devolverá las predicciones.

Para obtener más información sobre el proceso de implementación completa de hello, consulte [implementar un servicio web de aprendizaje automático de Azure][deploy]

[deploy]: machine-learning-publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
