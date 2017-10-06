---
title: entornos aaaCompute compatibles con Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de los entornos de proceso que puede usar en los datos de tootransform o proceso de canalizaciones (por ejemplo, HDInsight de Azure) de Data Factory de Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>Entornos de proceso compatibles con Azure Data Factory
Este artículo explica entornos de proceso diferente que puede usar tooprocess o transformar datos. También proporciona detalles sobre las diferentes configuraciones (demand frente a aportar su propia) compatibles con factoría de datos al configurar los servicios vinculados vincular estos factoría de datos de Azure compute tooan de entornos.

Hello tabla siguiente proporciona una lista de entornos de ejecución compatible con las actividades de hello y factoría de datos que se pueden ejecutar en ellos. 

| Entorno de procesos | actividades |
| --- | --- |
| [Clúster de HDInsight a petición](#azure-hdinsight-on-demand-linked-service) o [clúster HDInsight propio](#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md) |
| [Azure Batch](#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](#azure-machine-learning-linked-service) |[Actividades de Machine Learning: ejecución de Batch y recurso de actualización](data-factory-azure-ml-batch-execution-activity.md) |
| [Análisis con Azure Data Lake](#azure-data-lake-analytics-linked-service) |[U-SQL de análisis con Data Lake](data-factory-usql-activity.md) |
| [Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service) |[Procedimiento almacenado](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a>Versiones admitidas de HDInsight en Azure Data Factory
HDInsight de Azure es compatible con varias versiones de clústeres de Hadoop que se pueden implementar en cualquier momento. Cada opción de versión crea una versión específica de la distribución de hello Hortonworks Data Platform (HDP) y un conjunto de componentes que están dentro de la distribución. Microsoft mantiene actualizar lista Hola de versiones admitidas de componentes de ecosistema de Hadoop más recientes de HDInsight tooprovide y correcciones. Hola 3.2 de HDInsight está en desuso en el 1 de abril de 2017. Para más información, consulte [Versiones compatibles de HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).

Esto afecta a las instancias de Azure Data Factory que ejecutan actividades en los clústeres de HDInsight 3.2. Se recomienda que los usuarios instrucciones de hello toofollow Hola siguiendo la sección tooupdate Hola factorías de datos afectados:

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a>Para los servicios vinculados que señala tooyour propios clústeres de HDInsight
* **Servicios vinculados de HDInsight que señala tooyour posee HDInsight 3.2 o por debajo de clústeres:**

  Factoría de datos de Azure es compatible con clústeres de HDInsight propio de HDI 3.1 demasiado enviando tooyour de trabajos[Hola admitido la última versión de HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). Sin embargo, ya no puede crear el clúster de HDInsight 3.2 después del 1 de abril de 2017 basándose en la directiva de degradación de hello documentado en [HDInsight versiones compatibles](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).  

  **Recomendaciones:** 
  * Realizar pruebas tooensure Hola compatibilidad de hello las actividades que hacen referencia a los servicios vinculados demasiado[Hola admitido la última versión de HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) con la información que se documentan en [disponible con componentes de Hadoop diferentes versiones de HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) y [Hortonworks notas asociados con las versiones de HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Actualizar el clúster de HDInsight 3.2 demasiado[Hola admitido la última versión de HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget Hola componentes del ecosistema de Hadoop y correcciones más recientes. 

* **Servicios vinculados de HDInsight que señala tooyour posee HDInsight 3.3 o una versión posterior de clústeres:**

  Factoría de datos de Azure es compatible con clústeres de HDInsight propio de HDI 3.1 demasiado enviando tooyour de trabajos[Hola admitido la última versión de HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). 
  
  **Recomendaciones:** 
  * No se requiere ninguna acción en relación con Data Factory. Sin embargo, si se encuentra en una versión anterior de HDInsight, todavía sigue siendo recomendable actualizar demasiado[Hola admitido la última versión de HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget Hola componentes del ecosistema de Hadoop y correcciones más recientes.

### <a name="for-hdinsight-on-demand-linked-services"></a>Para Servicios vinculados a petición de HDInsight
* **La versión 3.2, u otra inferior, se especifica en la definición de JSON de los Servicios vinculados a petición de HDInsight:**
  
  Azure Data Factory admitirá la creación de clústeres de HDInsight a petición de la versión 3.3 o superior a partir del **15/05/2017** en adelante. Y, al final de Hola de soporte técnico para existente 3.2 de HDInsight a petición servicios vinculados se extiende demasiado**15/07/2017**.  

  **Recomendaciones:** 
  * Realizar pruebas tooensure Hola compatibilidad de hello las actividades que hacen referencia a los servicios vinculados demasiado [Hola admitido la última versión de HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) con la información que se documentan en [disponible con componentes de Hadoop diferentes versiones de HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) y [Hortonworks notas asociados con las versiones de HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Antes de **15/07/2017**, actualizar la propiedad de versión de hello en la definición de JSON de servicio vinculado de petición HDI demasiado[Hola admitido la última versión de HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) componentes del ecosistema de Hadoop de última tooget hello y correcciones. Para la definición de JSON detallado, consulte toohello [ejemplo de servicio vinculado de Azure HDInsight a petición](#azure-hdinsight-on-demand-linked-service). 

* **Versión no especificada de los Servicios vinculados de HDInsight a petición:**
  
  Azure Data Factory admitirá la creación de clústeres de HDInsight a petición de la versión 3.3 o superior a partir del **15/05/2017** en adelante. Y, en el final de hello de servicios de soporte técnico tooexisting petición 3.2 de HDInsight vinculada se extiende demasiado**15/07/2017**. 

  Antes de **15/07/2017**, si se deja en blanco, valores predeterminados de Hola de versión y osType propiedades son: 

  | Propiedad | Valor predeterminado | Obligatorio |
  | --- | --- | --- |
  Versión   | HDI 3.1 para clústeres de Windows y HDI 3.2 para clústeres de Linux.| No
  osType | valor predeterminado de Hello es Windows | No

  Después de **15/07/2017**, si se deja en blanco, valores predeterminados de Hola de versión y osType propiedades son:

  | Propiedad | Valor predeterminado | Obligatorio |
  | --- | --- | --- |
  Versión   | HDI 3.3 para clústeres de Windows y HDI 3.5 para clústeres de Linux.    | No
  osType | valor predeterminado de Hello es Linux   | No

  **Recomendaciones:** 
  * Antes de **15/07/2017**, realizar pruebas tooensure Hola compatibilidad de hello las actividades que hacen referencia a los servicios vinculados demasiado[Hola admitido la última versión de HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) con información documentado en [Hadoop componentes disponibles con distintas versiones de HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) y [Hortonworks notas asociados con las versiones de HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).  
  * Después de **15/07/2017**, asegúrese de especificar explícitamente valores osType y versión si desea que la configuración predeterminada de toooverride Hola. 

>[!Note]
>Actualmente Azure Data Factory no es compatible con clústeres de HDInsight que usan Azure Data Lake Store como almacén principal. Use Azure Storage como almacén principal para los clústeres de HDInsight. 
>  
>  

## <a name="on-demand-compute-environment"></a>Entorno de procesos a petición
En este tipo de configuración, entorno informático de hello es completamente administrado por servicio de factoría de datos de Azure Hola. Automáticamente se crea por hello servicio factoría de datos antes de que un trabajo se tooprocess enviado datos y quitan cuando se completa el trabajo de Hola. Puede crear un servicio vinculado para el entorno de proceso a petición de hello, configurar y controlar la configuración granular de ejecución del trabajo, administración del clúster y acciones de arranque.

> [!NOTE]
> configuración de la petición de Hello actualmente solo se admite para clústeres de HDInsight de Azure.
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Servicio vinculado a petición de HDInsight de Azure
Hola servicio Data Factory de Azure puede crear automáticamente un basadas en Windows/Linux a petición HDInsight tooprocess datos del clúster. clúster Hola se crea en la misma región que la cuenta de almacenamiento de hello (propiedad linkedServiceName en hello JSON) asociada a clúster Hola de Hola. cuenta de almacenamiento de Hello debe ser una cuenta de almacenamiento de Azure estándar general. 

Tenga en cuenta los siguiente hello **importante** puntos acerca de HDInsight a petición de servicio vinculado:

* No se ve en la petición de hello clúster de HDInsight creado en su suscripción de Azure. Hola servicio Data Factory de Azure administra el clúster de HDInsight a petición de hello en su nombre.
* Hello registros para los trabajos que se ejecutan en un HDInsight a petición clúster copian toohello cuenta de almacenamiento asociada con el clúster de HDInsight de Hola. Puede tener acceso a estos registros de portal de Azure en Hola Hola **detalles de ejecución de la actividad** hoja. Consulte el artículo [Supervisión y administración de canalizaciones](data-factory-monitor-manage-pipelines.md) para obtener más información.
* Se le cobra solo por hora de hello al clúster de HDInsight de hello está activo y los trabajos en ejecución.

> [!IMPORTANT]
> Suele tardar **20 minutos** o más tooprovision un HDInsight de Azure de clúster a petición.
> 
> 

### <a name="example"></a>Ejemplo
Hola después de JSON define un servicio de vinculado de HDInsight a petición basadas en Linux. Hola servicio factoría de datos crea automáticamente un **basados en Linux** clúster de HDInsight al procesar un segmento de datos. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

toouse un clúster de HDInsight basados en Windows, establecer **osType** demasiado**windows** o no use la propiedad hello como valor predeterminado de hello es: windows.  

> [!IMPORTANT]
> clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (**linkedServiceName**). HDInsight no elimine este contenedor cuando se elimina el clúster de Hola. Este comportamiento es así por diseño. Con el servicio de vinculado de HDInsight a petición, se crea un clúster de HDInsight cada vez que un segmento necesario toobe procesado a menos que haya un clúster existente en vivo (**timeToLive**) y se elimina cuando se realiza un procesamiento Hola. 
> 
> A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure. Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola. nombres de Hola de estos contenedores siguen un patrón: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.
> 
> 

### <a name="properties"></a>Propiedades
| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |se debe establecer propiedad de tipo Hello demasiado**HDInsightOnDemand**. |Sí |
| clusterSize |Número de nodos de trabajador/datos en clúster de Hola. clúster de HDInsight de Hola se crea con 2 nodos principales junto con el número de Hola de nodos de trabajador que especifique para esta propiedad. nodos de Hello son de tamaño Standard_D3 que tiene 4 núcleos, por lo que un clúster de nodo de 4 trabajo tiene 24 núcleos (4\*para nodos de trabajador, además de 2 núcleos, 4 = 16\*4 = 8 núcleos para nodos principales). Vea [Hadoop basado en Linux crear clústeres de HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) para obtener más información acerca del nivel de hello Standard_D3. |Sí |
| timeToLive |Hola permitido de tiempo de inactividad para el clúster de HDInsight a petición Hola. Especifica cuánto tiempo permanece activo clúster de HDInsight a petición Hola tras la finalización de una actividad que se ejecutan si no hay otros trabajos activos en clúster de Hola.<br/><br/>Por ejemplo, si la ejecución de una actividad tiene 6 minutos y timetolive es establecer too5 minutos, Hola clúster permanece activo durante 5 minutos después de hello 6 minutos de procesamiento de ejecución de la actividad de Hola. Si se ejecuta otra actividad que se ejecute con la ventana de 6 minutos hello, que se procesa por hello mismo clúster.<br/><br/>Creación de un clúster de HDInsight a petición es una operación costosa (podría tardar un poco), por lo que use esta opción como sea necesario tooimprove de rendimiento de una factoría de datos mediante la reutilización de un clúster de HDInsight a petición.<br/><br/>Si establece too0 de valor timetolive, clúster Hola se eliminará tan pronto como finaliza la ejecución de la actividad de Hola. Mientras que, si establece un valor alto, puede que el clúster de hello permanezca inactivo innecesariamente da lugar a altos costos. Por lo tanto, es importante que establezca el valor adecuado de hello según sus necesidades.<br/><br/>Si el valor de la propiedad timetolive Hola está configurado correctamente, varias canalizaciones pueden compartir instancia Hola Hola a petición del clúster de HDInsight.  |Sí |
| versión |Versión Hola del clúster de HDInsight. valor predeterminado de Hello es 3.1 para clúster de Windows y 3.2 para clústeres de Linux. |No |
| linkedServiceName | Almacenamiento de Azure vinculada toobe servicio utilizado por clúster de petición de Hola para almacenar y procesar datos. Hello clúster de HDInsight se crea en Hola misma región que esta cuenta de almacenamiento de Azure.<p>Actualmente, no se puede crear un clúster de HDInsight a petición que utiliza un almacén de Azure Data Lake como almacenamiento de Hola. Si desea que los datos del resultado de hello toostore de HDInsight de procesamiento en un almacén de Data Lake de Azure, use una actividad de copia toocopy Hola de datos de almacenamiento de blobs de Azure de hello toohello almacén de Azure Data Lake. </p>  | Sí |
| additionalLinkedServiceNames |Especifica las cuentas de almacenamiento adicional para hello HDInsight el servicio vinculado para que el servicio de factoría de datos de hello puede registrar en su nombre. Estas cuentas de almacenamiento deben estar en hello misma región que el clúster de HDInsight de hello, que se crea en Hola misma región que la cuenta de almacenamiento de hello especificado por linkedServiceName. |No |
| osType |Tipo de sistema operativo. Los valores permitidos son: Windows (predeterminado) y Linux |No |
| hcatalogLinkedServiceName |nombre de Hola de SQL Azure vinculado esa base de datos de HCatalog toohello de punto de servicio. clúster de HDInsight a petición Hola se crea mediante el uso de base de datos de SQL Azure hello como Hola tienda de metadatos. |No |

#### <a name="additionallinkedservicenames-json-example"></a>Ejemplo JSON de additionalLinkedServiceNames

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a>Propiedades avanzadas
También puede especificar Hola propiedades para la configuración granular de Hola Hola a petición del clúster de HDInsight siguientes.

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| coreConfiguration |Especifica parámetros de configuración de núcleo de hello (como en core-site.xml) para toobe de clúster de HDInsight Hola creado. |No |
| hBaseConfiguration |Especifica los parámetros de configuración hello HBase (hbase-site.xml) para el clúster de HDInsight Hola. |No |
| hdfsConfiguration |Especifica los parámetros de configuración Hola HDFS (hdfs-site.xml) para el clúster de HDInsight Hola. |No |
| hiveConfiguration |Especifica los parámetros de configuración Hola hive (hive-site.xml) para el clúster de HDInsight Hola. |No |
| mapReduceConfiguration |Especifica los parámetros de configuración Hola MapReduce (mapred-site.xml) para el clúster de HDInsight Hola. |No |
| oozieConfiguration |Especifica los parámetros de configuración de Oozie (oozie-Site.mxl) de Hola para clúster de HDInsight Hola. |No |
| stormConfiguration |Especifica los parámetros de configuración Hola Storm (storm-site.xml) para el clúster de HDInsight de Hola. |No |
| yarnConfiguration |Especifica los parámetros de configuración de Yarn (yarn-site.xml) de Hola para clúster de HDInsight Hola. |No |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a>Ejemplo: configuración del clúster de HDInsight a petición con propiedades avanzadas

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
      "coreConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "hiveConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "mapReduceConfiguration": {
        "mapreduce.reduce.java.opts": "-Xmx4000m",
        "mapreduce.map.java.opts": "-Xmx4000m",
        "mapreduce.map.memory.mb": "5000",
        "mapreduce.reduce.memory.mb": "5000",
        "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
      },
      "yarnConfiguration": {
        "yarn.app.mapreduce.am.resource.mb": "5000",
        "mapreduce.map.memory.mb": "5000"
      },
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a>Tamaño de nodo
Puede especificar tamaños de Hola de nodos de head, los datos y zookeeper con hello propiedades siguientes: 

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| headNodeSize |Especifica el tamaño de hello del nodo principal de Hola. valor predeterminado de Hello es: Standard_D3. Vea hello **especificación de tamaños de nodo** sección para obtener más información. |No |
| dataNodeSize |Especifica el tamaño de Hola de nodo de datos de Hola. valor predeterminado de Hello es: Standard_D3. |No |
| zookeeperNodeSize |Especifica el tamaño de Hola de nodo de Zoo poseedor de Hola. valor predeterminado de Hello es: Standard_D3. |No |

#### <a name="specifying-node-sizes"></a>Especificación de tamaños de nodo
Vea hello [tamaños de las máquinas virtuales](../virtual-machines/linux/sizes.md) artículo para valores de cadena necesario toospecify para las propiedades de hello mencionados en la sección anterior de Hola. los valores de Hello tienen tooconform toohello **CMDLETs & API** al que hace referencia en el artículo Hola. Como puede ver en el artículo hello, nodo de datos de Hola de tamaño grande (valor predeterminado) tiene 7 GB de memoria, que puede no ser suficiente para su escenario. 

Si desea un tamaño toocreate D4 nodos principales y trabajo, especifique **Standard_D4** como valor de Hola para las propiedades headNodeSize y dataNodeSize. 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

Si especifica un valor incorrecto para estas propiedades, puede recibir el siguiente hello **error:** no se pudo toocreate clúster. Excepción: Clúster de hello toocomplete no se puede crear la operación. Error en la operación con el código '400'. El clúster generó el estado: 'Error'. Mensaje: 'PreClusterCreationValidationFailure'. Cuando reciba este error, asegúrese de que está utilizando hello **CMDLET & API** nombre de tabla de Hola Hola [tamaños de las máquinas virtuales](../virtual-machines/linux/sizes.md) artículo.  

## <a name="bring-your-own-compute-environment"></a>Traer su propio entorno de procesos
En este tipo de configuración, los usuarios pueden registrar un entorno de procesos existente como un servicio vinculado en la Factoría de datos. entorno informático de Hola está administrada por el usuario de Hola y Hola servicio factoría de datos utiliza las actividades de hello tooexecute.

Este tipo de configuración es compatible para entornos de proceso siguiente hello:

* HDInsight de Azure
* Azure Batch
* Aprendizaje automático de Azure
* Análisis con Azure Data Lake
* Azure SQL DB, Azure SQL DW, SQL Server

## <a name="azure-hdinsight-linked-service"></a>Servicio vinculado de HDInsight de Azure
Puede crear su propio clúster de HDInsight de un tooregister de servicio vinculado de HDInsight de Azure con factoría de datos.

### <a name="example"></a>Ejemplo

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a>Propiedades
| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |se debe establecer propiedad de tipo Hello demasiado**HDInsight**. |Sí |
| clusterUri |Hola URI Hola del clúster de HDInsight. |Sí |
| nombre de usuario |Especificar nombre de Hola de hello usuario toobe usa clúster de HDInsight de tooconnect tooan existente. |Sí |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola. |Sí |
| linkedServiceName | Nombre del servicio vinculado de almacenamiento de Azure que hace referencia el almacenamiento de blobs de Azure toohello hello usa Hola clúster de HDInsight. <p>Actualmente, no se puede especificar un servicio vinculado de Azure Data Lake Store para esta propiedad. Si el clúster de HDInsight de hello tiene acceso toohello almacén de Data Lake, puede tener acceso a datos en el almacén de Azure Data Lake Hola desde scripts de Pig/Hive. </p>  |Sí |

## <a name="azure-batch-linked-service"></a>Servicio vinculado de Lote de Azure
Puede crear un tooregister de servicio vinculado Azure Batch en un grupo de lote de la factoría de datos de tooa de máquinas virtuales (VM). Puede ejecutar actividades personalizadas .NET con Lote de Azure o HDInsight de Azure.

Vea los temas siguientes si es un nuevo servicio de lote de tooAzure:

* [Aspectos básicos de Azure por lotes](../batch/batch-technical-overview.md) para obtener información general de hello servicio Azure Batch.
* [Nueva AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet toocreate una cuenta de lote de Azure (o) [portal de Azure](../batch/batch-account-create-portal.md) toocreate cuenta de Azure Batch hello mediante el portal de Azure. Vea [toomanage mediante PowerShell cuenta de lote de Azure](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) tema para obtener instrucciones detalladas sobre cómo usar el cmdlet de Hola.
* [Nueva AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet toocreate un grupo de lote de Azure.

### <a name="example"></a>Ejemplo

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

Anexar "**.\< nombre de la región\>**"toohello nombre de la cuenta de lote para hello **accountName** propiedad. Ejemplo:

```json
"accountName": "mybatchaccount.eastus"
```

Otra opción es el punto de conexión de tooprovide hello batchUri tal y como se muestra en el siguiente ejemplo de Hola:

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a>Propiedades
| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |se debe establecer propiedad de tipo Hello demasiado**AzureBatch**. |Sí |
| accountName |Nombre de cuenta de Azure Batch Hola. |Sí |
| accessKey |Clave de acceso de hello cuenta de lote de Azure. |Sí |
| poolName |Nombre del grupo de Hola de máquinas virtuales. |Sí |
| linkedServiceName |Nombre del servicio vinculado de almacenamiento de Azure asociado a este servicio vinculado Azure Batch Hola. Este servicio vinculado se usa para archivos de almacenamiento provisional actividad de hello toorun y almacenar los registros de ejecución de actividad de hello necesarios. |Sí |

## <a name="azure-machine-learning-linked-service"></a>Servicio vinculado de aprendizaje automático de Azure
Crear un tooregister de servicio vinculado de aprendizaje de automático de Azure de un lote de aprendizaje automático factoría de datos de punto de conexión tooa de puntuación.

### <a name="example"></a>Ejemplo

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a>Propiedades
| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| Tipo |propiedad de tipo Hello debe establecerse en: **AzureML**. |Sí |
| mlEndpoint |dirección URL de puntuación de lotes de Hola. |Sí |
| apiKey |Hola publica API del modelo de área de trabajo. |Sí |

## <a name="azure-data-lake-analytics-linked-service"></a>Servicio vinculado con el Análisis con Azure Data Lake
Crear un **análisis de Azure Data Lake** vinculado toolink un generador de datos de Azure análisis de Azure Data Lake tooan de servicio de proceso de servicio. actividad de Data Lake Analytics U-SQL en la canalización de Hola Hola hace referencia servicio toothis vinculado. 

Hello tabla siguiente ofrece descripciones de hello genéricos propiedades utilizadas en hello definición de JSON. Puede elegir entre la autenticación de la entidad de servicio y la autenticación de credenciales de usuario.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| **type** |propiedad de tipo Hello debe establecerse en: **AzureDataLakeAnalytics**. |Sí |
| **accountName** |Nombre de la cuenta de Análisis de Azure Data Lake |Sí |
| **dataLakeAnalyticsUri** |Identificador URI de Análisis de Azure Data Lake. |No |
| **subscriptionId** |Identificador de suscripción de Azure |No (si no se especifica, suscripción de Hola se usa la factoría de datos). |
| **resourceGroupName** |Nombre del grupo de recursos de Azure. |No (si no se especifica, el grupo de recursos de Hola se usa la factoría de datos). |

### <a name="service-principal-authentication-recommended"></a>Autenticación de la entidad de servicio (recomendada)
toouse autenticación principal del servicio, registrar una entidad de la aplicación en Azure Active Directory (Azure AD) y conceda a Hola acceso tooData Lake almacén. Consulte [Autenticación entre servicios](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) para ver los pasos detallados. Tome nota de hello después de valores, que se utiliza toodefine Hola servicio vinculado:
* Identificador de aplicación
* Clave de la aplicación 
* Id. de inquilino

Utilizar autenticación de entidad de seguridad de servicio mediante la especificación de hello propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| **servicePrincipalId** | Especifique el identificador de cliente de. la aplicación hello | Sí |
| **servicePrincipalKey** | Especifique la clave de la aplicación hello. | Sí |
| **tenant** | Especifique la información de inquilino de hello (inquilino o el nombre de identificador de dominio) en que se encuentra la aplicación. Puede recuperarlo mediante el desplazamiento del mouse de hello en la esquina superior derecha de Hola de hello portal de Azure. | Sí |

**Ejemplo: autenticación de la entidad de servicio**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Autenticación de credenciales de usuario
Como alternativa, puede usar la autenticación de credenciales de usuario para el análisis de Data Lake especificando Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| **authorization** | Haga clic en hello **Authorize** botón Hola Editor de generador de datos y escriba sus credenciales que asigna la propiedad de hello autogenerado autorización URL toothis. | Sí |
| **sessionId** | Identificador de sesión de OAuth de sesión de autorización de OAuth de Hola. Cada id. de sesión es único y solo se puede usar una vez. Esta configuración se genera automáticamente cuando se usa Hola Editor de generador de datos. | Sí |

**Ejemplo: autenticación de credenciales de usuario**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Expiración del token
Hola código de autorización ha generado mediante el uso de hello **Authorize** botón expira después de unos minutos. Vea hello en la tabla siguiente para unos tiempos de expiración Hola para diferentes tipos de cuentas de usuario. Es posible que vea Hola mensaje de error siguiente cuando Hola autenticación **expira el token**: error de operación de credenciales: concesión_no_válida - AADSTS70002: Error al validar las credenciales. AADSTS70008: Hola proporciona concesión de acceso expiró o se revocó. Id. de seguimiento: d18629e8-af88-43c5-88e3-d8419eb1fca1 Id. de correlación: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Marca de tiempo: 2015-12-15 21:09:31Z

| Tipo de usuario | Expira después de |
|:--- |:--- |
| Cuentas de usuario NO administradas por Azure Active Directory (@hotmail.com, @live.com, etc.) |12 horas |
| Cuentas de usuario administradas por Azure Active Directory (AAD) |Ejecute 14 días después de último segmento de Hola. <br/><br/>Noventa días, si un segmento basado en el servicio vinculado basado en OAuth se ejecuta al menos una vez cada catorce días. |

tooavoid/resolve este error, volver a autorizar mediante hello **Authorize** botón cuando hello **expira el token** y vuelva a implementar el servicio de hello vinculado. También puede generar valores para las propiedades **sessionId** y **authorization** mediante programación, para lo que usará el código siguiente:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Vea [azuredatalakestorelinkedservice clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), y [AuthorizationSessionGetResponse clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) temas para obtener más información acerca de clases de factoría de datos de hello utilizadas en el código de hello. Agregue una referencia a: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll para hello WindowsFormsWebAuthenticationDialog clase. 

## <a name="azure-sql-linked-service"></a>Servicio vinculado SQL de Azure
Crear un servicio vinculado de SQL Azure y usarlo con hello [actividad de procedimiento almacenado](data-factory-stored-proc-activity.md) tooinvoke un procedimiento almacenado desde una canalización del generador de datos. Vea el artículo [Conector SQL de Azure](data-factory-azure-sql-connector.md#linked-service-properties) para más información sobre este servicio vinculado.

## <a name="azure-sql-data-warehouse-linked-service"></a>Servicio vinculado del Almacenamiento de datos SQL de Azure
Crear un servicio de almacenamiento de datos de SQL Azure vinculado y usarlo con hello [actividad de procedimiento almacenado](data-factory-stored-proc-activity.md) tooinvoke un procedimiento almacenado desde una canalización del generador de datos. Consulte el artículo sobre el [conector de Almacenamiento de datos SQL de Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) para más información acerca de este servicio vinculado.

## <a name="sql-server-linked-service"></a>Servicio vinculado de SQL Server
Crear un servicio de SQL Server vinculado y usarlo con hello [actividad de procedimiento almacenado](data-factory-stored-proc-activity.md) tooinvoke un procedimiento almacenado desde una canalización del generador de datos. Consulte el artículo sobre el [conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties) para más información acerca de este servicio vinculado.

