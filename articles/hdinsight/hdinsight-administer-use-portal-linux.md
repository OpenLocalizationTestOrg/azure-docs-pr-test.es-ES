---
title: "clústeres de aaaManage Hadoop en HDInsight con el portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y administrar clústeres de HDInsight con hello portal de Azure."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Administrar clústeres de Hadoop en HDInsight con hello portal de Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Con hello [portal de Azure][azure-portal], puede administrar los clústeres de Hadoop en HDInsight de Azure. Utilice el tabulador de Hola para obtener información acerca de cómo administrar clústeres de Hadoop en HDInsight con otras herramientas.

**Requisitos previos**

Antes de comenzar este artículo, debe tener Hola siguientes elementos:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="open-hello-portal"></a>Portal de hello abierto
1. Inicie sesión en demasiado[https://portal.azure.com](https://portal.azure.com).
2. Después de abrir el portal de hello, hacer lo siguiente:

   * Haga clic en **New** de hello menú izquierdo toocreate un nuevo clúster:

       ![botón nuevo clúster de HDInsight](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * Haga clic en **clústeres de HDInsight** de hello toolist menú izquierdo Hola clústeres existentes

       ![Portal de Azure botón clúster de HDInsight](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       Si no ve el clúster de HDInsight, haga clic en **más servicios** en Hola parte inferior de la lista de hello y, a continuación, haga clic en **clústeres de HDInsight** en hello **Intelligence + análisis** sección.


## <a name="create-clusters"></a>Creación de clústeres
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

HDInsight trabaja con una amplia gama de componentes de Hadoop. Para hello lista de componentes de Hola que se han comprobado y compatibles, consulte [es la versión de Hadoop en HDInsight de Azure](hdinsight-component-versioning.md). Para obtener información de creación de clúster general de hello, consulte [Hadoop crear clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

### <a name="access-control-requirements"></a>Requisitos de control de acceso

Debe especificar una suscripción de Azure cuando cree un clúster de HDInsight. Este clúster se puede crear en un nuevo grupo de Azure Resource o en un grupo de recursos existente. Puede usar Hola siguiendo los pasos tooverify sus permisos para crear clústeres de HDInsight:

- toouse un grupo de recursos existente.

    1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
    2. Haga clic en **grupos de recursos** Hola menú izquierdo toolist Hola de grupos de recursos.
    3. Haga clic en el grupo de recursos de hello desea toouse para crear el clúster de HDInsight.
    4. Haga clic en **(de índices IAM) de control de acceso**y compruebe que usted (o un grupo que pertenecen a) tiene al menos Hola grupo de recursos de toohello de acceso de colaborador.

- toocreate un nuevo grupo de recursos

    1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
    2. Haga clic en **suscripción** desde el menú de la izquierda Hola. Tiene un icono amarillo de una llave amarilla. Verá una lista de suscripciones.
    3. Haga clic en suscripción de Hola que utiliza toocreate clústeres. 
    4. Haga clic en **Mis permisos**.  Muestra el [rol](../active-directory/role-based-access-control-what-is.md#built-in-roles) de suscripción de Hola. Necesita como mínimo clúster de HDInsight de toocreate de acceso de colaborador.

Si recibe el error de NoRegisteredProviderFound de Hola o hello MissingSubscriptionRegistration, consulte [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md).

## <a name="list-and-show-clusters"></a>Enumeración y visualización de clústeres
1. Inicie sesión en demasiado[https://portal.azure.com](https://portal.azure.com).
2. Haga clic en **clústeres de HDInsight** de hello toolist menú izquierdo Hola clústeres existentes.
3. Haga clic en el nombre del clúster de Hola. Si la lista de clústeres de hello es larga, puede utilizar el filtro en la parte superior de Hola de página Hola.
4. Haga clic en un clúster desde la página de información general de hello lista toosee hello:

    ![Azure Portal: aspectos básicos del clúster de HDInsight](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * **Panel**: panel de clúster de Hola se abre, que es Ambari Web para clústeres basados en Linux.
    * **Secure Shell**: clúster muestra hello instrucciones tooconnect toohello mediante conexión de Secure Shell (SSH).
    * **Escalar Cluster**: permite el número de hello toochange de nodos de trabajador para este clúster.
    * **Eliminar**: clúster de Hola de eliminaciones.
    * **Registros de actividad**: consultar y mostrar registros de actividad.
    * **Access Control (IAM)**: usar las asignaciones de roles.  Vea [usar recursos de suscripción de Azure de rol asignaciones toomanage acceso tooyour](../active-directory/role-based-access-control-configure.md).
    * **Etiquetas**: permite tooset clave-valor pares toodefine una taxonomía personalizada de servicios en la nube. Por ejemplo, puede crear una clave denominada **proyecto**y luego usar un valor común para todos los servicios asociados a un proyecto específico.
    * **Diagnosticar y solucionar problemas**: mostrar información sobre solución de problemas.
    * **Bloquea**: Agregar bloqueo tooprevent Hola clúster que se va a modificar o eliminar.
    * **Script de automatización**: plantilla de Azure Resource Manager Hola visualización y exportación para clúster Hola. Actualmente, sólo se puede exportar la cuenta de almacenamiento de Azure dependientes de Hola. Vea [Creación de clústeres de Hadoop basados en Linux en HDInsight con plantillas de Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).
    * **Inicio rápido**: muestra información que le ayuda a empezar a usar HDInsight.
    * **Herramientas para HDInsight**: información de ayuda para herramientas relacionadas con HDInsight.
    * **Inicio de sesión del clúster**: mostrar información de inicio de sesión de clúster de Hola.
    * **Uso de núcleo de suscripción**: mostrar hello núcleos utilizados y disponibles para su suscripción.
    * **Escalar Cluster**: aumento y reducción Hola número de nodos de trabajador del clúster. Vea [Escalado de clústeres](hdinsight-administer-use-management-portal.md#scale-clusters).
    * **Secure Shell**: clúster muestra hello instrucciones tooconnect toohello mediante conexión de Secure Shell (SSH). Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
    * **Asociado de HDInsight**: agregar o quitar Hola asociado de HDInsight actual.
    * **Las tiendas de metadatos externos**: ver las tiendas de metadatos de Hive y Oozie de Hola. las tiendas de metadatos de Hello solo pueden configurarse durante el proceso de creación de clúster de Hola. Vea [Uso de Hive/Oozie Metastore](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).
    * **Acciones de script**: Bash ejecutar scripts en clúster de Hola. Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).
    * **Aplicaciones**: agregar o quitar aplicaciones de HDInsight.  Vea [Instalación de aplicaciones de HDInsight personalizadas](hdinsight-apps-install-custom-applications.md).
    * **Propiedades**: ver las propiedades del clúster Hola.
    * **Las cuentas de almacenamiento**: ver cuentas de almacenamiento de Hola y claves de Hola. se configuran las cuentas de almacenamiento de Hola durante el proceso de creación de clúster de Hola.
    * **Identidad AAD de clúster**:
    * **Nueva solicitud de soporte técnico**: permite toocreate una incidencia de soporte técnico con el soporte técnico de Microsoft.
    
6. Haga clic en **Propiedades**.

    Hola propiedades son:

   * **Nombre del clúster**: nombre del clúster.
   * **Dirección URL del clúster**. dirección URL de Hello para la interfaz de hello Ambari web.
   * **Estado**: puede ser Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Región**: ubicación de Azure. Para obtener una lista de ubicaciones de Azure compatibles, vea hello **región** cuadro de lista desplegable en [precios HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Fecha de creación**.
   * **Sistema operativo**: **Windows** o **Linux**.
   * **Tipo**: Hadoop, HBase, Storm, Spark.
   * **Versión**. Consulte [Versiones de HDInsight](hdinsight-component-versioning.md)
   * **Suscripción**: nombre de la suscripción.
   * **Origen de datos predeterminado**: Hola de sistema de archivos de clúster de forma predeterminada.
   * **Tamaño de los nodos de trabajo**.
   * **Tamaño del nodo principal**.

## <a name="delete-clusters"></a>Eliminación de clústeres
La eliminación de un clúster no elimina la cuenta de almacenamiento predeterminada de Hola o las cuentas de almacenamiento vinculadas. Puede volver a crear el clúster de hello mediante el uso de hello las mismas cuentas de almacenamiento y hello las tiendas de metadatos mismo. Es recomendable toouse un nuevo contenedor de blobs de manera predeterminada cuando vuelve a crear el clúster de Hola.

1. Inicie sesión en toohello [Portal][azure-portal].
2. Haga clic en **clústeres de HDInsight** desde el menú de la izquierda Hola. Si no ve **clústeres de HDInsight**, primero haga clic en **More services** (Más servicios).
3. Haga clic en el clúster de Hola que desea toodelete.
4. Haga clic en **eliminar** desde el menú superior de hello y, a continuación, siga las instrucciones de Hola.

Vea también [Pausa o apagado de clústeres](#pauseshut-down-clusters).

## <a name="add-additional-storage-accounts"></a>Adición de cuentas de almacenamiento adicionales

Puede agregar más cuentas de Azure Storage y cuentas de Azure Data Lake Store una vez creado un clúster. Para obtener más información, consulte [agregar almacenamiento adicional cuentas tooHDInsight](./hdinsight-hadoop-add-storage.md).

## <a name="scale-clusters"></a>Escalado de clústeres
característica de ajuste de escala de clúster de Hola permite toochange número de Hola de nodos de trabajador usado por un clúster que se ejecuta en HDInsight de Azure sin necesidad de toore-crear clúster Hola.

> [!NOTE]
> Solo son compatibles los clústeres con la versión 3.1.3 de HDInsight, o superior. Si no está seguro de la versión de Hola del clúster, puede comprobar la página de propiedades de Hola.  Consulte [Enumeración y visualización de clústeres](#list-and-show-clusters).
>
>

impacto de Hola de cambiar el número de Hola de nodos de datos para cada tipo de clúster compatible con HDInsight:

* Hadoop

    Perfectamente puede aumentar el número de Hola de nodos de trabajador en un clúster de Hadoop que se ejecuta sin afectar a los trabajos pendientes o en ejecución. También se pueden enviar trabajos nuevos mientras Hola operación está en curso. Errores en una operación de ajuste de escala se controlan correctamente para que hello clúster siempre se deja en un estado funcional.

    Cuando un clúster de Hadoop es reducido reduciendo el número de Hola de nodos de datos, algunos de los servicios de hello en clúster de Hola se reinician. Este comportamiento provoca ejecutan todos y pendiente de trabajos toofail al término de Hola Hola la operación de escalado. Sin embargo, puede volver a enviar trabajos de hello una vez completada la operación de Hola.
* HBase

    Sin problemas, puede agregar o quitar el clúster de HBase tooyour nodos mientras se está ejecutando. Los servidores regionales se equilibran automáticamente dentro de unos pocos minutos después de completar la operación de escalado de Hola. No obstante, puede equilibrar manualmente servidores regionales Hola al iniciar sesión en el nodo principal de toohello del clúster y ejecución Hola siguientes comandos de una ventana del símbolo del sistema:

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

    ![Reequilibrio de escalado de HDInsight Storm](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Este es un ejemplo cómo toouse Hola CLI comando topología de Storm Hola toorebalance:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**clústeres de tooscale**

1. Inicie sesión en toohello [Portal][azure-portal].
2. Haga clic en **clústeres de HDInsight** desde el menú de la izquierda Hola.
3. Haga clic en el clúster de Hola que desee tooscale.
3. Haga clic en **Escalar clúster**.
4. Escriba el **Número de nodos de trabajo**. Hola Hola número límite de nodos del clúster varía para las suscripciones de Azure. Puede ponerse en contacto con facturación límite de hello tooincrease de soporte técnico.  información de costos de Hello refleja los cambios de hello realizados toohello número de nodos.

    ![HDInsight hadoop hbase storm spark escalar](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a>Pausa o apagado de clústeres

La mayoría de los trabajos de Hadoop son trabajos por lotes que se ejecutan solo ocasionalmente. Para la mayoría de los clústeres de Hadoop, hay períodos largos de tiempo no se utiliza ese clúster hello para el procesamiento. Con HDInsight, los datos se almacenan en Almacenamiento de Azure, por lo que puede eliminar un clúster de forma segura cuando no está en uso.
También se le cargará por un clúster de HDInsight aunque no esté en uso. Puesto que los cargos de Hola de clúster de hello son muchas veces más que los cargos de hello para el almacenamiento, conviene económico toodelete clústeres cuando no están en uso.

Hay muchas maneras se puede programar el proceso de hello:

* Usar Factoría de datos de Azure. Consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight a petición con Data Factory de Azure](hdinsight-hadoop-create-linux-clusters-adf.md) para crear servicios vinculados a HDInsight a petición.
* Usar Azure PowerShell.  Vea [Análisis de datos de retrasos de vuelos](hdinsight-analyze-flight-delay-data.md).
* Uso de CLI de Azure. Consulte [Administrar clústeres de HDInsight con la CLI de Azure](hdinsight-administer-use-command-line.md).
* Usar .NET SDK de HDInsight. Vea [Envío de trabajos de Hadoop](hdinsight-submit-hadoop-jobs-programmatically.md).

Para obtener información sobre precios de hello, consulte [precios HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete un clúster de hello Portal, consulte [eliminar clústeres](#delete-clusters)


## <a name="upgrade-clusters"></a>Actualización de clústeres

Vea [versión más reciente de HDInsight actualizar clúster tooa](./hdinsight-upgrade-cluster.md).

## <a name="change-passwords"></a>Cambio de contraseñas
Un clúster de HDInsight puede tener dos cuentas de usuario. Hola (también conocida como cuenta de usuario del clúster de HDInsight Cuenta de usuario HTTP) y Hola cuenta de usuario SSH se crean durante el proceso de creación de hello. Puede usar hello Ambari web UI toochange Hola clúster cuenta de usuario y contraseña, script acciones toochange hello y cuenta de usuario SSH

### <a name="change-hello-cluster-user-password"></a>Cambiar contraseña de usuario del clúster de Hola
Puede usar la contraseña de usuario de clúster de hello Ambari Web UI toochange Hola. toolog en tooAmbari, debe usar contraseña y nombre de usuario de clúster existente Hola.

> [!NOTE]
> Cambiar contraseña de usuario (admin) de clúster de hello puede provocar un script que las acciones que se ejecutaron en este toofail de clúster. Si dispone de todas las acciones de script persistentes que los nodos de trabajo de destino, estas secuencias de comandos pueden fallar al agregar nodos de clúster de toohello a través de operaciones de cambio de tamaño. Para más información sobre acciones de script, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Inicie sesión usando de interfaz de usuario de Ambari Web toohello Hola credenciales de usuario del clúster de HDInsight. el nombre de usuario de Hello predeterminada es **administración**. Hola dirección URL es **https://&lt;nombre del clúster de HDInsight > azurehdinsight.net**.
2. Haga clic en **administración** de menú superior de hello y, a continuación, haga clic en "Administrar Ambari".
3. Hola menú izquierdo, haga clic en **usuarios**.
4. Haga clic en **Administrador**.
5. Haga clic en **Cambiar contraseña**.

Ambari, a continuación, cambia la contraseña de hello en todos los nodos de clúster de Hola.

### <a name="change-hello-ssh-user-password"></a>Cambiar contraseña de usuario SSH de Hola
1. Con un editor de texto, guardar Hola después de texto como un archivo denominado **changepassword.sh**.

   > [!IMPORTANT]
   > Debe utilizar un editor que utiliza LF como final de la línea de saludo. Si el editor de hello usa CRLF, script de Hola no funciona.
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. Cargar hello tooa almacenamiento ubicación del archivo que puede tener acceso desde HDInsight mediante una dirección HTTP o HTTPS. Por ejemplo, un almacén de archivos público como OneDrive o Almacenamiento de blobs de Azure. Guardar archivo de toohello de hello URI (dirección HTTP o HTTPS), ya que este URI es necesaria en el paso siguiente de saludo.
3. En el portal de Azure hello, haga clic en **clústeres de HDInsight**.
4. Haga clic en el clúster de HDInsight.
4. Haga clic en **Acciones de scripts**.
4. De hello **acciones de Script** hoja, seleccione **Enviar nueva**. Cuando Hola **acción de secuencia de comandos de envío** hoja aparece, escriba Hola siguiente información:

   | Campo | Valor |
   | --- | --- |
   | Nombre |Cambio de contraseña de SSH |
   | URI de script de Bash |archivo de Hello URI toohello changepassword.sh |
   | Nodos (principal, de trabajo, nimbus, supervisor, Zookeeper, etc.) |✓ para todos los tipos de nodo enumerados |
   | parameters |Escriba el nombre de usuario SSH de hello y, a continuación, la contraseña nueva de Hola. Debe haber un espacio entre el nombre de usuario de Hola y Hola. |
   | Conservar esta acción de script... |Deje este campo en sin activar. |
5. Seleccione **crear** secuencia de comandos de tooapply Hola. Una vez finalizada la secuencia de comandos de hello, es capaz de tooconnect toohello clúster mediante SSH con la nueva contraseña de Hola.

## <a name="grantrevoke-access"></a>Concesión o revocación del acceso
Clústeres de HDInsight tienen Hola después de servicios web HTTP (todos estos servicios tienen extremos RESTful):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

De manera predeterminada, estos servicios se conceden para el acceso. Se puede revocar/grant Hola acceso mediante [CLI de Azure](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) y [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).

## <a name="find-hello-subscription-id"></a>Encuentra el Id. de suscripción de Hola

**toofind su Id. de suscripción de Azure**

1. Inicie sesión en toohello [Portal][azure-portal].
2. Haga clic en **Suscripciones**. Cada suscripción tiene un nombre y un identificador.

Cada clúster está ligada tooan suscripción de Azure. Hola suscripción identificador se muestra en el clúster de hello **esencial** icono. Consulte [Enumeración y visualización de clústeres](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Encontrar el grupo de recursos de Hola
En el modo de administrador de recursos de Azure de hello, cada clúster de HDInsight se crea con un grupo de Azure Resource Manager. grupo de administrador de recursos de Hola que un clúster pertenece tooappears en:

* lista de clúster de Hello tiene un **grupo de recursos** columna.
* Icono **Esencial** del clúster.  

Consulte [Enumeración y visualización de clústeres](#list-and-show-clusters).

## <a name="find-hello-default-storage-account"></a>Busque la cuenta de almacenamiento predeterminada de Hola
Cada clúster de HDInsight tiene una cuenta de almacenamiento predeterminada. Hola cuenta de almacenamiento predeterminada y sus claves para un clúster aparece en **cuentas de almacenamiento**. Consulte [Enumeración y visualización de clústeres](#list-and-show-clusters).

## <a name="run-hive-queries"></a>Ejecución de consultas de Hive
No se puede ejecutar el trabajo de Hive directamente desde Hola portal de Azure, pero puede usar Hola Hive vista en la interfaz de usuario de Ambari Web.

**consultas de Hive toorun con Ambari Hive View**

1. Inicie sesión usando de interfaz de usuario de Ambari Web toohello Hola credenciales de usuario del clúster de HDInsight. el nombre de usuario de Hello predeterminada es **administración**. Hola dirección URL es **https://&lt;nombre del clúster de HDInsight > azurehdinsight.net**.
2. Abrir vista Hive tal y como se muestra en la siguiente captura de pantalla de hello:  

    ![Vista de hive de HDInsight](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. Haga clic en **consulta** desde el menú superior Hola.
4. Escriba una consulta de Hive en el **Editor de consultas** y haga clic en **Execute** (Ejecutar).

## <a name="monitor-jobs"></a>Supervisión de trabajos
Vea [HDInsight administrar clústeres mediante el uso de hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring).

## <a name="browse-files"></a>Examinar archivos
Con hello portal de Azure, puede examinar el contenido de Hola de contenedor de hello predeterminado.

1. Inicie sesión en demasiado[https://portal.azure.com](https://portal.azure.com).
2. Haga clic en **clústeres de HDInsight** de hello toolist menú izquierdo Hola clústeres existentes.
3. Haga clic en el nombre del clúster de Hola. Si la lista de clústeres de hello es larga, puede utilizar el filtro en la parte superior de Hola de página Hola.
4. Haga clic en **cuentas de almacenamiento** desde el menú de la izquierda de hello clúster.
5. Haga clic en una cuenta de almacenamiento.
7. Haga clic en hello **Blobs** icono.
8. Haga clic en el nombre del contenedor predeterminado Hola.

## <a name="monitor-cluster-usage"></a>Supervisión del uso de los clústeres
Hola **uso** sección de hoja de clúster de HDInsight de hello muestra información sobre el número de Hola de suscripción de núcleos tooyour disponibles para su uso con HDInsight, así como número de Hola de núcleos asignados toothis clúster y cómo se asignar para nodos de hello en este clúster. Consulte [Enumeración y visualización de clústeres](#list-and-show-clusters).

> [!IMPORTANT]
> Servicios de hello toomonitor proporcionan por hello clúster de HDInsight, se debe usar Ambari Web u Hola API de REST de Ambari. Para obtener más información sobre el uso de Ambari, consulte [Administración de clústeres de HDInsight con Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="connect-tooa-cluster"></a>Conectar el clúster tooa

* [Uso de Hive con HDInsight](hdinsight-hadoop-use-hive-ambari-view.md)
* [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a>Pasos siguientes
En este artículo ha aprendido algunas funciones básicas administrativas. toolearn más información, vea Hola siguientes artículos:

* [Administración de HDInsight con PowerShell de Azure](hdinsight-administer-use-powershell.md)
* [Administración de HDInsight con la CLI de Azure](hdinsight-administer-use-command-line.md)
* [Creación de clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Uso de Hive en HDInsight](hdinsight-use-hive.md)
* [Uso de Pig en HDInsight](hdinsight-use-pig.md)
* [Uso de Sqoop en HDInsight](hdinsight-use-sqoop.md)
* [Introducción a HDInsight de Azure](hdinsight-hadoop-linux-tutorial-get-started.md)
* [¿Qué versión de Hadoop tiene HDInsight de Azure?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Línea de comandos de Hadoop"
