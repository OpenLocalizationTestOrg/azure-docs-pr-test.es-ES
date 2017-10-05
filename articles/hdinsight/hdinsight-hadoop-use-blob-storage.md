---
title: 'Consulta de datos desde Azure Storage compatible con HDFS: Azure HDInsight | Microsoft Docs'
description: "Aprenda a consultar datos desde Azure Storage y Azure Data Lake Store para almacenar los resultados del análisis."
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
ms.openlocfilehash: a44c2b363f7ebb593b9a9c5bd9e0d4fc3b4c31bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="4590a-104">Uso de Azure Storage con clústeres de Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4590a-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="4590a-105">Para analizar datos del clúster de HDInsight, puede almacenar los datos en Azure Storage, Azure Data Lake Store, o en ambos lugares.</span><span class="sxs-lookup"><span data-stu-id="4590a-105">To analyze data in HDInsight cluster, you can store the data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="4590a-106">Ambas opciones de almacenamiento le permiten eliminar de forma segura clústeres de HDInsight que se usan para el cálculo sin perder datos del usuario.</span><span class="sxs-lookup"><span data-stu-id="4590a-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="4590a-107">Hadoop admite una noción del sistema de archivos predeterminado.</span><span class="sxs-lookup"><span data-stu-id="4590a-107">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="4590a-108">El sistema de archivos predeterminado implica una autoridad y un esquema predeterminados.</span><span class="sxs-lookup"><span data-stu-id="4590a-108">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="4590a-109">También se puede usar para resolver rutas de acceso relativas.</span><span class="sxs-lookup"><span data-stu-id="4590a-109">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="4590a-110">Durante el proceso de creación del clúster de HDInsight, puede especificar un contenedor de blobs en Azure Blob Storage como el sistema de archivos predeterminado; también, con HDInsight 3.5, puede seleccionar Azure Storage o Azure Data Lake Store como el sistema de archivos predeterminado con algunas excepciones.</span><span class="sxs-lookup"><span data-stu-id="4590a-110">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> <span data-ttu-id="4590a-111">Para más información sobre la compatibilidad con el uso de Data Lake Store como almacenamiento predeterminado y como almacenamiento vinculado, consulte [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters) (Disponibilidad del clúster de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="4590a-111">For the supportability of using Data Lake Store as both the default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="4590a-112">En este artículo, aprenderá cómo funciona Azure Storage con clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4590a-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="4590a-113">Para más información sobre cómo funciona Data Lake Store con clústeres de HDInsight, consulte [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md) (Uso de Azure Data Lake Store con clústeres de Azure HDInsight).</span><span class="sxs-lookup"><span data-stu-id="4590a-113">To learn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="4590a-114">Consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obtener información sobre la creación de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4590a-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="4590a-115">Azure Storage es una solución de almacenamiento sólida y de uso general, que se integra sin problemas con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4590a-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="4590a-116">HDInsight puede usar un contenedor de blobs en Azure Storage como el sistema de archivos predeterminado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="4590a-116">HDInsight can use a blob container in Azure Storage as the default file system for the cluster.</span></span> <span data-ttu-id="4590a-117">Mediante una interfaz del sistema de archivos distribuido de Hadoop (HDFS), el conjunto completo de componentes de HDInsight puede operar directamente en datos estructurados o no estructurados almacenados como blobs.</span><span class="sxs-lookup"><span data-stu-id="4590a-117">Through a Hadoop distributed file system (HDFS) interface, the full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="4590a-118">Hay varias opciones disponibles al crear una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4590a-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="4590a-119">En la tabla siguiente se proporciona información sobre qué opciones se admiten en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4590a-119">The following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="4590a-120">Tipo de cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4590a-120">Storage account type</span></span> | <span data-ttu-id="4590a-121">Capa de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4590a-121">Storage tier</span></span> | <span data-ttu-id="4590a-122">Compatible con HDInsight</span><span class="sxs-lookup"><span data-stu-id="4590a-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="4590a-123">Cuenta de almacenamiento de uso general</span><span class="sxs-lookup"><span data-stu-id="4590a-123">General-purpose Storage Account</span></span> | <span data-ttu-id="4590a-124">Estándar</span><span class="sxs-lookup"><span data-stu-id="4590a-124">Standard</span></span> | <span data-ttu-id="4590a-125">__Sí__</span><span class="sxs-lookup"><span data-stu-id="4590a-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="4590a-126">Premium</span><span class="sxs-lookup"><span data-stu-id="4590a-126">Premium</span></span> | <span data-ttu-id="4590a-127">No</span><span class="sxs-lookup"><span data-stu-id="4590a-127">No</span></span> |
> | <span data-ttu-id="4590a-128">Cuenta de Blob Storage</span><span class="sxs-lookup"><span data-stu-id="4590a-128">Blob Storage Account</span></span> | <span data-ttu-id="4590a-129">Acceso frecuente</span><span class="sxs-lookup"><span data-stu-id="4590a-129">Hot</span></span> | <span data-ttu-id="4590a-130">No</span><span class="sxs-lookup"><span data-stu-id="4590a-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="4590a-131">Acceso esporádico</span><span class="sxs-lookup"><span data-stu-id="4590a-131">Cool</span></span> | <span data-ttu-id="4590a-132">No</span><span class="sxs-lookup"><span data-stu-id="4590a-132">No</span></span> |

<span data-ttu-id="4590a-133">No se recomienda usar el contenedor de blobs predeterminado para almacenar datos empresariales.</span><span class="sxs-lookup"><span data-stu-id="4590a-133">We do not recommend that you use the default blob container for storing business data.</span></span> <span data-ttu-id="4590a-134">Conviene eliminar el contenedor de blobs predeterminado después de cada uso para reducir los costos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4590a-134">Deleting the default blob container after each use to reduce storage cost is a good practice.</span></span> <span data-ttu-id="4590a-135">Tenga en cuenta que el contenedor predeterminado contiene los registros del sistema y de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4590a-135">Note that the default container contains application and system logs.</span></span> <span data-ttu-id="4590a-136">Asegúrese de recuperar los registros antes de eliminar el contenedor.</span><span class="sxs-lookup"><span data-stu-id="4590a-136">Make sure to retrieve the logs before deleting the container.</span></span>

<span data-ttu-id="4590a-137">No se permite compartir un contenedor de blobs entre varios clústeres.</span><span class="sxs-lookup"><span data-stu-id="4590a-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="4590a-138">Arquitectura de almacenamiento de HDInsight</span><span class="sxs-lookup"><span data-stu-id="4590a-138">HDInsight storage architecture</span></span>
<span data-ttu-id="4590a-139">El diagrama siguiente proporciona una panorámica de la arquitectura de almacenamiento de HDInsight disponible al utilizar Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="4590a-139">The following diagram provides an abstract view of the HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="4590a-140">![Los clústeres de Hadoop usan la API de HDFS para acceder y almacenar datos estructurados y no estructurados en Blob Storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Arquitectura de almacenamiento para HDInsight")</span><span class="sxs-lookup"><span data-stu-id="4590a-140">![Hadoop clusters use the HDFS API to access and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="4590a-141">HDInsight brinda acceso al sistema de archivos distribuidos que se adjunta localmente a los nodos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="4590a-141">HDInsight provides access to the distributed file system that is locally attached to the compute nodes.</span></span> <span data-ttu-id="4590a-142">Se puede acceder a este sistema de archivos usando el URI completo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4590a-142">This file system can be accessed by using the fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="4590a-143">Además, HDInsight le permite acceder a los datos almacenados en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4590a-143">In addition, HDInsight allows you to access data that is stored in Azure Storage.</span></span> <span data-ttu-id="4590a-144">La sintaxis es:</span><span class="sxs-lookup"><span data-stu-id="4590a-144">The syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="4590a-145">A la hora de usar una cuenta de Azure Storage con clústeres de HDInsight, es necesario tener en cuenta algunas cosas.</span><span class="sxs-lookup"><span data-stu-id="4590a-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="4590a-146">**Contenedores de las cuentas de almacenamiento que se conectan a un clúster:** dado que el nombre y la clave de la cuenta se asocian al clúster durante la creación, tiene acceso total a los blobs de dichos contenedores.</span><span class="sxs-lookup"><span data-stu-id="4590a-146">**Containers in the storage accounts that are connected to a cluster:** Because the account name and key are associated with the cluster during creation, you have full access to the blobs in those containers.</span></span>

* <span data-ttu-id="4590a-147">**Los contenedores o blobs públicos de las cuentas de almacenamiento que NO están conectados a un clúster:** tiene permiso de solo lectura a los blobs de los contenedores.</span><span class="sxs-lookup"><span data-stu-id="4590a-147">**Public containers or public blobs in storage accounts that are NOT connected to a cluster:** You have read-only permission to the blobs in the containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4590a-148">Los contenedores públicos le permiten obtener una lista de todos los blobs disponibles del contenedor en cuestión y obtener sus metadatos.</span><span class="sxs-lookup"><span data-stu-id="4590a-148">Public containers allow you to get a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="4590a-149">Los blobs públicos le permiten acceder a los blobs solo si conoce la URL exacta.</span><span class="sxs-lookup"><span data-stu-id="4590a-149">Public blobs allow you to access the blobs only if you know the exact URL.</span></span> <span data-ttu-id="4590a-150">Para obtener más información, consulte <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restringir acceso a contenedores y blobs</a>.</span><span class="sxs-lookup"><span data-stu-id="4590a-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access to containers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="4590a-151">**Contenedores privados de las cuentas de almacenamiento que no están conectados a un clúster:** no puede tener acceso a los blobs de los contenedores a menos que defina la cuenta de almacenamiento al enviar los trabajos de WebHCat.</span><span class="sxs-lookup"><span data-stu-id="4590a-151">**Private containers in storage accounts that are NOT connected to a cluster:** You can't access the blobs in the containers unless you define the storage account when you submit the WebHCat jobs.</span></span> <span data-ttu-id="4590a-152">Esto se explica posteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="4590a-152">This is explained later in this article.</span></span>

<span data-ttu-id="4590a-153">Las cuentas de almacenamiento definidas en el proceso de creación y sus claves se almacenan en %HADOOP_HOME%/conf/core-site.xml en los nodos de clúster.</span><span class="sxs-lookup"><span data-stu-id="4590a-153">The storage accounts that are defined in the creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on the cluster nodes.</span></span> <span data-ttu-id="4590a-154">El comportamiento predeterminado de HDInsight es usar las cuentas de almacenamiento definidas en el archivo core-site.xml.</span><span class="sxs-lookup"><span data-stu-id="4590a-154">The default behavior of HDInsight is to use the storage accounts defined in the core-site.xml file.</span></span> <span data-ttu-id="4590a-155">Puede modificar esta configuración mediante [Ambari](./hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="4590a-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="4590a-156">Varios trabajos de WebHCat, incluidos Hive, MapReduce, streaming de Hadoop y Pig, pueden llevar una descripción de cuentas de almacenamiento y metadatos con ellos.</span><span class="sxs-lookup"><span data-stu-id="4590a-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="4590a-157">(Actualmente esto funciona para Pig con cuentas de almacenamiento pero no para metadatos). Para obtener más información, consulte [Uso de un clúster de HDInsight con cuentas de almacenamiento y tiendas de metadatos alternativas](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span><span class="sxs-lookup"><span data-stu-id="4590a-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="4590a-158">Los blobs se pueden usar para datos estructurados y no estructurados.</span><span class="sxs-lookup"><span data-stu-id="4590a-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="4590a-159">Los contenedores de blobs almacenan los datos como pares de clave-valor y no hay jerarquía de directorios.</span><span class="sxs-lookup"><span data-stu-id="4590a-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="4590a-160">No obstante, el carácter de barra diagonal ( / ) se puede usar en el nombre de la clave para que parezca que el archivo está almacenado dentro de una estructura de directorios.</span><span class="sxs-lookup"><span data-stu-id="4590a-160">However the slash character ( / ) can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="4590a-161">Por ejemplo, la clave de un blob puede ser *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="4590a-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="4590a-162">No hay directorios *input* , pero dada la presencia del carácter de barra diagonal en el nombre de la clave, parece la ruta de un archivo.</span><span class="sxs-lookup"><span data-stu-id="4590a-162">No actual *input* directory exists, but due to the presence of the slash character in the key name, it has the appearance of a file path.</span></span>

## <span data-ttu-id="4590a-163"><a id="benefits"></a>Ventajas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4590a-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="4590a-164">El costo de rendimiento implícito por no tener ubicados juntos los recursos de almacenamiento y clústeres de proceso se ve mitigado por el modo en que los clústeres de proceso se crean cerca de los recursos de la cuenta de almacenamiento dentro de la región de Azure, donde la red de alta velocidad consigue que los nodos de proceso sean eficientes en el acceso a los datos de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4590a-164">The implied performance cost of not co-locating compute clusters and storage resources is mitigated by the way the compute clusters are created close to the storage account resources inside the Azure region, where the high-speed network makes it efficient for the compute nodes to access the data inside Azure storage.</span></span>

<span data-ttu-id="4590a-165">Hay varias ventajas asociadas al almacenamiento de datos en Azure Storage en lugar de en HDFS:</span><span class="sxs-lookup"><span data-stu-id="4590a-165">There are several benefits associated with storing the data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="4590a-166">**Reutilización de uso compartido de datos:** los datos de HDFS se ubican dentro del clúster de cálculo.</span><span class="sxs-lookup"><span data-stu-id="4590a-166">**Data reuse and sharing:** The data in HDFS is located inside the compute cluster.</span></span> <span data-ttu-id="4590a-167">Solamente las aplicaciones que tengan acceso al clúster de cálculo podrán usar los datos usando las API HDFS.</span><span class="sxs-lookup"><span data-stu-id="4590a-167">Only the applications that have access to the compute cluster can use the data by using HDFS APIs.</span></span> <span data-ttu-id="4590a-168">Se puede acceder a los datos de Azure Storage mediante las API de HDFS o las [API de REST de Blob Storage][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="4590a-168">The data in Azure storage can be accessed either through the HDFS APIs or through the [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="4590a-169">Por lo tanto, se puede usar un conjunto mayor de aplicaciones (incluyendo otros clústeres de HDInsight) y herramientas para producir y consumir los datos.</span><span class="sxs-lookup"><span data-stu-id="4590a-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used to produce and consume the data.</span></span>
* <span data-ttu-id="4590a-170">**Archivo de datos:** almacenar los datos en Azure Storage permite que los clústeres de HDInsight usados para el cálculo se eliminen de forma segura sin perder datos del usuario.</span><span class="sxs-lookup"><span data-stu-id="4590a-170">**Data archiving:** Storing data in Azure storage enables the HDInsight clusters used for computation to be safely deleted without losing user data.</span></span>
* <span data-ttu-id="4590a-171">**Costo de almacenamiento de datos:** almacenar datos en DFS es más caro a largo plazo que almacenarlos en Azure Storage, ya que el costo de un clúster de proceso es superior al de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4590a-171">**Data storage cost:** Storing data in DFS for the long term is more costly than storing the data in Azure storage because the cost of a compute cluster is higher than the cost of Azure storage.</span></span> <span data-ttu-id="4590a-172">Además, como no hay que volver a cargar los datos para cada generación de clúster de cálculo, también se ahorra en costes de carga de datos.</span><span class="sxs-lookup"><span data-stu-id="4590a-172">In addition, because the data does not have to be reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="4590a-173">**Escalación horizontal elástica:** aunque HDFS proporciona un sistema de archivos escalable en horizontal, la escala se determina en función del número de nodos que cree para su clúster.</span><span class="sxs-lookup"><span data-stu-id="4590a-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, the scale is determined by the number of nodes that you create for your cluster.</span></span> <span data-ttu-id="4590a-174">Cambiar la escala puede ser un proceso más complicado que basarse en las funcionalidades de escalado elástico que se obtienen automáticamente en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4590a-174">Changing the scale can become a more complicated process than relying on the elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="4590a-175">**Replicación geográfica:** su almacenamiento de Azure Storage se puede replicar geográficamente.</span><span class="sxs-lookup"><span data-stu-id="4590a-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="4590a-176">Aunque esto le aporta recuperación geográfica y redundancia de datos, una conmutación por error en la ubicación replicada geográficamente afecta gravemente a su rendimiento y puede incurrir en costes adicionales.</span><span class="sxs-lookup"><span data-stu-id="4590a-176">Although this gives you geographic recovery and data redundancy, a failover to the geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="4590a-177">Por lo tanto, nuestra recomendación es que elija la replicación geográfica de forma inteligente y únicamente si merece la pena pagar el coste adicional por el valor de los datos.</span><span class="sxs-lookup"><span data-stu-id="4590a-177">So our recommendation is to choose the geo-replication wisely and only if the value of the data is worth the additional cost.</span></span>

<span data-ttu-id="4590a-178">Determinados trabajos y paquetes de MapReduce podrían crear resultados intermedios que realmente no desea almacenar en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4590a-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want to store in Azure storage.</span></span> <span data-ttu-id="4590a-179">En tal caso, puede optar por almacenar los datos en el HDFS local.</span><span class="sxs-lookup"><span data-stu-id="4590a-179">In that case, you can elect to store the data in the local HDFS.</span></span> <span data-ttu-id="4590a-180">De hecho, HDInsight usa DFS para varios de estos resultados intermedios en los trabajos de Hive y otros procesos.</span><span class="sxs-lookup"><span data-stu-id="4590a-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="4590a-181">La mayoría de los comandos HDFS (por ejemplo, <b>ls</b>, <b>copyFromLocal</b> y <b>mkdir</b>) siguen funcionando según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="4590a-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="4590a-182">Únicamente los comandos específicos de la implementación nativa de HDFS (a la que nos referiremos como DFS), como <b>fschk</b> y <b>dfsadmin</b>, muestran comportamientos diferentes en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4590a-182">Only the commands that are specific to the native HDFS implementation (which is referred to as DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="4590a-183">Creación de contenedores de blobs</span><span class="sxs-lookup"><span data-stu-id="4590a-183">Create Blob containers</span></span>
<span data-ttu-id="4590a-184">Para usar blobs, en primer lugar debe crear una [cuenta de Azure Storage][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="4590a-184">To use blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="4590a-185">Como parte de esto, especifica una región de Azure donde se crea la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4590a-185">As part of this, you specify an Azure region where the storage account is created.</span></span> <span data-ttu-id="4590a-186">El clúster y la cuenta de almacenamiento deben ubicarse en la misma región.</span><span class="sxs-lookup"><span data-stu-id="4590a-186">The cluster and the storage account must be hosted in the same region.</span></span> <span data-ttu-id="4590a-187">La base de datos de SQL Server de la tienda de metadatos Hive y la base de datos de SQL Server de la tienda de metadatos Oozie también deben encontrarse en la misma región.</span><span class="sxs-lookup"><span data-stu-id="4590a-187">The Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in the same region.</span></span>

<span data-ttu-id="4590a-188">Cualquiera que sea su ubicación, todos los blobs que cree pertenecerán a un contenedor de su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4590a-188">Wherever it lives, each blob you create belongs to a container in your Azure Storage account.</span></span> <span data-ttu-id="4590a-189">Este contenedor puede ser un blob existente creado fuera de HDInsight, o bien un contenedor que se crea para un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4590a-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="4590a-190">El contenedor de blobs predeterminado almacena información específica del clúster, como registros y el historial de trabajos.</span><span class="sxs-lookup"><span data-stu-id="4590a-190">The default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="4590a-191">No comparta un contenedor de blobs predeterminado con varios clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4590a-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="4590a-192">Se podría dañar el historial de trabajos.</span><span class="sxs-lookup"><span data-stu-id="4590a-192">This might corrupt job history.</span></span> <span data-ttu-id="4590a-193">Es recomendable usar un contenedor diferente para cada clúster y colocar los datos compartidos en una cuenta de almacenamiento vinculada especificada en la implementación de todos los clústeres pertinentes en lugar de la cuenta de almacenamiento predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4590a-193">It is recommended to use a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than the default storage account.</span></span> <span data-ttu-id="4590a-194">Para más información acerca de cómo configurar cuentas de almacenamiento vinculadas, consulte [Creación de clústeres de HDInsight][hdinsight-creation].</span><span class="sxs-lookup"><span data-stu-id="4590a-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="4590a-195">Sin embargo, puede volver a usar un contenedor de almacenamiento predeterminado después de que se haya eliminado el clúster de HDInsight original.</span><span class="sxs-lookup"><span data-stu-id="4590a-195">However you can reuse a default storage container after the original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="4590a-196">En el caso de los clústeres de HBase, para conservar el esquema y los datos de tabla de HBase se puede crear un nuevo clúster de HBase mediante el contenedor de blobs predeterminado que usaba un clúster de HBase eliminado.</span><span class="sxs-lookup"><span data-stu-id="4590a-196">For HBase clusters, you can actually retain the HBase table schema and data by creating a new HBase cluster using the default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-the-azure-portal"></a><span data-ttu-id="4590a-197">Uso de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4590a-197">Use the Azure portal</span></span>
<span data-ttu-id="4590a-198">Al crear un clúster de HDInsight desde el Portal, tendrá las opciones (tal y como se muestra a continuación) para proporcionar los detalles de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4590a-198">When creating an HDInsight cluster from the Portal, you have the options (as shown below) to provide the storage account details.</span></span> <span data-ttu-id="4590a-199">También puede especificar si quiere una cuenta de almacenamiento adicional asociada al clúster y, en este caso, elegir entre Data Lake Store u otro blob de Azure Storage como almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="4590a-199">You can also specify whether you want an additional storage account associated with the cluster, and if so, choose from Data Lake Store or another Azure Storage blob as the additional storage.</span></span>

![Origen de datos de creación de un clúster de Hadoop en HDInsight](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="4590a-201">No se admite el uso de una cuenta de almacenamiento adicional en una ubicación diferente a la del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4590a-201">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="4590a-202">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4590a-202">Use Azure PowerShell</span></span>
<span data-ttu-id="4590a-203">Si ha [instalado y configurado Azure PowerShell][powershell-install], puede usar lo siguiente desde el símbolo del sistema de Azure PowerShell para crear un contenedor y una cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="4590a-203">If you [installed and configured Azure PowerShell][powershell-install], you can use the following from the Azure PowerShell prompt to create a storage account and container:</span></span>

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

### <a name="use-azure-cli"></a><span data-ttu-id="4590a-204">Uso de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4590a-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="4590a-205">Si ha [instalado y configurado la CLI Azure](../cli-install-nodejs.md), se puede usar el comando siguiente para una cuenta de almacenamiento y contenedor.</span><span class="sxs-lookup"><span data-stu-id="4590a-205">If you have [installed and configured the Azure CLI](../cli-install-nodejs.md), the following command can be used to a storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="4590a-206">El parámetro `--type` indica cómo se replica la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4590a-206">The `--type` parameter indicates how the storage account is replicated.</span></span> <span data-ttu-id="4590a-207">Para obtener más información, vea [Replicación de Azure Storage](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="4590a-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="4590a-208">No utilice ZRS, ya que no admite blob en páginas, archivo, tabla o cola.</span><span class="sxs-lookup"><span data-stu-id="4590a-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="4590a-209">Se le pide que especifique la región geográfica en la que se crea la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4590a-209">You are prompted to specify the geographic region that the storage account is created in.</span></span> <span data-ttu-id="4590a-210">Debe crear la cuenta de almacenamiento en la misma región en la que planea crear el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4590a-210">You should create the storage account in the same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="4590a-211">Una vez creada la cuenta de almacenamiento, use el siguiente comando para recuperar las claves de la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="4590a-211">Once the storage account is created, use the following command to retrieve the storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="4590a-212">Para crear un contenedor, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4590a-212">To create a container, use the following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="4590a-213">Archivos adicionales en Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4590a-213">Address files in Azure storage</span></span>
<span data-ttu-id="4590a-214">El esquema de URI para acceder a los archivos de Azure Storage desde HDInsight es:</span><span class="sxs-lookup"><span data-stu-id="4590a-214">The URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="4590a-215">El esquema URI proporciona acceso sin cifrar (con el prefijo *wasb:*) y acceso cifrado SSL con *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="4590a-215">The URI scheme provides unencrypted access (with the *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="4590a-216">Se recomienda usar *wasbs* siempre que sea posible, incluso cuando se acceda a datos que se encuentren en la misma región de Azure.</span><span class="sxs-lookup"><span data-stu-id="4590a-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside the same region in Azure.</span></span>

<span data-ttu-id="4590a-217">&lt;BlobStorageContainerName&gt; identifica el nombre del contenedor de blobs del Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4590a-217">The &lt;BlobStorageContainerName&gt; identifies the name of the blob container in Azure storage.</span></span>
<span data-ttu-id="4590a-218">&lt;StorageAccountName&gt; identifica el nombre de la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4590a-218">The &lt;StorageAccountName&gt; identifies the Azure Storage account name.</span></span> <span data-ttu-id="4590a-219">Se necesita el nombre completo de dominio (FQDN).</span><span class="sxs-lookup"><span data-stu-id="4590a-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="4590a-220">Si no se ha especificado ningún valor en &lt;BlobStorageContainerName&gt; ni en &lt;StorageAccountName&gt;, se usará el sistema de archivos predeterminado.</span><span class="sxs-lookup"><span data-stu-id="4590a-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, the default file system is used.</span></span> <span data-ttu-id="4590a-221">Para los archivos del sistema de archivos predeterminado, puede usar una ruta relativa o absoluta.</span><span class="sxs-lookup"><span data-stu-id="4590a-221">For the files on the default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="4590a-222">Por ejemplo, se puede hacer referencia al archivo *hadoop-mapreduce-examples.jar* que se incluye con los clústeres de HDInsight usando uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="4590a-222">For example, the *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred to by using one of the following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="4590a-223">El nombre del archivo es <i>hadoop-examples.jar</i> en las versiones 2.1 y 1.6 de los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4590a-223">The file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="4590a-224">La &lt;ruta&gt; es el nombre de la ruta HDFS del archivo o el directorio.</span><span class="sxs-lookup"><span data-stu-id="4590a-224">The &lt;path&gt; is the file or directory HDFS path name.</span></span> <span data-ttu-id="4590a-225">Dado que los contenedores de Azure Storage son solamente almacenes de pares clave-valor, no hay ningún sistema de archivos jerárquico real.</span><span class="sxs-lookup"><span data-stu-id="4590a-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="4590a-226">Un carácter de barra inclinada ( / ) dentro de la clave de blob se interpreta como separador de directorios.</span><span class="sxs-lookup"><span data-stu-id="4590a-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="4590a-227">Por ejemplo, el nombre del blob para *hadoop-mapreduce-examples.jar* es:</span><span class="sxs-lookup"><span data-stu-id="4590a-227">For example, the blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="4590a-228">Al trabajar con blobs fuera de HDInsight, la mayoría de las utilidades no reconocen el formato WASB y en su lugar, espera un formato básico de ruta de acceso, como `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="4590a-228">When working with blobs outside of HDInsight, most utilities do not recognize the WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="4590a-229">Acceso a blobs</span><span class="sxs-lookup"><span data-stu-id="4590a-229">Access blobs</span></span> 


### <span data-ttu-id="4590a-230"><a name="access-blobs-using-azure-powershell"></a> Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4590a-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="4590a-231">Los comandos de esta sección proporcionan un ejemplo básico de uso de PowerShell para acceder a los datos almacenados en blobs.</span><span class="sxs-lookup"><span data-stu-id="4590a-231">The commands in this section provide a basic example of using PowerShell to access data stored in blobs.</span></span> <span data-ttu-id="4590a-232">Para obtener un ejemplo más completo que se personaliza para trabajar con HDInsight, vea las [Herramientas de HDInsight](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="4590a-232">For a more full-featured example that is customized for working with HDInsight, see the [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="4590a-233">Utilice el comando siguiente para incluir los cmdlets relacionados con el blob:</span><span class="sxs-lookup"><span data-stu-id="4590a-233">Use the following command to list the blob-related cmdlets:</span></span>

    Get-Command *blob*

![Lista de cmdlets de PowerShell relacionados con el blob.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="4590a-235">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="4590a-235">Upload files</span></span>
<span data-ttu-id="4590a-236">Consulte [Carga de datos en HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="4590a-236">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="4590a-237">Descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="4590a-237">Download files</span></span>
<span data-ttu-id="4590a-238">El script siguiente descarga un blob en bloques en la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="4590a-238">The following script downloads a block blob to the current folder.</span></span> <span data-ttu-id="4590a-239">Antes de ejecutar el script, cambie el directorio a una carpeta en la que tenga permisos de escritura.</span><span class="sxs-lookup"><span data-stu-id="4590a-239">Before running the script, change the directory to a folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # The storage account used for the default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # The default file system container has the same name as the cluster.
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    # Use Add-AzureAccount if you haven't connected to your Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List the downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="4590a-240">Al proporcionar el nombre del grupo de recursos y el nombre del clúster, podrá utilizar el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="4590a-240">Providing the resource group name and the cluster name, you can use the following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="4590a-241">Eliminar archivos</span><span class="sxs-lookup"><span data-stu-id="4590a-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="4590a-242">Enumerar archivos</span><span class="sxs-lookup"><span data-stu-id="4590a-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="4590a-243">Ejecutar consultas de Hive usando una cuenta de almacenamiento sin definir</span><span class="sxs-lookup"><span data-stu-id="4590a-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="4590a-244">En este ejemplo se presenta cómo mostrar una carpeta en una lista desde la cuenta de almacenamiento no definida durante el proceso de creación.</span><span class="sxs-lookup"><span data-stu-id="4590a-244">This example shows how to list a folder from storage account that is not defined during the creating process.</span></span>
<span data-ttu-id="4590a-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="4590a-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="4590a-246">Uso de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4590a-246">Use Azure CLI</span></span>
<span data-ttu-id="4590a-247">Use el siguiente comando para mostrar los cmdlets relacionados con blobs:</span><span class="sxs-lookup"><span data-stu-id="4590a-247">Use the following command to list the blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="4590a-248">**Ejemplo de uso de CLI de Azure para cargar un archivo**</span><span class="sxs-lookup"><span data-stu-id="4590a-248">**Example of using Azure CLI to upload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="4590a-249">**Ejemplo de uso de CLI de Azure para descargar un archivo**</span><span class="sxs-lookup"><span data-stu-id="4590a-249">**Example of using Azure CLI to download a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="4590a-250">**Ejemplo de uso de CLI de Azure para eliminar un archivo**</span><span class="sxs-lookup"><span data-stu-id="4590a-250">**Example of using Azure CLI to delete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="4590a-251">**Ejemplo de uso de CLI de Azure para mostrar archivos**</span><span class="sxs-lookup"><span data-stu-id="4590a-251">**Example of using Azure CLI to list files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="4590a-252">Uso de cuentas de almacenamiento adicionales</span><span class="sxs-lookup"><span data-stu-id="4590a-252">Use additional storage accounts</span></span>

<span data-ttu-id="4590a-253">Al crear un clúster de HDInsight, se especifica la cuenta de Azure Storage a la que quiere asociarlo.</span><span class="sxs-lookup"><span data-stu-id="4590a-253">While creating an HDInsight cluster, you specify the Azure Storage account you want to associate with it.</span></span> <span data-ttu-id="4590a-254">Además de esta cuenta de almacenamiento, puede agregar otras desde la misma suscripción de Azure o desde otras diferentes tanto durante el proceso de creación como después de que el clúster se haya creado.</span><span class="sxs-lookup"><span data-stu-id="4590a-254">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or different Azure subscriptions during the creation process or after a cluster has been created.</span></span> <span data-ttu-id="4590a-255">Para obtener instrucciones sobre cómo agregar más cuentas de almacenamiento, consulte [Creación de clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4590a-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="4590a-256">No se admite el uso de una cuenta de almacenamiento adicional en una ubicación diferente a la del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4590a-256">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4590a-257">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4590a-257">Next steps</span></span>
<span data-ttu-id="4590a-258">En este artículo, aprendió a usar Azure Storage compatible con HDFS con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4590a-258">In this article, you learned how to use HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="4590a-259">Esto le permite crear soluciones de adquisición de datos de archivado escalables y a largo plazo y usar HDInsight para desbloquear la información que hay dentro de los datos estructurados y no estructurados almacenados.</span><span class="sxs-lookup"><span data-stu-id="4590a-259">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="4590a-260">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="4590a-260">For more information, see:</span></span>

* <span data-ttu-id="4590a-261">[Introducción a Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="4590a-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="4590a-262">Introducción Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4590a-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="4590a-263">[Carga de datos en HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="4590a-263">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="4590a-264">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="4590a-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="4590a-265">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="4590a-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="4590a-266">[Uso de firmas de acceso compartido de Azure Storage para restringir el acceso a datos con HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="4590a-266">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

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
