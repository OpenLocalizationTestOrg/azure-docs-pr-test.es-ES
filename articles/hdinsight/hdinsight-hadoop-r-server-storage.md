---
title: Soluciones de Azure Storage para R Server en HDInsight (Azure) | Microsoft Docs
description: "Obtenga información sobre las distintas opciones de almacenamiento disponibles para los usuarios con R Server en HDInsight."
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
ms.openlocfilehash: aef9c15636ccaecce07d4fa218a40ed26ebad9df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="fd8ac-103">Soluciones de Azure Storage para R Server en HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd8ac-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="fd8ac-104">Microsoft R Server en HDInsight dispone de diversas soluciones para almacenar datos, código u objetos que contienen resultados de análisis.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-104">Microsoft R Server on HDInsight has a variety of storage solutions to persist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="fd8ac-105">Entre ellas se incluyen las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="fd8ac-105">These include the following options:</span></span>

- [<span data-ttu-id="fd8ac-106">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="fd8ac-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="fd8ac-107">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="fd8ac-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="fd8ac-108">Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="fd8ac-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="fd8ac-109">También tiene la opción de acceder a varias cuentas o contenedores de Azure Storage con el clúster de HDI.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-109">You also have the option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="fd8ac-110">Azure File Storage constituye una práctica opción de almacenamiento de datos para usar en el nodo perimetral que le permite montar un recurso compartido de archivos de Azure Storage en, por ejemplo, el sistema de archivos Linux.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-110">Azure File storage is a convenient data storage option for use on the edge node that enables you to mount an Azure Storage file share to, for example, the Linux file system.</span></span> <span data-ttu-id="fd8ac-111">Pero los recursos compartidos de Azure File se pueden montar y utilizar en cualquier sistema que tenga un sistema operativo compatible, como Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="fd8ac-112">Cuando se crea un clúster de Hadoop en HDInsight, se especifica una cuenta de **Azure Storage** o una de **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="fd8ac-113">Un contenedor de almacenamiento específico de esa cuenta conserva el sistema de archivos para el clúster creado (por ejemplo, el Sistema de archivos distribuido de Hadoop).</span><span class="sxs-lookup"><span data-stu-id="fd8ac-113">A specific storage container from that account holds the file system for the cluster that you create (for example, the Hadoop Distributed File System).</span></span> <span data-ttu-id="fd8ac-114">Para más información e instrucciones, consulte:</span><span class="sxs-lookup"><span data-stu-id="fd8ac-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="fd8ac-115">Uso de Azure Storage con HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd8ac-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="fd8ac-116">[Uso de Data Lake Store con clústeres de Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md)</span><span class="sxs-lookup"><span data-stu-id="fd8ac-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="fd8ac-117">Para más información sobre las soluciones de almacenamiento de Azure, consulte [Introducción a Microsoft Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fd8ac-117">For more information on the Azure storage solutions, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="fd8ac-118">Para obtener instrucciones sobre cómo seleccionar la opción de almacenamiento más adecuada para su escenario, consulte [Decisión sobre cuándo usar Azure Blobs, Azure Files o Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md).</span><span class="sxs-lookup"><span data-stu-id="fd8ac-118">For guidance on selecting the most appropriate storage option to use for your scenario, see [Deciding when to use Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="fd8ac-119">Uso de cuentas de Azure Blob Storage con R Server</span><span class="sxs-lookup"><span data-stu-id="fd8ac-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="fd8ac-120">Si es necesario, se puede acceder a varias cuentas de almacenamiento o contenedores de Azure con el clúster de HDI.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="fd8ac-121">Para ello, tiene que especificar las cuentas de almacenamiento adicionales en la interfaz de usuario durante la creación del clúster y seguir estos pasos para poder usarlas en R Server.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-121">To do so, you need to specify the additional storage accounts in the UI when you create the cluster, and then follow these steps to use them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="fd8ac-122">Con vistas al rendimiento, el clúster de HDInsight se crea en el mismo centro de datos que la cuenta de almacenamiento principal especificada.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-122">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span></span> <span data-ttu-id="fd8ac-123">No se admite el uso de una cuenta de almacenamiento en una ubicación diferente a la del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-123">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="fd8ac-124">Cree un clúster de HDInsight con el nombre de cuenta de almacenamiento **storage1** y un contenedor predeterminado denominado **container1**.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="fd8ac-125">Especifique una cuenta de almacenamiento adicional con el nombre **storage2**.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="fd8ac-126">Copie el archivo mycsv.csv en el directorio /share y realice un análisis en ese archivo.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-126">Copy the mycsv.csv file to the /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="fd8ac-127">En código R, establezca el nodo de nombre en **default** e indique el directorio y el archivo que se van a procesar.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-127">In R code, set the name node to **default,** and set your directory and file to process.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of the data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define the Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify the input file to analyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="fd8ac-128">Todas las referencias de archivos y directorios apuntan a la cuenta de almacenamiento wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-128">All the directory and file references point to the storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="fd8ac-129">Esta es la **cuenta de almacenamiento predeterminada** asociada al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-129">This is the **default storage account** that's associated with the HDInsight cluster.</span></span>

<span data-ttu-id="fd8ac-130">Ahora supongamos que quiere procesar un archivo llamado mySpecial.csv que se encuentra en el directorio /private de **container2** en **storage2**.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-130">Now, suppose you want to process a file called mySpecial.csv that's located in the  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="fd8ac-131">En el código R, apunte la referencia del nodo de nombres a la cuenta de almacenamiento **storage2** .</span><span class="sxs-lookup"><span data-stu-id="fd8ac-131">In your R code, point the name node reference to the **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of the data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify the input file to analyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="fd8ac-132">Todas las referencias de archivos y directorios apuntan ahora a la cuenta de almacenamiento wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-132">All of the directory and file references now point to the storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="fd8ac-133">Este es el **nodo de nombres** que ha especificado.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-133">This is the **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="fd8ac-134">Debe configurar el directorio /user/RevoShare/<SSH username> en **storage2** de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="fd8ac-134">You have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="fd8ac-135">Uso de una instancia de Azure Data Lake Store con R Server</span><span class="sxs-lookup"><span data-stu-id="fd8ac-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="fd8ac-136">Para utilizar los almacenes de Data Lake con su cuenta de HDInsight, tiene que dar al clúster acceso a cada almacén de Azure Data Lake que quiera usar.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-136">To use Data Lake stores with your HDInsight account, you need to give your cluster access to each Azure Data Lake store that you want to use.</span></span> <span data-ttu-id="fd8ac-137">Para obtener instrucciones sobre cómo usar Azure Portal para crear un clúster de HDInsight con una cuenta de Azure Data Lake Store como almacenamiento predeterminado o como almacén adicional, consulte [Creación de un clúster de HDInsight con Data Lake Store mediante Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd8ac-137">For instructions on how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="fd8ac-138">El uso del almacén en el script de R es muy similar al uso de una cuenta de almacenamiento secundaria de Azure (tal como se describe en el procedimiento anterior).</span><span class="sxs-lookup"><span data-stu-id="fd8ac-138">You then use the store in your R script much like you did a secondary Azure storage account as described in the previous procedure.</span></span>

### <a name="add-cluster-access-to-your-azure-data-lake-stores"></a><span data-ttu-id="fd8ac-139">Incorporación de acceso del clúster a los almacenes de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="fd8ac-139">Add cluster access to your Azure Data Lake stores</span></span>
<span data-ttu-id="fd8ac-140">El acceso a un almacén de Azure Data Lake se establece mediante el uso de una entidad de servicio de Azure Active Directory (AAD) asociada a su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="fd8ac-141">Para agregar una entidad de servicio de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="fd8ac-141">To add an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="fd8ac-142">Al crear el clúster de HDInsight, seleccione **Identidad de AAD del clúster** en la pestaña **Origen de datos**.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span></span>

2. <span data-ttu-id="fd8ac-143">En el cuadro de diálogo **Identidad de AAD del clúster**, en **Seleccionar entidad de servicio de AD**, elija **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-143">In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="fd8ac-144">Después de asignar un nombre a la entidad de servicio y crear una contraseña para ella, haga clic en **Administrar acceso a ADLS** para asociar la entidad de servicio a los almacenes Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-144">After you give the Service Principal a name and create a password for it, click **Manage ADLS Access** to associate the Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="fd8ac-145">También es posible agregar acceso al clúster a una o varias instancias de Data Lake Store después de la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-145">It’s also possible to add cluster access to one or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="fd8ac-146">Abra la entrada de Azure Portal para una instancia de Data Lake Store y vaya a **Explorador de datos > Acceso > Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-146">Open the Azure portal entry for a Data Lake store and go to **Data Explorer > Access > Add**.</span></span> 

### <a name="how-to-access-the-data-lake-store-from-r-server"></a><span data-ttu-id="fd8ac-147">Acceso a la instancia de Data Lake Store desde R Server</span><span class="sxs-lookup"><span data-stu-id="fd8ac-147">How to access the Data Lake store from R Server</span></span>

<span data-ttu-id="fd8ac-148">Una vez que haya dado acceso a un almacén de Data Lake, puede usar el almacén en R Server en HDInsight de la manera en que lo haría con una cuenta de almacenamiento de Azure secundaria.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-148">Once you’ve given access to a Data Lake store, you can use the store in R Server on HDInsight the way you would a secondary Azure storage account.</span></span> <span data-ttu-id="fd8ac-149">La única diferencia es que el prefijo **wasb://** cambia a **adl://**, de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="fd8ac-149">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span></span>


    # Point to the ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of the data (assumes a /share directory on the ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify the input file in HDFS to analyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of the week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define the data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="fd8ac-150">Los siguientes comandos se usan para configurar la cuenta de almacenamiento de Data Lake con el directorio RevoShare y agregar el archivo .csv de ejemplo del ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="fd8ac-150">The following commands are used to configure the Data Lake storage account with the RevoShare directory and add the sample .csv file from the previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="fd8ac-151">Uso de Azure File Storage con R Server</span><span class="sxs-lookup"><span data-stu-id="fd8ac-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="fd8ac-152">También hay una práctica opción de almacenamiento de datos para usar en el nodo perimetral llamada [Azure Files] ((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="fd8ac-152">There is also a convenient data storage option for use on the edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="fd8ac-153">Con esta opción podrá montar un recurso compartido de archivos de Almacenamiento de Azure en el sistema de archivos de Linux.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-153">It enables you to mount an Azure Storage file share to the Linux file system.</span></span> <span data-ttu-id="fd8ac-154">Esta opción puede resultar práctica para almacenar archivos de datos, scripts de R y objetos de resultado que podría necesitar más adelante, en especial cuando sea conveniente usar el sistema de archivos nativo en el nodo perimetral en lugar de HDFS.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense to use the native file system on the edge node rather than HDFS.</span></span> 

<span data-ttu-id="fd8ac-155">Una ventaja importante de Archivos de Azure es que los recursos compartidos de archivos se pueden montar y utilizar en cualquier sistema que tenga un sistema operativo compatible, como Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-155">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="fd8ac-156">Por ejemplo, puede utilizarse con otro clúster de HDInsight que sea suyo o de alguien de su equipo, con una máquina virtual de Azure, o incluso con un sistema local.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="fd8ac-157">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="fd8ac-157">For more information, see:</span></span>

- [<span data-ttu-id="fd8ac-158">Uso de Azure File Storage con Linux</span><span class="sxs-lookup"><span data-stu-id="fd8ac-158">How to use Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="fd8ac-159">Uso de Azure File Storage en Windows</span><span class="sxs-lookup"><span data-stu-id="fd8ac-159">How to use Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="fd8ac-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fd8ac-160">Next steps</span></span>

<span data-ttu-id="fd8ac-161">Ahora que comprende las opciones de Azure Storage, use los vínculos siguientes para descubrir otras maneras de realizar tareas de ciencia de datos con R Server en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fd8ac-161">Now that you understand the Azure storage options, use the following links to discover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="fd8ac-162">Información general de R Server en HDInsight (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="fd8ac-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="fd8ac-163">Introducción al servidor de R en Hadoop</span><span class="sxs-lookup"><span data-stu-id="fd8ac-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="fd8ac-164">Instalación de RStudio con R Server en HDInsight (si no está instalado durante la creación del clúster)</span><span class="sxs-lookup"><span data-stu-id="fd8ac-164">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="fd8ac-165">Opciones de contexto de proceso para R Server en HDInsight (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="fd8ac-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

