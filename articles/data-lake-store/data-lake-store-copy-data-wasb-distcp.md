---
title: "aaaCopy datos tooand de WASB en el almacén de Data Lake con Distcp | Documentos de Microsoft"
description: "Usar Distcp herramienta toocopy datos tooand almacenamiento de Blobs tooData Lake del almacén de Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="2079d-103">Usar Distcp toocopy datos entre los Blobs de almacenamiento de Azure y almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2079d-103">Use Distcp toocopy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2079d-104">Uso de DistCp</span><span class="sxs-lookup"><span data-stu-id="2079d-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="2079d-105">Uso de AdlCopy</span><span class="sxs-lookup"><span data-stu-id="2079d-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="2079d-106">Una vez haya creado un clúster de HDInsight con la cuenta de acceso de almacén de Data Lake tooa, también puede usar herramientas de ecosistema de Hadoop como Distcp toocopy datos **tooand de** un almacenamiento de clúster de HDInsight (WASB) en una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2079d-106">Once you have created an HDInsight cluster that has access tooa Data Lake Store account, you can use Hadoop ecosystem tools like Distcp toocopy data **tooand from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="2079d-107">Este artículo proporciona instrucciones sobre cómo tooachieve esto.</span><span class="sxs-lookup"><span data-stu-id="2079d-107">This article provides instructions on how tooachieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2079d-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2079d-108">Prerequisites</span></span>
<span data-ttu-id="2079d-109">Antes de comenzar este artículo, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="2079d-109">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="2079d-110">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="2079d-110">**An Azure subscription**.</span></span> <span data-ttu-id="2079d-111">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2079d-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2079d-112">**Una cuenta de Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="2079d-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="2079d-113">Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2079d-113">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="2079d-114">**Clúster de HDInsight de Azure** con acceso tooa cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2079d-114">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="2079d-115">Consulte [Creación de un clúster de HDInsight con Data Lake Store mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2079d-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="2079d-116">Asegúrese de que habilitar Escritorio remoto para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="2079d-116">Make sure you enable Remote Desktop for hello cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="2079d-117">¿Obtener información más rápidamente con vídeos?</span><span class="sxs-lookup"><span data-stu-id="2079d-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="2079d-118">[Vea este vídeo](https://mix.office.com/watch/1liuojvdx6sie) acerca de cómo toocopy datos entre los Blobs de almacenamiento de Azure y almacén de Data Lake mediante DistCp.</span><span class="sxs-lookup"><span data-stu-id="2079d-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="2079d-119">Usar Distcp desde un clúster de HDInsight de Linux</span><span class="sxs-lookup"><span data-stu-id="2079d-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="2079d-120">Un clúster de HDInsight que se incluye con la utilidad Distcp hello, que puede ser utilizados toocopy datos de orígenes diferentes en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2079d-120">An HDInsight cluster comes with hello Distcp utility, which can be used toocopy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="2079d-121">Si ha configurado el almacén de hello HDInsight clúster toouse Data Lake como un almacenamiento adicional, hello Distcp utilidad se puede utiliza tooand de datos de cuadro toocopy desde una cuenta del almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2079d-121">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, hello Distcp utility can be used out-of-the-box toocopy data tooand from a Data Lake Store account as well.</span></span> <span data-ttu-id="2079d-122">En esta sección veremos cómo toouse Hola Distcp utilidad.</span><span class="sxs-lookup"><span data-stu-id="2079d-122">In this section we look at how toouse hello Distcp utility.</span></span>

1. <span data-ttu-id="2079d-123">Desde el escritorio, use SSH tooconnect toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="2079d-123">From your desktop, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="2079d-124">Vea [clúster de HDInsight basados en Linux de conectar tooa](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2079d-124">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="2079d-125">Ejecute comandos de Hola desde el símbolo del sistema de hello SSH.</span><span class="sxs-lookup"><span data-stu-id="2079d-125">Run hello commands from hello SSH prompt.</span></span>

2. <span data-ttu-id="2079d-126">Compruebe si puede tener acceso a Hola Blobs de almacenamiento de Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="2079d-126">Verify whether you can access hello Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="2079d-127">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="2079d-127">Run hello following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="2079d-128">Esto debería proporcionar una lista de contenido de blob de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2079d-128">This should provide a list of contents in hello storage blob.</span></span>
3. <span data-ttu-id="2079d-129">De forma similar, compruebe si tiene acceso a cuenta de almacén de Data Lake Hola de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="2079d-129">Similarly, verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="2079d-130">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="2079d-130">Run hello following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="2079d-131">Esto debería proporcionar una lista de archivos o carpetas en hello cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2079d-131">This should provide a list of files/folders in hello Data Lake Store account.</span></span>
4. <span data-ttu-id="2079d-132">Usar datos de toocopy de Distcp de WASB tooa cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2079d-132">Use Distcp toocopy data from WASB tooa Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="2079d-133">Esto copiará el contenido de Hola de hello **/ejemplo/datos/gutenberg/** carpeta en WASB demasiado**/myfolder** Hola cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2079d-133">This will copy hello contents of hello **/example/data/gutenberg/** folder in WASB too**/myfolder** in hello Data Lake Store account.</span></span>
5. <span data-ttu-id="2079d-134">Asimismo, utilice Distcp toocopy datos de almacén de Data Lake cuenta tooWASB.</span><span class="sxs-lookup"><span data-stu-id="2079d-134">Similarly, use Distcp toocopy data from Data Lake Store account tooWASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="2079d-135">Esto copiará el contenido de Hola de **/myfolder** Hola almacén de Data Lake cuenta demasiado**/ejemplo/datos/gutenberg/** carpeta en WASB.</span><span class="sxs-lookup"><span data-stu-id="2079d-135">This will copy hello contents of **/myfolder** in hello Data Lake Store account too**/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="2079d-136">Consideraciones de rendimiento sobre el uso de DistCp</span><span class="sxs-lookup"><span data-stu-id="2079d-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="2079d-137">Porque DistCp's menor granularidad es un único archivo, establecer número máximo de Hola de copias simultáneas es hello toooptimize de parámetro más importante con el almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2079d-137">Because DistCp’s lowest granularity is a single file, setting hello maximum number of simultaneous copies is hello most important parameter toooptimize it against Data Lake Store.</span></span> <span data-ttu-id="2079d-138">Esto se controla estableciendo el número de Hola de asignadores ('m ') parámetro en la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2079d-138">This is controlled by setting hello number of mappers (‘m’) parameter on hello command line.</span></span> <span data-ttu-id="2079d-139">Este parámetro especifica el número máximo de Hola de asignadores que será usado toocopy datos.</span><span class="sxs-lookup"><span data-stu-id="2079d-139">This parameter specifies hello maximum number of mappers that will be used toocopy data.</span></span> <span data-ttu-id="2079d-140">El valor predeterminado es 20.</span><span class="sxs-lookup"><span data-stu-id="2079d-140">Default value is 20.</span></span>

<span data-ttu-id="2079d-141">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="2079d-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a><span data-ttu-id="2079d-142">¿Cómo se determina el número de Hola de asignadores toouse?</span><span class="sxs-lookup"><span data-stu-id="2079d-142">How do I determine hello number of mappers toouse?</span></span>

<span data-ttu-id="2079d-143">A continuación hay algunas instrucciones que puede usar.</span><span class="sxs-lookup"><span data-stu-id="2079d-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="2079d-144">**Paso 1: Determinar la memoria total de YARN** -Hola primer paso es clúster toodetermine hello YARN memoria disponible toohello donde ejecutar trabajo de DistCp Hola.</span><span class="sxs-lookup"><span data-stu-id="2079d-144">**Step 1: Determine total YARN memory** - hello first step is toodetermine hello YARN memory available toohello cluster where you run hello DistCp job.</span></span> <span data-ttu-id="2079d-145">Esta información está disponible en el portal de Ambari Hola asociada Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="2079d-145">This information is available in hello Ambari portal associated with hello cluster.</span></span> <span data-ttu-id="2079d-146">Navegue tooYARN y ver Hola configuraciones pestaña toosee hello YARN memoria.</span><span class="sxs-lookup"><span data-stu-id="2079d-146">Navigate tooYARN and view hello Configs tab toosee hello YARN memory.</span></span> <span data-ttu-id="2079d-147">tooget hello YARN memoria total, multiplicar Hola de memoria YARN por nodo con el número de Hola de nodos tienen en el clúster.</span><span class="sxs-lookup"><span data-stu-id="2079d-147">tooget hello total YARN memory, multiply hello YARN memory per node with hello number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="2079d-148">**Paso 2: Calcular el número de Hola de asignadores** -Hola valo **m** es toohello igual cociente de la memoria total de YARN dividido por hello tamaño del contenedor YARN.</span><span class="sxs-lookup"><span data-stu-id="2079d-148">**Step 2: Calculate hello number of mappers** - hello value of **m** is equal toohello quotient of total YARN memory divided by hello YARN container size.</span></span> <span data-ttu-id="2079d-149">Hola información de tamaño del contenedor YARN está disponible en el portal de Ambari Hola también.</span><span class="sxs-lookup"><span data-stu-id="2079d-149">hello YARN container size information is available in hello Ambari portal as well.</span></span> <span data-ttu-id="2079d-150">Navegue tooYARN y vista Hola configuraciones ficha Hola tamaño de contenedor YARN se muestra en esta ventana.</span><span class="sxs-lookup"><span data-stu-id="2079d-150">Navigate tooYARN and view hello Configs tab. hello YARN container size is displayed in this window.</span></span> <span data-ttu-id="2079d-151">Hola tooarrive ecuación en el número de Hola de asignadores (**m**) es</span><span class="sxs-lookup"><span data-stu-id="2079d-151">hello equation tooarrive at hello number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="2079d-152">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="2079d-152">**Example**</span></span>

<span data-ttu-id="2079d-153">Supongamos que tiene un 4 nodos D14v2s en clúster de Hola y que está tratando de tootransfer 10TB de datos de 10 carpetas diferentes.</span><span class="sxs-lookup"><span data-stu-id="2079d-153">Let’s assume that you have a 4 D14v2s nodes in hello cluster and you are trying tootransfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="2079d-154">Cada una de las carpetas de hello contienen diferentes cantidades de datos y tamaños de archivo hello dentro de cada carpeta son diferentes.</span><span class="sxs-lookup"><span data-stu-id="2079d-154">Each of hello folders contain varying amounts of data and hello file sizes within each folder are different.</span></span>

* <span data-ttu-id="2079d-155">Memoria total de YARN - de hello portal Ambari determinar esa memoria YARN hello es 96GB para un nodo de D14.</span><span class="sxs-lookup"><span data-stu-id="2079d-155">Total YARN memory - From hello Ambari portal you determine that hello YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="2079d-156">Por lo tanto, la memoria de YARN total para el clúster de 4 nodos es:</span><span class="sxs-lookup"><span data-stu-id="2079d-156">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="2079d-157">Número de asignadores - de hello portal Ambari determinar que ese tamaño de contenedor YARN hello es 3072 para un nodo de clúster D14.</span><span class="sxs-lookup"><span data-stu-id="2079d-157">Number of mappers - From hello Ambari portal you determine that hello YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="2079d-158">Por lo tanto, el número de asignadores es:</span><span class="sxs-lookup"><span data-stu-id="2079d-158">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="2079d-159">Si otras aplicaciones utilizan la memoria, puede elegir la utilización de tooonly parte de la memoria de hilo de su clúster para DistCp.</span><span class="sxs-lookup"><span data-stu-id="2079d-159">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="2079d-160">Copia de grandes conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="2079d-160">Copying large datasets</span></span>

<span data-ttu-id="2079d-161">Cuando desplaza el tamaño de Hola de hello toobe de conjunto de datos es muy grande (por ejemplo, > 1TB) o si tiene muchas carpetas distintas, considere la posibilidad de usar varios trabajos de DistCp.</span><span class="sxs-lookup"><span data-stu-id="2079d-161">When hello size of hello dataset toobe moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="2079d-162">Es probable que no hay ninguna mejora de rendimiento, pero se propagan trabajos hello, por lo que si se produce un error en cualquier trabajo, solo tendrá que toorestart ese trabajo específico en lugar de trabajo completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2079d-162">There is likely no performance gain, but it will spread out hello jobs so that if any job fails, you will only need toorestart that specific job rather than hello entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="2079d-163">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="2079d-163">Limitations</span></span>

* <span data-ttu-id="2079d-164">DistCp intenta a asignadores toocreate que son similares en el rendimiento de toooptimize de tamaño.</span><span class="sxs-lookup"><span data-stu-id="2079d-164">DistCp tries toocreate mappers that are similar in size toooptimize performance.</span></span> <span data-ttu-id="2079d-165">Aumentar el número de Hola de asignadores puede no siempre aumentar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2079d-165">Increasing hello number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="2079d-166">DistCp es tooonly limitado el uno asignador por cada archivo.</span><span class="sxs-lookup"><span data-stu-id="2079d-166">DistCp is limited tooonly one mapper per file.</span></span> <span data-ttu-id="2079d-167">Por lo tanto, no debería tener más asignadores que archivos.</span><span class="sxs-lookup"><span data-stu-id="2079d-167">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="2079d-168">Puesto que DistCp solo puede asignar al asignador de un archivo de tooa, esto limita la cantidad de Hola de simultaneidad que puede ser archivos de gran tamaño toocopy usado.</span><span class="sxs-lookup"><span data-stu-id="2079d-168">Since DistCp can only assign one mapper tooa file, this limits hello amount of concurrency that can be used toocopy large files.</span></span>

* <span data-ttu-id="2079d-169">Si tiene un pequeño número de archivos de gran tamaño, a continuación, se deben dividir en una toogive de fragmentos de archivo de 256MB se más simultaneidad posible.</span><span class="sxs-lookup"><span data-stu-id="2079d-169">If you have a small number of large files, then you should split them into 256MB file chunks toogive you more potential concurrency.</span></span> 
 
* <span data-ttu-id="2079d-170">Si va a copiar de una cuenta de almacenamiento de blobs de Azure, se puede limitar el trabajo de copia en lado de almacenamiento de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="2079d-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on hello blob storage side.</span></span> <span data-ttu-id="2079d-171">Esto disminuirá el rendimiento de Hola de su trabajo de copia.</span><span class="sxs-lookup"><span data-stu-id="2079d-171">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="2079d-172">toolearn más información acerca de los límites de Hola de almacenamiento de blobs de Azure, consulte los límites de almacenamiento de Azure en [suscripción de Azure y límites de servicio](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="2079d-172">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2079d-173">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="2079d-173">See also</span></span>
* [<span data-ttu-id="2079d-174">Copiar los datos de almacén de Blobs de Azure almacenamiento Lake tooData</span><span class="sxs-lookup"><span data-stu-id="2079d-174">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="2079d-175">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2079d-175">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="2079d-176">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2079d-176">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="2079d-177">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2079d-177">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
