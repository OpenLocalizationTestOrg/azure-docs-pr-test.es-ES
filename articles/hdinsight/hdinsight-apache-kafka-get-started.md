---
title: aaaStart con Apache Kafka - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una Kafka Apache de clúster de HDInsight de Azure. Obtenga información acerca de cómo toocreate temas, los suscriptores y los consumidores."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a>Introducción a Apache Kafka (versión preliminar) en HDInsight

Obtenga información acerca de cómo toocreate y utilizar una [Kafka Apache](https://kafka.apache.org) clúster de HDInsight de Azure. Kafka es una plataforma de streaming distribuida de código abierto que está disponible con HDInsight. A menudo se usa como un agente de mensajes, ya que proporciona una funcionalidad similar tooa publicación / suscripción cola de mensajes.

> [!NOTE]
> Actualmente hay dos versiones de Kafka disponibles con HDInsight; 0.9.0 (HDInsight 3.4) y 0.10.0 (HDInsight 3.5 y 3.6). Hola en este documento da por sentado que está usando a Kafka en 3.6 de HDInsight.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a>Creación de un clúster de Kafka

Usar hello siguiendo los pasos toocreate un Kafka en clúster de HDInsight:

1. De hello [portal de Azure](https://portal.azure.com), seleccione **+ nuevo**, **Intelligence + análisis**y, a continuación, seleccione **HDInsight**.
   
    ![Creación de un clúster de HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. De **Fundamentos**, escriba Hola siguiente información:

    * **Nombre del clúster**: nombre de Hola Hola del clúster de HDInsight.
    * **Suscripción**: seleccione Hola suscripción toouse.
    * **Nombre de usuario de inicio de sesión del clúster** y **contraseña de inicio de sesión de clúster**: inicio de sesión de hello al tener acceso a los clústeres de Hola a través de HTTPS. Utilice estos servicios de tooaccess de credenciales como Hola interfaz de usuario de Ambari Web o API de REST.
    * **Secure Shell (SSH) username**: inicio de sesión de hello usado al acceder a clúster hello mediante SSH. De forma predeterminada contraseña hello es Hola igual que la contraseña de inicio de sesión de clúster de Hola.
    * **Grupo de recursos**: clúster hello toocreate de grupo de recursos de hello en.
    * **Ubicación**: Hola región de Azure toocreate Hola clúster.
   
 ![Seleccione la suscripción.](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. Seleccione **clúster tipo**, y, a continuación, conjunto Hola siguiendo los valores de **configuración de clúster**:
   
    * **Tipo de clúster**: Kafka

    * **Versión**: Kafka 0.10.0 (HDI 3.6)

    * **Nivel de clúster**: estándar
     
 Por último, utilice hello **seleccione** botón toosave configuración.
     
 ![Seleccionar el tipo de clúster](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. Después de seleccionar el tipo de clúster de hello, usar hello __seleccione__ tooset Hola clúster tipo de botón. A continuación, usar hello __siguiente__ configuración básica del botón toofinish.

5. Desde **Storage**, seleccione o cree una cuenta de Storage. Para conocer los pasos hello en este documento, deje Hola otros campos en los valores predeterminados de Hola. Hola de uso __siguiente__ configuración de almacenamiento de toosave de botón.

    ![Establecer la configuración de cuenta de almacenamiento de Hola para HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. De __aplicaciones (opcionales)__, seleccione __siguiente__ toocontinue. Para este ejemplo no se requieren aplicaciones.

7. De __tamaño de clúster__, seleccione __siguiente__ toocontinue.

    > [!WARNING]
    > disponibilidad de tooguarantee de Kafka en HDInsight, el clúster debe contener al menos tres nodos de trabajador.

    ![Hola de conjunto de tamaño de clúster Kafka](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > Hola **discos por nodo de trabajo** controles de entrada de Hola escalabilidad de Kafka en HDInsight. Para más información, consulte [Configure storage and scalability for Apache Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Configuración del almacenamiento y escalabilidad de Apache Kafka en HDInsight).

8. De __configuración avanzada__, seleccione __siguiente__ toocontinue.

9. De hello **resumen**, revisar configuración de hello para el clúster de Hola. Hola de uso __editar__ vincula toochange cualquier configuración que no sean correcta. Por último, utilice el clúster de the__Create__ botón toocreate Hola.
   
    ![Resumen de configuración del clúster](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > Puede durar de clúster de too20 minutos toocreate Hola.

## <a name="connect-toohello-cluster"></a>Conectar el clúster toohello

> [!IMPORTANT]
> Al realizar Hola pasos, debe utilizar a un cliente de SSH. Para obtener más información, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

Desde el cliente, use SSH tooconnect toohello clúster:

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

Reemplace **SSHUSER** con nombre de usuario SSH de hello proporcionado durante la creación del clúster. Reemplace **CLUSTERNAME** con nombre de hello del clúster de Hola.

Cuando se le solicite, escriba contraseña de hello destinadas Hola SSH cuenta.

Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="getkafkainfo"></a>Obtener información de hello Zookeeper y agente de host

Cuando se trabaja con Kafka, debe conocer los dos valores de host; Hola *Zookeeper* hello y hosts *Broker* hosts. Estos hosts se usan con hello Kafka API y muchas de las utilidades de Hola que se suministran con Kafka.

Use Hola siguientes pasos le indican las variables de entorno de toocreate que contienen información de host de Hola. Estas variables de entorno se utilizan en los pasos de hello en este documento.

1. Desde un clúster de toohello de conexión de SSH, comando hello tooinstall siguiente de Hola de uso `jq` utilidad. Esta utilidad es tooparse usado documentos JSON y es útil para recuperar la información de host de agente de hello:
   
    ```bash
    sudo apt -y install jq
    ```

2. variables de entorno de hello tooset con la información se recuperan de Ambari, Hola de uso después de comandos:

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > Establecer `CLUSTERNAME=` toohello nombre de clúster Kafka Hola. Establecer `PASSWORD=` toohello contraseña de inicio de sesión (admin) que utilizó al crear el clúster de Hola.

    Hello texto siguiente es un ejemplo de contenido de Hola de `$KAFKAZKHOSTS`:
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    Hello texto siguiente es un ejemplo de contenido de Hola de `$KAFKABROKERS`:
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > Hola `cut` comando es la lista de Hola de tootrim uso de entradas de host de hosts tootwo. No es necesario lista completa de hello tooprovide de hosts al crear un productor o consumidor de Kafka.
   
    > [!WARNING]
    > No confíe en la información de hello devuelta por esta sesión tooalways sea exacto. Si ajusta el clúster de hello, corredores de bolsa nuevos se agregan o se quitan. Si se produce un error y se reemplaza un nodo, puede cambiar el nombre de host de hello para el nodo de Hola.
    >
    > Debe recuperar la información de hosts de Zookeeper y agente de hello poco antes de usarlo tooensure tiene información válida.

## <a name="create-a-topic"></a>de un tema

Kafka almacena los flujos de datos en categorías denominadas *temas*. Desde un SSH conexión tooa clúster nodo principal, use una secuencia de comandos proporcionada con Kafka toocreate un tema:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

Este comando conecta tooZookeeper utilizando información de host de hello almacenada en `$KAFKAZKHOSTS`y, a continuación, crear tema Kafka llamado **probar**. También puede comprobar que ese tema Hola se creó mediante Hola script toolist temas siguientes:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

Hello resultado de este comando enumera temas Kafka, que contiene Hola **probar** tema.

## <a name="produce-and-consume-records"></a>Generación y consumo de registros

Kafka almacena *registros* en temas. Los registros se generan mediante *productores* y se consumen mediante *consumidores*. Los productores recuperan registros de *agentes* de Kafka. Cada nodo de trabajo del clúster de HDInsight es un agente de Kafka.

Usar hello siguientes registros de toostore de pasos en el tema de prueba de Hola que creó anteriormente y, a continuación, leerlos mediante un consumidor:

1. Desde la sesión de SSH de hello, use un script que se proporciona con el tema de Kafka toowrite registros toohello:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    No se devuelven toohello símbolo del sistema después de este comando. En su lugar, escriba algunos mensajes de texto y, a continuación, utilice **Ctrl + C** toostop enviar toohello tema. Cada línea se envía como un registro independiente.

2. Utilice una secuencia de comandos con registros de tooread de Kafka de tema de hello:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    Este comando recupera los registros de Hola de tema de Hola y mostrarlos. Usar `--from-beginning` indica Hola consumidor toostart desde principio Hola de secuencia de hello, por lo que se recuperan todos los registros.

3. Use __Ctrl + C__ consumidor de hello toostop.

## <a name="producer-and-consumer-api"></a>API de productor y consumidor

Mediante programación puede generar y consumir los registros mediante hello [Kafka API](http://kafka.apache.org/documentation#api). toobuild un productor de Java y el consumidor, utilice Hola siguiendo los pasos de su entorno de desarrollo.

> [!IMPORTANT]
> Debe tener Hola instalados en el entorno de desarrollo de los componentes siguientes:
>
> * [Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o equivalente, como OpenJDK.
>
> * [Apache Maven](http://maven.apache.org/)
>
> * Un cliente de SSH y hello `scp` comando. Para obtener más información, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

1. Descargar ejemplos de hello de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started). Por ejemplo de productores y consumidores de hello, utilice el proyecto de hello en hello `Producer-Consumer` directory. Este ejemplo contiene Hola siguientes clases:
   
    * **Ejecute** -inicia el consumidor de Hola o productor.

    * **Productor** -almacenes 1.000.000 registros toohello tema.

    * **Consumidor** -lee los registros de tema de Hola.

2. toocreate un paquete jar, cambiar la ubicación de toohello de directorios de hello `Producer-Consumer` Hola de directorio y el uso siguiente comando:

    ```
    mvn clean package
    ```

    Este comando crea un directorio denominado `target`, que contiene un archivo denominado `kafka-producer-consumer-1.0-SNAPSHOT.jar`.

3. Siguiente de hello use comandos hello toocopy `kafka-producer-consumer-1.0-SNAPSHOT.jar` clúster de HDInsight de tooyour de archivo:
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    Reemplace **SSHUSER** con el usuario SSH de hello para el clúster y reemplazar **CLUSTERNAME** con nombre hello del clúster. Cuando se le solicite escribir contraseña de hello para el usuario SSH Hola.

4. Una vez Hola `scp` comando termina de copiar el archivo hello, conecte el clúster toohello mediante SSH. Usar hello comando toowrite registros toohello prueba tema siguiente:

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. Una vez que ha finalizado el proceso de hello, utilice Hola siguientes tooread de comando de tema de hello:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    registros de Hello leídos, junto con un recuento de registros, se muestra. Puede ver algunas más de 1.000.000 registran como enviados tema de toohello varios registros mediante un script en un paso anterior.

6. Use __Ctrl + C__ consumidor de hello tooexit.

### <a name="multiple-consumers"></a>Varios consumidores

Los consumidores de Kafka usan un grupo de consumidores al leer los registros. Con hello misma grupo con varios consumidores resultados en la carga equilibrada las lecturas de un tema. Cada consumidor en grupo Hola recibe una parte de los registros de Hola. toosee este proceso en acción, Hola uso siguiendo los pasos:

1. Abra un nuevo clúster de toohello de sesión SSH, para que tenga dos de ellos. En cada sesión, use Hola siguientes toostart un consumidor con Hola mismo Id. de grupo de consumidor:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    Este comando inicia un consumidor con el Id. de grupo de hello `mygroup`.

    > [!NOTE]
    > Usar comandos de hello en hello [obtener información de hello Zookeeper y agente host](#getkafkainfo) tooset sección `$KAFKABROKERS` para esta sesión SSH.

2. Observe cómo cada sesión recuentos Hola los registros que recibe de tema de Hola. total de Hola de ambas sesiones debe Hola mismo tal y como se ha recibido previamente de un consumidor.

Consumo de los clientes dentro de hello mismo grupo se controla a través de las particiones de hello para el tema de Hola. Para hello `test` tema creado anteriormente, tiene ocho particiones. Si abre las sesiones SSH ocho e iniciar un consumidor en todas las sesiones, cada consumidor lee los registros de una única partición para el tema de Hola.

> [!IMPORTANT]
> No puede haber más instancias de consumidor en un grupo de consumidores que particiones. En este ejemplo, un grupo de consumidor puede contener una tooeight consumidores ya que es el número de Hola de particiones en el tema de Hola. O bien, puede tener varios grupos de consumidores, los cuales no tengan más de ocho consumidores cada uno.

Registros guardados en Kafka se almacenan en orden de Hola se reciben dentro de una partición. tooachieve ordenada de entrega para los registros *dentro de una partición*, cree un grupo de consumidores donde hello número de instancias de consumidor coincide con hello de particiones. tooachieve ordenada de entrega para los registros *en el tema de hello*, cree un grupo de consumidores con instancia de un solo consumidor.

## <a name="streaming-api"></a>API de streaming

Hola API de transmisión por secuencias se agregó tooKafka en versión 0.10.0; las versiones anteriores se basan en Apache Spark o aluvión de para el procesamiento de la secuencia.

1. Si aún no lo ha hecho, descargue los ejemplos de hello de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour entorno de desarrollo. Para la transmisión por secuencias de ejemplo de Hola, utilice el proyecto de hello en hello `streaming` directory.
   
    Este proyecto contiene solo una clase, `Stream`, que lee los registros de hello `test` tema creado anteriormente. Recuentos de palabras de hello leer y emite cada tema tooa word y recuento llamado `wordcounts`. Hola `wordcounts` tema se crea en un paso más adelante en esta sección.

2. Desde la línea de comandos de hello en el entorno de desarrollo, cambiar la ubicación de toohello de directorios de hello `Streaming` directorio y, a continuación, Hola use después el comando toocreate un paquete jar:

    ```bash
    mvn clean package
    ```

    Este comando crea un directorio denominado `target`, que contiene un archivo denominado `kafka-streaming-1.0-SNAPSHOT.jar`.

3. Siguiente de hello use comandos hello toocopy `kafka-streaming-1.0-SNAPSHOT.jar` clúster de HDInsight de tooyour de archivo:
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    Reemplace **SSHUSER** con el usuario SSH de hello para el clúster y reemplazar **CLUSTERNAME** con nombre hello del clúster. Cuando se le solicite escribir contraseña de hello para el usuario SSH Hola.

4. Una vez Hola `scp` comando termina de copiar el archivo hello, conéctese clúster toohello mediante SSH y, a continuación, usar hello después comando toocreate hello `wordcounts` tema:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. A continuación, inicie Hola streaming proceso mediante el uso de hello siguiente comando:
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    Este comando inicia Hola proceso en segundo plano de Hola de transmisión por secuencias.

6. Siguiente Hola de uso del comando toosend mensajes toohello `test` tema. Estos mensajes se procesan por hello transmisión por secuencias de ejemplo:
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. Hola de uso después de la salida del comando tooview Hola escrita toohello `wordcounts` tema por hello streaming proceso:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > datos de hello tooview, debe indicar clave hello tooprint Hola y Hola deserializador toouse para hello clave y valor. nombre de clave de Hello es palabra Hola y clave-valor hello contiene el recuento de Hola.
   
    Hola de salida es toohello similar siguiente texto:
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > recuento de Hola incrementa cada vez que se encuentra una palabra.

7. Usar hello __Ctrl + C__ tooexit Hola consumidor, a continuación, usar hello `fg` comando toobring Hola transmisión por secuencias de primer plano de back-toohello de tareas de fondo. Use __Ctrl + C__ tooexit también.

## <a name="delete-hello-cluster"></a>Eliminar el clúster de Hola

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Solución de problemas

Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Pasos siguientes

En este documento, ha aprendido los conceptos básicos de hello sobre cómo trabajar con Apache Kafka en HDInsight. Usar hello después toolearn más acerca de cómo trabajar con Kafka:

* [Alta disponibilidad de los datos con Apache Kafka (versión preliminar) en HDInsight](hdinsight-apache-kafka-high-availability.md)
* [Aumento de la escalabilidad mediante la configuración de discos administrados con Kafka en HDInsight](hdinsight-apache-kafka-scalability.md)
* [Documentación de Apache Kafka](http://kafka.apache.org/documentation.html) en kafka.apache.org.
* [Usar MirrorMaker toocreate una réplica de Kafka en HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Uso de Apache Kafka con Storm en HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Uso de Apache Spark con Kafka en HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Conectar tooKafka a través de una red Virtual de Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
