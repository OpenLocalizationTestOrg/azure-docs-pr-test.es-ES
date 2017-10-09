---
title: aaaProcess eventos desde los centros de eventos con Storm - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooprocess los datos de los centros de eventos de Azure con una topología de C# Storm crean en Visual Studio, mediante el uso de hello herramientas de HDInsight para Visual Studio."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a>Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight (C#)

Obtenga información acerca de cómo toowork con concentradores de eventos de Azure desde Apache Storm en HDInsight. Este documento usa una tormenta de C# topología tooread y escritura de datos desde los centros de Evbent

> [!NOTE]
> Para ver una versión en Java de este proyecto, consulte [Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="scpnet"></a>SCP.NET

pasos de Hello en este documento utiliza SCP.NET, un paquete de NuGet que resulta fácil toocreate C# topologías y componentes para su uso con Storm en HDInsight.

> [!IMPORTANT]
> Aunque Hola los pasos de este documento se basan en un entorno de desarrollo de Windows con Visual Studio, proyecto compilado Hola puede ser enviado tooa Storm en clúster de HDInsight que usa Linux. Solo los clústeres basados en Linux creados después del 28 de octubre de 2016 admiten topologías SCP.NET.

3.4 de HDInsight y topologías de Mono toorun C# de mayor uso. ejemplo de Hola usado en este documento funciona con 3.6 de HDInsight. Si tiene previsto crear sus propias soluciones de .NET para HDInsight, comprobar hello [compatibilidad Mono](http://www.mono-project.com/docs/about-mono/compatibility/) documento para detectar posibles incompatibilidades.

### <a name="cluster-versioning"></a>Control de versiones de clúster

Hola paquete Microsoft.SCP.Net.SDK NuGet se utiliza para el proyecto debe coincidir con la versión principal de Hola de Storm instalado en HDInsight. Las versiones de HDInsight 3.5 y 3.6 usan Storm 1.x, por lo que debe usar la versión 1.0.x.x de SCP.NET con estos clústeres.

> [!IMPORTANT]
> ejemplo de Hola en este documento espera un 3.5 HDInsight o clúster 3,6.
>
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Las topologías de C# también deben tener como destino .NET 4.5.

## <a name="how-toowork-with-event-hubs"></a>¿Cómo toowork con concentradores de eventos

Microsoft proporciona un conjunto de componentes de Java que pueden ser utilizado toocommunicate con concentradores de eventos de una topología de Storm. Puede encontrar Hola Java (JAR) archivo que contiene una versión compatible de HDInsight 3.6 de estos componentes en [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

> [!IMPORTANT]
> Mientras que los componentes de hello están escritos en Java, puede utilizarlos fácilmente de una topología de C#.

en este ejemplo se utiliza Hola de los componentes siguientes:

* __EventHubSpout__: lee datos de Event Hubs.
* __EventHubBolt__: escribe tooEvent centros de datos.
* __EventHubSpoutConfig__: usar tooconfigure EventHubSpout.
* __EventHubBoltConfig__: usar tooconfigure EventHubBolt.

### <a name="example-spout-usage"></a>Ejemplo de uso de spout

SCP.NET proporciona métodos para agregar una topología de tooyour EventHubSpout. Estos métodos que sea más fácil tooadd un pitorro que el uso de métodos genéricos de Hola para agregar un componente de Java. Hello en el ejemplo siguiente se muestra cómo toocreate un pitorro utilizando Hola __SetEventHubSpout__ y **EventHubSpoutConfig** métodos proporcionados por SCP.NET:

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

ejemplo de Hola anterior crea un nuevo componente de pitorro denominado __EventHubSpout__y configura toocommunicate con un concentrador de eventos. Sugerencia de paralelismo de Hello para el componente de Hola se establece toohello número de particiones en el centro de eventos de Hola. Esta configuración permite Storm toocreate una instancia del componente de Hola para cada partición.

### <a name="example-bolt-usage"></a>Ejemplo de uso de bolt

Hola de uso **JavaComponmentConstructor** método toocreate una instancia de rayo Hola. Hello ejemplo siguiente se muestra cómo toocreate y configurar una nueva instancia de hello **EventHubBolt**:

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> Este ejemplo utiliza una expresión de Clojure pasada como una cadena, en lugar de usar **JavaComponentConstructor** toocreate una **EventHubBoltConfig**, tal y como ejemplo de Hola pitorro hacía. Cualquiera de estos métodos funciona. Utilice el método de Hola que se siente tooyou mejor.

## <a name="download-hello-completed-project"></a>Descargar proyecto Hola completado

Puede descargar una versión completa de proyecto Hola creada en este tutorial de [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub). Sin embargo, todavía necesita opciones de configuración de tooprovide siguiendo los pasos de hello en este tutorial.

### <a name="prerequisites"></a>Requisitos previos

* Una [instancia de Apache Storm en un clúster de HDInsight, versión 3.5 o 3.6](hdinsight-apache-storm-tutorial-get-started.md).

    > [!WARNING]
    > ejemplo de Hola usado en este documento requiere Storm en HDInsight versión 3.5 o 3.6. Esto no funciona con versiones anteriores de HDInsight, debido a cambios de nombre de clase toobreaking. Para obtener una versión de este ejemplo que funcione con clústeres anteriores, vea [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).

* Un [centro de eventos de Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* Hola [Azure SDK para .NET](http://azure.microsoft.com/downloads/).

* Hola [HDInsight tools para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Java JDK 1.8 o posterior en el entorno de desarrollo. Las descargas de JDK están disponibles en [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

  * Hola **JAVA_HOME** entorno debe variable punto toohello el directorio que contiene Java.
  * Hola **%JAVA_HOME%/bin** directorio debe estar en la ruta de acceso de Hola.

## <a name="download-hello-event-hubs-components"></a>Descargar los componentes de los centros de eventos de Hola

Descarga Hola centros de eventos apetezca charlar y el tornillo del componente de [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

Cree un directorio denominado `eventhubspout`y guarde el archivo de hello en el directorio de Hola.

## <a name="configure-event-hubs"></a>Configuración de Centros de eventos

Centros de eventos es el origen de datos de Hola para este ejemplo. Utilice la información de hello en la sección "Crear un concentrador de eventos" de Hola de [empezar a trabajar con concentradores de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

1. Una vez creado el concentrador de eventos de hello, ver hello **EventHub** hoja en hello Azure portal y, a continuación, seleccione **directivas de acceso compartido**. Seleccione **+ agregar** hello tooadd las siguientes directivas:

   | Nombre | Permisos |
   | --- | --- |
   | escritor |Los métodos Send |
   | lector |Escuchar |

    ![Captura de pantalla de la ventana Directivas de acceso compartido](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. Seleccione hello **lector** y **escritor** directivas. Copie y guarde el valor de clave principal de Hola para las dos directivas, ya que estos valores se usan más adelante.

## <a name="configure-hello-eventhubwriter"></a>Configurar hello EventHubWriter

1. Si no ha instalado ya Hola versión más reciente de las herramientas de HDInsight de Hola para Visual Studio, consulte [Introducción al uso de herramientas de HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Descargue la solución Hola de [eventhub-storm-híbrida](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

3. Hola **EventHubWriter** proyecto, abra hello **App.config** archivo. Utilice información de Hola de concentrador de eventos de Hola que configuró toofill anterior en el valor de Hola para hello siguiendo las claves:

   | Clave | Valor |
   | --- | --- |
   | EventHubPolicyName |sistema de escritura (si utiliza un nombre diferente para la directiva de hello con *enviar* permiso, utilizarlo en su lugar.) |
   | EventHubPolicyKey |clave de Hello para la directiva de sistema de escritura de Hola. |
   | EventHubNamespace |Hola espacio de nombres que contiene el centro de eventos. |
   | EventHubName |Nombre del centro de eventos. |
   | EventHubPartitionCount |número de Hola de particiones en el centro de eventos. |

4. Guarde y cierre hello **App.config** archivo.

## <a name="configure-hello-eventhubreader"></a>Configurar hello EventHubReader

1. Abra hello **EventHubReader** proyecto.

2. Abra hello **App.config** archivo para hello **EventHubReader**. Utilice información de Hola de concentrador de eventos de Hola que configuró toofill anterior en el valor de Hola para hello siguiendo las claves:

   | Clave | Valor |
   | --- | --- |
   | EventHubPolicyName |lector (si utiliza un nombre diferente para la directiva de hello con *escuchar* permiso, utilizarlo en su lugar.) |
   | EventHubPolicyKey |clave de Hola para directiva de lector de Hola. |
   | EventHubNamespace |Hola espacio de nombres que contiene el centro de eventos. |
   | EventHubName |Nombre del centro de eventos. |
   | EventHubPartitionCount |número de Hola de particiones en el centro de eventos. |

3. Guarde y cierre hello **App.config** archivo.

## <a name="deploy-hello-topologies"></a>Implementar topologías de Hola

1. De **el Explorador de soluciones**, contextual hello **EventHubReader** de proyecto y seleccione **enviar tooStorm en HDInsight**.

    ![Captura de pantalla del explorador de soluciones, con enviar tooStorm en HDInsight resaltado](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. En hello **topología enviar** cuadro de diálogo, seleccione la **clúster de Storm**. Expanda **configuraciones adicionales**, seleccione **las rutas de acceso de Java**, seleccione **...** y un directorio de hello select que contiene el archivo JAR de Hola que ha descargado anteriormente. Finalmente, haga clic en **Enviar**.

    ![Captura de pantalla del cuadro de diálogo Enviar topología](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. Cuando se ha enviado la topología de hello, Hola **aluvión de topologías Visor** aparece. tooview información acerca de la topología de hello, seleccione hello **EventHubReader** topología en el panel izquierdo de Hola.

    ![Captura de pantalla del Visor de topologías de Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. De **el Explorador de soluciones**, contextual hello **EventHubWriter** de proyecto y seleccione **enviar tooStorm en HDInsight**.

5. En hello **topología enviar** cuadro de diálogo, seleccione la **clúster de Storm**. Expanda **configuraciones adicionales**, seleccione **las rutas de acceso de Java**, seleccione **...** , y el directorio de hello select que contiene el archivo JAR de Hola descargó anteriormente. Finalmente, haga clic en **Enviar**.

6. Cuando se ha enviado la topología de hello, actualice la lista de topología de Hola Hola **aluvión de topologías Visor** tooverify que todas estas topologías se ejecutan en el clúster de Hola.

7. En **aluvión de topologías Visor**, seleccione hello **EventHubReader** topología.

8. componente de hello tooopen resumen rayo de hello, haga doble clic en hello **LogBolt** componente en el diagrama de Hola.

9. Hola **ejecutor** sección, seleccione uno de los vínculos de Hola Hola **puerto** columna. Esto muestra la información registrada por el componente de Hola. información de Hello optimizado es similar toohello siguiente texto:

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a>Detener las topologías de Hola

topologías de hello toostop, seleccione cada topología de hello **Visor de la topología de Storm**, a continuación, haga clic en **Kill**.

![Captura de pantalla del Visor de topologías de Storm con el botón Eliminar resaltado](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Eliminación del clúster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Pasos siguientes

En este documento, ha aprendido cómo toouse Hola Java y centros de eventos apetezca charlar un tornillo desde un toowork de topología de C# con datos en los centros de eventos de Azure. toolearn más información acerca de la creación de topologías de C#, vea Hola recursos siguientes:

* [Desarrollo de topologías de C# para Apache Storm en HDInsight con Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Guía de programación de SCP](hdinsight-storm-scp-programming-guide.md)
* [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md)
