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
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="471e9-103">Soluciones de Azure Storage para R Server en HDInsight</span><span class="sxs-lookup"><span data-stu-id="471e9-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="471e9-104">Microsoft R Server en HDInsight presenta una variedad de datos de toopersist de soluciones de almacenamiento, código u objetos que contienen los resultados del análisis.</span><span class="sxs-lookup"><span data-stu-id="471e9-104">Microsoft R Server on HDInsight has a variety of storage solutions toopersist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="471e9-105">Estas incluyen hello siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="471e9-105">These include hello following options:</span></span>

- [<span data-ttu-id="471e9-106">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="471e9-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="471e9-107">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="471e9-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="471e9-108">Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="471e9-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="471e9-109">También tiene opción de Hola de obtener acceso a varias cuentas de almacenamiento de Azure o contenedores con el clúster HDI.</span><span class="sxs-lookup"><span data-stu-id="471e9-109">You also have hello option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="471e9-110">Almacenamiento de archivos de Azure es una opción de almacenamiento de datos adecuada para su uso en el nodo de borde de Hola que le permite toomount un recurso compartido de archivos de almacenamiento de Azure para, por ejemplo, sistema de archivos de hello Linux.</span><span class="sxs-lookup"><span data-stu-id="471e9-110">Azure File storage is a convenient data storage option for use on hello edge node that enables you toomount an Azure Storage file share to, for example, hello Linux file system.</span></span> <span data-ttu-id="471e9-111">Pero los recursos compartidos de Azure File se pueden montar y utilizar en cualquier sistema que tenga un sistema operativo compatible, como Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="471e9-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="471e9-112">Cuando se crea un clúster de Hadoop en HDInsight, se especifica una cuenta de **Azure Storage** o una de **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="471e9-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="471e9-113">Un contenedor de almacenamiento específico de esa cuenta contiene sistema de archivos de Hola para clúster Hola creados por usted (por ejemplo, hello sistema de archivos distribuido de Hadoop).</span><span class="sxs-lookup"><span data-stu-id="471e9-113">A specific storage container from that account holds hello file system for hello cluster that you create (for example, hello Hadoop Distributed File System).</span></span> <span data-ttu-id="471e9-114">Para más información e instrucciones, consulte:</span><span class="sxs-lookup"><span data-stu-id="471e9-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="471e9-115">Uso de Azure Storage con HDInsight</span><span class="sxs-lookup"><span data-stu-id="471e9-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="471e9-116">[Uso de Data Lake Store con clústeres de Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md)</span><span class="sxs-lookup"><span data-stu-id="471e9-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="471e9-117">Para obtener más información sobre soluciones de almacenamiento de Azure de hello, consulte [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="471e9-117">For more information on hello Azure storage solutions, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="471e9-118">Para obtener instrucciones sobre cómo seleccionar hello toouse de opción de almacenamiento más adecuado para su escenario, consulte [decidir cuando toouse Blobs de Azure, archivos de Azure o discos de datos de Azure](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="471e9-118">For guidance on selecting hello most appropriate storage option toouse for your scenario, see [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="471e9-119">Uso de cuentas de Azure Blob Storage con R Server</span><span class="sxs-lookup"><span data-stu-id="471e9-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="471e9-120">Si es necesario, se puede acceder a varias cuentas de almacenamiento o contenedores de Azure con el clúster de HDI.</span><span class="sxs-lookup"><span data-stu-id="471e9-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="471e9-121">toodo por lo tanto, necesita cuentas de almacenamiento adicionales toospecify Hola Hola interfaz de usuario al crear el clúster de hello y, a continuación, siga estos pasos toouse con R Server.</span><span class="sxs-lookup"><span data-stu-id="471e9-121">toodo so, you need toospecify hello additional storage accounts in hello UI when you create hello cluster, and then follow these steps toouse them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="471e9-122">Para optimizar el rendimiento, clúster de HDInsight de Hola se crea en Hola mismo centro de datos como cuenta de almacenamiento principal de Hola que especifique.</span><span class="sxs-lookup"><span data-stu-id="471e9-122">For performance purposes, hello HDInsight cluster is created in hello same data center as hello primary storage account that you specify.</span></span> <span data-ttu-id="471e9-123">No se admite el uso de una cuenta de almacenamiento en una ubicación diferente que el clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="471e9-123">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="471e9-124">Cree un clúster de HDInsight con el nombre de cuenta de almacenamiento **storage1** y un contenedor predeterminado denominado **container1**.</span><span class="sxs-lookup"><span data-stu-id="471e9-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="471e9-125">Especifique una cuenta de almacenamiento adicional con el nombre **storage2**.</span><span class="sxs-lookup"><span data-stu-id="471e9-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="471e9-126">Copie el directorio /share toohello de hello mycsv.csv archivo y realizar análisis en ese archivo.</span><span class="sxs-lookup"><span data-stu-id="471e9-126">Copy hello mycsv.csv file toohello /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="471e9-127">En el código de R, establecer el nodo de nombre de hello demasiado**de manera predeterminada,** y establecer su tooprocess de archivos y directorios.</span><span class="sxs-lookup"><span data-stu-id="471e9-127">In R code, set hello name node too**default,** and set your directory and file tooprocess.</span></span>  

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

<span data-ttu-id="471e9-128">Todos Hola directorio y archivo de la cuenta de almacenamiento de punto toohello referencias wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="471e9-128">All hello directory and file references point toohello storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="471e9-129">Se trata de hello **cuenta de almacenamiento predeterminada** asociado con el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="471e9-129">This is hello **default storage account** that's associated with hello HDInsight cluster.</span></span>

<span data-ttu-id="471e9-130">Ahora, suponga que desea tooprocess un archivo denominado mySpecial.csv que se encuentra en hello /private directorio de **container2** en **: storage2**.</span><span class="sxs-lookup"><span data-stu-id="471e9-130">Now, suppose you want tooprocess a file called mySpecial.csv that's located in hello  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="471e9-131">En el código de R, seleccione Hola nombre nodo referencia toohello **: storage2** cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="471e9-131">In your R code, point hello name node reference toohello **storage2** storage account.</span></span>


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

<span data-ttu-id="471e9-132">Todo de hello archivos y directorios referencias ahora punto toohello cuenta de almacenamiento wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="471e9-132">All of hello directory and file references now point toohello storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="471e9-133">Se trata de hello **nombre de nodo** que ha especificado.</span><span class="sxs-lookup"><span data-stu-id="471e9-133">This is hello **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="471e9-134">Tienes tooconfigure Hola/User/RevoShare/<SSH username> directorio **: storage2** como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="471e9-134">You have tooconfigure hello /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="471e9-135">Uso de una instancia de Azure Data Lake Store con R Server</span><span class="sxs-lookup"><span data-stu-id="471e9-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="471e9-136">toouse Data Lake almacena con su cuenta de HDInsight, debe toogive tu tienda de Azure Data Lake tooeach de acceso de clúster que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="471e9-136">toouse Data Lake stores with your HDInsight account, you need toogive your cluster access tooeach Azure Data Lake store that you want toouse.</span></span> <span data-ttu-id="471e9-137">Para obtener instrucciones sobre cómo toouse Hola toocreate portal Azure HDInsight de un clúster con una cuenta de almacén de Azure Data Lake como almacenamiento predeterminado de Hola o como un almacén adicional, consulte [crear un clúster de HDInsight con el almacén de Data Lake mediante el portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="471e9-137">For instructions on how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="471e9-138">A continuación, utiliza Hola almacén en el script de R mucho como hizo una cuenta de almacenamiento de Azure secundario como se describe en el procedimiento anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="471e9-138">You then use hello store in your R script much like you did a secondary Azure storage account as described in hello previous procedure.</span></span>

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a><span data-ttu-id="471e9-139">Agregar clúster acceso tooyour que almacena Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="471e9-139">Add cluster access tooyour Azure Data Lake stores</span></span>
<span data-ttu-id="471e9-140">El acceso a un almacén de Azure Data Lake se establece mediante el uso de una entidad de servicio de Azure Active Directory (AAD) asociada a su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="471e9-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="471e9-141">tooadd una entidad de seguridad de servicio de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="471e9-141">tooadd an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="471e9-142">Cuando se crea el clúster de HDInsight, seleccione **identidad de AAD de clúster** de hello **origen de datos** ficha.</span><span class="sxs-lookup"><span data-stu-id="471e9-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from hello **Data Source** tab.</span></span>

2. <span data-ttu-id="471e9-143">Hola **identidad de AAD de clúster** cuadro de diálogo **Seleccionar entidad de servicio de AD**, seleccione **crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="471e9-143">In hello **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="471e9-144">Cuando asigne un nombre a Hola entidad de servicio y crear una contraseña para él, haga clic en **administrar el acceso a ADLS** hello tooassociate almacena la entidad de servicio con su Data Lake.</span><span class="sxs-lookup"><span data-stu-id="471e9-144">After you give hello Service Principal a name and create a password for it, click **Manage ADLS Access** tooassociate hello Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="471e9-145">También es posible tooadd clúster acceso tooone o más Data Lake almacena después de crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="471e9-145">It’s also possible tooadd cluster access tooone or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="471e9-146">Abra hello Azure entrada portal para un almacén de Data Lake y vaya demasiado**Explorador de datos > acceso > agregar**.</span><span class="sxs-lookup"><span data-stu-id="471e9-146">Open hello Azure portal entry for a Data Lake store and go too**Data Explorer > Access > Add**.</span></span> 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a><span data-ttu-id="471e9-147">¿Cómo tooaccess Hola almacén Data Lake de R Server</span><span class="sxs-lookup"><span data-stu-id="471e9-147">How tooaccess hello Data Lake store from R Server</span></span>

<span data-ttu-id="471e9-148">Una vez que se le ha dado el almacén de Data Lake tooa acceso, puede usar el almacén de hello en R Server en forma de hello HDInsight que lo haría con una cuenta de almacenamiento de Azure secundario.</span><span class="sxs-lookup"><span data-stu-id="471e9-148">Once you’ve given access tooa Data Lake store, you can use hello store in R Server on HDInsight hello way you would a secondary Azure storage account.</span></span> <span data-ttu-id="471e9-149">Hola solo diferencia es ese prefijo hello **wasb: / /** cambia demasiado**adl: / /** como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="471e9-149">hello only difference is that hello prefix **wasb://** changes too**adl://** as follows:</span></span>


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


<span data-ttu-id="471e9-150">Hello siguientes comandos son tooconfigure usado Hola cuenta de almacenamiento de Data Lake con directorio de hello RevoShare y agregar el archivo .csv de ejemplo de Hola del anterior ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="471e9-150">hello following commands are used tooconfigure hello Data Lake storage account with hello RevoShare directory and add hello sample .csv file from hello previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="471e9-151">Uso de Azure File Storage con R Server</span><span class="sxs-lookup"><span data-stu-id="471e9-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="471e9-152">También hay una opción de almacenamiento de datos adecuada para su uso en el nodo de hello borde llamada [archivos de Azure] ((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="471e9-152">There is also a convenient data storage option for use on hello edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="471e9-153">Le permite toomount un toohello de recurso compartido de archivos de almacenamiento de Azure sistema de archivos de Linux.</span><span class="sxs-lookup"><span data-stu-id="471e9-153">It enables you toomount an Azure Storage file share toohello Linux file system.</span></span> <span data-ttu-id="471e9-154">Esta opción puede resultar útil para almacenar los archivos de datos, los scripts de R y objetos de resultado que podrían ser necesaria una versión posterior, especialmente cuando lo hace el sistema de archivos nativo de sentido toouse hello en el nodo del borde de hello en lugar de HDFS.</span><span class="sxs-lookup"><span data-stu-id="471e9-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense toouse hello native file system on hello edge node rather than HDFS.</span></span> 

<span data-ttu-id="471e9-155">Una de las ventajas principal de los archivos de Azure es ese archivo hello recursos compartidos se pueden montar y utilizados por cualquier sistema que tenga un sistema operativo compatible, como Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="471e9-155">A major benefit of Azure Files is that hello file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="471e9-156">Por ejemplo, puede utilizarse con otro clúster de HDInsight que sea suyo o de alguien de su equipo, con una máquina virtual de Azure, o incluso con un sistema local.</span><span class="sxs-lookup"><span data-stu-id="471e9-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="471e9-157">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="471e9-157">For more information, see:</span></span>

- [<span data-ttu-id="471e9-158">¿Cómo toouse almacenamiento de archivos de Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="471e9-158">How toouse Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="471e9-159">¿Cómo toouse almacenamiento de archivos de Azure en Windows</span><span class="sxs-lookup"><span data-stu-id="471e9-159">How toouse Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="471e9-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="471e9-160">Next steps</span></span>

<span data-ttu-id="471e9-161">Ahora que sabe opciones de almacenamiento de Azure de hello, siguientes de Hola de uso vínculos toodiscover maneras de obtener las tareas de ciencia de datos que realiza con el servidor de R en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="471e9-161">Now that you understand hello Azure storage options, use hello following links toodiscover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="471e9-162">Información general de R Server en HDInsight (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="471e9-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="471e9-163">Introducción al servidor de R en Hadoop</span><span class="sxs-lookup"><span data-stu-id="471e9-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="471e9-164">Agregar servidor RStudio tooHDInsight (si no se agregan durante la creación del clúster)</span><span class="sxs-lookup"><span data-stu-id="471e9-164">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="471e9-165">Opciones de contexto de proceso para R Server en HDInsight (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="471e9-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

