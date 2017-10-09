---
title: datos aaaQuery de HDFS compatible con el almacenamiento de Azure - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooquery datos desde almacenamiento de Azure y almacén de Azure Data Lake toostore da como resultado del análisis."
keywords: blob storage, hdfs, datos estructurados, datos no estructurados, data lake store, entrada Hadoop, salida Hadoop, almacenamiento hadoop, entrada hdfs, salida hdfs, almacenamiento hdfs, wasb azure
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a>Uso de Azure Storage con clústeres de Azure HDInsight

tooanalyze datos en clúster de HDInsight, puede almacenar datos de hello en el almacenamiento de Azure, el almacén de Azure Data Lake o ambos. Ambas opciones de almacenamiento le permiten eliminar toosafely clústeres de HDInsight que se usan para el cálculo sin perder los datos de usuario.

Hadoop admite una noción de sistema de archivos predeterminado de Hola. sistema de archivos predeterminado de Hello implica un esquema predeterminado y la entidad. También puede ser tooresolve usa rutas de acceso relativas. Durante el proceso de creación de clúster de HDInsight de hello, puede especificar un contenedor de blobs en almacenamiento de Azure como sistema de archivos predeterminado de Hola o con HDInsight 3.5, puede seleccionar el almacenamiento de Azure o almacén de Azure Data Lake como sistema de archivos predeterminado de hello con unas pocas excepciones. Por motivos de compatibilidad de hello del uso de almacén de Data Lake como valor predeterminado de Hola y almacenamiento vinculado, vea [Availabilities para clúster de HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).

En este artículo, aprenderá cómo funciona Azure Storage con clústeres de HDInsight. toolearn cómo funciona el almacén de Data Lake con los clústeres de HDInsight, vea [clústeres de almacén de Data Lake utilice Azure con HDInsight de Azure](hdinsight-hadoop-use-data-lake-store.md). Consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obtener información sobre la creación de un clúster de HDInsight.

Azure Storage es una solución de almacenamiento sólida y de uso general, que se integra sin problemas con HDInsight. HDInsight puede usar un contenedor de blobs en almacenamiento de Azure como sistema de archivos predeterminado de Hola para clúster de Hola. A través de una interfaz (HDFS) del sistema de archivos distribuido de Hadoop, conjunto completo de Hola de componentes de HDInsight puede trabajar directamente en los datos estructurados o no estructurados almacenados como blobs.

> [!WARNING]
> Hay varias opciones disponibles al crear una cuenta de Azure Storage. Hello en la tabla siguiente proporciona información sobre qué opciones son compatibles con HDInsight:
> 
> | Tipo de cuenta de almacenamiento | Capa de almacenamiento | Compatible con HDInsight |
> | ------- | ------- | ------- |
> | Cuenta de almacenamiento de uso general | Estándar | __Sí__ |
> | &nbsp; | Premium | No |
> | Cuenta de Blob Storage | Acceso frecuente | No |
> | &nbsp; | Acceso esporádico | No |

No se recomienda que utilice contenedor de blob de hello predeterminado para almacenar los datos empresariales. Eliminar el contenedor de blob de hello predeterminado después de cada tooreduce de uso coste de almacenamiento es una buena práctica. Tenga en cuenta ese contenedor predeterminado de hello contiene la aplicación y del sistema registros. Asegúrese de registros de hello tooretrieve seguro antes de eliminar el contenedor de Hola.

No se permite compartir un contenedor de blobs entre varios clústeres.

## <a name="hdinsight-storage-architecture"></a>Arquitectura de almacenamiento de HDInsight
Hola siguiente diagrama proporciona una vista de resumen de hello HDInsight arquitectura de almacenamiento de información de uso de almacenamiento de Azure:

![Clústeres de Hadoop usar Hola HDFS API tooaccess y almacenan datos estructurados y no en el almacenamiento de blobs. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Arquitectura de almacenamiento de HDInsight")

HDInsight proporciona toohello distribuida filesystem acceso localmente adjunta toohello nodos de proceso. Puede tener acceso a este sistema de archivos mediante Hola completo URI, por ejemplo:

    hdfs://<namenodehost>/<path>

Además, HDInsight le permite tooaccess datos que se almacenan en el almacenamiento de Azure. Hola sintaxis es:

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

A la hora de usar una cuenta de Azure Storage con clústeres de HDInsight, es necesario tener en cuenta algunas cosas.

* **Contenedores de las cuentas de almacenamiento de Hola que son tooa conectado con clústeres:** debido a nombre de la cuenta de hello y la clave están asociados con el clúster de Hola durante la creación, tienen blobs de toohello de acceso completa en estos contenedores.

* **Contenedores públicos o blobs públicos de las cuentas de almacenamiento que no están conectados clúster tooa:** tiene blobs de toohello de permiso de solo lectura en los contenedores de Hola.
  
  > [!NOTE]
  > Contenedores públicos permiten tooget una lista de todos los blobs que están disponibles en ese contenedor y obtener metadatos del contenedor. Blobs públicos permiten blobs de hello tooaccess únicamente si sabe Hola la misma dirección URL. Para obtener más información, consulte <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">restringir acceso toocontainers y blobs</a>.
  > 
  > 
* **Contenedores privados de las cuentas de almacenamiento que no están conectados clúster tooa:** no puede acceder a blobs de hello en contenedores de Hola a menos que defina la cuenta de almacenamiento de hello al enviar trabajos de hello WebHCat. Esto se explica posteriormente en este artículo.

cuentas de almacenamiento de Hola que se definen en el proceso de creación de hello y sus claves están almacenadas en %HADOOP_HOME%/conf/core-site.xml en nodos de clúster de Hola. comportamiento predeterminado de Hola de HDInsight es cuentas de almacenamiento de hello toouse definidas en el archivo de hello core-site.xml. Puede modificar esta configuración mediante [Ambari](./hdinsight-hadoop-manage-ambari.md)

Varios trabajos de WebHCat, incluidos Hive, MapReduce, streaming de Hadoop y Pig, pueden llevar una descripción de cuentas de almacenamiento y metadatos con ellos. (Actualmente esto funciona para Pig con cuentas de almacenamiento pero no para metadatos). Para obtener más información, consulte [Uso de un clúster de HDInsight con cuentas de almacenamiento y tiendas de metadatos alternativas](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).

Los blobs se pueden usar para datos estructurados y no estructurados. Los contenedores de blobs almacenan los datos como pares de clave-valor y no hay jerarquía de directorios. Sin embargo, puede usarse el carácter de barra diagonal (/) de hello en Hola toomake de nombre de la clave parece como si un archivo se almacena en una estructura de directorios. Por ejemplo, la clave de un blob puede ser *input/log1.txt*. No real *entrada* directorio existe, pero debido toohello presencia del carácter de barra diagonal de hello en nombre de clave de hello, tiene el aspecto de Hola de una ruta de acceso de archivo.

## <a id="benefits"></a>Ventajas de Azure Storage
Hola implícito costo de rendimiento de los clústeres de cálculo no comparte ubicación y recursos de almacenamiento se mitiga con la forma de hello clústeres de cálculo de Hola se crean recursos toohello cerrar de la cuenta de almacenamiento dentro de hello región de Azure, en red de alta velocidad Hola facilita eficaz para los nodos de proceso de hello tooaccess Hola datos dentro de almacenamiento de Azure.

Hay varias ventajas asociados al almacenamiento de datos de hello en el almacenamiento de Azure en lugar de HDFS:

* **Compartir y reutilizar los datos:** datos hello en HDFS se encuentran dentro del clúster de cálculo de Hola. Solo las aplicaciones de Hola que tienen acceso toohello compute Cluster Server puede usar datos de hello mediante las API de HDFS. pueden tener acceso a datos de Hello en el almacenamiento de Azure a través de API de HDFS Hola o hello [API de REST de almacenamiento de blobs][blob-storage-restAPI]. Por lo tanto, un conjunto mayor de aplicaciones (incluidos los otros clústeres de HDInsight) y las herramientas puede ser utilizado tooproduce y consumir datos de Hola.
* **Archivado de datos:** almacenar datos en el almacenamiento de Azure permite a los clústeres de HDInsight de hello usa para eliminar de forma segura sin perder los datos de usuario de toobe de cálculo.
* **Costo de almacenamiento de datos:** almacenar datos en DFS para a largo plazo de hello es más costoso que almacenamiento de datos de hello en el almacenamiento de Azure porque el costo de Hola de un clúster de cálculo es mayor que el costo de Hola de almacenamiento de Azure. Además, porque los datos de hello no tienen toobe volver a cargar para cada generación de clúster de proceso, también se guardan los costos de la carga de datos.
* **Escalado horizontal elástico:** HDFS aunque se proporciona con un sistema de archivos de escala horizontal, escala Hola viene determinado por el número de Hola de nodos que se crean para el clúster. Cambiar escala Hola puede convertirse en un proceso más complicado que depender de elásticas Hola escalar las capacidades que se obtienen automáticamente en el almacenamiento de Azure.
* **Replicación geográfica:** su almacenamiento de Azure Storage se puede replicar geográficamente. Aunque esta opción permite la recuperación geográfica y redundancia de datos, una ubicación de replicación geográfica de conmutación por error toohello afecta gravemente el rendimiento y pueden suponer costes adicionales. Por lo que esta es nuestra recomendación es toochoose Hola replicación geográfica con cuidado y sólo si es valor de Hola de los datos de hello correspondientes Hola costo adicional alguno.

Ciertos trabajos MapReduce y paquetes pueden crear resultados intermedios que realmente no desea toostore en almacenamiento de Azure. En ese caso, puede elegir datos de hello toostore en Hola HDFS local. De hecho, HDInsight usa DFS para varios de estos resultados intermedios en los trabajos de Hive y otros procesos.

> [!NOTE]
> La mayoría de los comandos HDFS (por ejemplo, <b>ls</b>, <b>copyFromLocal</b> y <b>mkdir</b>) siguen funcionando según lo previsto. Hola sólo los comandos que son específicos toohello nativo HDFS la implementación (que es lo que se conoce tooas DFS), como <b>fschk</b> y <b>dfsadmin</b>, mostrar un comportamiento diferente en el almacenamiento de Azure.
> 
> 

## <a name="create-blob-containers"></a>Creación de contenedores de blobs
toouse blobs, cree primero un [cuenta de almacenamiento de Azure][azure-storage-create]. Como parte de esto, especifique una región de Azure donde se crea la cuenta de almacenamiento de Hola. clúster de Hola y cuenta de almacenamiento de hello deben estar hospedados en hello misma región. base de datos de SQL Server de tienda de metadatos de Hello Hive y tienda de metadatos de Oozie SQL Server, base de datos también debe estar ubicado en Hola misma región.

Siempre que vive, cada blob que se crea pertenece tooa contenedor en la cuenta de almacenamiento de Azure. Este contenedor puede ser un blob existente creado fuera de HDInsight, o bien un contenedor que se crea para un clúster de HDInsight.

contenedor de Blob de Hello predeterminado almacena información específica del clúster como registros y el historial de trabajos. No comparta un contenedor de blobs predeterminado con varios clústeres de HDInsight. Se podría dañar el historial de trabajos. Se recomienda toouse un contenedor diferente para cada clúster y colocar los datos compartidos en una cuenta de almacenamiento vinculado especificada en la implementación de todos los clústeres en lugar de la cuenta de almacenamiento predeterminada de Hola. Para más información acerca de cómo configurar cuentas de almacenamiento vinculadas, consulte [Creación de clústeres de HDInsight][hdinsight-creation]. Sin embargo puede reutilizar un contenedor de almacenamiento de forma predeterminada una vez se ha eliminado el clúster de HDInsight original de Hola. Para los clústeres de HBase, realmente puede conservar datos y esquema de la tabla de hello HBase mediante la creación de un nuevo clúster de HBase mediante el contenedor de blobs de hello predeterminado utilizado por un clúster de HBase que se ha eliminado.

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a>Usar hello portal de Azure
Al crear un clúster de HDInsight desde el Portal de hello, tiene detalles de la cuenta de hello opciones (tal y como se muestra a continuación) tooprovide Hola almacenamiento. También puede especificar si desea que una cuenta de almacenamiento adicionales asociados con el clúster de hello y, si es así, elija desde otro blob de almacenamiento de Azure como almacenamiento adicional de Hola o de almacén de Data Lake.

![Origen de datos de creación de un clúster de Hadoop en HDInsight](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> No se admite con una cuenta de almacenamiento adicional en una ubicación diferente que el clúster de HDInsight Hola.


### <a name="use-azure-powershell"></a>Uso de Azure PowerShell
Si se [instalado y configurado Azure PowerShell][powershell-install], puede usar Hola siguientes de hello Azure PowerShell prompt toocreate una cuenta de almacenamiento y el contenedor:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a>Uso de CLI de Azure

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

Si tiene [instalado y configurado hello Azure CLI](../cli-install-nodejs.md), siguiente Hola comando puede ser usado tooa cuenta de almacenamiento y el contenedor.

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> Hola `--type` parámetro indica cómo se replica la cuenta de almacenamiento de Hola. Para obtener más información, vea [Replicación de Azure Storage](../storage/storage-redundancy.md). No utilice ZRS, ya que no admite blob en páginas, archivo, tabla o cola.
> 
> 

Son región geográfica de toospecify solicitadas Hola que se crea la cuenta de almacenamiento de hello en. Debe crear cuenta de almacenamiento de Hola Hola misma región que piensa sobre la creación de su clúster de HDInsight.

Una vez creada la cuenta de almacenamiento de hello, utilice Hola después de claves de la cuenta de almacenamiento de comando tooretrieve hello:

    azure storage account keys list <storageaccountname>

toocreate un contenedor, use Hola siguiente comando:

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a>Archivos adicionales en Azure Storage
es el esquema URI de Hello para tener acceso a archivos de almacenamiento de Azure de HDInsight:

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

esquema URI de Hello proporciona acceso sin cifrar (con hello *wasb:* prefijo) y acceso de cifrado de SSL (con *wasbs*). Se recomienda usar *wasbs* siempre que sea posible, incluso cuando el acceso a datos que residen dentro de Hola misma región de Azure.

Hola &lt;BlobStorageContainerName&gt; identifica Hola nombre de contenedor de blobs de hello en el almacenamiento de Azure.
Hola &lt;StorageAccountName&gt; identifica el nombre de cuenta de almacenamiento de Azure de Hola. Se necesita el nombre completo de dominio (FQDN).

Si no &lt;BlobStorageContainerName&gt; ni &lt;StorageAccountName&gt; se ha especificado, se utiliza el sistema de archivos predeterminado de Hola. Para los archivos de hello en el sistema de archivos predeterminado de hello, puede usar una ruta de acceso relativa o absoluta. Por ejemplo, hello *archivo hadoop mapreduce examples.jar* archivo que se incluye con clústeres de HDInsight puede tooby que se hace referencia mediante uno de los siguientes hello:

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> nombre de archivo de Hello es <i>archivo hadoop-examples.jar</i> en clústeres de HDInsight las versiones 2.1 y 1.6.
> 
> 

Hola &lt;ruta de acceso&gt; es el nombre de ruta de acceso HDFS de archivo o directorio Hola. Dado que los contenedores de Azure Storage son solamente almacenes de pares clave-valor, no hay ningún sistema de archivos jerárquico real. Un carácter de barra inclinada ( / ) dentro de la clave de blob se interpreta como separador de directorios. Por ejemplo, nombre de blob de Hola para *archivo hadoop mapreduce examples.jar* es:

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> Cuando se trabaja con los blobs fuera de HDInsight, mayoría de las utilidades no reconoce el formato WASB de Hola y en su lugar, espera un formato básico de la ruta de acceso, como `example/jars/hadoop-mapreduce-examples.jar`.
> 
> 

## <a name="access-blobs"></a>Acceso a blobs 


### <a name="access-blobs-using-azure-powershell"></a> Uso de Azure PowerShell
> [!NOTE]
> comandos de Hello en esta sección proporcionan un ejemplo básico de usar PowerShell tooaccess datos almacenados en blobs. Para obtener un ejemplo más completo que se personaliza para trabajar con HDInsight, vea hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).
> 
> 

Usar hello después comando toolist Hola relacionados con el blob cmdlets:

    Get-Command *blob*

![Lista de cmdlets de PowerShell relacionados con el blob.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a>Carga de archivos
Vea [cargar datos tooHDInsight][hdinsight-upload-data].

#### <a name="download-files"></a>Descarga de archivos
Hello secuencia de comandos siguiente descarga una carpeta en la toohello de blob de bloque actual. Antes de ejecutar script de Hola, cambiar carpeta del directorio de hello tooa que tiene permisos de escritura.

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

Proporcionar el nombre de grupo de recursos de Hola y el nombre de clúster de hello, puede usar Hola siguiente código:

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a>Eliminar archivos
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a>Enumerar archivos
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a>Ejecutar consultas de Hive usando una cuenta de almacenamiento sin definir
Este ejemplo muestra cómo toolist una carpeta de la cuenta de almacenamiento que no está definido durante Hola proceso de creación.
$clusterName = "<HDInsightClusterName>"

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a>Uso de CLI de Azure
Usar hello siga los comandos relacionados con el blob del comando toolist hello:

    azure storage blob

**Ejemplo del uso de tooupload un archivo de CLI de Azure**

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Ejemplo del uso de toodownload un archivo de CLI de Azure**

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

**Ejemplo del uso de CLI de Azure toodelete un archivo**

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Ejemplo del uso de archivos de toolist de CLI de Azure**

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a>Uso de cuentas de almacenamiento adicionales

Al crear un clúster de HDInsight, especificar cuenta de almacenamiento de Azure de Hola que desee tooassociate con él. Además toothis cuenta de almacenamiento, puede agregar cuentas de almacenamiento adicional de hello misma suscripción de Azure o suscripciones de Azure diferentes durante el proceso de creación de Hola o después de que se ha creado un clúster. Para obtener instrucciones sobre cómo agregar más cuentas de almacenamiento, consulte [Creación de clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

> [!WARNING]
> No se admite con una cuenta de almacenamiento adicional en una ubicación diferente que el clúster de HDInsight Hola.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, se habrá aprendido cómo toouse HDFS compatible con el almacenamiento de Azure con HDInsight. Esto le permite toobuild escalable y a largo plazo, archivado soluciones de adquisición de datos y usar información de hello toounlock de HDInsight dentro de hello almacenado estructurado y datos no estructurados.

Para más información, consulte:

* [Introducción a Azure HDInsight][hdinsight-get-started]
* [Introducción Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)
* [Cargar datos tooHDInsight][hdinsight-upload-data]
* [Uso de Hive con HDInsight][hdinsight-use-hive]
* [Uso de Pig con HDInsight][hdinsight-use-pig]
* [Usar firmas de acceso compartido de almacenamiento de Azure toorestrict acceso toodata con HDInsight][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
