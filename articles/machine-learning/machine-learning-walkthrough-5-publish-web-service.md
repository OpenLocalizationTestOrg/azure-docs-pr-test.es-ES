---
title: "Paso 5: Implementar el servicio web de aprendizaje automático de hello | Documentos de Microsoft"
description: "Paso 5 de hello desarrollar un solución de predicción Tutorial: implementar un experimento de predicción en estudio de aprendizaje automático como un servicio web."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a>Tutorial paso 5: Implementar el servicio web de aprendizaje automático de Azure de Hola
Esto es Hola quinto paso del tutorial de hello, [desarrollar una solución de análisis predictivos en aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Creación de un área de trabajo de Aprendizaje automático](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Carga de los datos existentes](machine-learning-walkthrough-2-upload-data.md)
3. [Crear un experimento nuevo](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Entrenar y evaluar modelos de Hola](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. **Implementar el servicio web de Hola**
6. [Servicio web de acceso Hola](machine-learning-walkthrough-6-access-web-service.md)

- - -
toogive otros una ocasión toouse Hola modelo predictivo, hemos desarrollado en este tutorial, nos podemos implementarlo como un servicio web en Azure.

Toothis punto hemos sido experimentar con nuestro modelo de entrenamiento. Pero los servicio Hola implementado ya no queda toodo entrenamiento; será necesario toogenerate nuevas predicciones por entradas de usuario de hello según nuestro modelo de puntuación. Por lo que vamos a toodo algunos tooconvert preparación esto experimentar de un ***entrenamiento*** experimentar tooa ***predictivo*** experimentar. 

Se trata de un proceso de tres pasos:  

1. Quite uno de los modelos de Hola
2. Convertir hello *experimento de entrenamiento* hemos creado en un *experimento predictivo*
3. Implementar experimento predictivo Hola como un servicio web

## <a name="remove-one-of-hello-models"></a>Quite uno de los modelos de Hola

En primer lugar, necesitamos tootrim este experimento hacia abajo un poco. Actualmente tenemos dos modelos distintos en el experimento de hello, pero solamente queremos toouse un modelo cuando esto se implementa como un servicio web.  

Supongamos que hemos decidido ese modelo de árbol de hello impulsado realiza un rendimiento mejor que el modelo SVM de Hola. Por lo que Hola primera cosa toodo es quitar hello [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] módulo y módulos de Hola que se utilizaron para entrenar a él. Puede que desee toomake una copia del experimento de hello en primer lugar, haga clic en **Guardar como** final Hola de hello experimentar el lienzo.

Necesitamos hello toodelete siguientes módulos:  

* [Two-Class Support Vector Machine][two-class-support-vector-machine] (Máquina de vectores de soporte de dos clases)
* [Entrenar modelo] [ train-model] y [puntuar modelo] [ score-model] módulos que estaban conectado tooit
* [Normalize Data][normalize-data] (Normalizar datos) (ambos)
* [Evaluar el modelo de] [ evaluate-model] (porque se haya terminado de evaluación de modelos de hello)

Seleccione cada módulo y presione la tecla SUPR de Hola o un módulo de Hola de menú contextual y seleccione **eliminar**. 

![Quita el modelo SVM de Hola][3a]

Nuestro modelo debería tener ahora un aspecto similar al siguiente:

![Quita el modelo SVM de Hola][3]

Ahora estamos listo toodeploy esto modelados con hello [árbol de decisión impulsado de dos clases][two-class-boosted-decision-tree].

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Convertir el experimento de predicción de hello entrenamiento experimento tooa

tooget este modelo listo para la implementación, necesitamos tooconvert este experimento tooa predictivo experimento de entrenamiento. Esto implica tres pasos:

1. Guardar el modelo de Hola se ha entrenado y, a continuación, reemplace nuestros módulos de entrenamiento
2. Módulos de tooremove de experimento de Hola que eran necesarios únicamente para el entrenamiento de recorte
3. Definir donde va a Aceptar proporcionados por el servicio web de Hola y donde genera la salida de hello

Podríamos hacer esto manualmente, pero afortunadamente, los tres pasos pueden realizarse haciendo clic en **configurar el servicio de Web** final Hola del lienzo del experimento de hello (y seleccionando hello **predictivo servicio Web** opción).

> [!TIP]
> Si desea obtener más detalles sobre lo que ocurre cuando se convierte un tooa de experimento de entrenamiento predictivo experimentar, consulte [cómo tooprepare el modelo para la implementación en estudio de aprendizaje automático de Azure](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Al hacer clic en **Set Up Web Service**(Configurar servicio web), pasa lo siguiente:

* Hola entrenado es convertido tooa único **entrenado** módulo y almacenan en hello módulo paleta toohello izquierda de hello experimentar lienzo (puede encontrar en **modelos entrenados**)
* Se quitan los módulos que se utilizaron para el entrenamiento, en particular:
  * [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Árbol de decisión ampliado de dos clases)
  * [Train Model][train-model] (Entrenar modelo)
  * [Split Data][split] (Dividir datos)
  * en segundo lugar Hola [ejecutar Script de R] [ execute-r-script] módulo que se usa para los datos de prueba
* modelo entrenado Hola guardado se agrega en el experimento de Hola
* **Entrada de servicio de Web** y **Web resultado del servicio** módulos se agregan (identifican donde los datos del usuario de hello introducirá modelo hello, así como qué datos se devuelven cuando se accede al servicio web de hello)

> [!NOTE]
> Puede ver que el experimento de Hola se guarda en dos partes en pestañas que se han agregado en parte superior de hello del lienzo del experimento de Hola. Hello experimento de entrenamiento original está en la ficha de hello **experimento de entrenamiento**, y Hola recién creado experimento predictivo está por debajo del **experimento predictivo**. experimento predictivo Hello es hello uno que se implementará como un servicio web.

Es necesario un paso adicional tootake con este experimento determinado.
Hemos agregado dos [ejecutar Script de R] [ execute-r-script] tooprovide módulos una ponderación función toohello datos. Que era simplemente un truco que necesitábamos para el entrenamiento y pruebas, por lo que podemos realizar out esos módulos en el modelo final Hola.
Estudio de aprendizaje automático quitado uno [ejecutar Script de R] [ execute-r-script] módulo cuando quita hello [división] [ split] módulo. Ahora podemos quitar Hola sí y conectar [Editor de metadatos] [ metadata-editor] directamente demasiado[puntuar modelo][score-model].    

Nuestro experimento debería tener ahora un aspecto similar al siguiente:  

![La puntuación del modelo entrenado Hola][4]  

> [!NOTE]
> Quizás se pregunte por qué se deja el conjunto de datos de tarjeta de crédito de alemán de UCI de Hola en experimento predictivo Hola. servicio de Hello va datos del usuario de tooscore hello, no Hola conjunto de datos original, por lo tanto ¿por qué dejar Hola conjunto de datos original en hello modelo?
> 
> Es cierto que servicio hello no necesita datos de tarjeta de crédito originales Hola. Pero debe esquema Hola de esos datos, que incluye información como el número de columnas hay y qué columnas son numéricos. Esta información de esquema es datos del usuario de hello toointerpret necesarios. Se deje estos componentes conectados para que hello puntuación módulo tiene esquema de conjunto de datos de hello cuando se está ejecutando el servicio de Hola. no se usan datos de Hello, solo el esquema de Hola.  
> 
> 

Ejecute el experimento de hello una última vez (haga clic en **ejecutar**.) Si desea tooverify que Hola modelo sigue funcionando, haga clic en salida de hello de hello [puntuar modelo] [ score-model] módulo y seleccione **ver los resultados de**. Puede ver que se muestran los datos originales de hello, junto con el valor de riesgo de crédito de hello ("etiquetas con puntuación") y Hola la puntuación del valor de probabilidad ("puntúan probabilidades".) 

## <a name="deploy-hello-web-service"></a>Implementar el servicio web de Hola
Puede implementar Hola experimento como un servicio web de clásico o como un nuevo servicio web que se basa en el Administrador de recursos de Azure.

### <a name="deploy-as-a-classic-web-service"></a>Implementación como servicio web clásico
toodeploy un clásico web servicio derivado de nuestro experimento, haga clic en **implementar el servicio de Web** por debajo de hello lienzo y seleccione **implementar servicio Web [estándar]**. Estudio de aprendizaje automático implementa Hola experimento como un servicio web y le toohello panel para ese servicio web. Desde esta página puede devolver toohello experimento (**ver instantánea** o **ver más reciente**) y ejecutar una prueba sencilla del servicio web de hello (vea **probar el servicio web de hello** a continuación). También hay información aquí para crear aplicaciones que pueden tener acceso a los servicio web de hello (más que en el paso siguiente de Hola de este tutorial).

![Panel del servicio web][6]

Puede configurar el servicio de hello haciendo clic en hello **configuración** ficha. Aquí puede modificar el nombre del servicio hello (es nombre de experimento Hola determinado de forma predeterminada) y escriba una descripción. También se pueden proporcionar más etiquetas descriptivas Hola datos de entrada y salida.  

![Configurar el servicio web de Hola][5]  

### <a name="deploy-as-a-new-web-service"></a>Implementación como servicio web nuevo

> [!NOTE] 
> toodeploy un nuevo servicio web debe tener permisos suficientes en hello toowhich de suscripción que va a implementar Hola servicio web. Para obtener más información, consulte [administrar un servicio web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

toodeploy un nuevo servicio web se deriva de nuestro experimento:

1. Haga clic en **implementar el servicio de Web** por debajo de hello lienzo y seleccione **implementar [New] servicio Web**. Estudio de aprendizaje automático transfiere los servicios web de aprendizaje automático de Azure de toohello **implementar experimento** página.

2. Escriba un nombre para el servicio web de Hola. 

3. Para **Plan de precios**, puede seleccionar un plan de precios existente o seleccione "Crear nuevo" y conceda a Hola de nuevo plan de un nombre y una opción de plan mensual de hello select. plan de Hello niveles predeterminados toohello planes para la región predeterminada y el servicio web está implementado toothat región.

4. Haga clic en **Implementar**.

Después de unos minutos, Hola **inicio rápido** se abre la página para el servicio web.

Puede configurar el servicio de hello haciendo clic en hello **configurar** ficha. Aquí puede modificar el servicio de hello título y escriba una descripción. 

Hola tootest servicio web, haga clic en hello **prueba** pestaña (vea **probar el servicio web de hello** a continuación). Para obtener información sobre cómo crear aplicaciones que pueden tener acceso a los servicio web de hello, haga clic en hello **Consume** pestaña (paso siguiente de hello en este tutorial entrarán en más detalle).

> [!TIP]
> Puede actualizar el servicio web de hello una vez que haya implementado. Por ejemplo, si desea toochange el modelo, a continuación, puede editar el experimento de entrenamiento de Hola, ajustar los parámetros del modelo hello y haga clic en **implementar el servicio de Web**, seleccione **implementar servicio Web [estándar]** o  **Implementar el servicio Web [New]**. Cuando implemente el experimento de Hola de nuevo, reemplaza el servicio web de hello, ahora con el modelo actualizado.  
> 
> 

## <a name="test-hello-web-service"></a>Servicio web de Hola de prueba

Cuando se accede al servicio web de hello, datos del usuario de hello entra a través de hello **Web proporcionados por el servicio** módulo donde ha pasado toohello [puntuar modelo] [ score-model] módulo y puntuación. forma de Hello que hemos configurado experimento predictivo hello, modelo de hello espera datos en el mismo formato que el conjunto de datos de riesgo de crédito original de Hola de Hola.
se devuelven resultados de Hola de toohello usuario de servicio web de Hola a través de hello **Web resultado del servicio** módulo.

> [!TIP]
> forma de Hello tenemos Hola predictivo experimento configurado, Hola todo da como resultado de hello [puntuar modelo] [ score-model] módulo se devuelven. Esto incluye todos los datos de entrada de hello más valores de riesgo de crédito de Hola y Hola la puntuación de probabilidad. Pero puede devolver algo distinto si desea; por ejemplo, podría devolver solamente el valor de riesgo del crédito de Hola. toodo, inserte un [proyectar columnas] [ project-columns] módulo entre [puntuar modelo] [ score-model] hello y **Web resultado del servicio** columnas tooeliminate que no desea Hola tooreturn de servicio web. 
> 
> 

Puede probar un servidor web estándar de servicio en **estudio de aprendizaje automático** o en hello **servicios Web de Azure Machine Learning** portal.
Puede probar un nuevo servicio web solo en hello **servicios Web de aprendizaje de máquina** portal.

> [!TIP]
> Al realizar pruebas en el portal de servicios Web de Azure Machine Learning hello, puede tener portal Hola crear datos de ejemplo que puede usar tootest Hola respuesta de solicitud de servicio. En hello **configurar** , seleccione "Sí" para **habilitado de datos de ejemplo?**. Cuando se abre la pestaña de hello solicitudes y respuestas de hello **prueba** página, portal de hello rellena los datos de ejemplo tomados de conjunto de datos de riesgo de crédito original de Hola.

### <a name="test-a-classic-web-service"></a>Prueba de un servicio web clásico

Puede probar un servicio web de clásico en estudio de aprendizaje automático o en el portal de servicios Web de aprendizaje de máquina de Hola. 

#### <a name="test-in-machine-learning-studio"></a>Prueba en Machine Learning Studio

1. En hello **panel** página de servicio web de hello, haga clic en hello **prueba** situado bajo **punto de conexión predeterminado**. Un cuadro de diálogo aparece y le pide de datos de entrada de hello para el servicio de Hola. Estos es Hola mismas columnas que aparecían en el conjunto de datos de riesgo de crédito original de Hola.  

2. Escriba un conjunto de datos y haga clic en **Aceptar**. 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a>Probar en el portal de servicios Web de aprendizaje de máquina de Hola

1. En hello **panel** página de servicio web de hello, haga clic en hello **vista previa de prueba** vincular en **punto de conexión predeterminado**. página de prueba de Hello en el portal de servicios Web de Azure Machine Learning hello para el extremo del servicio web Hola se abre y le pide de datos de entrada de hello para el servicio de Hola. Estos es Hola mismas columnas que aparecían en el conjunto de datos de riesgo de crédito original de Hola.

2. Haga clic en **Test Request-Response** (Probar solicitud-respuesta). 

### <a name="test-a-new-web-service"></a>Prueba de un servicio web nuevo

Puede probar un nuevo servicio web solo en el portal de servicios Web de aprendizaje de máquina de Hola.

1. Hola [servicios Web de Azure Machine Learning](https://services.azureml.net/quickstart) portal, haga clic en **prueba** al principio de Hola de página de Hola. Hola **prueba** se abre la página y puede escribir datos de servicio de Hola. campos de entrada de Hello mostrados corresponden columnas toohello que aparecían en el conjunto de datos de riesgo de crédito original de Hola. 

2. Escriba un conjunto de datos y, después, haga clic en **Test Request-Response**(Probar solicitud-respuesta).

Hola se muestran resultados de prueba de hello en lado derecho de Hola de página de hello en la columna de salida de hello. 


## <a name="manage-hello-web-service"></a>Administrar el servicio web de Hola

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a>Administrar un servicio web de clásico en hello portal de Azure clásico

Una vez haya implementado el servicio web de clásico, puede administrar de hello [portal de Azure clásico](https://manage.windowsazure.com).

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com)
2. En el panel de servicios de Microsoft Azure hello, haga clic en **aprendizaje automático**
3. Haga clic en el área de trabajo.
4. Haga clic en hello **servicios Web** ficha
5. Haga clic en el servicio web de hello creamos
6. Haga clic en el punto de conexión de Hola "predeterminado"

Desde aquí, puede hacer cosas como supervisar cómo realiza el servicio web de Hola y realizar ajustes de rendimiento cambiando el número de llamadas concurrentes Hola servicio puede controlar.

Para obtener información, consulte:

* [Creación de extremos](machine-learning-create-endpoint.md)
* [Escalado del servicio web](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a>Administrar un nuevo servicio web en el portal de servicios Web de Azure Machine Learning Hola o clásico

Una vez haya implementado el servicio web, ya sea clásico o nueva, se puede administrar desde hello [servicios Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portal.

rendimiento de hello toomonitor del servicio web:

1. Inicie sesión en toohello [servicios Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portal
2. Haga clic en **Servicios web**.
3. Haga clic en el servicio web.
4. Haga clic en hello **panel**

- - -
**Siguiente: [acceder al servicio web Hola](machine-learning-walkthrough-6-access-web-service.md)**

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
