---
title: datos del sensor aaaAnalyze con Apache Storm y HBase | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect tooApache Storm con una red virtual. Usar Storm con los datos de sensor de HBase tooprocess de un centro de eventos y visualizar con D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a>Análisis de datos de sensores con Apache Storm, Centro de eventos y HBase en HDInsight (Hadoop)

Obtenga información acerca de cómo toouse Apache Storm en los datos de sensor tooprocess de HDInsight de concentrador de eventos de Azure. datos de Hello, a continuación, se almacenan en Apache HBase en HDInsight y visualizan mediante D3.js.

plantilla de Azure Resource Manager Hola usado en este documento se muestra cómo toocreate varios recursos de Azure en un grupo de recursos. plantilla de Hello crea una red Virtual de Azure, dos clústeres de HDInsight (Storm y HBase) y una aplicación Web de Azure. Una implementación de node.js de un panel web en tiempo real está implementado automáticamente toohello web app.

> [!NOTE]
> información de Hello en el documento y el ejemplo de este documento requieren HDInsight versión 3.6.
>
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Requisitos previos

* Una suscripción de Azure.
* [Node.js](http://nodejs.org/): panel de toopreview usado hello web localmente en el entorno de desarrollo.
* [Hello JDK 1.7 y Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html): usar topología de Storm hello toodevelop.
* [Maven](http://maven.apache.org/what-is-maven.html): proyecto de hello toobuild y compilación utilizado.
* [GIT](http://git-scm.com/): proyecto de hello toodownload usado desde GitHub.
* Un **SSH** cliente: usar clústeres de HDInsight basados en Linux toohello tooconnect. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).


> [!IMPORTANT]
> No necesita un clúster existente de HDInsight. pasos de Hello en este documento para crear Hola recursos siguientes:
> 
> * Una red virtual de Azure
> * Un clúster de Storm en HDInsight (dos nodos de trabajo basados en Linux)
> * Un clúster de HBase en HDInsight (dos nodos de trabajo basados en Linux)
> * Una aplicación Web de Azure que hospeda el panel de hello web

## <a name="architecture"></a>Arquitectura

![diagrama de arquitectura](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

Este ejemplo consta de Hola de los componentes siguientes:

* **Centros de eventos de Azure**: contiene datos que se recopilan de los sensores.
* **Storm en HDInsight**: ofrece procesamiento en tiempo real de datos desde el Centro de eventos.
* **HBase en HDInsight**: proporciona un almacén de datos NoSQL persistente para los datos después de haberse procesado en Storm.
* **Servicio de red Virtual de Azure**: permite proteger las comunicaciones entre hello Storm en HDInsight y HBase en clústeres de HDInsight.
  
  > [!NOTE]
  > Una red virtual se requiere cuando se usa la API de cliente de hello HBase de Java. No se expone a través de puerta de enlace pública de Hola para clústeres de HBase. Clústeres de HBase instalación y Storm en hello misma red virtual permite Hola clúster de Storm (o cualquier otro sistema en la red virtual de hello) toodirectly tener acceso a HBase mediante la API de cliente.

* **Sitio web del panel**: un panel de ejemplo que muestra datos en tiempo real.
  
  * sitio Web de Hola se implementa en Node.js.
  * [Socket.IO](http://socket.io/) se utiliza para la comunicación en tiempo real entre topología aluvión de Hola y Hola.
    
    > [!NOTE]
    > Usar Socket.io para comunicaciones es un detalle de implementación. Puede usar cualquier marco de comunicaciones, como SignalR o WebSockets sin procesar.

  * [D3.js](http://d3js.org/) toograph usado Hola datos que se envía el sitio Web de toohello.

> [!IMPORTANT]
> Dos clústeres son necesarios, ya que no existe ningún método admitido toocreate un HDInsight clúster de Storm y HBase.

Hello topología lee datos desde el concentrador de eventos mediante hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) clase y escribe los datos en HBase mediante hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) clase. Comunicación con el sitio Web de Hola se logra mediante [socket.io client.java](https://github.com/nkzawa/socket.io-client.java).

Hola después diagrama explica diseño Hola de topología de hello:

![diagrama de topología](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> Este diagrama es una vista simplificada de topología de Hola. Por cada partición del Centro de eventos se crea una instancia de cada componente. Estas instancias se distribuyen en nodos de hello en clúster de Hola y datos se enrutan entre ellos los siguientes:
> 
> * Datos del analizador de hello pitorro toohello tiene una carga equilibrada.
> * Datos de hello analizador toohello panel y HBase están agrupados por Id. de dispositivo, para que los mensajes de Hola mismo dispositivo siempre flujo toohello mismo componente.

### <a name="topology-components"></a>Componentes de la topología

* **Concentrador de eventos apetezca charlar**: pitorro Hola se proporciona como parte de la versión de Apache Storm 0.10.0 y versiones posteriores.
  
  > [!NOTE]
  > pitorro de concentrador de eventos de Hello utilizado en este ejemplo requiere una tormenta de la versión de clúster de HDInsight 3.5 o 3.6.

* **ParserBolt.java**: Hola datos que se emiten por pitorro Hola JSON sin formato y en ocasiones más de un evento se genera cada vez. Este rayo lee datos Hola emitidos por hello apetezca charlar y analiza el mensaje de bienvenida de JSON. tornillo de Hello, a continuación, emite los datos de hello como una tupla que contiene varios campos.
* **DashboardBolt.java**: este componente muestra cómo toouse Hola Socket.io biblioteca de cliente para los datos de toosend de Java en el panel en tiempo real toohello web.
* **no hbase.yaml**: Hola definición de topología que se usa cuando se ejecuta en modo local. No usa componentes de HBase.
* **con hbase.yaml**: Hola definición de topología que se usa al ejecutar la topología de hello en clúster de Hola. Usa componentes de HBase.
* **dev.Properties**: Hola información de configuración para pitorro de concentrador de eventos de hello, HBase rayo y componentes de panel.

## <a name="prepare-your-environment"></a>Preparación del entorno

Antes de utilizar este ejemplo, debe crear un concentrador de eventos de Azure, lee qué topología de Storm Hola de.

### <a name="configure-event-hub"></a>Configuración del centro de eventos

Centro de eventos es el origen de datos de Hola para este ejemplo. Usar hello siguiendo los pasos toocreate un concentrador de eventos.

1. De hello [portal de Azure](https://portal.azure.com), seleccione **+ nuevo** -> **Internet de las cosas** -> **centros de eventos**.
2. Hola **crear Namespace** sección, lleve a cabo Hola siguientes tareas:
   
   1. Escriba un **nombre** para el espacio de nombres de Hola.
   2. Seleccione un plan de tarifa. **Básico** es suficiente para este ejemplo.
   3. Seleccione hello Azure **suscripción** toouse.
   4. Seleccione un grupo de recursos existente o cree uno.
   5. Seleccione hello **ubicación** para hello concentrador de eventos.
   6. Seleccione **Pin toodashboard**y, a continuación, haga clic en **crear**.

3. Cuando se completa el proceso de creación de hello, se muestra información de los centros de eventos para el espacio de nombres de Hola. Desde ahí, seleccione **+ Agregar Centro de eventos**. Hola **crear centro de eventos** sección, escriba un nombre de **sensordata**y, a continuación, seleccione **crear**. Deje Hola otros campos en los valores predeterminados de Hola.
4. Hola los centros de eventos permite ver el espacio de nombres, seleccione **centros de eventos**. Seleccione hello **sensordata** entrada.
5. En hello sensordata concentrador de eventos, seleccione **directivas de acceso compartido**. Hola de uso **+ agregar** Hola de vínculo tooadd las siguientes directivas:

    | Nombre de la directiva | Notificaciones |
    | ----- | ----- |
    | devices | Enviar |
    | storm | Escuchar |

1. Seleccione las dos directivas y tome nota de hello **PRIMARY KEY** valor. Se necesita el valor de Hola para ambas directivas en pasos futuros.

## <a name="download-and-configure-hello-project"></a>Descargar y configurar el proyecto de Hola

Usar hello siguiendo el proyecto de hello toodownload de GitHub.

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

Una vez completado el comando de hello, deberá Hola siguiendo la estructura de directorios:

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> Este documento no entra en detalles de toofull de código de hello incluido en este ejemplo. Sin embargo, el código de hello totalmente se hace referencia.

tooconfigure Hola proyecto tooread de concentrador de eventos, abra hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` de archivos y agregar su toohello de información de concentrador de eventos siguientes líneas:

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a>Compilación y pruebas locales

> [!IMPORTANT]
> Con la topología de hello localmente, requiere un entorno de desarrollo de Storm en funcionamiento. Para más información, consulte [Setting up a development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) (Configuración de un entorno de desarrollo) en Apache.org.

> [!WARNING]
> Si está utilizando un entorno de desarrollo de Windows, puede recibir un `java.io.IOException` cuando se ejecuta localmente topología Hola. Si es así, mueva topología de hello toorunning en HDInsight.

Antes de probar, debe iniciar Hola panel tooview Hola salida de topología de Hola y generar datos toostore en el concentrador de eventos.

> [!IMPORTANT]
> componente de HBase Hola de esta topología no está activa cuando se prueba localmente. Hola API Java para el clúster de HBase Hola no son accesibles desde el exterior Hola red Virtual de Azure que contiene los clústeres de Hola.

### <a name="start-hello-web-application"></a>Iniciar la aplicación web de hello

1. Abra un símbolo del sistema y cambie los directorios demasiado`hdinsight-eventhub-example/dashboard`. Usar hello después dependencias Hola comando tooinstall que sea necesarios mediante la aplicación web de hello:
   
    ```bash
    npm install
    ```

2. Usar hello tras la aplicación web de comando toostart hello:
   
    ```bash
    node server.js
    ```
   
    Vea un toohello similar de mensaje siguiente texto:
   
        Server listening at port 3000

3. Abra un explorador web y escriba `http://localhost:3000/` como dirección de Hola. Se muestra un toohello similar de página después de la imagen:
   
    ![panel web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    Deje abierto este símbolo del sistema. Después de realizar pruebas, usar servidor web de Ctrl-C toostop Hola.

### <a name="generate-data"></a>Generación de datos

> [!NOTE]
> Hello pasos de esta sección usan Node.js para que pueden usarse en cualquier plataforma. Para obtener ejemplos de idioma, vea hello `SendEvents` directory.

1. Abra un nuevo símbolo del sistema, el shell o terminal y cambie los directorios demasiado`hdinsight-eventhub-example/SendEvents/nodejs`. dependencias de hello tooinstall aplicación Hola, necesarios usar hello siguiente comando:

    ```bash
    npm install
    ```

2. Abra hello `app.js` un archivo en un editor de texto y agregue Hola información de concentrador de eventos ha obtenido antes:
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > En este ejemplo se da por supuesto que ha usado `sensordata` como nombre de Hola de su centro de eventos. Y que `devices` como nombre de Hola de directiva de Hola que tiene un `Send` de notificación.

3. Usar hello después comando tooinsert las nuevas entradas de concentrador de eventos:
   
    ```bash
    node app.js
    ```
   
    Ve varias líneas de salida que contienen datos de hello envían tooEvent concentrador:
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a>Compile y comience la topología de Hola

1. Abra un símbolo del sistema nuevo y cambie los directorios demasiado`hdinsight-eventhub-example/TemperatureMonitor`. toobuild y paquete Hola topología, use Hola siguiente comando: 

    ```bash
    mvn clean package
    ```

2. toostart Hola topología en modo local, usar hello siguiente comando:

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * `--local`topología de Hola se inicia en modo local.
    * `--filter`hello usa `dev.properties` toopopulate parámetros de archivo de definición de la topología de Hola.
    * `resources/no-hbase.yaml`hello usa `no-hbase.yaml` definición de topología.
 
   Una vez iniciado, topología Hola lee las entradas de concentrador de eventos y los envía panel toohello ejecutando en el equipo local. Debe ver líneas aparezcan en el panel de hello web, similar toohello después de imagen:
   
    ![panel con datos](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. Mientras se ejecuta el panel de hello, usar hello `node app.js` toosend nuevos datos tooEvent centros de los pasos del comando de hello anterior. Dado que los valores de temperatura de Hola se generan de forma aleatoria, gráfico de hello debe actualizar tooshow grandes cambios de temperatura.
   
   > [!NOTE]
   > Debe estar en hello **hdinsight-eventhub-ejemplo/SendEvents/Nodejs** directory al utilizar hello `node app.js` comando.

3. Después de comprobar las actualizaciones de ese panel hello, stop Hola topología mediante Ctrl + C. También puede utilizar el servidor web local de Ctrl + C toostop Hola.

## <a name="create-a-storm-and-hbase-cluster"></a>Creación de un clúster de Storm y HBase

Hola los pasos de esta sección utilizan un [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate un clúster de red Virtual de Azure y una tormenta y HBase en red virtual de Hola. plantilla de Hello también crea una aplicación Web de Azure e implementa una copia del panel de hello en él.

> [!NOTE]
> Se utiliza una red virtual para que la topología de hello ejecutando en el clúster de Storm Hola puede comunicarse directamente con el clúster de HBase de hello mediante Hola API de Java de HBase.

plantilla de administrador de recursos de Hello usado en este documento se encuentra en un contenedor de blob público en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.

1. Haga clic en hello siguientes toosign de botón en tooAzure y plantilla de administrador de recursos abiertos Hola Hola portal de Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. De hello **implementación personalizada** sección, escriba Hola siguientes valores:
   
    ![Parámetros de HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * **Nombre de clúster base**: este valor se utiliza como nombre de base de Hola para clústeres de Storm y HBase Hola. Por ejemplo, si escribe **abc**, se creará un clúster de Storm denominado **storm-abc** y un clúster de HBase denominado **hbase-abc**.
   * **Nombre de usuario de inicio de sesión del clúster**: nombre de usuario de administrador de Hola para clústeres de Storm y HBase Hola.
   * **Contraseña de inicio de sesión del clúster**: contraseña de usuario de administrador de Hola para clústeres de Storm y HBase de Hola.
   * **Nombre de usuario SSH**: Hola toocreate de usuario SSH para clústeres de Storm y HBase Hola.
   * **Contraseña SSH**: contraseña de hello para el usuario SSH de Hola para clústeres de Storm y HBase Hola.
   * **Ubicación**: región Hola que se crean los clústeres de hello en.
     
     Haga clic en **Aceptar** parámetros de hello toosave.

3. Hola de uso **Fundamentos** sección toocreate un grupo de recursos o seleccione uno existente.
4. Hola **ubicación del grupo de recursos** menú desplegable, seleccione Hola indicarlo tal y como se ha seleccionado para hello **ubicación** parámetro Hola **configuración** sección.
5. Lea Hola términos y condiciones y, a continuación, seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**.
6. Finalmente, compruebe **Pin toodashboard** y, a continuación, seleccione **compra**. Tarda aproximadamente 20 minutos toocreate clústeres Hola.

Una vez que se han creado Hola recursos, se muestra información sobre el grupo de recursos de Hola.

![Grupo de recursos de red virtual de Hola y clústeres](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> Tenga en cuenta que los nombres de Hola de clústeres de HDInsight de hello **BASENAME storm** y **hbase BASENAME**, donde BASENAME es el nombre hello proporcionado toohello plantilla. Utilice estos nombres en un paso posterior al conectarse a clústeres de toohello. También tenga en cuenta que Hola nombre del sitio de escritorio de hello es **basename panel**. Este valor se usa más adelante en este documento.

## <a name="configure-hello-dashboard-bolt"></a>Configurar rayo de panel de Hola

panel de toosend datos toohello implementado como una aplicación web, debe modificar Hola línea siguiente en hello `dev.properties`archivo:

```yaml
dashboard.uri: http://localhost:3000
```

Cambio `http://localhost:3000` demasiado`http://BASENAME-dashboard.azurewebsites.net` y guarde el archivo hello. Reemplace **BASENAME** con el nombre de base de hello proporcionado en el paso anterior de Hola. También puede utilizar el grupo de recursos de hello creado previamente tooselect Hola panel y ver Hola una URL.

## <a name="create-hello-hbase-table"></a>Crear tabla de hello HBase

toostore datos en HBase, primero que debemos crear una tabla. Crear previamente los recursos que necesita de Storm toowrite a, tal y como se pueden dar lugar a tratar de recursos de toocreate desde dentro de una topología de Storm en varias instancias intentar toocreate Hola mismo recurso. Crear recursos de hello fuera la topología de Hola y usar aluvión de lectura/escritura y análisis.

1. Use el clúster de HBase SSH tooconnect toohello mediante SSH hello y la contraseña que proporcionó toohello plantilla durante la creación del clúster. Por ejemplo, si se conecta con hello `ssh` comando, usaría Hola según la sintaxis:
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    Reemplace `sshuser` con el nombre de usuario SSH de Hola que proporcionó al crear el clúster de Hola. Reemplace `clustername` con el nombre del clúster de HBase Hola.

2. De sesión SSH de hello, inicie el shell de HBase Hola.
   
    ```bash
    hbase shell
    ```
   
    Una vez que ha cargado el shell de hello, verá un `hbase(main):001:0>` símbolo del sistema.

3. En el Hola shell de HBase, escriba Hola después comando toocreate una tabla toostore Hola sensor de datos:
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. Comprobar que esa tabla Hola se ha creado mediante el uso de hello siguiente comando:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Esto devuelve información similar toohello siguiente ejemplo, que indica que hay 0 filas en la tabla de Hola.
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. Escriba `exit` tooexit Hola shell de HBase:

## <a name="configure-hello-hbase-bolt"></a>Configurar rayo de hello HBase

toowrite tooHBase de clúster de Storm hello, debe proporcionar rayo de HBase Hola con detalles de configuración de Hola de su clúster de HBase.

1. Use uno de hello después ejemplos tooretrieve hello Zookeeper quórum en el clúster de HBase:

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > Reemplace `your_HDInsight_cluster_name` con el nombre de Hola de su clúster de HDInsight. Para obtener más información acerca de cómo instalar hello `jq` utilidad, vea [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).
    >
    > Cuando se le solicite, escriba la contraseña de hello para el inicio de sesión de hello HDInsight admin.

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > Reemplace ' your_HDInsight_cluster_name con el nombre de Hola de su clúster de HDInsight. Cuando se le solicite, escriba la contraseña de hello para el inicio de sesión de hello HDInsight admin.
    >
    > Este ejemplo requiere Azure PowerShell. Para información acerca de cómo usar Azure PowerShell, consulte el artículo de [introducción a Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6).

    información de Hello devuelta por estos ejemplos es similar toohello siguiente texto:

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    Esta información se usa por Storm toocommunicate con clúster de HBase Hola.

2. Modificar hello `dev.properties` de archivos y agregar información de quórum de hello Zookeeper toohello después de línea:

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a>Compilar, empaquetar e implementar Hola solución tooHDInsight

En el entorno de desarrollo, use Hola después de clúster de storm toohello de pasos toodeploy Hola Storm topología.

1. De hello `TemperatureMonitor` directorio, use siguiente de hello tooperform una nueva compilación de comandos y cree un paquete JAR desde el proyecto:
   
        mvn clean package
   
    Este comando crea un archivo denominado `TemperatureMonitor-1.0-SNAPSHOT.jar in hello ` en el directorio de destino del proyecto.

2. Hola de uso scp tooupload `TemperatureMonitor-1.0-SNAPSHOT.jar` y `dev.properties` clúster de Storm tooyour de archivos. Hola siguiente ejemplo, reemplace `sshuser` con el usuario SSH de Hola que proporcionó al crear el clúster de hello, y `clustername` con el nombre de Hola de su clúster de Storm. Cuando se le solicite, escriba la contraseña de hello para el usuario SSH Hola.
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > Archivos de hello tooupload puede tardar varios minutos.

    Para obtener más información sobre el uso de hello `scp` y `ssh` comandos con HDInsight, vea [utilizar SSH con HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)

3. Una vez que se ha cargado el archivo hello, conecte el clúster de Storm toohello mediante SSH.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Reemplace `sshuser` con el nombre de usuario SSH de Hola. Reemplace `clustername` con el nombre de clúster de Storm Hola.

4. toostart Hola topología, usar hello siguiente comando desde la sesión de SSH de hello:
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * `--remote`Hola topología toohello servicio Nimbus, que distribuye toohello nodos de supervisor en clúster de Hola se envía.
    * `--filter`hello usa `dev.properties` toopopulate parámetros de archivo de definición de la topología de Hola.
    * `-R /with-hbase.yaml`hello usa `with-hbase.yaml` topología incluida en el paquete de saludo.

5. Después de que ha iniciado la topología de hello, abrir un sitio Web de toohello de explorador publica en Azure, a continuación, use hello `node app.js` comando toosend datos tooEvent concentrador. Debería ver la información de hello web panel actualización toodisplay Hola.
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a>Visualización de datos de HBase

Usar hello siguiendo los pasos tooconnect tooHBase y compruebe que se ha escrito datos hello toohello tabla:

1. Use el clúster de HBase de toohello tooconnect SSH.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Reemplace `sshuser` con el nombre de usuario SSH de Hola. Reemplace `clustername` con el nombre del clúster de HBase Hola.

2. De sesión SSH de hello, inicie el shell de HBase Hola.
   
    ```bash
    hbase shell
    ```
   
    Una vez que ha cargado el shell de hello, verá un `hbase(main):001:0>` símbolo del sistema.

3. Ver las filas de tabla de hello:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Este comando devuelve información similar toohello después de texto, que indica que no hay datos en la tabla de Hola.
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > Esta operación de búsqueda devuelve un máximo de 10 filas de tabla de Hola.

## <a name="delete-your-clusters"></a>Eliminación de los clústeres

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

clústeres de hello toodelete, el almacenamiento y la aplicación web al mismo tiempo, eliminar grupo de recursos de Hola que los contiene.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más ejemplos de topologías de Storm con HDInsight, vea [Topologías y componentes de ejemplo de Storm para Apache Storm en HDInsight](hdinsight-storm-example-topology.md).

Para obtener más información acerca de Apache Storm, vea hello [Apache Storm](https://storm.incubator.apache.org/) sitio.

Para obtener más información acerca de HBase en HDInsight, vea hello [HBase visión general de HDInsight](hdinsight-hbase-overview.md).

Para obtener más información sobre Socket.io, vea hello [socket.io](http://socket.io/) sitio.

Para obtener más información sobre D3.js, consulte [D3.js: documentos controlados por datos](http://d3js.org/).

Para obtener información sobre la creación de topologías en Java, consulte [Desarrollo de topologías de Java para Apache Storm en HDInsight](hdinsight-storm-develop-java-topology.md).

Para obtener información sobre la creación de topologías en .NET, consulte [Desarrollo de topologías de C# para Apache Storm en HDInsight mediante Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

[azure-portal]: https://portal.azure.com
