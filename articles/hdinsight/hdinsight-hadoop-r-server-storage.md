---
title: soluciones de almacenamiento de aaaAzure para R Server en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de opciones de almacenamiento diferente Hola disponible toousers con R Server en HDInsight"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: ff5e80fee14d5e74cbc22e873e6bc1439a3b6037
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a>Soluciones de Azure Storage para R Server en HDInsight

Microsoft R Server en HDInsight presenta una variedad de datos de toopersist de soluciones de almacenamiento, código u objetos que contienen los resultados del análisis. Estas incluyen hello siguientes opciones:

- [Azure Blob](https://azure.microsoft.com/services/storage/blobs/)
- [Almacén de Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/)
- [Azure File Storage](https://azure.microsoft.com/services/storage/files/)

También tiene opción de Hola de obtener acceso a varias cuentas de almacenamiento de Azure o contenedores con el clúster HDI. Almacenamiento de archivos de Azure es una opción de almacenamiento de datos adecuada para su uso en el nodo de borde de Hola que le permite toomount un recurso compartido de archivos de almacenamiento de Azure para, por ejemplo, sistema de archivos de hello Linux. Pero los recursos compartidos de Azure File se pueden montar y utilizar en cualquier sistema que tenga un sistema operativo compatible, como Windows o Linux. 

Cuando se crea un clúster de Hadoop en HDInsight, se especifica una cuenta de **Azure Storage** o una de **Data Lake Store**. Un contenedor de almacenamiento específico de esa cuenta contiene sistema de archivos de Hola para clúster Hola creados por usted (por ejemplo, hello sistema de archivos distribuido de Hadoop). Para más información e instrucciones, consulte:

- [Uso de Azure Storage con HDInsight](hdinsight-hadoop-use-blob-storage.md)
- [Uso de Data Lake Store con clústeres de Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md) 

Para obtener más información sobre soluciones de almacenamiento de Azure de hello, consulte [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md). 

Para obtener instrucciones sobre cómo seleccionar hello toouse de opción de almacenamiento más adecuado para su escenario, consulte [decidir cuando toouse Blobs de Azure, archivos de Azure o discos de datos de Azure](../storage/common/storage-decide-blobs-files-disks.md) 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a>Uso de cuentas de Azure Blob Storage con R Server

Si es necesario, se puede acceder a varias cuentas de almacenamiento o contenedores de Azure con el clúster de HDI. toodo por lo tanto, necesita cuentas de almacenamiento adicionales toospecify Hola Hola interfaz de usuario al crear el clúster de hello y, a continuación, siga estos pasos toouse con R Server.

> [!WARNING]
> Para optimizar el rendimiento, clúster de HDInsight de Hola se crea en Hola mismo centro de datos como cuenta de almacenamiento principal de Hola que especifique. No se admite el uso de una cuenta de almacenamiento en una ubicación diferente que el clúster de HDInsight de Hola.

1. Cree un clúster de HDInsight con el nombre de cuenta de almacenamiento **storage1** y un contenedor predeterminado denominado **container1**.
2. Especifique una cuenta de almacenamiento adicional con el nombre **storage2**.  
3. Copie el directorio /share toohello de hello mycsv.csv archivo y realizar análisis en ese archivo.  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. En el código de R, establecer el nodo de nombre de hello demasiado**de manera predeterminada,** y establecer su tooprocess de archivos y directorios.  

        myNameNode <- "default"
        myPort <- 0

        #Location of hello data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define hello Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify hello input file tooanalyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

Todos Hola directorio y archivo de la cuenta de almacenamiento de punto toohello referencias wasb://container1@storage1.blob.core.windows.net. Se trata de hello **cuenta de almacenamiento predeterminada** asociado con el clúster de HDInsight Hola.

Ahora, suponga que desea tooprocess un archivo denominado mySpecial.csv que se encuentra en hello /private directorio de **container2** en **: storage2**.

En el código de R, seleccione Hola nombre nodo referencia toohello **: storage2** cuenta de almacenamiento.


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of hello data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify hello input file tooanalyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

Todo de hello archivos y directorios referencias ahora punto toohello cuenta de almacenamiento wasb://container2@storage2.blob.core.windows.net. Se trata de hello **nombre de nodo** que ha especificado.

Tienes tooconfigure Hola/User/RevoShare/<SSH username> directorio **: storage2** como se indica a continuación:


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a>Uso de una instancia de Azure Data Lake Store con R Server

toouse Data Lake almacena con su cuenta de HDInsight, debe toogive tu tienda de Azure Data Lake tooeach de acceso de clúster que desea toouse. Para obtener instrucciones sobre cómo toouse Hola toocreate portal Azure HDInsight de un clúster con una cuenta de almacén de Azure Data Lake como almacenamiento predeterminado de Hola o como un almacén adicional, consulte [crear un clúster de HDInsight con el almacén de Data Lake mediante el portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

A continuación, utiliza Hola almacén en el script de R mucho como hizo una cuenta de almacenamiento de Azure secundario como se describe en el procedimiento anterior de Hola.

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a>Agregar clúster acceso tooyour que almacena Azure Data Lake
El acceso a un almacén de Azure Data Lake se establece mediante el uso de una entidad de servicio de Azure Active Directory (AAD) asociada a su clúster de HDInsight.

tooadd una entidad de seguridad de servicio de Azure AD:

1. Cuando se crea el clúster de HDInsight, seleccione **identidad de AAD de clúster** de hello **origen de datos** ficha.

2. Hola **identidad de AAD de clúster** cuadro de diálogo **Seleccionar entidad de servicio de AD**, seleccione **crear nuevo**.

Cuando asigne un nombre a Hola entidad de servicio y crear una contraseña para él, haga clic en **administrar el acceso a ADLS** hello tooassociate almacena la entidad de servicio con su Data Lake.

También es posible tooadd clúster acceso tooone o más Data Lake almacena después de crear el clúster. Abra hello Azure entrada portal para un almacén de Data Lake y vaya demasiado**Explorador de datos > acceso > agregar**. 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a>¿Cómo tooaccess Hola almacén Data Lake de R Server

Una vez que se le ha dado el almacén de Data Lake tooa acceso, puede usar el almacén de hello en R Server en forma de hello HDInsight que lo haría con una cuenta de almacenamiento de Azure secundario. Hola solo diferencia es ese prefijo hello **wasb: / /** cambia demasiado**adl: / /** como se indica a continuación:


    # Point toohello ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of hello data (assumes a /share directory on hello ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify hello input file in HDFS tooanalyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of hello week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define hello data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


Hello siguientes comandos son tooconfigure usado Hola cuenta de almacenamiento de Data Lake con directorio de hello RevoShare y agregar el archivo .csv de ejemplo de Hola del anterior ejemplo de Hola:


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a>Uso de Azure File Storage con R Server

También hay una opción de almacenamiento de datos adecuada para su uso en el nodo de hello borde llamada [archivos de Azure] ((https://azure.microsoft.com/services/storage/files/). Le permite toomount un toohello de recurso compartido de archivos de almacenamiento de Azure sistema de archivos de Linux. Esta opción puede resultar útil para almacenar los archivos de datos, los scripts de R y objetos de resultado que podrían ser necesaria una versión posterior, especialmente cuando lo hace el sistema de archivos nativo de sentido toouse hello en el nodo del borde de hello en lugar de HDFS. 

Una de las ventajas principal de los archivos de Azure es ese archivo hello recursos compartidos se pueden montar y utilizados por cualquier sistema que tenga un sistema operativo compatible, como Windows o Linux. Por ejemplo, puede utilizarse con otro clúster de HDInsight que sea suyo o de alguien de su equipo, con una máquina virtual de Azure, o incluso con un sistema local. Para más información, consulte:

- [¿Cómo toouse almacenamiento de archivos de Azure con Linux](../storage/files/storage-how-to-use-files-linux.md)
- [¿Cómo toouse almacenamiento de archivos de Azure en Windows](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a>Pasos siguientes

Ahora que sabe opciones de almacenamiento de Azure de hello, siguientes de Hola de uso vínculos toodiscover maneras de obtener las tareas de ciencia de datos que realiza con el servidor de R en HDInsight.

* [Información general de R Server en HDInsight (versión preliminar)](hdinsight-hadoop-r-server-overview.md)
* [Introducción al servidor de R en Hadoop](hdinsight-hadoop-r-server-get-started.md)
* [Agregar servidor RStudio tooHDInsight (si no se agregan durante la creación del clúster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opciones de contexto de proceso para R Server en HDInsight (versión preliminar)](hdinsight-hadoop-r-server-compute-contexts.md)

