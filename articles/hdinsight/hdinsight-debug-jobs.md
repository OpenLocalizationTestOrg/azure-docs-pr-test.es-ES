---
title: "Depuración de Hadoop en HDInsight: ver registros e interpretar mensajes de error - Azure | Microsoft Docs"
description: "Obtenga información acerca de los mensajes de error de hello que puede producirse cuando se administra con PowerShell y pasos que puede seguir toorecover de HDInsight."
services: hdinsight
tags: azure-portal
editor: cgronlun
manager: jhubbard
author: mumian
documentationcenter: 
ms.assetid: 7e6ceb0e-8be8-4911-bc80-20714030a3ad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 2f12a40e9dcac32ce2e11d66d60d8b3b212ecb53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-hdinsight-logs"></a>Analizar los registros de HDInsight
Cada clúster de Hadoop en HDInsight de Azure tiene una cuenta de almacenamiento de Azure utilizada como sistema de archivos predeterminado de Hola. cuenta de almacenamiento de Hola se conoce como cuenta de almacenamiento predeterminada de Hola. Clúster usa Hola almacenamiento de tabla de Azure y almacenamiento de blobs de Hola en hello predeterminado almacenamiento cuenta toostore sus archivos de registro.  toofind cuenta de almacenamiento predeterminado de hello para el clúster, consulte [Hadoop administrar clústeres de HDInsight](hdinsight-administer-use-management-portal.md#find-the-default-storage-account). los registros de Hola se conservan en hello cuenta de almacenamiento incluso después de que se elimina el clúster de Hola.

## <a name="logs-written-tooazure-tables"></a>Registros escritos tooAzure tablas
Hello registros escritos tooAzure tablas proporcionan un nivel de una visión general de lo que ocurre con un clúster de HDInsight.

Cuando se crea un clúster de HDInsight, 6 tablas se crean automáticamente para los clústeres basados en Linux en el almacenamiento de tabla predeterminada hello:

* hdinsightagentlog
* syslog
* daemonlog
* hadoopservicelog
* ambariserverlog
* ambariagentlog

Se crean tres tablas para los clústeres basados en Windows:

* setuplog: registro de eventos y excepciones detectados en el aprovisionamiento y la configuración de los clústeres de HDInsight.
* hadoopinstalllog: registro de eventos y las excepciones producidas durante la instalación de Hadoop en clúster de Hola. Esta tabla puede ser útil para depurar problemas relacionados con tooclusters creado con parámetros personalizados.
* hadoopservicelog: registro de eventos y excepciones registrados por todos los servicios de Hadoop. Esta tabla puede ser útil para depurar problemas relacionados toojob errores en clústeres de HDInsight.

nombres de archivo de tabla de Hello son **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**.

Estas tablas contienen Hola siguientes campos:

* ClusterDnsName
* ComponentName
* EventTimestamp
* Host
* MALoggingHash
* Message
* N
* PreciseTimeStamp
* Rol
* RowIndex
* Inquilino
* TIMESTAMP
* TraceLevel

### <a name="tools-for-accessing-hello-logs"></a>Herramientas para tener acceso a registros de Hola
Hay muchas herramientas disponibles para acceder a los datos de estas tablas:

* Visual Studio
* Explorador de almacenamiento de Azure
* Power Query para Excel

#### <a name="use-power-query-for-excel"></a>Uso de Power Query para Excel
Puede instalar Power Query desde [www.microsoft.com/en-US/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379). Vea Hola página de descargas de requisitos de sistema de Hola

**toouse Power Query tooopen y analizar el registro del servicio de Hola**

1. Abra **Microsoft Excel**.
2. De hello **Power Query** menú, haga clic en **de Azure**y, a continuación, haga clic en **almacenamiento de tabla de Azure de Microsoft**.
   
    ![Power Query de Excel de Hadoop de HDInsight: abrir el almacenamiento de tablas de Azure](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. Escriba el nombre de cuenta de almacenamiento de Hola. Esto puede ser el nombre corto de Hola u Hola FQDN.
4. Escriba la clave de cuenta de almacenamiento de Hola. Verá una lista de tablas:
   
    ![Registros de Hadoop de HDInsight almacenados en el almacenamiento de tablas de Azure](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. Tabla de hadoopservicelog contextual Hola Hola **navegador** panel y seleccione **editar**. Verá cuatro columnas. Si lo desea, eliminar hello **clave de partición**, **clave de fila**, y **Timestamp** columnas por ello, selecciónelos, a continuación, haga clic en **quitar columnas** entre las opciones de hello en la cinta de opciones de Hola.
6. Haga clic en hello icono en hello expandir columna toochoose Hola columnas que quiera tooimport en la hoja de cálculo de Excel de Hola de contenido. Para esta demostración, se ha elegido TraceLevel y ComponentName, ya que pueden aportar información básica sobre qué componentes tenían problemas.
   
    ![Registros de Hadoop de HDInsight: elegir columnas](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. Haga clic en **Aceptar** tooimport datos de saludo.
8. Seleccione hello **TraceLevel**, rol, y **ComponentName** columnas y, a continuación, haga clic en **Group By** control en la cinta de opciones de Hola.
9. Haga clic en **Aceptar** en hello cuadro Agrupar por
10. Haga clic en **Aplicar y cerrar**.

Ahora puede usar Excel toofilter y ordenación según sea necesario. Obviamente, puede que desee tooinclude otras columnas (por ejemplo, mensaje) en orden toodrill hacia abajo en problemas cuando se producen, pero seleccionando y agrupación de columnas de Hola que se ha descrito anteriormente proporcionan una imagen decente de lo que ocurre con los servicios de Hadoop. Hello idea mismo puede ser toohello aplicado setuplog y hadoopinstalllog tablas.

#### <a name="use-visual-studio"></a>Usar Visual Studio
**toouse Visual Studio**

1. Abra Visual Studio.
2. De hello **vista** menú, haga clic en **nube explorador**. También puede hacer clic simplemente en **CTRL+\,, CTRL+X**.
3. En **Cloud Explorer**, seleccione **Tipos de recursos**.  Hola otra opción disponible es **grupos de recursos**.
4. Expanda **cuentas de almacenamiento**, Hola cuenta de almacenamiento predeterminada para el clúster y, a continuación, **tablas**.
5. Haga doble clic en **hadoopservicelog**.
6. Agregue un filtro. Por ejemplo:
   
        TraceLevel eq 'ERROR'
   
    ![Registros de Hadoop de HDInsight: elegir columnas](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    Para obtener más información sobre cómo crear filtros, consulte [construir cadenas de filtro para el Diseñador de tablas de hello](../vs-azure-tools-table-designer-construct-filter-strings.md).

## <a name="logs-written-tooazure-blob-storage"></a>Registros escrito tooAzure almacenamiento de blobs
[Hola registra tablas tooAzure escrito](#log-written-to-azure-tables) proporcionan un nivel de una visión general de lo que ocurre con un clúster de HDInsight. Sin embargo, estas tablas no proporcionan registros de nivel de tarea, que pueden ser útiles para obtener detalles sobre los problemas cuando se producen. tooprovide este nivel de detalle, son los clústeres de HDInsight siguiente configura cuenta de almacenamiento de blobs de toowrite tareas registros tooyour para cualquier trabajo que se envía a través de Templeton. En la práctica, esto significa trabajos enviados mediante cmdlets de PowerShell de Azure de Microsoft de Hola u Hola .NET trabajo envío de API, no los trabajos enviados a través de RDP/comandos-línea toohello clúster de acceso. 

vea los registros de hello tooview, [aplicación hilo de acceso se registra en HDInsight basados en Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md).

Para obtener más información sobre los registros de aplicación, consulte [Simplifying user-logs management and access in YARN](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/)(Simplificar la administración de registros de usuario y el acceso en YARN).

## <a name="view-cluster-health-and-job-logs"></a>Visualización de los registros de trabajo y del estado del clúster
### <a name="access-hadoop-ui"></a>Acceder a la interfaz de usuario de Hadoop
Hola portal de Azure, haga clic en una hoja de clúster de HDInsight clúster nombre tooopen Hola. En la hoja de clúster de hello, haga clic en **panel**.

![Inicie el panel del clúster](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

Cuando se le solicite, escriba las credenciales de administrador de clúster de Hola. Hola consola de consultas que se abre, haga clic en **Hadoop UI**.

![Inicie la IU de Hadoop](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-hello-yarn-ui"></a>Hola Yarn interfaz de usuario de acceso
Hola portal de Azure, haga clic en una hoja de clúster de HDInsight clúster nombre tooopen Hola. En la hoja de clúster de hello, haga clic en **panel**. Cuando se le solicite, escriba las credenciales de administrador de clúster de Hola. Hola consola de consultas que se abre, haga clic en **YARN UI**.

Puede usar hello YARN UI toodo Hola a continuación:

* **Obtener el estado del clúster**. En el panel izquierdo de hello, expanda **clúster**y haga clic en **sobre**. Este present clúster detalles de estado como total asignados a la memoria, núcleos usados, estado del Administrador de recursos de clúster de hello, versión etcetera en clúster.
  
    ![Inicie el panel del clúster](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* **Obtener el estado del nodo**. En el panel izquierdo de hello, expanda **clúster**y haga clic en **nodos**. Esta acción muestra todos los nodos de hello en clúster de hello, dirección HTTP de cada nodo, nodo de tooeach la asignación de recursos, etcetera.
* **Supervisar el estado de los trabajos**. En el panel izquierdo de hello, expanda **clúster**y, a continuación, haga clic en **aplicaciones** toolist todos Hola trabajos en clúster de Hola. Si desea que toolook trabajos en un determinado estado (por ejemplo, ejecutando nuevo, enviada, etc.), haga clic en el vínculo apropiado de hello en **aplicaciones**. Además puede hacer clic Hola trabajo nombre toofind más información acerca de este tipo, incluidas la salida de hello, registros, etcetera trabajo de Hola.

### <a name="access-hello-hbase-ui"></a>Hola acceso HBase UI
Hola portal de Azure, haga clic en una hoja de clúster de HBase para HDInsight clúster nombre tooopen Hola. En la hoja de clúster de hello, haga clic en **panel**. Cuando se le solicite, escriba las credenciales de administrador de clúster de Hola. Hola consola de consultas que se abre, haga clic en **HBase UI**.

## <a name="hdinsight-error-codes"></a>Códigos de error de HDInsight
Hello mensajes de error que se detallan en esta sección se proporcionan a los usuarios de toohelp Hola de Hadoop en HDInsight de Azure comprenden posibles condiciones de error que pueden encontrar al administrar el servicio de hello con PowerShell de Azure y tooadvise usarlas en pasos de Hola que se pueden obtener toorecover de error de Hola.

Algunos de estos mensajes de error pudieron también aparecer en hello portal de Azure cuando es clústeres de HDInsight de toomanage usado. Otros mensajes de error que puede surgir, pero hay menos pormenorizados debido a restricciones de toohello en las acciones correctoras de hello posibles en este contexto. Otros mensajes de error se muestran en contextos de Hola donde mitigación hello es obvio. 

### <a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided
* **Descripción**: proporcione detalles de la base de datos de SQL Azure para al menos un componente en orden toouse configuración personalizada para las tiendas de metadatos de Hive y Oozie.
* **Mitigación**: usuario de hello necesita toosupply un SQL Azure tienda de metadatos y vuelva a intentarlo Hola de solicitud válido.  

### <a id="AzureRegionNotSupported"></a>AzureRegionNotSupported
* **Descripción**: no se pudo crear un clúster en la región *nombredelaregión*. Utilice una región de HDInsight válida y vuelva a enviar la solicitud.
* **Mitigación**: cliente debe crear área de clúster de Hola que actualmente es compatible con ellos: sudeste de Asia, Europa occidental, Europa del Norte, UU u oeste de Estados Unidos.  

### <a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound
* **Descripción**: no se encontró el servidor de Hola Hola solicitó el registro de clúster.  
* **Mitigación**: vuelva a intentar la operación de Hola.

### <a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord
* **Descripción**: el nombre DNS del clúster *nombreDNS* no es válido. Asegúrese de que empiece y acabe con un carácter alfanumérico y de que no contenga ningún carácter especial aparte de “-”.  
* **Mitigación**: asegúrese de que ha usado un nombre DNS válido para el clúster que comienza y termina con alfanuméricos y no contiene ningún especial caracteres distintos de guión de hello '-' y, a continuación, vuelva a intentar la operación de Hola.

### <a id="ClusterNameUnavailable"></a>ClusterNameUnavailable
* **Descripción**: el nombre de clúster *nombredeclúster* no está disponible. Elija otro nombre.  
* **Mitigación**: Hola debe especificar un nombre del clúster que es único y no existe y vuelva a intentar. Si el usuario hello usa Hola Portal, Hola UI ellos le notificará si un nombre de clúster ya se está utilizando durante Hola cree pasos.

### <a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid
* **Descripción**: la contraseña del clúster no es válida. Contraseña debe tener al menos 10 caracteres y debe contener al menos un número, letra mayúscula, letra minúscula y un carácter especial sin espacios en blanco y no debe contener el nombre de usuario de hello como parte del mismo.  
* **Mitigación**: proporcione una contraseña de clúster válido y vuelva a intentar la operación de Hola.

### <a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid
* **Descripción**: el nombre de usuario del clúster no es válido. Asegúrese de que no contenga caracteres especiales ni espacios.  
* **Mitigación**: proporcionar un nombre de usuario de clúster válido y vuelva a intentar la operación de Hola.

### <a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord
* **Descripción**: el nombre DNS del clúster *nombreDNSdelclúster* no es válido. Asegúrese de que empiece y acabe con un carácter alfanumérico y de que no contenga ningún carácter especial aparte de “-”.  
* **Mitigación**: proporcionar un nombre de usuario del clúster DNS válido y vuelva a intentar la operación de Hola.

### <a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName
* **Descripción**: nombre del contenedor en URI *yourcontainerURI* y el nombre DNS *yourDnsName* en solicitud cuerpo debe ser Hola igual.  
* **Mitigación**: asegúrese de que el nombre del contenedor y el nombre DNS Hola mismo y vuelva a intentar la operación de Hola.

### <a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound
* **Descripción**: la configuración de clúster no es válida. No se puede toofind las definiciones del nodo de datos de tamaño de nodo.  
* **Mitigación**: vuelva a intentar la operación de Hola.

### <a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure
* **Descripción**: error de eliminación de la implementación de hello clúster  
* **Mitigación**: vuelva a intentar la operación de eliminación de Hola.

### <a id="DnsMappingNotFound"></a>DnsMappingNotFound
* **Descripción**: error de configuración del servicio. No se encuentra la información de asignación de DNS requerida.  
* **Mitigación**: elimine el clúster y cree uno nuevo.

### <a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest
* **Descripción**: intento de duplicación de un contenedor de clúster. Existe un registro con el nombre *nombredelcontenedor* , pero las propiedades Etag no coinciden.
* **Mitigación**: proporcione un nombre único para el contenedor de Hola y Hola de reintento de la operación de creación.

### <a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService
* **Descripción**: el servicio hospedado *nombredelserviciohospedado* ya incluye un clúster. Los servicios hospedados no pueden contener varios clústeres.  
* **Mitigación**: clúster de hosts de hello en otro servicio hospedado.

### <a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus
* **Descripción**: servidor hello no pudo actualizar el estado de Hola de implementación del clúster Hola.  
* **Mitigación**: vuelva a intentar la operación de Hola. Si esto ocurre varias veces, póngase en contacto con CSS.

### <a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered
* **Descripción**: el clúster *nombredelclúster* se eliminó durante el mantenimiento. Por favor, vuelva a crear el clúster de Hola.
* **Mitigación**: clúster de hello vuelva a crear.

### <a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound
* **Descripción**: la configuración de clúster no es válida. Configuración de nodo principal requerida no encontrada en los tamaños de nodo.
* **Mitigación**: vuelva a intentar la operación de Hola.

### <a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure
* **Descripción**: no se puede toocreate servicio hospedado *nameOfYourHostedService*. Vuelva a intentarlo.  
* **Mitigación**: solicitud de Hola de reintento.

### <a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment
* **Descripción**: el servicio hospedado *nombredelserviciohospedado* ya incluye una implementación de producción. Los servicios hospedados no pueden contener varias implementaciones de producción. Vuelva a intentar la solicitud de hello con un nombre de clúster distinto.
* **Mitigación**: Use un nombre de clúster diferente y vuelva a intentar la solicitud de Hola.

### <a id="HostedServiceNotFound"></a>HostedServiceNotFound
* **Descripción**: servicio hospedado *nameOfYourHostedService* para no se puede encontrar el clúster de Hola.  
* **Mitigación**: si el clúster de hello está en estado de error, elimínelo y, a continuación, vuelva a intentarlo.

### <a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment
* **Descripción**: el servicio hospedado *nombredelserviciohospedado* no tiene asociada ninguna implementación.  
* **Mitigación**: si el clúster de hello está en estado de error, elimínelo y, a continuación, vuelva a intentarlo.

### <a id="InsufficientResourcesCores"></a>InsufficientResourcesCores
* **Descripción**: Hola SubscriptionId *yourSubscriptionId* no tiene clústeres de toocreate izquierdo núcleos *yourClusterName*. Necesario: *recursosrequeridos*, Disponible: *recursosdisponibles*.  
* **Mitigación**: liberar recursos de la suscripción o aumentar la suscripción de hello recursos toohello disponibles e inténtelo de nuevo clúster de hello toocreate.

### <a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices
* **Descripción**: Id. de suscripción *yourSubscriptionId* no tiene una cuota para un nuevo clúster de toocreate HostedService *yourClusterName*.  
* **Mitigación**: liberar recursos de la suscripción o aumentar la suscripción de hello recursos toohello disponibles e inténtelo de nuevo clúster de hello toocreate.

### <a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest
* **Descripción**: servidor hello encontró un error interno. Vuelva a intentarlo.  
* **Mitigación**: solicitud de Hola de reintento.

### <a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation
* **Descripción**: la ubicación de almacenamiento de Azure *nombrederegióndedatos* no es válida. Asegúrese de que la región de hello es correcta y vuelva a intentar la solicitud.
* **Mitigación**: seleccione una ubicación de almacenamiento que es compatible con HDInsight, compruebe que el clúster se ubican conjuntamente y vuelva a intentar la operación de Hola.

### <a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode
* **Descripción**: tamaño de máquina virtual no válido para los nodos de datos. Únicamente el tamaño de máquina virtual grande es compatible con todos los nodos de datos.  
* **Mitigación**: especifique el tamaño de nodo de hello compatible de nodo de datos de Hola y vuelva a intentar la operación de Hola.

### <a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode
* **Descripción**: tamaño de máquina virtual no válido para un nodo principal. Únicamente el tamaño de máquina virtual extragrande es compatible con los nodos principales.  
* **Mitigación**: especifique el tamaño de nodo de hello compatible de nodo principal de Hola y vuelva a intentar la operación de Hola

### <a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion
* **Descripción**: Id. de suscripción *yourSubscriptionId* usándola no tiene la operación de eliminación de tooexecute de permisos suficientes para clúster *yourClusterName*.  
* **Mitigación**: si el clúster de hello está en estado de error, se quita y, a continuación, vuelva a intentarlo.  

### <a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName
* **Descripción**: el nombre del contenedor de blobs de la cuenta de almacenamiento externa *nombredelcontenedor* no es válido. Asegúrese de que el nombre comience con una letra y solo contenga minúsculas, números y guiones.  
* **Mitigación**: especifique un nombre de contenedor de blob de cuenta de almacenamiento válida y vuelva a intentar la operación de Hola.

### <a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey
* **Descripción**: configuración de cuenta de almacenamiento externo de *yourStorageAccountName* es necesario toohave detalles de la clave secretas toobe conjunto.  
* **Mitigación**: especifique una clave secreta válida para la cuenta de almacenamiento de Hola y vuelva a intentar la operación de Hola.

### <a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat
* **Descripción**: el encabezado de la versión *encabezadodelaversión* no tiene el formato válido de aaaa-mm-dd.  
* **Mitigación**: especifique un formato válido para el encabezado de versión de Hola y vuelva a intentar la solicitud de saludo.

### <a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode
* **Descripción**: la configuración de clúster no es válida. Se encontró más de una configuración de nodo principal.  
* **Mitigación**: Editar configuración de Hola por lo que se especifica que sólo un nodo principal.

### <a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest
* **Descripción**: no se pudo completar la operación de hello en hello permitida tiempo u Hola número máximo de reintentos posibles. Vuelva a intentarlo.  
* **Mitigación**: solicitud de Hola de reintento.

### <a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty
* **Descripción**: el parámetro *nombredelparámetro* no puede ser nulo ni estar vacío.  
* **Mitigación**: especifique un valor válido para el parámetro hello.

### <a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure
* **Descripción**: uno o más entradas de la solicitud de creación de hello clúster no son válido. Asegúrese de que los valores de entrada de hello son correctos y vuelva a intentar la solicitud.  
* **Mitigación**: asegúrese de que los valores de entrada de hello son correctos y vuelva a intentar la solicitud.

### <a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable
* **Descripción**: la funcionalidad de región no está disponible para la región *nombredelaregión* y el identificador de suscripción *identificadordelasuscripción*.  
* **Mitigación**: especifique una región compatible con los clústeres de HDInsight. Hola públicamente admitido regiones son: sudeste de Asia, Europa occidental, Europa del Norte, UU u oeste de Estados Unidos.

### <a id="StorageAccountNotColocated"></a>StorageAccountNotColocated
* **Descripción**: la cuenta de almacenamiento *nombredelacuentadealmacenamiento* se encuentra en la región *nombredelaregiónactual*. Debe ser igual a la región de clúster de hello *yourClusterRegionName*.  
* **Mitigación**: especifique una cuenta de almacenamiento en Hola misma región que el clúster está en o si los datos ya están en la cuenta de almacenamiento de hello, crear un nuevo clúster en hello misma región que la cuenta de almacenamiento existente de Hola. Si usas Hola Portal, Hola interfaz de usuario les enviarán una notificación de este problema de antemano.

### <a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive
* **Descripción**: el identificador de suscripción proporcionado *identificadordelasuscripción* no está activo.  
* **Mitigación**: vuelva a activar la suscripción u obtenga una nueva suscripción válida.

### <a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound
* **Descripción**: no se encuentra el identificador de suscripción *identificadordelasuscripción* .  
* **Mitigación**: Compruebe que el identificador de suscripción es válido y vuelva a intentar la operación de Hola.

### <a id="UnableToResolveDNS"></a>UnableToResolveDNS
* **Descripción**: no se puede tooresolve DNS *yourDnsUrl*. Asegúrese de dirección URL de hello completo del extremo de blob de Hola se realiza.  
* **Mitigación**: proporcione una URL de blob válida. Hola dirección URL debe ser totalmente válido, incluidos a partir de *http://* y finales de *.com*.

### <a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource
* **Descripción**: no se puede tooverify ubicación del recurso *yourDnsUrl*. Asegúrese de dirección URL de hello completo del extremo de blob de Hola se realiza.  
* **Mitigación**: proporcione una URL de blob válida. Hola dirección URL debe ser totalmente válido, incluidos a partir de *http://* y finales de *.com*.

### <a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable
* **Descripción**: la funcionalidad de versión no está disponible para la versión *versiónespecificada* y el identificador de suscripción *identificadordelasuscripción*.  
* **Mitigación**: elegir una versión que está disponible y vuelva a intentar la operación de Hola.

### <a id="VersionNotSupported"></a>VersionNotSupported
* **Descripción**: la versión *versiónespecificada* no es compatible.
* **Mitigación**: elegir una versión que sea compatible y vuelva a intentar la operación de Hola.

### <a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion
* **Descripción**: la versión *versiónespecificada* no está disponible en la región de Azure *regiónespecificada*.  
* **Mitigación**: elegir una versión que se admite en la región de hello especificada y vuelva a intentar la operación de Hola.

### <a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound
* **Descripción**: la configuración de clúster no es válida. No se encuentra la configuración de cuenta WASB requerida en las cuentas externas.  
* **Mitigación**: Compruebe que la cuenta de hello existe y se ha establecido correctamente en operación de hello configuración e inténtelo de nuevo.

## <a name="next-steps"></a>Pasos siguientes
* [Usar vistas de Ambari toodebug Tez trabajos en HDInsight](hdinsight-debug-ambari-tez-view.md)
* [Habilitar los volcados de montón de los servicios de Hadoop en HDInsight basado en Linux (vista previa)](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [Administrar clústeres de HDInsight con Ambari Web UI Hola](hdinsight-hadoop-manage-ambari.md)

