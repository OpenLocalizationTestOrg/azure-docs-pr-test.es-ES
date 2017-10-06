---
title: disponibilidad de aaaHigh para Hadoop - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información sobre cómo los clústeres de HDInsight mejoran la confiabilidad y la disponibilidad gracias al uso de un nodo principal extra. Obtenga información acerca de cómo esto afecta a los servicios Hadoop como Ambari y subárbol, así como la tooindividually conectar tooeach nodo principal mediante SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: hadoop alta disponibilidad
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a>Disponibilidad y fiabilidad de clústeres de Hadoop en HDInsight

Clústeres de HDInsight proporcionan dos nodos principales tooincrease Hola confiabilidad y disponibilidad de servicios de Hadoop y trabajos que se ejecutan.

Hadoop logra una alta disponibilidad y confiabilidad al replicar datos y servicios en varios nodos de un clúster. Sin embargo, las distribuciones estándar de Hadoop suelen tener un único nodo principal. Cualquier interrupción del nodo principal de hello único puede provocar trabajo toostop de hello clúster. HDInsight proporciona dos headnodes tooimprove Hadoop disponibilidad y confiabilidad.

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="availability-and-reliability-of-nodes"></a>Disponibilidad y confiabilidad de los nodos

Los nodos de un clúster de HDInsight se implementan mediante Máquinas virtuales de Azure. Hello siguientes secciones describen los tipos de nodos individuales de hello usa con HDInsight. 

> [!NOTE]
> No todos los tipos de nodo se utilizan para un tipo de clúster. Por ejemplo, un tipo de clúster de Hadoop no tiene ningún nodo Nimbus. Para obtener más información sobre nodos utilizados por tipos de clúster de HDInsight, vea la sección de tipos de clúster de Hola de hello [Hadoop basado en Linux crear clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) documento.

### <a name="head-nodes"></a>Nodos principales

tooensure servicios de alta disponibilidad Hadoop, HDInsight proporciona dos nodos principales. Ambos nodos principales están activo y en ejecución en el clúster de HDInsight de hello simultáneamente. Algunos servicios, como HDFS o YARN, solo están “activos” en un nodo principal en un determinado momento. Otros servicios como HiveServer2 o tienda de metadatos de Hive están activos en ambos nodos principales en hello mismo tiempo.

Los nodos principales (y otros nodos en HDInsight) tienen un valor numérico como parte del nombre de host de hello del nodo de Hola. Por ejemplo, `hn0-CLUSTERNAME` o `hn4-CLUSTERNAME`.

> [!IMPORTANT]
> No asocie valor numérico de Hola a si un nodo es principal ni secundario. valor numérico de Hello es solo está presente tooprovide un nombre único para cada nodo.

### <a name="nimbus-nodes"></a>Nodos Nimbus

Los nodos Nimbus están disponibles con los clústeres de Storm. los nodos de Nimbus Hola proporcionar similar funcionalidad toohello Hadoop JobTracker, distribuir y supervisar el procesamiento a través de nodos de trabajador. HDInsight proporciona dos nodos Nimbus de clústeres de Storm.

### <a name="zookeeper-nodes"></a>Nodos Zookeeper

Los nodos [ZooKeeper](http://zookeeper.apache.org/) sirven para seleccionar el líder de los servicios principales en los nodos principales. También son utilizado tooinsure que servicios, los nodos de datos (trabajo) y las puertas de enlace saber qué nodo principal está activo en un servicio principal. De forma predeterminada, HDInsight proporciona tres nodos ZooKeeper.

### <a name="worker-nodes"></a>Nodos de trabajo

Nodos de trabajador realizan análisis de datos reales de hello cuando un trabajo está clúster toohello enviado. Si se produce un error en un nodo de trabajo, tarea hello que estaba llevando a cabo es el nodo de trabajo tooanother enviado. De forma predeterminada, HDInsight crea cuatro nodos de trabajo. Puede cambiar este número toosuit sus necesidades durante y después de la creación del clúster.

### <a name="edge-node"></a>Nodo perimetral

Un nodo del borde no participar activamente en el análisis de datos en clúster de Hola. sino que lo usan desarrolladores o científicos de datos al trabajar con Hadoop. Hello borde nodo vida en Hola misma red Virtual de Azure como Hola otros nodos de clúster de Hola y puede tener acceso directamente a todos los demás nodos. nodo de Hello borde puede utilizarse sin consumen recursos fuera de los servicios esenciales de Hadoop o los trabajos de análisis.

Actualmente, servidor de R en HDInsight es el único tipo de clúster de Hola que proporciona un nodo del borde de forma predeterminada. Para servidor de R de HDInsight, se usa el nodo del borde Hola código de prueba R localmente en el nodo de hello antes del envío toohello clúster para el procesamiento distribuido.

Para obtener información sobre el uso de un nodo del borde con tipos de clúster que no sea servidor de R, vea hello [usar nodos perimetrales en HDInsight](hdinsight-apps-use-edge-node.md) documento.

## <a name="accessing-hello-nodes"></a>Obtener acceso a los nodos de Hola

Clúster de toohello de acceso a través de hello internet se proporciona a través de una puerta de enlace pública. El acceso se nodos principales del toohello tooconnecting limitado y (si existe) Hola nodo del borde. Tooservices de acceso que se ejecutan en nodos principales de hello no se realiza al tener varios nodos principales. Hola pública de la puerta de enlace rutas solicitudes toohello nodo principal que hospeda Hola servicio solicitado. Por ejemplo, si Ambari se hospede actualmente en el nodo principal secundario de hello, puerta de enlace de hello enruta las solicitudes entrantes de nodo de toothat de Ambari.

Acceso a través de puerta de enlace pública hello es limitado tooport 443 (HTTPS), 22 y 23.

* Puerto __443__ es tooaccess usado Ambari y otros web API de REST hospedada en nodos principales de Hola o interfaz de usuario.

* Puerto __22__ es nodo principal de tooaccess usado Hola principal o perimetral mediante SSH.

* Puerto __23__ es tooaccess usado Hola secundario del nodo principal mediante SSH. Por ejemplo, `ssh username@mycluster-ssh.azurehdinsight.net` conecta toohello, principal, nodo principal del clúster Hola denominado **mycluster**.

Para obtener más información sobre el uso de SSH, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

### <a name="internal-fully-qualified-domain-names-fqdn"></a>Nombres completos de dominio (FQDN) internos

Nodos en un clúster de HDInsight tienen una dirección IP y los FQDN que solo puede tener acceso desde el clúster de hello interno. Al obtener acceso a servicios en un clúster de hello mediante Hola interna FQDN o dirección IP, debe usar Ambari tooverify Hola IP o FQDN toouse al tener acceso a servicios de Hola.

Por ejemplo, hello Oozie servicio solo puede ejecutarse en un nodo principal y el uso de hello `oozie` comando desde una sesión de SSH requiere el servicio de toohello de dirección URL de Hola. Esta dirección URL se puede recuperar desde Ambari mediante Hola siguiente comando:

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

Este comando devuelve un toohello similar valor siguiente comando, que contiene hello toouse de dirección URL interna con hello `oozie` comando:

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

Para obtener más información sobre cómo trabajar con hello Ambari API de REST, consulte [supervisar y administrar HDInsight con hello API de REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).

### <a name="accessing-other-node-types"></a>Acceso a otros tipos de nodos

Puede conectarse toonodes que están no directamente accesible over Hola internet utilizando Hola siguientes métodos:

* **SSH**: una vez conectado el nodo principal de tooa mediante SSH, a continuación, puede utilizar SSH desde Hola nodo principal tooconnect tooother nodos Hola clúster. Para obtener más información, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

* **Túnel SSH**: si necesita tooaccess un servicio web hospedado en uno de los nodos de Hola que no expone toohello internet, debe usar un túnel SSH. Para obtener más información, vea hello [utilizar un túnel SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

* **Red Virtual de Azure**: si HDInsight clúster forma parte de una red Virtual de Azure, cualquier recurso de Hola misma red Virtual puede acceder directamente a todos los nodos de clúster de Hola. Para obtener más información, vea hello [HDInsight extender mediante la red Virtual de Azure](hdinsight-extend-hadoop-virtual-network.md) documento.

## <a name="how-toocheck-on-a-service-status"></a>¿Cómo toocheck en un estado del servicio

estado de hello toocheck de servicios que se ejecutan en nodos principales de hello, usar hello Ambari Web UI u Hola API de REST de Ambari.

### <a name="ambari-web-ui"></a>Interfaz de usuario web de Ambari

Hola Ambari Web IU sea visible en https://CLUSTERNAME.azurehdinsight.net. Reemplace **CLUSTERNAME** con nombre hello del clúster. Si se le solicite, escriba las credenciales de usuario HTTP de hello para el clúster. nombre de usuario HTTP de Hello predeterminado es **administración** y Hola contraseña es Hola que especificó al crear el clúster de Hola.

Cuando llegan en la página de Ambari hello, aparecerán los servicios de hello instalado izquierda Hola de página Hola.

![Servicios instalados](./media/hdinsight-high-availability-linux/services.png)

Hay una serie de iconos que pueden aparecer el siguiente estado de tooindicate del servicio de tooa. Las alertas relacionadas con servicio tooa puede verse mediante hello **alertas** vínculo situado en la parte superior de Hola de página de Hola. Puede seleccionar cada servicio tooview más información sobre él.

Mientras la página del servicio Hola proporciona información sobre estado de Hola y la configuración de cada servicio, no proporciona información en el que se está ejecutando servicios de Hola de nodo principal. tooview esta información, use hello **Hosts** vínculo situado en la parte superior de Hola de página de Hola. Esta página muestra los hosts en clúster de hello, incluidos los nodos principales de Hola.

![lista de hosts](./media/hdinsight-high-availability-linux/hosts.png)

Seleccionar vínculo de Hola de uno de los nodos principales de hello muestra servicios de Hola y componentes que se ejecutan en ese nodo.

![Estado del componente](./media/hdinsight-high-availability-linux/nodeservices.png)

Para obtener más información sobre el uso de Ambari, consulte [Monitor y administrar HDInsight con Ambari Web UI hello](hdinsight-hadoop-manage-ambari.md).

### <a name="ambari-rest-api"></a>API de REST de Ambari

Hola Ambari REST API está disponible a través de hello internet. puerta de enlace de Hello HDInsight pública controla las solicitudes toohello principal el nodo de enrutamiento que hospeda actualmente Hola API de REST.

Puede usar Hola después de estado de hello toocheck de comandos de un servicio a través de la API de REST de Ambari hello:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* Reemplace **contraseña** con la contraseña de cuenta de usuario (admin) Hola HTTP.
* Reemplace **CLUSTERNAME** con nombre de hello del clúster de Hola.
* Reemplace **SERVICENAME** por nombre de hello del servicio de hello desea toocheck estado de Hola de.

Por ejemplo, toocheck estado Hola de hello **HDFS** servicio en un clúster denominado **mycluster**, con una contraseña de **contraseña**, usaría Hola siguiente comando:

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

respuesta de Hello es toohello similar después de JSON:

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

Hello URL nos indica que el servicio de Hola se está ejecutando actualmente en un nodo principal denominado **hn0 CLUSTERNAME**.

Hello estado nos indica que se está ejecutando actualmente el servicio de hello, o **iniciado**.

Si no sabe qué servicios están instalados en el clúster de hello, puede usar Hola después tooretrieve una lista de comandos:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

Para obtener más información sobre cómo trabajar con hello Ambari API de REST, consulte [supervisar y administrar HDInsight con hello API de REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).

#### <a name="service-components"></a>Componentes de servicio

Los servicios pueden contener componentes que desee toocheck estado de Hola de forma individual. Por ejemplo, HDFS contiene componentes de NameNode Hola. tooview información en un componente, Hola comando sería:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

Si no sabe qué componentes se proporcionan por un servicio, puede usar Hola después tooretrieve una lista de comandos:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a>¿Cómo tooaccess archivos de registro en nodos principales Hola

### <a name="ssh"></a>SSH

Al nodo principal de tooa conectado a través de SSH, archivos de registro pueden encontrarse en **/var/log**. Por ejemplo, **/var/log/hadoop-yarn/yarn** contiene registros de YARN.

Cada nodo principal puede tener entradas del registro único, por lo que debe comprobar Hola inicia sesión en ambos.

### <a name="sftp"></a>SFTP

También puede conectarse mediante Hola SSH File Transfer Protocol o protocolo de transferencia de archivo seguro (SFTP) del nodo principal toohello y descargar archivos de registro de hello directamente.

Toousing similar un cliente de SSH, cuando se conecta el clúster toohello debe proporcionar Hola SSH usuario cuenta hello y nombre SSH dirección Hola del clúster de. Por ejemplo: `sftp username@mycluster-ssh.azurehdinsight.net`. Proporcionar contraseña hello para la cuenta de hello cuando se le solicite, o proporcionar una clave pública mediante hello `-i` parámetro.

Una vez conectado, se le presentará un símbolo del sistema `sftp>` . Desde este símbolo del sistema, puede cambiar los directorios, cargar y descargar archivos. Por ejemplo, hello siga los comandos cambia directorios toohello **/var/log/hadoop/hdfs** directorio y, a continuación, descarga todos los archivos en el directorio de Hola.

    cd /var/log/hadoop/hdfs
    get *

Para obtener una lista de comandos disponibles, escriba `help` en hello `sftp>` símbolo del sistema.

> [!NOTE]
> También hay interfaces gráficas que le permiten el sistema de archivos de hello toovisualize cuando se conecta mediante SFTP. Por ejemplo, [MobaXTerm](http://mobaxterm.mobatek.net/) le permite el sistema de archivos de hello toobrowse mediante un explorador de tooWindows similar de interfaz.

### <a name="ambari"></a>Ambari

> [!NOTE]
> con Ambari de archivos de registro de tooaccess, debe utilizar un túnel SSH. interfaces de Hello web para los servicios individuales de hello no se exponen públicamente en hello Internet. Para obtener información sobre el uso de un túnel SSH, vea hello [uso de SSH túnel](hdinsight-linux-ambari-ssh-tunnel.md) documento.

Desde la interfaz de usuario de Ambari Web hello, seleccione servicio de hello desea tooview registros (por ejemplo, YARN). A continuación, utilice **vínculos rápidos** tooselect registra qué hello tooview de nodo principal para.

![Usar rápida vincula tooview registros](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a>¿Cómo tooconfigure Hola tamaño de nodo

tamaño de Hola de un nodo solo puede seleccionarse durante la creación del clúster. Se pueden encontrar una lista de Hola disponibles diferentes tamaños de máquina virtual de HDInsight en hello [HDInsight página de precios](https://azure.microsoft.com/pricing/details/hdinsight/).

Al crear un clúster, puede especificar el tamaño de Hola de nodos de Hola. Hello siguiente información proporciona instrucciones sobre cómo toospecify Hola tamaño con Hola [portal de Azure][preview-portal], [Azure PowerShell][azure-powershell], hello y [CLI de Azure][azure-cli]:

* **Portal de Azure**: al crear un clúster, puede establecer tamaño de Hola de nodos de hello usado Hola clúster:

    ![Imagen del asistente para creación de clústeres con selección del tamaño del nodo](./media/hdinsight-high-availability-linux/headnodesize.png)

* **CLI de Azure**: al usar hello `azure hdinsight cluster create` comando, puede establecer tamaño de Hola de head hello, trabajo y sus nodos ZooKeeper mediante hello `--headNodeSize`, `--workerNodeSize`, y `--zookeeperNodeSize` parámetros.

* **Azure PowerShell**: al usar hello `New-AzureRmHDInsightCluster` cmdlet, puede establecer tamaño de Hola de hello head, trabajo y nodos de ZooKeeper mediante hello `-HeadNodeVMSize`, `-WorkerNodeSize`, y `-ZookeeperNodeSize` parámetros.

## <a name="next-steps"></a>Pasos siguientes

Usar hello siguiendo vínculos toolearn más sobre lo que se mencionan en este documento.

* [Referencia de REST de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [Instalar y configurar Hola CLI de Azure](../cli-install-nodejs.md)
* [Instalación y configuración de Azure PowerShell](/powershell/azure/overview)
* [Administración de HDInsight mediante Ambari](hdinsight-hadoop-manage-ambari.md)
* [Aprovisionamiento de clústeres de HDInsight basado en Linux](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
