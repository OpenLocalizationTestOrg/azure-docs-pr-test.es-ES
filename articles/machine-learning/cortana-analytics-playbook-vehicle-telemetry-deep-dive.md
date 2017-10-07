---
title: "aaaDeep profundizar en mantenimiento de vehículo de predecir y dirigir hábitos - Azure | Documentos de Microsoft"
description: "Usar funciones de Hola de toogain en tiempo real y predicción visión de inteligencia de Cortana en el estado del vehículo y dirigir hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a>Guía de solución de análisis de telemetría de vehículo: profundización en soluciones de Hola
Esto **menú** vincula toohello secciones de esta guía: 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Esta sección detalla en cada una de las fases de hello representados en hello arquitectura de la solución con instrucciones y punteros para la personalización. 

## <a name="data-sources"></a>Orígenes de datos
solución de Hello utiliza dos orígenes de datos diferentes:

* **conjunto de datos de señales de vehículo y diagnósticos simulados** y 
* **catálogo de vehículo**

Se incluye un simulador telemático del vehículo como parte de esta solución. Se emite información de diagnóstico y se indica el estado de toohello correspondiente del vehículo hello y toohello automóvil patrón en un momento dado en el tiempo. Haga clic en [vehículo telemáticas simulador](http://go.microsoft.com/fwlink/?LinkId=717075) hello toodownload **solución de Visual Studio de vehículo telemáticas simulador** para las personalizaciones en función de sus requisitos. catálogo de vehículo Hello contiene un conjunto de datos de referencia con una asignación de toomodel Niv.

![Simulador telemático de vehículo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

*Ilustración 1: Simulador telemático de vehículo*

Se trata de un conjunto de datos con formato JSON que contiene Hola después de esquema.

| Columna | Description | Valores |
| --- | --- | --- |
| VIN |Número de identificación del vehículo generado de forma aleatoria |Se obtiene a partir de una lista maestra de 10.000 números de identificación de vehículo generados de forma aleatoria. |
| Outside temperature |Hola fuera temperatura donde está impulsando vehículo Hola |Número generado al azar de 0 a 100 |
| Engine temperature |temperatura del motor Hola de vehículo Hola |Número generado al azar de 0 a 500 |
| Velocidad |velocidad de motor de Hello en qué Hola está impulsando vehículo |Número generado al azar de 0 a 100 |
| Fuel |nivel de combustible Hola de vehículo Hola |Número generado al azar de 0 a 100 (indica el porcentaje del nivel de combustible) |
| EngineOil |nivel de petróleo de motor de Hola de vehículo Hola |Número generado al azar de 0 a 100 (indica el porcentaje del nivel de aceite del motor) |
| Presión de los neumáticos |presión del neumático Hola de vehículo Hola |Número generado al azar de 0 a 50 (indica el porcentaje del nivel de presión de los neumáticos) |
| Odometer |cuentakilómetros Hola de vehículo Hola |Número generado al azar de 0 a 200000 |
| Accelerator_pedal_position |posición pedales Hola del Acelerador de vehículo Hola |Número generado al azar de 0 a 100 (indica el porcentaje del nivel del acelerador) |
| Parking_brake_status |Indica si está aparcado vehículo de Hola o no |Verdadero o falso |
| Headlamp_status |Indica la ubicación proyector hello en o no |Verdadero o falso |
| Brake_pedal_status |Indica si se presionó pedal frenos de Hola o no |Verdadero o falso |
| Transmission_gear_position |posición de engranaje de transmisión de Hello del vehículo Hola |Estados: primera, segunda, tercera y cuarta, quinta, sexta, séptima, octava |
| Ignition_status |Indica si el vehículo de hello está en ejecución o detenido |Verdadero o falso |
| Windshield_wiper_status |Indica si está activada limpiaparabrisas Hola o no |Verdadero o falso |
| ABS |Indica si el ABS está activado o no |Verdadero o falso |
| Timestamp |Hola de marca de tiempo cuando se crea el punto de datos de Hola |Date |
| City |ubicación de Hola de vehículo Hola |En esta solución tiene la opción de 4 ciudades: Bellevue, Redmond, Sammamish, Seattle |

conjunto de datos de referencia de modelo de Hello vehículo contiene la asignación de modelo de toohello de bastidor. 

| VIN | Modelo |
| --- | --- |
| FHL3O1SA4IEHB4WU1 |Sedán |
| 8J0U8XCPRGW4Z3NQE |Híbrido |
| WORG68Z2PLTNZDBI7 |Berlina familiar |
| JTHMYHQTEPP4WBMRN |Sedán |
| W9FTHG27LZN1YWO0Y |Híbrido |
| MHTP9N792PHK08WJM |Berlina familiar |
| EI4QXI2AXVQQING4I |Sedán |
| 5KKR2VB4WHQH97PF8 |Híbrido |
| W9NSZ423XZHAONYXB |Berlina familiar |
| 26WJSGHX4MA5ROHNL |Descapotable |
| GHLUB6ONKMOSI7E77 |Familiar |
| 9C2RHVRVLMEJDBXLP |Compacto |
| BRNHVMZOUJ6EOCP32 |SUV pequeño |
| VCYVW0WUZNBTM594J |Deportivo |
| HNVCE6YFZSA5M82NY |SUV mediano |
| 4R30FOR7NUOBL05GJ |Familiar |
| WYNIIY42VKV6OQS1J |SUV grande |
| 8Y5QKG27QET1RBK7I |SUV grande |
| DF6OX2WSRA6511BVG |Cupé |
| Z2EOZWZBXAEW3E60T |Sedán |
| M4TV6IEALD5QDS3IR |Híbrido |
| VHRA1Y2TGTA84F00H |Berlina familiar |
| R0JAUHT1L1R3BIKI0 |Sedán |
| 9230C202Z60XX84AU |Híbrido |
| T8DNDN5UDCWL7M72H |Berlina familiar |
| 4WPYRUZII5YV7YA42 |Sedán |
| D1ZVY26UV2BFGHZNO |Híbrido |
| XUF99EW9OIQOMV7Q7 |Berlina familiar |
| 8OMCL3LGI7XNCC21U |Descapotable |
| ……. | |

### <a name="references"></a>Referencias
[Solución de simulador telemático de vehículo de Visual Studio](http://go.microsoft.com/fwlink/?LinkId=717075) 

[Centro de eventos de Azure](https://azure.microsoft.com/services/event-hubs/)

[Factoría de datos de Azure](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a>Ingesta de datos
Combinaciones de factoría de datos, análisis de transmisiones y centros de eventos de Azure son tooingest aprovechado Hola vehículo señales, eventos de diagnóstico de hello y en tiempo real y análisis por lotes. Todos estos componentes se crean y configuran como parte de la implementación de la solución de Hola. 

### <a name="real-time-analysis"></a>Análisis en tiempo real
Hello eventos generados por hello vehículo telemáticas simulador se publican toohello concentrador de eventos mediante Hola SDK de concentrador de eventos. trabajo de análisis de transmisiones de Hello introduce estos eventos desde Hola centro de eventos y procesos Hola datos en estado de tiempo real tooanalyze Hola vehículo. 

![Panel del Centro de eventos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

*Ilustración 4: Panel del Centro de eventos*

![Procesamiento de datos del trabajo de Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

*Ilustración 5: Procesamiento de datos del trabajo de Stream Analytics*

trabajo de análisis de transmisiones de Hello;

* recopila datos de hello concentrador de eventos 
* realiza una combinación con hello referencia toomap Hola vehículo Niv toohello correspondiente modelo de datos 
* los conserva en Azure Blob Storage para unos análisis eficaces por lotes. 

Después de consulta de análisis de transmisiones de Hello es toopersist usado Hola datos en el almacenamiento de blobs de Azure. 

![Consulta de trabajo de Stream Analytics para la ingesta de datos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

*Ilustración 6: Consulta de trabajo de Stream Analytics para la ingesta de datos*

### <a name="batch-analysis"></a>Análisis por lotes
También se genera un volumen adicional de las señales y el conjunto de datos de diagnóstico del vehículo simulado para un análisis por lotes más completo. Esto es necesario tooensure un volumen de datos representativo en buen estado para el procesamiento por lotes. Para ello, usamos una canalización con el nombre "PrepareSampleDataPipeline" en toogenerate de flujo de trabajo de Data Factory de Azure de hello natural un año de las señales de vehículo simulada y conjunto de datos de diagnóstico. Haga clic en [actividad personalizada de factoría de datos](http://go.microsoft.com/fwlink/?LinkId=717077) hello toodownload actividad DotNet personalizada solución de Visual Studio para las personalizaciones de factoría de datos según sus requisitos. 

![Preparar los datos de muestra para el flujo de trabajo de procesamiento por lotes](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

*Ilustración 7: Preparar los datos de muestra para el flujo de trabajo de procesamiento por lotes*

canalización de Hello consta de ADF .net personalizado actividad, aparecen aquí:

![Actividad PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

*Ilustración 8: PrepareSampleDataPipeline*

Una vez que la canalización de Hola se ejecuta correctamente y el conjunto de datos de "RawCarEventsTable" está marcado como "Listo", un año que vale la pena de señales de vehículo simulado y de diagnóstico se generan datos. Ve a continuación Hola carpetas y archivos creados en su cuenta de almacenamiento en el contenedor de "connectedcar" hello:

![Resultados de PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

*Ilustración 9: Resultados de PrepareSampleDataPipeline*

### <a name="references"></a>Referencias
[SDK del Centro de eventos de Azure para ingesta de transmisiones](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

[Funcionalidades de movimiento de datos de Data Factory de Azure](../data-factory/data-factory-data-movement-activities.md)
[Actividad DotNet de Data Factory de Azure](../data-factory/data-factory-use-custom-activities.md)

[Solución de Visual Studio para la actividad DotNet de Factoría de datos de Azure para preparar datos de ejemplo](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a>El conjunto de datos de partición Hola
las señales de vehículo semiestructurados sin procesar de Hola y conjunto de datos de diagnóstico se crean particiones en el paso de preparación de datos de hello en un formato de mes/año. Esta subdivisión promociona consulta más eficaz y escalable a largo plazo habilitando a continuación como primera cuenta de hello conmutación de error de un blob cuenta toohello se llena. 

>[!NOTE] 
>Este paso de solución de hello es el procesamiento de toobatch solo es aplicable.

Administración de datos de entrada y salida:

* Hola **los datos de salida** (con la etiqueta *PartitionedCarEventsTable*) se mantiene toobe durante un largo período de tiempo como formulario de hello atractivos / "rawest" de datos "Data Lake" del cliente de Hola. 
* Hola **los datos de entrada** toothis canalización normalmente se descartará como datos de salida de hello tienen toohello con plena fidelidad de entrada: solo se almacena (particiones) mejor para su uso posterior.

![Flujo de trabajo de eventos de automóvil de partición](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

*Ilustración 10: Flujo de trabajo de eventos de automóvil de partición*

datos sin procesar de Hola se crean particiones en una actividad de HDInsight Hive "PartitionCarEventsPipeline". datos de ejemplo de Hola generados en el paso 1 para un año se dividen por año/mes. las particiones de Hello son señales de vehículo toogenerate usado y datos de diagnóstico para cada mes (total de 12 particiones) de un año. 

![Actividad PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

*Figure 11 - PartitionCarEventsPipeline*

***Script de Hive PartitionConnectedCarEvents***

Hola siguiente script de Hive, denominado "partitioncarevents.hql", se utiliza para crear particiones y se encuentra en hello "\demo\src\connectedcar\scripts" carpeta de descarga de Hola zip. 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

Una vez que se ejecuta la canalización de hello correctamente, verá Hola después particiones generadas en la cuenta de almacenamiento en el contenedor de "connectedcar" Hola.

![Salida con particiones](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

*Ilustración 12: Salida con particiones*

datos de Hola ahora está optimizado, es más fácil de administrar y listo para su posterior procesamiento toogain visión de lote completo. 

## <a name="data-analysis"></a>Análisis de datos
En esta sección, verá cómo avanzada toocombine análisis de transmisiones de Azure, aprendizaje automático de Azure, Data Factory de Azure y Azure HDInsight para datos completos de transformación de análisis de mantenimiento de vehículo y dirigir. Hay tres subsecciones aquí:

1. **Aprendizaje automático**: este apartado incluye información en el experimento de detección de anomalías de Hola que hemos usado en este vehículos toopredict de solución que requiere el servicio de mantenimiento y la necesidad de recuperaciones debido a problemas de toosafety de vehículos.
2. **Análisis en tiempo real**: este apartado incluye información sobre análisis en tiempo real de hello usando el lenguaje de consulta de análisis de transmisiones de Hola y aprendizaje automático de hello en marcha experimentar en tiempo real mediante una aplicación personalizada.
3. **Procesar por lotes analysis**: este apartado incluye información relativa a Hola transformar y el procesamiento de datos del lote Hola con HDInsight de Azure y aprendizaje automático de Azure operaciones por factoría de datos de Azure.

### <a name="machine-learning"></a>Machine Learning
Nuestro objetivo es toopredict vehículos de Hola que requieren mantenimiento o recuperación en función de algunas estadísticas de estado. Hacemos Hola después suposiciones

* Si uno de hello tres condiciones siguientes es verdaderas, requieren los vehículos hello **servicio de mantenimiento**:
  
  * Presión de los neumáticos es baja
  * Nivel de aceite del motor es bajo
  * Temperatura del motor es alta
* Si uno de hello condiciones siguientes es verdaderas, vehículos Hola pueden tener un **problema de seguridad** y requieren **recuperación**:
  
  * Temperatura del motor es alta, pero la temperatura exterior es baja
  * Temperatura del motor es baja, pero la temperatura exterior es alta

En función de los requisitos anteriores de hello, hemos creado las anomalías toodetect de dos modelos independientes, uno para la detección de mantenimiento del vehículo y otro para la detección de recuperación de vehículo. En estos modelos, el algoritmo de análisis de componentes principales (PCA) integrada de hello sirve para la detección de anomalías. 

**Modelo de detección de mantenimiento**

Si uno de los tres indicadores tire presión, petróleo motor o temperatura del motor - cumple su condición respectivo, modelo de detección de mantenimiento de hello notifica una anomalía. Como resultado, únicamente se necesitan tooconsider estos tres variables en la creación de modelos de Hola. En nuestro experimento de aprendizaje automático de Azure, se utiliza en primer lugar un **seleccionar columnas de conjunto de datos** tooextract módulo estos tres variables. A continuación utilizamos Hola anomalías basado en PCA módulo toobuild Hola anomalías detección modelo de detección. 

Análisis de componentes principales (PCA) es una técnica establecida en aprendizaje automático que puede ser la detección de anomalías, clasificación y selección de toofeature aplicado. PCA convierte un conjunto de casos con variables posiblemente correlacionadas, en un conjunto de valores denominados componentes principales. idea clave de Hola de modelado basado en PCA es tooproject datos en un espacio inferior dimensional para que las características y las anomalías se pueden identificar más fácilmente.

Para cada nueva entrada demasiado hello modelo de detección, detector de anomalías de hello calcula su proyección en vectores propios hello en primer lugar y, a continuación, calcula Hola normalizadas error reconstrucción. Este error normalizada es la puntuación de anomalías de Hola. error Hola Hola superior, hello más anómalos Hola instancia es. 

Problema de detección de mantenimiento de hello, cada registro se puede considerar un punto en un espacio de 3 dimensiones definido por la presión tire, petróleo de motor y temperatura del motor coordenadas. toocapture estas anomalías se puedan Hola original de datos del proyecto en el espacio de 3 dimensiones hello en un espacio de 2 dimensiones con PCA. Por lo tanto, los estableceremos parámetro hello número de componentes toouse en PCA toobe 2. Este parámetro desempeña un rol importante en la aplicación de la detección de anomalías basada en PCA. Después de proyectar datos con PCA, podemos identificar más fácilmente estas anomalías.

**Modelo de detección de anomalías de recuperación** en el modelo de detección de anomalías de recuperación de hello, usamos Hola seleccionar columnas de conjunto de datos y anomalías basado en PCA módulos de detección de forma similar. En concreto, se extraen tres variables: temperatura del motor, la temperatura exterior y velocidad - mediante hello **seleccionar columnas de conjunto de datos** módulo. También se incluye velocidad Hola variable, ya que normalmente es la temperatura del motor Hola correlacionado toohello velocidad. A continuación utilizamos datos de Hola de tooproject del módulo de detección de anomalías basado en PCA de espacio de 3 dimensiones de hello en un espacio tridimensional de 2. se cumplen los criterios de recuperación de Hola y vehículo Hola requiere recuperación cuando la temperatura del motor y la temperatura exterior se correlacionan muy negativamente. Usa el algoritmo de detección de anomalías basado en PCA, podemos capturar las anomalías de hello después de realizar el PCA. 

Cualquier modelo de aprendizaje, necesitamos toouse datos normales, que no requieren mantenimiento o recuperación como modelo de detección de anomalías basado en PCA de hello tootrain de datos de entrada de Hola. Hola experimento de puntuación, usamos toodetect de modelo de detección de anomalías de hello entrenado si vehículo Hola requiere mantenimiento o retirada o no. 

### <a name="real-time-analysis"></a>Análisis en tiempo real
Hola después de la consulta de SQL de análisis de secuencia se utiliza Hola de promedio de hello tooget de todos los parámetros del vehículo importante como la velocidad del vehículo, el nivel de combustible, temperatura del motor, cuentakilómetros, tire presión, nivel del motor petróleo y otros. Hello promedios son anomalías toodetect usado, emite alertas y determinar Hola condiciones de estado general de los vehículos utilizados en una región específica y, a continuación, correlacionará toodemographics. 

![Consulta de Stream Analytics para el procesamiento en tiempo real](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

*Ilustración 13: Consulta de Stream Analytics para el procesamiento en tiempo real*

Todos los promedios de Hola se calculan sobre un TumblingWindow de 3 segundos. En este caso estamos usando TubmlingWindow puesto que necesitamos que los intervalos de tiempo no se superpongan y sean contiguos. 

toolearn más información acerca de todas las funcionalidades de "Ventana" hello en análisis de transmisiones de Azure, haga clic en [basado en ventanas (análisis de transmisiones de Azure)](https://msdn.microsoft.com/library/azure/dn835019.aspx).

**Predicción en tiempo real**

Una aplicación se incluye como parte del modelo de aprendizaje automático de solución toooperationalize Hola Hola en tiempo real. Esta aplicación denominada "RealTimeDashboardApp" se crean y configuran como parte de la implementación de la solución de Hola. aplicación Hello realiza siguiente hello:

1. Escucha la instancia de concentrador de eventos de tooan donde análisis de transmisiones está publicando continuamente los eventos de hello en un patrón. ![Consulta de análisis de secuencia para publicar datos de hello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *figura 14: consulta de análisis de transmisiones para publicar Hola datos tooan instancia del concentrador de eventos de salida* 
2. Para cada evento que recibe esta aplicación: 
   
   * Datos de Hola de procesos mediante el extremo de puntuación de solicitudes y respuestas de aprendizaje de máquina (RR). el punto de conexión de Hola RR se publica automáticamente como parte de la implementación de Hola.
   * salida de Hello RR es el conjunto de datos de Power BI de tooa publicado mediante la inserción de hello API.

Este patrón también es aplicable tooscenarios del que desee toointegrate una aplicación de línea de negocio (LoB) con el flujo de análisis en tiempo real de hello, para escenarios como las alertas, notificaciones y mensajería.

Haga clic en [RealtimeDashboardApp descarga](http://go.microsoft.com/fwlink/?LinkId=717078) hello toodownload solución RealtimeDashboardApp Visual Studio para las personalizaciones. 

**Hola tooexecute aplicación de panel en tiempo real**
1. Extraer y guardar localmente la carpeta ![RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Ilustración 16: Carpeta RealtimeDashboardApp*  
2. Ejecutar la aplicación hello RealtimeDashboardApp.exe
3. Proporcione credenciales válidas de Power BI, inicie sesión y haga clic en Aceptar ![Aplicación de inicio de sesión tooPower BI de panel en tiempo real](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Aplicación de panel en tiempo real finalizar el inicio de sesión tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

*Figura 17: RealtimeDashboardApp: Inicio de sesión tooPower BI*

>[!NOTE] 
>Si desea que el conjunto de datos de tooflush Hola Power BI, ejecute hello RealtimeDashboardApp con el parámetro "flushdata" hello: 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a>Análisis por lotes
Hola objetivo es tooshow cómo motores Contoso usa hello Azure compute capacidades tooharness grandes cantidades de datos toogain información valiosa en impulsar el patrón, el comportamiento de uso y mantenimiento de vehículo. Con esto es posible:

* Mejorar la experiencia del usuario de Hola y hacerla más barato proporcionando información sobre los hábitos de y los comportamientos de conducción eficaz de combustible que conduce
* Obtenga información acerca de forma proactiva acerca de los clientes y sus decisiones de negocios de conducción patrones toogovern y proporcionar Hola mejor en servicios y productos de la clase

En esta solución, que estamos usando como objetivo Hola siguiendo las métricas:

1. **Dinámico automóvil comportamiento**: identifica la tendencia de Hola de modelos de hello, ubicaciones, condiciones de conducción y tiempo de visión de hello año toogain sobre los patrones de conducción agresivos. Contoso Motors puede usar esta información para campañas de marketing, dando lugar a seguros con nuevas características y prestaciones personalizadas y basados en el uso.
2. **Comportamiento determinante eficaz de combustible**: identifica la tendencia de Hola de modelos de hello, ubicaciones, condiciones de conducción y tiempo de visión de hello año toogain sobre los patrones de conducción eficaz de combustible. Motores de Contoso puede usar estas informaciones para las campañas de marketing imponen nuevas características y automático controladores toohello informes para costo hábitos de conducción descriptivos efectivas y de entorno. 
3. **Recuerde modelos**: identifica los modelos que requieren recuperaciones por experimento de aprendizaje automático de detección de anomalías de hello en marcha

Echemos un vistazo en los detalles de Hola de cada una de estas métricas,

**Patrón de comportamiento agresivo al volante**

Hola particiones señales de vehículo y se procesan los datos de diagnóstico en hello canalización denominado "AggresiveDrivingPatternPipeline" usar modelos de Hive toodetermine hello, la ubicación, vehículo, dando lugar a condiciones y otros parámetros que se comporta agresiva patrón de conducir.

![Flujo de trabajo de patrón de conducción agresiva](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Ilustración 18: Flujo de trabajo de patrón de conducción agresiva*


***Consulta de Hive para el patrón de comportamiento agresivo al volante***

Hola script de Hive denominado "aggresivedriving.hql" que se utiliza para el análisis agresiva patrón determinante de condición se encuentra en "\demo\src\connectedcar\scripts" carpeta de descarga de Hola zip. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


Usa combinación Hola del vehículo posición de engranaje de transmisión, frenos pedales el estado y velocidad toodetect sentido/agresiva automóvil comportamiento basado en frenos patrón a alta velocidad. 

Una vez que se ejecuta la canalización de hello correctamente, verá Hola después particiones generadas en la cuenta de almacenamiento en el contenedor de "connectedcar" Hola.

![Resultados de AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

*Ilustración 19: Resultados de AggressiveDrivingPatternPipeline*

**Patrón de conducción con consumo eficiente de combustible**

Hola particiones señales de vehículo y datos de diagnóstico se procesan en la canalización de hello denominado "FuelEfficientDrivingPatternPipeline". Subárbol es toodetermine usado Hola modelos, ubicación, vehículo, determinante condiciones y otras propiedades que exhiben patrón determinante eficaz de combustible.

![Patrón de conducción con consumo eficiente de combustible](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

*Ilustración 20: Flujo de trabajo del patrón de conducción con consumo eficiente de combustible*

***Consulta de Hive para el patrón de conducción con consumo eficiente de combustible***

Hola script de Hive denominado "fuelefficientdriving.hql" que se utiliza para el análisis agresiva patrón determinante de condición se encuentra en "\demo\src\connectedcar\scripts" carpeta de descarga de Hola zip. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


Usa la combinación de Hola de posición de engranaje de transmisión del vehículo, estado pedales frenos, velocidad y combustible de acelerador posición pedales toodetect comportamiento determinante eficaz en función de aceleración, frenos, y acelerar los patrones. 

Una vez que se ejecuta la canalización de hello correctamente, verá Hola después particiones generadas en la cuenta de almacenamiento en el contenedor de "connectedcar" Hola.

![Resultados de FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

*Ilustración 21: Resultados de FuelEfficientDrivingPatternPipeline*

**Predicciones de retirada**

experimento de aprendizaje automático de Hola se aprovisionan y se publica como un servicio web como parte de la implementación de la solución de Hola. se utiliza la puntuación punto final de lotes de Hello en este flujo de trabajo, registrado como un servicio vinculado del generador de datos y operaciones con actividad de puntuación de lote de generador de datos.

![Punto de conexión de Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

*Ilustración 22: Punto de conexión de Machine Learning registrado como un servicio vinculado en Factoría de datos*

Hola se usa servicio vinculado registrado en hello DetectAnomalyPipeline tooscore Hola datos mediante el modelo de detección de anomalías de Hola. 

![Actividad de puntuación por lotes de Azure Machine Learning en Factoría de datos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

*Ilustración 23: Actividad de puntuación por lotes de Azure Machine Learning en Data Factory* 

Hay algunos pasos realizados en esta canalización para la preparación de datos para que se puede operationalized con el servicio web de puntuación de lote de Hola. 

![DetectAnomalyPipeline para predecir la necesidad de retirada de vehículos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

*Ilustración 24: DetectAnomalyPipeline para predecir la necesidad de retirada de vehículos* 

***Consulta de Hive de detección de anomalías***

Una vez completada la puntuación de hello, una actividad de HDInsight es tooprocess utilizado y los datos de hello agregado que se clasifican como anomalías por modelo Hola con una puntuación de probabilidad de 0,60 o superior.

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


Una vez que se ejecuta la canalización de hello correctamente, verá Hola después particiones generadas en la cuenta de almacenamiento en el contenedor de "connectedcar" Hola.

![Resultados de DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

*Ilustración 25: Resultados de DetectAnomalyPipeline*

## <a name="publish"></a>Publicar

### <a name="real-time-analysis"></a>Análisis en tiempo real
Una de las consultas de hello en el trabajo de análisis de transmisiones de hello publica la salida de tooan de eventos de hello instancia del concentrador de eventos. 

![Trabajo de Stream Analytics publica la salida de tooan instancia del concentrador de eventos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

*Ilustración 26: análisis de transmisiones publica la salida de tooan instancia del concentrador de eventos*

![Instancia de concentrador de eventos de salida de toohello de toopublish de consultas de análisis de transmisiones](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

*Figura 27: instancia de concentrador de eventos de salida de análisis de transmisiones consulta toopublish toohello*

Hola que realtimedashboardapp incluido en la solución de hello consume este flujo de eventos. Esta aplicación aprovecha el servicio de web de aprendizaje de máquina de solicitud-respuesta de Hola para puntuar en tiempo real y publica Hola de conjunto de datos de Power BI de tooa datos resultantes para su uso. 

### <a name="batch-analysis"></a>Análisis por lotes
resultados de Hola de lote de Hola y el procesamiento en tiempo real son tablas de base de datos de SQL Azure toohello publicada para su uso. Hello Azure SQL Server, base de datos y tablas de Hola se crean automáticamente como parte del script de instalación de Hola. 

![Resultados del procesamiento por lotes copiar el flujo de trabajo de toodata mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

*Figura 28: resultados copiar toodata mart flujo de trabajo de procesamiento por lotes*

![Trabajo de Stream Analytics publica toodata mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

*Figura 29: análisis de transmisiones publica toodata mart*

![Ajuste de puesto de datos en el trabajo de Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

*Ilustración 30: Ajuste de puesto de datos en el trabajo de Stream Analytics*

## <a name="consume"></a>Consumo
Power BI ofrece a esta solución un panel completo para datos en tiempo real y visualizaciones de análisis predictivo. 

Haga clic aquí para obtener instrucciones detalladas sobre cómo configurar informes de Power BI de Hola y el panel de Hola. panel de Hello final tiene este aspecto:

![Panel de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

*Ilustración 31: Panel de Power BI*

## <a name="summary"></a>Resumen
Este documento contiene un desglose detallada de solución de análisis de telemetría de vehículo hello. Se presenta un patrón de arquitectura lambda para análisis en tiempo real y de procesamiento por lotes con predicciones y acciones. Este patrón aplica tooa amplia variedad de casos de uso que requieren la ruta de acceso activa (en tiempo real) y análisis de la ruta de acceso inactivos (lote). 

