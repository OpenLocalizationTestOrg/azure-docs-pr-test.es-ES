---
title: "Regresión lineal en el aprendizaje automático de aaaUsing | Documentos de Microsoft"
description: "Una comparación de los modelos de regresión lineal en Excel y en Estudio de aprendizaje automático de Azure"
metakeywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 417ae6ab-de4f-4bdd-957a-d96133234656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: kbaroni;garye
ms.openlocfilehash: 8716040ad296053a72fb06c7c9660a186123ac15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-linear-regression-in-azure-machine-learning"></a>Uso de regresión lineal en Aprendizaje automático de Azure
> *Kate Baroni* y *Ben Boatman* son arquitectos de soluciones para empresas del Centro de Excelencia de Perspectivas sobre los datos de Microsoft. En este artículo, describe su experiencia de migrar una regresión analysis suite tooa basada en la nube solución existente mediante el aprendizaje automático de Azure. 
> 
> 

&nbsp; 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="goal"></a>Objetivo
Nuestro proyecto se inició con dos objetivos en mente: 

1. Use la precisión de hello tooimprove de análisis predictivos de proyecciones de ingresos mensual de nuestra organización 
2. Usar aprendizaje automático de Azure tooconfirm, optimizar, aumentar la velocidad y la escala de los resultados. 

Como muchas empresas, nuestra organización pasa por un proceso de previsión de ingresos mensuales. Nuestro equipo pequeño de los analistas de negocios se ha asignado la tarea con el proceso de aprendizaje automático de Azure toosupport hello y mejora la exactitud de las proyecciones. equipo de Hello empleó varios meses de recopilación de datos de varios orígenes y ejecutada atributos de datos de hello mediante análisis estadísticos identificar atributos clave tooservices relevante ventas previsión. paso siguiente de Hello era modelos de regresión estadística de la creación de prototipos de toobegin en los datos de hello en Excel. Dentro de unas cuantas semanas, ha surgido un modelo de regresión de Excel que se superando campo actual de Hola y previsión procesos de finanzas. Se pasó a ser resultado de predicción de línea de base de Hola. 

A continuación, tomamos Hola siguiente paso toomoving nuestro análisis predictivo sobre toofind de aprendizaje automático de tooAzure out cómo podrían mejorar el aprendizaje automático en el rendimiento de predicción.

## <a name="achieving-predictive-performance-parity"></a>Consecución de la paridad en el rendimiento predictivo
Nuestra primera prioridad era tooachieve paridad entre los modelos de regresión de aprendizaje automático y Excel. Dados Hola los mismos datos y Hola mismo dividir para los datos de pruebas y entrenamiento, deseamos paridad de predicción del rendimiento de tooachieve entre Excel y el aprendizaje automático. Al principio no lo conseguimos. modelo de aprendizaje automático de Hola de Hello Excel superó el modelo. Error de Hello fue debido a falta de tooa de conocimiento de la herramienta de base de hello en aprendizaje automático. Después de una sincronización con el equipo de producto de aprendizaje automático de hello, obtener una mejor comprensión de hello base configuración necesaria para nuestros conjuntos de datos y lograr paridad entre dos modelos de Hola. 

### <a name="create-regression-model-in-excel"></a>Creación de un modelo de regresión en Excel
La regresión de Excel utiliza el modelo de regresión lineal estándar Hola de hello herramientas para análisis de Excel. 

Hemos calculado *% absoluto medio Error* y lo utilizó como medida de rendimiento de hello para el modelo de Hola. Se tardó tooarrive de 3 meses en un modelo de trabajo con Excel. Se pone mucho de aprendizaje de hello en hello experimentación de estudio de aprendizaje automático que en última instancia era beneficioso en la descripción de los requisitos.

### <a name="create-comparable-experiment-in-azure-machine-learning"></a>Creación de un experimento comparable en Aprendizaje automático de Azure
Seguimos estos pasos toocreate nuestro experimento en estudio de aprendizaje automático: 

1. Conjunto de datos de hello cargado como un tooMachine de archivo csv estudio de aprendizaje (archivo muy pequeño)
2. Crea un experimento de nuevo y utilizar hello [seleccionar columnas de conjunto de datos] [ select-columns] tooselect módulo Hola mismas características de datos usados en Excel 
3. Hola usado [dividir datos] [ split] módulo (con *expresión relativa* modo) datos de hello toodivide en Hola mismos conjuntos de datos de entrenamiento, tal y como hizo en Excel 
4. Experimentado con hello [regresión lineal] [ linear-regression] módulo (solo opciones predeterminadas), documentada y en comparación con el modelo de regresión de hello resultados tooour Excel

### <a name="review-initial-results"></a>Revisión de los resultados iniciales
En primer lugar, modelo de Excel hello claramente superó a modelo de estudio de aprendizaje automático de hello: 

|  | Excel | Estudio |
| --- |:---:|:---:|
| Rendimiento | | |
| <ul style="list-style-type: none;"><li>R cuadrado ajustado</li></ul> |0,96 |N/D |
| <ul style="list-style-type: none;"><li>Coeficiente de <br />Determinación</li></ul> |N/D |0,78<br />(baja precisión) |
| Error medio absoluto |9,5 millones de $ |19,4 millones de $ |
| Error medio absoluto (%) |6,03 % |12,2 % |

Cuando ejecutamos nuestro proceso y los resultados por los desarrolladores de Hola y científicos de datos en el equipo de aprendizaje automático de hello, rápidamente proporcionan algunas sugerencias útiles. 

* Cuando usas hello [regresión lineal] [ linear-regression] módulo en estudio de aprendizaje automático, se proporcionan dos métodos:
  * Descenso de gradiente en línea: pueden resultar más adecuado para los problemas a mayor escala.
  * Mínimos cuadrados ordinarios: Se trata de método hello que considerar mayoría de los usuarios cuando oye regresión lineal. Para los conjuntos de datos más pequeños, la regresión ordinaria de mínimos cuadrados puede ser una opción más adecuada.
* Considere la posibilidad de aumentar el rendimiento de tooimprove de parámetro de peso de regularización L2 Hola. Too0.001 se establece de forma predeterminada, pero en nuestro conjunto de datos pequeño se establézcalo too0.005 tooimprove rendimiento. 

### <a name="mystery-solved"></a>¡Misterio resuelto!
Cuando se aplican las recomendaciones de hello, se consigue Hola mismo rendimiento de línea de base en estudio de aprendizaje automático como con Excel: 

|  | Excel | Studio (inicial) | Studio con mínimos cuadrados |
| --- |:---:|:---:|:---:|
| Valor etiquetado |Valores reales (numéricos) |same |same |
| Objetivo del aprendizaje |Excel -> Análisis de datos -> Regresión |Regresión lineal |Regresión lineal |
| Opciones del objetivo del aprendizaje |N/D |Valores predeterminados |ordinaria de mínimos cuadrados<br />L2 = 0,005 |
| Conjunto de datos |26 filas, 3 características, 1 etiqueta. Todas numéricas. |same |same |
| División: aprendizaje |Excel había entrenado en hello primero 18 filas, se comprueba en hello última 8 filas. |same |same |
| División: prueba |Fórmula de regresión aplicada de Excel toohello última 8 filas |same |same |
| **Rendimiento** | | | |
| R cuadrado ajustado |0,96 |N/D | |
| Coeficiente de determinación |N/D |0,78 |0,952049 |
| Error medio absoluto |9,5 millones de $ |19,4 millones de $ |9,5 millones de $ |
| Error medio absoluto (%) |<span style="background-color: 00FF00;"> 6,03 %</span> |12,2 % |<span style="background-color: 00FF00;"> 6,03 %</span> |

Además, coeficientes de Excel hello también comparan pesos de característica toohello Hola entrenado Azure:

|  | Coeficientes de Excel | Ponderaciones de la característica de Azure |
| --- |:---:|:---:|
| Intersección/sesgo |19 470 209,88 |19 328 500 |
| Característica A |0,832653063 |0,834156 |
| Característica B |11 071 967,08 |11 007 300 |
| Característica C |25 383 318,09 |25 140 800 |

## <a name="next-steps"></a>Pasos siguientes
Deseamos que el servicio de web de aprendizaje automático de tooconsume hello en Excel. Nuestro los analistas de negocios se basan en Excel y se necesita un Hola de toocall forma aprendizaje automático de servicio con una fila de datos de Excel web y hacer que devuelva Hola predecir tooExcel de valor. 

También deseamos toooptimize nuestro modelo, con opciones de Hola y algoritmos disponibles en estudio de aprendizaje automático.

### <a name="integration-with-excel"></a>Integración con Excel
Nuestra solución era toooperationalize nuestro regresión de aprendizaje automático de modelo creando un servicio web desde el modelo entrenado Hola. Dentro de unos minutos, se creó el servicio web de Hola y lo podríamos llamamos directamente desde Excel tooreturn un valor de predicción de ingresos. 

Hola *panel de servicios Web* sección incluye un libro de Excel que se pueden descargar. libro de Hola incluye hello web servicio API y el esquema de información incrustada con formato previo. Al hacer clic en *descargar el libro de Excel*, Hola libro se abre y puede guardarlo tooyour de equipo local. 

![][1]

Abra el libro de hello, copie los parámetros predefinidos en la sección de parámetros de hello azul tal y como se muestra a continuación. Una vez que se especifican parámetros de hello, Excel llama toohello servicio web de aprendizaje automático y hello etiquetas con puntuación de predicción mostrará de sección de valores de predicción de hello verde. libro de Hello continuará toocreate predicciones para los parámetros en función del modelo entrenado para todos los elementos de fila que se ha indicado en parámetros. Para obtener más información sobre cómo toouse esta característica, consulte [consumir un servicio Web de Azure Machine Learning desde Excel](machine-learning-consuming-from-excel.md). 

![][2]

### <a name="optimization-and-further-experiments"></a>Optimización y otros experimentos
Ahora que tuvimos una línea base con nuestro modelo de Excel, se mueve toooptimize anticipada nuestro modelo de regresión lineal del aprendizaje automático. Hemos usado el módulo de hello [selección de características basada en filtros] [ filter-based-feature-selection] tooimprove en nuestra selección de elementos de datos iniciales y nos ayudaron a lograr una mejora del rendimiento de 4.6% significa la desviación. Para proyectos futuros usaremos esta característica lo que nos podría ahorrar semanas iterar a través de atributos toofind Hola derecho conjunto de datos de toouse de características para la modelización. 

A continuación tenemos previsto tooinclude algoritmos adicionales como [bayesiano] [ bayesian-linear-regression] o [árboles de decisión impulsado] [ boosted-decision-tree-regression] en nuestro toocompare de experimento rendimiento. 

Si desea que tooexperiment con regresión, un buen conjunto de datos tootry es dataset de ejemplo de regresión de eficacia energética hello, lo que tiene un gran número de atributos numéricos. conjunto de datos de Hola se proporciona como parte de los conjuntos de datos de ejemplo de Hola en estudio de aprendizaje automático. Puede utilizar una variedad de toopredict de módulos de aprendizaje carga calefacción o refrigeración carga. gráfico de Hello siguiente es que una comparación de rendimiento de diferentes de regresión aprende contra Hola eficiencia energética dataset predecir para hello carga variable refrigeración de destino: 

| Modelo | Error medio absoluto | Error cuadrático medio | Error absoluto relativo | Error cuadrático relativo | Coeficiente de determinación |
| --- | --- | --- | --- | --- | --- |
| Árbol de decisiones incrementados |0,930113 |1,4239 |0,106647 |0,021662 |0,978338 |
| Regresión lineal (descenso de gradiente) |2,035693 |2,98006 |0,233414 |0,094881 |0,905119 |
| Regresión de red neuronal |1,548195 |2,114617 |0,177517 |0,047774 |0,952226 |
| Regresión lineal (ordinaria de mínimos cuadrados) |1,428273 |1,984461 |0,163767 |0,042074 |0,957926 |

## <a name="key-takeaways"></a>Puntos clave
Hemos aprendido mucho al ejecutar experimentos de regresión en Excel y en Aprendizaje automático de Azure de forma paralela. Crear modelo de línea de base de hello en Excel y lo compara con aprendizaje automático de toomodels [regresión lineal] [ linear-regression] ayudado nos Obtenga información acerca de aprendizaje automático de Azure y encontramos datos tooimprove de oportunidades rendimiento de selección y el modelo. 

También encontramos que resulta aconsejable toouse [selección de características basada en filtros] [ filter-based-feature-selection] tooaccelerate proyectos de predicción futura. Mediante la aplicación de datos de tooyour de selección de características, puede crear un modelo mejorado en el aprendizaje automático con un mejor rendimiento global. 

Hola Hola de tootransfer capacidad predictivo analítica previsión sistémica de aprendizaje automático tooExcel permite un aumento significativo de hello capacidad toosuccessfully proporcionar resultados audiencia de usuarios empresariales amplia tooa. 

## <a name="resources"></a>Recursos
A continuación, encontrará algunos recursos que le ayudarán a trabajar con la regresión: 

* Regresión en Excel. Si nunca ha intentado realizar la regresión en Excel, este tutorial le facilitará el trabajo: [http://www.excel-easy.com/examples/regression.html](http://www.excel-easy.com/examples/regression.html)
* Regresión frente a previsión. Figura de ajedrez Tyler escribió un artículo de blog que explica cómo toodo tiempo pronóstico de series en Excel, que contiene la descripción de una buena para principiantes de regresión lineal. [http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts](http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts) 
* Regresión lineal ordinaria con mínimos cuadrados: errores, problemas y riesgos. Introducción y análisis sobre la regresión: [http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/ ](http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/)

[1]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-1.png
[2]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-2.png


<!-- Module References -->
[bayesian-linear-regression]: https://msdn.microsoft.com/library/azure/ee12de50-2b34-4145-aec0-23e0485da308/
[boosted-decision-tree-regression]: https://msdn.microsoft.com/library/azure/0207d252-6c41-4c77-84c3-73bdf1ac5960/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

