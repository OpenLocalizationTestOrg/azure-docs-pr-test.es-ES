---
title: aaaTroubleshoot YARN mediante el uso de HDInsight de Azure | Documentos de Microsoft
description: "Obtenga respuestas toocommon preguntas sobre cómo trabajar con Apache Hadoop YARN y HDInsight de Azure."
keywords: "Azure HDInsight, YARN, preguntas más frecuentes, guía de solución de problemas, preguntas comunes"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a>Solución de problemas de YARN mediante Azure HDInsight

Obtenga información acerca de los principales problemas de Hola y sus soluciones cuando se trabaja con cargas de Apache Hadoop YARN en Ambari de Apache.

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a>Creación de una nueva cola de YARN en un clúster


### <a name="resolution-steps"></a>Pasos de la solución 

A continuación Hola use los pasos de Ambari toocreate una nueva cola YARN y equilibrar, a continuación, la asignación de capacidad de hello entre todas las colas de Hola. 

En este ejemplo, dos colas existentes (**predeterminado** y **thriftsvr**) ambos se cambian de 50% capacidad too25% de la capacidad, que proporciona la nueva capacidad de 50% de cola (spark) Hola.
| Cola | Capacity | Capacidad máxima |
| --- | --- | --- | --- |
| default | 25 % | 50 % |
| thrftsvr | 25 % | 50 % |
| spark | 50 % | 50 % |

1. Seleccione hello **Ambari vistas** icono y el patrón de cuadrícula de hello, a continuación, seleccione. A continuación, seleccione **YARN Queue Manager** (Administrador de colas de YARN).

    ![Seleccione Hola vistas Ambari icono](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. Seleccione hello **predeterminado** cola.

    ![Seleccione Hola predeterminado cola](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. Para hello **predeterminado** de cola, cambie hello **capacidad** del 50% too25%. Para hello **thriftsvr** de cola, cambie hello **capacidad** too25%.

    ![Cambiar la capacidad de hello too25% para las colas de forma predeterminada y thriftsvr de Hola](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. toocreate una nueva cola, seleccione **agregar cola**.

    ![Selección de Agregar cola](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. Nombre hello nueva cola.

    ![Nombre de cola de hello Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. Deje hello **capacidad** valores al 50% y, a continuación, seleccione hello **acciones** botón.

    ![Seleccione el botón de acciones de Hola](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. Seleccione **Save and Refresh Queues** (Guardar y actualizar colas).

    ![Selección de Save and Refresh Queues (Guardar y actualizar colas)](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

Estos cambios son visibles inmediatamente en hello YARN programador UI.

### <a name="additional-reading"></a>Lecturas adicionales

- [YARN CapacityScheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a>Descarga de los registros de YARN desde un clúster


### <a name="resolution-steps"></a>Pasos de la solución 

1. Conecta el clúster de HDInsight de toohello con un cliente de Shell seguro (SSH). Para más información, consulte [Lecturas adicionales](#additional-reading-2).

2. toolist todos Hola Id. de aplicación de las aplicaciones de hilo de Hola que se están ejecutando, ejecute hello siguiente comando:

    ```apache
    yarn top
    ```
    Hello identificadores aparecen en hello **APPLICATIONID** columna. Puede descargar los registros de hello **APPLICATIONID** columna.

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. registros de contenedor YARN toodownload para todos los patrones de aplicación, use Hola siguiente comando:
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    Este comando crea un archivo de registro denominado amlogs.txt. 

4. registros de contenedor YARN toodownload para solo Hola última aplicación maestra, utilice Hola siguiente comando:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    Este comando crea un archivo de registro denominado latestamlogs.txt. 

4. registros de contenedor YARN toodownload para patrones de aplicación dos primera hello, utilice Hola siguiente comando:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    Este comando crea un archivo de registro denominado first2amlogs.txt. 

5. toodownload todos los registros de contenedor de hilo, utilice Hola comando siguiente:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    Este comando crea un archivo de registro denominado logs.txt. 

6. registro de contenedor de toodownload hello YARN para un contenedor específico, Hola de uso siguiente comando:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    Este comando crea un archivo de registro denominado containerlogs.txt.

### <a name="additional-reading-2"></a>Lecturas adicionales

- [Conectar tooHDInsight (Hadoop) a través de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [Apache Hadoop Yarn concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/) (Conceptos y aplicaciones de YARN en Apache Hadoop)







