---
title: "API de detección de anomalías de aprendizaje de máquina aaaAzure | Documentos de Microsoft"
description: "La API de detección de anomalías es un ejemplo integrado en Aprendizaje automático de Microsoft Azure que detecta anomalías en los datos de serie temporales con valores numéricos espaciados de manera uniforme en el tiempo."
services: machine-learning
documentationcenter: 
author: alokkirpal
manager: jhubbard
editor: cgronlun
ms.assetid: 52fafe1f-e93d-47df-a8ac-9a9a53b60824
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/05/2017
ms.author: alok;rotimpe
ms.openlocfilehash: ce153689b8ddb36b67a2ad3607d846ea83ebcf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-anomaly-detection-api"></a>API de detección de anomalías de Machine Learning
## <a name="overview"></a>Información general
La [API de detección de anomalías](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2) es un ejemplo integrado en Azure Machine Learning que detecta anomalías en los datos de serie temporales con valores numéricos espaciados de manera uniforme en el tiempo.

Esta API puede detectar los siguientes tipos de patrones anómalos en los datos de serie temporal de Hola:

* **Tendencias positivas y negativas**: por ejemplo, al supervisar el uso de memoria en informática, una tendencia al alza puede resultar interesante porque puede ser indicativa de una pérdida de memoria.
* **Cambios en el intervalo dinámico de Hola de valores**: por ejemplo, al supervisar excepciones de hello iniciadas por un servicio de nube, los cambios en el intervalo dinámico de Hola de valores pudieron indicar inestabilidad en estado de Hola de servicio de hello, y
* **Cambios abruptos e interrupciones**: por ejemplo, al supervisar el número de Hola de errores de inicio de sesión en un servicio o de desprotecciones en un sitio de comercio electrónico, picos o DIP pudieron indicar un comportamiento anómalo.

Estos detectores de aprendizaje automático realizan un seguimiento de dichos cambios en los valores con el paso del tiempo e informan de los cambios continuados en sus valores con puntuaciones de anomalías. No requieren ajuste del umbral "ad hoc" y sus puntuaciones pueden ser falsos positivos toocontrol usado. detección de anomalías de Hello API es útil en varios escenarios como la supervisión del servicio de seguimiento de KPI con el tiempo, uso de supervisión a través de las métricas como el número de búsquedas, número de clics, supervisión del rendimiento a través de contadores como archivo de memoria, CPU, lecturas, etc. con el tiempo.

oferta de detección de anomalías de Hello incluye tooget herramientas útiles que se inició.

* Hola [aplicación web](http://anomalydetection-aml.azurewebsites.net/) le ayuda a evaluar y visualizar los resultados de Hola de API de detección de anomalías en los datos.

> [!NOTE]
> Pruebe **IT Anomaly Insights solution** de [esta API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2).
> 
> tooget esta solución de tooend final implementado tooyour suscripción de Azure <a href="https://gallery.cortanaintelligence.com/Solution/Anomaly-Detection-Pre-Configured-Solution-1" target="_blank"> **empiece aquí >**</a>
> 
>

## <a name="api-deployment"></a>Implementación de la API
Hola de orden toouse API, debe implementarlo tooyour suscripción de Azure donde se hospedará como un servicio web de aprendizaje automático de Azure.  Puede hacerlo desde hello [Cortana Intelligence galería](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2).  Esta acción implementará dos servicios Web de aprendizaje automático de Azure (y sus recursos relacionados) tooyour suscripción de Azure: una para la detección de anomalías con detección de la estacionalidad y otra sin la detección de estacionalidad.  Cuando haya completado la implementación de hello, podrá toomanage capaz de las API de hello [servicios web de aprendizaje automático de Azure](https://services.azureml.net/webservices/) página.  Desde esta página, se ser capaz de toofind las ubicaciones de punto de conexión, las claves de API, así como código de ejemplo para llamar a API de Hola.  Puede encontrar instrucciones más detalladas [aquí](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice).

## <a name="scaling-hello-api"></a>API de Hola de ajuste de escala
De forma predeterminada, la implementación tendrá un plan de facturación de desarrollo y pruebas gratuito que incluye 1000 transacciones al mes y 2 horas de proceso al mes.  Puede actualizar el plan de tooanother según sus necesidades.  Los detalles sobre los precios de Hola de distintos planes están disponibles [aquí](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) en "Precios de API Web de producción".

## <a name="managing-aml-plans"></a>Administración de los planes de AML 
Puede administrar el plan de facturación [aquí](https://services.azureml.net/plans/).  nombre del plan de Hola se basará en el nombre del grupo de recursos de Hola que eligió al implementar la API de hello, además de una cadena que es el único tooyour suscripción.  Obtener instrucciones sobre cómo tooupgrade su plan están disponibles [aquí](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice) en la sección "Administrar planes de facturación" de Hola.

## <a name="api-definition"></a>Definición de la API
servicio web Hello proporciona una API basada en REST a través de HTTPS que se pueden usar de maneras diferentes, incluida una web o aplicación móvil, R, Python, Excel, etcetera.  Enviar tiempo serie toothis servicio de datos a través de una llamada de API de REST, y se ejecuta una combinación de los tres tipos de anomalías Hola que se describe a continuación.

## <a name="calling-hello-api"></a>Llamar a API de Hola
Hola de orden toocall API, necesitará ubicación de punto de conexión de tooknow hello y clave de API.  Ambos de estos, junto con el código de ejemplo para llamar a la API de hello, están disponibles en hello [servicios web de aprendizaje automático de Azure](https://services.azureml.net/webservices/) página.  Navegar por la API de toohello deseado y, a continuación, haga clic en toofind de pestaña "Usar" hello ellos.  Tenga en cuenta que puede llamar a la API de hello como una API de Swagger (es decir, con el parámetro de dirección URL de hello `format=swagger`) o como una API no Swagger (es decir, sin hello `format` parámetro de dirección URL).  código de ejemplo de Hola utiliza el formato de Swagger de Hola.  A continuación se muestra una solicitud de ejemplo y una respuesta en formato no Swagger.  Estos ejemplos son el punto de conexión de toohello estacionalidad.  el punto de conexión de Hello no estacionalidad es similar.

### <a name="sample-request-body"></a>Cuerpo de solicitud de ejemplo
solicitud de Hello contiene dos objetos: `Inputs` y `GlobalParameters`.  En la solicitud de ejemplo Hola a continuación, algunos parámetros se envían explícitamente mientras que otros no lo están (desplácese hacia abajo para obtener una lista completa de parámetros para cada punto de conexión).  Parámetros que no se envían explícitamente en la solicitud de Hola usará los valores predeterminados de hello indicados a continuación.

    {
                "Inputs": {
                        "input1": {
                                "ColumnNames": ["Time", "Data"],
                                "Values": [
                                        ["5/30/2010 18:07:00", "1"],
                                        ["5/30/2010 18:08:00", "1.4"],
                                        ["5/30/2010 18:09:00", "1.1"]
                                ]
                        }
                },
        "GlobalParameters": {
            "tspikedetector.sensitivity": "3",
            "zspikedetector.sensitivity": "3",
            "bileveldetector.sensitivity": "3.25",
            "detectors.spikesdips": "Both"
        }
    }

### <a name="sample-response"></a>Respuesta de ejemplo
Tenga en cuenta que, en Hola de orden toosee `ColumnNames` campo, debe incluir `details=true` como un parámetro de dirección URL en la solicitud.  Ver tablas de Hola a continuación para el significado de Hola a todos estos campos.

    {
        "Results": {
            "output1": {
                "type": "table",
                "value": {
                    "Values": [
                        ["5/30/2010 6:07:00 PM", "1", "1", "0", "0", "-0.687952590518378", "0", "-0.687952590518378", "0", "-0.687952590518378", "0"],
                        ["5/30/2010 6:08:00 PM", "1.4", "1.4", "0", "0", "-1.07030497733224", "0", "-0.884548154298423", "0", "-1.07030497733224", "0"],
                        ["5/30/2010 6:09:00 PM", "1.1", "1.1", "0", "0", "-1.30229513613974", "0", "-1.173800281031", "0", "-1.30229513613974", "0"]
                    ],
                    "ColumnNames": ["Time", "OriginalData", "ProcessedData", "TSpike", "ZSpike", "BiLevelChangeScore", "BiLevelChangeAlert", "PosTrendScore", "PosTrendAlert", "NegTrendScore", "NegTrendAlert"],
                    "ColumnTypes": ["DateTime", "Double", "Double", "Double", "Double", "Double", "Int32", "Double", "Int32", "Double", "Int32"]
                }
            }
        }
    }


## <a name="score-api"></a>API de puntuación
Hola API de puntuación se utiliza para ejecutar la detección de anomalías en los datos de serie temporal no estacionales. Hola API ejecuta una serie de detección de anomalías en los datos de Hola y devuelve sus puntuaciones de anomalías. Hola siguiente ilustración muestra un ejemplo de las anomalías que Hola que puede detectar la API de puntuación. Esta serie temporal tiene 2 cambios de nivel distintos y 3 picos. puntos de Hello rojo muestran el tiempo de hello en qué Hola se detecta el cambio del nivel de, mientras que los puntos de hello negro muestran picos de hello detectado.
![API de puntuación][1]

### <a name="detectors"></a>Detectores
detección de anomalías de Hello API es compatible con detectores en 3 categorías generales. Obtener más información sobre los parámetros de entrada específicos y los resultados de cada detector puede encontrarse en hello en la tabla siguiente.

| Categoría del detector | Detector | Description | Parámetros de entrada | Salidas |
| --- | --- | --- | --- | --- |
| Detectores de pico |Detector de TSpike |Detectar picos y DIP en función de hello lejano valores están comprendidos entre el primer y el tercer cuartil |*tspikedetector.Sensitivity:* toma el valor entero en el intervalo de saludo predeterminado de 1 a 10: 3; Los valores más altos filtrará los valores extremos más realizar menos sensibles |TSpike: valores binarios: '1' si se detecta un pico o una interrupción, '0' en caso contrario |
| Detectores de pico | Detector de ZSpike |Detectar picos y DIP en función de la diferencia entre puntos de hello son de su Media |*zspikedetector.Sensitivity:* tomar el valor entero en el intervalo de saludo predeterminado de 1 a 10,: 3; Los valores más altos filtrará los valores extremos más realizar menos sensibles |ZSpike: valores binarios: '1' si se detecta un pico o una interrupción, si no '0' | |
| Detector de tendencia lenta |Detector de tendencia lenta |Detectar lenta tendencia positiva según la sensibilidad del conjunto de Hola |*trenddetector.Sensitivity:* umbral de puntuación de detector (valor predeterminado: 3,25, 3,25 – 5 es un tooselect intervalo razonable de; Hola Hola superior menos sensible) |tscore: número flotante que representa la puntuación de anomalías en la tendencia |
| Detectores de cambio de nivel | Detector de cambio de nivel bidireccional |Detectar cambio hacia arriba y hacia abajo nivel según la sensibilidad del conjunto de Hola |*bileveldetector.Sensitivity:* umbral de puntuación de detector (valor predeterminado: 3,25, 3,25 – 5 es un tooselect intervalo razonable de; Hola Hola superior menos sensible) |rpscore: número flotante que representa la puntuación de anomalía en el cambio de nivel ascendente y descendente | |

### <a name="parameters"></a>parameters
Información más detallada sobre estos parámetros de entrada aparece en la tabla de hello siguiente:

| Parámetros de entrada | Description | Configuración predeterminada | Tipo | Intervalo válido | Intervalo sugerido |
| --- | --- | --- | --- | --- | --- |
| detectors.historyWindow |Historial (en número de puntos de datos) utilizado para el cálculo de la puntuación de anomalía |500 |integer |10-2000 |Dependiente de la serie temporal |
| detectors.spikesdips | Si toodetect solo tiene un pico, solo DIP, o ambos |Ambos |enumerated |Ambos, subidas, bajadas |Ambos |
| bileveldetector.sensitivity |Sensibilidad del detector de cambio de nivel bidireccional. |3.25 |double |None |3.25-5 (cuanto menores sean los valores, mayor es la sensibilidad) |
| trenddetector.sensitivity |Sensibilidad del detector de tendencia positiva. |3.25 |double |None |3.25-5 (cuanto menores sean los valores, mayor es la sensibilidad) |
| tspikedetector.sensitivity |Sensibilidad del detector TSpike |3 |integer |1-10 |3-5 (cuanto menores sean los valores, mayor es la sensibilidad) |
| zspikedetector.sensitivity |Sensibilidad del detector ZSpike |3 |integer |1-10 |3-5 (cuanto menores sean los valores, mayor es la sensibilidad) |
| postprocess.tailRows |Número de datos más recientes de hello puntos toobe mantienen en los resultados de la salida de hello |0 |integer |0 (mantenga todos los puntos de datos), o especifique el número de puntos tookeep en los resultados |N/D |

### <a name="output"></a>Salida
Hola API ejecuta todos los detectores en los datos de serie temporal y devuelve las puntuaciones de anomalías e indicadores de pico binario para cada punto en el tiempo. Hola tabla siguiente enumeran salidas de hello API. 

| Salidas | Description |
| --- | --- |
| Hora |Marcas de tiempo de datos sin procesar, o datos agregados (o) atribuidos si se aplica la agregación (o) atribución de los datos que faltan |
| Datos |Valores de datos sin procesar, o datos agregados (o) atribuidos si se aplica la agregación (o) atribución de los datos que faltan |
| TSpike |Indicador binario tooindicate si se detecta un pico TSpike Detector |
| ZSpike |Indicador binario tooindicate si se detecta un pico ZSpike Detector |
| rpscore |Número flotante que representa la puntuación de anomalía en el cambio de nivel bidireccional |
| rpalert |valor de 1/0 que indica un nivel bidireccional cambiar anomalías según su importancia entrada Hola |
| tscore |Número flotante que representa la puntuación de anomalía en tendencia positiva |
| talert |valor de 1/0 que se indica es un anomalías de tendencia positiva según su importancia entrada Hola |

## <a name="scorewithseasonality-api"></a>La API ScoreWithSeasonality
Hola ScoreWithSeasonality API se utiliza para ejecutar la detección de anomalías de serie temporal que tienen patrones estacionales. Esta API es útil toodetect desviaciones en patrones estacionales.  
Hello en la ilustración siguiente se muestra un ejemplo de anomalías detectado en una serie de tiempo periódico. serie temporal de Hello tiene un pico (punto negro 1 de hello), dos DIP (punto 2 º negro de hello y otro final Hola) y un cambio del nivel (punto rojo). Tenga en cuenta que ambos Hola dip en medio de Hola de serie temporal de Hola y cambio del nivel de hello solo perceptible después de quitaron componentes de temporada de serie de Hola.
![API de estacionalidad][2]

### <a name="detectors"></a>Detectores
los detectores de Hello en el punto de conexión de hello estacionalidad son toohello similar que en el punto de conexión de hello no estacionalidad, pero con nombres de parámetro ligeramente diferentes (incluidos más abajo).

### <a name="parameters"></a>parameters

Información más detallada sobre estos parámetros de entrada aparece en la tabla de hello siguiente:

| Parámetros de entrada | Description | Configuración predeterminada | Tipo | Intervalo válido | Intervalo sugerido |
| --- | --- | --- | --- | --- | --- |
| preprocess.aggregationInterval |Intervalo de agregación en segundos para agregar series temporales de entrada |0 (no se realiza ninguna agregación) |integer |0: omitir agregación, de lo contrario, > 0 |día de too1 de 5 minutos, dependiente de la serie temporal |
| preprocess.aggregationFunc |Función que se usa para agregar datos en hello especificado AggregationInterval |mean |enumerated |mean, sum, length |N/D |
| preprocess.replaceMissing |Valores utilizan tooimpute los datos que faltan |lkv (último valor conocido) |enumerated |zero, lkv, mean |N/D |
| detectors.historyWindow |Historial (en número de puntos de datos) utilizado para el cálculo de la puntuación de anomalía |500 |integer |10-2000 |Dependiente de la serie temporal |
| detectors.spikesdips | Si toodetect solo tiene un pico, solo DIP, o ambos |Ambos |enumerated |Ambos, subidas, bajadas |Ambos |
| bileveldetector.sensitivity |Sensibilidad del detector de cambio de nivel bidireccional. |3.25 |double |None |3.25-5 (cuanto menores sean los valores, mayor es la sensibilidad) |
| postrenddetector.sensitivity |Sensibilidad del detector de tendencia positiva. |3.25 |double |None |3.25-5 (cuanto menores sean los valores, mayor es la sensibilidad) |
| negtrenddetector.sensitivity |Sensibilidad del detector de tendencia negativa. |3.25 |double |None |3.25-5 (cuanto menores sean los valores, mayor es la sensibilidad) |
| tspikedetector.sensitivity |Sensibilidad del detector TSpike |3 |integer |1-10 |3-5 (cuanto menores sean los valores, mayor es la sensibilidad) |
| zspikedetector.sensitivity |Sensibilidad del detector ZSpike |3 |integer |1-10 |3-5 (cuanto menores sean los valores, mayor es la sensibilidad) |
| seasonality.enable |Si el análisis de estacionalidad está toobe realizadas |true |boolean |true, false |Dependiente de la serie temporal |
| seasonality.numSeasonality |Número máximo de toobe ciclos periódicos detectado |1 |integer |1, 2 |1-2 |
| seasonality.transform |Si los componentes de tendencia (y) estacionales se eliminarán antes de aplicar la detección de anomalías |deseason |enumerated |none, deseason, deseasontrend |N/D |
| postprocess.tailRows |Número de datos más recientes de hello puntos toobe mantienen en los resultados de la salida de hello |0 |integer |0 (mantenga todos los puntos de datos), o especifique el número de puntos tookeep en los resultados |N/D |

### <a name="output"></a>Salida
Hola API ejecuta todos los detectores en los datos de serie temporal y devuelve las puntuaciones de anomalías e indicadores de pico binario para cada punto en el tiempo. Hola tabla siguiente enumeran salidas de hello API. 

| Salidas | Description |
| --- | --- |
| Hora |Marcas de tiempo de datos sin procesar, o datos agregados (o) atribuidos si se aplica la agregación (o) atribución de los datos que faltan |
| OriginalData |Valores de datos sin procesar, o datos agregados (o) atribuidos si se aplica la agregación (o) atribución de los datos que faltan |
| ProcessedData |Cualquiera de hello siguientes: <ul><li>Serie temporal ajustada estacionalmente si se ha detectado una estacionalidad importante y se ha seleccionado la opción deseason.</li><li>Serie temporal ajustada estacionalmente y con anulación de tendencia (detrended) si se ha detectado una estacionalidad importante y se ha seleccionado la opción deseasontrend;</li><li>en caso contrario, es Hola igual que OriginalData</li> |
| TSpike |Indicador binario tooindicate si se detecta un pico TSpike Detector |
| ZSpike |Indicador binario tooindicate si se detecta un pico ZSpike Detector |
| BiLevelChangeScore |Número flotante que representa la puntuación de anomalía en el cambio de nivel |
| BiLevelChangeAlert |1/0 valor indica que se está un anomalías de cambio del nivel según su importancia entrada Hola |
| PosTrendScore |Número flotante que representa la puntuación de anomalía en tendencia positiva |
| PosTrendAlert |valor de 1/0 que se indica es un anomalías de tendencia positiva según su importancia entrada Hola |
| NegTrendScore |Número flotante que representa la puntuación de anomalía en tendencia negativa |
| NegTrendAlert |valor de 1/0 que se indica es un anomalías de tendencia negativa según su importancia entrada Hola |

[1]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-score.png
[2]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-seasonal.png

