---
title: aaaUse Kafka Apache con Storm en HDInsight - Azure | Documentos de Microsoft
description: "Apache Kafka se instala con Apache Storm en HDInsight. Obtenga información acerca de cómo toowrite tooKafka y, a continuación, leer de él, con Hola KafkaBolt y KafkaSpout componentes suministrados con Storm. También Obtenga información acerca cómo toouse Hola toodefine del marco de trabajo de un flujo y enviar las topologías de Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a>Uso de Apache Kafka (versión preliminar) con Storm en HDInsight

Obtenga información acerca de cómo toouse Apache Storm tooread de y escribir tooApache Kafka. En este ejemplo también muestra cómo sistema utilizado por HDInsight del archivo de datos de toosave de un toohello de topología de Storm HDFS compatible.

> [!NOTE]
> pasos de Hello en este documento crea un grupo de recursos de Azure que contiene tanto una tormenta de HDInsight y un Kafka en clúster de HDInsight. Estos clústeres son ambos ubicados en una red Virtual de Azure, lo que permite hello toodirectly de clúster de Storm comunican con hello clúster Kafka.
> 
> Cuando haya terminado con pasos de hello en este documento, recuerde toodelete Hola clústeres tooavoid exceso cargos.

## <a name="get-hello-code"></a>Obtener el código de hello

código de Hello de ejemplo de Hola usado en este documento está disponible en [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).

toocompile este proyecto, deberá Hola siguiente configuración para el entorno de desarrollo:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versiones posteriores. HDInsight 3.5 y versiones posteriores requieren Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

* Un cliente de SSH (necesita hello `ssh` y `scp` comandos): para obtener información, consulte [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Un editor de texto o IDE.

Hello siguientes variables de entorno pueden establecerse cuando se instalación Java y Hola JDK en su estación de trabajo de desarrollo. Sin embargo, debe comprobar que existan y que contienen valores correctos de hello para el sistema.

* `JAVA_HOME`-debe apuntar toohello directorio donde hello JDK está instalado.
* `PATH`-debe contener Hola siguiendo las rutas de acceso:
  
    * `JAVA_HOME`(o la ruta de acceso equivalente hello).
    * `JAVA_HOME\bin`(o la ruta de acceso equivalente hello).
    * directorio de Hola donde está instalado Maven.

## <a name="create-hello-clusters"></a>Crear clústeres de Hola

Apache Kafka en HDInsight no ofrece acceso toohello Kafka corredores de bolsa respecto Hola internet pública. Todo lo que tooKafka debe estar en las conversaciones Hola misma red virtual de Azure como nodos de hello en Hola clúster Kafka. En este ejemplo, hello Kafka y clústeres de Storm se encuentran en una red virtual de Azure. Hello diagrama siguiente muestra cómo fluye la comunicación entre clústeres de hello:

![Diagrama de clústeres Storm y Kafka en una red virtual de Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> Otros servicios en clúster de Hola Hola a como SSH y Ambari pueden tener acceso a través de internet. Para obtener más información sobre los puertos públicos de hello disponibles con HDInsight, vea [puertos y URI utilizado por HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Aunque puede crear una red virtual de Azure, Kafka, y aluvión de clústeres manualmente, resulta más fácil toouse una plantilla de Azure Resource Manager. Use Hola siguientes pasos le indican una red virtual de Azure, Kafka, toodeploy y aluvión de clústeres tooyour suscripción de Azure.

1. Usar hello siguientes toosign de botón en tooAzure y plantilla abierto Hola Hola portal de Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello plantilla de Azure Resource Manager se encuentra en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**. Se crea Hola recursos siguientes:
    
    * Grupo de recursos de Azure
    * Red virtual
    * Cuenta de almacenamiento de Azure
    * Kafka en HDInsight versión 3.6 (tres nodos de trabajo)
    * Storm en HDInsight versión 3.6 (tres nodos de trabajo)

  > [!WARNING]
  > disponibilidad de tooguarantee de Kafka en HDInsight, el clúster debe contener al menos tres nodos de trabajador. Esta plantilla crea un clúster de Kafka que contiene tres nodos de trabajo.

2. Hola de uso después de las entradas de orientación toopopulate hello en hello **implementación personalizada** hoja:
   
    ![Implementación personalizada de HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * **Grupo de recursos**: cree un nuevo grupo de recursos o seleccione uno existente. Este grupo contiene clúster de HDInsight Hola.
   
    * **Ubicación**: seleccione una tooyou geográficamente cerrar de ubicación.

    * **Nombre de clúster base**: este valor se utiliza como nombre de base de Hola para clústeres de Storm y Kafka Hola. Por ejemplo, si especifica **hdi**, creará un clúster Storm llamado **storm-hdi** y un clúster Kafka llamado **kafka-hdi**.
   
    * **Nombre de usuario de inicio de sesión del clúster**: nombre de usuario de administrador de Hola para clústeres de Storm y Kafka Hola.
   
    * **Contraseña de inicio de sesión del clúster**: contraseña de usuario de administrador de Hola para clústeres de Storm y Kafka de Hola.
    
    * **Nombre de usuario SSH**: Hola toocreate de usuario SSH para clústeres de Storm y Kafka Hola.
    
    * **Contraseña SSH**: contraseña de hello para el usuario SSH de Hola para clústeres de Storm y Kafka Hola.

3. Hola de lectura **términos y condiciones**y, a continuación, seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**.

4. Finalmente, compruebe **Pin toodashboard** y, a continuación, seleccione **compra**. Tarda aproximadamente 20 minutos toocreate clústeres Hola.

Una vez que se han creado los recursos de hello, se muestra la hoja de hello para el grupo de recursos de Hola.

![Hoja de grupo de recursos de red virtual de Hola y clústeres](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> Tenga en cuenta que los nombres de Hola de clústeres de HDInsight de hello **BASENAME storm** y **kafka BASENAME**, donde BASENAME es el nombre hello proporcionado toohello plantilla. Utilice estos nombres en pasos posteriores al conectarse a clústeres de toohello.

## <a name="understanding-hello-code"></a>Comprensión del código de hello

Este proyecto contiene dos topologías:

* **KafkaWriter**: definido por hello **writer.yaml** archivo, esta topología escribe tooKafka frases aleatorio con hello KafkaBolt proporcionada con Apache Storm.

    Esta topología utiliza un personalizado **SentenceSpout** frases aleatorio de toogenerate de componente.

* **KafkaReader**: definido por hello **reader.yaml** archivo, esta topología lee datos del Kafka con hello KafkaSpout proporcionada con Apache Storm después registros Hola toostdout de datos.

    Esta topología utiliza el Hola Storm HdfsBolt toowrite datos toodefault almacenamiento de clúster de Storm Hola.
### <a name="flux"></a>Flux

topologías de saludo se definen mediante [flujo](https://storm.apache.org/releases/1.1.0/flux.html). Un flujo se introdujo en Storm 0.10.x y permite la configuración de la topología tooseparate Hola desde el código de hello. Para las topologías que utilizan el marco de trabajo de un flujo de hello, topología Hola se define en un archivo YAML. archivo de Hello YAML puede incluirse como parte de topología de Hola. También puede ser un archivo independiente que se usa al enviar topología Hola. Flux también admite la sustitución de variables en tiempo de ejecución, que se usa en este ejemplo.

Hola se establecen los parámetros siguientes en tiempo de ejecución para estas topologías:

* `${kafka.topic}`: nombre de Hola de hello tema Kafka que topologías Hola lectura/escritura para.

* `${kafka.broker.hosts}`: Hola hospeda esa hello Kafka establece ejecutar en. información de agente de Hola se usa por hello KafkaBolt al escribir tooKafka.

* `${kafka.zookeeper.hosts}`: hosts de Hola que Zookeeper se ejecuta en Hola clúster Kafka.

Para más información sobre las topologías de Flux, vea [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="download-and-compile-hello-project"></a>Descargar y compile el proyecto de Hola

1. En el entorno de desarrollo, descargue el proyecto de Hola de [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), abra una línea de comandos y cambie la ubicación de toohello de directorios que descargó el proyecto de Hola.

2. De hello **hdinsight-storm-java-kafka** directorio comando proyecto de hello toocompile siguiente de Hola de uso y crea un paquete de implementación:

  ```bash
  mvn clean package
  ```

    proceso de paquetes de saludo crea un archivo denominado `KafkaTopology-1.0-SNAPSHOT.jar` en hello `target` directory.

3. Usar hello siguiente comandos toocopy Hola paquete tooyour aluvión de clúster de HDInsight. Reemplace **nombre de usuario** con nombre de usuario SSH de hello para el clúster de Hola. Reemplace **BASENAME** con el nombre de base de Hola que utilizó al crear el clúster de Hola.

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    Cuando se le solicite, escriba contraseña Hola que utilizó al crear clústeres de Hola.

## <a name="configure-hello-topology"></a>Configurar topología Hola

1. Utilice uno de hello siguiendo métodos toodiscover Hola hosts de agente de Kafka:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Hello intensiva de ejemplo se da por supuesto que `$CLUSTERNAME` contiene el nombre de Hola Hola del clúster de HDInsight. También se supone que [jq](https://stedolan.github.io/jq/) está instalado. Cuando se le solicite, escriba la contraseña de hello para la cuenta de inicio de sesión de clúster de Hola.

    valor de Hello devuelto es similar toohello siguiente texto:

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > Aunque puede haber más de dos hosts de agente para el clúster, no es necesario tooprovide una lista completa de todos los tooclients de hosts. Con uno o dos es suficiente.

2. Use uno de hello siguientes hosts de métodos toodiscover hello Kafka Zookeeper:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Hello intensiva de ejemplo se da por supuesto que `$CLUSTERNAME` contiene el nombre de Hola Hola del clúster de HDInsight. También se supone que [jq](https://stedolan.github.io/jq/) está instalado. Cuando se le solicite, escriba la contraseña de hello para la cuenta de inicio de sesión de clúster de Hola.

    valor de Hello devuelto es similar toohello siguiente texto:

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > Aunque hay más de dos nodos de Zookeeper, no es necesario tooprovide una lista completa de todos los tooclients de hosts. Con uno o dos es suficiente.

    Guarde este valor, porque se usará más adelante.

3. Editar hello `dev.properties` archivo en hello raíz del proyecto de Hola. Agregar Hola Broker y líneas coincidentes del toohello Zookeeper hosts información en este archivo. Hello en el ejemplo siguiente se se configura con los valores de ejemplo de Hola de los pasos anteriores de hello:

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. Guardar hello `dev.properties` archivo y después usar Hola siguientes comando tooupload, clúster de Storm toohello:

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    Reemplace **nombre de usuario** con nombre de usuario SSH de hello para el clúster de Hola. Reemplace **BASENAME** con el nombre de base de Hola que utilizó al crear el clúster de Hola.

## <a name="start-hello-writer"></a>Escritor de Hola de inicio

1. Usar hello después de clúster de Storm toohello tooconnect mediante SSH. Reemplace **nombre de usuario** con nombre de usuario SSH Hola utilizado al crear el clúster de Hola. Reemplace **BASENAME** con el nombre de base de hello usado al crear el clúster de Hola.

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    Cuando se le solicite, escriba contraseña Hola que utilizó al crear clústeres de Hola.
   
    Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Desde Hola conexión SSH, use Hola después comando toocreate hello tema Kafka utilizado por la topología de hello:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    Reemplace `$KAFKAZKHOSTS` con hello Zookeeper hospedar la información recuperada en la sección anterior de Hola.

2. Desde el clúster de Storm de hello SSH conexión toohello, usar hello después de la topología de sistema de escritura de comando toostart hello:

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    parámetros de Hello utilizados con este comando son:

    * `org.apache.storm.flux.Flux`: Se usa un flujo tooconfigure y ejecutar esta topología.

    * `--remote`: Enviar Hola topología tooNimbus. topología de Hola se distribuye entre los nodos de trabajador de hello en clúster de Hola.

    * `-R /writer.yaml`: Hola usar `writer.yaml` topología de hello tooconfigure de archivos. `-R`indica que este recurso se incluye en el archivo jar de Hola. Está en la raíz Hola jar de hello, por lo que `/writer.yaml` es hello tooit de ruta de acceso.

    * `--filter`: Rellenar las entradas de hello `writer.yaml` topología con valores de hello `dev.properties` archivo. Hola por ejemplo, el valor de hello `kafka.topic` entrada de archivo hello es tooreplace usado hello `${kafka.topic}` entrada en la definición de la topología de Hola.

5. Una vez que ha iniciado la topología de hello, utilice Hola después tooverify de comando que está escribiendo datos toohello tema Kafka:

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    Reemplace `$KAFKAZKHOSTS` con hello Zookeeper hospedar la información recuperada en la sección anterior de Hola.

    Este comando usa un script incluido con el tema de Kafka toomonitor Hola. Tras unos instantes, debe iniciar devolver frases aleatorias que se han escrito toohello tema. Hola de salida es similar toohello siguiente ejemplo:

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    Utilice Ctrl + c toostop script de Hola.

## <a name="start-hello-reader"></a>Lector de Hola de inicio

1. Desde el clúster de Storm del toohello Hola de sesión SSH, use Hola después de la topología de lector de comando toostart hello:

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. Una vez que se inicia la topología de hello, abra Hola aluvión de interfaz de usuario. Esta interfaz de usuario web se encuentra en https://storm-BASENAME.azurehdinsight.net/stormui. Reemplace __BASENAME__ con el nombre de base de Hola utilizada cuando se creó el clúster de Hola. 

    Cuando se le pida, use el nombre de inicio de sesión de administrador de hello (de forma predeterminada, `admin`) y la contraseña que utilizó al crea el clúster de Hola. Vea un toohello similar de página web después de imagen:

    ![UI de Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. En hello aluvión de interfaz de usuario, seleccione hello __kafka lector__ vínculo Hola __resumen de la topología__ sección toodisplay saber hello __kafka lector__ topología.

    ![Sección Resumen de topología de interfaz de usuario de web de Storm Hola](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. toodisplay información acerca de las instancias de hello del componente de registrador rayo hello, seleccione hello __registrador rayo__ vínculo Hola __tornillos (todo tiempo)__ sección.

    ![Vínculo de rayo de registrador en hello tornillos sección](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. Hola __ejecutor__ sección, seleccione un vínculo en hello __puerto__ información de registro de toodisplay de columna acerca de esta instancia de componente de Hola.

    ![Vínculo Executors](./media/hdinsight-apache-storm-with-kafka/executors.png)

    registro de Hello contiene un registro de datos de hello leídos de hello tema Kafka. información de Hello en el registro de hello es similar toohello siguiente texto:

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a>Detener las topologías de Hola

Desde un clúster de Storm toohello de sesión SSH, use Hola siguiendo las topologías de comandos toostop Hola Storm:

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a>Eliminar el clúster de Hola

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Puesto que los pasos de hello en este documento para crear ambos Hola de clústeres en el mismo grupo de recursos de Azure, puede eliminar el grupo de recursos de Hola Hola portal de Azure. Eliminando grupo de recursos de hello quita todos los recursos creados siguiendo este documento.

## <a name="next-steps"></a>Pasos siguientes

Para ver más ejemplos de topologías que pueden utilizarse con Storm en HDInsight, consulte [Topologías y componentes de ejemplo de Storm para Apache Storm en HDInsight](hdinsight-storm-example-topology.md).

Para más información sobre la implementación y supervisión de topologías en HDInsight basado en Linux, consulte [Implementación y administración de topologías de Apache Storm en HDInsight basado en Linux](hdinsight-storm-deploy-monitor-topology-linux.md).