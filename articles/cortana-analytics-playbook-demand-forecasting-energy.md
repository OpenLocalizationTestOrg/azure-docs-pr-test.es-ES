---
title: "aaaCortana Guía de plantilla de solución de inteligencia de previsión de demanda de energía | Documentos de Microsoft"
description: "Plantilla de solución con Microsoft Cortana Intelligence que ayuda a prever la demanda de una empresa de suministro de energía."
services: cortana-analytics
documentationcenter: 
author: ilanr9
manager: ilanr9
editor: yijichen
ms.assetid: 8855dbb9-8543-45b9-b4c6-aa743a04d547
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2016
ms.author: ilanr9;yijichen;garye
ms.openlocfilehash: 32fc6ece7e24ced34282baf107548039694a38b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-demand-forecasting-of-energy"></a>Cuaderno de estrategias de la plantilla de soluciones de Cortana Intelligence para la previsión de la demanda de energía
## <a name="executive-summary"></a>Resumen ejecutivo
Hola más allá de los años, Internet de las cosas (IoT), las fuentes de energía alternativas y grandes cantidades de datos se combinan oportunidades gran toocreate utilidad Hola y el dominio de energía. En hello mismo tiempo, utilidad de Hola y sector de la energía completa de hello han visto el consumo de acoplamiento con consumidores exigentes toocontrol de maneras de mejorar el uso de energía. Por lo tanto, Hola utilidad y la cuadrícula inteligente compañías se encuentran en gran necesidad tooinnovate y renovación por sí mismos. Además, muchos cuadrículas de energía y utilidad cada vez son obsoleta y muy costoso toomaintain y administración. Durante el último año Hola, equipo de hello ha estado trabajando en una serie de contrataciones dentro de dominio de energía de Hola. Durante estas contrataciones, hemos encontrado muchos casos en que Hola utilidades o ISV (proveedores de Software independientes) han estado viendo en previsión de demanda de energía futuras. Estas previsiones desempeñan un papel importante en su negocio actual y futuro y se han convertido en foundation Hola para varios casos de uso. Aquí se incluye la previsión de carga energética a corto y largo plazo, su comercialización, el equilibrio de carga, la optimización de la red. Grandes cantidades de datos y los métodos de análisis avanzado (AA) como el aprendizaje de máquina (ML) son factores clave de Hola para generar previsiones precisas y confiables.  

En esta guía, hemos reunido en business hello y analíticas directrices necesarias para un desarrollo correcto y solución de previsión de la implementación de la demanda de energía. Estas directrices propuestas pueden ayudar a los servicios públicos, científicos de datos e ingenieros de datos a establecer soluciones en la nube de previsión de demanda totalmente operativas. Para las empresas que están iniciándose sus grandes cantidades de datos y el viaje de análisis avanzado, esta solución puede representar un valor de inicialización inicial de hello en su estrategia de cuadrícula inteligente a largo plazo.

> [!TIP]
> toodownload un diagrama que proporciona una introducción a la arquitectura de esta plantilla, consulte [arquitectura de la plantilla de solución de inteligencia de Cortana de previsión de demanda de energía](cortana-analytics-architecture-demand-forecasting-energy.md).  
> 
> 

## <a name="overview"></a>Información general
Este documento cubre Hola business, datos y aspectos técnicos del uso de inteligencia de Cortana y en determinado Azure Machine Learning (AML) Hola e implementación de soluciones de previsión de energía. documento de Hello consta de tres partes principales:  

1. Conocimiento del negocio  
2. Conocimiento de los datos  
3. Implementación técnica

Hola **conocimiento de la empresa** parte contornos Hola uno toounderstand de necesidades de negocio aspecto y tenga en cuenta toomaking anterior una decisión de inversión. Se explica cómo tooqualify Hola problema empresarial en tooensure de mano que análisis predictivos y aprendizaje automático son realmente eficaz y es aplicable. documento Hola Explica conceptos básicos de Hola de aprendizaje automático y cómo es problemas de previsión de energía tooaddress usado. Se describen los requisitos previos de Hola y criterios de calificación de Hola de un caso de uso. También se proporcionan varios escenarios de casos de uso y casos de negocio de ejemplo.

Los datos son ingredientes principales de Hola para cualquier solución de aprendizaje automático. Hola **datos descripción** parte de este documento trata algunos aspectos importantes de los datos de Hola. Se describe los tipo de Hola de datos que son necesarios para la previsión de energía, requisitos de calidad de datos y los orígenes de datos normalmente existen. También se explica cómo los datos sin procesar de hello están tooprepare usado características de datos que realmente unidad Hola modelado parte.

Hola tercera parte de hello documento cubre hello **implementación técnica** aspecto de una solución. Característica ingeniería y modelado son Hola núcleo del proceso de ciencia de datos de hello y, por tanto, que se va a se describen con más detalle. Se ocupa de concepto de hello de servicios web, que son un vehículo importante para la implementación de nube de soluciones de análisis predictivo. También se describe una arquitectura típica de una solución operativa de un extremo a otro.

Además, documento Hola incluye material de referencia que puede usar toogain más información sobre tecnología y dominio Hola.

Es importante toonote que no tenemos previsto toocover en este documento Hola un poco más datos ciencia proceso, sus aspectos técnicos y matemáticos. Estos detalles se pueden encontrar en la [documentación de Azure Machine Learning](http://azure.microsoft.com/services/machine-learning/) y estos [blogs](http://blogs.microsoft.com/blog/tag/azure-machine-learning/).

### <a name="target-audience"></a>Audiencia de destino
Hola destino este documento está dirigido empresarial y personal técnico que desearía toogain conocimiento y comprensión de aprendizaje automático en función soluciones y cómo estos se utilizan específicamente en el dominio de previsión de energía de Hola.

Los científicos de datos también pueden beneficiarse de leer este documento toogain una mejor comprensión del proceso de nivel alto de Hola que unidades Hola implementación de una solución de previsión de energía. En este contexto puede ser también usa tooestablish una buena línea base y el punto de partida para obtener más información detallan y avanzado material.

### <a name="industry-trends"></a>Tendencias del sector
Hola más allá de los próximos años, IoT y las fuentes de energía alternativas, grandes cantidades de datos han combinado toocreate gran oportunidades de utilidad de Hola y el espacio de energía. En hello mismo tiempo, utilidad de Hola y sectores de energía todo Hola han visto el consumo de acoplamiento con consumidores exigentes toocontrol de maneras de mejorar el uso de energía.

Muchos utilidad y las empresas de energía inteligente han sido innovadoras hello [cuadrícula inteligente](https://en.wikipedia.org/wiki/Smart_grid) mediante la implementación de un número de uso casos que hacen usan de datos de hello generados por la cuadrícula de Hola. Muchos de los casos de uso giran en torno a las características inherentes de Hola de producción de electricidad: no se pueden acumular ni reservar almacenan como inventario. Por lo tanto, se debe usar lo que se produzca. Utilidades que desea toobecome más eficaz que necesitan consumo de energía tooforecast simplemente porque les proporcionará mayor capacidad demasiado**equilibrar la oferta y la demanda**, lo que evita pérdidas de energía, **reducir el efecto invernadero emisión de gas**y controlar los costos.

Cuando se habla de costos, hay otro aspecto importante, el precio. Nueva potencia de tootrade capacidades entre utilidades sitúan en una gran necesidad demasiado**previsión de demanda futura y precio futuro de electricidad**. Esto puede ayudar a las compañías a determinar sus volúmenes de producción.

Cuando se usa la palabra Hola "inteligente", nos referimos realmente cuadrícula tooa que puede obtener información y, a continuación, realizar predicciones. Puede prever no solo los cambios estacionales en el consumo, sino también **las situaciones de sobrecarga temporal y ajustarse automáticamente en consecuencia**. Mediante la regulación consumo (con la Ayuda de Hola de estos medidores inteligentes) de forma remota, se pueden controlar situaciones de sobrecarga localizado. **Predecir en primer lugar y, a continuación, actúa**, cuadrícula de hello pasa a convertirse en más inteligente con el tiempo.

Para rest Hola de este documento nos centraremos en una familia de casos de uso que cubren la previsión de futuro, específica a corto plazo y la demanda de energía a largo plazo. Se ha estado trabajando en estas áreas durante unos meses y obtenidos algunos conocimientos y habilidades que nos permiten resultados de grado de sector de tooproduce. Se explicará también otros casos de uso en documentos de Hola Hola futuro próximo.

## <a name="business-understanding"></a>Conocimiento del negocio
### <a name="business-goals"></a>Objetivos empresariales
Hola **demostración de energía** objetivo es toodemonstrate un análisis predictivos típica y la solución que se pueden implementar en un breve período de tiempo de aprendizaje automático. En concreto, actualmente nos centramos en habilitar soluciones de previsión de demanda de energía, con el fin de que su valor empresarial se pueda producir y aprovechar rápidamente. información de Hello en esta guía puede ayudar a clientes de Hola para realizar Hola siguientes objetivos:

* Solución basada en toovalue de hora corta del aprendizaje automático
* Capacidad tooexpand un tooother de casos de uso piloto casos de uso y un ámbito más amplio tooa según sus necesidades del negocio
* Obtener rápidamente información de los productos del conjunto de aplicaciones Cortana Intelligence.

Teniendo en cuenta estos objetivos, esta guía pretende entregar business hello y conocimientos técnicos que le ayudarán a lograr estos objetivos.

### <a name="power-load-and-demand-forecasting"></a>Previsión de demanda y carga energéticas
En el sector de la energía de hello, puede haber muchas formas en qué petición previsión puede ayudar a resolver problemas empresariales críticas. De hecho, previsión de demanda se puede considerar foundation Hola para muchos casos de uso principales en el sector de Hola. En general, consideramos dos tipos de previsiones de demanda de energía: a corto plazo y a largo plazo. Cada uno de ellos puede servir para un propósito distinto y utilizar un enfoque diferente. Hola principal diferencia entre Hola dos es Hola previsión horizonte, lo que significa Hola intervalo de tiempo en hello futura para el que podría predecir.

#### <a name="short-term-load-forecasting"></a>Previsión de carga a corto plazo
En contexto de Hola de demanda de energía, corto plazo cargar previsión (STLF) se define como carga agregados de Hola que pronosticó Hola próximas en distintas partes de la cuadrícula de hello (o cuadrícula Hola como un todo). En este contexto, a corto plazo es horizonte toobe definido dentro del alcance de Hola de horas de too24 de 1 hora. En algunos casos, también es posible un horizonte de 48 horas. Por lo tanto, STLF es muy habitual en un caso de uso operativo de cuadrícula de Hola. Estos son algunos ejemplos de casos de usos controlador por STLF:

* Equilibrio de suministro y demanda
* Soporte de la comercialización de la energía
* Creación de mercado (establecimiento del precio de la energía)
* Optimización operativa de la red de distribución de electricidad
* [Respuesta a la demanda](https://en.wikipedia.org/wiki/Demand_response)
* Previsión de máxima demanda
* Administración del lado de la demanda
* Equilibrio de carga y prevención de sobrecargas
* Previsión de carga a largo plazo
* Detección de fallos y anomalías
* Reducción o redistribución de los picos 

Modelo STLF se basan principalmente en hello cerca más allá (último día o semana) los datos de consumo y el uso previsión temperatura como un elemento de predicción importante. Obtener la temperatura precisa de previsión para hello siguiente hora y too24 horas cada vez menor de un desafío días ahora. Estos modelos son menos sensibles patrones tooseasonal o las tendencias de consumo a largo plazo.

Soluciones SLTF también son toogenerate es probable que un gran volumen de llamadas de predicción (solicitudes de servicio) desde que se está llamando a cada hora y en algunos casos incluso con mayor frecuencia. También es muy común implantación de toosee donde cada subestación individual o transformer se representa como un modelo independiente y, por tanto, son incluso mayor volumen de Hola de solicitudes de predicción.

#### <a name="long-term-load-forecasting"></a>Previsión de carga a largo plazo
el objetivo de Hola de largo plazo carga previsión (LTLF) es tooforecast demanda de energía con un horizonte de tiempo que van de los meses de 1 semana toomultiple (y en algunos casos para un número de años). Este intervalo se aplica principalmente a los casos de uso de planeamiento e inversión.

Para los escenarios a largo plazo, es importante toohave datos de alta calidad que abarca un intervalo de varios años (mínimo de 3 años). Estos modelos normalmente se extraer patrones estacionalidad de datos históricos de Hola y hacer uso de predicators externos como patrones de tiempo y clima.

Es importante es tooclarify que Hola Hola más horizonte de previsión, puede ser Hola menos precisos Hola previsión. Por lo tanto, es importante tooproduce previsión algunos intervalos de confianza junto con hello real que permitiría que los seres humanos toofactor Hola posibles en la variación su proceso de planeación.

Como escenario de consumo de Hola para LTLF principalmente está planeando, podemos esperamos mucho menores volúmenes de predicción (como comparado tooSTLF). Se ven normalmente estas predicciones incrustadas en las herramientas de visualización, como Excel o Power BI y se puede invocar manualmente por el usuario de Hola.

### <a name="short-term-vs-long-term-prediction"></a>Predicción a corto plazo frente a predicción a largo plazo
Hello en la tabla siguiente compara STLF LTLF en toohello respetan los atributos más importantes:

| Atributo | Previsión de carga a corto plazo | Previsión de carga a largo plazo |
| --- | --- | --- |
| Horizonte de pronóstico |De 1 hora too48 horas |De 1 too6 meses o más |
| Granularidad de datos |Cada hora |Cada hora o a diario |
| Casos de uso típicos |<ul><li>Equilibrio entre demanda y suministro</li><li>Elección de la hora de previsión</li><li>Respuesta a la demanda</li></ul> |<ul><li>Planeamiento a largo plazo</li><li>Planeamiento de recursos de cuadrícula</li><li>Planeamiento de recursos</li></ul> |
| Indicadores típicos |<ul><li>Día o semana</li><li>Hora del día</li><li>Temperatura cada hora</li></ul> |<ul><li>Mes del año</li><li>Día del mes</li><li>Temperatura y clima a largo plazo</li></ul> |
| Intervalo de datos históricos |Con dos años toothree datos |Con cinco años too10 datos |
| Precisión típica |MAPE* del 5 % o inferior |MAPE* del 25 % o inferior |
| Frecuencia de pronóstico |Se realiza cada hora o cada 24 horas |Generado una vez al mes, trimestre o año |

\*[MAPE](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error): error absoluto porcentual de la media

Tal y como se puede ver en esta tabla, es muy importante toodistinguish entre Hola corto y a largo plazo Hola previsión escenarios como estos representan diferentes necesidades del negocio y pueden tener una implementación diferente y patrones de consumo.

### <a name="example-use-case-1-esmart-systems--overload-optimization"></a>Caso de uso de ejemplo 1: eSmart Systems (optimización de la sobrecarga)
Una función importante de un [cuadrícula inteligente](https://en.wikipedia.org/wiki/Smart_grid) es toodynamically constantemente optimizar y ajustar para cambiar los patrones de consumo de Hola. El consumo de energía puede verse afectado por los cambios a corto plazo que suelen causar principalmente las fluctuaciones de temperatura (*por ejemplo,*, se usa más electricidad para la calefacción o el aire condición). Hola al mismo tiempo, energía consumo también se ve afectado por las tendencias a largo plazo. Dichas tendencias pueden incluir los efectos de las estacionalidad, los días festivos nacionales, el crecimiento del consumo a largo plazo e incluso factores económicos como el índice de consumo, el precio de petróleo y el PIB.

En este caso de uso, [eSmart](http://www.esmartsystems.com/) deseaba solución toodeploy basados en nube que permite predecir la tendencia de Hola de una situación de sobrecarga en cualquier subestación determinado de cuadrícula de Hola. En concreto, eSmart deseaba subestaciones tooidentify que están toooverload probable en hello siguiente hora, por lo que una acción inmediata se pudo tomar tooavoid o resolver esta situación.

Una predicción precisa y rápida del funcionamiento requiere la implementación de tres modelos predictivos:

* Modelo de término larga que habilita la previsión de consumo de energía en cada subestación durante Hola siguiente algunas semanas o meses
* Modelo de a corto plazo que permite la predicción de la situación de sobrecarga en un determinado subestación durante la hora siguiente de Hola
* Un modelo de temperatura que permite el pronóstico la temperatura futura en varios escenarios.

objetivo de Hola de modelo a largo plazo de hello es subestaciones de hello toorank por su toooverload de tendencia (dada su capacidad de transmisión de energía) durante Hola próxima semana o mes. Esto permite la creación de hello de una lista breve de las subestaciones que podría servir como entrada para la predicción a corto plazo de Hola. Temperatura sea un elemento de predicción importante para el modelo de Hola a largo plazo, hay una temperatura de escenario de múltiples necesidad tooconstantly producen pronostica e introducirlos como entrada en el modelo de toohello a largo plazo. a corto plazo Hola de previsión, a continuación, se invoca toopredict qué subestación es probable toooverload sobre Hola hora siguiente.

los modelos de Hola a corto plazo y a largo plazo se implementan individualmente por cada subestación. Por lo tanto, ejecución resulta muy práctico de Hola de estos modelos necesita orquestación amplia. toogain una mayor precisión de predicción a corto plazo hello, un modelo más específico dedicada para cada hora del día de Hola. Todos estos modelos se ejecutan cada hora y finalizan la ejecución dentro de unos minutos tooallow suficiente tiempo toorespond y toman medidas preventivas si es necesario. Esta colección de modelos se mantiene actualizada por reciclaje periódico con datos más recientes de Hola.

[Aquí](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18945)puede encontrar más información acerca de este caso de uso.

#### <a name="use-case-qualification-criteria--prerequisites"></a>Criterios de cualificación de casos de uso: requisitos previos
seguridad principal de Hola de inteligencia de Cortana es en su capacidad eficaz toodeploy y escala máquina aprendizaje centradas en soluciones. Está diseñado toosupport miles de predicciones que se ejecutan simultáneamente. Puede escalar automáticamente toomeet un patrón de consumo cambiantes. Por tanto el enfoque de la solución se encuentra en la precisión y el rendimiento de cálculo. Por ejemplo, una compañía de servicios está interesada en la creación de previsión para hello siguiente hora y para cada hora del día de hello de la demanda de energía precisos. En Hola otra parte, nos interesa menos contestar Hola pregunta por qué petición hello es toobe predicho que (el propio modelo Hola se encargará de ese).

Por lo tanto, es importante toorealize que no todos los casos de uso y problemas empresariales puedan resolverse de forma eficaz con aprendizaje automático.

Inteligencia de Cortana y el aprendizaje automático pudieron ser muy eficaces para resolver un problema empresarial determinado cuando se cumple Hola siguiendo criterios:

* Hola problema empresarial en mano es **predictivo** por naturaleza. Un ejemplo de casos de uso predictivo es una compañía de utilidad que desearía toopredict power carga en un determinado subestación durante Hola hora siguiente. En Hola otra parte, analizar y la clasificación de controladores de demanda histórico sería **descriptivo** por naturaleza y, por tanto, menor es aplicable.
* Hay un método clear **ruta de acceso de acción** toobe una vez realizada predicción Hola está disponible. Por ejemplo, predecir una sobrecarga en una subestación durante la hora siguiente de hello puede desencadenar una acción preventiva de reducir la carga que está asociado a ese subestación y, por tanto, potencialmente evitar una sobrecarga.
* caso de uso de Hello representa un **habitual de tipo de problema** tal que cuando se ha resuelto puede pave Hola forma toosolving otros casos de uso similar.
* puede establecer cliente Hello **objetivos cuantitativos y cualitativos** toodemonstrate una implementación de la solución correcta. Por ejemplo, un objetivo cuantitativo buena de previsión de la demanda de energía sería umbral de precisión necesario de hello (*p. ej.*, seguridad too5 se permite % error) o cuando se predicen sobrecarga subestación, a continuación, precisión hello (tasa de verdaderos positivos) y Recuerde (extensión de verdaderos positivos) debe estar por encima de un umbral determinado. Estos objetivos deben derivarse de objetivos de negocio del cliente de Hola.
* Hay un método clear **escenario de integración** con flujo de trabajo de la compañía de Hola. Por ejemplo, se puede integrar Hola subestación carga previsión en las actividades de prevención de hello cuadrícula control center tooallow sobrecarga.
* cliente de Hello tiene listo toouse **datos con calidad suficiente** hello toosupport el caso de uso (consulte más información en la sección siguiente de hello, **calidad de los datos**, de esta guía).
* Hola arquitectura centradas en datos de cliente abrazos en la nube o **aprendizaje automático basado en la nube**, incluidos el aprendizaje automático de Azure y otros componentes del conjunto de inteligencia de Cortana.
* cliente de Hello está dispuesto tooestablish **un flujo de datos final tooend** que instalaciones Hola entrega de datos en la nube de Hola de forma continuada y está dispuestas demasiado**poner** Hola solución.
* cliente Hello es listo demasiado**dedicar recursos** que se pueden comprometidos activamente durante la implementación piloto de saludo inicial para que pueden conocimiento y la propiedad de la solución de hello transfieren toohello cliente tras la correcta finalización.
* recurso de cliente Hello debe ser un **professional datos cualificado**, preferiblemente científico de datos.

Calificación de un caso de uso en función de hello criterio anterior en gran medida puede mejorar las tasas de éxito de Hola de un caso de uso y establecer un buen beachhead para la implementación de Hola de casos de uso en el futuro.

### <a name="cloud-based-solutions"></a>Soluciones basadas en la nube
Conjunto de inteligencia de Cortana en Azure es un entorno integrado que se encuentra en la nube de Hola. implementación de Hola de una solución de análisis avanzado en un entorno de nube contiene ventajas importantes para las empresas y en hello mismo tiempo puede significar un cambio importante para las empresas que aún use local soluciones de TI. En el sector de la energía de hello, hay una tendencia clara de la migración gradual de las operaciones en la nube de Hola. Esta tendencia va de la mano junto con el desarrollo de Hola de cuadrícula inteligente Hola tal y como se dijo anteriormente, en **tendencias de la industria**. Como esta guía se centra en una solución basada en la nube en el dominio de energía de hello, es importante tooexplain ventajas de Hola y otras consideraciones de implementación de una solución basada en la nube.

Quizás hello mayor ventaja de una solución basada en la nube es Hola costo. Dado que la solución hace uso de componentes implementados en la nube, no hay costos iniciales ni costos de COGS (costo de bienes vendidos) asociados a ellos. Esto significa que no hay ningún tooinvest necesidad de hardware, software y el mantenimiento de TI y, por lo tanto, hay una reducción considerable de riesgo para el negocio.

Otra ventaja importante es la estructura de costo de pago por uso de Hola de soluciones basadas en la nube. Los servidores basados en la nube para la realización de cálculo o almacenamiento se pueden implementar y escalar solo cuando sea necesario. Esto representa Hola ventaja de eficiencia de costo de una solución basada en la nube.

Por último, no hay ninguna necesidad de invertir en desarrollo futuro de infraestructura o de mantenimiento de TI ya todo esto forma parte de la oferta de hello en la nube. extensión toothat, Cortana Intelligence Suite incluye Hola mejor en los servicios de clase y mantiene evoluciona su mapa de carreteras. Constantemente se introducen nuevas características, componentes y capacidades, y evolucionan los existentes.

Para una compañía que se está iniciando su transición en la nube hello, estamos muy recomendando tootake un enfoque gradual mediante la implementación de un mapa de carreteras de migración de nube. Creemos que de utilidades y compañías de dominio de energía de hello, casos de uso de Hola que se tratan en esta guía representan una excelente oportunidad para piloto soluciones de análisis predictivo en la nube de Hola.

#### <a name="business-case-justification-considerations"></a>Consideraciones que justifican los casos empresariales
En muchos casos, el cliente de hello puede estar interesado en realizar una justificación de negocio para un caso de uso determinado en el que una solución basada en la nube y el aprendizaje automático son componentes importantes. A diferencia de una solución local, en caso de hello de una solución basada en la nube, Hola coste por adelantado componente es mínima y la mayoría de los elementos de costo de hello está asociada con el uso real. Cuando se trata de una previsión de la solución en el conjunto de inteligencia de Cortana de energía toodeploying, varios servicios pueden integrarse con una única estructura de costo comunes. Por ejemplo, las bases de datos (*p. ej.*, SQL Azure) pueden ser datos sin procesar de hello toostore usado y la, a continuación, para hello real pronostica aprendizaje automático de Azure es toohost usado Hola previsión servicios. En este ejemplo, Hola costo estructura podría incluir componentes transaccionales y almacenamiento.

En hello otra parte, uno debe tener un buen conocimiento de valor para el negocio Hola de operativo una demanda de energía de previsión (corto o largo plazo). De hecho, es importante toorealize valor para el negocio Hola de cada operación de previsión. Por ejemplo, con precisión previsión carga de energía para hello próximas 24 horas puede evitar overproduction o puede ayudar a evitar sobrecargas en cuadrícula de Hola y esto puede cuantificado en términos de ahorro a diario.

Una fórmula básica para calcular un beneficio financiero Hola de demanda de previsión solución sería: ![fórmula básica para calcular un beneficio financiero Hola de demanda de previsión solución](media/cortana-analytics-playbook-demand-forecasting-energy/financial-benefit-formula.png)

Puesto que Cortana Intelligence Suite proporciona un modelo de precios de pago por uso, no hay ninguna necesidad de incurrir en una fórmula de toothis de componente de costo fijo. Esta fórmula se puede calcular diaria, mensual o anualmente.

Los planes de precios actuales del conjunto de aplicaciones Cortana Intelligence y del Aprendizaje automático de Azure se pueden encontrar [aquí](http://azure.microsoft.com/pricing/details/machine-learning/).

### <a name="solution-development-process"></a>Proceso de desarrollo de soluciones
ciclo de desarrollo de Hola de una demanda de energía previsión solución suele implica 4 fases, en el que se realice el uso de tecnologías basadas en la nube y servicios dentro de Hola Suite de inteligencia de Cortana.

Esto se muestra en hello siguiente diagrama:

![Ciclo de red de distribución inteligente de electricidad](media/cortana-analytics-playbook-demand-forecasting-energy/smart-grid-cycle.png)

Hola después de párrafo describe este proceso 4 paso:

1. **Recopilación de datos**: todas las soluciones basadas en el análisis avanzado confían en los datos (consulte **Conocimiento de los datos**). En concreto, cuando se trata de análisis de toopredictive y la previsión, confiamos en curso y dinámico, flujo de datos. En caso de hello de previsión de demanda de energía, estos datos pueden proceder directamente de metros inteligentes o ya se ha agregado en una base de datos local. También confiamos en otros orígenes externos de datos, como el tiempo y la temperatura. Este flujo continuo de datos debe orquestarse, programarse y almacenarse. [Data Factory de Azure](http://azure.microsoft.com/services/data-factory/) (ADF) es nuestro producto estrella para llevar a cabo esta tarea.
2. **Modelado** : para las previsiones de energía preciso y fiable, uno debe desarrollar (tren) y mantener un gran modelo que hace uso de datos históricos de Hola y Hola extrae significativo y patrones de predicción en Hola datos. área de Hola de aprendizaje de máquina (ML) ha ido aumentando rápidamente con algoritmos más avanzados habitualmente que se está desarrollados. Estudio de aprendizaje automático proporciona una experiencia de usuario excelente que le ayuda a utilizar hello más avanzada algoritmos de aprendizaje automático dentro de un flujo de trabajo completo. Ese flujo de trabajo se muestra en un diagrama de flujo intuitiva e incluye la preparación de datos de hello, extracción de características, modelado y evaluación de modelos. usuario de Hello puede extraer en cientos de varios modelos que se incluyen en este entorno. Extremo de Hola de esta fase científico de datos tendrá un modelo de trabajo que se evalúa totalmente y listo para la implementación.
   
   Hola siguiente diagrama es una ilustración de un flujo de trabajo típico:
   
   ![Flujo de trabajo de modelado](media/cortana-analytics-playbook-demand-forecasting-energy/modeling-workflow.png)
3. **Implementación** : con un modelo de trabajo en la mano, paso siguiente hello es la implementación. Este modelo Hola se convierte en un servicio web que expone una API de REST que se pueden invocar simultáneamente a través de Hola Internet desde varios clientes de consumo. Aprendizaje automático de Azure proporciona una manera sencilla de implementar un modelo directamente desde Hola estudio de aprendizaje automático con un solo clic de un botón. proceso de toda la implementación de Hello tiene lugar bajo el paraguas de Hola. Esta solución puede escalar automáticamente toomeet consumo de hello necesario.
4. **Consumo** : en esta fase, hacemos realmente el uso de hello predicciones de tooproduce de modelo de previsión. consumo de Hello pueden controlar desde una aplicación de usuario (*p. ej.*, panel) o directamente desde un sistema operativo como petición/supply equilibrio de sistema o una solución de optimización de la cuadrícula. Desde un modelo individual se pueden controlar varios casos de uso.

## <a name="data-understanding"></a>Conocimiento de los datos
Después de que tratan sobre las consideraciones de negocio de hello (vea **conocimiento de la empresa**) de la demanda de energía previsión de la solución, se está ahora listo toodiscuss Hola parte de datos. Todas las soluciones de análisis predictivo se basa en datos confiables. Para la previsión de la demanda energética, nos basamos en los datos históricos de consumo con distintos niveles de granularidad. Que se utilizan datos históricos como prima Hola. Se someterá a un cuidadoso análisis en qué Hola científico de datos identifica para la predicción (también denominado tooas características) que se pueden colocar en un modelo que finalmente generará previsiones de hello necesario.

En el resto de Hola de esta sección, vamos a describir Hola varios pasos y consideraciones para la descripción de los datos de Hola y cómo toobring se tooa de formato utilizable.

### <a name="hello-model-development-cycle"></a>Hola ciclo de desarrollo del modelo
La generación de buenos modelos de previsión requiere una preparación y un planeamiento meticulosos. Dividir Hola proceso de modelado en varios pasos y centrarse en un paso a la vez puede mejorar drásticamente el resultado de hello del proceso completo de Hola.

Hello siguiente diagrama ilustra cómo Hola modelado proceso puede dividirse en varios pasos:

![ciclo de desarrollo del modelo](media/cortana-analytics-playbook-demand-forecasting-energy/model-development-cycle.png)

Como puede verse ciclo Hola consta de seis pasos:

* Formulación del problema
* Ingesta y exploración de datos
* Preparación de los datos e ingeniería de características
* Modelado
* Evaluación del modelo
* Desarrollo

En el resto de Hola de esta sección, vamos a describir los pasos individuales de Hola y tooconsider de elementos en cada paso.

### <a name="problem-formulation"></a>Formulación del problema
Podemos consideramos formulación de problema de hello medida hello más importante paso uno tootake anterior tooimplementing cualquier solución de análisis predictivos. Aquí se transformaría Hola problema empresarial y descomponer toospecific elementos que se pueden resolver utilizando los datos y modelado técnicas. Es un problema de hello tooformulate recomendable como un conjunto de preguntas que nos gustaría tooanswer. Estas son algunas preguntas posibles que pueden aplicarse en ámbito de Hola de previsión de demanda de energía:

* ¿Cuál es la carga de hello esperado en un subestación individual en hello siguiente hora o día?
* ¿En qué momento del día de hello experimentarán mi cuadrícula momentos de máxima demanda?
* ¿Qué probabilidades hay mi cuadrícula toosustain Hola esperada pico de carga?
* ¿Cuánta energía debe generar Hola power estación durante cada hora del día de hello?

Formular estas preguntas, nos permite toofocus en obtener datos derecho Hola e implementar una solución que se ajusta totalmente a problema al lado de hello empresarial. Además, a continuación, podemos establecer algunas métricas claves que nos permiten el rendimiento de hello tooevaluate del modelo de Hola. ¿Por ejemplo, grado de precisión debe Hola predecir y se lo intervalo Hola de error que todavía es aceptable por empresa Hola?

### <a name="data-sources"></a>Orígenes de datos
cuadrícula inteligente moderna de Hello recopila datos de varias partes y componentes de cuadrícula de Hola. Estos datos representan diversos aspectos de la operación de Hola y la utilización de Hola de cuadrícula de alimentación de Hola. En el ámbito de Hola de previsión de demanda de energía de hello, estamos limitar la discusión de hello en orígenes de datos que reflejan el consumo de hello demanda real. Una importante fuente de consumo de energía son los medidores inteligentes. Utilidades de todo el mundo de Hola son implementar rápidamente metros inteligentes para sus consumidores. Metros inteligentes registran el consumo de energía actuales de Hola y retransmisión constantemente la compañía de utilidad toohello atrás de datos. Datos se recopilan y se envían en un intervalo fijo, comprendido entre cada hora de too1 de 5 minutos. Metros inteligentes más avanzados pueden programarse remotamente toocontrol y analice Hola consumo real dentro de un núcleo. Los datos del medidor inteligente son relativamente confiables e incluyen una marca de tiempo. Esto hace que sea una parte importante de la previsión de la demanda. Datos de medidor se pueden agregar (sumados seguridad) en varios niveles dentro de la topología de la cuadrícula de hello: transformer, subestación, región, *etcetera*. A continuación, podemos elegir toobuild de nivel de agregación de hello requerido un modelo de pronóstico para él. Por ejemplo, si la empresa de la utilidad de hello como tooforecast futuras carga en cada uno de sus subestaciones de cuadrícula, a continuación, datos de todos los medidores pueden se agrega para cada subestación individual y utilizar como entrada para el modelo de previsión de Hola. Nos referimos toosmart metros como un origen de datos interno.

Una previsión confiable de la demanda de energía también usará otros orígenes de datos externos. Un factor importante que afecta al consumo de energía es el tiempo de Hola o temperatura de hello con mayor precisión. Los datos históricos muestran una fuerte correlación entre la temperatura exterior y el consumo de energía. Durante los días de verano activa, los consumidores hacer uso de su aire acondicionado y durante el apagado de invierno hello en sistemas de calefacción. Por lo tanto, una fuente confiable de temperaturas históricas en la ubicación de la cuadrícula de Hola es clave. Además, también confiamos en un pronóstico preciso de la temperatura como indicador de consumo de energía.

Otros orígenes de datos externos también pueden resultar de ayuda durante la creación de modelos de previsión de demanda energética. Entre ellos se pueden incluir los cambios climáticos a largo plazo y los índices económicos (*por ejemplo*, PIB), entre otros. En este documento no se incluirán dichos orígenes de datos.

### <a name="data-structure"></a>Estructura de datos
Después de identificar Hola necesario orígenes de datos, se podrían como tooensure que los datos sin procesar que se han recopilado incluyen Hola corregir las características de datos. modelo de previsión de toobuild una petición de confianza, se necesita tooensure que Hola datos recopilados incluye elementos de datos que pueden ayudarles a predecir la demanda futura Hola. Estos son algunos requisitos básicos relativos a la estructura de datos de hello (esquema) de los datos sin procesar de Hola.

datos sin procesar de Hello constan de filas y columnas. Cada medida se representa en una sola fila de datos. Cada fila de datos incluye varias columnas (también denominado tooas características o campos).

1. **Marca de tiempo** : campo de marca de tiempo de hello representa el tiempo real de hello cuando se registró la medición de Hola. Deben cumplir uno de los formatos de fecha y hora de hello comunes. Se deben incluir las partes de fecha y hora. En la mayoría de los casos, no es necesario para hello tiempo toobe registra hasta Hola de segundo nivel de granularidad. Es importante toospecify zona de horaria hello en el que se registran los datos de Hola.
2. **Id. del panel de instrumentos** -este campo identifica el medidor de Hola o dispositivo de medición de Hola. Es una variable de categoría y puede ser una combinación de caracteres y dígitos.
3. **Valor de consumo** : se trata de consumo real de hello en una determinada fecha y hora. se puede medir el consumo de Hello en kWh (hora-kilowatt) o cualquier otro preferible unidades. Es importante toonote que Hola unidad de medida debe permanecer coherente a través de todas las mediciones en datos Hola. En algunos casos, el consumo se puede suministrar en tres fases de alimentación. En ese caso se necesita toocollect todas las fases de consumo independientes de Hola.
4. **Temperatura** : temperatura Hola normalmente se recopila desde una fuente independiente. Sin embargo, debe ser compatible con los datos de consumo de Hola. Debe incluir una marca de tiempo como se describió anteriormente que le permitirá toobe sincronizada con los datos de consumo real de Hola. valor de temperatura de Hello puede especificarse en grados centígrados o grados Fahrenheit, pero debe permanecer coherente a través de todas las medidas.
5. **Ubicación:** campo de ubicación de Hola se suelen estar asociado a lugar Hola donde se han recopilado datos de temperatura de saludo. Se puede representar como un número de código postal o en formato de latitud y longitud (lat. y long.).

Hola las tablas siguientes muestra ejemplos de un formato de datos de consumo y temperatura buena:

| **Fecha** | **Hora** | **Id. de medidor** | **Fase 1** | **Fase 2** | **Fase 3** |
| --- | --- | --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |ABC1234 |7.0 |2.1 |5.3 |
| 7/1/2015 |10:00:01 |ABC1234 |7.1 |2.2 |4.3 |
| 7/1/2015 |10:00:02 |ABC1234 |6.0 |2.1 |4.0 |

| **Date** | **Hora** | **Ubicación** | **Temperatura** |
| --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |11242 |24,4 |
| 7/1/2015 |10:00:01 |11242 |24,4 |
| 7/1/2015 |10:00:02 |11242 |24,5 |

Como puede verse, este ejemplo incluye tres valores diferentes de consumo, asociados a tres fases de energía. Además, tenga en cuenta que los campos de fecha y hora de hello están separados, sin embargo también se pueden combinar en una sola columna. En este caso la columna de la ubicación de Hola se representa en un formato de código postal de 5 dígitos y la temperatura de hello en un formato de grados Celsius.

### <a name="data-format"></a>Formato de datos
Conjunto de inteligencia de Cortana puede admitir formatos de datos más comunes de hello como CSV, TSV, JSON, *etcetera*. Es importante que ese formato de datos de hello mantiene la coherencia de hello todo ciclo de vida del proyecto de Hola.

### <a name="data-ingestion"></a>Ingesta de datos
Puesto que la previsión de la demanda de energía se predice constantemente y con frecuencia, debemos asegurarnos de que se envíen datos sin procesar de Hola por medio de un proceso de recopilación de datos sólido y confiable. proceso de recopilación de Hello debe garantizar que los datos sin procesar de hello están disponibles para hello previsión proceso en tiempo de hello necesario. Que implica que la frecuencia de recopilación de datos de hello debe ser mayor que Hola previsión frecuencia.

Por ejemplo: si nuestra petición previsión solución generaría una previsión nuevo a las 8:00 a diario, a continuación, necesitamos tooensure que Hola a todos los datos de Hola que se han recopilado durante la última se tooeven incluyen hello y 24 horas ha sido ingestión totalmente hasta ese punto última hora de datos.

En orden tooaccomplish, Cortana Intelligence Suite ofrece toosupport de varias maneras de un proceso de recopilación de datos confiable. Esto se explicará más Hola **implementación** sección de este documento.

### <a name="data-quality"></a>Calidad de los datos
origen de datos sin procesar de Hola que es necesaria para realizar la previsión de demanda precisa y confiable debe cumplir algunos criterios de calidad de datos básicos. Aunque avanzados métodos estadísticos pueden ser toocompensate usado para algún problema de calidad de datos posibles, todavía necesitamos tooensure que estamos cruzar determinado umbral de calidad de la base de datos cuando se recopila datos nuevos. Estas son algunas consideraciones relativas a la calidad de los datos sin procesar:

* **Valor que falta** : Esto refiere toohello situación cuando no se recopiló la medida específica. requisito básico de Hello aquí es que Hola falta el tipo de valor no debe ser superior al 10% en cualquier período de tiempo determinado. En caso de que falte un solo valor, debe indicarse mediante un valor predefinido (por ejemplo: '9999'), pero no '0', que podría ser una medida válida.
* **Precisión de la medida** : se debe registrar con precisión el valor real de Hola de consumo o la temperatura. Unas medidas que no sean exactas generarán previsiones imprecisas. Por lo general, error de medición de hello debe ser inferior al valor de 1% toohello relativa es true.
* **Tiempo de medida** : se requiere esa marca de tiempo real de Hola de hello los datos recopilados no se desviarán por algo más que la hora real en 10 segundos toohello relativa de medida real Hola.
* **Sincronización** : cuando se utilizan varios orígenes de datos (*por ejemplo*, consumo y temperatura) debemos asegurarnos de que no hay problemas de sincronización de hora entre ellos. Esto significa que tiempo Hola diferencia entre la marca de tiempo de hello recopilan los dos orígenes de datos independientes no debe superar más de 10 segundos.
* **Latencia**: como ya se ha explicado, en **Ingesta de datos**, dependemos de un flujo de datos y de un proceso de ingesta confiables. toocontrol que debemos asegurarnos de que se controla de latencia de datos de Hola. Esto se especifica como diferencia de tiempo de hello entre la hora de Hola que se tomó la medida real de Hola y Hola en el que se ha cargado en hello almacenamiento Cortana Intelligence Suite y está listo para su uso. Para la carga a corto plazo latencia total de pronóstico hello no debe ser superior a 30 minutos. Para la carga a largo plazo pronóstico latencia total de hello no debe ser mayor que 1 día.

### <a name="data-preparation-and-feature-engineering"></a>Preparación de los datos e ingeniería de características
Una vez que han sido ingestión datos sin procesar de hello (vea **ingesta de datos**) y se ha de forma segura almacenada, resulta toobe listo procesado. Hello fase de preparación de datos es básicamente poner los datos sin procesar de Hola y convertir (transformar, reformular) en un formulario para hello fase de modelado. Que puede incluir operaciones sencillas, como el uso de la columna de datos sin procesar de hello tal cual con su valor medido real, valores estandarizados, operaciones más complejas como [tiempo retardado](https://en.wikipedia.org/wiki/Lag_operator)y otros. Hola que acaba de crear columnas de datos son funciones de datos de la que se hace referencia tooas y proceso de Hola de generar estas ingeniería de la característica de tooas que se hace referencia. Extremo de Hola de este proceso tendríamos un nuevo conjunto de datos que se ha derivado de los datos sin procesar de Hola y puede utilizarse para el modelado. Además, la fase de preparación de datos de hello debe tootake atención valores que faltan (vea **calidad de datos**) y compensar para ellos. En algunos casos, también se necesitaría toonormalize Hola datos tooensure que todos los valores se representan en Hola la misma escala.

En esta sección que se indican algunas de las características comunes de hello datos que se incluyen en "energía" hello petición modelos de previsión.

**Tiempo características orientadas:** estas características se derivan de datos de marca de fecha/hora de saludo. Dichos datos se extraen y se convierten en características de categoría como:

* Hora del día: esta es la hora de hello del día de Hola que toma los valores de 0 too23
* Día de la semana: Esto representa Hola día de semana de Hola y toma los valores de 1 (domingo) too7 (sábado)
* Día del mes: Esto representa la fecha real de Hola y puede tomar los valores de 1 too31
* Mes del año: lo que representa el mes de Hola y toma los valores de 1 (enero) too12 (diciembre)
* Fin de semana: se trata de una característica de valor binario que toma valores de hello de 0 para los días laborables o 1 para fines de semana
* Vacaciones: se trata de una característica de valor binario que toma valores de hello de 0 para un día normal o 1 para un día no laborable
* Términos de Fourier: Hola Fourier términos son pesos que se derivan de la marca de tiempo de Hola y son toocapture usado Hola estacionalidad (ciclos) en datos Hola. Dado que podemos tener varias estaciones en los datos, es posible que necesitemos varios términos de Fourier. Por ejemplo, los valores de la demanda pueden tener ciclos o estaciones anuales, semanales y diarios, lo que generará tres términos de Fourier.

**Funciones de medida independientes:** Hola independiente incluye todos los elementos de datos de Hola que queremos toouse como para la predicción en nuestro modelo. Aquí excluimos característica dependiente de hello, que se necesita toopredict.

* Característica de posposición: se trata de tiempo desplazado a valores de demanda real Hola. Por ejemplo, lag 1 características contendrá el valor de la petición de Hola en la marca de tiempo actual de hello hora anterior (suponiendo que los datos por hora) toohello relativa. Del mismo modo, nos podemos agregar lag 2, 3, de retardo *etcetera*. combinación real de Hola de características de retraso que se usan se determinan durante la fase de modelado de Hola por evaluación de los resultados del modelo Hola.
* Tendencias a largo plazo: esta característica representa crecimiento lineal de hello en petición entre años.

**Característica dependiente:** característica dependiente hello es la columna de datos de Hola que nos gustaría nuestro toopredict de modelo. Con [supervisado aprendizaje automático](https://en.wikipedia.org/wiki/Supervised_learning), necesitamos primero entrenar modelo de hello mediante las características dependientes hello (que también es etiquetas tooas que se hace referencia). Esto permite Hola modelo toolearn Hola de modelos de datos Hola asociados con la característica dependiente de Hola. En previsión de la demanda de energía normalmente deseamos demanda real de toopredict hello y, por tanto, se utilizaría como característica dependiente Hola.

**Control de valores que faltan:** durante la fase de preparación de datos de hello, se necesita toodetermine Hola mejor estrategia toohandle valores que faltan. Esto es especialmente mediante el uso de Hola diversas estadísticas [métodos de imputación datos](https://en.wikipedia.org/wiki/Imputation_\(statistics\)). En caso de hello de la previsión de demanda de energía, se suele imputar valores ausentes mediante el uso de la media móvil de los puntos de datos disponibles anteriores.

**Normalización de datos:** normalización de datos es otro tipo de transformación que es usado toobring todos los datos numéricos como demanda de previsión en una escala similar. Normalmente esto ayuda a mejorar la precisión y la precisión del modelo Hola. Se suele realizar esta operación dividiendo el valor real de Hola por intervalo de Hola de datos de Hola.
Esta operación escalará valor original de hello hacia abajo en un intervalo más reducido, normalmente entre -1 y 1.

## <a name="modeling"></a>Modelado
Hola fase de modelado es donde realiza la conversión de Hola de hello en un modelo. Hola principales de este proceso se avanzan algoritmos que analizar datos históricos de hello (datos de entrenamiento), extraer patrones y generación un modelo. Ese modelo puede ser más tarde toopredict usa datos nuevos que no se estableció el modelo de hello toobuild usado.

Una vez que tenemos un funcionamiento confiable modelo, a continuación, podemos usar lo tooscore nuevos datos que sean tooinclude estructurado Hola requiere características (X). Hola proceso de puntuación hará que el uso de hello persistentes del modelo (objeto de la fase de aprendizaje de hello) y predecir la variable de destino de Hola que se indica mediante Ŷ.

### <a name="demand-forecasting-modeling-techniques"></a>Técnicas de modelado de la previsión de la demanda
En caso de hello de petición previsión realizamos el uso de datos históricos que se ordenan por tiempo. Nos referimos generalmente toodata que incluye la dimensión de tiempo de hello como [series temporales](https://en.wikipedia.org/wiki/Time_series). objetivo de Hello en el tiempo modelado de series es hora de toofind relacionada con las tendencias, estacionalidad, auto-correlación (correlación con el tiempo) y formular en un modelo.

En los últimos años han sido algoritmos avanzados pronóstico de series temporales tooaccommodate desarrollada y tooimprove previsión precisión. A continuación explicaremos brevemente algunos de ellos.

> [!NOTE]
> En esta sección no es toobe previsto usar como una máquina de aprendizaje y la previsión de información general, sino como una breve encuesta de modelado técnicas que se usan habitualmente para previsión de demanda. Para obtener más información y material educativo acerca de la predicción de serie temporal, recomendamos encarecidamente libros en línea hello [Forecasting: principios y prácticas](https://www.otexts.org/book/fpp).
> 
> 

#### <a name="ma-moving-averagehttpswwwotextsorgfpp62"></a>[**MA (media móvil)**](https://www.otexts.org/fpp/6/2)
Media móvil es una de hello primera técnicas analíticos que se haya utilizado para la predicción de series temporales y sigue siendo una de las técnicas de hello más utilizada en este momento. También es base de hello más avanzadas de técnicas de previsión. Con la media móvil se estamos previsión siguiente punto de datos Hola calculando el promedio a través de puntos de hello K más reciente, donde K indica el orden de Hola de hello Media móvil.

técnica de promedio móvil de Hello no tiene efecto de Hola de suavizado Hola de previsión y, por tanto, no puede controlar también gran volatilidad de los datos de Hola.

#### <a name="ets-exponential-smoothinghttpswwwotextsorgfpp75"></a>[**ETS (suavizado exponencial)**](https://www.otexts.org/fpp/7/5)
Suavizado exponencial (ETS) es una familia de diversos métodos que usan la media ponderada de puntos de datos recientes en el punto de datos siguiente de orden toopredict Hola. idea Hello es ponderaciones mayores tooassign valores recientes toomore y reducir gradualmente el peso para los valores antiguos medidos. Hay una serie de métodos diferentes con esta familia, algunas de ellas incluyen control de la estacionalidad en los datos de hello como [método estacionales Holt deporte de invierno](https://www.otexts.org/fpp/7/5).

Algunos de estos métodos también tener en cuenta estacionalidad Hola de datos de Hola.

#### <a name="arima-auto-regression-integrated-moving-averagehttpswwwotextsorgfpp8"></a>[**ARIMA (modelo autorregresivo integrado de media móvil)**](https://www.otexts.org/fpp/8)
El modelo autorregresivo integrado de media móvil (ARIMA) es otra familia de métodos que habitualmente se utiliza para la previsión de series temporales. A nivel práctico, combina métodos de regresión automática con la media móvil. Métodos de regresión automática, usan los modelos de regresión tomando valores de series de tiempo anterior punto siguiente fecha de pedido toocompute Hola. Métodos ARIMA también aplican métodos de diferencias que incluyen calcular la diferencia de hello entre puntos de datos y el uso de éstos en lugar del valor medido original de Hola. Por último, ARIMA también hace uso de hello mover promedio técnicas que se mencionan anteriormente. combinación de Hola de todos estos métodos de distintas maneras es qué construcciones Hola familia de métodos ARIMA.

En la actualidad, ETS y ARIMA se utilizan profusamente para la previsión de la demanda de energía y para muchos otros problemas de predicción. En muchos casos estas se combinan los resultados muy precisos de toodeliver.

**Regresión varios general** los modelos de regresión pudieron ser el método de modelado más importante de hello en dominio Hola de aprendizaje automático y estadísticas. En el contexto de Hola de serie temporal se utiliza valores futuros de regresión toopredict Hola (*p. ej.*, de demanda). En regresión tomamos una combinación de predicción de Hola y obtenga información acerca de los pesos de hello (también denominado tooas coeficientes) de los predictores durante el proceso de entrenamiento de Hola. objetivo de Hello es tooproduce una línea de regresión que se prever el valor de predicción. Métodos de regresión son adecuadas cuando la variable de destino de hello es numérico y por lo tanto encaja también pronóstico de series temporales. Hay un gran número de métodos de regresión, entre los que se incluyen modelos de regresión muy sencillos, como la [regresión lineal](https://en.wikipedia.org/wiki/Linear_regression), y otros más avanzados, como los árboles de decisión, las [selvas aleatorias](https://en.wikipedia.org/wiki/Random_forest), las [redes neuronales](https://en.wikipedia.org/wiki/Artificial_neural_network) y los árboles de decisión incrementados.

Construir la demanda de energía de previsión como un problema de regresión, nos da mucha flexibilidad en la selección de datos de series temporales de hello demanda real y factores externos, como la temperatura de nuestras características de datos que se pueden combinar. Para obtener más información acerca de las características de hello seleccionado se tratan en hello característica ingeniería (vea **preparación de los datos y de ingeniería de característica**) sección de esta guía.

En nuestra experiencia con la instalación e implementación de prueba piloto de previsiones de demanda de energía, hemos encontrado que los modelos de regresión avanzadas que están disponibles en Azure ML hello suelen obtener los mejores resultados de tooproduce hello y hacemos uso de los mismos.

## <a name="model-evaluation"></a>Evaluación del modelo
Evaluación del modelo tiene un papel fundamental dentro de hello **ciclo de desarrollo del modelo**. En este paso, ponemos atención a validar el modelo de Hola y su rendimiento con datos reales. Durante el paso de modelado de Hola usamos una parte de los datos disponibles de Hola para entrenar el modelo de Hola. Durante la fase de evaluación de hello tomamos el resto de Hola Hola tootest Hola del modelo de datos. Prácticamente significa que se están procesando Hola modelo nuevos datos que se ha reestructurado y contiene Hola mismas características como conjunto de datos de entrenamiento de Hola. Sin embargo, durante el proceso de validación de hello, se utiliza variable de destino de hello modelo toopredict hello en lugar de proporcionar Hola variable de destino disponibles. Nos referimos a menudo toothis proceso como modelo de puntuación. A continuación, se utilizaría valores de destino es true de Hola y compárelos con hello predecirlos. objetivo Hello es toomeasure y minimizar los errores de predicción de hello, lo que significa que la diferencia de hello entre las predicciones de Hola y el valor de true Hola. Cuantificación de medición de error de hello es la clave ya que se podría como modelo de hello toofine ajustar y validar si realmente está disminuyendo el error Hola. Modelo de hello ajuste puede realizarse mediante la modificación de parámetros del modelo que controlan el proceso de aprendizaje de hello, o agregando o quitando características de datos (denominada tooas [barrido de parámetros](https://channel9.msdn.com/Blogs/Azure/Data-Science-Series-Building-an-Optimal-Model-With-Parameter-Sweep)). Prácticamente que significa que es posible necesita tooiterate entre ingeniería de característica de hello, el modelado y de modelo fases de evaluación varias veces hasta que se está tooreduce capaz de toohello requerido el nivel del error Hola.

Es importante tooemphasis que el error de predicción de hello nunca será cero porque no hay nunca es un modelo que puede predecir perfectamente cada resultado. Sin embargo, hay una determinada magnitud de los errores que es aceptable por empresa Hola. Durante el proceso de validación de hello, nos gustaría tooensure que nuestro error de predicción de modelo está en hello nivel o un rendimiento mejor que la tolerancia de negocio de Hola de nivel. Por lo tanto, es importante tooset Hola nivel de hello tolerable error principio Hola de hello ciclo durante hello **problema formulación** fase.

### <a name="typical-evaluation-techniques"></a>Técnicas de evaluación típicas
Hay varias formas de medir y cuantificar los errores de predicción. En esta sección nos centraremos discusión hello en serie de tootime relevantes de técnicas de evaluación y específicos de previsión de la demanda de energía.

#### <a name="mapehttpsenwikipediaorgwikimeanabsolutepercentageerror"></a>[**MAPE**](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
MAPE son las siglas de Mean Absolute Percentage Error (error absoluto porcentual de la media). Con MAPE estamos calculando la diferencia de hello entre cada punto de previsión y el valor real de Hola de ese punto. A continuación, se cuantificar error Hola por punto al calcular la proporción de hello del valor real de hello diferencia toohello relativa. En el último paso, se obtiene la media de estos valores. fórmula matemática Hola usada para MAPE es siguiente de hello:

![Fórmula MAPE](media/cortana-analytics-playbook-demand-forecasting-energy/mape-formula.png)
*donde un<sub>t</sub> es el valor real hello, F<sub>t</sub> Hola valor de predicción, y la n Hola horizonte de previsión.*

## <a name="deployment"></a>Implementación
Una vez que hemos aclarado Hola fase de modelado y validar el rendimiento de los modelos Hola estamos toogo listo en la fase de implementación de Hola. En este contexto, implementación indica lo que permite al cliente hello tooconsume Hola modelo por en ejecución predicciones reales a gran escala. concepto de Hola de implementación es la clave en Azure ML puesto que nuestro objetivo principal es tooconstantly invocar predicciones como lugar toojust obtener una visión general de Hola de datos de Hola. fase de implementación de Hello es parte de Hola donde habilitamos Hola modelo toobe consumido a gran escala.

En contexto de Hola de previsión de la demanda de energía, nuestro objetivo es tooinvoke continua y periódica previsiones y garantizar que están disponibles para el modelo de hello datos actualizados y ese Hola pronosticó que se envían datos cliente consume toohello atrás.

### <a name="web-services-deployment"></a>Implementación de servicios web
principal bloque de creación Hola pueden implementar en Azure ML es servicio de hello web. Se trata de consumo de tooenable de manera más eficaz de Hola de un modelo de predicción en la nube de Hola. servicio Web de Hola encapsula modelo hello y concluye con una [RESTful](http://www.restapitutorial.com/) API (interfaz de programación de aplicaciones). Hola API puede usarse como parte del código de cliente como se muestra en el siguiente diagrama de Hola.

![Implementación y consumo de servicio web](media/cortana-analytics-playbook-demand-forecasting-energy/web-service-deployment-and-consumption.png)

Como puede ver, servicio web de hello está implementado en hello en la nube Cortana Intelligence Suite y puede invocarse a través de su extremo de API de REST expuesto. Un tipo diferente de los clientes a través de distintos dominios puede invocar servicio Hola a través de hello API Web al mismo tiempo. servicio web de Hello también puede escalar para admitir miles de llamadas simultáneas.

### <a name="a-typical-solution-architecture"></a>Arquitectura de una solución típica
Al implementar una solución de previsión de la demanda de energía, estamos interesados en la implementación de una solución de tooend end que va más allá del servicio web de predicción de Hola y facilita el flujo de datos completo de Hola. En el momento de hello que Invocamos una previsión nuevo, se necesita toomake seguro de que ese modelo Hola se introduce con las características de datos actualizados. Que implica que Hola recién datos sin procesar recopilados constantemente se ingestión, procesa y transforma en característica necesaria Hola establecer qué modelo Hola se utilizó para generar. Hola al mismo tiempo, nos gustaría toomake Hola pronosticó datos disponibles para hello terminar los clientes de consumo. Un ciclo de flujo de datos de ejemplo (o canalización de datos) se muestra en el diagrama de hello siguiente:

![TooEnd de final de flujo de datos de previsión de la demanda de energía](media/cortana-analytics-playbook-demand-forecasting-energy/energy-demand-forecase-end-data-flow.png)

Estos son los pasos de Hola que tienen lugar como parte del ciclo de previsión de demanda de energía de hello:

1. Los millones de medidores de datos implementados generan constantemente datos de consumo de energía en tiempo real.
2. Dichos datos de recopilan y cargan en un repositorio en la nube (*por ejemplo*, Blob de Azure).
3. Antes de ser procesados, datos sin procesar de hello son subestación tooa agregados o nivel regional según se define en business Hola.
4. procesamiento de la característica de Hello (vea **preparación de los datos y el procesamiento de la característica**), a continuación, se lleva a cabo y modelo de datos de Hola de produce que se requiere para entrenamiento o de puntuación: Hola característica conjunto de datos se almacenan en una base de datos (*p. ej.*, SQL Azure).
5. se invoca Hola volver a entrenar servicio hello toore entrenar previsión modelo: actualizado a la versión del modelo de Hola se conserva para que se puede utilizar por Hola la puntuación del servicio web.
6. Hola la puntuación del servicio web se invoca en una programación que se adapte a la frecuencia de previsión de hello necesario.
7. Hola pronosticó datos se almacenan en una base de datos que se puede acceder por cliente de consumo de hello final.
8. cliente de consumo de Hello recupera las previsiones de hello, aplica en cuadrícula de Hola y consume con arreglo al caso de uso de hello necesario.

Es importante toonote que este ciclo completo está totalmente automatizada y se ejecuta según una programación. orquestación completa de Hola de este ciclo de datos puede realizarse mediante herramientas como [Data Factory de Azure](http://azure.microsoft.com/services/data-factory/).

### <a name="end-tooend-deployment-architecture"></a>Terminar tooEnd arquitectura de implementación
En orden toopractically implementar una solución de previsión de demanda de energía en la inteligencia de Cortana, necesitamos tooensure que los componentes necesario de Hola se establezcan y configurados correctamente.

Hello siguiente diagrama muestra una arquitectura en función de inteligencia de Cortana típica que implementa y orquesta ciclo de flujo de datos de Hola que se ha descrito anteriormente:

![Terminar tooEnd arquitectura de implementación](media/cortana-analytics-playbook-demand-forecasting-energy/architecture.png)

Para obtener más información acerca de cada uno de los componentes de Hola y Hola arquitectura completa, consulte toohello plantilla de solución de energía.

