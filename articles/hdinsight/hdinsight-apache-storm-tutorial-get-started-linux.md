---
title: ejemplos de inicio de aaaStorm en Apache Storm en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodo análisis de grandes cantidades de datos y procesar los datos en tiempo real con Apache Storm y Hola ejemplos de inicio de storm en HDInsight."
keywords: storm-starter, ejemplo de apache storm
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a>Introducción a Apache Storm en HDInsight con ejemplos de hello storm-inicio

Obtenga información acerca de cómo toouse Apache Storm en HDInsight utilizando Hola ejemplos storm starter.

Apache Storm es un sistema de cálculo distribuido, escalable, con tolerancia a errores y en tiempo real para el procesamiento de secuencias de datos. Con Storm en HDInsight de Azure, puede crear un clúster de Storm basado en la nube que realice análisis en tiempo real de grandes cantidades de datos en tiempo real.

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Requisitos previos

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Familiaridad con SSH y SCP**. Para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-a-storm-cluster"></a>Creación de un clúster de Storm

Usar hello siguiendo los pasos toocreate una tormenta en clúster de HDInsight:

1. De hello [portal de Azure](https://portal.azure.com), seleccione **+ nuevo**, **Intelligence + análisis**y, a continuación, seleccione **HDInsight**.

    ![Creación de un clúster de HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. De hello **Fundamentos** hoja, escriba Hola siguiente información:

    * **Nombre del clúster**: nombre de Hola Hola del clúster de HDInsight.
    * **Suscripción**: seleccione Hola suscripción toouse.
    * **Nombre de usuario de inicio de sesión del clúster** y **contraseña de inicio de sesión de clúster**: inicio de sesión de hello al tener acceso a los clústeres de Hola a través de HTTPS. Utilice estos servicios de tooaccess de credenciales como Hola interfaz de usuario de Ambari Web o API de REST.
    * **Secure Shell (SSH) username**: inicio de sesión de hello usado al acceder a clúster hello mediante SSH. De forma predeterminada contraseña hello es Hola igual que la contraseña de inicio de sesión de clúster de Hola.
    * **Grupo de recursos**: clúster hello toocreate de grupo de recursos de hello en.
    * **Ubicación**: Hola región de Azure toocreate Hola clúster.

    ![Seleccione la suscripción.](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. Seleccione **clúster tipo**, y, a continuación, Hola de conjunto de valores de hello **configuración de clúster** hoja:

    * **Tipo de clúster**: Storm

    * **Sistema operativo**: Linux

    * **Versión**: Storm 1.1.0 (HDI 3.6)

    * **Nivel de clúster**: estándar

    Por último, utilice hello **seleccione** botón toosave configuración.

    ![Seleccionar el tipo de clúster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. Después de seleccionar el tipo de clúster de hello, usar hello __seleccione__ tooset Hola clúster tipo de botón. A continuación, usar hello __siguiente__ configuración básica del botón toofinish.

5. De hello **almacenamiento** hoja, seleccione o cree una cuenta de almacenamiento. Para conocer los pasos hello en este documento, deje Hola otros campos en esta hoja en valores predeterminados de Hola. Hola de uso __siguiente__ configuración de almacenamiento de toosave de botón.

    ![Establecer la configuración de cuenta de almacenamiento de Hola para HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. De hello **resumen** hoja, revisar la configuración de hello para el clúster de Hola. Hola de uso __editar__ vincula toochange cualquier configuración que no sean correcta. Por último, utilice el clúster de the__Create__ botón toocreate Hola.

    ![Resumen de configuración del clúster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > Puede durar de clúster de too20 minutos toocreate Hola.

## <a name="run-a-storm-starter-sample-on-hdinsight"></a>Ejecución de un ejemplo de Storm-Starter en HDInsight

1. Conecte el clúster de HDInsight de toohello mediante SSH:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Si utiliza un toosecure de contraseña de su cuenta de usuario SSH, son tooenter solicitada se. Si utiliza una clave pública, que necesita utilizar hello `-i` parámetro toospecify Hola clave privada correspondiente. Por ejemplo: `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

    Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Usar hello después comando toostart una topología de ejemplo:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > En versiones anteriores de HDInsight, nombre de clase de Hola de topología de hello es `storm.starter.WordCountTopology` en lugar de `org.apache.storm.starter.WordCountTopology`.

    Este comando inicia la topología de WordCount de ejemplo de Hola en clúster de hello, con un nombre descriptivo de 'wordcount'. Genera aleatoriamente frases y repetición de Hola de recuento de cada palabra en las frases de Hola.

    > [!NOTE]
    > Al enviar su propio clúster de toohello topologías, primero debe copiar archivo jar de Hola que contiene el clúster de hello antes de usar hello `storm` comando. Hola de uso `scp` archivo de comandos toocopy Hola. Por ejemplo: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > ejemplo de WordCount Hello y otros ejemplos de storm starter, ya están incluidas en el clúster en `/usr/hdp/current/storm-client/contrib/storm-starter/`.

Si está interesado en Ver origen Hola para obtener ejemplos de inicio aluvión de hello, puede encontrar código de hello en [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter). Este vínculo es para Storm 1.1.x, que se proporciona con HDInsight 3.6. Para otras versiones de Storm, usar hello __bifurcación__ situado en la parte superior de Hola de hello página tooselect una versión diferente de Storm.

## <a name="monitor-hello-topology"></a>Topología de Hola de Monitor

Hola aluvión de interfaz de usuario proporciona una interfaz web para trabajar con topologías en ejecución y se incluye en el clúster de HDInsight.

Usar hello después de la topología de hello toomonitor pasos con hello aluvión de interfaz de usuario:

1. Hola toodisplay aluvión de interfaz de usuario, abra un web explorador toohttps://CLUSTERNAME.azurehdinsight.net/stormui. Reemplace **CLUSTERNAME** con nombre hello del clúster.

    > [!NOTE]
    > Si se le solicita tooprovide un nombre de usuario y una contraseña, escriba Administrador de clústeres de hello (admin) y la contraseña que ha utilizado al crear clúster Hola.

2. En **resumen de la topología**, seleccione hello **wordcount** entrada Hola **nombre** columna. Se muestra información acerca de la topología de Hola.

    ![Panel de Storm con la información de topología de WordCount de Storm-Starter.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    Esta página proporciona Hola siguiente información:

    * **Estadísticas de topología** -información básica sobre el rendimiento de la topología de hello, que se organizan en las ventanas de tiempo.

        > [!NOTE]
        > Al seleccionar un período de tiempo de hora específica ventana cambios hello para la información que se muestra en otras secciones de página de Hola.

    * **Spouts** -información básica sobre spouts, incluido el último error de hello devuelto por cada pitorro.

    * **Bolts** : información básica sobre bolts.

    * **Configuración de la topología** -información detallada sobre la configuración de la topología de Hola.

    Esta página también proporciona las acciones que pueden realizarse en la topología de hello:

    * **Activar** : reanuda el procesamiento de una topología desactivada.

    * **Desactivar** : pausa una topología en ejecución.

    * **Reequilibrar** -ajusta paralelismo Hola de topología de Hola. Debe volver a equilibrar las topologías de ejecución después de que haya cambiado Hola número de nodos de clúster de Hola. Reequilibrio ajusta toocompensate de paralelismo para número aumenta o disminuye de Hola de nodos de clúster de Hola. Para obtener más información, consulte [descripción paralelismo Hola de una topología de Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

    * **Kill** -termine una topología de Storm después Hola especifica el tiempo de espera.

3. En esta página, seleccione una entrada de hello **Spouts** o **tornillos** sección. Se muestra información acerca del componente seleccionado Hola.

    ![Panel de Storm con información acerca de los componentes seleccionados.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    Esta página muestra hello siguiente información:

    * **Estadísticas de pitorro/rayo** -información básica sobre el rendimiento de componente de hello, que se organizan en las ventanas de tiempo.

        > [!NOTE]
        > Al seleccionar un período de tiempo de hora específica ventana cambios hello para la información que se muestra en otras secciones de página de Hola.

    * **Estadísticas de entrada** (solo tornillo): información sobre los componentes que generan datos utilizados por el rayo Hola.

    * **Estadísticas de salida** : información sobre los datos que emite este bolt.

    * **Ejecutores** : información sobre las instancias de este componente.

    * **Errores** : errores que ha generado este componente.

4. Al ver los detalles de Hola de un pitorro o rayo, seleccione una entrada de hello **puerto** columna Hola **ejecutor** sección tooview detalles para una instancia específica del componente de Hola.

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    En este ejemplo, hello word **siete** se ha producido 1493957 veces. Este recuento indica cuántas veces se ha encontrado la palabra Hola desde que se inició esta topología.

## <a name="stop-hello-topology"></a>Detener la topología de Hola

Devolver toohello **resumen de la topología** página topología de recuento de palabras de hello y, a continuación, seleccione hello **Kill** botón de hello **acciones de topología** sección. Cuando se le solicite, escriba 10 para hello segundos toowait antes de detener la topología de Hola. Después de tiempo de espera de hello, topología Hola ya no aparece cuando visiten hello **aluvión de interfaz de usuario** sección del panel de Hola.

## <a name="delete-hello-cluster"></a>Eliminar el clúster de Hola

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Si experimenta un problema con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a id="next"></a>Pasos siguientes

En este tutorial Apache Storm, ha aprendido conceptos básicos de hello sobre cómo trabajar con Storm en HDInsight. A continuación, obtenga información acerca de cómo demasiado[topologías de basados en Java desarrollar con Maven](hdinsight-storm-develop-java-topology.md).

Si ya está familiarizado con el desarrollo de topologías basados en Java y desea toodeploy una tooHDInsight topología existente, consulte [implementar y administrar topologías de Apache Storm en HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).

Si es desarrollador de. NET, puede crear topologías de C# o C#/Java híbridas con Visual Studio. Para más información, consulte [Desarrollo de topologías de C# para Apache Storm en HDInsight con herramientas de Hadoop para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Para las topologías de ejemplo que pueden utilizarse con Storm en HDInsight, vea hello en los ejemplos siguientes:

* [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
