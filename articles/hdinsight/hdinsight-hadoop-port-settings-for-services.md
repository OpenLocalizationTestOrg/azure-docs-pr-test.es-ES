---
title: aaaPorts utilizado por los servicios de Hadoop en HDInsight - Azure | Documentos de Microsoft
description: Una lista de puertos utilizados por los servicios Hadoop que se ejecutan en HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd14aed9-ec25-4bb3-a20c-e29562735a7d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 0abc5c1c678aa79816e3e82a74538d2fb6db40ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ports-used-by-hadoop-services-on-hdinsight"></a>Puertos utilizados por los servicios Hadoop en HDInsight

Este documento proporciona una lista de puertos de hello utilizados por servicios de Hadoop que se ejecutan en clústeres de HDInsight basados en Linux. También proporciona información sobre puertos usa tooconnect toohello clúster mediante SSH.

## <a name="public-ports-vs-non-public-ports"></a>Puertos públicos frente a puertos no públicos

Hola de HDInsight basados en Linux clústeres solo exponen tres puertos públicamente en internet; 22, 23 y 443. Estos puertos son clúster de hello acceso toosecurely usado con SSH y servicios expuestos a través de un protocolo HTTPS seguro Hola.

Internamente, HDInsight se implementa mediante varias máquinas virtuales de Azure (nodos de hello en clúster de Hola) se ejecuta en una red Virtual de Azure. Desde dentro de la red virtual de hello, se pueden acceder a puertos no expuestos a través de hello internet. Por ejemplo, si se conecta tooone de nodos principales hello mediante SSH, desde el nodo principal de Hola se pueden, a continuación, acceder directamente a servicios que se ejecutan en nodos de clúster de Hola.

> [!IMPORTANT]
> Si no especifica una red virtual de Azure como una opción de configuración de HDInsight, automáticamente se crea una. Sin embargo, no puede unirse a otra red virtual de toothis máquinas (por ejemplo, otras máquinas virtuales de Azure o el equipo de desarrollo de cliente).


red virtual de toojoin máquinas adicionales toohello, debe crear red virtual de Hola y especificarlo al crear el clúster de HDInsight. Para más información, consulte [Extensión de las funcionalidades de HDInsight con Red virtual de Azure](hdinsight-extend-hadoop-virtual-network.md)

## <a name="public-ports"></a>Puertos públicos

Hola a Hola todos los nodos de un clúster de HDInsight se encuentran en una red Virtual de Azure y no se pueden tener acceso directamente desde internet. Una puerta de enlace pública proporciona toohello de acceso de internet después de puertos, que son comunes a todos los tipos de clúster de HDInsight.

| Servicio | Port | Protocol | Description |
| --- | --- | --- | --- | --- |
| sshd |22 |SSH |Se conecta toosshd de clientes en el nodo principal de hello principal. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |22 |SSH |Se conecta a los clientes toosshd en el nodo del borde de Hola. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |23 |SSH |Se conecta toosshd de clientes en el nodo principal de hello secundaria. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| Ambari |443 |HTTPS |Interfaz de usuario web de Ambari. Vea [administrar HDInsight utilizando Hola Ambari Web UI](hdinsight-hadoop-manage-ambari.md) |
| Ambari |443 |HTTPS |API de REST de Ambari. Vea [administrar HDInsight utilizando Hola Ambari API de REST](hdinsight-hadoop-manage-ambari-rest-api.md) |
| WebHCat |443 |HTTPS |API de REST de HCatalog. Consulte [Uso de Hive con Curl](hdinsight-hadoop-use-pig-curl.md), [Uso de Pig con Curl](hdinsight-hadoop-use-pig-curl.md) y [Uso de MapReduce con Curl](hdinsight-hadoop-use-mapreduce-curl.md). |
| HiveServer2 |443 |ODBC |Se conecta tooHive mediante ODBC. Vea [tooHDInsight Excel conectarse con el controlador ODBC de Microsoft de hello](hdinsight-connect-excel-hive-odbc-driver.md). |
| HiveServer2 |443 |JDBC |Se conecta tooHive mediante JDBC. Vea [conectar tooHive en usar Hola del controlador JDBC de Hive de HDInsight](hdinsight-connect-hive-jdbc-driver.md) |

están disponibles para determinados tipos de clúster Hola siguientes:

| Servicio | Port | Protocol | Tipo de clúster | Description |
| --- | --- | --- | --- | --- |
| Stargate |443 |HTTPS |HBase |API de REST de HBase. Consulte [Introducción al uso de HBase](hdinsight-hbase-tutorial-get-started-linux.md) |
| Livy |443 |HTTPS |Spark |API de REST de Spark. Consulte [Envío de trabajos de Spark remotamente a un clúster de Apache Spark en HDInsight Linux mediante Livy](hdinsight-apache-spark-livy-rest-interface.md) |
| Storm |443 |HTTPS |Storm |La interfaz de usuario web de Storm. Consulte [Implementación y administración de topologías de Apache Storm en HDInsight basado en Linux](hdinsight-storm-deploy-monitor-topology-linux.md) |

### <a name="authentication"></a>Autenticación

Todos los servicios expuestos públicamente en hello que Internet debe ser autenticados:

| Port | Credenciales |
| --- | --- |
| 22 o 23 |credenciales de usuario SSH Hola especificadas durante la creación del clúster |
| 443 |nombre de inicio de sesión de Hello (valor predeterminado: administrador) y la contraseña que estableció durante la creación del clúster |

## <a name="non-public-ports"></a>Puertos no públicos

> [!NOTE]
> Algunos servicios solo están disponibles en determinados tipos de clúster. Por ejemplo, HBase solo está disponible en los tipos de clúster de HBase.

> [!IMPORTANT]
> Algunos servicios solo se ejecutan en un nodo principal cada vez. Si intenta tooconnect toohello servicio en el nodo principal primario de Hola y recibe un error 404, volver a intentarlo con el nodo principal de hello secundaria.

### <a name="ambari"></a>Ambari

| Servicio | Nodos | Port | Ruta de acceso URL | Protocol | 
| --- | --- | --- | --- | --- |
| Interfaz de usuario web de Ambari | Nodos principales | 8080 | / | HTTP |
| API de REST de Ambari | Nodos principales | 8080 | /api/v1 | HTTP |

Ejemplos:

* API de REST de Ambari: `curl -u admin "http://10.0.0.11:8080/api/v1/clusters"`

### <a name="hdfs-ports"></a>Puertos HDFS

| Servicio | Nodos | Port | Protocol | Description |
| --- | --- | --- | --- | --- |
| Interfaz de usuario web de NameNode |Nodos principales |30070 |HTTPS |Estado de tooview de interfaz de usuario Web |
| Servicio de metadatos de NameNode |Nodos principales |8020 |IPC |Metadatos del sistema de archivos |
| DataNode |Todos los nodos de trabajo |30075 |HTTPS |Estado de tooview de interfaz de usuario Web, registros, etcetera. |
| DataNode |Todos los nodos de trabajo |30010 |&nbsp; |Transferencia de datos |
| DataNode |Todos los nodos de trabajo |30020 |IPC |Operaciones de metadatos |
| NameNode secundario |Nodos principales |50090 |HTTP |Punto de control para metadatos de NameNode |

### <a name="yarn-ports"></a>Puertos de YARN

| Servicio | Nodos | Port | Protocol | Description |
| --- | --- | --- | --- | --- |
| Interfaz de usuario web de Resource Manager |Nodos principales |8088 |HTTP |Interfaz de usuario web para Resource Manager |
| Interfaz de usuario web de Resource Manager |Nodos principales |8090 |HTTPS |Interfaz de usuario web para Resource Manager |
| Interfaz de administración de Resource Manager |Nodos principales |8141 |IPC |Para envíos de aplicaciones (Hive, servidor de Hive, Pig, etc.) |
| Programador de Resource Manager |Nodos principales |8030 |HTTP |Interfaz administrativa |
| Interfaz de aplicación de Resource Manager |Nodos principales |8050 |HTTP |Dirección de interfaz del Administrador de aplicaciones de Hola |
| NodeManager |Todos los nodos de trabajo |30050 |&nbsp; |dirección de Hello del Administrador de contenedores de Hola |
| Interfaz de usuario web de NodeManager |Todos los nodos de trabajo |30060 |HTTP |Interfaz de Resource Manager |
| Dirección de escala de tiempo |Nodos principales |10200 |RPC |Hola servicio RPC de escala de tiempo. |
| Interfaz de usuario web de escala de tiempo |Nodos principales |8181 |HTTP |interfaz de usuario de web de servicio de la escala de tiempo Hola |

### <a name="hive-ports"></a>Puertos de Hive

| Servicio | Nodos | Port | Protocol | Description |
| --- | --- | --- | --- | --- |
| HiveServer2 |Nodos principales |10001 |Thrift |Servicio para la conexión tooHive (Thrift/JDBC) |
| Tienda de metadatos Hive |Nodos principales |9083 |Thrift |Servicio de conexión de tooHive de metadatos (Thrift/JDBC) |

### <a name="webhcat-ports"></a>Puertos de WebHCat

| Servicio | Nodos | Port | Protocol | Description |
| --- | --- | --- | --- | --- |
| Servidor de WebHCat |Nodos principales |30111 |HTTP |Web API encima de HCatalog y otros servicios de Hadoop |

### <a name="mapreduce-ports"></a>Puertos de MapReduce

| Servicio | Nodos | Port | Protocol | Description |
| --- | --- | --- | --- | --- |
| Historial de trabajos |Nodos principales |19888 |HTTP |Interfaz de usuario web del historial de trabajos de MapReduce |
| Historial de trabajos |Nodos principales |10020 |&nbsp; |Servidor de historial de trabajos de MapReduce |
| ShuffleHandler |&nbsp; |13562 |&nbsp; |Las transferencias mapa intermedio genera reductores toorequesting |

### <a name="oozie"></a>Oozie

| Servicio | Nodos | Port | Protocol | Description |
| --- | --- | --- | --- | --- |
| Servidor de Oozie |Nodos principales |11000 |HTTP |Dirección URL del servicio de Oozie |
| Servidor de Oozie |Nodos principales |11001 |HTTP |Puerto de administración de Oozie |

### <a name="ambari-metrics"></a>Métricas de Ambari

| Servicio | Nodos | Port | Protocol | Description |
| --- | --- | --- | --- | --- |
| Escala de tiempo (historial de aplicaciones) |Nodos principales |6188 |HTTP |interfaz de usuario de web de servicio de la escala de tiempo Hola |
| Escala de tiempo (historial de aplicaciones) |Nodos principales |30200 |RPC |interfaz de usuario de web de servicio de la escala de tiempo Hola |

### <a name="hbase-ports"></a>Puertos de HBase

| Servicio | Nodos | Port | Protocol | Description |
| --- | --- | --- | --- | --- |
| HMaster |Nodos principales |16000 |&nbsp; |&nbsp; |
| Interfaz de usuario web de información de HMaster |Nodos principales |16010 |HTTP |puerto de Hello para la interfaz de usuario de web de Master HBase Hola |
| Servidor de región |Todos los nodos de trabajo |16020 |&nbsp; |&nbsp; |
| &nbsp; |&nbsp; |2181 |&nbsp; |puerto de Hola que los clientes usan tooconnect tooZooKeeper |

### <a name="kafka-ports"></a>Puertos Kafka

| Servicio | Nodos | Port | Protocol | Description |
| --- | --- | --- | --- | --- |
| Agente |Nodos de trabajo |9092 |[Protocolo de conexión de Kafka](http://kafka.apache.org/protocol.html) |Se utiliza para la comunicación del cliente |
| &nbsp; |Nodos Zookeeper |2181 |&nbsp; |puerto de Hola que los clientes usan tooconnect tooZookeeper |

### <a name="spark-ports"></a>Puertos de Spark

| Servicio | Nodos | Port | Protocol | Ruta de acceso URL | Descripción |
| --- | --- | --- | --- | --- | --- |
| Servidores Thrift de Spark |Nodos principales |10002 |Thrift | &nbsp; | Servicio para conectarse tooSpark SQL (Thrift/JDBC) |
| Servidor Livy | Nodos principales | 8998 | HTTP | /lotes | Servicio para ejecutar instrucciones, trabajos y aplicaciones |

Ejemplos:

* Livy: `curl "http://10.0.0.11:8998/batches"`. En este ejemplo, `10.0.0.11` es dirección IP de hello del nodo principal de Hola que hospeda el servicio Livio Hola.
