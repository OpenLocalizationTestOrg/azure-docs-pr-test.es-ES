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
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="9e048-104">Uso de Azure Storage con clústeres de Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e048-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="9e048-105">tooanalyze datos en clúster de HDInsight, puede almacenar datos de hello en el almacenamiento de Azure, el almacén de Azure Data Lake o ambos.</span><span class="sxs-lookup"><span data-stu-id="9e048-105">tooanalyze data in HDInsight cluster, you can store hello data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="9e048-106">Ambas opciones de almacenamiento le permiten eliminar toosafely clústeres de HDInsight que se usan para el cálculo sin perder los datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="9e048-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="9e048-107">Hadoop admite una noción de sistema de archivos predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-107">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="9e048-108">sistema de archivos predeterminado de Hello implica un esquema predeterminado y la entidad.</span><span class="sxs-lookup"><span data-stu-id="9e048-108">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="9e048-109">También puede ser tooresolve usa rutas de acceso relativas.</span><span class="sxs-lookup"><span data-stu-id="9e048-109">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="9e048-110">Durante el proceso de creación de clúster de HDInsight de hello, puede especificar un contenedor de blobs en almacenamiento de Azure como sistema de archivos predeterminado de Hola o con HDInsight 3.5, puede seleccionar el almacenamiento de Azure o almacén de Azure Data Lake como sistema de archivos predeterminado de hello con unas pocas excepciones.</span><span class="sxs-lookup"><span data-stu-id="9e048-110">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> <span data-ttu-id="9e048-111">Por motivos de compatibilidad de hello del uso de almacén de Data Lake como valor predeterminado de Hola y almacenamiento vinculado, vea [Availabilities para clúster de HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="9e048-111">For hello supportability of using Data Lake Store as both hello default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="9e048-112">En este artículo, aprenderá cómo funciona Azure Storage con clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e048-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="9e048-113">toolearn cómo funciona el almacén de Data Lake con los clústeres de HDInsight, vea [clústeres de almacén de Data Lake utilice Azure con HDInsight de Azure](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="9e048-113">toolearn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="9e048-114">Consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obtener información sobre la creación de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e048-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="9e048-115">Azure Storage es una solución de almacenamiento sólida y de uso general, que se integra sin problemas con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e048-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="9e048-116">HDInsight puede usar un contenedor de blobs en almacenamiento de Azure como sistema de archivos predeterminado de Hola para clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-116">HDInsight can use a blob container in Azure Storage as hello default file system for hello cluster.</span></span> <span data-ttu-id="9e048-117">A través de una interfaz (HDFS) del sistema de archivos distribuido de Hadoop, conjunto completo de Hola de componentes de HDInsight puede trabajar directamente en los datos estructurados o no estructurados almacenados como blobs.</span><span class="sxs-lookup"><span data-stu-id="9e048-117">Through a Hadoop distributed file system (HDFS) interface, hello full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="9e048-118">Hay varias opciones disponibles al crear una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9e048-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="9e048-119">Hello en la tabla siguiente proporciona información sobre qué opciones son compatibles con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9e048-119">hello following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="9e048-120">Tipo de cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="9e048-120">Storage account type</span></span> | <span data-ttu-id="9e048-121">Capa de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="9e048-121">Storage tier</span></span> | <span data-ttu-id="9e048-122">Compatible con HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e048-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="9e048-123">Cuenta de almacenamiento de uso general</span><span class="sxs-lookup"><span data-stu-id="9e048-123">General-purpose Storage Account</span></span> | <span data-ttu-id="9e048-124">Estándar</span><span class="sxs-lookup"><span data-stu-id="9e048-124">Standard</span></span> | <span data-ttu-id="9e048-125">__Sí__</span><span class="sxs-lookup"><span data-stu-id="9e048-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="9e048-126">Premium</span><span class="sxs-lookup"><span data-stu-id="9e048-126">Premium</span></span> | <span data-ttu-id="9e048-127">No</span><span class="sxs-lookup"><span data-stu-id="9e048-127">No</span></span> |
> | <span data-ttu-id="9e048-128">Cuenta de Blob Storage</span><span class="sxs-lookup"><span data-stu-id="9e048-128">Blob Storage Account</span></span> | <span data-ttu-id="9e048-129">Acceso frecuente</span><span class="sxs-lookup"><span data-stu-id="9e048-129">Hot</span></span> | <span data-ttu-id="9e048-130">No</span><span class="sxs-lookup"><span data-stu-id="9e048-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="9e048-131">Acceso esporádico</span><span class="sxs-lookup"><span data-stu-id="9e048-131">Cool</span></span> | <span data-ttu-id="9e048-132">No</span><span class="sxs-lookup"><span data-stu-id="9e048-132">No</span></span> |

<span data-ttu-id="9e048-133">No se recomienda que utilice contenedor de blob de hello predeterminado para almacenar los datos empresariales.</span><span class="sxs-lookup"><span data-stu-id="9e048-133">We do not recommend that you use hello default blob container for storing business data.</span></span> <span data-ttu-id="9e048-134">Eliminar el contenedor de blob de hello predeterminado después de cada tooreduce de uso coste de almacenamiento es una buena práctica.</span><span class="sxs-lookup"><span data-stu-id="9e048-134">Deleting hello default blob container after each use tooreduce storage cost is a good practice.</span></span> <span data-ttu-id="9e048-135">Tenga en cuenta ese contenedor predeterminado de hello contiene la aplicación y del sistema registros.</span><span class="sxs-lookup"><span data-stu-id="9e048-135">Note that hello default container contains application and system logs.</span></span> <span data-ttu-id="9e048-136">Asegúrese de registros de hello tooretrieve seguro antes de eliminar el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-136">Make sure tooretrieve hello logs before deleting hello container.</span></span>

<span data-ttu-id="9e048-137">No se permite compartir un contenedor de blobs entre varios clústeres.</span><span class="sxs-lookup"><span data-stu-id="9e048-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="9e048-138">Arquitectura de almacenamiento de HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e048-138">HDInsight storage architecture</span></span>
<span data-ttu-id="9e048-139">Hola siguiente diagrama proporciona una vista de resumen de hello HDInsight arquitectura de almacenamiento de información de uso de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="9e048-139">hello following diagram provides an abstract view of hello HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="9e048-140">![Clústeres de Hadoop usar Hola HDFS API tooaccess y almacenan datos estructurados y no en el almacenamiento de blobs. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Arquitectura de almacenamiento de HDInsight")</span><span class="sxs-lookup"><span data-stu-id="9e048-140">![Hadoop clusters use hello HDFS API tooaccess and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="9e048-141">HDInsight proporciona toohello distribuida filesystem acceso localmente adjunta toohello nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="9e048-141">HDInsight provides access toohello distributed file system that is locally attached toohello compute nodes.</span></span> <span data-ttu-id="9e048-142">Puede tener acceso a este sistema de archivos mediante Hola completo URI, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9e048-142">This file system can be accessed by using hello fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="9e048-143">Además, HDInsight le permite tooaccess datos que se almacenan en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e048-143">In addition, HDInsight allows you tooaccess data that is stored in Azure Storage.</span></span> <span data-ttu-id="9e048-144">Hola sintaxis es:</span><span class="sxs-lookup"><span data-stu-id="9e048-144">hello syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="9e048-145">A la hora de usar una cuenta de Azure Storage con clústeres de HDInsight, es necesario tener en cuenta algunas cosas.</span><span class="sxs-lookup"><span data-stu-id="9e048-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="9e048-146">**Contenedores de las cuentas de almacenamiento de Hola que son tooa conectado con clústeres:** debido a nombre de la cuenta de hello y la clave están asociados con el clúster de Hola durante la creación, tienen blobs de toohello de acceso completa en estos contenedores.</span><span class="sxs-lookup"><span data-stu-id="9e048-146">**Containers in hello storage accounts that are connected tooa cluster:** Because hello account name and key are associated with hello cluster during creation, you have full access toohello blobs in those containers.</span></span>

* <span data-ttu-id="9e048-147">**Contenedores públicos o blobs públicos de las cuentas de almacenamiento que no están conectados clúster tooa:** tiene blobs de toohello de permiso de solo lectura en los contenedores de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-147">**Public containers or public blobs in storage accounts that are NOT connected tooa cluster:** You have read-only permission toohello blobs in hello containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="9e048-148">Contenedores públicos permiten tooget una lista de todos los blobs que están disponibles en ese contenedor y obtener metadatos del contenedor.</span><span class="sxs-lookup"><span data-stu-id="9e048-148">Public containers allow you tooget a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="9e048-149">Blobs públicos permiten blobs de hello tooaccess únicamente si sabe Hola la misma dirección URL.</span><span class="sxs-lookup"><span data-stu-id="9e048-149">Public blobs allow you tooaccess hello blobs only if you know hello exact URL.</span></span> <span data-ttu-id="9e048-150">Para obtener más información, consulte <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">restringir acceso toocontainers y blobs</a>.</span><span class="sxs-lookup"><span data-stu-id="9e048-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access toocontainers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="9e048-151">**Contenedores privados de las cuentas de almacenamiento que no están conectados clúster tooa:** no puede acceder a blobs de hello en contenedores de Hola a menos que defina la cuenta de almacenamiento de hello al enviar trabajos de hello WebHCat.</span><span class="sxs-lookup"><span data-stu-id="9e048-151">**Private containers in storage accounts that are NOT connected tooa cluster:** You can't access hello blobs in hello containers unless you define hello storage account when you submit hello WebHCat jobs.</span></span> <span data-ttu-id="9e048-152">Esto se explica posteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="9e048-152">This is explained later in this article.</span></span>

<span data-ttu-id="9e048-153">cuentas de almacenamiento de Hola que se definen en el proceso de creación de hello y sus claves están almacenadas en %HADOOP_HOME%/conf/core-site.xml en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-153">hello storage accounts that are defined in hello creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on hello cluster nodes.</span></span> <span data-ttu-id="9e048-154">comportamiento predeterminado de Hola de HDInsight es cuentas de almacenamiento de hello toouse definidas en el archivo de hello core-site.xml.</span><span class="sxs-lookup"><span data-stu-id="9e048-154">hello default behavior of HDInsight is toouse hello storage accounts defined in hello core-site.xml file.</span></span> <span data-ttu-id="9e048-155">Puede modificar esta configuración mediante [Ambari](./hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="9e048-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="9e048-156">Varios trabajos de WebHCat, incluidos Hive, MapReduce, streaming de Hadoop y Pig, pueden llevar una descripción de cuentas de almacenamiento y metadatos con ellos.</span><span class="sxs-lookup"><span data-stu-id="9e048-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="9e048-157">(Actualmente esto funciona para Pig con cuentas de almacenamiento pero no para metadatos). Para obtener más información, consulte [Uso de un clúster de HDInsight con cuentas de almacenamiento y tiendas de metadatos alternativas](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e048-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="9e048-158">Los blobs se pueden usar para datos estructurados y no estructurados.</span><span class="sxs-lookup"><span data-stu-id="9e048-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="9e048-159">Los contenedores de blobs almacenan los datos como pares de clave-valor y no hay jerarquía de directorios.</span><span class="sxs-lookup"><span data-stu-id="9e048-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="9e048-160">Sin embargo, puede usarse el carácter de barra diagonal (/) de hello en Hola toomake de nombre de la clave parece como si un archivo se almacena en una estructura de directorios.</span><span class="sxs-lookup"><span data-stu-id="9e048-160">However hello slash character ( / ) can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="9e048-161">Por ejemplo, la clave de un blob puede ser *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="9e048-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="9e048-162">No real *entrada* directorio existe, pero debido toohello presencia del carácter de barra diagonal de hello en nombre de clave de hello, tiene el aspecto de Hola de una ruta de acceso de archivo.</span><span class="sxs-lookup"><span data-stu-id="9e048-162">No actual *input* directory exists, but due toohello presence of hello slash character in hello key name, it has hello appearance of a file path.</span></span>

## <span data-ttu-id="9e048-163"><a id="benefits"></a>Ventajas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9e048-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="9e048-164">Hola implícito costo de rendimiento de los clústeres de cálculo no comparte ubicación y recursos de almacenamiento se mitiga con la forma de hello clústeres de cálculo de Hola se crean recursos toohello cerrar de la cuenta de almacenamiento dentro de hello región de Azure, en red de alta velocidad Hola facilita eficaz para los nodos de proceso de hello tooaccess Hola datos dentro de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e048-164">hello implied performance cost of not co-locating compute clusters and storage resources is mitigated by hello way hello compute clusters are created close toohello storage account resources inside hello Azure region, where hello high-speed network makes it efficient for hello compute nodes tooaccess hello data inside Azure storage.</span></span>

<span data-ttu-id="9e048-165">Hay varias ventajas asociados al almacenamiento de datos de hello en el almacenamiento de Azure en lugar de HDFS:</span><span class="sxs-lookup"><span data-stu-id="9e048-165">There are several benefits associated with storing hello data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="9e048-166">**Compartir y reutilizar los datos:** datos hello en HDFS se encuentran dentro del clúster de cálculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-166">**Data reuse and sharing:** hello data in HDFS is located inside hello compute cluster.</span></span> <span data-ttu-id="9e048-167">Solo las aplicaciones de Hola que tienen acceso toohello compute Cluster Server puede usar datos de hello mediante las API de HDFS.</span><span class="sxs-lookup"><span data-stu-id="9e048-167">Only hello applications that have access toohello compute cluster can use hello data by using HDFS APIs.</span></span> <span data-ttu-id="9e048-168">pueden tener acceso a datos de Hello en el almacenamiento de Azure a través de API de HDFS Hola o hello [API de REST de almacenamiento de blobs][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="9e048-168">hello data in Azure storage can be accessed either through hello HDFS APIs or through hello [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="9e048-169">Por lo tanto, un conjunto mayor de aplicaciones (incluidos los otros clústeres de HDInsight) y las herramientas puede ser utilizado tooproduce y consumir datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used tooproduce and consume hello data.</span></span>
* <span data-ttu-id="9e048-170">**Archivado de datos:** almacenar datos en el almacenamiento de Azure permite a los clústeres de HDInsight de hello usa para eliminar de forma segura sin perder los datos de usuario de toobe de cálculo.</span><span class="sxs-lookup"><span data-stu-id="9e048-170">**Data archiving:** Storing data in Azure storage enables hello HDInsight clusters used for computation toobe safely deleted without losing user data.</span></span>
* <span data-ttu-id="9e048-171">**Costo de almacenamiento de datos:** almacenar datos en DFS para a largo plazo de hello es más costoso que almacenamiento de datos de hello en el almacenamiento de Azure porque el costo de Hola de un clúster de cálculo es mayor que el costo de Hola de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e048-171">**Data storage cost:** Storing data in DFS for hello long term is more costly than storing hello data in Azure storage because hello cost of a compute cluster is higher than hello cost of Azure storage.</span></span> <span data-ttu-id="9e048-172">Además, porque los datos de hello no tienen toobe volver a cargar para cada generación de clúster de proceso, también se guardan los costos de la carga de datos.</span><span class="sxs-lookup"><span data-stu-id="9e048-172">In addition, because hello data does not have toobe reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="9e048-173">**Escalado horizontal elástico:** HDFS aunque se proporciona con un sistema de archivos de escala horizontal, escala Hola viene determinado por el número de Hola de nodos que se crean para el clúster.</span><span class="sxs-lookup"><span data-stu-id="9e048-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, hello scale is determined by hello number of nodes that you create for your cluster.</span></span> <span data-ttu-id="9e048-174">Cambiar escala Hola puede convertirse en un proceso más complicado que depender de elásticas Hola escalar las capacidades que se obtienen automáticamente en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e048-174">Changing hello scale can become a more complicated process than relying on hello elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="9e048-175">**Replicación geográfica:** su almacenamiento de Azure Storage se puede replicar geográficamente.</span><span class="sxs-lookup"><span data-stu-id="9e048-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="9e048-176">Aunque esta opción permite la recuperación geográfica y redundancia de datos, una ubicación de replicación geográfica de conmutación por error toohello afecta gravemente el rendimiento y pueden suponer costes adicionales.</span><span class="sxs-lookup"><span data-stu-id="9e048-176">Although this gives you geographic recovery and data redundancy, a failover toohello geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="9e048-177">Por lo que esta es nuestra recomendación es toochoose Hola replicación geográfica con cuidado y sólo si es valor de Hola de los datos de hello correspondientes Hola costo adicional alguno.</span><span class="sxs-lookup"><span data-stu-id="9e048-177">So our recommendation is toochoose hello geo-replication wisely and only if hello value of hello data is worth hello additional cost.</span></span>

<span data-ttu-id="9e048-178">Ciertos trabajos MapReduce y paquetes pueden crear resultados intermedios que realmente no desea toostore en almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e048-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want toostore in Azure storage.</span></span> <span data-ttu-id="9e048-179">En ese caso, puede elegir datos de hello toostore en Hola HDFS local.</span><span class="sxs-lookup"><span data-stu-id="9e048-179">In that case, you can elect toostore hello data in hello local HDFS.</span></span> <span data-ttu-id="9e048-180">De hecho, HDInsight usa DFS para varios de estos resultados intermedios en los trabajos de Hive y otros procesos.</span><span class="sxs-lookup"><span data-stu-id="9e048-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="9e048-181">La mayoría de los comandos HDFS (por ejemplo, <b>ls</b>, <b>copyFromLocal</b> y <b>mkdir</b>) siguen funcionando según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="9e048-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="9e048-182">Hola sólo los comandos que son específicos toohello nativo HDFS la implementación (que es lo que se conoce tooas DFS), como <b>fschk</b> y <b>dfsadmin</b>, mostrar un comportamiento diferente en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e048-182">Only hello commands that are specific toohello native HDFS implementation (which is referred tooas DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="9e048-183">Creación de contenedores de blobs</span><span class="sxs-lookup"><span data-stu-id="9e048-183">Create Blob containers</span></span>
<span data-ttu-id="9e048-184">toouse blobs, cree primero un [cuenta de almacenamiento de Azure][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="9e048-184">toouse blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="9e048-185">Como parte de esto, especifique una región de Azure donde se crea la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-185">As part of this, you specify an Azure region where hello storage account is created.</span></span> <span data-ttu-id="9e048-186">clúster de Hola y cuenta de almacenamiento de hello deben estar hospedados en hello misma región.</span><span class="sxs-lookup"><span data-stu-id="9e048-186">hello cluster and hello storage account must be hosted in hello same region.</span></span> <span data-ttu-id="9e048-187">base de datos de SQL Server de tienda de metadatos de Hello Hive y tienda de metadatos de Oozie SQL Server, base de datos también debe estar ubicado en Hola misma región.</span><span class="sxs-lookup"><span data-stu-id="9e048-187">hello Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in hello same region.</span></span>

<span data-ttu-id="9e048-188">Siempre que vive, cada blob que se crea pertenece tooa contenedor en la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e048-188">Wherever it lives, each blob you create belongs tooa container in your Azure Storage account.</span></span> <span data-ttu-id="9e048-189">Este contenedor puede ser un blob existente creado fuera de HDInsight, o bien un contenedor que se crea para un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e048-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="9e048-190">contenedor de Blob de Hello predeterminado almacena información específica del clúster como registros y el historial de trabajos.</span><span class="sxs-lookup"><span data-stu-id="9e048-190">hello default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="9e048-191">No comparta un contenedor de blobs predeterminado con varios clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e048-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="9e048-192">Se podría dañar el historial de trabajos.</span><span class="sxs-lookup"><span data-stu-id="9e048-192">This might corrupt job history.</span></span> <span data-ttu-id="9e048-193">Se recomienda toouse un contenedor diferente para cada clúster y colocar los datos compartidos en una cuenta de almacenamiento vinculado especificada en la implementación de todos los clústeres en lugar de la cuenta de almacenamiento predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-193">It is recommended toouse a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than hello default storage account.</span></span> <span data-ttu-id="9e048-194">Para más información acerca de cómo configurar cuentas de almacenamiento vinculadas, consulte [Creación de clústeres de HDInsight][hdinsight-creation].</span><span class="sxs-lookup"><span data-stu-id="9e048-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="9e048-195">Sin embargo puede reutilizar un contenedor de almacenamiento de forma predeterminada una vez se ha eliminado el clúster de HDInsight original de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-195">However you can reuse a default storage container after hello original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="9e048-196">Para los clústeres de HBase, realmente puede conservar datos y esquema de la tabla de hello HBase mediante la creación de un nuevo clúster de HBase mediante el contenedor de blobs de hello predeterminado utilizado por un clúster de HBase que se ha eliminado.</span><span class="sxs-lookup"><span data-stu-id="9e048-196">For HBase clusters, you can actually retain hello HBase table schema and data by creating a new HBase cluster using hello default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a><span data-ttu-id="9e048-197">Usar hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9e048-197">Use hello Azure portal</span></span>
<span data-ttu-id="9e048-198">Al crear un clúster de HDInsight desde el Portal de hello, tiene detalles de la cuenta de hello opciones (tal y como se muestra a continuación) tooprovide Hola almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9e048-198">When creating an HDInsight cluster from hello Portal, you have hello options (as shown below) tooprovide hello storage account details.</span></span> <span data-ttu-id="9e048-199">También puede especificar si desea que una cuenta de almacenamiento adicionales asociados con el clúster de hello y, si es así, elija desde otro blob de almacenamiento de Azure como almacenamiento adicional de Hola o de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="9e048-199">You can also specify whether you want an additional storage account associated with hello cluster, and if so, choose from Data Lake Store or another Azure Storage blob as hello additional storage.</span></span>

![Origen de datos de creación de un clúster de Hadoop en HDInsight](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="9e048-201">No se admite con una cuenta de almacenamiento adicional en una ubicación diferente que el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-201">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="9e048-202">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e048-202">Use Azure PowerShell</span></span>
<span data-ttu-id="9e048-203">Si se [instalado y configurado Azure PowerShell][powershell-install], puede usar Hola siguientes de hello Azure PowerShell prompt toocreate una cuenta de almacenamiento y el contenedor:</span><span class="sxs-lookup"><span data-stu-id="9e048-203">If you [installed and configured Azure PowerShell][powershell-install], you can use hello following from hello Azure PowerShell prompt toocreate a storage account and container:</span></span>

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

### <a name="use-azure-cli"></a><span data-ttu-id="9e048-204">Uso de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9e048-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="9e048-205">Si tiene [instalado y configurado hello Azure CLI](../cli-install-nodejs.md), siguiente Hola comando puede ser usado tooa cuenta de almacenamiento y el contenedor.</span><span class="sxs-lookup"><span data-stu-id="9e048-205">If you have [installed and configured hello Azure CLI](../cli-install-nodejs.md), hello following command can be used tooa storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="9e048-206">Hola `--type` parámetro indica cómo se replica la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-206">hello `--type` parameter indicates how hello storage account is replicated.</span></span> <span data-ttu-id="9e048-207">Para obtener más información, vea [Replicación de Azure Storage](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="9e048-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="9e048-208">No utilice ZRS, ya que no admite blob en páginas, archivo, tabla o cola.</span><span class="sxs-lookup"><span data-stu-id="9e048-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="9e048-209">Son región geográfica de toospecify solicitadas Hola que se crea la cuenta de almacenamiento de hello en.</span><span class="sxs-lookup"><span data-stu-id="9e048-209">You are prompted toospecify hello geographic region that hello storage account is created in.</span></span> <span data-ttu-id="9e048-210">Debe crear cuenta de almacenamiento de Hola Hola misma región que piensa sobre la creación de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e048-210">You should create hello storage account in hello same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="9e048-211">Una vez creada la cuenta de almacenamiento de hello, utilice Hola después de claves de la cuenta de almacenamiento de comando tooretrieve hello:</span><span class="sxs-lookup"><span data-stu-id="9e048-211">Once hello storage account is created, use hello following command tooretrieve hello storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="9e048-212">toocreate un contenedor, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9e048-212">toocreate a container, use hello following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="9e048-213">Archivos adicionales en Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9e048-213">Address files in Azure storage</span></span>
<span data-ttu-id="9e048-214">es el esquema URI de Hello para tener acceso a archivos de almacenamiento de Azure de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9e048-214">hello URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="9e048-215">esquema URI de Hello proporciona acceso sin cifrar (con hello *wasb:* prefijo) y acceso de cifrado de SSL (con *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="9e048-215">hello URI scheme provides unencrypted access (with hello *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="9e048-216">Se recomienda usar *wasbs* siempre que sea posible, incluso cuando el acceso a datos que residen dentro de Hola misma región de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e048-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside hello same region in Azure.</span></span>

<span data-ttu-id="9e048-217">Hola &lt;BlobStorageContainerName&gt; identifica Hola nombre de contenedor de blobs de hello en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e048-217">hello &lt;BlobStorageContainerName&gt; identifies hello name of hello blob container in Azure storage.</span></span>
<span data-ttu-id="9e048-218">Hola &lt;StorageAccountName&gt; identifica el nombre de cuenta de almacenamiento de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-218">hello &lt;StorageAccountName&gt; identifies hello Azure Storage account name.</span></span> <span data-ttu-id="9e048-219">Se necesita el nombre completo de dominio (FQDN).</span><span class="sxs-lookup"><span data-stu-id="9e048-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="9e048-220">Si no &lt;BlobStorageContainerName&gt; ni &lt;StorageAccountName&gt; se ha especificado, se utiliza el sistema de archivos predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, hello default file system is used.</span></span> <span data-ttu-id="9e048-221">Para los archivos de hello en el sistema de archivos predeterminado de hello, puede usar una ruta de acceso relativa o absoluta.</span><span class="sxs-lookup"><span data-stu-id="9e048-221">For hello files on hello default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="9e048-222">Por ejemplo, hello *archivo hadoop mapreduce examples.jar* archivo que se incluye con clústeres de HDInsight puede tooby que se hace referencia mediante uno de los siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="9e048-222">For example, hello *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred tooby using one of hello following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="9e048-223">nombre de archivo de Hello es <i>archivo hadoop-examples.jar</i> en clústeres de HDInsight las versiones 2.1 y 1.6.</span><span class="sxs-lookup"><span data-stu-id="9e048-223">hello file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="9e048-224">Hola &lt;ruta de acceso&gt; es el nombre de ruta de acceso HDFS de archivo o directorio Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-224">hello &lt;path&gt; is hello file or directory HDFS path name.</span></span> <span data-ttu-id="9e048-225">Dado que los contenedores de Azure Storage son solamente almacenes de pares clave-valor, no hay ningún sistema de archivos jerárquico real.</span><span class="sxs-lookup"><span data-stu-id="9e048-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="9e048-226">Un carácter de barra inclinada ( / ) dentro de la clave de blob se interpreta como separador de directorios.</span><span class="sxs-lookup"><span data-stu-id="9e048-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="9e048-227">Por ejemplo, nombre de blob de Hola para *archivo hadoop mapreduce examples.jar* es:</span><span class="sxs-lookup"><span data-stu-id="9e048-227">For example, hello blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="9e048-228">Cuando se trabaja con los blobs fuera de HDInsight, mayoría de las utilidades no reconoce el formato WASB de Hola y en su lugar, espera un formato básico de la ruta de acceso, como `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="9e048-228">When working with blobs outside of HDInsight, most utilities do not recognize hello WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="9e048-229">Acceso a blobs</span><span class="sxs-lookup"><span data-stu-id="9e048-229">Access blobs</span></span> 


### <span data-ttu-id="9e048-230"><a name="access-blobs-using-azure-powershell"></a> Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e048-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="9e048-231">comandos de Hello en esta sección proporcionan un ejemplo básico de usar PowerShell tooaccess datos almacenados en blobs.</span><span class="sxs-lookup"><span data-stu-id="9e048-231">hello commands in this section provide a basic example of using PowerShell tooaccess data stored in blobs.</span></span> <span data-ttu-id="9e048-232">Para obtener un ejemplo más completo que se personaliza para trabajar con HDInsight, vea hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="9e048-232">For a more full-featured example that is customized for working with HDInsight, see hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="9e048-233">Usar hello después comando toolist Hola relacionados con el blob cmdlets:</span><span class="sxs-lookup"><span data-stu-id="9e048-233">Use hello following command toolist hello blob-related cmdlets:</span></span>

    Get-Command *blob*

![Lista de cmdlets de PowerShell relacionados con el blob.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="9e048-235">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="9e048-235">Upload files</span></span>
<span data-ttu-id="9e048-236">Vea [cargar datos tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="9e048-236">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="9e048-237">Descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="9e048-237">Download files</span></span>
<span data-ttu-id="9e048-238">Hello secuencia de comandos siguiente descarga una carpeta en la toohello de blob de bloque actual.</span><span class="sxs-lookup"><span data-stu-id="9e048-238">hello following script downloads a block blob toohello current folder.</span></span> <span data-ttu-id="9e048-239">Antes de ejecutar script de Hola, cambiar carpeta del directorio de hello tooa que tiene permisos de escritura.</span><span class="sxs-lookup"><span data-stu-id="9e048-239">Before running hello script, change hello directory tooa folder where you have write permissions.</span></span>

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

<span data-ttu-id="9e048-240">Proporcionar el nombre de grupo de recursos de Hola y el nombre de clúster de hello, puede usar Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="9e048-240">Providing hello resource group name and hello cluster name, you can use hello following code:</span></span>

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


#### <a name="delete-files"></a><span data-ttu-id="9e048-241">Eliminar archivos</span><span class="sxs-lookup"><span data-stu-id="9e048-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="9e048-242">Enumerar archivos</span><span class="sxs-lookup"><span data-stu-id="9e048-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="9e048-243">Ejecutar consultas de Hive usando una cuenta de almacenamiento sin definir</span><span class="sxs-lookup"><span data-stu-id="9e048-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="9e048-244">Este ejemplo muestra cómo toolist una carpeta de la cuenta de almacenamiento que no está definido durante Hola proceso de creación.</span><span class="sxs-lookup"><span data-stu-id="9e048-244">This example shows how toolist a folder from storage account that is not defined during hello creating process.</span></span>
<span data-ttu-id="9e048-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="9e048-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="9e048-246">Uso de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9e048-246">Use Azure CLI</span></span>
<span data-ttu-id="9e048-247">Usar hello siga los comandos relacionados con el blob del comando toolist hello:</span><span class="sxs-lookup"><span data-stu-id="9e048-247">Use hello following command toolist hello blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="9e048-248">**Ejemplo del uso de tooupload un archivo de CLI de Azure**</span><span class="sxs-lookup"><span data-stu-id="9e048-248">**Example of using Azure CLI tooupload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="9e048-249">**Ejemplo del uso de toodownload un archivo de CLI de Azure**</span><span class="sxs-lookup"><span data-stu-id="9e048-249">**Example of using Azure CLI toodownload a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="9e048-250">**Ejemplo del uso de CLI de Azure toodelete un archivo**</span><span class="sxs-lookup"><span data-stu-id="9e048-250">**Example of using Azure CLI toodelete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="9e048-251">**Ejemplo del uso de archivos de toolist de CLI de Azure**</span><span class="sxs-lookup"><span data-stu-id="9e048-251">**Example of using Azure CLI toolist files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="9e048-252">Uso de cuentas de almacenamiento adicionales</span><span class="sxs-lookup"><span data-stu-id="9e048-252">Use additional storage accounts</span></span>

<span data-ttu-id="9e048-253">Al crear un clúster de HDInsight, especificar cuenta de almacenamiento de Azure de Hola que desee tooassociate con él.</span><span class="sxs-lookup"><span data-stu-id="9e048-253">While creating an HDInsight cluster, you specify hello Azure Storage account you want tooassociate with it.</span></span> <span data-ttu-id="9e048-254">Además toothis cuenta de almacenamiento, puede agregar cuentas de almacenamiento adicional de hello misma suscripción de Azure o suscripciones de Azure diferentes durante el proceso de creación de Hola o después de que se ha creado un clúster.</span><span class="sxs-lookup"><span data-stu-id="9e048-254">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or different Azure subscriptions during hello creation process or after a cluster has been created.</span></span> <span data-ttu-id="9e048-255">Para obtener instrucciones sobre cómo agregar más cuentas de almacenamiento, consulte [Creación de clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9e048-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="9e048-256">No se admite con una cuenta de almacenamiento adicional en una ubicación diferente que el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="9e048-256">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e048-257">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9e048-257">Next steps</span></span>
<span data-ttu-id="9e048-258">En este artículo, se habrá aprendido cómo toouse HDFS compatible con el almacenamiento de Azure con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e048-258">In this article, you learned how toouse HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="9e048-259">Esto le permite toobuild escalable y a largo plazo, archivado soluciones de adquisición de datos y usar información de hello toounlock de HDInsight dentro de hello almacenado estructurado y datos no estructurados.</span><span class="sxs-lookup"><span data-stu-id="9e048-259">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="9e048-260">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="9e048-260">For more information, see:</span></span>

* <span data-ttu-id="9e048-261">[Introducción a Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="9e048-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="9e048-262">Introducción Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9e048-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="9e048-263">[Cargar datos tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="9e048-263">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="9e048-264">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="9e048-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="9e048-265">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="9e048-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="9e048-266">[Usar firmas de acceso compartido de almacenamiento de Azure toorestrict acceso toodata con HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="9e048-266">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
