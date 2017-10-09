---
title: "Renovación de cliente mediante el aprendizaje automático de aaaAnalyzing | Documentos de Microsoft"
description: "Caso práctico de desarrollo de un modelo integrado para analizar y puntuar el abandono de clientes"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: 1333ffe2-59b8-4f40-9be7-3bf1173fc38d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 070e6a2ebe4f2fe439a42ffe1a3fa9d6d3788d62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a>Análisis del el abandono de clientes mediante el Aprendizaje automático de Azure
## <a name="overview"></a>Información general
En este artículo se presenta una implementación de referencia de un proyecto de análisis de pérdida de clientes creado mediante Azure Machine Learning. En este artículo, analizaremos modelos genéricos asociados para resolver holísticamente problema Hola de renovación de cliente industrial. Medimos también precisión Hola de modelos que se generan mediante el uso de aprendizaje automático, y se evaluación instrucciones para su posterior desarrollo.  

### <a name="acknowledgements"></a>Agradecimientos
Este experimento lo desarrolló y probó Serge Berger, principal científico de datos de Microsoft y Roger Barga, anterior director de productos para Aprendizaje automático de Microsoft Azure. equipo de documentación de Azure Hola expresar confirma su experiencia y gracias a ellos para compartir estas notas del producto.

> [!NOTE]
> datos de Hello utilizados para este experimento no están disponibles públicamente. Para obtener un ejemplo de cómo toobuild un aprendizaje automático de modelo para el análisis de renovación, consulte: [comercial renovación de plantilla de modelo](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) en [Cortana Intelligence Galería](http://gallery.cortanaintelligence.com/)
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-problem-of-customer-churn"></a>problema de Hola de renovación de cliente
Las empresas en el mercado de consumo de Hola y en todos los sectores de enterprise tienen toodeal con la renovación. En ocasiones el abandono es excesivo e influye sobre las decisiones políticas. soluciones tradicionales de Hello es toopredict churners de tendencia de alta y satisfacer sus necesidades a través de un servicio de soporte, las campañas de marketing o aplicando dispensas especial. Estos enfoques pueden variar desde sector tooindustry e incluso un tooanother de clúster de consumidor determinado dentro de un sector (por ejemplo, telecomunicaciones).

factor común de Hello es que las empresas necesitan toominimize estos intentos de retención especiales para los clientes. Por lo tanto, una metodología natural podría ser tooscore todos los clientes con probabilidad de Hola de renovación y tratan Hola principales N unos. los principales clientes de Hello podría ser Hola los más rentables; Por ejemplo, en escenarios más complejos, se emplea una función de beneficios durante la selección de Hola de candidatos para la exención especial. Sin embargo, estas consideraciones son solo una parte de la estrategia global de Hola para ocuparse de renovación. Las empresas también tienen tootake en riesgo de cuenta (y tolerancia al riesgo asociado), Hola nivel y el costo de intervención hello y segmentación de clientes plausible.  

## <a name="industry-outlook-and-approaches"></a>Perspectiva y enfoques de la industria
La gestión del abandono de forma adecuada es signo de madurez industrial. ejemplo clásico de Hello es sector de telecomunicaciones Hola donde los suscriptores son conocidos toofrequently conmutador de tooanother de un proveedor. Este abandono voluntario es realmente preocupante. Además, los proveedores acumuladas conocimientos importantes sobre *renovación controladores*, que son factores de Hola que tooswitch de los clientes de la unidad.

Por ejemplo, elección auricular o el dispositivo es un controlador conocido de actividad de negocio de teléfono móvil de Hola. Como resultado, una directiva popular es precio de hello toosubsidize de unos auriculares para nuevos suscriptores y cobrar una tooexisting precio completo a los clientes para realizar una actualización. Históricamente, esta directiva ha suscitado un salto de un proveedor tooanother tooget un descuento nuevo, que a su vez, ha hecho que los proveedores toorefine sus estrategias de toocustomers.

La alta volatilidad en las ofertas de terminales es un factor que invalida de manera muy rápida los modelos de abandono que se basan en los modelos de terminales actuales. Además, teléfonos móviles no son solo los dispositivos de telecomunicaciones; también son instrucciones de manera (se recomienda Hola iPhone), y estas predicciones sociales son fuera ámbito Hola de conjuntos de datos de telecomunicaciones regular.

resultado de Hello para el modelado es que no se debe definir una directiva de sonido eliminando motivos conocidos para la renovación. De hecho, es **obligatorio**establecer una estrategia de modelado continua, que incluye modelos clásicos que cuantifican variables de categorías (por ejemplo, árboles de decisión).

Con grandes conjuntos de datos en sus clientes, las organizaciones son realizar análisis de grandes cantidades de datos (en particular, en función de grandes cantidades de datos de detección de renovación) como un problema de toohello enfoque efectivo. Puede encontrar más información acerca del problema de toohello de enfoque de hello grandes cantidades de datos de renovación en hello recomendaciones sobre la sección ETL.  

## <a name="methodology-toomodel-customer-churn"></a>Renovación de metodología toomodel del cliente
Una comunes para solucionar problemas proceso toosolve cliente renovación se muestra en las figuras 1-3:  

1. Un modelo de riesgos permite tooconsider cómo afectan a las acciones probabilidad y el riesgo.
2. Un modelo de intervención permite tooconsider cómo nivel Hola de intervención podría afectar a la probabilidad de Hola de hello y renovación de cantidad del valor de duración de cliente (CLV).
3. Este análisis presta tooa cualitativos analysis que sea automático campaña de marketing concentrados tooa que tenga como destino oferta óptimo de cliente segmentos toodeliver Hola.  

![][1]

Este enfoque hacia delante la claridad es Hola mejor manera tootreat la renovación, pero se trata de complejidad: tenemos toodevelop un varios modelos Arquetipo y seguimiento de las dependencias entre los modelos de Hola. interacción de Hello entre los modelos se puede encapsular tal como se muestra en hello siguiente diagrama:  

![][2]

*Ilustración 4: Arquetipo basado en varios modelos unificado*  

Interacción entre los modelos de hello es clave si estamos toodeliver una retención de toocustomer enfoque integral. Cada modelo necesariamente empeora con el tiempo; por lo tanto, arquitectura de hello es un bucle implícita (similar Arquetipo toohello conjunto estándar de minería de datos de hello CRISP-DM, [***3***]).  

Hello ciclo general de marketing de decisión de riesgo segmentación/descomposición sigue siendo una estructura generalizada, que es aplicable toomany los problemas empresariales. Análisis de renovación es simplemente un representante de seguro de este grupo de problemas porque exhibe todos los rasgos de Hola de un problema de negocios compleja que no permite una solución de predicción simplificada. Hola social aspectos de hello enfoque moderno toochurn no se resaltan especialmente en el enfoque de hello, pero aspectos sociales Hola se encapsulan en Arquetipo de modelado de hello, como se haría en cualquier modelo.  

Un interesante aporte aquí es el análisis de Big Data. Las empresas de hoy en día de telecomunicaciones y comercial recopilan datos exhaustivas sobre sus clientes, y nos podemos prevé fácilmente esa Hola necesita Hola para conectividad de varios modelo se convertirá en una tendencia común, dada apareciendo como las tendencias de Internet de las cosas y dispositivos ubicuos, lo que permite a business tooemploy soluciones inteligentes en varios niveles.  

 

## <a name="implementing-hello-modeling-archetype-in-machine-learning-studio"></a>Implementar Hola modelado Arquetipo en estudio de aprendizaje automático
Dado el problema de Hola que acabamos de describir, ¿qué es Hola mejor manera tooimplement un modelo integrado y un nuevo enfoque de puntuación? En esta sección, demostraremos cómo lo hemos conseguido mediante Azure Machine Learning Studio.  

enfoque de varios modelos de Hello es obligatorio cuando se diseña un Arquetipo global para la renovación. Hola incluso puntuación (predicción) parte del enfoque de hello debe ser varios modelo.  

Hello siguiente diagrama muestra el prototipo de hello que creamos, que emplea cuatro algoritmos de puntuación de renovación de toopredict de estudio de aprendizaje automático. razón de Hola para utilizar un enfoque de varios modelo es toocreate una precisión de conjunto clasificador tooincrease pero tooprotect frente a sobreajustar y selección de características preceptivas de tooimprove.  

![][3]

*Ilustración 5: Prototipo de un enfoque de creación de modelos de abandono*  

Hello las secciones siguientes proporcionan más detalles acerca de la puntuación del modelo que se implementa mediante el uso de estudio de aprendizaje automático de prototipo de Hola.  

### <a name="data-selection-and-preparation"></a>Selección y preparación de los datos
datos de Hello usan modelos de hello toobuild y los clientes de puntuación se obtuvo de una solución CRM vertical, con la privacidad de los clientes de hello datos ofuscados tooprotect. datos Hello contienen información sobre 8.000 suscripciones Hola EE. UU., y combina tres orígenes: aprovisionamiento de datos (metadatos de suscripción), datos de actividad (uso del sistema de hello) y datos de soporte técnico al cliente. Hola datos no incluyen cualquier negocio relacionados con la información sobre los clientes de hello; Por ejemplo, no incluye las puntuaciones de metadatos o el crédito de fidelidad.  

Por motivos de simplicidad, los procesos de ETL y de limpieza de datos escapan de nuestro ámbito dado que se supone que la preparación de los datos ya se ha realizado en otra parte.   

Selección de características de modelado se basa en la puntuación de importancia preliminar de conjunto de Hola de predicción, incluidos en el proceso de Hola que usa el módulo de bosque aleatorio de Hola. Para la implementación de hello en estudio de aprendizaje automático, se calculan Hola Media, mediana e intervalos para características representativas. Por ejemplo, hemos agregado agregados para los datos cualitativa hello, como los valores mínimos y máximo para la actividad de usuario.    

También se captura información de tiempo para hello seis meses más recientes. Hemos analizado los datos durante un año y se establece que, incluso si hubiera tendencias estadísticamente significativas, efecto de hello en la renovación de se reduce en gran medida después de seis meses.  

Hola más importante es Hola todo ese proceso, incluidos ETL, selección de características, y modelado se implementó en estudio de aprendizaje automático, usar orígenes de datos de Microsoft Azure.   

Hello diagramas siguientes muestran datos Hola que se utilizan.  

![][4]

*Ilustración 6: Extracto de la fuente de datos (oculta)*  

![][5]

*Ilustración 7: Características extraídas de la fuente de datos*
 

> Tenga en cuenta que estos datos están privados y, por tanto, no se puede compartir datos y el modelo de Hola.
> Sin embargo, para un modelo similar mediante datos públicamente disponibles, vea este experimento de ejemplo Hola [Galería de inteligencia de Cortana](http://gallery.cortanaintelligence.com/): [renovación de cliente de telecomunicaciones](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383).
> 
> toolearn más información acerca de cómo puede implementar un modelo de análisis de renovación con Cortana Intelligence Suite, también se recomienda [este vídeo](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) por el jefe de programa sénior oeste Hyong Tok. 
> 
> 

### <a name="algorithms-used-in-hello-prototype"></a>Algoritmos usados en el prototipo de Hola
Utilizamos Hola después de cuatro algoritmos de aprendizaje automático prototipo de hello toobuild (no hay ninguna personalización):  

1. Regresión logística (LR)
2. Árbol de decisiones ampliado (BT)
3. Perceptron promediado (AP)
4. Máquina de vectores de soporte (SVM)  

Hello siguiente diagrama muestra una parte de la superficie de diseño de experimento hello, que indica la secuencia de hello en qué Hola crearon modelos:  

![][6]  

*Ilustración 8: Creación de modelos en Estudio de aprendizaje automático*  

### <a name="scoring-methods"></a>Métodos de puntuación
Se puntúan los modelos de hello cuatro mediante el uso de un conjunto de datos de entrenamiento etiquetado.  

También se envía Hola puntuar modelo comparables del tooa conjunto de datos generado mediante la edición de escritorio de Hola de SAS Enterprise extractor de 12. Se mide la precisión de hello del modelo SAS de Hola y todos los modelos de estudio de aprendizaje automático de cuatro.  

## <a name="results"></a>Results
En esta sección, presentamos nuestras conclusiones acerca de la precisión de Hola de modelos de hello, en función de Hola la puntuación del conjunto de datos.  

### <a name="accuracy-and-precision-of-scoring"></a>Exactitud y precisión de la puntuación
Por lo general, la implementación de hello en aprendizaje automático de Azure está detrás de SAS en precisión aproximadamente 10-15% (área en curva o AUC).  

Sin embargo, métrica más importante de hello en la renovación de es la tasa de clasificaciones incorrectas de hello: es decir, de churners de top N hello como predicción clasificador de hello, cuál de ellos hizo **no** renovación y ha recibido un tratamiento especial? Hola diagrama siguiente compara esta velocidad de clasificaciones incorrectas para todos los modelos de hello:  

![][7]

*Ilustración 9: Área del prototipo de Passau situada bajo la curva*

### <a name="using-auc-toocompare-results"></a>Uso de AUC toocompare resultados
Área en curva (AUC) es una medida que representa una medida global de *cláusula de salvedad* entre las distribuciones de Hola de puntuaciones para rellenados positivos y negativos. Es similar toohello gráfico de característica de operador de receptor (ROC) tradicionales, pero una diferencia importante es que esa métrica AUC hello no requiere toochoose un valor de umbral. En su lugar, resume los resultados de hello sobre **todos los** opciones posibles. En contraste, gráfico ROC tradicional de hello muestra la tasa positivo de hello en el eje vertical de Hola y Hola de falsos positivos en el eje horizontal de Hola y Hola clasificación umbral varía.   

AUC suele utilizarse como una medida de vale la pena para algoritmos diferentes (o distintos sistemas) porque permite comparar por medio de sus valores AUC de toobe de modelos. Se trata de un enfoque popular en sectores como la meteorología y las biociencias. Por lo tanto, AUC representa una herramienta generalizada para la evaluación del rendimiento del clasificador.  

### <a name="comparing-misclassification-rates"></a>Comparación de las tasas de clasificaciones incorrectas
Se comparan las tasas de clasificaciones incorrectas de hello en hello en cuestión del conjunto de datos mediante el uso de datos CRM de saludo de aproximadamente 8.000 suscripciones.  

* tasa de clasificaciones incorrectas de SAS de Hello era de 10 a 15%.
* tasa de clasificaciones incorrectas de estudio de aprendizaje automático de Hello era 15-20% para churners de hello top 200-300.  

En el sector de telecomunicaciones hello, es importante tooaddress solo los clientes que tienen Hola toochurn de riesgo más alto, ya que les ofrece un servicio de supervisor u otro tratamiento especial. En ese sentido, implementación de estudio de aprendizaje automático de Hola obtiene resultados a la par de modelo de hello SAS.  

Por hello mismo símbolo (token), la precisión es más importante que la precisión porque principalmente nos interesa correctamente clasificar churners posibles.  

Hola siguientes diagrama de Wikipedia muestra la relación de hello en un gráfico muy interesante y fácil de entender:  

![][8]

*Ilustración 10: Balance entre exactitud y precisión*

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a>Resultados de precisión del modelo de árbol de decisiones ampliado
Hola siguiente gráfico muestra hello sin procesar el resultado de puntuación mediante el prototipo de aprendizaje automático de hello para el modelo de árbol de decisión de hello impulsado, lo que sucede toobe Hola sean más preciso entre cuatro modelos de hello:  

![][9]

*Ilustración 11: Características del modelo de árbol de decisión ampliado*

## <a name="performance-comparison"></a>Comparación del rendimiento
Se compara la velocidad de hello en el que se puntúan datos utilizando modelos de estudio de aprendizaje automático de Hola y un modelo comparable creados mediante la edición de escritorio de Hola de SAS Enterprise extractor 12.1.  

Hello en la tabla siguiente resume el rendimiento de Hola de algoritmos de hello:  

*Tabla 1. Rendimiento general (precisión) de algoritmos de Hola*

| LR | BT | AP | SVM |
| --- | --- | --- | --- |
| Modelo promedio |Hola mejor modelo |Déficit de rendimiento |Modelo promedio |

modelos de Hello hospedados en el estudio de aprendizaje automático de SAS superó a 15-25% para acelerar el proceso de ejecución, pero la precisión era en gran parte del mismo nivel.  

## <a name="discussion-and-recommendations"></a>Debate y recomendaciones
En el sector de telecomunicaciones hello, varias prácticas han surgido tooanalyze renovación, incluidos:  

* Las métricas se pueden clasificar en cuatro categorías fundamentales:
  * **Entidad (por ejemplo, una suscripción)**. Proporcionar información básica acerca de la suscripción de Hola o cliente que está sujeto Hola de renovación.
  * **Actividad**. Obtenga toda la información de uso posible es entidad toohello relacionados, por ejemplo, el número de Hola de inicios de sesión.
  * **Servicio al cliente**. Recopilar información de tooindicate de registros de soporte al cliente si la suscripción de hello tenía problemas o las interacciones con el cliente admite.
  * **Datos competitivos y empresariales**. Obtener ninguna información posible acerca del cliente de hello (por ejemplo, puede ser tootrack no esté disponible o disco duro).
* Usar selección de características de toodrive de importancia. Esto implica que ese modelo de árbol de decisión impulsado de hello siempre es un enfoque prometedor.  

Hello uso de estas cuatro categorías crea Hola ilusión que una simple *determinista* enfoque, basada en índices formados en factores razonables por categoría, debe ser suficiente tooidentify clientes en peligro para la renovación. Por desgracia, aunque esta noción parece plausible, es una concepción errónea. motivo de Hello es que renovación es un efecto temporal y factores de Hola que han contribuido toochurn suelen encontrarse en estados transitorios. Lo que conduce a un cliente tooconsider dejando hoy en día puede variar mañana y por supuesto, será diferente seis meses desde ahora. Por lo tanto, un modelo *probabilístico* es una necesidad.  

A menudo se pasa por alto esta observación importante en el negocio, que suele preferir un tooanalytics de enfoque orientado a inteligencia empresarial, principalmente porque es una más fácil vender y admite automatización sencillo.  

Sin embargo, promesa de Hola de análisis de autoservicio mediante el uso de estudio de aprendizaje automático es que las cuatro categorías de Hola de información, clasificadas por división o departamento, son una valiosa fuente para el aprendizaje automático sobre la renovación.  

Otra función interesante que entran en aprendizaje automático de Azure es Hola capacidad tooadd un repositorio de toohello de módulo personalizado de módulos predefinidos que ya están disponibles. Esta capacidad, básicamente, crea una oportunidad tooselect bibliotecas y crear plantillas para los mercados verticales. Es una diferencia importante de aprendizaje automático de Azure en lugar de mercado de Hola.  

Esperamos que toocontinue en este tema en el análisis de datos de hello toobig futuras, especialmente relacionados.
  

## <a name="conclusion"></a>Conclusión
Este documento describe un problema común de enfoque significativo tootackling Hola de renovación de cliente mediante un marco genérico. Hemos considerado un prototipo para puntuar modelos y lo hemos implementado mediante el Aprendizaje automático de Azure. Por último, se evalúan la precisión de Hola y el rendimiento de la solución de prototipo de hello con algoritmos de toocomparable de tener en cuenta en SAS.  

**Para obtener más información:**  

¿Le ha ayudado este documento? Proporciónenos sus comentarios. Díganos en una escala de 1 too5 (deficiente) (excelente), ¿cómo clasificaría este documento y motivo de esta clasificación? Por ejemplo:  

* ¿Se le da una puntuación alta debido toohaving buenos ejemplos, capturas de pantalla excelentes, desactive escribiendo o por otro motivo?
* ¿Se le da una puntuación baja de vencimiento toopoor ejemplos, capturas de pantalla aproximada o escritura claro?  

Estos comentarios nos ayudarán a mejorar la calidad de Hola de notas del producto que publiquemos.   

[Enviar comentarios](mailto:sqlfback@microsoft.com).
 

## <a name="references"></a>Referencias
[1] análisis predictivos: más allá de las predicciones de hello, w. McKnight, Information Management, julio/agosto de 2011, p.18-20.  

[2] Artículo de Wikipedia: [Precisión y exactitud](http://en.wikipedia.org/wiki/Accuracy_and_precision)

[3] [CRISP-DM 1.0: Step-by-Step Data Mining Guide](http://www.the-modeling-agency.com/crisp-dm.pdf) (Metodología CRISP-DM 1.0: Guía paso a paso de minería de datos)   

[4] [[Big Data Marketing: Engage Your Customers More Effectively and Drive Value]](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn) (Marketing de macrodatos: atraer más eficazmente a los clientes e impulsar el valor)

[5] [Telco churn model template](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) (Plantilla del modelo de pérdida de clientes en empresas de telecomunicaciones) en la [galería de Cortana Intelligence](http://gallery.cortanaintelligence.com/) 
 

## <a name="appendix"></a>Anexo
![][10]

*Ilustración 12. Instantánea de una presentación sobre un prototipo de abandono*

[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png
[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
