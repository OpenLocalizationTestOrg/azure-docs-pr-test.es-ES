---
title: "aaaDeploy y administrar topologías de Apache Storm en HDInsight | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy, supervisar y administrar topologías de Apache Storm con hello aluvión de panel en HDInsight. Utilice herramientas de Hadoop para Visual Studio"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>Implementación y administración de topologías de Apache Storm en HDInsight basado en Windows

Hola aluvión de panel permite tooeasily implementar y ejecutar el clúster de HDInsight de Apache Storm topologías tooyour utilizando el explorador web. También puede utilizar Hola panel toomonitor y administrar topologías de ejecución. Si utiliza Visual Studio, hello HDInsight Tools para Visual Studio proporciona características similares en Visual Studio.

Hola aluvión de panel y las características de Storm Hola Hola HDInsight Tools dependen de hello API de REST de Storm, que puede ser usado toocreate sus propias soluciones de supervisión y administración.

> [!IMPORTANT]
> pasos de Hello en este documento, es necesario un aluvión de clúster de HDInsight que usa Windows como sistema operativo de Hola. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Para más información sobre la implementación y la administración de topologías de Storm con un clúster de HDInsight que usa Linux, consulte [Implementación y administración de topologías de Apache Storm en HDInsight basado en Linux](hdinsight-storm-deploy-monitor-topology-linux.md).

## <a name="prerequisites"></a>Requisitos previos

* **Apache Storm en HDInsight**: consulte [Introducción a Apache Storm en HDInsight](hdinsight-apache-storm-tutorial-get-started.md) para conocer los pasos para la creación de un clúster.

* Para hello **aluvión de panel**: un explorador web moderna que es compatible con HTML5.

* Para **Visual Studio** -Azure SDK 2.5.1 o versiones más recientes y Hola HDInsight Tools para Visual Studio. Vea [Introducción al uso de herramientas de HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall y configurar las herramientas de HDInsight de Hola para Visual Studio.

    Uno de hello después de versiones de Visual Studio:

  * Visual Studio 2012 con la actualización 4

  * Visual Studio 2013 con la actualización 4 o Visual Studio Community 2013

  * Visual Studio 2015 (cualquier edición)

  * Visual Studio 2017 (cualquier edición)

## <a name="storm-dashboard"></a>panel de Storm

Hola aluvión de panel es una página web disponibles en el clúster de Storm. dirección URL de Hello es **https://&lt;clustername >.azurehdinsight.net/**, donde **clustername** es Hola nombre de su Storm en clúster de HDInsight.

De arriba Hola de hello aluvión de panel, seleccione **topología enviar**. Siga las instrucciones de hello en hello página toorun una topología de ejemplo o tooupload y ejecute una topología que ha creado.

![Hola Enviar página topología][storm-dashboard-submit]

### <a name="storm-ui"></a>UI de Storm

En hello aluvión de panel, seleccione hello **aluvión de interfaz de usuario** vínculo. Esto muestra información sobre el clúster hello, en tooany adición ejecutando topologías.

![interfaz de usuario de Hello storm][storm-dashboard-ui]

> [!NOTE]
> Con algunas versiones de Internet Explorer, es posible que descubra que Hola que aluvión de interfaz de usuario no se actualiza después de que ha visitado en primer lugar. Por ejemplo, no puede mostrar nuevas topologías de Hola que ha enviado o puede mostrar una topología como activo cuando se desactivado anteriormente. Microsoft conoce este problema y está trabajando para conseguir una solución.

#### <a name="main-page"></a>Página principal

página principal de Hola de hello aluvión de interfaz de usuario proporciona Hola siguiente información:

* **Resumen de clúster**: información básica sobre el clúster de Storm Hola.

* **Resumen de las topologías**: una lista de las topologías en ejecución. Usar vínculos de hello en esta sección tooview obtener más información acerca de las topologías específicas.

* **Resumen de supervisor**: obtener información sobre el supervisor de Storm Hola.

* **Configuración de Nimbus**: configuración de Nimbus para clúster Hola.

#### <a name="topology-summary"></a>Resumen de las topologías

Si selecciona un vínculo de hello **resumen de la topología** sección muestra hello después de obtener información acerca de la topología de hello:

* **Resumen de la topología**: información básica acerca de la topología de Hola.

* **Acciones de topología**: acciones de administración que puede realizar para la topología de Hola.

  * **Activar**: reanuda el procesamiento de una topología desactivada.

  * **Desactivar**: pausa una topología en ejecución.

  * **Reequilibrar**: ajusta el paralelismo de Hola de topología de Hola. Debe volver a equilibrar las topologías de ejecución después de que haya cambiado Hola número de nodos de clúster de Hola. Esto permite Hola topología tooadjust paralelismo toocompensate para hello aumenta o reduce el número de nodos de clúster de Hola.

      Para obtener más información, consulte [descripción paralelismo Hola de una topología de Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

  * **Kill**: termine una topología de Storm después Hola especifica el tiempo de espera.

* **Estadísticas de topología**: estadísticas acerca de la topología de Hola. Use los vínculos de Hola Hola **ventana** período de tiempo de columna tooset Hola para hello restantes entradas en la página de Hola.

* **Spouts**: Hola spouts utilizados por la topología de Hola. Usar vínculos de hello en esta sección tooview obtener más información sobre spouts específicos.

* **Tornillos**: Hola tornillos utilizados por la topología de Hola. Usar vínculos de hello en esta sección tooview obtener más información acerca de los tornillos específicos.

* **Configuración de la topología**: configuración de Hola de topología de hello seleccionado.

#### <a name="spout-and-bolt-summary"></a>Resumen de spouts y bolts

Seleccionar un pitorro de hello **Spouts** o **tornillos** secciones muestra hello después de obtener información sobre el elemento Hola seleccionado:

* **Resumen de componentes**: información básica sobre pitorro Hola o rayo.

* **Estadísticas de pitorro/rayo**: estadísticas sobre Hola apetezca charlar o el tornillo. Use los vínculos de Hola Hola **ventana** período de tiempo de columna tooset Hola para hello restantes entradas en la página de Hola.

* **Estadísticas de entrada** (solo tornillo): utilizados por el rayo Hola de flujos de entrada de información acerca de Hola.

* **Estadísticas de salida**: información sobre los flujos de hello emitidos por esta apetezca charlar o el tornillo.

* **Ejecutor**: información sobre instancias de Hola de pitorro Hola o rayo. Seleccione hello **puerto** entrada para un tooview ejecutor específico un registro de información de diagnóstico generados para esta instancia.

* **Errores**: cualquier información de error de este spout o bolt.

## <a name="hdinsight-tools-for-visual-studio"></a>Herramientas de HDInsight para Visual Studio

Herramientas de HDInsight de Hello puede ser toosubmit usa C# o híbrida topologías tooyour clúster de Storm. Hola pasos usa una aplicación de ejemplo. Para obtener información acerca de cómo crear sus propios topologías mediante las herramientas de HDInsight de hello, consulte [C# desarrollar topologías con hello HDInsight Tools para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Usar hello siguiendo los pasos toodeploy una tormenta de ejemplo tooyour en clúster de HDInsight, a continuación, ver y administrar la topología de Hola.

1. Si no ha instalado ya Hola versión más reciente de hello HDInsight Tools para Visual Studio, consulte [Introducción al uso de herramientas de HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Abra Visual Studio, seleccione **Archivo** > **Nuevo** > **Proyecto**.

3. Hola **nuevo proyecto** cuadro de diálogo, expanda **instalado** > **plantillas**y, a continuación, seleccione **HDInsight**. En la lista Hola de plantillas, seleccione **aluvión de ejemplo**. En parte inferior de Hola Hola del cuadro de diálogo, escriba un nombre para la aplicación hello.

    ![imagen](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **enviar tooStorm en HDInsight**.

   > [!NOTE]
   > Si se le solicite, escriba las credenciales de inicio de sesión de hello para la suscripción de Azure. Si tiene más de una suscripción, inicie sesión en toohello uno que contiene el aluvión en clúster de HDInsight.

5. Seleccione el aluvión en clúster de HDInsight de hello **clúster de Storm** lista desplegable y, a continuación, seleccione **enviar**. Puede supervisar si el envío de hello es correcto mediante hello **salida** ventana.

6. Cuando se ha enviado correctamente la topología de hello, Hola **aluvión de topologías** para clúster Hola debería aparecer. Seleccione topología Hola de hello mostrar tooview información acerca de hello ejecutando topología.

    ![supervisión de visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > También puede ver las **topologías de Storm** en el **Explorador de servidores** expandiendo **Azure** > **HDInsight** y, después, haciendo clic con el botón derecho en un clúster de Storm en HDInsight y seleccionando **View Storm Topologies** (Ver topologías de Storm).

    Seleccione la forma de Hola Hola spouts o tornillos tooview información acerca de estos componentes. Se abrirá una ventana nueva para cada elemento seleccionado.

   > [!NOTE]
   > nombre de Hola de topología de hello es el nombre de clase de Hola de topología de hello (en este caso, `HelloWord`,) con una marca de tiempo que se anexa.

7. De hello **resumen de la topología** visualizarla, seleccione **Kill** topología de hello toostop.

   > [!NOTE]
   > Topologías de Storm continúan ejecutándose hasta que se hayan detenido o se elimina el clúster de Hola.


## <a name="rest-api"></a>API de REST

Hola aluvión de interfaz de usuario se basa en hello API de REST, para que pueda realizar la administración y funcionalidad de supervisión mediante el uso de API de REST de hello similares. Puede usar herramientas personalizadas de toocreate de API de REST de Hola para administrar y supervisar las topologías de Storm.

Para más información, vea la [API de REST de la IU de Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md). Hello siguiente información es específica toousing hello API de REST con Apache Storm en HDInsight.

### <a name="base-uri"></a>URI base

Hola URI base para la API de REST de hello en clústeres de HDInsight es **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, donde **clustername** es el nombre de Hola de su Storm en Clúster de HDInsight.

### <a name="authentication"></a>Autenticación

Toohello de las solicitudes que se debe usar la API de REST **la autenticación básica**, por lo que usar el nombre del Administrador de clúster de HDInsight de hello y una contraseña.

> [!NOTE]
> Dado que la autenticación básica se envía mediante el uso de texto no cifrado, debe **siempre** utilizar comunicaciones HTTPS a toosecure con clúster de Hola.

### <a name="return-values"></a>Valores devueltos

Información que se devuelve de hello API de REST solo pueden ser utilizable desde dentro de clúster de Hola o máquinas virtuales en Hola misma red Virtual de Azure como clúster de Hola. Por ejemplo, nombre de dominio completo de hello (FQDN) devuelto para los servidores de Zookeeper no se pueden accesible desde Internet Hola.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo topologías toodeploy y monitor mediante el uso de Hola aluvión de panel, obtenga información acerca de cómo:

* [Desarrollar las topologías de C# con hello HDInsight Tools para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [Desarrollar topologías basadas en Java con Maven](hdinsight-storm-develop-java-topology.md)

Para obtener una lista con más topologías de ejemplo, consulte [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
