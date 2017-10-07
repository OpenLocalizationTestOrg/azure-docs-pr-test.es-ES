---
title: aaaTroubleshoot Storm mediante el uso de HDInsight de Azure | Documentos de Microsoft
description: Obtenga respuestas toocommon preguntas sobre el uso de Apache Storm con HDInsight de Azure.
keywords: "Azure HDInsight, Storm, preguntas más frecuentes, guía de solución de problemas, problemas comunes"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a>Solución de problemas de Storm mediante Azure HDInsight

Obtenga información acerca de los principales problemas de Hola y sus soluciones para trabajar con cargas de Apache Storm en Apache Ambari.

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a>¿Cómo obtengo acceso Hola aluvión de interfaz de usuario en un clúster
Tiene dos opciones para tener acceso a Hola aluvión de interfaz de usuario desde un explorador:

### <a name="ambari-ui"></a>Interfaz de usuario de Ambari
1. Vaya a Panel de Ambari toohello.
2. En la lista de hello de servicios, seleccione **Storm**.
3. Hola **vínculos rápidos** menú, seleccione **aluvión de interfaz de usuario**.

### <a name="direct-link"></a>Vínculo directo
Puede tener acceso a Hola aluvión de interfaz de usuario en hello después de la dirección URL:

https://\<nombre DNS del clúster\>/stormui

Ejemplo:

 https://stormcluster.azurehdinsight.net/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a>Cómo transferir información de punto de comprobación de Storm eventos concentrador pitorro de una topología tooanother

Cuando se desarrollan las topologías que leen desde los centros de eventos de Azure mediante Hola archivo .jar de HDInsight Storm eventos concentrador pitorro, debe implementar una topología que tiene el mismo nombre en un nuevo clúster de Hola. Sin embargo, debe conservar los datos de punto de comprobación de Hola que estaba confirmada tooApache ZooKeeper en el clúster antiguo Hola.

### <a name="where-checkpoint-data-is-stored"></a>Dónde se almacenan los datos de punto de control
Datos de punto de control de los desplazamientos se almacenan por hello pitorro de concentrador de eventos en ZooKeeper en dos rutas de acceso raíz:
- Los puntos de control de spout no transaccionales se almacenan en /eventhubspout.
- Los datos de punto de control de spout de transacciones se almacenan en /transactional.

### <a name="how-toorestore"></a>Cómo toorestore
secuencias de comandos de tooget hello y bibliotecas que se utilizan datos de tooexport fuera ZooKeeper y, a continuación, importa Hola datos atrás tooZooKeeper con un nombre nuevo, consulte [ejemplos aluvión de HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).

carpeta de "lib" Hello tiene archivos .jar que contienen la implementación de hello para la operación de exportación/importación de Hola. carpeta de bash Hello tiene un script de ejemplo que muestra cómo tooexport datos de Hola server ZooKeeper en el clúster antiguo hello y después importarlos a un servidor de ZooKeeper toohello atrás en el nuevo clúster de Hola.

Ejecute hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script de Hola ZooKeeper nodos tooexport y, a continuación, importar datos. Hola script toohello correcta Hortonworks Data Platform (HDP) versión de actualización. (Estamos trabajando en que estos scripts sean genéricos en HDInsight. Scripts genéricos pueden ejecutar desde cualquier nodo en clúster de hello sin modificaciones por el usuario de Hola.)

comando de exportación de Hello escribe Hola metadatos tooan sistema de archivos distribuido de Apache Hadoop (HDFS) ruta de acceso (en un almacén de almacenamiento de blobs de Azure o almacén de Azure Data Lake) en una ubicación que se establece.

### <a name="examples"></a>Ejemplos

#### <a name="export-offset-metadata"></a>Exportación de los metadatos de desplazamiento
1. Usar clústeres SSH toogo toohello ZooKeeper en clúster de Hola desde qué punto de control de hello desplazamiento debe toobe exportado.
2. Hola ejecución comando siguiente (después de actualizar la cadena de versión HDP hello) tooexport ZooKeeper desplazamiento datos toohello /stormmetadta/zkdata HDFS ruta de acceso:

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>Importación de los metadatos de desplazamiento
1. Usar clústeres SSH toogo toohello ZooKeeper en clúster de Hola desde qué punto de control de hello desplazamiento debe toobe exportado.
2. Ejecución hello después del comando (después de actualizar la cadena de versión de Hola HDP) tooimport ZooKeeper desplazamiento datos Hola HDFS ruta de acceso/stormmetadata/zkdata toohello ZooKeeper servidor en clúster de destino de hello:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a>Eliminar los metadatos de desplazamiento para que las topologías pueden comenzar a procesar datos desde el principio de Hola o de una marca de tiempo que el usuario Hola elige
1. Usar clústeres SSH toogo toohello ZooKeeper en clúster de Hola desde qué punto de control de hello desplazamiento debe toobe exportado.
2. Ejecución hello después del comando (después de actualizar la cadena de versión de Hola HDP) toodelete todos los ZooKeeper desplazamiento datos en el clúster de hello actual:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>Cómo se buscan los archivos binarios de Storm en un clúster
Los archivos binarios de aluvión de pila actual de HDP de hello están en /usr/hdp/current/storm-client. ubicación de Hello es Hola mismo para los nodos principales y para los nodos de trabajador.
 
Puede haber varios archivos binarios para versiones específicas de HDP en /usr/hdp (por ejemplo, /usr/hdp/2.5.0.1233/storm). carpeta de Hello /usr/hdp/current/storm-client es symlinked toohello versión más reciente que se ejecuta en el clúster de Hola.

Para obtener más información, consulte [clúster de HDInsight de tooan de conectar a través de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) y [Storm](http://storm.apache.org/).
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a>¿Cómo se puede determinar la topología de implementación de Hola de un clúster de Storm
En primer lugar, identifique todos los componentes que se instalan con Storm de HDInsight. Un clúster de Storm consta de cuatro categorías de nodo:

* Nodos de puerta de enlace
* Nodos principales
* Nodos de ZooKeeper
* Nodos de trabajo
 
### <a name="gateway-nodes"></a>Nodos de puerta de enlace
Un nodo de puerta de enlace es una puerta de enlace y el servicio de proxy inverso que permite el servicio de administración de acceso público tooan active Ambari. También controla la elección del líder de Ambari.
 
### <a name="head-nodes"></a>Nodos principales
Nodos principales del aluvión ejecutan hello siguientes servicios:
* Nimbus
* Servidor Ambari
* Servidor de métricas de Ambari
* Recopilador de métricas de Ambari
 
### <a name="zookeeper-nodes"></a>Nodos de ZooKeeper
HDInsight incluye un cuórum de ZooKeeper de tres nodos. tamaño de quórum de Hello es fijo y no se puede reconfigurar.
 
Servicios de Storm en clúster de hello son quórum de tooautomatically configurado uso hello ZooKeeper.
 
### <a name="worker-nodes"></a>Nodos de trabajo
Nodos de trabajador de Storm ejecutan hello siguientes servicios:
* Supervisor
* Máquinas virtuales Java (JVM) de trabajo, para topologías en ejecución
* Agente de Ambari
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>Localización de los archivos binarios del spout del centro de eventos de Storm para el desarrollo
 
Para obtener más información acerca del uso de archivos .jar de Storm eventos concentrador pitorro con la topología, consulte Hola recursos siguientes.
 
### <a name="java-based-topology"></a>Topología basada en Java
[Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (Java)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>Topología basada en C# (Mono en clústeres de Storm Linux HDInsight 3.4 o superior)
[Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>Archivos binarios de spout del centro de eventos de Storm para clústeres de Storm Linux HDInsight 3.5 y superior
toolearn cómo toouse hello más reciente Storm eventos concentrador pitorro que funciona con HDInsight 3.5 + aluvión de Linux clústeres, vea hello mvn-repo [archivo Léame](https://github.com/hdinsight/mvn-repo/blob/master/README.md).
 
### <a name="source-code-examples"></a>Ejemplos de código fuente
Vea [ejemplos](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) de cómo tooread y escribir desde el centro de eventos de Azure mediante una topología de Apache Storm (escrita en Java) en un clúster de HDInsight de Azure.
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a>Cómo se pueden encontrar los archivos de configuración Log4J de Storm en clústeres
 
archivos de configuración de tooidentify Log4J Apache para servicios de Storm.
 
### <a name="on-head-nodes"></a>En nodos principales
se lee la configuración de Hello Nimbus Log4J desde/usr/hdp/\<versión HDP\>/storm/log4j2/cluster.xml.
 
### <a name="on-worker-nodes"></a>En nodos de trabajo
configuración de supervisor Log4J Hola se lee desde/usr/hdp/\<versión HDP\>/storm/log4j2/cluster.xml.
 
archivo de configuración de trabajo Log4J Hola se lee desde/usr/hdp/\<versión HDP\>/storm/log4j2/worker.xml.
 
Ejemplos: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml

