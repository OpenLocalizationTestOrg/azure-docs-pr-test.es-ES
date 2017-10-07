---
title: ciclo de vida del proceso de equipo datos ciencia aaaAzure | Documentos de Microsoft
description: Pasos necesarios tooexecute los proyectos de ciencia de datos.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 58114a1c2d3289d1c4b2781219d0bf9647dbccd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-lifecycle"></a>Ciclo de vida del proceso de ciencia de datos en equipo

Hola proceso de ciencia de datos de equipo (TDSP) proporciona un ciclo de vida recomendada puede usar toostructure en los proyectos de ciencia de datos. ciclo de vida de Hello describe los pasos de hello, de toofinish de inicio, que los proyectos suelen seguir cuando se ejecutan. Si está usando otro ciclo de vida de ciencia de datos, como [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) o el proceso personalizado de la organización, puede seguir usando Hola basado en tareas TDSP con estos ciclos de vida de desarrollo. 

Este ciclo de vida se ha diseñado para los proyectos de ciencia de datos que son tooship previsto como parte de aplicaciones inteligentes. Estas aplicaciones implementan modelos de aprendizaje o inteligencia artificial de máquina para realizar un análisis predictivo. Los proyectos de ciencia de datos exploratorios y los proyectos de análisis ad hoc también se pueden beneficiar del uso de este proceso. Pero, en estos casos, puede que algunos de los pasos descritos no sean necesarios.    

Esta es una representación visual de hello **ciclo de vida del proceso de ciencia de datos de equipo**. 

![Ciclo de vida de TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

ciclo de vida de Hello TDSP se compone de cinco fases principales que se ejecutan de forma iterativa. Entre ellos se incluyen los siguientes:

* **Conocimiento del negocio**
* **Adquisición y comprensión de los datos**
* **Modelado**
* **Implementación**
* **Aceptación del cliente**

Para cada fase, proporcionamos Hola siguiente información:

* **Objetivos**: Hola objetivos concretos.
* **¿Cómo toodo se**: Hola tareas específicas que se describen y las instrucciones proporcionadas en realizarlas.
* **Artefactos**: compatibilidad con las entregas de Hola y Hola para producirlos para.


## <a name="1-business-understanding"></a>1. Conocimiento del negocio

### <a name="goals"></a>Objetivos
* Hola **clave variables** están especificados que son tooserve como Hola **modelo destinos** y se usan cuyas métricas relacionadas determinar Hola ha realizado correctamente para el proyecto de Hola.
* Hola relevante **orígenes de datos** se identifican que business hello tiene acceso tooor necesidades tooobtain.

### <a name="how-toodo-it"></a>¿Cómo toodo,
En esta fase se abordan dos tareas principales: 

* **Definir los objetivos del**: trabajar con el cliente y otro toounderstand de las partes interesadas e identificar los problemas de negocios de Hola. Formular preguntas que definen los objetivos empresariales de Hola y que pueden tener como destino las técnicas de ciencia de datos.
* **Identifique los orígenes de datos**: encontrar Hola relevantes datos que le ayuda a responder a preguntas de Hola que definen los objetivos de hello del proyecto de Hola.

#### <a name="11-define-objectives"></a>1.1 Definición de objetivos

1. Un objetivo central de este paso es clave de hello tooidentify **variables empresariales** que análisis de hello necesita toopredict. Estas variables son los que se hace referencia tooas hello **modelo destinos** y las métricas de hello asociadas con ellos son toodetermine usado Hola éxito del proyecto de Hola. Dos ejemplos de estos destinos son probabilidad de Hola o de previsión de ventas de un pedido que se va a fraudulentos.

2. Definir hello **objetivos del proyecto** pidiendo y refinar "nitidez" preguntas a las que son relevantes y específico y no ambigua. Ciencia de datos es proceso Hola del uso de nombres y números tooanswer esas preguntas. Para obtener más información sobre preguntas agudo, consulte [cómo toodo ciencia de datos](https://blogs.technet.microsoft.com/machinelearning/2016/03/28/how-to-do-data-science/) blog. Ciencia de datos / aprendizaje automático es tooanswer usados normalmente cinco tipos de preguntas:
 
   * ¿Cuánto? o ¿cuántos? (regresión)
   * ¿Qué categoría? (clasificación)
   * ¿Qué grupo? (agrupación en clústeres)
   * ¿Es extraño? (detección de anomalías)
   * ¿Qué opción se debe elegir? (recomendación)

    Determine cuál de las siguientes es su pregunta y cómo la respuesta logra sus objetivos empresariales.

3. Definir hello **equipo de proyecto** especificando Hola roles y responsabilidades de sus miembros. Desarrolle un plan general de hitos que se pueda repetir a medida que se descubra más información.  

4. **Defina las métricas del éxito**. Por ejemplo: lograr cliente renovación de precisión de la predicción de X % al final de Hola de este proyecto de 3 meses, por lo que podemos ofrecer promociones tooreduce renovación. las métricas de Hello deben ser **inteligente**: 
   * **S**pecific (específicas) 
   * **M**easurable (mensurables)
   * **A**chievable (alcanzables) 
   * **R**elevant (pertinentes) 
   * **T**ime-bound (con un límite de tiempo) 

#### <a name="12-identify-data-sources"></a>1.2 Identificación de los orígenes de datos
Identifique los orígenes de datos que contienen ejemplos conocidos de preguntas de respuestas tooyour agudo. Busque Hola datos siguientes:

* Datos **pertinente** toohello pregunta. ¿Tenemos las medidas de destino de Hola y características que son destino de toohello relacionados?
* Datos que es un **medida precisa** de nuestras características de hello y el destino del modelo de interés.

No es raro, por ejemplo, toofind que los sistemas existentes otros tipos de datos tooaddress de registro y necesitan toocollect Hola problema y lograr los objetivos del proyecto Hola. En este caso, puede desea toolook para orígenes de datos externos o actualizar los datos nuevos de toocollect de sistemas.

### <a name="artifacts"></a>Artefactos
Estas son las entregas de hello en esta fase:

* [**Fletar documento**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Charter.md): una plantilla estándar se proporciona en hello definición TDSP de la estructura de proyecto. Se trata de un documento vivo que se actualiza a lo largo del proyecto de hello mientras se realizan nuevas detecciones y como negocios cambian los requisitos. clave de Hello es tooiterate en este documento, agregar información más detallada, según avance por el proceso de detección de Hola. Mantener Hola customer y otras partes interesadas implicados para realizar cambios de Hola y comunican claramente los motivos de Hola para hello cambios toothem.  
* [**Orígenes de datos**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#raw-data-sources): se trata de hello **orígenes de datos sin procesar** sección de hello **definiciones de datos** informes que se encuentra en el proyecto de hello TDSP **informe de datos**  carpeta. Especifica ubicaciones de destino para los datos sin procesar de Hola y Hola original. En fases posteriores, rellene detalles adicionales, como scripts toomove datos hello tooyour entorno analítica.  
* [**Los diccionarios de datos**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/DataDictionaries): este documento proporciona descripciones de datos de hello proporcionada por el cliente de Hola. Estas descripciones incluyen información acerca del esquema de hello (tipos de datos, información sobre las reglas de validación, si lo hay) y Hola diagramas de relación de entidades, si está disponible.


## <a name="2-data-acquisition-and-understanding"></a>2. Adquisición y comprensión de los datos

### <a name="goals"></a>Objetivos
* Limpio y de alta calidad dataset se entienden las variables cuyo destino de toohello de relaciones que se encuentran en el entorno de análisis adecuado de hello, toomodel listo.
* Una arquitectura de solución de toorefresh de canalización de datos de Hola y puntuación de datos se ha desarrollado con regularidad.

### <a name="how-toodo-it"></a>¿Cómo toodo,
En esta fase se abordan tres tareas principales:

* **Recopilar datos de hello** a entorno de análisis de destino de Hola.
* **Explorar datos hello** toodetermine si calidad de datos de hello es cuestión de Hola de tooanswer adecuada. 
* **Configurar una canalización de datos** tooscore nuevas o con regularidad actualiza datos.

#### <a name="21-ingest-hello-data"></a>2.1 introducir datos Hola
Configurar Hola proceso toomove Hola datos desde ubicaciones de origen toohello ubicaciones de destino donde las operaciones de análisis como entrenamiento y las predicciones son toobe ejecutado. Para detalles técnicos y las opciones de toodo con varios servicios de datos de Azure, vea [cargar datos en entornos de almacenamiento de información para análisis](machine-learning-data-science-ingest-data.md). 

#### <a name="22-explore-hello-data"></a>2.2 explorar datos Hola
Antes de entrenar los modelos, deberá toodevelop un conocimiento claro de los datos de Hola. A menudo, los conjuntos de datos reales contienen ruido, les faltan datos o presentan un sinfín de discrepancias de otros tipos. Visualización y resumen de datos pueden ser usado tooaudit Hola calidad de los datos y proporcionar información de hello necesarios tooprocess Hola datos antes de esté listo para el modelado. Normalmente, se trata de un proceso iterativo.

TDSP proporciona una utilidad automatizada denominada [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) toohelp visualizar datos de Hola y preparar los informes de resumen de datos. Se recomienda empezar por IDEAR primera tooexplore Hola datos toohelp desarrollar comprensión de los datos iniciales interactivamente con ningún código y, a continuación, escribir código personalizado para visualización y exploración de datos. Para obtener instrucciones sobre la limpieza de datos de hello, consulte [tooprepare datos para el aprendizaje automático mejorada de tareas](machine-learning-data-science-prepare-data.md).  

Una vez que esté satisfecho con la calidad de Hola de hello limpiado datos, Hola siguiente paso es toobetter comprender los modelos de Hola que son inherentes a los datos de Hola que le ayudarán a elección y desarrollar un modelo de predicción adecuado para el destino. Buscar pruebas de grado datos Hola conectado están toohello destino y si hay suficientes toomove de datos al día con los siguientes pasos de modelado Hola. Como hemos indicado, normalmente, se trata de un proceso iterativo. Puede que tenga toofind nuevos orígenes de datos con más preciso o relevante más datos tooaugment Hola conjunto de datos inicialmente identificados en la fase anterior Hola.  

#### <a name="23-set-up-a-data-pipeline"></a>2.3 Configuración de una canalización de datos
Además toohello inicial ingesta y limpieza de Hola datos, normalmente deberá tooset un tooscore nuevos datos de proceso o una actualización de datos de Hola con regularidad como parte de un proceso de aprendizaje en curso. Para ello, puede configurar una canalización de datos o un flujo de trabajo. Este es un [ejemplo](machine-learning-data-science-move-sql-azure-adf.md) de cómo tooset de una canalización con [Data Factory de Azure](https://azure.microsoft.com/services/data-factory/). 

En esta fase se desarrolla a una arquitectura de la solución de canalización de datos de Hola. canalización de Hello también se desarrolla en paralelo con hello siguiendo las etapas de proyecto de ciencia de datos de Hola. canalización de Hello puede basarse en lote o streaming/en tiempo real o un híbrido dependiendo de su negocio necesita y hello las restricciones de los sistemas existentes en el que se integra esta solución. 

### <a name="artifacts"></a>Artefactos
siguiente Hola es las entregas de hello en esta fase.

* [**Informe de calidad de datos**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/DataSummaryReport.md): este informe contiene resúmenes de los datos, las relaciones entre cada atributo y el destino, la variable clasificación Hola etc. [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) herramienta que se proporciona como parte de TDSP puede generar rápidamente Este informe en cualquier conjunto de datos tabular, como un archivo CSV o una tabla relacional. 
* **Arquitectura de la solución**: Esto puede ser un diagrama o una descripción de los datos canalización usa toorun puntuación o predicciones sobre nuevos datos una vez que ha creado un modelo. También contiene Hola canalización tooretrain el modelo se basa en datos nuevos. documento de Hola se almacena en hello [proyecto](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/Project) directorio cuando se usa la plantilla de la estructura de directorio de hello TDSP.
* **Decisión de punto de comprobación**: antes de comenzar la ingeniería de todas las características y la compilación del modelo, puede volver a evaluar Hola proyecto toodetermine si se esperaba un valor de hello es toocontinue suficiente trabajo que supone. Por ejemplo, puede estar listo tooproceed, necesidad toocollect más datos o abandonar el proyecto de hello como datos de hello no existen pregunta de hello tooanswer.


## <a name="3-modeling"></a>3. Modelado

### <a name="goals"></a>Objetivos
* Características de datos óptima para el modelo de aprendizaje automático de Hola.
* Un modelo de aprendizaje automático informativo que predice destino Hola con más precisión.
* Un modelo de aprendizaje automático que es adecuado para entornos de producción.

### <a name="how-toodo-it"></a>¿Cómo toodo,
En esta fase se abordan tres tareas principales:

* **Característica ingeniería**: crear las características de datos de entrenamiento del modelo de toofacilitate de hello datos sin procesar.
* **Entrenamiento del modelo**: Buscar modelo Hola esa pregunta de hello respuestas con más precisión comparando sus métricas de éxito.
* Determine si el modelo es **adecuado para su uso en producción**.

#### <a name="31-feature-engineering"></a>3.1 Diseño de características
Característica ingeniería implica la inclusión, agregación y transformación de variables sin formato toocreate Hola características que se utilizan en el análisis de Hola. Si desea una visión general de qué debe a un modelo, deberá toounderstand características están relacionada tooeach otro y algoritmos de aprendizaje automático de hello son toouse esas características. Este paso requiere una combinación creativa de experiencia de dominio e información que obtuvo en el paso de exploración de datos de Hola. Se trata hallar el equilibrio: por un lado, buscar e incluir variables informativas y, por otro, evitar que se utilicen demasiadas variables no relacionadas. Variables informativas mejoran nuestros resultados; las variables no relacionadas introducen ruido innecesario en modelo Hola. También necesitará toogenerate estas características para los nuevos datos obtenidos durante la puntuación. Por lo tanto generación Hola de estas características sólo puede depender de datos que están disponibles en tiempo de Hola de puntuación. Para obtener orientación técnica de ingeniería de característica al usar varias tecnologías de datos de Azure, consulte [ingeniería Hola proceso de ciencia de datos de características](machine-learning-data-science-create-features.md). 

#### <a name="32-model-training"></a>3.2 Entrenamiento del modelo
Según el tipo de la pregunta que intenta responder, existen muchos algoritmos de modelado disponibles. Para obtener instrucciones sobre cómo elegir algoritmos hello, consulte [cómo toochoose algoritmos de aprendizaje automático de Microsoft Azure](machine-learning-algorithm-choice.md). Aunque en este artículo se escribió para aprendizaje automático de Azure, Hola guía proporciona es útil para los proyectos de aprendizaje automático. 

proceso de Hello para el entrenamiento del modelo incluye Hola pasos: 

* **Hola de dividir los datos de entrada** aleatoriamente para el modelado en un conjunto de datos de entrenamiento y un conjunto de datos de prueba.
* **Generar modelos de hello** con conjunto de datos de entrenamiento de Hola.
* **Evaluar** (conjunto de datos entrenamiento y prueba) una serie de máquina competencia algoritmos junto con hello de aprendizaje diversas asociados parámetros de ajuste (conocidos como barrido de parámetros) que están orientadas a responder a la pregunta de Hola de interés con hello datos actuales.
* **Determinar la solución "recomendada" hello** pregunta de hello tooanswer mediante la comparación de métrica de éxito de hello entre métodos alternativos.

> [!NOTE]
> **Evitar la pérdida de**: pérdida de datos puede estar causada por inclusión Hola de datos desde fuera conjunto de datos de entrenamiento de Hola que permite un modelo o el algoritmo de aprendizaje de máquina toomake excesivamente buena predicciones. Pérdida es un motivo habitual por qué los científicos de datos no saben nerviosos cuando reciben resultados de predicción que parecen buena toobe es true. Estas dependencias pueden ser difícil toodetect. pérdida de tooavoid a menudo requiere iterar entre generar un conjunto de datos de análisis, creando un modelo y evaluar la precisión de Hola. 
> 
> 

Proporcionamos un [herramienta automatizada Modelación e informes](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/Modeling) con TDSP que es capaz de toorun a través de varios algoritmos y parámetro barre tooproduce un modelo de línea de base. También genera un informe de modelado de base de referencia que resume el rendimiento de cada combinación de modelo y parámetros, incluida la importancia de las variables. Este proceso también es iterativo, porque así permite avanzar en el diseño de características. 

### <a name="artifacts"></a>Artefactos
los artefactos de Hello generados en esta fase se incluyen:

* [**Conjuntos de características**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#feature-sets): características de hello desarrollados para el modelado de Hola se describen en hello **conjuntos de características** sección de hello **definición de datos** informes. Contiene características de punteros toohello código toogenerate hello y una descripción acerca de cómo se genera las característica Hola.
* [**Informe del modelo**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Model/Model%201/Model%20Report.md): para cada modelo que se prueba, se genera un informe estándar basado en una plantilla que proporciona información detallada sobre cada experimento.
* **Decisión de punto de comprobación**: evaluar si el modelo de hello está realizando lo suficientemente bien toodeploy, tooa sistema de producción. Algunos tooask preguntas clave son:
  * ¿Pregunta de Hola Hola modelo respuestas con suficiente confianza teniendo en cuenta los datos de prueba de hello? 
  * ¿Debe probar algún enfoque alternativo, como recopilar datos adicionales, rediseñar las características o experimentar con otros algoritmos?


## <a name="4-deployment"></a>4. Implementación

### <a name="goal"></a>Objetivo
* Los modelos con una canalización de datos son tooa implementado producción o entorno similar de producción de aceptación del usuario final. 

### <a name="how-toodo-it"></a>¿Cómo toodo,
tarea principal de Hello cubierto en esta fase:

* **Incorporación de operatividad a modelo de Hola**: implementar la producción de tooa de modelo y la canalización de Hola o entorno similar de producción para el consumo de la aplicación.

#### <a name="41-operationalize-a-model"></a>4.1 Uso del modelo
Una vez que tenga un conjunto de modelos que funcionan bien, puede operationalized para otro tooconsume de aplicaciones. Dependiendo de los requisitos empresariales hello, se crean las predicciones en tiempo real o en forma de lote. toobe operaciones, los modelos de hello tienen toobe que se exponen a través de una interfaz API abierta que se puedan usar fácilmente desde diversas aplicaciones, como sitios Web en línea, hojas de cálculo, paneles o línea de aplicaciones empresariales y de back-end. Para obtener información sobre cómo crear e implementar un servicio web de Azure Machine Learning, consulte [Implementación de un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md). También es una telemetría de toobuild prácticas recomendada y supervisión en modelo de producción de hello y Hola toohelp de canalización implementado de datos con el estado de sistema posteriores reporting y solución de problemas.  

### <a name="artifacts"></a>Artefactos
* Panel de estado de estado del sistema y métricas clave.
* Informe de modelado final con detalles de implementación.
* Documento de arquitectura de la solución final.

## <a name="5-customer-acceptance"></a>5. Aceptación del cliente

### <a name="goal"></a>Objetivo
* **Finalizar entregas del proyecto Hola**: confirme que la canalización de hello, modelo de Hola y su implementación en un entorno de producción son satisfaciendo los objetivos de cliente.

### <a name="how-toodo-it"></a>¿Cómo toodo,
En esta fase se abordan dos tareas principales:

* **Validación de sistema**: confirmar modelo Hola implementado y canalización cumple las necesidades del cliente.
* **Proyecto entrega**: entidad toohello que es toorun Hola sistema en producción.

cliente de Hello debe validar que sistema Hola satisface sus necesidades empresariales y respuestas de Hola Hola preguntas con una precisión suficiente toodeploy Hola sistema tooproduction para su uso por la aplicación cliente. Toda la documentación de hello finaliza y revisada. Una parte off de entidad de toohello de proyecto Hola responsable de las operaciones se ha completado. Por ejemplo, esta entidad podría ser una TI o equipo al cliente de ciencia de datos o un agente de cliente de Hola que se encarga de ejecutar el sistema de hello en producción. 

### <a name="artifacts"></a>Artefactos
artefacto principal Hola generado en esta fase final es hello **salida del proyecto de informe de cliente**. Esto es informe técnico Hola que contiene todos los detalles de proyecto de Hola que toolearn útil sobre y Hola sistema funcione. TDSP incluye una plantilla de [informe de salida](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md) que se puede utilizar tal cual o personalizarse de acuerdo con las necesidades concretas del cliente. 

## <a name="summary"></a>Resumen
Hola [ciclo de vida del proceso de ciencia de datos de equipo](http://aka.ms/datascienceprocess) se modela como una secuencia de pasos iteradas que ofrecen orientación sobre las tareas de hello necesarios toouse modelos de predicción. Estos modelos se pueden implementar en un entorno toobe aprovecha toobuild inteligente las aplicaciones de producción. objetivo de Hola de este ciclo de vida del proceso es toocontinue toomove un proyecto de ciencia de datos al día hacia un punto final de contratación clara. Si bien es cierto que ciencia de datos es un ejercicio de investigación y comunicar la detección, que se va a tooclearly capaz de estas tareas tooyour equipo y sus clientes mediante un conjunto bien definido de artefactos de plantillas estándar de los empleados pueden ayudar a evitar malentendido y aumentar las posibilidades de saludo de la finalización correcta de un proyecto de ciencia de datos complejos.

## <a name="next-steps"></a>Pasos siguientes
Completa-to-end tutoriales que muestran todos los pasos de hello en proceso de Hola para **escenarios concretos** también se proporcionan. Se enumeran y vinculados con descripciones en miniatura en hello [tutoriales de proceso de ciencia de datos de equipo](data-science-process-walkthroughs.md) tema.

