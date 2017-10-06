---
title: aaaUse Apache Spark streaming con concentradores de eventos de HDInsight de Azure | Documentos de Microsoft
description: "Compilar un ejemplo de transmisión por secuencias de Apache Spark en cómo toosend datos transmitir tooAzure centro de eventos y, a continuación, recibir los eventos de clúster de HDInsight Spark mediante una aplicación scala."
keywords: apache spark streaming de, streaming de spark, ejemplo de spark, ejemplo de streaming de apache spark, ejemplo de azure event hub, ejemplo de spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a>Streaming de Apache Spark: procesamiento de datos desde Azure Event Hubs con clústeres de Spark en HDInsight

En este artículo, se crea una transmisión por secuencias de ejemplo que implica Hola siguiendo los pasos de Apache Spark:

1. Un mensaje de tooingest la aplicación independiente que se usa en un centro de eventos de Azure.

2. Con dos enfoques diferentes, puede recuperar mensajes de saludo de concentrador de eventos en tiempo real con una aplicación se ejecuta en el clúster de Spark en HDInsight de Azure.

3. Compilar canalizaciones de analíticas de transmisión por secuencias sistemas de almacenamiento de toopersist datos toodifferent u obtener información de datos en marcha Hola.

## <a name="prerequisites"></a>Requisitos previos

* Una suscripción de Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="spark-streaming-concepts"></a>Conceptos de streaming de Spark

Para obtener una explicación detallada del streaming de Spark consulte la [información general sobre el streaming de Apache Spark](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview). HDInsight aporta hello tooa de características de transmisión por secuencias mismo Spark de Cluster Server en Azure.  

## <a name="what-does-this-solution-do"></a>¿Cómo funciona la solución?

En este artículo, toocreate un ejemplo de transmisión por secuencias de Spark, realizar Hola pasos:

1. Cree un Centro de eventos de Azure, que será el que reciba una transmisión de eventos.

2. Ejecutar una aplicación local independiente que genera eventos y lo inserta toohello concentrador de eventos de Azure. se publica la aplicación de ejemplo de Hola que lo haga en [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).

3. Ejecute una aplicación de streaming de forma remota en un clúster de Spark que lea los eventos de streaming desde el centro de eventos de Azure y lleve a cabo varios análisis y procesamientos de datos.

## <a name="create-an-azure-event-hub"></a>Crear un centro de eventos de Azure

1. Inicie sesión en toohello [Portal de Azure](https://ms.portal.azure.com)y haga clic en **New** en hello parte superior izquierda de la pantalla de bienvenida.

2. Haga clic en **Internet de las cosas** y en **Event Hubs**.

    ![Creación de un centro de eventos para un ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")

3. Hola **crear espacio de nombres** hoja, escriba un nombre de espacio de nombres. Elija Hola tarifa (básico o estándar). Además, elija una suscripción de Azure, el grupo de recursos y la ubicación en el recurso que hello toocreate. Haga clic en **crear** el espacio de nombres de toocreate Hola.

      ![Aportación de un nombre de centro de evento para el ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")

    > [!NOTE]
    > Debe seleccionar Hola mismo **ubicación** como el clúster de Apache Spark en HDInsight tooreduce latencia y los costos.
    >
    >

4. En la lista de espacio de nombres de los centros de eventos de hello, haga clic en el espacio de nombres de hello recién creado.      


5. En la hoja de espacio de nombres de hello, haga clic en **centros de eventos**y, a continuación, haga clic en **+ concentrador de eventos** toocreate un nuevo centro de eventos.
   
    ![Creación de un centro de eventos para un ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")

6. Escriba un nombre para el concentrador de eventos, conjunto Hola partición recuento too10 y too1 de retención de mensajes. No nos estamos archivar los mensajes de Hola en esta solución para que pueda dejar resto hello como valor predeterminado y, a continuación, haga clic en **crear**.
   
    ![Aportación de detalles del centro de evento para el ejemplo de streaming de Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")

7. Hola recién creado concentrador de eventos se muestra en la hoja de concentrador de eventos de Hola.
    
     ![Ver centro de eventos de ejemplo de Hola Spark streaming](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "concentrador de eventos de vista para hello inspirará ejemplo de transmisión por secuencias")

8. En la hoja de espacio de nombres de hello (no Hola específico concentrador de eventos hoja), haga clic en **directivas de acceso compartido**y, a continuación, haga clic en **RootManageSharedAccessKey**.
    
     ![Establecer directivas de concentrador de eventos de ejemplo de Hola Spark streaming](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "directivas de concentrador de eventos establecido para hello inspirará ejemplo de transmisión por secuencias")

9. Haga clic en Hola de hello copia botón toocopy **RootManageSharedAccessKey** principal Portapapeles de toohello de cadena de conexión y la clave. Guardar estas toouse más adelante en el tutorial Hola.
    
     ![Ver claves de directiva de centro de eventos de ejemplo de Hola Spark streaming](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "claves de directiva de centro de eventos de vista para hello inspirará ejemplo de transmisión por secuencias")

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a>Enviar mensajes tooAzure centro de eventos mediante una aplicación de ejemplo Scala

En esta sección utiliza local Scala aplicación independiente que se genera una secuencia de eventos y lo envía tooAzure concentrador de eventos que creó anteriormente. Esta aplicación está disponible en GitHub en [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer). Hola aquí da por sentado que ya ha bifurcado este repositorio de GitHub.

1. Asegúrese de que tiene los siguientes Hola instalados en el equipo de Hola donde se ejecuta esta aplicación.

    * Kit de desarrollo de Oracle Java. Puede instalarlo desde [aquí](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
    * Apache Maven. Puede descargarla [aquí](https://maven.apache.org/download.cgi). Existen instrucciones tooinstall Maven [aquí](https://maven.apache.org/install.html).

2. Abra un símbolo del sistema, navegue ubicación toohello clonar el repositorio de GitHub de Hola para aplicación de Scala de ejemplo de Hola y ejecute hello tras la aplicación de comando toobuild Hola.

        mvn package

3. Hola jar de salida para la aplicación hello, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, se crea en **/target** directory. Utilice este JAR más adelante en esta solución completa de artículo tootest Hola.

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a>Crear mensajes de tooreceive la aplicación de centro de eventos en un clúster de Spark 

Tenemos dos tooconnect enfoques Spark transmisión por secuencias y centros de eventos de Azure, conexión basada en el receptor y conexión directa basada en DStream. Direct-DStream-based se introdujo en enero de 2017, en la versión de Hola 2.0.3. Se suponía que conexión basada en el receptor de tooreplace Hola original sea más eficiente y eficaz de los recursos. Encontrará más información en [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs). Direct DStream solo admite Spark 2.0+.

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a>Compilar aplicaciones con el conector de hello dependencia toospark eventhubs

También publicaremos Hola versión de Spark EventHubs en GitHub de almacenamiento provisional. versión de almacenamiento provisional de Hola de toouse de Spark EventHubs, Hola primer paso es tooindicate GitHub como Hola repositorio de origen mediante la adición de hello después toopom.xml de entrada:

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

A continuación, puede agregar Hola después de la versión preliminar de dependencia tooyour proyecto tootake Hola.

Dependencia de Maven

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

Dependencia de SBT

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a>Conexión de Direct DStream

En [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar) se puede descargar un archivo JAR pregenerado que contiene ejemplos en los que se usa Direct DStream.

archivo jar de Hello contiene tres ejemplos cuyo código fuente está disponible en [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).

Si tomamos [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) como ejemplo:

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

Hola por encima de ejemplo, `eventhubParameters` instancia única de EventHubs de hello parámetros tooa específico y tienen toopass se toohello `createDirectStreams` API que crea un espacio de nombres de los centros de eventos de DStream directo objeto asignación tooa. A través de objeto de hello DStream directa, puede llamar a cualquier API DStream proporcionada por marco API de transmisión por secuencias de Spark. En este ejemplo, calculamos frecuencia Hola de cada palabra en intervalos de hello último lote micro 3.

### <a name="receiver-based-connection"></a>Conexión basada en un receptor

Está disponible en una aplicación de ejemplo escrita en Scala, que recibe eventos y destinos de enrutamiento hello toodifferent, de transmisión por secuencias de Spark [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples). Siga los pasos de Hola por debajo de la aplicación de hello tooupdate para la configuración del centro de eventos y cree Hola jar de salida.

1. Inicie la IDEA de IntelliJ y de hello iniciar pantalla Seleccione **desproteger del Control de versiones** y, a continuación, haga clic en **Git**.
   
    ![Ejemplo de streaming de Apache Spark: obtener orígenes de Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")

2. Hola **clon repositorio** cuadro de diálogo, proporcionar tooclone del repositorio de Git Hola URL toohello desde, especifique Hola directory tooclone a y, a continuación, haga clic en **clon**.
   
    ![Ejemplo de streaming de Apache Spark: clonar de Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")
3. Siga las indicaciones de hello hasta que el proyecto de hello completamente se clona. Presione **Alt + 1** tooopen hello **vista proyecto**. Debe parecerse al siguiente Hola.
   
    ![Ejemplo de streaming de Apache Spark: vista de proyecto](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")
4. Asegúrese de que se compila código de la aplicación hello con Java8. tooensure, haga clic en **archivo**, haga clic en **estructura del proyecto**y en hello **proyecto** ficha, asegúrese de que el nivel de lenguaje de proyecto se establece demasiado**8 - las expresiones lambda, tipo las anotaciones, etc.**.
   
    ![Ejemplo de streaming de Apache Spark: establecer compilador](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")
5. Abra hello **pom.xml** y asegúrese de que la versión de Hola Spark es correcta. En `<properties>` nodo, busque el siguiente fragmento de código de hello y comprobar la versión de Hola Spark.

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. aplicación Hello requiere un archivo jar de dependencia llama **jar del controlador JDBC**. Se trata de mensajes de saludo de toowrite necesario recibidos del concentrador de eventos en una base de datos de SQL Azure. Puede descargar este archivo jar (versión 4.1, o las versiones posteriores) desde [aquí](https://msdn.microsoft.com/sqlserver/aa937724.aspx). Agregar referencia toothis jar en la biblioteca de proyectos de Hola. Lleve a cabo Hola pasos:
     
     1. En la ventana de IDEA IntelliJ donde hay aplicación hello abierta, haga clic en **archivo**, haga clic en **estructura del proyecto**y, a continuación, haga clic en **bibliotecas**. 
     2. Haga clic en hello agregar icono (![agregar icono](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), haga clic en **Java**y, a continuación, navegue ubicación toohello donde descargó jar de controlador JDBC de Hola. Siga Hola indicaciones tooadd Hola jar archivo toohello biblioteca de proyectos.

         ![agregar dependencias que faltan](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Agregar archivos jar de dependencias que faltan")
     3. Haga clic en **Apply**.

7. Crear archivo jar de salida de hello. Realizar pasos de Hola.

   1. Hola **estructura del proyecto** cuadro de diálogo, haga clic en **artefactos** y, a continuación, haga clic en hello además de símbolos. En el cuadro de diálogo emergente de hello, haga clic en **JAR**y, a continuación, haga clic en **de módulos con dependencias**.      
       
       ![Ejemplo de streaming de Apache Spark: crear archivo JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")
   2. Hola **crear JAR de módulos** diálogo cuadro, haga clic en el botón de puntos suspensivos hello (![puntos suspensivos](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) contra Hola **clase principal**.
   3. Hola **seleccionar clase de Main** diálogo cuadro, seleccione cualquiera de las clases disponibles de hello y, a continuación, haga clic en **Aceptar**.
      
       ![Ejemplo de streaming de Apache Spark: seleccionar clase para el archivo jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")
   4. Hola **crear JAR de módulos** diálogo cuadro, asegúrese de que esa opción Hola demasiado**extraer toohello destino JAR** está seleccionada y, a continuación, haga clic en **Aceptar**. Así se crea un archivo JAR único con todas las dependencias.
      
       ![Ejemplo de streaming de Apache Spark: crear archivo jar desde módulos](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")
   5. Hola **salida diseño** ficha enumera todos los archivos JAR Hola que se incluyen como parte del proyecto de Maven Hola. Puede seleccionar y Hola delete aquellos en los que Hola Scala aplicación no tiene ninguna dependencia directa. Para la aplicación hello vamos a crear a continuación, puede quitar todos menos Hola último (**spark-transmisión por secuencias de datos-persistencia-ejemplos compilan salida**). Seleccione toodelete de archivos JAR de hello y, a continuación, haga clic en hello **eliminar** icono (![icono Eliminar](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).
      
       ![Ejemplo de streaming de Apache Spark: eliminar archivos jar extraídos](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")
      
       Asegúrese de que **compilar en hacer** casilla está activada, lo que garantiza que jar Hola se crea cada vez proyecto Hola se compila o se actualiza. Haga clic en **Apply**.
   6. Hola **salida diseño** ficha, en parte inferior de Hola de Hola **elementos disponibles** cuadro, tiene que agregar biblioteca de proyectos de toohello anterior archivo jar JDBC de SQL de Hola. Debe agregar esta toohello **salida diseño** ficha. Haga clic en archivo jar de hello y, a continuación, haga clic en **extraer en la raíz de salida**.
      
       ![Ejemplo de streaming de Apache Spark: extraer archivo jar de dependencia](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")  
      
       Hola **salida diseño** ficha debe tener el siguiente aspecto.
      
       ![Ejemplo de streaming de Apache Spark: pestaña de salida final](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")        
      
       Hola **estructura del proyecto** cuadro de diálogo, haga clic en **aplicar** y, a continuación, haga clic en **Aceptar**.    
   7. En la barra de menús de hello, haga clic en **generar**y, a continuación, haga clic en **proyecto realizar**. También puede hacer clic en **Generar artefactos** jar de hello toocreate. jar de salida Hello se crea una en **\classes\artifacts**.
      
       ![Ejemplo de streaming de Apache Spark: salida de archivo JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a>Ejecutar aplicación hello de forma remota en un clúster de Spark mediante Livio

En este artículo se utiliza Livio toorun Hola Apache Spark streaming aplicación remotamente en un clúster de Spark. Para obtener información detallada sobre cómo agrupar toouse Livio con HDInsight Spark, consulte [enviar trabajos remotamente clúster tooan Apache Spark en HDInsight de Azure](hdinsight-apache-spark-livy-rest-interface.md). Antes de que puede empezar a ejecutar la aplicación de transmisión por secuencias de Spark hello, hay un par de cosas que debe hacer:

1. Iniciar aplicación toogenerate eventos de hello local independiente y envían tooEvent concentrador. El comando siguiente de Hola de uso toodo así:

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. Hola copia jar de transmisión por secuencias (**spark archivo-transmisión por secuencias de datos-persistencia-examples.jar**) toohello asociada Hola clúster de almacenamiento de blobs de Azure. Esto hace que Hola jar accesible tooLivy. Puede usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), por lo que utilidad, toodo un comando de línea. Hay mucho de otros clientes puede usar datos de tooupload. Puede encontrar más información al respecto en [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).
3. Instalar CURL en donde se ejecuta estas aplicaciones desde el equipo de Hola. Utilizamos CURL tooinvoke Hola Hola de Livio extremos toorun trabajos de forma remota.

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a>Hola ejecución Spark streaming tooreceive Hola eventos de aplicación en un Blob de almacenamiento de Azure como texto

Abra un símbolo del sistema, navegue directorio toohello donde instaló CURL y ejecute hello siguiente comando (reemplazar nombre de usuario/contraseña y clúster nombre):

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hola parámetros en el archivo hello **inputBlob.txt** se definen como sigue:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Vamos a explicar cuáles son los parámetros de hello en el archivo de entrada de hello:

* **archivo** es Hola el archivo jar de ruta de acceso toohello aplicación hello Azure cuenta de almacenamiento asociado con el clúster de Hola.
* **className** es Hola nombre de clase de hello en jar Hola.
* **args** es Hola lista de argumentos requeridos por la clase hello
* **numExecutors** es Hola número de núcleos usados por Hola de Spark toorun transmisión por secuencias la aplicación. Siempre debería ser al menos dos veces el número de Hola de particiones de concentrador de eventos.
* **executorMemory**, **executorCores**, **driverMemory** son parámetros utilizados tooassign requerido recursos toohello de transmisión por secuencias la aplicación.

> [!NOTE]
> No es necesario toocreate Hola carpetas de salida (EventCheckpoint, conteo de eventos/EventCount10) que se utilizan como parámetros. Hola streaming aplicación creará automáticamente.
>
>

Al ejecutar el comando de hello, debería ver una salida similar Hola siguiente:

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

Tome nota del identificador de lote de hello en la última línea de saludo del resultado de hello (en este ejemplo es '1'). tooverify que Hola aplicación se ejecuta correctamente, puede mirar la cuenta de almacenamiento de Azure asociada con el clúster de Hola y debería ver Hola **/conteo de eventos/EventCount10** carpeta creado. Esta carpeta debe contener blobs que captura Hola número de eventos procesados en hello período de tiempo especificado para el parámetro hello **lote intervalo en segundos**.

aplicación de transmisión por secuencias de Hello Spark continuará toorun hasta que la elimine. toodo por lo tanto, use Hola siguiente comando:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a>Ejecutar aplicaciones de hello tooreceive eventos de hello en un Blob de almacenamiento de Azure como JSON
Abra un símbolo del sistema, navegue directorio toohello donde instaló CURL y ejecute hello siguiente comando (reemplazar nombre de usuario/contraseña y clúster nombre):

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hola parámetros en el archivo hello **inputJSON.txt** se definen como sigue:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

parámetros de Hello son toowhat similar que especificó para la salida de texto hello, en el paso anterior de Hola. Una vez más, no es necesario toocreate Hola carpetas de salida (EventCheckpoint, conteo de eventos/EventCount10) que se utilizan como parámetros. Hola streaming aplicación creará automáticamente.

 Después de ejecutar el comando de hello, puede mirar la cuenta de almacenamiento de Azure asociada con el clúster de Hola y debería ver Hola **/EventStore10** carpeta creado. Abra cualquier archivo con el prefijo **parte -** y debería ver los eventos de hello procesados en un formato JSON.

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a>Ejecutar aplicaciones de hello tooreceive eventos de hello en una tabla de Hive
Hola toorun aplicación de streaming de Spark que la tabla eventos de secuencias en un subárbol necesita algunos componentes adicionales. Dichos componentes son:

* datanucleus-api-jdo-3.2.6.jar
* datanucleus-rdbms-3.2.9.jar
* datanucleus-core-3.2.10.jar
* hive-site.xml

Hola **.jar** archivos están disponibles en el clúster de HDInsight Spark en `/usr/hdp/current/spark-client/lib`. Hola **hive-site.xml** está disponible en `/usr/hdp/current/spark-client/conf`.

Puede usar [WinScp](http://winscp.net/eng/download.php) toocopy a través de estos archivos del equipo local de hello clúster tooyour. A continuación, puede usar toocopy herramientas estos archivos a través de la cuenta de almacenamiento de tooyour asociados a clúster Hola. Para obtener más información sobre cómo se tooupload archivos toohello cuenta de almacenamiento, consulte [cargar datos para los trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).

Una vez que migraron Hola archivos tooyour cuenta de almacenamiento de Azure, abra un símbolo del sistema, navegue directorio toohello donde instaló CURL y ejecute hello siguiente comando (reemplazar nombre de usuario/contraseña y clúster nombre):

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hola parámetros en el archivo hello **inputHive.txt** se definen como sigue:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

parámetros de Hello son toowhat similar que especificó para la salida de texto hello, en los pasos anteriores de Hola. Una vez más, no es necesario salida de hello toocreate carpetas (EventCheckpoint, conteo de eventos/EventCount10) o hello de la tabla de Hive (EventHiveTable10) que se utilizan como parámetros de salida. Hola streaming aplicación creará automáticamente. Tenga en cuenta que hello **archivos JAR** y **archivos** opción incluye archivos .jar de rutas de acceso toohello y Hola hive-site.xml que copió toohello cuenta de almacenamiento.

tooverify que Hola tabla de hive se creó correctamente, puede SSH en clúster de Hola y ejecución de consultas de Hive. Para obtener instrucciones, consulte [Uso de Hive con Hadoop en HDInsight con SSH](hdinsight-hadoop-use-hive-ssh.md). Una vez que están conectados a través de SSH, puede ejecutar Hola después comando tooverify esa tabla de Hive hello, **EventHiveTable10**, se crea.

    show tables;

Debería ver un siguiente toohello similar de salida:

    OK
    eventhivetable10
    hivesampletable

También puede ejecutar una consulta SELECT tooview contenido de Hola de tabla Hola.

    SELECT * FROM eventhivetable10 LIMIT 10;

Debería ver una salida similar Hola siguiente:

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a>Ejecutar aplicaciones de hello tooreceive eventos de hello en una tabla de base de datos de SQL Azure
Antes de realizar este paso, asegúrese de que ha creado una Base de datos SQL de Azure. Para instrucciones, consulte el artículo sobre la [creación de una base de datos SQL en cuestión de minutos](../sql-database/sql-database-get-started.md). toocomplete esta sección, necesita valores de nombre de base de datos, el nombre del servidor de base de datos y credenciales de administrador de base de datos de hello como parámetros. No es necesario aunque la tabla de base de datos de toocreate Hola. Hola aplicación de streaming de Spark crea para usted.

Abra un símbolo del sistema, navegue directorio toohello donde instaló CURL y ejecute el siguiente comando de hello:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Hola parámetros en el archivo hello **inputSQL.txt** se definen como sigue:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

tooverify que Hola aplicación se ejecuta correctamente, puede conectarse toohello de base de datos de SQL Azure con SQL Server Management Studio. Para obtener instrucciones sobre cómo toodo que vea [conectar tooSQL base de datos con SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md). Una vez que esté conectado toohello base de datos, puede navegar toohello **EventContent** tabla creada por hello transmisión por secuencias la aplicación. Puede ejecutar una consulta rápida tooget Hola de datos de tabla de Hola. Ejecute hello después de consulta:

    SELECT * FROM EventCount

Debería ver resultados similares toohello siguiente:

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <a name="seealso"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)
* [Design of Receiver-based Connection and Direct DStream](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317) (Diseño de conexiones basadas en receptor y Direct DStream)

### <a name="scenarios"></a>Escenarios
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar Spark Scala aplicaciones](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
