---
title: aaaWhat es Apache Storm - HDInsight de Azure | Documentos de Microsoft
description: "Apache Storm permite tooprocess flujos de datos en tiempo real. HDInsight de Azure le permite tooeasily crear clústeres de Storm en hello nube de Azure. Con Visual Studio, puede crear soluciones de Storm utilizando C# y, a continuación, implementar clústeres de HDInsight aluvión de tooyour."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "apache storm casos de uso, el clúster de storm, qué es apache storm"
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6c6b2925ef3e5666dfecc3fb3c835bb362902c51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a>¿Qué es Apache Storm en Azure HDInsight?

[Apache Storm](http://storm.apache.org/) es un sistema de cálculo de código abierto distribuido, con tolerancia a errores. Puede utilizar secuencias de tooprocess aluvión de datos en tiempo real con Hadoop. Las soluciones de Storm también pueden proporcionar garantizado procesamiento de datos, con hello capacidad tooreplay datos que no estaba correctamente procesan Hola primera vez.

Storm en HDInsight proporciona Hola siguientes ventajas principales:

* Actúa como un servicio administrado con un Acuerdo de Nivel de Servicio de un 99,9 % de tiempo de actividad.

* Admite la personalización sencilla mediante la ejecución de scripts en el clúster de Storm durante su creación o después de ella. Para más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).

* Usa diversos lenguajes. Puede escribir componentes de Storm en lenguaje de Hola de su elección, como Java, C# y Python.

    * Se integra Visual Studio con HDInsight para el desarrollo de hello, administración y supervisión de las topologías de C#. Para obtener más información, consulte [topologías de C# Storm desarrollar con hello HDInsight Tools para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

    * Interfaz de admite Hola Trident Java. Puede crear topologías de Storm que admitan el procesamiento de mensajes "exactamente una vez", la persistencia del almacén de datos transaccional y un conjunto de operaciones comunes de Stream Analytics.

*  Escale o reduzca verticalmente clústeres de Storm con facilidad. Puede agregar o quitar nodos de trabajador con ningún impacto toorunning Storm las topologías.

* Se integra con hello después de los servicios de Azure:

    * Azure Event Hubs

    * Red virtual

    * Azure SQL Database

    * Azure Storage

    * Azure Cosmos DB

* Forma segura combina capacidades de Hola de varios clústeres de HDInsight mediante red Virtual. Puede crear canalizaciones analíticas que usen clústeres de Storm, Kafka, Spark, HBase o Hadoop.

Para obtener una lista de empresas que usan Apache Storm con sus soluciones de análisis en tiempo real, consulte las [compañías que usan Apache Storm](https://storm.apache.org/documentation/Powered-By.html).

tooget se hayan iniciado mediante aluvión de, consulte [empezar a trabajar con Storm en HDInsight][gettingstarted].

## <a name="how-does-storm-work"></a>¿Cómo funciona Storm?

Storm ejecuta topologías en lugar de hello trabajos MapReduce que es posible que esté familiarizado con. Las topologías de Storm están formadas por varios componentes que se organizan en un grafo acíclico dirigido (DAG). Los datos fluyen entre los componentes de hello en el gráfico de Hola. Cada componente consume uno o varios flujos de datos y, opcionalmente, puede emitir uno o varios flujos. Hola siguiente diagrama ilustra cómo fluyen los datos entre componentes de una topología básica de recuento de palabras:

![Ejemplo de cómo se organizan los componentes en una topología de Storm](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* Los componentes spout introducen los datos en una topología y Emiten uno o varios flujos en la topología de Hola.

* Los componentes bolt consumen los flujos emitidos desde spouts u otros bolts. Tornillos, opcionalmente, podrían emitir secuencias en la topología de Hola. Tornillos también son responsables de escribir servicios de datos de tooexternal o almacenamiento, como HDFS, Kafka o HBase.

## <a name="ease-of-creation"></a>Creación fácil

Puede aprovisionar un nuevo clúster de Storm en HDInsight en minutos. Para información sobre la creación de un clúster de Storm, consulte [Introducción a Storm en HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

## <a name="ease-of-use"></a>Facilidad de uso

* __Secure Shell (SSH) conectividad__: puede tener acceso a nodos principales del saludo de su clúster de Storm sobre Hola Internet a través de SSH. Puede ejecutar comandos directamente en el clúster mediante SSH.

  Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* __Web conectividad__: clústeres de HDInsight todos los proporcionan la interfaz de usuario de web de hello Ambari. Fácilmente puede supervisar, configurar y administrar servicios en el clúster mediante el uso de la interfaz de usuario de web de hello Ambari. Clústeres de Storm también proporcionan Hola aluvión de interfaz de usuario. Puede supervisar y administrar topologías de Storm ejecución desde el explorador mediante Hola aluvión de interfaz de usuario.

  Para obtener más información, vea hello [HDInsight administrar usando Hola Ambari Web UI](hdinsight-hadoop-manage-ambari.md) y [Monitor y administrar mediante Hola aluvión de interfaz de usuario](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) documentos.

* __Azure PowerShell y la CLI de Azure__: PowerShell y la CLI ambos proporcionan utilidades de línea de comandos que pueden utilizar desde su toowork de sistema de cliente con HDInsight y otros servicios de Azure.

* __Integración de Visual Studio__: Azure Data Lake Tools para Visual Studio incluye plantillas de proyecto para crear topologías aluvión de C# mediante el marco de trabajo de hello SCP.Net. Herramientas de datos Lake también proporcionan herramientas toodeploy, supervisar y administrar soluciones con Storm en HDInsight.

  Para obtener más información, consulte [topologías de C# Storm desarrollar con hello HDInsight Tools para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="integration-with-other-azure-services"></a>Integración con otros servicios de Azure

* __Azure Data Lake Store__: para ver un ejemplo del uso de Data Lake Store con un clúster de Storm, consulte [Uso de Azure Data Lake Store con Apache Storm con HDInsight](hdinsight-storm-write-data-lake-store.md).

* __Los concentradores de eventos__: para obtener un ejemplo del uso de los centros de eventos con un clúster de Storm, vea Hola siguientes documentos:

    * [Desarrollo de una topología basada en Java para Storm en HDInsight](hdinsight-storm-develop-java-topology.md)

    * [Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (C#)](hdinsight-storm-develop-csharp-event-hub-topology.md)

* __Base de datos SQL__, __Cosmos DB__, __centros de eventos__, y __HBase__: ejemplos de plantillas se incluyen en hello Data Lake Tools para Visual Studio. Para más información, consulte [Desarrollo de topologías de C# para Storm en HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="reliability"></a>Confiabilidad

Apache Storm garantiza que siempre por completo se procesa cada mensaje entrante, incluso cuando el análisis de datos de Hola se extienden a cientos de nodos.

nodo de Hello Nimbus proporciona funcionalidad similar toohello Hadoop JobTracker y se asignan tareas tooother nodos de un clúster a través de Zookeeper. Los nodos de zookeeper proporcionan coordinación para un clúster y facilitan la comunicación entre Nimbus y proceso de Supervisor en nodos de trabajador de Hola Hola. Si falla un nodo de procesamiento, se le informará de nodo de hello Nimbus y asigna tareas de Hola y el nodo de tooanother de datos asociados.

configuración predeterminada de Hola para clústeres de Apache Storm es solo un nodo de Nimbus toohave. Storm en HDInsight proporciona dos nodos Nimbus. Si se produce un error en el nodo principal de hello, clúster de Storm Hola cambia nodo secundario toohello mientras se recupera el nodo principal de Hola. Hello siguiente diagrama muestra configuración de flujo de la tarea de Hola para Storm en HDInsight:

![Diagrama de nimbus, zookeeper y supervisor](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a>Escala

Los clústeres de HDInsight se pueden escalar dinámicamente mediante la adición o supresión de nodos de trabajo. Esta operación puede realizarse durante el procesamiento de datos.

> [!IMPORTANT]
> tootake aprovechar nuevos nodos agregadas a través de ajuste de escala, necesita las topologías de Storm toorebalance iniciadas antes de que se incrementa el tamaño del clúster Hola.

## <a name="support"></a>Soporte técnico

Storm en HDInsight incluye soporte técnico completo y continuo de nivel de empresa. Storm en HDInsight también tiene un Acuerdo de Nivel de Servicio del 99,9 %. Esto significa que se garantiza que un clúster de Storm tiene conectividad externa al menos un 99,9% del tiempo de Hola.

Para más información, consulte [Soporte técnico de Azure](https://azure.microsoft.com/support/options/).

## <a name="apache-storm-use-cases"></a>Casos de uso de Apache Storm

siguiente Hola muestran algunos escenarios comunes que puede usar Storm en HDInsight:

* Internet de las cosas (IoT)
* Detección de fraudes
* Análisis social
* Extracción, transformación y carga de datos (ETL)
* Supervisión de redes
* Search
* Mobile Engagement

Para obtener información sobre situaciones del mundo real, vea hello [modo en que las empresas usan Storm](https://storm.apache.org/documentation/Powered-By.html) documento.

## <a name="development"></a>Desarrollo

Los desarrolladores de .NET pueden diseñar e implementar topologías en C# mediante las Herramientas de Data Lake para Visual Studio. También puede crear topologías híbridas que usen los componentes de Java y C#.

Para más información, consulte [Desarrollo de topologías de C# para Storm en HDInsight con Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

También puede desarrollar soluciones de Java mediante el uso de hello IDE de su elección. Para más información, consulte [Desarrollo de topologías de Java para Storm en HDInsight](hdinsight-storm-develop-java-topology.md).

Python también puede ser utilizados toodevelop Storm componentes. Para más información, consulte [Desarrollo de topologías Apache Storm con Python en HDInsight](hdinsight-storm-develop-python-topology.md).

## <a name="common-development-patterns"></a>Patrones de desarrollo comunes

### <a name="guaranteed-message-processing"></a>Procesamiento de mensajes garantizado

Apache Storm puede proporcionar diferentes niveles de procesamiento de mensajes garantizado. Por ejemplo, una aplicación básica de Storm puede garantizar un procesamiento una vez al menos y Trident puede garantizar exactamente el procesamiento una vez.

Para obtener más información, consulte las [Garantías en el procesamiento de los datos](https://storm.apache.org/about/guarantees-data-processing.html) en apache.org.

### <a name="ibasicbolt"></a>IBasicBolt

Hola patrón de leer una tupla de entrada, la emisión de cero o más tuplas, y, a continuación, acking Hola entrada tupla inmediatamente al final de Hola de hello execute (método) es común. Storm proporciona hello [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) interfaz tooautomate este patrón.

### <a name="joins"></a>Combinaciones

El modo en que se unen las secuencias de datos varía entre aplicaciones. Por ejemplo, puede unir las tuplas procedentes de varios flujos en uno nuevo o unir únicamente los lotes de tuplas de una ventana específica. En cualquier caso, se puede realizar la unión mediante el uso de [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Campo de agrupación es una forma de definir cómo tuplas son toobolts enrutado.

Hola siguiente ejemplo de Java, fieldsGrouping es tooroute usado tuplas que se originan en componentes de "1", "2" y "3" toohello MyJoiner rayo:

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a>Lotes

Apache Storm proporciona un mecanismo de temporización interno conocido como "tupla tick". Puede establecer con qué frecuencia se genera una tupla tick en la topología.

Para ver un ejemplo del uso de una tupla tick desde un componente de C#, consulte [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).

### <a name="caches"></a>Memorias caché

El almacenamiento en caché de memoria interna se usa a menudo como mecanismo para acelerar el procesamiento, porque mantiene en memoria los activos usados con mayor frecuencia. Como una topología se distribuye entre varios nodos, y varios proceso dentro de cada nodo, debe considerar el uso de [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Use `fieldsGrouping` tooensure que tuplas que contiene campos de Hola que se usan para la búsqueda en la caché siempre son toohello enrutado mismo proceso. Esta funcionalidad de agrupación evita la duplicación de entradas de caché entre procesos.

### <a name="stream-top-n"></a>Secuencia "N principal"

Cuando la topología depende de calcular un valor top N, calcular el valor de top N de hello en paralelo. A continuación, Hola resultado de la combinación de esos cálculos en un valor global. Esta operación puede realizarse mediante [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute por campo para el procesamiento paralelo. A continuación, puede enrutar rayo tooa que global determina el valor de top N de Hola.

Para obtener un ejemplo de cálculo de un valor top N, vea hello [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) ejemplo.

## <a name="logging"></a>Registro

Storm utiliza Apache Log4j toolog información. De forma predeterminada, se registra una gran cantidad de datos, y puede ser difícil toosort a través de información de Hola. Puede incluir un archivo de configuración de registro como parte de su comportamiento de registro de toocontrol de topología de Storm.

Para una topología de ejemplo que muestra cómo tooconfigure registro, consulte [basados en Java WordCount](hdinsight-storm-develop-java-topology.md) ejemplo de Storm en HDInsight.

## <a name="next-steps"></a>Pasos siguientes

Aprenda más sobre las soluciones de análisis en tiempo real con Storm en HDInsight:

* [Introducción a Apache Storm en HDInsight][gettingstarted]
* [Topologías de ejemplo para Apache Storm en HDInsight](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
