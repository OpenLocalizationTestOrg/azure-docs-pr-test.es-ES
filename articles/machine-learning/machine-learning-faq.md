---
title: "aaaAzure aprendizaje automático con frecuencia preguntas frecuentes (P+f) | Documentos de Microsoft"
description: "Introducción a Aprendizaje automático Azure: preguntas más frecuentes sobre facturación, capacidades y limitaciones de un servicio de nube para un modelado de predicción optimizado."
keywords: "introducción de aprendizaje automático, modelo predictivo, qué es el aprendizaje automático"
services: machine-learning
documentationcenter: 
author: garyericson
manager: paulettm
editor: cgronlun
ms.assetid: a4a32a06-dbed-4727-a857-c10da774ce66
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 3af84451dde064c3c9520ee520b541128b1eef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-frequently-asked-questions-billing-capabilities-limitations-and-support"></a>Preguntas más frecuentes sobre Azure Machine Learning: facturación, funcionalidades, limitaciones y soporte técnico
Estas son algunas de las preguntas más frecuentes (P+F) y las respuestas correspondientes sobre Azure Machine Learning, un servicio en la nube para el desarrollo de modelos predictivos y la aplicación de soluciones mediante servicios web. Estas preguntas más frecuentes proporcionan preguntas acerca de cómo toouse Hola servicio, que incluye Hola modelo, las capacidades, limitaciones y soporte técnico de facturación.

**¿Tiene una pregunta que no se encuentra aquí?**

Aprendizaje automático de Azure tiene un foro en MSDN donde los miembros de la Comunidad de ciencia de datos de hello pueden formular alguna pregunta sobre aprendizaje automático de Azure. equipo de aprendizaje automático de Azure Hola supervisa foro Hola. Vaya toohello [foro de aprendizaje de máquina de Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toosearch para respuestas o toopost una pregunta nueva.

## <a name="general-questions"></a>Preguntas generales
**¿Qué es el Aprendizaje automático de Azure?**

Aprendizaje automático de Azure es un servicio completamente administrado que puede usar toocreate, probar, operar y administrar soluciones analíticas predictivas en nube de Hola. Con solo un explorador, puede iniciar sesión, cargar datos y comenzar rápidamente experimentos de aprendizaje automático. Un modelo predictivo basado en la funcionalidad de arrastrar y soltar, una gran paleta de módulos y una biblioteca de plantillas de inicio convierten las tareas de aprendizaje automático comunes en algo sencillo y rápido. Para obtener más información, vea hello [Introducción al servicio de aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/). Para el aprendizaje de toomachine introducción que explica los conceptos y terminología clave, consulte [tooAzure de introducción de aprendizaje automático](machine-learning-what-is-machine-learning.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**¿Qué es Estudio de aprendizaje automático?**

Machine Learning Studio es un entorno de trabajo al que se puede acceder mediante un explorador web. Estudio de aprendizaje automático hospeda un palet de módulos en una interfaz de composición visual que le ayuda a crear un extremo a otro, el flujo de trabajo de ciencia de datos en forma de Hola de un experimento.

Para más información sobre Estudio de aprendizaje automático, consulte [¿Qué es Estudio de aprendizaje automático de Azure?](machine-learning-what-is-ml-studio.md)

**¿Qué es el servicio de API de aprendizaje de máquina de hello?**

Hola servicio API de aprendizaje de máquina permite toodeploy modelos de predicción, como los que están integradas en estudio de aprendizaje automático, como servicios web escalable, tolerante. servicios web de Hola que crea el servicio de la API de aprendizaje de máquina de hello son las API de REST que proporcionan una interfaz para la comunicación entre aplicaciones externas y sus modelos de análisis predictivos.

Para obtener más información, consulte [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).

**¿Dónde se muestran mis servicios web clásicos? ¿Dónde se muestran mis nuevos servicios web basados Azure Resource Manager?**

Servicios Web creados mediante Hola clásico implementación modelo y los servicios web creados mediante el modelo de implementación del nuevo administrador de recursos de Azure de Hola se enumeran en hello [servicios Web de Microsoft Azure Machine Learning](https://services.azureml.net/) portal.

También se enumeran los servicios web clásico en [estudio de aprendizaje automático](http://studio.azureml.net) en hello **servicios Web** ficha.

## <a name="azure-machine-learning-questions"></a>Preguntas sobre Azure Machine Learning
**¿Qué son los servicios web Azure Machine Learning?**

Los servicios web Machine Learning proporcionan una interfaz entre una aplicación y un modelo de puntuación de flujo de trabajo de Machine Learning. Una aplicación externa puede utilizar toocommunicate de aprendizaje automático de Azure con un modelo de puntuación de flujo de trabajo de aprendizaje automático en tiempo real. Un servicio web de aprendizaje automático de llamada tooa devuelve aplicación externa de tooan de resultados de predicción. toomake un servicio web de tooa de llamada, se pasa una clave de API que se creó cuando implementó el servicio web de Hola. Un servicio web Machine Learning se basa en REST, una conocida opción de arquitectura para proyectos de programación web.

Azure Machine Learning tiene dos tipos de servicios web:

* Servicio de respuesta de solicitud (RR): Una latencia baja, servicio altamente escalable que proporciona una interfaz toohello modelos sin estado creado e implementado mediante el uso de estudio de aprendizaje automático.
* Servicio de ejecución por lotes (BES): servicio asincrónico que puntúa un lote de registros de datos.

Hay varias maneras de tooconsume Hola API de REST de servicio y acceso hello web. Por ejemplo, puede escribir una aplicación en C#, R o Python mediante código de ejemplo de Hola que se genera automáticamente cuando implementa el servicio web de Hola.

código de ejemplo de Hola está disponible en:
- Hola usar página de hello servicio web en el portal de servicios Web de Azure Machine Learning Hola
- Página de Ayuda de la API de Hello en el panel de servicio web de hello en estudio de aprendizaje automático

También puede utilizar el libro de Microsoft Excel de ejemplo de Hola que se crea automáticamente y está disponible en el panel de servicio web de hello en estudio de aprendizaje automático.

**¿Qué Hola actualizaciones principales tooAzure aprendizaje automático?**

Actualizaciones más recientes de hello, consulte [What's new aprendizaje automático de Azure](machine-learning-whats-new.md).

## <a name="machine-learning-studio-questions"></a>Preguntas sobre Estudio de aprendizaje automático
### <a name="import-and-export-data-for-machine-learning"></a>Importación y exportación de datos en Machine Learning
**¿Qué orígenes de datos admite Aprendizaje automático?**

Puede descargar datos tooa experimentación de estudio de aprendizaje automático de tres maneras:

- Cargar un archivo local como un conjunto de datos
- Utilizar datos tooimport módulo de servicios de datos en la nube
- Importar un conjunto de datos guardado de otro experimento

toolearn Obtenga más información sobre formatos de archivo compatibles, consulte [importar datos de entrenamiento en estudio de aprendizaje automático](machine-learning-data-science-import-data.md).

#### <a id="ModuleLimit"></a>¿El tamaño puede ser el conjunto de datos de Hola para mi módulos?
Módulos de estudio de aprendizaje automático admiten conjuntos de datos de seguridad too10 GB de datos numéricos densos para casos de uso comunes. Si un módulo toma más de una entrada, hello 10 GB valor es Hola total de tamaños de todas las entradas. También puede realizar el muestreo de conjuntos de datos grandes mediante consultas de Hive o Azure SQL Database, o usar el procesamiento previo de aprendizaje por recuentos antes de la ingesta.  

Hello siguientes tipos de datos puede expandir los conjuntos de datos de toolarger durante la normalización de características y están limitados que no requiere herramientas de 10 GB:

* Dispersos
* Categorías
* Cadenas
* Datos binarios

Hola siguiendo los módulos es limitados toodatasets menor que 10 GB:

* Módulos de recomendación.
* Módulo Synthetic Minority Oversampling Technique (SMOTE)
* Módulos de script: R, Python y SQL
* Módulos donde el tamaño de los datos de la salida de hello pueden ser mayores que el tamaño de datos de entrada, como Join o hash de características
* La validación cruzada, optimizar Hiperparámetros de modelo, la regresión Ordinal y Multiclase uno contra todos, cuando Hola número de iteraciones es demasiado grande

#### <a id="UploadLimit"></a>¿Cuáles son los límites de Hola para datos carga?
Para conjuntos de datos mayores de GB de un par, cargar datos tooAzure almacenamiento o base de datos de SQL Azure, o usar HDInsight de Azure en lugar de que se cargan directamente desde un archivo local.

**¿Se pueden leer datos de Amazon S3?**

Si tiene una pequeña cantidad de datos y desea tooexpose a través de una dirección URL HTTP; a continuación, puede usar hello [importar datos] [ import-data] módulo. Para grandes cantidades de datos, transferirla tooAzure almacenamiento primero y, a continuación, usar hello [importar datos] [ import-data] toobring de módulo en el experimento.
<!--

<SEE CLOUD DS PROCESS>
-->

**¿Hay una capacidad integrada para usar una entrada de imagen?**

Puede obtener información acerca de la capacidad de entrada de imagen en hello [importar imágenes] [ image-reader] referencia.

### <a name="modules"></a>Módulos
**Hola algoritmo, origen de datos, formato de datos o la operación de transformación de datos que busco no está en estudio de aprendizaje automático de Azure. ¿Qué opciones tengo?**

Puede ir toohello [foro de comentarios de usuario](http://go.microsoft.com/fwlink/?LinkId=404231) toosee característica solicita que estamos haciendo un seguimiento. Agregue la solicitud de tooa de voto si ya se ha solicitado una capacidad que está buscando. Si no existe la capacidad de Hola que está buscando, cree una nueva solicitud. Puede ver estado de saludo de la solicitud en este foro demasiado. Se esta lista a un seguimiento detallado y actualizar estado de Hola de disponibilidad de las características con frecuencia. Además, puede utilizar la compatibilidad integrada de Hola para R y Python toocreate transformaciones personalizadas cuando sea necesario.

**¿Puedo usar mi código existente en Estudio de aprendizaje automático?**

Sí, puede hacer que el código existente de R o Python en estudio de aprendizaje automático, ejecútelo en hello mismo experimentar con aprendices de aprendizaje automático de Azure e implementar soluciones de Hola como un servicio web a través de aprendizaje automático de Azure. Para más información, consulte [Extender el experimento con R](machine-learning-extend-your-experiment-with-r.md) y [Ejecución de scripts de Machine Learning de Python en Azure Machine Learning Studio](machine-learning-execute-python-scripts.md).

**¿Es posible toouse un resultado similar [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) toodefine un modelo?**

No, no se admite el lenguaje de marcado de modelos de predicción (PMML). Puede usar R personalizado y toodefine un módulo de código de Python.

**¿Cuántos módulos puedo ejecutar en paralelo en mi experimento?**  

Puede ejecutar los módulos de toofour en paralelo en un experimento.

### <a name="data-processing"></a>Procesamiento de datos
**¿Hay un dato de toovisualize de capacidad (más allá de visualizaciones de R) interactivamente en el experimento de hello?**

Haga clic en la salida de hello de un módulo toovisualize Hola de datos y obtener las estadísticas.

**Al obtener una vista previa de resultados o datos en un explorador, el número de Hola de filas y columnas está limitado. ¿Por qué?**

Dado que pueden enviarse el explorador tooa grandes cantidades de datos, tamaño de los datos es limitado tooprevent ralentizar estudio de aprendizaje automático. toovisualize todos Hola/resultados de los datos, es mejor toodownload Hola datos y usar Excel u otra herramienta.

### <a name="algorithms"></a>Algoritmos
**¿Qué algoritmos existentes se admiten en Machine Learning Studio?**

Machine Learning Studio ofrece los algoritmos mas innovadores, como árboles de decisión incrementados escalables, sistemas de recomendaciones bayesianas, redes neuronales profundas y selvas de decisión, que se han desarrollado en Microsoft Research. También se incluyen paquetes de aprendizaje automático escalables de código abierto, como Vowpal Wabbit. Estudio de aprendizaje automático admite algoritmos de aprendizaje automático para clasificación, regresión y agrupación en clústeres y binarias y multiclase. Vea la lista completa de Hola de [módulos de aprendizaje de máquina][machine-learning-modules].

**¿Usted sugiera automáticamente Hola derecho toouse de algoritmo de aprendizaje automático para Mis datos?**

No, pero estudio de aprendizaje automático tiene varias maneras de resultados de hello toocompare de cada algoritmo toodetermine Hola uno adecuado para su problema.

**¿Tienen las instrucciones en un algoritmo de selección sobre otro para los algoritmos de hello proporcionado?**

Vea [cómo toochoose un algoritmo](machine-learning-algorithm-choice.md).

**¿Algoritmos de hello proporciona escritos en R o Python?**

No, estos algoritmos se escriben principalmente lenguajes compilados tooprovide mejorar el rendimiento.

**¿Son los detalles de los algoritmos de hello proporcionados?**

Hola documentación proporciona información acerca de los algoritmos de Hola y parámetros para la optimización son algoritmo de hello toooptimize descrito para su uso.  

**¿Se admite el aprendizaje en línea?**

No. Actualmente solo se admite el reentrenamiento mediante programación.

**¿Se puede visualizar las capas de Hola de un modelo de red neuronal mediante Hola integrados módulo?**

No.

**¿Puedo crear mis propios módulos en C# o algún otro lenguaje?**

Actualmente, sólo se pueden utilizar módulos personalizados de R toocreate nuevos.

### <a name="r-module"></a>Módulo R
**¿Qué paquetes de R están disponibles en Estudio de aprendizaje automático?**

Estudio de aprendizaje automático admite más de 400 paquetes de CRAN R hoy en día, y aquí es hello [lista actual](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) todos incluidos paquetes. Consulte también [ampliar su experimento con R](machine-learning-extend-your-experiment-with-r.md) toolearn cómo tooretrieve esta lista usted mismo. Si el paquete de Hola que desea no está en esta lista, proporcione el nombre de Hola de paquete de hello en hello [foro de comentarios de usuario](http://go.microsoft.com/fwlink/?LinkId=404231).

**¿Es posible toobuild a R personalizado módulo?**

Sí. Para más información, consulte [Creación de módulos R personalizados en Azure Machine Learning](machine-learning-custom-r-modules.md).

**¿Hay un entorno de REPL para R?**

No, no hay ningún entorno de lectura Eval-Print-bucle (REPL) para R en studio Hola.

### <a name="python-module"></a>Módulo de Python
**¿Es posible toobuild un módulo personalizado de Python?**

No actualmente, pero se pueden usar uno o varios [ejecutar Script de Python] [ python] tooget módulos Hola el mismo resultado.

**¿Hay un entorno de REPL para Python?**

Puede utilizar blocs de notas de Jupyter de hello en estudio de aprendizaje automático. Para más información, consulte [Introducing Jupyter Notebooks in Azure Machine Learning Studio](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)(Introducción a Jupyter Notebooks en Estudio de aprendizaje automático de Azure).

## <a name="web-service"></a>Servicio web
### <a name="retrain"></a>Reentrenar el modelo
**¿Cómo reentreno los modelos de Azure Machine Learning mediante programación?**

Usar hello reciclaje API. Para obtener más información, consulte [Volver a entrenar modelos de aprendizaje automático mediante programación](machine-learning-retrain-models-programmatically.md). Ejemplo de código también está disponible en hello [demostración de reciclaje de aprendizaje de Microsoft Azure máquina](https://azuremlretrain.codeplex.com/).

### <a name="create"></a>Crear
**¿Puedo implementar modelo Hola localmente o en una aplicación que no tiene una conexión a Internet?**

No.

**¿Cabe esperar una latencia de línea de base para todos los servicios web?**

Vea hello [límites de suscripción de Azure](../azure-subscription-service-limits.md).

### <a name="use"></a>Uso
**¿Cuándo podría ser necesario toorun mi modelo predictivo como un servicio de ejecución por lotes frente a un servicio de respuesta de solicitud?**

Hola servicio de respuesta de solicitud (RR) es una latencia baja, modelos de servicio web de gran escala que se usa tooprovide un toostateless de interfaz que se crean y se implementan a partir de entorno de experimentación de Hola. Hola servicio de ejecución por lotes (BES) es un servicio que puntúa un lote de registros de datos de forma asincrónica. Hola para BES es de entrada como entrada de datos que utiliza registros de recursos. Hola principal diferencia es que BES lee un bloque de registros desde una variedad de orígenes, como almacenamiento de blobs de Azure, almacenamiento de tabla de Azure, base de datos de SQL Azure, HDInsight (consulta de hive) y orígenes HTTP. Para obtener más información, consulte [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).

**¿Cómo se puede actualizar modelo Hola para servicio web de hello implementado?**

tooupdate un modelo de predicción para un servicio ya implementado, modificar y volver a ejecutar el experimento de Hola que usa tooauthor y Guardar modelo entrenado Hola. Una vez que una nueva versión de hello entrenado disponible, estudio de aprendizaje automático le pregunta si desea tooupdate su servicio web. Para obtener más información acerca de cómo tooupdate un servicio web implementado, vea [implementar un servicio web de aprendizaje automático](machine-learning-publish-a-machine-learning-web-service.md).

También puede usar hello Retraining API.
Para obtener más información, consulte [Volver a entrenar modelos de aprendizaje automático mediante programación](machine-learning-retrain-models-programmatically.md). Ejemplo de código también está disponible en hello [demostración de reciclaje de aprendizaje de Microsoft Azure máquina](https://azuremlretrain.codeplex.com/).

**¿Cómo se supervisa el servicio web implementado en producción?**

Después de implementar un modelo de predicción, también puede supervisar desde hello Azure clásico portal (solo para servicios web estándar) o el portal de servicios Web de Azure Machine Learning de Hola. Cada servicio implementado cuenta con su propio panel, donde se puede ver la información de supervisión de ese servicio. Para obtener más información acerca de cómo toomanage los servicios web implementados, consulte [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md) y [administrar un área de trabajo de aprendizaje automático de Azure](machine-learning-manage-workspace.md).

**¿Hay un lugar dónde puedo ver la salida de hello de mi RR/BES?**

RR, respuesta del servicio web Hola normalmente es donde verá resultados Hola. También puede escribirlo tooAzure el almacenamiento de blobs. Para BES, salida de hello se escribe tooa blob de forma predeterminada. También puede escribir la tabla o base de datos de tooa de salida de hello mediante hello [exportar datos] [ export-data] módulo.

**¿Solamente puedo crear servicios web a partir de modelos creados en Machine Learning Studio?**

No. También puede crear servicios web directamente desde Jupyter Notebooks y RStudio.

**¿Dónde puedo encontrar información sobre los códigos de error?**

Consulte [Códigos de error del módulo de Aprendizaje automático](https://msdn.microsoft.com/library/azure/dn905910.aspx) para ver una lista de códigos de error y sus descripciones.

## <a name="scalability"></a>Escalabilidad
**¿Qué es la escalabilidad de hello del servicio web de hello?**

Actualmente, el punto de conexión de hello predeterminado se haya aprovisionado con 20 solicitudes simultáneas de registros de recursos por cada extremo. Puede escalar este too200 de solicitudes simultáneas por punto de conexión y se pueden escalar cada too10 de servicio web, 000 extremos por servicio web como se describe en [escalar un servicio Web](machine-learning-scaling-webservice.md). En BES, cada punto de conexión permite el procesamiento de 40 solicitudes a la vez y el resto de solicitudes adicionales que superan este número se ponen en cola. Estas solicitudes en cola se ejecutan automáticamente como Hola cola agota.

**¿Los trabajos de R se reparten entre nodos?**

Nº  

**¿Cuántos datos se pueden usar para el entrenamiento?**

Módulos de estudio de aprendizaje automático admiten conjuntos de datos de seguridad too10 GB de datos numéricos densos para casos de uso comunes. Si un módulo toma total Hola de entrada, más de un tamaño de todas las entradas es 10 GB. También puede realizar un muestreo de conjuntos de datos mayores mediante consultas de Hive o Azure SQL Database, o bien mediante el procesamiento previo con los módulos de [aprendizaje con recuentos][counts] antes de la ingesta.  

Hello siguientes tipos de datos puede expandir los conjuntos de datos de toolarger durante la normalización de características y están limitados que no requiere herramientas de 10 GB:

* Dispersos
* Categorías
* Cadenas
* Datos binarios

Hola siguiendo los módulos es limitados toodatasets menor que 10 GB:

* Módulos de recomendación.
* Módulo Synthetic Minority Oversampling Technique (SMOTE)
* Módulos de script: R, Python y SQL
* Módulos donde el tamaño de los datos de la salida de hello pueden ser mayores que el tamaño de datos de entrada, como Join o hash de características
* Validación cruzada, ajuste de los hiperparámetros del modelo, regresión ordinal y multiclase uno contra todos, cuando el número de iteraciones sea muy grande.

Para conjuntos de datos mayores de GB unos, cargar datos tooAzure almacenamiento o base de datos de SQL Azure, o use HDInsight en lugar de que se cargan directamente desde un archivo local.

**¿Hay alguna limitación en el tamaño de los vectores?**

Filas y columnas son cada limitación de .NET toohello limitado de Max Int: 2.147.483.647.

**¿Se puede ajustar el tamaño Hola de máquina virtual de Hola que ejecuta el servicio web de Hola?**

No.  

## <a name="security-and-availability"></a>Seguridad y disponibilidad
**¿Quién puede acceder a punto de conexión de http de hello para el servicio web de Hola de forma predeterminada? ¿Cómo se restringe el punto de conexión de acceso toohello?**

Cuando se implementa un servicio web, se crea un punto de conexión predeterminado para ese servicio. el punto de conexión de saludo predeterminado se puede llamar mediante su clave de API. Puede agregar que más puntos de conexión con sus propias claves de hello portal de Azure clásico o mediante programación usando Hola API de administración de servicios Web. Las claves de acceso son llamadas a toomake necesaria de servicio web de toohello. Para obtener más información, consulte [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).

**¿Qué sucede si no se encuentra mi cuenta de Azure Storage?**

Estudio de aprendizaje automático se basa en datos intermedios de almacenamiento de Azure proporcionada por el usuario cuenta toosave cuando se ejecuta el flujo de trabajo de Hola. Esta cuenta de almacenamiento se proporciona tooMachine estudio de aprendizaje cuando se crea un área de trabajo. Después de hello Crear área de trabajo, si la cuenta de almacenamiento de Hola se elimina y ya no se encuentra, el área de trabajo de hello dejará de funcionar y todos los experimentos en que se producirá un error de área de trabajo.

Si elimina accidentalmente cuenta de almacenamiento de hello, volver a crear cuenta de almacenamiento de hello con hello igual nombre en hello misma región que Hola elimina cuenta de almacenamiento. A continuación, resincronice la tecla de acceso de Hola.

**¿Qué sucede si la clave de acceso de mi cuenta de almacenamiento no está sincronizada?**

Estudio de aprendizaje automático se basa en datos intermedios de almacenamiento de Azure proporcionada por el usuario cuenta toostore cuando se ejecuta el flujo de trabajo de Hola. Esta cuenta de almacenamiento se proporciona tooMachine estudio de aprendizaje cuando se crea un área de trabajo y las teclas de acceso de hello están asociadas con dicha área de trabajo. Si se cambian las teclas de acceso de hello después de crea el área de trabajo de hello, área de trabajo de hello ya no puede tener acceso a cuenta de almacenamiento de Hola. Dejará de funcionar y se producirá un error en todos los experimentos que haya en esa área de trabajo.

Si cambia las teclas de acceso de cuenta de almacenamiento, las teclas de acceso de resincronización hello en el área de trabajo de hello mediante el uso de Hola portal de Azure clásico.  

## <a name="support-and-training"></a>Soporte técnico y entrenamiento
**¿Dónde puedo recibir entrenamiento para Aprendizaje automático de Azure?**

Hola [centro de documentación de aprendizaje automático](https://azure.microsoft.com/services/machine-learning/) hospeda tutoriales en vídeo y cómo tooguides. Estas guías paso a paso introducen servicios hello y explican Hola ciclo de vida de ciencia de datos de importación de datos, limpieza de datos, generar modelos predictivos y su implementación en producción mediante el uso de aprendizaje automático de Azure.

Agregamos toohello material nuevo centro de aprendizaje de máquina de forma continuada. Puede enviar solicitudes para obtener el material de aprendizaje adicionales en el centro de aprendizaje de máquina en hello [foro de comentarios de usuario](https://windowsazure.uservoice.com/forums/257792-machine-learning).

También puede buscar cursos en [Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning).

**¿Dónde puedo recibir soporte técnico para Aprendizaje automático de Azure?**

tooget de soporte técnico para el aprendizaje automático de Azure, vaya demasiado[soporte técnico de Azure](/support/options/)y seleccione **aprendizaje automático**.

Azure Machine Learning cuenta también con un foro de la comunidad en MSDN, donde puede plantear preguntas sobre el tema. equipo de aprendizaje automático de Azure Hola supervisa foro Hola. Vaya demasiado[foro de Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning).

## <a name="billing-questions"></a>Preguntas sobre facturación
**¿Cómo funciona la facturación de Aprendizaje automático?**

Azure Machine Learning tiene dos componentes: Machine Learning Studio y servicios web Machine Learning.

Mientras se está planteando estudio de aprendizaje automático, puede utilizar el nivel de facturación de Hola. nivel gratis Hello también le permite implementar un servicio web clásico que una capacidad limitada.

Si decide que el aprendizaje automático de Azure satisface sus necesidades, puede registrarse para Hola nivel estándar. toosign seguridad, debe tener una suscripción de Microsoft Azure.

En el nivel de estándar de hello, se le facturará mensualmente para cada área de trabajo que defina en estudio de aprendizaje automático. Cuando se ejecuta un experimento en studio hello, se le facturará de recursos de proceso cuando se ejecuta un experimento. Al implementar un servicio web estándar, las transacciones y se facturan horas en función de la opción de pago de Hola de proceso.

En los nuevos servicios web (basados en Resource Manager) se han incorporado planes de facturación que permiten costos más predecibles. En niveles de precios ofrece toocustomers descuentos que necesitan una gran cantidad de capacidad.

Cuando se crea un plan, confirmar tooa costo que viene con una cantidad incluida de horas de proceso de API y transacciones de API fijo. Si necesita más de las cantidades incluidas, puede agregar instancias tooyour plan. Si necesita un volumen de cantidades mucho mayor, puede elegir un plan superior que incluya muchas más cantidades, ya que el porcentaje de descuento resulta más ventajoso.

Después de hello las cantidades incluidas en las instancias existentes se agotan, uso adicional se cobra a velocidad por encima del límite de Hola que esté asociada con el nivel de plan de facturación de Hola.

> [!NOTE]
Las cantidades incluidas se reasignan cada 30 días y las cantidades incluidas no utilizadas no pasan toohello período siguiente.

Para más información sobre los precios y la facturación, consulte los [precios de Aprendizaje automático](https://azure.microsoft.com/pricing/details/machine-learning/).

**¿Dispone Aprendizaje automático de una evaluación gratuita?**

 Azure Machine Learning dispone de una opción de suscripción gratuita que se explica en [Precios de Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/). Estudio de aprendizaje automático tiene una versión de prueba de evaluación rápida de ocho horas que está disponible al iniciar sesión demasiado[estudio de aprendizaje automático](https://studio.azureml.net/?selectAccess=true&o=2).

 Además, al registrarse para obtener una evaluación gratuita de Azure, puede probar cualquier servicio de Azure durante un mes. toolearn más información acerca de hello evaluación gratuita de Azure, visite [Azure P+F de prueba gratuita](https://azure.microsoft.com/pricing/free-trial-faq/).

**¿Qué es una transacción?**

Una transacción representa una llamada API a la que responde Aprendizaje automático de Azure. Las transacciones de las llamadas del Servicio de solicitud-respuesta (RRS) y del Servicio de ejecución por lotes (BES) se computan y se facturan de acuerdo con el plan de facturación.

**¿Puedo usar Hola incluida cantidades de transacciones en un plan para las transacciones de registros de recursos y BES?**

Sí. Las transacciones de RRS y BES se computan y se facturan en función del plan de facturación.

**¿Qué es una hora de proceso de API?**

Una hora de proceso de API es la unidad de facturación de Hola para tiempo de Hola que toman toorun de llamadas de API mediante el uso de aprendizaje automático de los recursos de proceso. Todas las llamadas computan a la hora de facturar.

**¿Cuánto tarda una llamada API de producción típica?**

Horas de llamada a API de producción pueden variar significativamente, comprendido generalmente entre cientos de milisegundos tooa pocos segundos. Algunas llamadas de API pueden requerir minutos, según la complejidad de Hola de procesamiento de datos de Hola y el modelo de aprendizaje automático. Hola mejor manera tooestimate API de producción llamada es a menudo toobenchmark un modelo de servicio de aprendizaje automático de Hola.

**¿Qué es una hora de proceso de Studio?**

Una hora de proceso Studio es la unidad de facturación de Hola para tiempo agregado Hola que sus experimentos usan recursos de proceso en studio.

**¿En los nuevos servicios web (basado en el Administrador de recursos de Azure), capa de desarrollo/pruebas de hello significado para?**

Servicios web basados en el Administrador de recursos proporcionan varios niveles que puede usar tooprovision el plan de facturación. Hello tarifa de desarrollo/pruebas proporciona limitadas, incluyen cantidades que le permiten tootest el experimento como un servicio web sin incurrir en costos. Tener Hola oportunidad toosee su funcionamiento.

**¿Existen otros cargos de almacenamiento?**

nivel gratuito de aprendizaje de máquina de Hello no requiere ni permitir el almacenamiento independiente. nivel estándar de aprendizaje de máquina de Hello requiere que los usuarios toohave una cuenta de almacenamiento de Azure. Azure Storage se [factura por separado](https://azure.microsoft.com/pricing/details/storage/).

**¿Admite Machine Learning alta disponibilidad?**

Sí. Para obtener más información, consulte [precios de aprendizaje de máquina](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) para obtener una descripción del contrato de nivel de servicio (SLA) de Hola.

**¿En qué tipo específico de recursos de proceso se van a ejecutar las llamadas API de producción?**

Hola servicio aprendizaje automático es un servicio para varios inquilinos. Recursos de proceso real que se usan en el back-end de hello varían y están optimizados para rendimiento y capacidad de predicción.

### <a name="management-of-new-resource-manager-based-web-services"></a>Administración de nuevos servicios web (basados en Resource Manager)
**¿Qué ocurre si elimino mi plan?**

plan de Hola se quita de su suscripción y se le cobra según uso prorrateado.

> [!NOTE]
No se puede eliminar un plan que use un servicio web. plan de hello toodelete, debe o bien asignar un nuevo plan de servicio web de toohello o eliminar el servicio web de Hola.

**¿Qué es una instancia del plan?**

Una instancia de plan es una unidad de las cantidades incluidas que puede agregar tooyour plan de facturación. Cuando selecciona un nivel de facturación para el plan, incluye una instancia. Si necesita más de las cantidades incluidas, puede agregar instancias de hello seleccionado nivel tooyour plan de facturación.

**¿Cuántas instancias del plan puedo agregar?**

Puede tener una instancia de nivel de precios de desarrollo/pruebas de hello en una suscripción.

En los niveles Estándar S1, Estándar S2 y Estándar S3, puede agregar tantas como sean necesarias.

> [!NOTE]
En función del uso previsto, puede ser más rentable tooupgrade tooa capa que más se ha incluido las cantidades en lugar de agregar el nivel actual de instancias toohello.

**¿Qué ocurre si cambio los niveles del plan (por ejemplo, cambio a un plan superior o inferior)?**

se elimina el plan anterior Hello y uso actual de Hola se factura según una prorrateados. Se crea un nuevo plan con hello incluye las cantidades totales de capa de actualizar o degradar Hola de rest de hello del período de Hola.

> [!NOTE]
Las cantidades incluidas se asignan cada período y las cantidades no utilizadas no se transfieren al período siguiente.

**¿Qué ocurre cuando incrementan a instancias de Hola en un plan de?**

Las cantidades se incluyen de forma prorrateado y pueden tardar 24 horas toobe efectivo.

**¿Qué ocurre si elimino una instancia de un plan?**

instancia de Hola se quita de su suscripción y se le cobra según uso prorrateado.

### <a name="sign-up-for-new-resource-manager-based-web-services-plans"></a>Registro en los nuevos planes de servicios web (basados en Resource Manager)
**¿Cómo me puedo suscribir a un plan?**

Tiene dos planes de facturación toocreate de formas.

La primera vez que implemente un servicio web basado en Resource Manager, puede elegir un plan existente o crear uno nuevo.

Planes creados de esta manera se encuentran en su región de manera predeterminada, y el servicio web serán región toothat implementado.

Si desea toodeploy services tooregions distinto de su región de manera predeterminada, puede que desee toodefine los planes de facturación antes de implementar el servicio.

En ese caso, puede iniciar sesión en el portal de servicios Web de Azure Machine Learning toohello e ir a página de planes de toohello. Desde allí, puede agregar planes, eliminar planes y modificar los planes existentes.

**¿Plan que debo elegir toostart off con?**

Se recomienda que comienzan con hello estándar S1 nivel y supervisar el servicio de uso. Si encuentra que está usando sus las cantidades incluidas rápidamente, puede agregar instancias o mover tooa de nivel superior y obtener mejor descuentos. Puede ajustar el plan de facturación a sus necesidades durante el ciclo de facturación.

**¿Qué regiones existen nuevos planes de hello en?**

nuevos planes de facturación Hola están disponibles en tres regiones de producción hello en el que se admiten servicios web nuevos de hello:

* Centro-Sur de EE. UU
* Europa occidental
* Sudeste de Asia

**Tengo servicios web en varias regiones. ¿Necesito un plan para cada región?**

Sí. Los precios del plan varían según la región. Cuando se implementa una región de tooanother del servicio web, necesita tooassign TI un plan que es específico toothat región. Para más información, consulte [Productos disponibles por región]( https://azure.microsoft.com/regions/services/).

### <a name="new-web-services-overages"></a>Nuevos servicios web: uso por encima del límite
**¿Cómo puedo comprobar si he superado el uso del servicio web?**

Puede ver el uso de hello en todos los planes en la página de planes de hello en el portal de servicios Web de Azure Machine Learning Hola. Inicie sesión en el portal de toohello y, a continuación, haga clic en hello **planes** opción de menú.

Hola **transacciones** y **proceso** las columnas de tabla de hello, puede ver las cantidades de hello incluyen del plan de Hola y porcentaje usado de Hola.

**¿Qué ocurre cuando agote Hola incluir cantidades en el nivel de precios de desarrollo/pruebas de hello?**

Se detienen servicios que tienen un nivel asignado toothem de precios para desarrollo y pruebas hasta Hola período siguiente o hasta que mueva nivel tooa de pago.

**En los servicios web clásicos y en el uso por encima del límite de los nuevos servicios web (basados en Resource Manager), ¿cómo se calculan los precios de las cargas de trabajo de los servicios de solicitud-respuesta (RRS) y de los servicios de ejecución por lotes (BES)?**

Para una carga de trabajo RR, se le cobrará por cada llamada de transacciones de API que se realiza y Hola por tiempo de proceso que está asociado con esas solicitudes. Número total de Hola de llamadas de API que realice se multiplican por precio de Hola por 1000 transacciones (prorrateada por transacciones individuales), se calculan los costos de transacciones de API de producción de RR. Sus gastos de horas de proceso de API de RR API de producción se calculan como cantidad de Hola de tiempo necesario para cada toorun de llamada de API, multiplicado por el número total de transacciones de API, multiplicado por el precio Hola por las horas de proceso de API de producción de hello.

Por ejemplo, para estándar S1 por encima del límite, 1.000.000 de transacciones de API que tardan segundos 0,72 cada toorun, se crearán (1.000.000 * 0,50 $/ 1K transacciones de API) en 500 USD en los costos de transacciones de API de producción y (1.000.000 * 0.72 s * $2 / h) $400 en proceso de API de producción horas, para un total de 900 $.

Para una carga de trabajo BES, se le cobra Hola igual manera. Sin embargo, los costos de transacciones de API de hello representan el número de Hola de trabajos por lotes que se envía y gastos de proceso de hello representan el tiempo de proceso de Hola que esté asociada con los trabajos por lotes. Los costos de transacciones de API de producción BES se calculan como número total de Hola de trabajos enviados multiplicado por precio de Hola por 1000 transacciones (prorrateada por transacciones individuales). Los costos de horas de proceso de API de producción BES API se calculan como cantidad de Hola de tiempo necesario para cada fila de su toorun trabajo multiplicado por el número total de filas de su trabajo multiplicado por el número total de trabajos que se multiplica por el precio Hola por las API de producción de hello Hola horas de proceso. Cuando usas Hola Calculadora de aprendizaje automático, Hola transacción medidor representa Hola número de trabajos que piensa toosubmit, así como campo de hora por transacción Hola representa Hola combina tiempo requerido para todas las filas de cada toorun de trabajo.

Por ejemplo, suponga un uso por encima del límite del nivel Estándar S1. Envía 100 trabajos al día, cada uno de los cuales consta de 500 filas, cada una de las cuales tarda 0,72 segundos en ejecutarse. Los costos mensuales de uso por encima del límite serían (100 trabajos al día = 3100 trabajos/mes 0,50 USD/1000 transacciones de API) 1,55 USD en costos de transacciones de API de producción y (500 filas 0,72 seg. 3100 trabajos 2 USD/h) 620 USD en horas de proceso de API de producción, lo que haría un total de 621,55 USD.

### <a name="azure-machine-learning-classic-web-services"></a>Servicios web clásicos de Azure Machine Learning
**¿Sigue estando disponible el plan de pago por uso?**

Sí. Los servicios web clásicos siguen disponibles en Azure Machine Learning.  

### <a name="azure-machine-learning-free-and-standard-tier"></a>Nivel Gratis y Estándar de Azure Machine Learning
**¿Qué se incluye en el nivel gratuito de aprendizaje de máquina de Azure de hello?**

nivel de Azure Machine Learning libre de Hello está previsto tooprovide un toohello introducción detallada estudio de aprendizaje automático de Azure. Todo lo que necesita es un toosign de cuenta de Microsoft hasta. nivel gratis Hello incluye acceso gratuito a área de trabajo de estudio de aprendizaje automático de Azure de tooone por [cuenta de Microsoft](https://www.microsoft.com/account/default.aspx). En este nivel, puede usar too10 GB de almacenamiento y hacer operativos los modelos como las API de almacenamiento provisionales. No hay ningún Acuerdo de Nivel de Servicio que cubra las cargas de trabajo del nivel Gratis, ya que estas cargas de trabajo están destinadas exclusivamente a desarrollo y uso personal. 

Áreas de trabajo de nivel gratuito tienen Hola siguientes limitaciones:

* Las cargas de trabajo no pueden tener acceso a datos mediante la conexión de servidor local de tooan que ejecuta SQL Server.
* No se pueden implementar nuevos servicios web de base de Resource Manager.


**¿Qué se incluye en planes y nivel de hello Azure Machine Learning estándar?**

nivel de Hello Azure Machine Learning estándar es una versión de producción de pago de estudio de aprendizaje automático de Azure. Hola estudio de aprendizaje automático de Azure se factura cuota mensual en un mes por cada área de trabajo y prorrateados para meses parciales. Las horas de experimentación de Azure Machine Learning Studio se facturan por hora de proceso de experimentación activa. La facturación se prorratea por horas parciales.  

Hola servicio API de aprendizaje de máquina de Azure se factura dependiendo de si es un servicio web de clásico o un nuevo servicio web (basado en el Administrador de recursos).

Hola siguiendo los cargos se agrega por área de trabajo para su suscripción.

* Suscripción de área de trabajo de aprendizaje de máquina: Hola suscripción del área de trabajo de aprendizaje automático es una cuota mensual que proporciona el área de trabajo de access tooa estudio de aprendizaje automático. suscripción de Hello es necesario toorun experimentos en hello studio tooutilize Hola producción y las API.
* Horas de experimentación de Studio: este contador agrega todos los cargos de proceso que se acumulan ejecutando experimentos en estudio de aprendizaje automático y llama a ejecución API de producción de hello entorno de ensayo.
* Acceder a los datos mediante la conexión de servidor local de tooan que se ejecuta SQL Server en los modelos para el entrenamiento y puntuación.
* En los servicios web clásicos:
  * Horas de proceso de API de producción: este medidor incluye los gastos de proceso acumulados por los servicios web que se ejecutan en producción.
  * Transacciones de API de producción (en 1000s): este contador incluye los cargos que se acumulan por el servicio web de llamada tooyour producción.

Además de hello anteriores cargos, en caso de hello del servicio web basado en el Administrador de recursos, cargos son plan seleccionado toohello agregados:

* Estándar S1, S2 y S3 API planear (unidades): Este contador representa el tipo de Hola de instancia que se selecciona para servicios web basados en el Administrador de recursos.
* Estándar S1, S2 y S3 por encima del límite API horas de proceso: Este contador incluye cargos de proceso que se acumulan los servicios web basados en el Administrador de recursos que se ejecutan en producción después de que se agoten las cantidades de hello incluida en las instancias existentes. uso de Hello adicionales se aplican cargos en hello overate tasa con la que está asociada a nivel de plan de S1, S2 y S3.
* Estándar transacciones de API por encima del límite de S1, S2 o S3 (en 1,000s): este contador incluye los cargos que se acumulan por llamada tooyour producción se agotan servicio de web basado en el Administrador de recursos después de hello incluido cantidades en las instancias existentes. Hello uso adicionales se aplican cargos en hello overate tasa asociada a nivel de plan de S1, S2 y S3.
* Incluye cantidad de horas de proceso de API: Con los servicios web basados en el Administrador de recursos, este contador representa cantidad Hola incluido de horas de proceso de API.
* Incluye la cantidad de transacciones de API (en 1,000s): servicios web basados en con el Administrador de recursos, este contador representa la cantidad de hello incluido de transacciones de API.

**¿Cómo puedo suscribirme al nivel Gratis de Azure Machine Learning?**

Todo lo que necesita es una cuenta de Microsoft. Vaya demasiado[principal de aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/)y, a continuación, haga clic en **comenzar ahora**. Inicie sesión con su cuenta de Microsoft y se creará un área de trabajo en el nivel Gratis. Puede iniciar tooexplore y crear experimentos de aprendizaje automático de forma inmediata.

**¿Cómo puedo suscribirme al nivel Estándar de Azure Machine Learning?**

En primer lugar debe tener acceso tooan suscripción de Azure toocreate un área de trabajo de aprendizaje automático estándar. Puede registrarse para una suscripción de Azure de evaluación gratuita de 30 días y suscripción de Azure de pago tooa actualización posterior, o puede comprar una suscripción de Azure pago directamente. A continuación, puede crear un área de trabajo de aprendizaje automático desde portal clásico de hello Microsoft Azure después de obtener acceso toohello suscripción. Hola de vista [instrucciones paso a paso](https://azure.microsoft.com/trial/get-started-machine-learning-b/).

Como alternativa, puede ser invitados por área de trabajo de un aprendizaje automático estándar área de trabajo propietario tooaccess Hola del propietario.

**¿Puedo especificar mi propio toouse de cuenta de almacenamiento de blobs de Azure con el nivel gratis Hola?**

No, nivel estándar de hello es equivalente toohello versión de hello servicio de aprendizaje automático que estaba disponible antes de Hola se introdujeron niveles.

**¿Puedo implementar mi máquina modelos como las API de aprendizaje en nivel gratis Hola?**

Sí, puede hacer operativos los modelos de aprendizaje automático toostaging API de servicios como parte del nivel gratis Hola. tooput Hola servicio de API de ensayo a producción y obtener un extremo de producción para el servicio de hello operaciones, debe utilizar nivel estándar Hola.

**¿Cuál es la diferencia de hello entre evaluación gratuita de Azure y nivel gratuito de aprendizaje de máquina de Azure?**

Hola [evaluación gratuita de Microsoft Azure](https://azure.microsoft.com/free/) ofrece créditos que se puede aplicar tooany Azure del servicio durante un mes. ofertas de nivel gratuito de aprendizaje de máquina de Azure de Hello continua acceso específicamente tooAzure aprendizaje automático para las cargas de trabajo no es de producción.

**¿Cómo se puede mover un experimento de nivel estándar de hello nivel gratuito toohello?**

toocopy sus experimentos de nivel estándar de hello nivel gratuito toohello:

1. Inicie sesión en estudio de aprendizaje automático de tooAzure y asegúrese de que puede ver área de trabajo gratuita de Hola y área de trabajo estándar de hello en el selector de área de trabajo de hello en la barra de navegación superior de Hola.
2. Cambiar el área de trabajo de tooFree si se encuentra en el área de trabajo estándar Hola.
3. En la vista de lista del experimento de hello, seleccione un experimento que haría que se toocopy y, a continuación, haga clic en hello **copia** botón de comando.
4. Seleccione área de trabajo estándar Hola Hola cuadro de diálogo que se abre y, a continuación, haga clic en hello **copia** botón.
   Hola a todos los conjuntos de datos asociados, el modelo entrenado, etc. se copian junto con el experimento de hello en el área de trabajo estándar de Hola.
5. Necesita toorerun Hola experimento y volver a publicar el servicio web en el área de trabajo estándar Hola.

### <a name="studio-workspace"></a>Área de trabajo de Studio
**¿Voy a tener facturas distintas por cada una de las áreas de trabajo?**

Los gastos de las áreas de trabajo se desglosan por separado por cada medidor aplicable en una sola factura.

**¿En qué tipo específico de recursos de proceso se ejecutarán mis experimentos?**

Hola servicio aprendizaje automático es un servicio para varios inquilinos. Recursos de proceso real que se usan en el back-end de hello varían y están optimizados para rendimiento y capacidad de predicción.

### <a name="guest-access"></a>Acceso de invitado
**¿Qué es el acceso de invitados tooAzure estudio de aprendizaje automático?**

El acceso de invitado es una experiencia de evaluación restringida. Puede crear y ejecutar experimentos en Azure Machine Learning Studio sin costo alguno y sin autenticación. Las sesiones de invitado no son persistentes (no se puede guardar) y limitado tooeight horas. Otras limitaciones son la falta de compatibilidad con R y Python, la falta de API de ensayo y la restricción en el tamaño del conjunto de datos y en la capacidad de almacenamiento. En comparación, los usuarios que decidan toosign con una cuenta de Microsoft tienen nivel gratuito de toohello de acceso completa de estudio de aprendizaje automático que se ha descrito anteriormente, que incluye un área de trabajo persistente y capacidades más completas. toochoose que experimenta el aprendizaje automático libre, haga clic en **Introducción** en [https://studio.azureml.net](https://studio.azureml.net)y, a continuación, seleccione **adivinar acceso** o inicie sesión con una de Microsoft cuenta.

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
