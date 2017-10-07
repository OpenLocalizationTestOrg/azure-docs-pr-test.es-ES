---
title: "clústeres de Hadoop basado en Windows de aaaManage en HDInsight utilizando Hola portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadminister HDInsight Service. Crear un clúster de HDInsight, la consola de JavaScript interactivo Hola abierto y la consola de comandos de Hadoop de hello abierto."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Administrar clústeres basados en Windows Hadoop en HDInsight con hello portal de Azure

Con hello [portal de Azure][azure-portal], puede crear clústeres basados en Windows Hadoop en HDInsight de Azure, cambiar la contraseña de usuario de Hadoop y habilitar el protocolo de escritorio remoto (RDP) para que pueda acceder Hola Hadoop consola de comandos en el clúster de Hola.

información de Hello en este artículo solo aplica a clústeres de HDInsight basados en tooWindow. Para obtener información acerca de cómo administrar clústeres basados en Linux, consulte [Hadoop administrar clústeres de HDInsight mediante el uso de Hola portal de Azure](hdinsight-administer-use-portal-linux.md).

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar este artículo, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Cuenta de almacenamiento de Azure** -HDInsight un clúster usa un contenedor de almacenamiento de blobs de Azure como sistema de archivos predeterminado de Hola. Para obtener más información acerca de cómo el almacenamiento de blobs de Azure ofrece una experiencia perfecta con los clústeres de HDInsight, consulte [Uso del almacenamiento de blobs de Azure con HDInsight](hdinsight-hadoop-use-blob-storage.md). Para obtener más información acerca de cómo crear una cuenta de almacenamiento de Azure, consulte [cómo tooCreate una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md).

## <a name="open-hello-portal"></a>Abra Hola Portal
1. Inicie sesión en demasiado[https://portal.azure.com](https://portal.azure.com).
2. Después de abrir el portal de hello, hacer lo siguiente:

   * Haga clic en **New** de hello menú izquierdo toocreate un nuevo clúster:

       ![botón nuevo clúster de HDInsight](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * Haga clic en **clústeres de HDInsight** desde el menú de la izquierda Hola.

       ![Portal de Azure botón clúster de HDInsight](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     Si **HDInsight** no aparece en el menú izquierdo hello, haga clic en **examinar**.

     ![Botón Examinar clúster de Azure Portal](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a>Creación de clústeres
Para obtener instrucciones de creación de hello mediante Hola Portal, consulte [HDInsight crear clústeres](hdinsight-hadoop-provision-linux-clusters.md).

HDInsight trabaja con una amplia gama de componentes de Hadoop. Para hello lista de componentes de Hola que se han comprobado y compatibles, consulte [es la versión de Hadoop en HDInsight de Azure](hdinsight-component-versioning.md). Puede personalizar HDInsight mediante una de las siguientes opciones de hello:

* Use acción de secuencia de comandos toorun scripts personalizados que pueden personalizar un clúster tooeither cambiar la configuración del clúster o instalación componentes personalizados, como Giraph o Solr. Para obtener más información, consulte [Personalización de un clúster de HDInsight mediante la acción de script](hdinsight-hadoop-customize-cluster.md).
* Usar parámetros de personalización de clúster de hello en hello HDInsight .NET SDK o Azure PowerShell durante la creación del clúster. Estos cambios de configuración, a continuación, se conservan a través de la duración de Hola de clúster de hello y no se ven afectados por reimages de nodo de clúster que plataforma Windows Azure se realiza periódicamente de mantenimiento. Para obtener más información sobre el uso de parámetros de personalización de clúster de hello, consulte [HDInsight crear clústeres](hdinsight-hadoop-provision-linux-clusters.md).
* Algunos componentes de Java nativo, como Mahout y en cascada, se pueden ejecutar en el clúster de hello como archivos JAR. Estos archivos JAR pueden ser distribuida tooAzure almacenamiento de blobs y los envían tooHDInsight clústeres a través de mecanismos de envío de trabajos de Hadoop. Para obtener más información, consulte [Envío de trabajos de Hadoop mediante programación](hdinsight-submit-hadoop-jobs-programmatically.md).

  > [!NOTE]
  > Si tiene problemas de implementación de clústeres de tooHDInsight archivos JAR o llamar a archivos JAR en clústeres de HDInsight, póngase en contacto con [Microsoft Support](https://azure.microsoft.com/support/options/).
  >
  > La presentación en cascada no se admite en HDInsight, y no puede optar a recibir soporte técnico de Microsoft. Para obtener listas de componentes compatibles, vea [cuáles son las novedades en las versiones de clúster Hola proporcionadas por HDInsight](hdinsight-component-versioning.md).
  >
  >

No se admite la instalación de software personalizado en clúster de hello mediante conexión a Escritorio remoto. No se deben almacenar los archivos en unidades de hello del nodo principal de hello, tal y como se perderán si necesita toore-crear clústeres de Hola. Recomendamos almacenar los archivos en el almacenamiento de blobs de Azure. El almacenamiento de blobs es persistente.

## <a name="list-and-show-clusters"></a>Enumeración y visualización de clústeres
1. Inicie sesión en demasiado[https://portal.azure.com](https://portal.azure.com).
2. Haga clic en **clústeres de HDInsight** desde el menú de la izquierda Hola.
3. Haga clic en el nombre del clúster de Hola. Si la lista de clústeres de hello es larga, puede utilizar el filtro en la parte superior de Hola de página Hola.
4. Haga doble clic en un clúster de detalles de hello lista tooshow Hola.

    **Menú y operaciones básicas**:

    ![Azure Portal: aspectos básicos del clúster de HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * menú de hello toocustomize, haga doble clic en cualquier lugar en el menú de hello y, a continuación, haga clic en **personalizar**.
   * **Configuración de** y **toda la configuración de**: Hola muestra **configuración** hoja para clúster de hello, que le permite tooaccess detallada información de configuración de clúster de Hola.
   * **Panel**, **panel clúster** y **dirección URL: estas son todas las formas tooaccess Hola panel clúster, que es Ambari Web para clústeres basados en Linux. -**Secure Shell **: Muestra hello instrucciones tooconnect toohello clúster con conexión de Secure Shell (SSH).
   * **Escalar Cluster**: permite el número de hello toochange de nodos de trabajador para este clúster.
   * **Eliminar**: clúster de Hola de eliminaciones.
   * **Inicio rápido**: muestra información que le ayudará a empezar a usar HDInsight.
   * **: Le permite tooset permisos para *portal administración* de este clúster para otros usuarios en su suscripción de Azure.

     > [!IMPORTANT]
     > Esto *sólo* afecta al acceso y permisos clúster toothis Hola portal de Azure, y no tiene ningún efecto en la que puede conectar el clúster de HDInsight de toohello de tooor enviar trabajos.
     >
     >
   * **Etiquetas**: las etiquetas permiten tooset clave-valor pares toodefine una taxonomía personalizada de servicios en la nube. Por ejemplo, puede crear una clave denominada **proyecto**y luego usar un valor común para todos los servicios asociados a un proyecto específico.
   * **Vistas de Ambari**: vincula tooAmbari Web.

     > [!IMPORTANT]
     > Servicios de hello toomanage proporcionan por hello clúster de HDInsight, se debe usar Ambari Web u Hola API de REST de Ambari. Para obtener más información sobre el uso de Ambari, consulte [Administración de clústeres de HDInsight con Ambari](hdinsight-hadoop-manage-ambari.md).
     >
     >

     **Uso**

     ![Uso del clúster de HDInsight en Azure Portal](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. Haga clic en **Configuración**.

    ![Uso del clúster de HDInsight en Azure Portal](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * **Propiedades**: ver las propiedades del clúster Hola.
   * **Identidad AAD de clúster**:
   * **Las claves de almacenamiento Azure**: ver la cuenta de almacenamiento predeterminada de Hola y su clave. cuenta de almacenamiento de Hello es configuración durante el proceso de creación de clúster de Hola.
   * **Inicio de sesión del clúster**: cambiar el nombre de usuario del clúster HTTP de Hola y la contraseña.
   * **Las tiendas de metadatos externos**: ver las tiendas de metadatos de Hive y Oozie de Hola. las tiendas de metadatos de Hello solo pueden configurarse durante el proceso de creación de clúster de Hola.
   * **Escalar Cluster**: aumento y reducción Hola número de nodos de trabajador del clúster.
   * **Escritorio remoto**: habilitar y deshabilitar el acceso de escritorio remoto (RDP) y configurar el nombre de usuario de hello RDP.  nombre de usuario RDP Hola debe ser distinto del nombre de usuario HTTP de Hola.
   * **Socio de registro**:

     > [!NOTE]
     > Se trata de una lista genérica de opciones de configuración disponibles; no todas ellas estarán presentes en todos los tipos de clúster.
     >
     >
6. Haga clic en **Propiedades**.

    sección de propiedades de Hello muestra siguiente de hello:

   * **Nombre del clúster**: nombre del clúster.
   * **Dirección URL del clúster**.
   * **Estado**: puede ser Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Región**: ubicación de Azure. Para obtener una lista de ubicaciones de Azure compatibles, vea hello **región** cuadro de lista desplegable en [precios HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Datos creados**.
   * **Sistema operativo**: **Windows** o **Linux**.
   * **Tipo**: Hadoop, HBase, Storm, Spark.
   * **Versión**. Consulte [Versiones de HDInsight](hdinsight-component-versioning.md)
   * **Suscripción**: nombre de la suscripción.
   * **Id. de suscripción**.
   * **Origen de datos principal**. Hola cuenta de almacenamiento Blob de Azure usa como valor predeterminado de hello sistema de archivos Hadoop.
   * **Plan de tarifa de los nodos de trabajo**.
   * **Plan de tarifa de los nodos de Head**.

## <a name="delete-clusters"></a>Eliminación de clústeres
Eliminar un clúster no elimina cuenta de almacenamiento predeterminada de Hola o las cuentas de almacenamiento vinculadas. Puede volver a crear el clúster de hello mediante el uso de hello las mismas cuentas de almacenamiento y hello las tiendas de metadatos mismo.

1. Inicie sesión en toohello [Portal][azure-portal].
2. Haga clic en **examinar todos los** Hola menú izquierdo, haga clic en **clústeres de HDInsight**, haga clic en el nombre del clúster.
3. Haga clic en **eliminar** desde el menú superior de hello y, a continuación, siga las instrucciones de Hola.

Vea también [Pausa o apagado de clústeres](#pauseshut-down-clusters).

## <a name="scale-clusters"></a>Escalado de clústeres
característica de ajuste de escala de clúster de Hola permite toochange número de Hola de nodos de trabajador usado por un clúster que se ejecuta en HDInsight de Azure sin necesidad de toore-crear clúster Hola.

> [!NOTE]
> Solo son compatibles los clústeres con la versión 3.1.3 de HDInsight, o superior. Si no está seguro de la versión de Hola del clúster, puede comprobar la página de propiedades de Hola.  Consulte [Enumeración y visualización de clústeres](#list-and-show-clusters).
>
>

impacto de Hola de cambiar el número de Hola de nodos de datos para cada tipo de clúster compatible con HDInsight:

* Hadoop

    Perfectamente puede aumentar el número de Hola de nodos de trabajador en un clúster de Hadoop que se ejecuta sin afectar a los trabajos pendientes o en ejecución. También se pueden enviar trabajos nuevos mientras Hola operación está en curso. Errores en una operación de ajuste de escala se controlan correctamente para que hello clúster siempre se deja en un estado funcional.

    Cuando un clúster de Hadoop es reducido reduciendo el número de Hola de nodos de datos, algunos de los servicios de hello en clúster de Hola se reinician. Esto hace que ejecutan todos y pendiente de trabajos toofail al término de Hola Hola la operación de escalado. Sin embargo, puede volver a enviar trabajos de hello una vez completada la operación de Hola.
* HBase

    Sin problemas, puede agregar o quitar el clúster de HBase tooyour nodos mientras se está ejecutando. Los servidores regionales se equilibran automáticamente dentro de unos pocos minutos después de completar la operación de escalado de Hola. No obstante, puede equilibrar manualmente servidores regionales Hola iniciando sesión en el nodo principal de hello del clúster y ejecución Hola siguientes comandos de una ventana del símbolo del sistema:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Para obtener más información sobre cómo usar el shell de HBase hello, consulte]
* Storm

    Sin problemas, puede agregar o quitar el clúster de Storm de tooyour de nodos de datos mientras se está ejecutando. Sin embargo, tras finalizar correctamente la operación de escalado de hello, debe topología de hello toorebalance.

    Esto se puede realizar de dos formas:

  * La interfaz de usuario web de Storm
  * La herramienta de la interfaz de línea de comandos (CLI)

    Consulte toohello [documentación de Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obtener más detalles.

    interfaz de usuario de web de Storm Hola está disponible en el clúster de HDInsight de hello:

    ![reequilibrio de escalado de storm de HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Este es un ejemplo cómo toouse Hola CLI comando topología de Storm Hola toorebalance:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**clústeres de tooscale**

1. Inicie sesión en toohello [Portal][azure-portal].
2. Haga clic en **examinar todos los** Hola menú izquierdo, haga clic en **clústeres de HDInsight**, haga clic en el nombre del clúster.
3. Haga clic en **configuración** desde el menú superior de hello y, a continuación, haga clic en **escala clúster**.
4. Escriba el **Número de nodos de trabajo**. Hola Hola número límite de nodo de clúster varía para las suscripciones de Azure. Puede ponerse en contacto con facturación límite de hello tooincrease de soporte técnico.  información de costos de Hello reflejará los cambios de hello realizados toohello número de nodos.

    ![HDInsight Hadoop HBase Storm Spark escalar](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a>Pausa o apagado de clústeres
La mayoría de los trabajos de Hadoop son trabajos por lotes que se ejecutan sol ocasionalmente. Para la mayoría de los clústeres de Hadoop, hay períodos largos de tiempo no se utiliza ese clúster hello para el procesamiento. Con HDInsight, los datos se almacenan en Almacenamiento de Azure, por lo que puede eliminar un clúster de forma segura cuando no está en uso.
También se le cargará por un clúster de HDInsight aunque no esté en uso. Puesto que los cargos de Hola de clúster de hello son muchas veces más que los cargos de hello para el almacenamiento, conviene económico toodelete clústeres cuando no están en uso.

Hay muchas maneras se puede programar el proceso de hello:

* Usar Factoría de datos de Azure. Consulte [Servicios vinculados de Azure HDInsight](../data-factory/data-factory-compute-linked-services.md) y [Transformación y análisis mediante Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) para conocer los servicios vinculados de HDInsight a petición y definidos por el usuario.
* Usar Azure PowerShell.  Vea [Análisis de datos de retrasos de vuelos](hdinsight-analyze-flight-delay-data.md).
* Uso de CLI de Azure. Consulte [Administrar clústeres de HDInsight con la CLI de Azure](hdinsight-administer-use-command-line.md).
* Usar .NET SDK de HDInsight. Vea [Envío de trabajos de Hadoop](hdinsight-submit-hadoop-jobs-programmatically.md).

Para obtener información sobre precios de hello, consulte [precios HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete un clúster de hello Portal, consulte [eliminar clústeres](#delete-clusters)

## <a name="change-cluster-username"></a>Cambio del nombre de usuario del clúster
Un clúster de HDInsight puede tener dos cuentas de usuario. Hola cuenta de usuario del clúster de HDInsight se crea durante el proceso de creación de hello. También puede crear una cuenta de usuario RDP para tener acceso a cluster de Hola a través de RDP. Consulte [Habilitación de escritorio remoto](#connect-to-hdinsight-clusters-by-using-rdp).

**contraseña y nombre de usuario del clúster de HDInsight de toochange Hola**

1. Inicie sesión en toohello [Portal][azure-portal].
2. Haga clic en **examinar todos los** Hola menú izquierdo, haga clic en **clústeres de HDInsight**, haga clic en el nombre del clúster.
3. Haga clic en **configuración** desde el menú superior de hello y, a continuación, haga clic en **inicio de sesión de clúster**.
4. Si **inicio de sesión de clúster** ha sido habilitada, debe hacer clic **deshabilitar**y, a continuación, haga clic en **habilitar** antes de poder cambiar Hola username y password...
5. Hola de cambio **nombre de inicio de sesión del clúster** o hello **contraseña de inicio de sesión de clúster**y, a continuación, haga clic en **guardar**.

    ![HDInsight change cluster user username password http user](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a>Concesión o revocación del acceso
Clústeres de HDInsight tienen Hola después de servicios web HTTP (todos estos servicios tienen extremos RESTful):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

De manera predeterminada, estos servicios se conceden para el acceso. Se puede revoke y conceder acceso de Hola de hello portal de Azure.

> [!NOTE]
> Por conceder o revocar el acceso de hello, se restablecerá la contraseña y el nombre de usuario del clúster de Hola.
>
>

**acceso de los servicios web de toogrant/revoke HTTP**

1. Inicie sesión en toohello [Portal][azure-portal].
2. Haga clic en **examinar todos los** Hola menú izquierdo, haga clic en **clústeres de HDInsight**, haga clic en el nombre del clúster.
3. Haga clic en **configuración** desde el menú superior de hello y, a continuación, haga clic en **inicio de sesión de clúster**.
4. Si **inicio de sesión de clúster** ha sido habilitada, debe hacer clic **deshabilitar**y, a continuación, haga clic en **habilitar** antes de poder cambiar Hola username y password...
5. Para **nombre de usuario de inicio de sesión de clúster** y **contraseña de inicio de sesión de clúster**, escriba Hola nuevo nombre de usuario y contraseña (respectivamente) para el clúster de Hola.
6. Haga clic en **GUARDAR**.

    ![HDInsight grand remove http web service access](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a>Busque la cuenta de almacenamiento predeterminada de Hola
Cada clúster de HDInsight tiene una cuenta de almacenamiento predeterminada. Hola cuenta de almacenamiento predeterminada y sus claves para un clúster aparece en **configuración**/**propiedades**/**las claves de almacenamiento de Azure**. Consulte [Enumeración y visualización de clústeres](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Encontrar el grupo de recursos de Hola
En el modo de administrador de recursos de Azure de hello, cada clúster de HDInsight se crea con un grupo de recursos de Azure. grupo de recursos de Azure de Hola que un clúster pertenece tooappears en:

* lista de clúster de Hello tiene un **grupo de recursos** columna.
* Icono **Esencial** del clúster.  

Vea [Enumeración y visualización de clústeres](#list-and-show-clusters).

## <a name="open-hdinsight-query-console"></a>Apertura de la consola de consulta de HDInsight
Hola consola de consultas de HDInsight incluye Hola siguientes características:

* **Editor Hive**: interfaz de web de GUI para el envío de trabajos de Hive.  Vea [consultas ejecutar Hive mediante Hola consola de consultas](hdinsight-hadoop-use-hive-query-console.md).

    ![HDInsight portal hive editor](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* **Historial de trabajos**: supervise los trabajos de Hadoop.  

    ![HDInsight portal job history](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    Haga clic en **nombre de la consulta** tooshow detalles de hello incluidas las propiedades de trabajo, **consulta de trabajo**, y ** salida del trabajo. También puede descargar consulta Hola y Hola salida tooyour workstation.
* **Explorador de archivos**: examinar la cuenta de almacenamiento predeterminada de Hola y Hola cuentas de almacenamiento vinculadas.

    ![HDInsight portal file browser browse](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    En la captura de pantalla de hello, Hola  **<Account>**  tipo indica el elemento de hello es una cuenta de almacenamiento de Azure.  Haga clic en archivos hello toobrowse nombre de cuenta de hello.
* **IU de Hadoop**.

    ![HDInsight portal Hadoop UI](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    En **IU de Hadoop*puede examinar los archivos y comprobar los registros.
* **UI de Yarn**.

    ![HDInsight portal YARN UI](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a>Ejecución de consultas de Hive
trabajos de Hive tooran de hello Portal, haga clic en **Editor de Hive** en hello HDInsight consulta de la consola. Vea [Apertura de la consola de consulta de HDInsight](#open-hdinsight-query-console).

## <a name="monitor-jobs"></a>Supervisión de trabajos
trabajos de toomonitor de hello Portal, haga clic en **historial de trabajos** en hello HDInsight consulta de la consola. Vea [Apertura de la consola de consulta de HDInsight](#open-hdinsight-query-console).

## <a name="browse-files"></a>Examinar archivos
toobrowse archivos almacenados en la cuenta de almacenamiento predeterminada de Hola y Hola cuentas de almacenamiento vinculado, haga clic en **Explorador de archivos** en hello HDInsight consulta de la consola. Vea [Apertura de la consola de consulta de HDInsight](#open-hdinsight-query-console).

También puede usar hello **examinar el sistema de archivos de hello** utilidad de hello **Hadoop UI** en la consola de HDInsight Hola.  Vea [Apertura de la consola de consulta de HDInsight](#open-hdinsight-query-console).

## <a name="monitor-cluster-usage"></a>Supervisión del uso de los clústeres
Hola **uso** sección de hoja de clúster de HDInsight de hello muestra información sobre el número de Hola de suscripción de núcleos tooyour disponibles para su uso con HDInsight, así como número de Hola de núcleos asignados toothis clúster y cómo se asignar para nodos de hello en este clúster. Consulte [Enumeración y visualización de clústeres](#list-and-show-clusters).

> [!IMPORTANT]
> Servicios de hello toomonitor proporcionan por hello clúster de HDInsight, se debe usar Ambari Web u Hola API de REST de Ambari. Para obtener más información sobre el uso de Ambari, consulte [Administración de clústeres de HDInsight con Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="open-hadoop-ui"></a>Apertura de la IU de Hadoop
clúster de hello toomonitor, sistema de archivos de examinar hello y compruebe los registros, haga clic en **Hadoop UI** en hello HDInsight consulta de la consola. Vea [Apertura de la consola de consulta de HDInsight](#open-hdinsight-query-console).

## <a name="open-yarn-ui"></a>Apertura de la UI de Yarn
toouse interfaz de usuario de Yarn, haga clic en **Yarn UI** en hello HDInsight consulta de la consola. Vea [Apertura de la consola de consulta de HDInsight](#open-hdinsight-query-console).

## <a name="connect-tooclusters-using-rdp"></a>Conectar tooclusters mediante RDP
las credenciales de Hola para clúster Hola que haya especificado en su creación conceda acceso toohello servicios en clúster de hello, pero no toohello propio clúster a través de escritorio remoto. Puede activar el acceso de Escritorio remoto cuando aprovisiona un clúster o después de su aprovisionamiento. Para obtener instrucciones acerca de cómo habilitar Escritorio remoto durante la creación de hello, consulte [clúster de HDInsight crear](hdinsight-hadoop-provision-linux-clusters.md).

**tooenable escritorio remoto**

1. Inicie sesión en toohello [Portal][azure-portal].
2. Haga clic en **examinar todos los** Hola menú izquierdo, haga clic en **clústeres de HDInsight**, haga clic en el nombre del clúster.
3. Haga clic en **configuración** desde el menú superior de hello y, a continuación, haga clic en **escritorio remoto**.
4. Especifique los valores de **Expira en**, **Nombre de usuario de Escritorio remoto** y **Contraseña de Escritorio remoto** y haga clic en **Habilitar**.

    ![HDInsight habilitar deshabilitar configurar escritorio remoto](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    valores predeterminados de Hola de expiración es una semana.

   > [!NOTE]
   > También puede usar hello HDInsight .NET SDK tooenable escritorio remoto en un clúster. Hola de uso **EnableRdp** método en el objeto de cliente de HDInsight de Hola Hola después de manera: **cliente. EnableRdp (nombre del clúster, ubicación, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**. De forma similar, toodisable escritorio remoto en clúster de hello, puede usar **cliente. DisableRdp (nombre del clúster, la ubicación)**. Para obtener más información sobre estos métodos, consulte [Referencia de .NET SDK de HDInsight](http://go.microsoft.com/fwlink/?LinkId=529017). Esto solo se aplica a los clústeres de HDInsight que se ejecutan en Windows.
   >
   >

**tooconnect tooa clúster mediante RDP**

1. Inicie sesión en toohello [Portal][azure-portal].
2. Haga clic en **examinar todos los** Hola menú izquierdo, haga clic en **clústeres de HDInsight**, haga clic en el nombre del clúster.
3. Haga clic en **configuración** desde el menú superior de hello y, a continuación, haga clic en **escritorio remoto**.
4. Haga clic en **conectar** y siga las instrucciones de Hola. Si Conectar está deshabilitado, debe habilitarlo primero. Asegúrese de que con nombre de usuario del usuario de escritorio remoto de hello y una contraseña.  No puede usar las credenciales de usuario del clúster de Hola.

## <a name="open-hadoop-command-line"></a>Apertura de la línea de comandos de Hadoop
tooconnect toohello clúster mediante el uso de escritorio remoto y la línea de comandos de uso hello Hadoop, debe primero ha habilitado clúster de toohello de acceso de escritorio remoto tal como se describe en la sección anterior de Hola.

**tooopen una línea de comandos de Hadoop**

1. Conecte el clúster toohello mediante Escritorio remoto.
2. En el escritorio de hello, haga doble clic en **línea de comandos de Hadoop**.

    ![HDI.HadoopCommandLine][image-hadoopcommandline]

    Para obtener más información acerca de los comandos de Hadoop, consulte [Referencia de comandos de Hadoop](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).

En hello captura de pantalla anterior, nombre de la carpeta de hello tiene el número de versión de Hadoop de hello incrustado. número de versión de Hola pueden utilizar modificada hello en función de versiones de componentes de Hadoop de hello instalados en el clúster de Hola. Puede usar carpetas de Hadoop entorno variables toorefer toothose. Por ejemplo:

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido cómo toocreate un clúster de HDInsight mediante el uso de Hola Portal y cómo tooopen Hola herramienta de línea de comandos de Hadoop. toolearn más información, vea Hola siguientes artículos:

* [Administración de HDInsight con PowerShell de Azure](hdinsight-administer-use-powershell.md)
* [Administración de HDInsight con la CLI de Azure](hdinsight-administer-use-command-line.md)
* [Creación de clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Envío de trabajos de Hadoop mediante programación](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Introducción a HDInsight de Azure](hdinsight-hadoop-linux-tutorial-get-started.md)
* [¿Qué versión de Hadoop tiene HDInsight de Azure?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Línea de comandos de Hadoop"
