---
title: "aaaUse almacén de Data Lake con Hadoop en HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooquery datos de almacén de Azure Data Lake y toostore da como resultado del análisis."
keywords: blob storage,hdfs,datos estructurados,datos no estructurados, data lake store
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a>Uso de Data Lake Store con clústeres de Azure HDInsight

datos de tooanalyze de clúster de HDInsight, puede almacenar datos de Hola o en [el almacenamiento de Azure](../storage/common/storage-introduction.md), [almacén de Azure Data Lake](../data-lake-store/data-lake-store-overview.md), o ambos. Ambas opciones de almacenamiento le permiten eliminar toosafely clústeres de HDInsight que se usan para el cálculo sin perder los datos de usuario.

En este artículo, aprenderá cómo funciona Data Lake Store con clústeres de HDInsight. toolearn cómo funciona el almacenamiento de Azure con los clústeres de HDInsight, vea [Use el almacenamiento de Azure con HDInsight de Azure clústeres](hdinsight-hadoop-use-blob-storage.md). Consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obtener información sobre la creación de un clúster de HDInsight.

> [!NOTE]
> Para acceder a Azure Data Lake Store siempre se usa un canal seguro, así que no hay ningún nombre de esquema de sistema de archivos `adls`. Usa siempre `adl`.
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a>Disponibilidades para clústeres de HDInsight

Hadoop admite una noción de sistema de archivos predeterminado de Hola. sistema de archivos predeterminado de Hello implica un esquema predeterminado y la entidad. También puede ser tooresolve usa rutas de acceso relativas. Durante el proceso de creación de clúster de HDInsight de hello, puede especificar un contenedor de blobs en almacenamiento de Azure como sistema de archivos predeterminado de Hola o con HDInsight 3.5 y versiones más recientes, puede seleccionar el almacenamiento de Azure o almacén de Azure Data Lake como sistema de archivos predeterminado de hello con un algunas excepciones. 

Los clústeres de HDInsight pueden usar Data Lake Store de dos maneras:

* Como almacenamiento predeterminado de Hola
* Como almacenamiento adicional, con Azure Storage Blob como almacenamiento predeterminado.

A partir de ahora, solo algunas de ellas hello HDInsight clúster tipos/compatibles con las versiones con el almacén de Data Lake como almacenamiento predeterminado y cuentas de almacenamiento adicionales:

| Tipo de clúster de HDInsight | Data Lake Store como almacenamiento predeterminado | Data Lake Store como almacenamiento adicional| Notas |
|------------------------|------------------------------------|---------------------------------------|------|
| HDInsight versión 3.6 | Sí | Sí | |
| Versión de HDInsight 3.5 | Sí | Sí | Con excepción de Hola de HBase|
| Versión de HDInsight 3.4 | No | Sí | |
| HDInsight versión 3.3 | No | No | |
| HDInsight versión 3.2 | No | Sí | |
| HDInsight Premium (nivel)| No | No | |
| Storm | | |Puede usar datos de almacén de Data Lake toowrite de una topología de Storm. Puede usar Data Lake Store para datos de referencia que luego puede leer una topología de Storm.|

Usar almacén de Data Lake como una cuenta de almacenamiento adicional no afecten al rendimiento o tooread de capacidad de Hola o escribir tooAzure almacenamiento en clúster de Hola.


## <a name="use-data-lake-store-as-default-storage"></a>Uso de Data Lake Store como almacenamiento predeterminado

Cuando HDInsight se implementa con el almacén de Data Lake como almacenamiento de forma predeterminada, los archivos relacionados con el clúster de Hola se almacenan en el almacén de Data Lake en hello ubicación siguiente:

    adl://mydatalakestore/<cluster_root_path>/

donde `<cluster_root_path>` es el nombre de Hola de una carpeta se crea en el almacén de Data Lake. Al especificar una ruta de acceso raíz para cada clúster, puede usar Hola la misma cuenta de almacén de Data Lake para más de un clúster. Por lo tanto, puede tener una configuración donde:

* Cluster1 puede usar la ruta de acceso de Hola`adl://mydatalakestore/cluster1storage`
* Usar ruta de acceso de hello Cluster2`adl://mydatalakestore/cluster2storage`

Observe que ambos Hola de uso de clústeres Hola misma cuenta de almacén de Data Lake **mydatalakestore**. Cada clúster tiene acceso tooits posee filesystem raíz en el almacén de Data Lake. Hola experiencia de implementación de portal de Azure en particular le pide que toouse un nombre de carpeta como **/clusters/\<clustername >** para la ruta de acceso de hello raíz.

toouse toobe capaz de un almacén de Data Lake como almacenamiento predeterminado, debe conceder toohello de acceso principal de servicio de hello siguiendo las rutas de acceso:

- raíz de cuenta de almacén de Data Lake Hola.  Por ejemplo: adl://mydatalakestore/.
- carpeta de Hola para todas las carpetas de clúster.  Por ejemplo: adl://mydatalakestore/clusters.
- carpeta de Hello para el clúster de Hola.  Por ejemplo: adl://mydatalakestore/clusters/cluster1storage.

Para más información sobre cómo crear la entidad de servicio y concederle acceso, consulte [Configuración del acceso a Data Lake Store](#configure-data-lake-store-access).


## <a name="use-data-lake-store-as-additional-storage"></a>Uso de Data Lake Store como almacenamiento adicional

Puede usar almacén de Data Lake como almacenamiento adicional para clúster de hello así. En tales casos, almacenamiento de hello clúster predeterminado puede ser un Blob de almacenamiento de Azure o una cuenta de almacén de Data Lake. Si se ejecutan trabajos de HDInsight con datos de hello almacenados en el almacén de Data Lake como almacenamiento adicional, debe usar archivos de toohello de ruta de acceso completa de Hola. Por ejemplo:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Tenga en cuenta que no hay ningún **cluster_root_path** en dirección URL de hello ahora. Eso es porque el almacén de Data Lake un almacenamiento predeterminado en este caso no es por lo que todo lo que necesita toodo es proporcionar a los archivos de toohello de ruta de acceso de Hola.

toouse toobe capaz de un almacén de Data Lake como almacenamiento adicional, solo necesita toogrant Hola servicio principal toohello las rutas de acceso donde se almacenan los archivos.  Por ejemplo:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Para más información sobre cómo crear la entidad de servicio y concederle acceso, consulte [Configuración del acceso a Data Lake Store](#configure-data-lake-store-access).


## <a name="use-more-than-one-data-lake-store-accounts"></a>Uso de más de una cuenta de Data Lake Store

Agregar una cuenta de almacén de Data Lake como adicionales y agregar más de un almacén de Data Lake cuentas se llevan a cabo por da permiso al clúster HDInsight hello en los datos en una o más cuentas de almacén de Data Lake. Consulte [Configuración del acceso a Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Configuración del acceso a Data Lake Store

tooconfigure acceso al almacén de Data Lake desde el clúster de HDInsight, debe tener una entidad de servicio de Azure Active directory (Azure AD). Solo un administrador de Azure AD puede crear una entidad de servicio. entidad de servicio de Hello debe crearse con un certificado. Para más información, consulte [Configuración del acceso a Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) y [Creación de una entidad de servicio con un certificado autofirmado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).

> [!NOTE]
> Si va a almacén de toouse Azure Data Lake como almacenamiento adicional para el clúster de HDInsight, se recomienda hacer esto al crear el clúster de hello tal como se describe en este artículo. Agregar almacén de Azure Data Lake como almacenamiento adicional tooan clúster de HDInsight existente es un proceso complicado y propensa a tooerrors.
>

## <a name="access-files-from-hello-cluster"></a>Acceder a los archivos del clúster de Hola

Hay varias maneras se pueden acceder a archivos de hello en el almacén de Data Lake desde un clúster de HDInsight.

* **Con el nombre completo de hello**. Con este enfoque, se proporcionan archivos de toohello de ruta de acceso completa de Hola que desea tooaccess.

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* **Con formato de ruta de acceso abreviada hello**. Con este enfoque, reemplace la ruta de acceso de Hola de raíz de clúster toohello con adl: / / /. Por lo tanto, en el ejemplo de Hola anterior, puede reemplazar `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` con `adl:///`.

        adl:///<file path>

* **Usar ruta de acceso relativa de hello**. Con este enfoque, sólo se proporcionan archivos de toohello de ruta de acceso relativa de Hola que desea tooaccess. Por ejemplo, si hello archivo toohello de ruta de acceso completa es:

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    Puede tener acceso a Hola mismo archivo sample.log mediante esta ruta de acceso relativa en su lugar.

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a>Crear clústeres de HDInsight con acceso a almacén de tooData Lake

Usar hello siguientes vínculos para obtener instrucciones detalladas en forma de toocreate clústeres de HDInsight con acceso a tooData Lake almacén.

* [Uso del Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [Uso de PowerShell (con Data Lake Store como almacenamiento predeterminado)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Uso de PowerShell (con Data Lake Store como almacenamiento adicional)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [Uso de plantillas de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a>Pasos siguientes
En este artículo, se habrá aprendido cómo toouse almacén de Data Lake HDFS compatible con Azure con HDInsight. Esto le permite toobuild escalable y a largo plazo, archivado soluciones de adquisición de datos y usar información de hello toounlock de HDInsight dentro de hello almacenado estructurado y datos no estructurados.

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
