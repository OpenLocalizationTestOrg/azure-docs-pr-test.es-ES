---
title: aaaApache Spark streaming con Kafka - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse datos de Spark Apache Spark toostream entra y sale Kafka Apache mediante DStreams. En este ejemplo, se transmiten datos con Jupyter Notebook de Spark en HDInsight."
keywords: ejemplo de kafka, kafka zookeeper, spark streaming kafka, ejemplo de spark streaming kafka
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a>Ejemplo de streaming de Apache Spark (DStream) con Kafka (versión preliminar) en HDInsight

Obtenga información acerca de cómo toouse datos de Spark Apache Spark toostream entre o salga de Apache Kafka en HDInsight con DStreams. Este ejemplo utiliza Jupyter notebook que se ejecuta en el clúster de Spark Hola.
> [!NOTE]
> pasos de Hello en este documento crea un grupo de recursos de Azure que contiene tanto un Spark en HDInsight y un Kafka en clúster de HDInsight. Estos clústeres son ambos ubicados en una red Virtual de Azure, lo que permite hello toodirectly de clúster de Spark comunican con hello clúster Kafka.
>
> Cuando haya terminado con pasos de hello en este documento, recuerde toodelete Hola clústeres tooavoid exceso cargos.

## <a name="create-hello-clusters"></a>Crear clústeres de Hola

Apache Kafka en HDInsight no ofrece acceso toohello Kafka corredores de bolsa respecto Hola internet pública. Todo lo que tooKafka debe estar en las conversaciones Hola misma red virtual de Azure como nodos de hello en Hola clúster Kafka. En este ejemplo, hello Kafka y clústeres de Spark se encuentran en una red virtual de Azure. Hello diagrama siguiente muestra cómo fluye la comunicación entre clústeres de hello:

![Diagrama de clústeres Spark y Kafka en una red virtual de Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Aunque Kafka propio es limitado toocommunication dentro de la red virtual de hello, otros servicios en clúster de hello como SSH y Ambari pueden tener acceso a través de Hola a internet. Para obtener más información sobre los puertos públicos de hello disponibles con HDInsight, vea [puertos y URI utilizado por HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Si bien puede crear una red virtual de Azure, Kafka y Spark clústeres manualmente, resulta más fácil toouse una plantilla de Azure Resource Manager. Use Hola siguientes pasos le indican una red virtual de Azure, Kafka, toodeploy y Spark clústeres tooyour suscripción de Azure.

1. Usar hello siguientes toosign de botón en tooAzure y plantilla abierto Hola Hola portal de Azure.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello plantilla de Azure Resource Manager se encuentra en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > disponibilidad de tooguarantee de Kafka en HDInsight, el clúster debe contener al menos tres nodos de trabajador. Esta plantilla crea un clúster de Kafka que contiene tres nodos de trabajo.

    Esta plantilla crea un clúster de HDInsight 3.6 para Kafka y Spark.

2. Hola uso seguidas de hello las entradas de información toopopulate hello **implementación personalizada** hoja:
   
    ![Implementación personalizada de HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Grupo de recursos**: cree un nuevo grupo de recursos o seleccione uno existente. Este grupo contiene clúster de HDInsight Hola.

    * **Ubicación**: seleccione una tooyou geográficamente cerrar de ubicación.

    * **Nombre de clúster base**: este valor se utiliza como nombre de base de Hola para clústeres de Spark y Kafka Hola. Por ejemplo, si especifica **hdi**, creará un clúster Spark denominado spark-hdi__ y un clúster Kafka denominado **kafka-hdi**.

    * **Nombre de usuario de inicio de sesión del clúster**: nombre de usuario de administrador de Hola para clústeres de Spark y Kafka Hola.

    * **Contraseña de inicio de sesión del clúster**: contraseña de usuario de administrador de Hola para clústeres de Spark y Kafka de Hola.

    * **Nombre de usuario SSH**: Hola toocreate de usuario SSH para clústeres de Spark y Kafka Hola.

    * **Contraseña SSH**: contraseña de hello para el usuario SSH de Hola para clústeres de Spark y Kafka Hola.

3. Hola de lectura **términos y condiciones**y, a continuación, seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**.

4. Finalmente, compruebe **Pin toodashboard** y, a continuación, seleccione **compra**. Tarda aproximadamente 20 minutos toocreate clústeres Hola.

Una vez que se han creado los recursos de hello, son hoja tooa redirigida Hola grupo de recursos que contiene los clústeres de Hola y el panel de la web.

![Hoja de grupo de recursos de red virtual de Hola y clústeres](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Tenga en cuenta que los nombres de Hola de clústeres de HDInsight de hello **BASENAME spark** y **kafka BASENAME**, donde BASENAME es el nombre hello proporcionado toohello plantilla. Utilice estos nombres en pasos posteriores al conectarse a clústeres de toohello.

## <a name="use-hello-notebooks"></a>Utilizar blocs de notas de Hola

código de Hello de ejemplo de Hola descrita en este documento está disponible en [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).

Siga los pasos de Hola Hola `README.md` toocomplete de archivos en este ejemplo.

## <a name="delete-hello-cluster"></a>Eliminar el clúster de Hola

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Puesto que los pasos de hello en este documento para crear ambos Hola de clústeres en el mismo grupo de recursos de Azure, puede eliminar el grupo de recursos de Hola Hola portal de Azure. Eliminando grupo de hello quita todos los recursos creados siguiendo este documento, el Hola red Virtual de Azure y la cuenta de almacenamiento usan los clústeres de Hola.

## <a name="next-steps"></a>Pasos siguientes

En este ejemplo, ha aprendido cómo toouse inspirará tooread y escribir tooKafka. Utilice Hola siguiendo vínculos toodiscover otro toowork maneras con Kafka:

* [Introducción a Apache Kafka en HDInsight](hdinsight-apache-kafka-get-started.md)
* [Usar MirrorMaker toocreate una réplica de Kafka en HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Uso de Apache Kafka con Storm en HDInsight](hdinsight-apache-storm-with-kafka.md)

