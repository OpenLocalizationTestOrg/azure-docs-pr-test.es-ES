---
title: "topologías de Apache Storm aaaExample en HDInsight | Documentos de Microsoft"
description: "Una lista de topologías de ejemplo de Storm creada y probada con Apache Storm en HDInsight, incluidas las topologías básicas de C# y Java, y trabajando con Event Hubs."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f9b1bdff-5928-4705-a76d-52fd200917cb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: b20299112f6489b7c99360f0a539fc732703c64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>Topologías y componentes de ejemplo de Storm para Apache Storm en HDInsight

Hola mostramos una lista de ejemplos creadas y mantenidas por Microsoft para su uso con Apache Storm en HDInsight. Estos ejemplos abarcan una gran variedad de temas de creación básico de C# y Java topologías tooworking con servicios de Azure como centros de eventos, base de datos de Cosmos, Power BI, base de datos SQL, HBase en HDInsight y el almacenamiento de Azure. Algunos ejemplos se muestra también cómo toowork con tecnologías distintas de Azure, o incluso no son de Microsoft, como SignalR y Socket.IO.

| Descripción | Muestra | Lenguaje/Marco de trabajo |
|:--- |:--- |:--- |
| [Escribir tooAzure almacén de Data Lake de Apache Storm](hdinsight-storm-write-data-lake-store.md) |Escribir tooAzure almacén de Data Lake |Java |
| [Origen de spout y bolt de Centro de eventos](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |Origen hello apetezca charlar un concentrador de eventos y rayo |Java |
| [Desarrollo de topologías basadas en Java para Apache Storm en HDInsight][5797064f] |Maven |Java |
| [Desarrollo de topologías de C# para Apache Storm en HDInsight con Visual Studio][16fce2d1] |Herramientas de HDInsight para Visual Studio |C#, Java |
| [Creación de varios flujos de datos en una topología de Storm en C#][ec5a4064] |Varios flujos |C# |
| [Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (C#)][844d1d81] |Event Hubs |C# y Java |
| [Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md) |Event Hubs |Java |
| [Usar datos de Power Bi toovisualize de una topología de Storm][94d15238] |Power BI |C# |
| [Analyzing sensor data with Storm and HBase in HDInsight][ab894747] [Análisis de los datos de sensor con Storm y HBase en HDInsight] |Event Hubs, HBase, Socket.IO, panel Web |C#, Java, JavaScript, HTML |
| [Procesamiento de los datos de sensor del vehículo desde Event Hubs usando Storm en HDInsight][246ee964] |Event Hubs, Cosmos DB y Azure Storage Blob (WASB) |C#, Java |
| [Extracción, transformación y carga (ETL) de tooHBase de centros de eventos de Azure, mediante Storm en HDInsight][b4b68194] |Event Hubs, HBase |C# |
| [Proyecto de topología de Storm en C# para plantillas para trabajar con servicios de Azure desde Storm en HDInsight][ce0c02a2] |Event Hubs, Cosmos DB, SQL Database, HBase y SignalR |C#, Java |
| [Pruebas comparativas de escalabilidad para leer desde Azure Event Hubs usando Storm en HDInsight][d6c540e3] |Rendimiento de mensajes, Event Hubs, SQL Database |C#, Java |
| [Poner en correlación eventos con Storm y HBase en HDInsight](hdinsight-storm-correlation-topology.md) |HBase |C# |
| [Usar Python con Storm en HDInsight](hdinsight-storm-develop-python-topology.md) |Componentes de Python con una topología Flux |Python |
| [Uso de Kafka con Storm en HDInsight](hdinsight-apache-storm-with-kafka.md) | Lectura de Apache Storm y escribir tooApache Kafka | Java |

### <a name="next-steps"></a>Pasos siguientes

* [Introducción a Apache Storm en HDInsight][2b8c3488]
* [Obtenga información acerca de cómo toodeploy y administrar topologías de Storm con Storm en HDInsight][6eb0d3b8]

[2b8c3488]: hdinsight-apache-storm-tutorial-get-started-linux.md "Obtenga información acerca de cómo toocreate una tormenta en clúster de HDInsight y utilice Hola topologías de ejemplo de panel de Storm toodeploy."
[6eb0d3b8]: hdinsight-storm-deploy-monitor-topology.md "Obtenga información acerca de cómo toodeploy y administrar topologías con hello basada en web aluvión de panel y aluvión de interfaz de usuario o hello HDInsight Tools para Visual Studio."
[16fce2d1]: hdinsight-storm-develop-csharp-visual-studio-topology.md "Obtenga información acerca de cómo las topologías de C# Storm toocreate mediante el uso de Hola HDInsight Tools para Visual Studio."
[5797064f]: hdinsight-storm-develop-java-topology.md "Obtenga información acerca de cómo toocreate topologías de Storm en Java, con Maven, mediante la creación de una topología de wordcount básica."
[94d15238]: hdinsight-storm-power-bi-topology.md "Muestra cómo toowrite datos tooPower BI de una topología de C#, a continuación, crear un gráfico y el panel de datos de Hola."
[ec5a4064]: https://github.com/Blackmist/csharp-storm-example "Muestra una topología básica de Storm que realiza un recuento de palabras, implementada en C#. Esto también demuestra cómo toocreate secuencias de datos múltiples dentro de una topología de C#."
[844d1d81]: hdinsight-storm-develop-csharp-event-hub-topology.md "Obtenga información acerca de cómo tooread y escribir datos desde los centros de eventos de Azure con Storm en HDInsight."
[ab894747]: hdinsight-storm-sensor-data-analysis.md "Obtenga información acerca de cómo visualizar mediante D3.js toouse Apache Storm en los datos de sensor tooprocess de HDInsight de centros de eventos de Azure y (opcionalmente), guárdela en tooHBase."
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "Obtenga información acerca de cómo la toouse una tormenta topología tooread los mensajes desde los centros de eventos de Azure, lea los documentos de base de datos de Azure Cosmos para hacer referencia a datos y guardar tooAzure almacenamiento de datos."
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "Varias topologías toodemonstrate rendimiento al leer desde los centros de eventos de Azure y almacenar tooSQL base de datos utilizando Apache Storm en HDInsight."
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "Obtenga información acerca de cómo Hola datos tooread datos de los centros de eventos de Azure, agregado y transformar del menú y después almacenan tooHBase en HDInsight."
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "Este proyecto contiene plantillas para toointeract spouts, tornillos y topologías con varios servicios de Azure como base de datos SQL, base de datos de Cosmos y centros de eventos."

