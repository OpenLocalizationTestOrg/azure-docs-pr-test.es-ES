---
title: "clústeres de Hadoop de aaaCreate mediante un explorador web - HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate Hadoop, HBase, tormenta o Spark clusters en Linux para HDInsight mediante un explorador web y Hola portal de vista previa."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a>Crear clústeres basados en Linux en HDInsight con hello portal de Azure
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Hola portal de Azure es una herramienta de administración basada en web para los servicios y recursos hospedados en la nube de Microsoft Azure Hola. En este artículo, aprenderá cómo toocreate HDInsight basados en Linux clústeres mediante el portal de Hola.

## <a name="prerequisites"></a>Requisitos previos
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Un explorador web moderno**. Hola portal de Azure usa HTML5 y Javascript y puede no funcionar correctamente en los exploradores más antiguos.

## <a name="create-clusters"></a>Creación de clústeres
Hola portal de Azure expone la mayor parte de las propiedades de clúster de Hola. Mediante la plantilla de Azure Resource Manager puede ocultar una gran cantidad de detalles. Para más información, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight con plantillas de Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **+**, en **Intelligence + analytics** y después en **HDInsight**.
   
    ![Crear un nuevo clúster en el portal de Azure hello](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "crear un nuevo clúster en hello portal de Azure")

3. Hola **HDInsight** hoja, haga clic en **personalizado (tamaño, configuración, aplicaciones)**, haga clic en **Fundamentos**y, a continuación, escriba Hola siguiente información.

    ![Crear un nuevo clúster en el portal de Azure hello](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "crear un nuevo clúster en hello portal de Azure")

    * Especifique el **nombre del clúster**: dicho nombre debe ser único globalmente.

    * De hello **suscripción** Hola de lista desplegable, seleccione suscripción de Azure que se usará para el clúster de Hola.

    * Haga clic en **Tipo de clúster** y luego seleccione:
   
        * **Tipo de clúster**: si no sabe qué toochoose, seleccione **Hadoop**. Es del tipo de clúster más popular de Hola.
     
            > [!IMPORTANT]
            > HDInsight clústeres vienen en una variedad de tipos, que corresponden a cargas de trabajo de toohello o tecnología de Hola clúster se optimiza para. No hay ningún toocreate método admitido para un clúster que combina varios tipos, como Storm y HBase en un clúster. 
            > 
            > 
        
        * **Sistema operativo**: seleccione **Linux**.
        
        * **Versión**: usar la versión predeterminada de hello si no sabe qué toochoose. Para obtener más información, consulte [Versiones de clústeres de HDInsight](hdinsight-component-versioning.md).
        * **Nivel de clúster**: HDInsight de Azure proporciona las ofertas de nube de hello grandes cantidades de datos en dos categorías: nivel estándar y nivel Premium. Para más información, consulte [Niveles de clúster](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).

    * Para **nombre de usuario de inicio de sesión de clúster** y **contraseña de inicio de sesión de clúster**, proporcionar Hola nombre de usuario y la contraseña de usuario de administrador de Hola.

    * Escriba un **nombre de usuario SSH** y si desea toohave Hola SSH contraseña igual Hola contraseña de administrador que especificó anteriormente, seleccione hello **usar la misma contraseña como inicio de sesión de clúster** casilla de verificación. Si no es así, proporcionar un **contraseña** o **clave pública**, que va a ser usuario SSH de hello tooauthenticate usado. El uso de una clave pública es Hola enfoque recomendado. Haga clic en **seleccione** en la configuración de credenciales de hello inferior toosave Hola.
   
        Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

    * Para **grupo de recursos**, especifique si desea toocreate un nuevo grupo de recursos o utilizar uno existente.

    * Especifique un centro de datos **ubicación** donde se creará el clúster de Hola.

    * Haga clic en **Siguiente**.

4. En hello **almacenamiento** hoja, especifique si desea que almacenamiento de Azure (WASB) o almacén de Data Lake como el almacenamiento de forma predeterminada. Buscar en la tabla de Hola a continuación para obtener más información.

    ![Crear un nuevo clúster en el portal de Azure hello](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "crear un nuevo clúster en hello portal de Azure")

    | Storage                                      | Descripción |
    |----------------------------------------------|-------------|
    | **Blobs de Azure Storage como almacenamiento predeterminado**   | <ul><li>En **Tipo de almacenamiento principal**, seleccione **Azure Storage**. Después de eso, para **método de selección**, puede elegir **Mis suscripciones** si desea toospecify una cuenta de almacenamiento que forma parte de su suscripción de Azure y cuenta de almacenamiento, a continuación, seleccione Hola. En caso contrario, haga clic en **clave de acceso** y proporcionar información de Hola Hola cuenta de almacenamiento que desea toochoose desde fuera de su suscripción de Azure.</li><li>Para **contenedor predeterminado**, puede elegir toogo con nombre del contenedor predeterminado Hola sugerido por el portal de Hola o especificar la suya propia.</li><li>Si usas WASB como almacenamiento predeterminado, puede hacer clic (opcionalmente) **cuentas de almacenamiento adicionales** cuentas de almacenamiento adicional de toospecify tooassociate con clúster de Hola. Hola **las claves de almacenamiento de Azure** hoja, haga clic en **agregar una clave de almacenamiento**, y, a continuación, puede proporcionar una cuenta de almacenamiento de las suscripciones de Azure o de otras suscripciones (no proporcionando cuenta de almacenamiento de Hola clave de acceso).</li><li>Si usas WASB como almacenamiento predeterminado, puede hacer clic (opcionalmente) **acceso de almacén de Data Lake** toospecify almacén de Data Lake de Azure como almacenamiento adicional. Para más información, vea [Creación de un clúster de HDInsight con Data Lake Store mediante Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</li></ul> |
    | **Azure Data Lake Store como almacenamiento predeterminado** | Para **tipo de almacenamiento principal**, seleccione **almacén de Data Lake** y, a continuación, consulte el artículo de toohello [crear un clúster de HDInsight con el almacén de Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) para instrucciones. |
    | **Tiendas de metadatos externas**                      | Si lo desea, puede especificar una base de datos toosave Hive y Oozie los metadatos de SQL asociados con el clúster de Hola. Para **seleccionar una base de datos SQL para Hive** seleccione una base de datos SQL y, a continuación, proporcionar Hola nombre de usuario/contraseña para la base de datos de Hola. Repita estos pasos para los metadatos de Oozie.<br><br>Algunas consideraciones al usar Azure SQL Database para las tiendas de metadatos. <ul><li>base de datos de SQL Azure de Hello utilizada de metadatos de hello debe permitir tooother de conectividad de servicios de Azure, incluidos HDInsight de Azure. En el panel de base de datos de SQL Azure hello, en el lado derecho de hello, haga clic en el nombre del servidor de Hola. Se trata de un servidor hello en qué Hola SQL se ejecuta la instancia de base de datos. Una vez que se encuentra en la vista de servidor hello, haga clic en **configurar**y, a continuación, para **servicios de Azure**, haga clic en **Sí**y, a continuación, haga clic en **guardar**.</li><li>Al crear una tienda de metadatos, no utilice un nombre de base de datos que contiene guiones o guiones, ya que esto puede provocar toofail de proceso de creación de clúster de Hola.</li></ul>                                                                                                                                                                       |

    Haga clic en **Siguiente**. 

    > [!WARNING]
    > No se admite con una cuenta de almacenamiento adicional en una ubicación diferente que el clúster de HDInsight Hola.

5. Si lo desea, haga clic en **aplicaciones** tooinstall las aplicaciones que funcionan con clústeres de HDInsight. Estas aplicaciones puede desarrollarlas Microsoft, fabricantes de software independientes (ISV) o el propio usuario. Para más información, consulte [Instalación de aplicaciones de HDInsight](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).


6. Haga clic en **tamaño de clúster** toodisplay información acerca de los nodos de Hola que va a crear para este clúster. Establecer número de Hola de nodos de trabajador que necesite para el clúster de Hola. Hola se calcula el costo de clúster de Hola se mostrará en la hoja de Hola.
   
    ![Hoja de planes de tarifa de nodos](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "Especificación del número de nodos del clúster")
   
   > [!IMPORTANT]
   > Si tiene previsto en más de 32 nodos de trabajo, en la creación del clúster, o mediante el ajuste de escala en clúster de hello después de su creación, debe seleccionar un tamaño de nodo principal con un mínimo de 8 núcleos y 14GB de ram.
   > 
   > Para obtener más información acerca de los tamaños de nodo y los costos asociados, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   > 
   > 
   
   Haga clic en **siguiente** nodo de hello toosave configuración de precios.

7. Haga clic en **configuración avanzada** tooconfigure otros valores de configuración opcionales, como el uso de **acciones de Script** toocustomize tooinstall de un clúster componentes personalizados o unirse a un **deredVirtual**. Buscar en la tabla de Hola a continuación para obtener más información.

    ![Hoja de planes de tarifa de nodos](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "Especificación del número de nodos del clúster")

    | Opción | Descripción |
    |--------|-------------|
    | **Acciones de script** | Utilice esta opción si desea toouse una toocustomize de secuencia de comandos personalizada un clúster, tal y como se va a crear el clúster de Hola. Para obtener más información sobre acciones de script, vea [Personalización de clústeres de HDInsight con una acción de script](hdinsight-hadoop-customize-cluster-linux.md). |
    | **Virtual Network** | Seleccione una subred de hello y red virtual Azure si desea que el clúster de hello tooplace en una red virtual. Para obtener información sobre el uso de HDInsight con una red Virtual, incluidos los requisitos de configuración específicos de hello red Virtual, vea [capacidades de HDInsight extender mediante el uso de una red Virtual de Azure](hdinsight-extend-hadoop-virtual-network.md). |

    Haga clic en **Siguiente**.

8. En hello **resumen** hoja, compruebe la información de Hola que escribió anteriormente y, a continuación, haga clic en **crear**.

    ![Hoja de planes de tarifa de nodos](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "Especificación del número de nodos del clúster")
    
    > [!NOTE]
    > Se tardará algún tiempo Hola clúster toobe creado, normalmente unos 15 minutos. Usar icono hello en el panel de inicio de Hola u Hola **notificaciones** entrada en hello encendidos de hello página toocheck Hola proceso de aprovisionamiento.
    > 
    > 
12. Una vez completado el proceso de creación de hello, haga clic en icono de Hola de clúster de Hola desde la hoja de clúster de hello panel de inicio toolaunch Hola. hoja de clúster de Hello proporciona Hola siguiente información.
    
    ![Hoja de clúster](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "Propiedades del clúster")
    
    Usar hello después toounderstand iconos de hello en parte superior de Hola de esta hoja.
    
    * **Información general sobre** ficha proporciona toda la información esencial Hola sobre clúster hello como nombre de hello, grupo de recursos de hello pertenece a ubicación hello, sistema operativo de hello, dirección URL de panel de clúster de hello, etcetera.
    * **Panel** dirige toohello Ambari portal asociado con el clúster de Hola.
    * **Secure Shell**: información necesaria de clúster de hello tooaccess mediante SSH.
    * **Clúster de escala** permite aumentar el número Hola de nodos de trabajo asociado con el clúster de Hola.
    * **Eliminar**: clúster de HDInsight de Hola de eliminaciones.
    

## <a name="customize-clusters"></a>Personalización de los clústeres
* Consulte [Personalización de los clústeres de HDInsight con Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).
* Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Eliminar el clúster de Hola
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Solución de problemas

Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha creado correctamente un clúster de HDInsight, usar hello sigue toolearn cómo toowork con el clúster:

### <a name="hadoop-clusters"></a>Clústeres Hadoop
* [Uso de Hive con HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Clústeres HBase
* [Introducción a HBase en HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Desarrollo de aplicaciones de Java para HBase en HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Clústeres Storm
* [Desarrollo de topologías de Java para Storm en HDInsight](hdinsight-storm-develop-java-topology.md)
* [Uso de componentes de Python en Storm en HDInsight](hdinsight-storm-develop-python-topology.md)
* [Implementación y supervisión de topologías con Storm en HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Clústeres de Spark
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)

