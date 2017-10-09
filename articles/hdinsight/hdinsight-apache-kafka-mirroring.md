---
title: temas de Apache Kafka aaaMirror - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo la creación de reflejo de toouse Apache Kafka característica toomaintain una réplica de un Kafka en clúster de HDInsight clúster secundario tooa de temas de creación de reflejo."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a>Use los temas de Apache Kafka de tooreplicate de MirrorMaker con Kafka en HDInsight (versión preliminar)

Obtenga información acerca de cómo toouse Kafka Apache de la creación de reflejo de clúster secundario de característica tooreplicate temas tooa. Creación de reflejo se pueden se ejecutaban como un proceso continuo, o utilizar de forma intermitente como un método de migración de datos de un clúster tooanother.

En este ejemplo, la creación de reflejo es temas tooreplicate utilizado entre dos clústeres de HDInsight. Ambos clústeres están en una red Virtual de Azure en hello misma región.

> [!WARNING]
> Creación de reflejo no debe considerarse como un medio tooachieve la tolerancia a errores. Hola tooitems desplazamiento dentro de un tema son diferentes entre los clústeres de origen y destino de hello, por lo que los clientes no pueden usar indistintamente Hola dos.
>
> Si le preocupa la tolerancia a errores, debe establecer la replicación para temas de hello dentro de su clúster. Para más información, consulte [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) (Introducción a Kafka en HDInsight).

## <a name="how-kafka-mirroring-works"></a>Funcionamiento de la creación de reflejo de Kafka

Creación de reflejo funciona mediante registros de hello MirrorMaker herramienta (parte de Apache Kafka) tooconsume de temas en Hola clúster de origen y, a continuación, crear una copia local en el clúster de destino de Hola. MirrorMaker usa uno (o más) *consumidores* que leen de clúster de origen de hello y un *productor* que escribe el clúster de toohello local (destino).

Hola siguiente diagrama ilustra el proceso de creación de reflejo de hello:

![Diagrama del proceso de creación de reflejo de Hola](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

Apache Kafka en HDInsight no proporciona acceso toohello servicio Kafka sobre Hola internet pública. Los productores Kafka o los consumidores deben estar en hello misma red virtual de Azure como nodos de Hola Hola clúster Kafka. En este ejemplo, hello origen Kafka y clústeres de destino se encuentran en una red virtual de Azure. Hello diagrama siguiente muestra cómo fluye la comunicación entre clústeres de hello:

![Diagrama de clústeres Kafka de origen y destino en una red virtual de Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

clústeres de origen y destino de Hola pueden ser diferentes en el número de Hola de nodos y las particiones y desplazamientos dentro de los temas de hello también son diferentes. Creación de reflejo mantiene el valor de clave de Hola que se utiliza para crear particiones, por lo que se conserva el orden de los registros en una base de cada clave.

### <a name="mirroring-across-network-boundaries"></a>Creación de reflejo en los límites de red

Si necesita toomirror entre clústeres de Kafka en distintas redes, hay Hola siguientes consideraciones adicionales:

* **Las puertas de enlace**: redes Hola deben ser capaz de toocommunicate en hello nivel de TCP/IP.

* **La resolución de nombres**: Hola Kafka clústeres en cada red debe ser capaz de tooconnect tooeach otros mediante el uso de los nombres de host. Esto puede requerir un servidor de sistema de nombres de dominio (DNS) en cada red que esté configurado tooforward solicitudes toohello otras redes.

    Al crear una red Virtual de Azure, en lugar de usar Hola que DNS automática proporcionada con la red de hello, debe especificar un DNS hello y servidor dirección IP personalizada para servidor hello. Después de Hola que se ha creado la red Virtual, a continuación, debe crear una máquina Virtual de Azure que usa esa dirección IP, a continuación, instalar y configurar software DNS en él.

    > [!WARNING]
    > Crear y configurar el servidor DNS personalizado de hello antes de instalar HDInsight en hello red Virtual. No hay ninguna configuración adicional necesaria para el servidor DNS de hello HDInsight toouse configurado para hello red Virtual.

Para más información sobre cómo conectar dos redes virtuales de Azure, consulte [Configuración de una conexión de red virtual a red virtual](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

## <a name="create-kafka-clusters"></a>Creación de clústeres Kafka

Aunque puede crear una red virtual de Azure y Kafka clústeres manualmente, resulta más fácil toouse una plantilla de Azure Resource Manager. Usar hello siguiendo los pasos toodeploy una red virtual de Azure y tooyour de clústeres de dos Kafka suscripción de Azure.

1. Usar hello siguientes toosign de botón en tooAzure y plantilla abierto Hola Hola portal de Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello plantilla de Azure Resource Manager se encuentra en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > disponibilidad de tooguarantee de Kafka en HDInsight, el clúster debe contener al menos tres nodos de trabajador. Esta plantilla crea un clúster de Kafka que contiene tres nodos de trabajo.

2. Hola uso seguidas de hello las entradas de información toopopulate hello **implementación personalizada** hoja:
    
    ![Implementación personalizada de HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * **Grupo de recursos**: cree un nuevo grupo de recursos o seleccione uno existente. Este grupo contiene clúster de HDInsight Hola.

    * **Ubicación**: seleccione una tooyou geográficamente cerrar de ubicación.
     
    * **Nombre de clúster base**: este valor se utiliza como nombre de base de Hola para hello Kafka clústeres. Por ejemplo, si se especifica **hdi**, se crean clústeres denominados **source-hdi** y **dest-hdi**.

    * **Nombre de usuario de inicio de sesión del clúster**: clústeres de Kafka de nombre de usuario de administrador de hello para el origen de Hola y de destino.

    * **Contraseña de inicio de sesión del clúster**: clústeres de Kafka de contraseña de usuario de administrador de Hola para hello origen y destino.

    * **Nombre de usuario SSH**: Hola toocreate de usuario SSH como Hola origen y destino Kafka clústeres.

    * **Contraseña SSH**: clústeres de Kafka de contraseña de hello para el usuario SSH de hello para el origen de Hola y de destino.

3. Hola de lectura **términos y condiciones**y, a continuación, seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**.

4. Finalmente, compruebe **Pin toodashboard** y, a continuación, seleccione **compra**. Tarda aproximadamente 20 minutos toocreate clústeres Hola.

Una vez que se han creado los recursos de hello, son hoja tooa redirigida Hola grupo de recursos que contiene los clústeres de Hola y el panel de la web.

![Hoja de grupo de recursos de red virtual de Hola y clústeres](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> Tenga en cuenta que los nombres de Hola de clústeres de HDInsight de hello **origen BASENAME** y **BASENAME dest**, donde BASENAME es el nombre hello proporcionado toohello plantilla. Utilice estos nombres en pasos posteriores al conectarse a clústeres de toohello.

## <a name="create-topics"></a>Creación de temas

1. Conectar toohello **origen** mediante SSH de clúster:

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    Reemplace **sshuser** con nombre de usuario SSH Hola utilizado al crear el clúster de Hola. Reemplace **BASENAME** con el nombre de base de hello usado al crear el clúster de Hola.

    Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Siguiente de hello use comandos hosts de Zookeeper toofind hello para el clúster de origen de hello:

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. Se ha creado Hola de uso después de tooverify de comando que Hola tema:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    respuesta de Hello contiene `testtopic`.

4. Hola de uso siguiente tooview hello Zookeeper host información de este (hello **origen**) clúster:

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    Esto devuelve información toohello similar siguiente texto:

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    Guarde esta información. Se utiliza en la sección siguiente Hola.

## <a name="configure-mirroring"></a>Configuración del reflejo

1. Conectar toohello **destino** mediante una sesión SSH diferente del clúster:

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    Reemplace **sshuser** con nombre de usuario SSH Hola utilizado al crear el clúster de Hola. Reemplace **BASENAME** con el nombre de base de hello usado al crear el clúster de Hola.

    Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Siguiente Hola de uso del comando toocreate un `consumer.properties` archivo que describe cómo toocommunicate con hello **origen** clúster:

    ```bash
    nano consumer.properties
    ```

    Hola de uso después de texto como contenido de Hola de hello `consumer.properties` archivo:

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    Reemplace **SOURCE_ZKHOSTS** con hello Zookeeper hospeda información de hello **origen** clúster.

    Este archivo describe Hola consumidor información toouse al leer desde el origen de hello clúster Kafka. Para más información sobre la configuración de los consumidores, consulte [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) (Configuraciones de consumidor) en kafka.apache.org.

    archivo de hello toosave, use **Ctrl + X**, **Y**y, a continuación, **ENTRAR**.

3. Antes de configurar el productor de Hola que se comunica con el clúster de destino de hello, debe buscar broker Hola hosts para hello **destino** clúster. Utilice esta información de hello después tooretrieve de comandos:

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    Reemplace `$PASSWORD` con la contraseña de cuenta (Administrador) de inicio de sesión de hello para el clúster de Hola.

    Reemplace `$CLUSTERNAME` con nombre de hello del clúster de destino de Hola.

    Estos comandos devuelven siguiente toohello similar de información:

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. Hola de uso después de toocreate un `producer.properties` archivo que describe cómo toocommunicate con hello **destino** clúster:

    ```bash
    nano producer.properties
    ```

    Hola de uso después de texto como contenido de Hola de hello `producer.properties` archivo:

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    Reemplace **DEST_BROKERS** con información de broker de hello del paso anterior de Hola.

    Para más información sobre la configuración del productor, consulte [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) (Configuraciones de productor) en kafka.apache.org.

## <a name="start-mirrormaker"></a>Inicio de MirrorMaker

1. De hello SSH conexión toohello **destino** de clúster, use Hola siguiendo comando toostart hello MirrorMaker proceso:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    parámetros de Hello utilizados en este ejemplo son:

    * **--consumer.config**: especifica el archivo hello que contiene propiedades de consumidor. Estas propiedades son toocreate usado un consumidor que lee de hello *origen* clúster Kafka.

    * **--producer.config**: especifica el archivo hello que contiene las propiedades del productor. Estas propiedades son toocreate usado un productor que escribe toohello *destino* clúster Kafka.

    * **lista blanca de direcciones--**: una lista de temas que se replica MirrorMaker de hello origen clúster toohello el destino.

    * **--num.streams**: Hola número de toocreate de subprocesos de consumidor.

 En el inicio, MirrorMaker devuelve información toohello similar siguiente texto:

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. De hello SSH conexión toohello **origen** de clúster, use Hola después comando toostart un productor y enviar tema toohello de mensajes:

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    Reemplace `$PASSWORD` con la contraseña de inicio de sesión (admin) hello para el clúster de origen Hola.

    Reemplace `$CLUSTERNAME` con el nombre de Hola de clúster de origen Hola.

     Cuando llegue a una línea en blanco con un cursor, escriba algunos mensajes de texto. Estos se envían toohello tema en hello **origen** clúster. Cuando haya terminado, use **Ctrl + C** proceso productor de tooend Hola.

3. De hello SSH conexión toohello **destino** de clúster, use **Ctrl + C** tooend hello MirrorMaker proceso. A continuación, siguiente de hello use comandos tooverify ese hello `testtopic` tema se creó, y esos datos en el tema de hello eran toothis replicada reflejado:

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    Reemplace `$PASSWORD` con la contraseña de inicio de sesión (admin) hello para el clúster de destino de Hola.

    Reemplace `$CLUSTERNAME` con nombre de hello del clúster de destino de Hola.

    Hello lista de temas ahora incluye `testtopic`, que se crea al MirrorMaster refleja tema Hola de hello origen clúster toohello el destino. mensajes de Hola recuperados de tema de hello son igual al escribir en el clúster de origen Hola Hola.

## <a name="delete-hello-cluster"></a>Eliminar el clúster de Hola

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Puesto que los pasos de hello en este documento para crear ambos Hola de clústeres en el mismo grupo de recursos de Azure, puede eliminar el grupo de recursos de Hola Hola portal de Azure. Eliminando grupo de recursos de hello quita todos los recursos creados siguiendo este documento, el Hola red Virtual de Azure y la cuenta de almacenamiento usan los clústeres de Hola.

## <a name="next-steps"></a>Pasos siguientes

En este documento, aprendió cómo toouse MirrorMaker toocreate una réplica de un Kafka de clúster. Utilice Hola siguiendo vínculos toodiscover otro toowork maneras con Kafka:

* [Documentación de Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) en cwiki.apache.org.
* [Introducción a Apache Kafka en HDInsight](hdinsight-apache-kafka-get-started.md)
* [Uso de Apache Spark con Kafka en HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Uso de Apache Kafka con Storm en HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Conectar tooKafka a través de una red Virtual de Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
