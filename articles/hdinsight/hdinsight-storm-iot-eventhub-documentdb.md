---
title: "datos del sensor del vehículo aaaProcess con Apache Storm en HDInsight | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los datos del sensor de vehículo tooprocess desde los centros de eventos con Apache Storm en HDInsight. Agregar datos de modelo de base de datos de Azure Cosmos y almacenar toostorage de salida."
services: hdinsight,documentdb,notification-hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 78980635-8bef-4c33-96c3-fae50e932e31
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/03/2017
ms.author: larryfr
ms.openlocfilehash: 8f7b1dbb9072e095ea32160bb731bedd071288af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>Procese datos del sensor de vehículo de Centros de eventos de Azure con Apache Storm en HDInsight

Obtenga información acerca de cómo los datos del sensor de vehículo tooprocess desde los centros de eventos de Azure con Apache Storm en HDInsight. Este ejemplo lee datos del sensor de centros de eventos de Azure, enriquecer datos Hola haciendo referencia a los datos almacenados en la base de datos de Azure Cosmos. Hola datos se almacenan en el almacenamiento de Azure con hello sistema de archivos de Hadoop (HDFS).

![HDInsight y Hola diagrama de arquitectura de Internet de las cosas (IoT)](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>Información general

Agregar sensores toovehicles le permite toopredict problemas de los equipos en función de las tendencias de los datos históricos. También permite las mejoras de toomake versiones toofuture basadas en el análisis de patrones de uso. Debe ser capaz de tooquickly y cargar eficazmente los datos de Hola de todos los vehículos en Hadoop para que pueda suceder MapReduce procesamiento. Además, es recomendable toodo el análisis de las rutas de acceso de error crítico (temperatura del motor, frenos, etc.) en tiempo real.

Centros de eventos de Azure se basa volumen masivo de hello toohandle de datos generados por sensores. Apache Storm puede ser usado tooload y procesar los datos de hello antes de almacenarlos en HDFS.

## <a name="solution"></a>Solución

Los datos de telemetría para la temperatura del motor, la temperatura ambiente y la velocidad del vehículo se registran mediante sensores. A continuación, se envían datos concentradores tooEvent junto con el número de identificación de vehículo (Niv) del automóvil hello y una marca de tiempo. Desde allí, una topología de Storm con un aluvión de Apache en clúster de HDInsight lee los datos de hello, lo procesa y lo almacena en HDFS.

Durante el procesamiento, Hola Niv es tooretrieve usa información sobre el modelo de base de datos de Cosmos. Estos datos se agregan toohello flujo de datos antes de que se almacene.

componentes de Hello utilizados en hello aluvión de topología son:

* **EventHubSpout** : lee los datos de Centros de eventos de Azure.
* **TypeConversionBolt** -convierte Hola cadena JSON desde los centros de eventos en una tupla que contiene Hola después de los datos de sensor:
    * Engine temperature
    * Temperatura ambiente
    * Velocidad
    * VIN
    * Timestamp
* **DataReferencBolt** -busca modelo del vehículo Hola de base de datos de Cosmos con hello VIN
* **WasbStoreBolt** -Hola de almacenes de datos tooHDFS (almacenamiento de Azure)

Hola después de la imagen es un diagrama de esta solución:

![topología de storm](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>Implementación

Una completa automatizada solución para este escenario está disponible como parte del programa Hola a [HDInsight-Storm-ejemplos](https://github.com/hdinsight/hdinsight-storm-examples) repositorio en GitHub. toouse en este ejemplo, siga los pasos de Hola Hola [IoTExample README. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md).

## <a name="next-steps"></a>Pasos siguientes

Para más topologías de ejemplo de Storm, vea [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).

