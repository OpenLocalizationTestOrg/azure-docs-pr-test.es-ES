---
title: "aaaDeploy y administrar topologías de Apache Storm en HDInsight basados en Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy, supervisar y administrar topologías de Apache Storm con hello aluvión de panel en HDInsight basados en Linux. Utilice herramientas de Hadoop para Visual Studio"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a>Implementación y administración de topologías de Apache Storm en HDInsight

En este documento, información sobre conceptos básicos de Hola de administración y supervisión de topologías de Storm ejecutando Storm en clústeres de HDInsight.

> [!IMPORTANT]
> Hello pasos de este artículo requieren una tormenta basadas en Linux en clúster de HDInsight. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). 
>
> Para obtener información sobre la implementación y la supervisar de topologías en HDInsight basado en Windows, vea [Implementar y administrar topologías de Apache Storm en HDInsight basado en Windows](hdinsight-storm-deploy-monitor-topology.md)


## <a name="prerequisites"></a>Requisitos previos

* **Clúster de Storm basado en Linux en HDInsight**: consulte [Introducción a Apache Storm en HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) para conocer los pasos para crear un clúster.

* **Familiaridad con SSH y SCP** (opcional): para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* (Opcional) **Visual Studio**: Azure SDK 2.5.1 o versiones más recientes y Hola Data Lake Tools para Visual Studio. Para más información, consulte [Introducción al uso de Herramientas de Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    Uno de hello después de versiones de Visual Studio:

  * Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)

  * Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio Community 2013](http://go.microsoft.com/fwlink/?LinkId=517284)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/)

  * Visual Studio 2015 (cualquier edición)

  * Visual Studio 2017 (cualquier edición). Data Lake Tools para Visual Studio de 2017 se instalan como parte del programa Hola a cargas de trabajo de Azure.

## <a name="submit-a-topology-visual-studio"></a>Envío de una topología: Visual Studio

Herramientas de HDInsight de Hello puede ser toosubmit usa C# o híbrida topologías tooyour clúster de Storm. Hola pasos usa una aplicación de ejemplo. Para obtener información acerca de cómo crear sus propios topologías mediante las herramientas de HDInsight de hello, consulte [C# desarrollar topologías con hello HDInsight Tools para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

1. Si no ha instalado ya Hola versión más reciente de las herramientas de Data Lake Hola para Visual Studio, consulte [Introducción al uso de Data Lake Tools para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    > [!NOTE]
    > Hola Data Lake Tools para Visual Studio se denominaba hello HDInsight Tools para Visual Studio.
    >
    > Data Lake Tools para Visual Studio se incluyen en hello __cargas de trabajo de Azure__ para Visual Studio de 2017.

2. Abra Visual Studio, seleccione **Archivo** > **Nuevo** > **Proyecto**.

3. Hola **nuevo proyecto** cuadro de diálogo, expanda **instalado** > **plantillas**y, a continuación, seleccione **HDInsight**. En la lista Hola de plantillas, seleccione **aluvión de ejemplo**. En parte inferior de Hola Hola del cuadro de diálogo, escriba un nombre para la aplicación hello.

    ![imagen](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **enviar tooStorm en HDInsight**.

   > [!NOTE]
   > Si se le solicite, escriba las credenciales de inicio de sesión de hello para la suscripción de Azure. Si tiene más de una suscripción, inicie sesión en toohello uno que contiene el aluvión en clúster de HDInsight.

5. Seleccione el aluvión en clúster de HDInsight de hello **clúster de Storm** lista desplegable y, a continuación, seleccione **enviar**. Puede supervisar si el envío de hello es correcto mediante hello **salida** ventana.

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a>Enviar una topología: SSH y hello Storm comando

1. Use el clúster de HDInsight de toohello tooconnect SSH. Reemplace **nombre de usuario** nombre hello del inicio de sesión SSH. Reemplace **CLUSTERNAME** por el nombre del clúster de HDInsight.

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Para obtener más información sobre cómo utilizar SSH tooconnect tooyour HDInsight de clúster, consulte [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Usar hello después comando toostart una topología de ejemplo:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    Este comando inicia la topología de WordCount de ejemplo de Hola en clúster de Hola. Esta topología generar de forma aleatoria las frases y repetición de Hola de recuento de cada palabra en las frases de Hola.

   > [!NOTE]
   > Al enviar el clúster de topología toohello, primero debe copiar archivo jar de Hola que contiene el clúster de hello antes de usar hello `storm` comando. clúster de toohello de toocopy Hola archivos, puede usar hello `scp` comando. Por ejemplo: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
   >
   > ejemplo de WordCount Hello y otros ejemplos de inicio de storm, ya están incluidas en el clúster en `/usr/hdp/current/storm-client/contrib/storm-starter/`.

## <a name="submit-a-topology-programmatically"></a>Envío de una topología: de manera programática

Mediante programación, puede implementar un tooStorm topología en HDInsight comunicándose con hello servicio Nimbus hospedado en el clúster. [https://github.com/Azure-Samples/hdinsight-Java-Deploy-Storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) proporciona un ejemplo de aplicación Java que muestra cómo toodeploy e iniciar una topología a través del servicio Nimbus Hola.

## <a name="monitor-and-manage-visual-studio"></a>Supervisión y administración: Visual Studio

Cuando una topología se ha enviado correctamente con Visual Studio, Hola **aluvión de topologías** de hello clúster aparece en la vista. Seleccione topología Hola de hello mostrar tooview información acerca de hello ejecutando topología.

![supervisión de visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> También puede ver las **topologías de Storm** en el **Explorador de servidores** expandiendo **Azure** > **HDInsight** y, después, haciendo clic con el botón derecho en un clúster de Storm en HDInsight y seleccionando **View Storm Topologies** (Ver topologías de Storm).

Seleccione la forma de Hola Hola spouts o tornillos tooview información acerca de estos componentes. Se abrirá una ventana nueva para cada elemento seleccionado.

### <a name="deactivate-and-reactivate"></a>Desactivar y reactivar

Al desactivar una topología se pone en pausa hasta que se elimine o se reactive. tooperform estas operaciones, usar hello __desactivar__ y __reactivar__ botones en la parte superior de Hola de hello __resumen de la topología__.

### <a name="rebalance"></a>Reequilibrar

Reequilibrio una topología permite Hola sistema toorevise Hola el paralelismo de topología de Hola. Por ejemplo, si se han cambiado el tamaño Hola clúster tooadd más notas, reequilibrio permite una topología de nuevos nodos de toosee Hola.

toorebalance una topología, usar hello __reequilibrar__ situado en la parte superior de Hola de hello __resumen de la topología__.

> [!WARNING]
> Reequilibrio primero una topología desactiva la topología de hello, redistribuye los trabajadores uniformemente en el clúster de hello y, luego, por último devuelve estado toohello Hola topología en que estaba antes de producirse el equilibrio. Por lo que si la topología de hello estaba activo, vuelve activo. Si se desactivó, seguirá desactivada.

### <a name="kill-a-topology"></a>Terminación de una topología

Topologías de Storm continúan ejecutándose hasta que se hayan detenido o se elimina el clúster de Hola. toostop una topología, usar hello __Kill__ situado en la parte superior de Hola de hello __resumen de la topología__.

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a>Supervisar y administrar: SSH y hello Storm comando

Hola `storm` utilidad le permite toowork con topologías en ejecución desde la línea de comandos de Hola. Use `storm -h` para obtener una lista completa de comandos.

### <a name="list-topologies"></a>Topologías de lista

Usar hello después a toolist comando todas las topologías de ejecución:

    storm list

Este comando devuelve información toohello similar siguiente texto:

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a>Desactivar y reactivar

Al desactivar una topología se pone en pausa hasta que se elimine o se reactive. Usar hello después toodeactivate de comando y volver a activar:

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a>Eliminar una topología de ejecución

Las topologías de Storm, una vez iniciadas, se siguen ejecutando hasta que se detengan. toostop una topología, utilice Hola siguiente comando:

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a>Reequilibrar

Reequilibrio una topología permite Hola sistema toorevise Hola el paralelismo de topología de Hola. Por ejemplo, si se han cambiado el tamaño Hola clúster tooadd más notas, reequilibrio permite una topología de nuevos nodos de toosee Hola.

> [!WARNING]
> Reequilibrio primero una topología desactiva la topología de hello, redistribuye los trabajadores uniformemente en el clúster de hello y, luego, por último devuelve estado toohello Hola topología en que estaba antes de producirse el equilibrio. Por lo que si la topología de hello estaba activo, vuelve activo. Si se desactivó, seguirá desactivada.

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a>Supervisión y administración: IU de Storm

Hola aluvión de interfaz de usuario proporciona una interfaz web para trabajar con topologías en ejecución y se incluye en el clúster de HDInsight. Hola tooview aluvión de interfaz de usuario, utilice un tooopen de explorador web **https://CLUSTERNAME.azurehdinsight.net/stormui**, donde **CLUSTERNAME** es Hola nombre del clúster.

> [!NOTE]
> Si se le solicita tooprovide un nombre de usuario y una contraseña, escriba Administrador de clústeres de hello (admin) y la contraseña que ha utilizado al crear clúster Hola.

### <a name="main-page"></a>Página principal

página principal de Hola de hello aluvión de interfaz de usuario proporciona Hola siguiente información:

* **Resumen de clúster**: información básica sobre el clúster de Storm Hola.
* **Resumen de las topologías**: una lista de las topologías en ejecución. Usar vínculos de hello en esta sección tooview obtener más información acerca de las topologías específicas.
* **Resumen de supervisor**: obtener información sobre el supervisor de Storm Hola.
* **Configuración de Nimbus**: configuración de Nimbus para clúster Hola.

### <a name="topology-summary"></a>Resumen de las topologías

Si selecciona un vínculo de hello **resumen de la topología** sección muestra hello después de obtener información acerca de la topología de hello:

* **Resumen de la topología**: información básica acerca de la topología de Hola.
* **Acciones de topología**: acciones de administración que puede realizar para la topología de Hola.

  * **Activar**: reanuda el procesamiento de una topología desactivada.
  * **Desactivar**: pausa una topología en ejecución.
  * **Reequilibrar**: ajusta el paralelismo de Hola de topología de Hola. Debe volver a equilibrar las topologías de ejecución después de que haya cambiado Hola número de nodos de clúster de Hola. Esta operación permite Hola topología tooadjust paralelismo toocompensate para hello aumenta o reduce el número de nodos de clúster de Hola.

    Para obtener más información, consulte <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">descripción paralelismo Hola de una topología de Storm</a>.
  * **Kill**: termine una topología de Storm después Hola especifica el tiempo de espera.
* **Estadísticas de topología**: estadísticas acerca de la topología de Hola. tooset Hola franja temporal para hello restantes entradas en la página de hello, usar los vínculos de Hola de hello **ventana** columna.
* **Spouts**: Hola spouts utilizados por la topología de Hola. Usar vínculos de hello en esta sección tooview obtener más información sobre spouts específicos.
* **Tornillos**: Hola tornillos utilizados por la topología de Hola. Usar vínculos de hello en esta sección tooview obtener más información acerca de los tornillos específicos.
* **Configuración de la topología**: configuración de Hola de topología de hello seleccionado.

### <a name="spout-and-bolt-summary"></a>Resumen de spouts y bolts

Seleccionar un pitorro de hello **Spouts** o **tornillos** secciones muestra hello después de obtener información sobre el elemento Hola seleccionado:

* **Resumen de componentes**: información básica sobre pitorro Hola o rayo.
* **Estadísticas de pitorro/rayo**: estadísticas sobre Hola apetezca charlar o el tornillo. tooset Hola franja temporal para hello restantes entradas en la página de hello, usar los vínculos de Hola de hello **ventana** columna.
* **Estadísticas de entrada** (solo tornillo): utilizados por el rayo Hola de flujos de entrada de información acerca de Hola.
* **Estadísticas de salida**: información sobre los flujos de hello emitidos por esta apetezca charlar o el tornillo.
* **Ejecutor**: información sobre instancias de Hola de pitorro Hola o rayo. Seleccione hello **puerto** entrada para un tooview ejecutor específico un registro de información de diagnóstico generados para esta instancia.
* **Errores**: cualquier información de error de este spout o bolt.

## <a name="monitor-and-manage-rest-api"></a>Supervisión y administración: API de REST

Hola aluvión de interfaz de usuario se basa en hello API de REST, para que pueda realizar la administración y funcionalidad de supervisión mediante el uso de API de REST de hello similares. Puede usar herramientas personalizadas de toocreate de API de REST de Hola para administrar y supervisar las topologías de Storm.

Para más información, vea la [API de REST de la IU de Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html). Hello siguiente información es específica toousing hello API de REST con Apache Storm en HDInsight.

> [!IMPORTANT]
> Hola aluvión de API de REST no esté disponible públicamente en internet de Hola y debe tener acceso utilizando un SSH túnel toohello HDInsight nodo principal del clúster. Para obtener información sobre cómo crear y usar un túnel SSH, consulte [tooaccess uso de SSH túnel Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie y otras interfaces de usuario web](hdinsight-linux-ambari-ssh-tunnel.md).

### <a name="base-uri"></a>URI base

Hello URI base para la API de REST de hello en clústeres de HDInsight basados en Linux está disponible en el nodo principal de hello en **https://HEADNODEFQDN:8744/api/v1/**. nombre de dominio de Hello del nodo principal de Hola se genera durante la creación del clúster y no es estático.

Puede encontrar el nombre de dominio completo (FQDN) de hello para el nodo principal del clúster Hola de varias maneras diferentes:

* **Desde una sesión de SSH**: Use el comando de hello `headnode -f` desde un clúster de toohello de sesión SSH.
* **Desde Ambari Web**: seleccione **servicios** desde la parte superior de la página de Hola Hola, a continuación, seleccione **Storm**. De hello **resumen** ficha, seleccione **aluvión de interfaz de usuario de servidor**. Hola FQDN del nodo de Hola que está ejecutando Hola aluvión de interfaz de usuario y la API de REST está al principio de Hola de página de Hola.
* **A través de API de REST de Ambari**: Use el comando de hello `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve información sobre el nodo Hola Hola aluvión de interfaz de usuario y la API de REST se ejecutan en. Reemplace **contraseña** con la contraseña de administrador de hello para el clúster de Hola. Reemplace **CLUSTERNAME** con el nombre del clúster de Hola. En la respuesta de hello, entrada de "host_name" hello contiene Hola FQDN del nodo de Hola.

### <a name="authentication"></a>Autenticación

Toohello de las solicitudes que se debe usar la API de REST **la autenticación básica**, por lo que usar el nombre del Administrador de clúster de HDInsight de hello y una contraseña.

> [!NOTE]
> Dado que la autenticación básica se envía mediante el uso de texto no cifrado, debe **siempre** utilizar comunicaciones HTTPS a toosecure con clúster de Hola.

### <a name="return-values"></a>Valores devueltos

Información que se devuelve de hello API de REST solo pueden ser utilizable desde dentro de clúster de Hola o máquinas virtuales en Hola misma red Virtual de Azure como clúster de Hola. Por ejemplo, devuelve para servidores de Zookeeper de nombre de dominio completo hello (FQDN) no es ser accesible desde Internet Hola.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo topologías toodeploy y monitor mediante el uso de Hola aluvión de panel, obtenga información acerca de cómo demasiado[topologías de basados en Java desarrollar con Maven](hdinsight-storm-develop-java-topology.md).

Para obtener una lista con más topologías de ejemplo, consulte [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).
