---
title: "aaaApache Spark estructurado de transmisión por secuencias con Kafka - HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Apache Spark transmisión por secuencias (DStream) tooget datos entre o salga de Apache Kafka. En este ejemplo, se transmiten datos con Jupyter Notebook de Spark en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>Uso del flujo estructurado de Spark con Kafka (versión preliminar) en HDInsight

Obtenga información acerca de cómo toouse Spark estructurado de transmisión por secuencias de datos de tooread de Kafka de Apache en HDInsight de Azure.

El flujo estructurado de Spark es un motor de procesamiento de flujo basado en Spark SQL. Permite que los cálculos de transmisión por secuencias de tooexpress Hola igual que el cálculo de lote de datos estáticos. Para obtener más información sobre estructurado de transmisión por secuencias, vea hello [estructurado Streaming Guía de programación [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) en Apache.org.

> [!IMPORTANT]
> En este ejemplo se utiliza Spark 2.1 en HDInsight 3.6. La versión de la funcionalidad de flujo estructurado se considera __alfa__ en Spark 2.1.
>
> pasos de Hello en este documento crea un grupo de recursos de Azure que contiene tanto un Spark en HDInsight y un Kafka en clúster de HDInsight. Estos clústeres son ambos ubicados en una red Virtual de Azure, lo que permite hello toodirectly de clúster de Spark comunican con hello clúster Kafka.
>
> Cuando haya terminado con pasos de hello en este documento, recuerde toodelete Hola clústeres tooavoid exceso cargos.

## <a name="create-hello-clusters"></a>Crear clústeres de Hola

Apache Kafka en HDInsight no ofrece acceso toohello Kafka corredores de bolsa respecto Hola internet pública. Todo lo que tooKafka debe estar en las conversaciones Hola misma red virtual de Azure como nodos de hello en Hola clúster Kafka. En este ejemplo, hello Kafka y clústeres de Spark se encuentran en una red virtual de Azure. Hello diagrama siguiente muestra cómo fluye la comunicación entre clústeres de hello:

![Diagrama de clústeres Spark y Kafka en una red virtual de Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Hola servicio Kafka es limitado toocommunication dentro de la red virtual de Hola. Otros servicios en clúster de hello, como SSH y Ambari, puede tener acceso a través de Hola a internet. Para obtener más información sobre los puertos públicos de hello disponibles con HDInsight, vea [puertos y URI utilizado por HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Si bien puede crear una red virtual de Azure, Kafka y Spark clústeres manualmente, resulta más fácil toouse una plantilla de Azure Resource Manager. Use Hola siguientes pasos le indican una red virtual de Azure, Kafka, toodeploy y Spark clústeres tooyour suscripción de Azure.

1. Usar hello siguientes toosign de botón en tooAzure y plantilla abierto Hola Hola portal de Azure.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello plantilla de Azure Resource Manager se encuentra en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.

    Esta plantilla crea Hola recursos siguientes:

    * Un clúster de Kafka en HDInsight 3.5
    * Un clúster de Spark en HDInsight 3.6
    * Una red Virtual de Azure, que contiene los clústeres de HDInsight Hola.

    > [!IMPORTANT]
    > Hola estructurado streaming Bloc de notas utilizado en este ejemplo requiere Spark en HDInsight 3.6. Si usa una versión anterior de Spark en HDInsight, recibirá errores al usar el Bloc de notas de Hola.

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

Una vez que se han creado los recursos de hello, son hoja del grupo de recursos de toohello redirigida.

![Hoja de grupo de recursos de red virtual de Hola y clústeres](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Tenga en cuenta que los nombres de Hola de clústeres de HDInsight de hello **BASENAME spark** y **kafka BASENAME**, donde BASENAME es el nombre hello proporcionado toohello plantilla. Utilice estos nombres en pasos posteriores al conectarse a clústeres de toohello.

## <a name="get-hello-kafka-brokers"></a>Obtener hello Kafka corredores de bolsa

código de este ejemplo Hello conecta toohello Kafka hosts en clúster Kafka Hola de broker. toofind Hola hosts de broker Kafka, usar hello PowerShell o Bash ejemplo siguiente:

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> En este ejemplo espera `$PASSWORD` toocontain contraseña de Hola para inicio de sesión de clúster de hello, y `$CLUSTERNAME` toocontain nombre de Hola de hello clúster Kafka.
>
> Este ejemplo utiliza hello [jq](https://stedolan.github.io/jq/) datos de utilidad tooparse fuera del documento JSON de Hola.

Hola de salida es toohello similar siguiente texto:

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Guarde esta información, tal como se utiliza en hello siguientes secciones de este documento.

## <a name="get-hello-notebooks"></a>Obtener los blocs de notas de Hola

código de Hello de ejemplo de Hola descrita en este documento está disponible en [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).

## <a name="upload-hello-notebooks"></a>Cargar blocs de notas de Hola

Usar hello siguiendo los pasos tooupload Hola blocs de notas de hello proyecto tooyour Spark en clúster de HDInsight:

1. En el explorador web, conéctese toohello Jupyter notebook en su clúster Spark. Hola después de la dirección URL, reemplace `CLUSTERNAME` con el nombre de hello del clúster Kafka:

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    Cuando se le solicite, escriba inicio de sesión de clúster de hello (admin) y la contraseña que utilizó cuando creó el clúster de Hola.

2. Desde Hola superior derecha de la página de hello, use hello __cargar__ Hola de botón tooupload __secuencia-Tweets-To_Kafka.ipynb__ clúster toohello de archivos. Seleccione __abiertos__ carga de hello toostart.

    ![Usar Hola carga botón tooselect y cargar un bloc de notas](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Seleccione el archivo de hello KafkaStreaming.ipynb](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. Buscar hello __secuencia-Tweets-To_Kafka.ipynb__ entrada de lista de Hola de blocs de notas y seleccione __cargar__ junto a él.

    ![Carga de uso Hola situado junto a la tooupload de entrada de hello KafkaStreaming.ipynb se toohello servidor de Bloc de notas](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. Repita los pasos Hola de 1 a 3 tooload __Spark-estructura-Streaming-de-Kafka.ipynb__ Bloc de notas.

## <a name="load-tweets-into-kafka"></a>Carga de tweets en Kafka

Una vez que se han cargado los archivos de hello, seleccione hello __secuencia-Tweets-To_Kafka.ipynb__ Bloc de notas de entrada tooopen Hola. Siga los pasos Hola Hola Bloc de notas tooload tweets en Kafka.

## <a name="process-tweets-using-spark-structured-streaming"></a>Procesamiento de tweets mediante el flujo estructurado de Spark

En página principal de Jupyter Notebook hello, seleccione hello __Spark-estructura-Streaming-de-Kafka.ipynb__ entrada. Siga los pasos Hola Hola Bloc de notas tooload tweets desde Kafka mediante transmisión por secuencias estructurado Spark.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo toouse Spark estructurado transmisión por secuencias, vea Hola después toolearn documentos más sobre cómo trabajar con Spark y Kafka:

* [¿Cómo toouse inspirará transmisión por secuencias (DStream) con Kafka](hdinsight-apache-spark-with-kafka.md).
* [Introducción a Jupyter Notebook y Spark en HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md)