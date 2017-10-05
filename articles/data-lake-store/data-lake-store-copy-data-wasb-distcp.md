---
title: Copia de datos a y desde WASB en Data Lake Store mediante Distcp| Microsoft Docs
description: "Use la herramienta Distcp para copiar datos a y desde los blobs de Almacenamiento de Azure al Almacén de Data Lake."
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
ms.openlocfilehash: 356a93d330e9e8ce3eb3c6c982fc5c2e087846a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="c2eed-103">Utilice Distcp para copiar datos entre los blobs de Almacenamiento de Azure y el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="c2eed-103">Use Distcp to copy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2eed-104">Uso de DistCp</span><span class="sxs-lookup"><span data-stu-id="c2eed-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="c2eed-105">Uso de AdlCopy</span><span class="sxs-lookup"><span data-stu-id="c2eed-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="c2eed-106">Una vez que haya creado un clúster de HDInsight que tenga acceso a una cuenta Data Lake Store, puede usar herramientas de ecosistema de Hadoop como Distcp para copiar datos **a y desde** un almacenamiento de clúster de HDInsight (WASB) en una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c2eed-106">Once you have created an HDInsight cluster that has access to a Data Lake Store account, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="c2eed-107">En este artículo se ofrecen instrucciones sobre cómo lograr esto.</span><span class="sxs-lookup"><span data-stu-id="c2eed-107">This article provides instructions on how to achieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2eed-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c2eed-108">Prerequisites</span></span>
<span data-ttu-id="c2eed-109">Antes de empezar este artículo, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c2eed-109">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="c2eed-110">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="c2eed-110">**An Azure subscription**.</span></span> <span data-ttu-id="c2eed-111">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2eed-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c2eed-112">**Una cuenta de Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="c2eed-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="c2eed-113">Para obtener instrucciones sobre cómo crear una, consulte la [introducción al Almacén de Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c2eed-113">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="c2eed-114">**Clúster de HDInsight de Azure** con acceso a una cuenta de Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c2eed-114">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="c2eed-115">Consulte [Creación de un clúster de HDInsight con Data Lake Store mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c2eed-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="c2eed-116">Asegúrese de habilitar el Escritorio remoto para el clúster.</span><span class="sxs-lookup"><span data-stu-id="c2eed-116">Make sure you enable Remote Desktop for the cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="c2eed-117">¿Obtener información más rápidamente con vídeos?</span><span class="sxs-lookup"><span data-stu-id="c2eed-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="c2eed-118">[Vea este vídeo](https://mix.office.com/watch/1liuojvdx6sie) para saber cómo copiar datos entre los blobs de Almacenamiento de Azure y Almacén de Data Lake mediante DistCp.</span><span class="sxs-lookup"><span data-stu-id="c2eed-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="c2eed-119">Usar Distcp desde un clúster de HDInsight de Linux</span><span class="sxs-lookup"><span data-stu-id="c2eed-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="c2eed-120">Un clúster de HDInsight incluye la utilidad Distcp, que puede utilizarse para copiar datos de orígenes diferentes en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2eed-120">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="c2eed-121">Si ha configurado el clúster de HDInsight para utilizar el Almacén de Data Lake como almacenamiento adicional, la utilidad Distcp puede utilizarse también directamente y sin configuraciones adicionales para copiar datos a y desde una cuenta de Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c2eed-121">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Store account as well.</span></span> <span data-ttu-id="c2eed-122">En esta sección veremos cómo usar la utilidad Distcp.</span><span class="sxs-lookup"><span data-stu-id="c2eed-122">In this section we look at how to use the Distcp utility.</span></span>

1. <span data-ttu-id="c2eed-123">Desde el escritorio, use SSH para conectarse al clúster.</span><span class="sxs-lookup"><span data-stu-id="c2eed-123">From your desktop, use SSH to connect to the cluster.</span></span> <span data-ttu-id="c2eed-124">Consulte [Conexión a un clúster de HDInsight basado en Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c2eed-124">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="c2eed-125">Ejecute los comandos desde el símbolo del sistema SSH.</span><span class="sxs-lookup"><span data-stu-id="c2eed-125">Run the commands from the SSH prompt.</span></span>

2. <span data-ttu-id="c2eed-126">Compruebe si puede tener acceso a los blobs de Almacenamiento de Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="c2eed-126">Verify whether you can access the Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="c2eed-127">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c2eed-127">Run the following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="c2eed-128">Esto debería proporcionar una lista de contenido en el blob de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2eed-128">This should provide a list of contents in the storage blob.</span></span>
3. <span data-ttu-id="c2eed-129">De forma similar, compruebe si puede tener acceso a la cuenta del Almacén de Data Lake desde el clúster.</span><span class="sxs-lookup"><span data-stu-id="c2eed-129">Similarly, verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="c2eed-130">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c2eed-130">Run the following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="c2eed-131">Esto debería proporcionar una lista de archivos o carpetas en la cuenta del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c2eed-131">This should provide a list of files/folders in the Data Lake Store account.</span></span>
4. <span data-ttu-id="c2eed-132">Utilice Distcp para copiar datos desde WASB a una cuenta de Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c2eed-132">Use Distcp to copy data from WASB to a Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="c2eed-133">Esto copiará el contenido de la carpeta **/example/data/gutenberg/** de WASB a **/myfolder** en la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c2eed-133">This will copy the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Store account.</span></span>
5. <span data-ttu-id="c2eed-134">Asimismo, utilice Distcp para copiar datos de la cuenta de la cuenta del Almacén de Data Lake a WASB.</span><span class="sxs-lookup"><span data-stu-id="c2eed-134">Similarly, use Distcp to copy data from Data Lake Store account to WASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="c2eed-135">Esto copiará el contenido de **/myfolder** de la cuenta de Data Lake Store en la carpeta **/example/data/gutenberg/** de WASB.</span><span class="sxs-lookup"><span data-stu-id="c2eed-135">This will copy the contents of **/myfolder** in the Data Lake Store account to **/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="c2eed-136">Consideraciones de rendimiento sobre el uso de DistCp</span><span class="sxs-lookup"><span data-stu-id="c2eed-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="c2eed-137">Dado que la granularidad más baja de DistCp es un único archivo, configurar el número máximo de copias simultáneas es el parámetro más importante para optimizar con respecto a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c2eed-137">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Store.</span></span> <span data-ttu-id="c2eed-138">Para controlar esto se establece el número de parámetros de asignador ("m ") en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="c2eed-138">This is controlled by setting the number of mappers (‘m’) parameter on the command line.</span></span> <span data-ttu-id="c2eed-139">Este parámetro especifica el número máximo de asignadores que se usará para copiar los datos.</span><span class="sxs-lookup"><span data-stu-id="c2eed-139">This parameter specifies the maximum number of mappers that will be used to copy data.</span></span> <span data-ttu-id="c2eed-140">El valor predeterminado es 20.</span><span class="sxs-lookup"><span data-stu-id="c2eed-140">Default value is 20.</span></span>

<span data-ttu-id="c2eed-141">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="c2eed-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a><span data-ttu-id="c2eed-142">¿Cómo se puede determinar el número de asignadores que se debe usar?</span><span class="sxs-lookup"><span data-stu-id="c2eed-142">How do I determine the number of mappers to use?</span></span>

<span data-ttu-id="c2eed-143">A continuación hay algunas instrucciones que puede usar.</span><span class="sxs-lookup"><span data-stu-id="c2eed-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="c2eed-144">**Paso 1: Determinación de la memoria total de YARN**: el primer paso consiste en determinar la memoria YARN disponible para el clúster donde se ejecuta el trabajo DistCp.</span><span class="sxs-lookup"><span data-stu-id="c2eed-144">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span></span> <span data-ttu-id="c2eed-145">Esta información está disponible en el portal de Ambari asociado con el clúster.</span><span class="sxs-lookup"><span data-stu-id="c2eed-145">This information is available in the Ambari portal associated with the cluster.</span></span> <span data-ttu-id="c2eed-146">Vaya a YARN y haga clic en la pestaña de configuración para ver la memoria YARN.</span><span class="sxs-lookup"><span data-stu-id="c2eed-146">Navigate to YARN and view the Configs tab to see the YARN memory.</span></span> <span data-ttu-id="c2eed-147">Para obtener la memoria de YARN total, multiplique la memoria de YARN por cada nodo por el número de nodos que tiene en el clúster.</span><span class="sxs-lookup"><span data-stu-id="c2eed-147">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="c2eed-148">**Paso 2: Cálculo del número de asignadores**: el valor de **m** es igual al cociente de la memoria de YARN total dividido por el tamaño del contenedor de YARN.</span><span class="sxs-lookup"><span data-stu-id="c2eed-148">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span></span> <span data-ttu-id="c2eed-149">La información del tamaño de contenedor de YARN está también disponible en el portal del Ambari.</span><span class="sxs-lookup"><span data-stu-id="c2eed-149">The YARN container size information is available in the Ambari portal as well.</span></span> <span data-ttu-id="c2eed-150">Vaya a YARN y examine la pestaña de configuración.</span><span class="sxs-lookup"><span data-stu-id="c2eed-150">Navigate to YARN and view the Configs tab.</span></span> <span data-ttu-id="c2eed-151">En esta ventana se muestra el tamaño del contenedor de YARN.</span><span class="sxs-lookup"><span data-stu-id="c2eed-151">The YARN container size is displayed in this window.</span></span> <span data-ttu-id="c2eed-152">La ecuación para llegar al número de asignadores (**m**) es</span><span class="sxs-lookup"><span data-stu-id="c2eed-152">The equation to arrive at the number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="c2eed-153">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="c2eed-153">**Example**</span></span>

<span data-ttu-id="c2eed-154">Supongamos que tiene 4 nodos D14v2s en el clúster y que intenta transferir 10 TB de datos desde 10 carpetas diferentes.</span><span class="sxs-lookup"><span data-stu-id="c2eed-154">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="c2eed-155">Cada una de las carpetas contiene diferentes cantidades de datos y los tamaños de archivo dentro de cada carpeta son diferentes.</span><span class="sxs-lookup"><span data-stu-id="c2eed-155">Each of the folders contain varying amounts of data and the file sizes within each folder are different.</span></span>

* <span data-ttu-id="c2eed-156">Memoria de YARN total: en el portal de Ambari determinará que la memoria de YARN es de 96 GB para un nodo D14.</span><span class="sxs-lookup"><span data-stu-id="c2eed-156">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="c2eed-157">Por lo tanto, la memoria de YARN total para el clúster de 4 nodos es:</span><span class="sxs-lookup"><span data-stu-id="c2eed-157">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="c2eed-158">Número de asignadores: en el portal de Ambari determinará que el tamaño del contenedor de YARN es 3072 para un nodo del clúster D14.</span><span class="sxs-lookup"><span data-stu-id="c2eed-158">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="c2eed-159">Por lo tanto, el número de asignadores es:</span><span class="sxs-lookup"><span data-stu-id="c2eed-159">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="c2eed-160">Si otras aplicaciones usan memoria, solo puede elegir usar una parte de la memoria de YARN del clúster para DistCp.</span><span class="sxs-lookup"><span data-stu-id="c2eed-160">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="c2eed-161">Copia de grandes conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="c2eed-161">Copying large datasets</span></span>

<span data-ttu-id="c2eed-162">Cuando el tamaño del conjunto de datos que se va a mover es muy grande (por ejemplo, >1 TB) o si tiene muchas carpetas diferentes, debe considerar el uso de varios trabajos de DistCp.</span><span class="sxs-lookup"><span data-stu-id="c2eed-162">When the size of the dataset to be moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="c2eed-163">Es probable que no haya ninguna mejora de rendimiento, pero se reparten los trabajos por lo que si se produce un error en cualquier trabajo, solo tendrá que reiniciar ese trabajo específico en lugar de todo el trabajo.</span><span class="sxs-lookup"><span data-stu-id="c2eed-163">There is likely no performance gain, but it will spread out the jobs so that if any job fails, you will only need to restart that specific job rather than the entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="c2eed-164">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="c2eed-164">Limitations</span></span>

* <span data-ttu-id="c2eed-165">DistCp intenta crear a asignadores que tengan un tamaño similar para optimizar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c2eed-165">DistCp tries to create mappers that are similar in size to optimize performance.</span></span> <span data-ttu-id="c2eed-166">El aumento del número de asignadores no siempre aumenta el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c2eed-166">Increasing the number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="c2eed-167">DistCp está limitado a solo un asignador por archivo.</span><span class="sxs-lookup"><span data-stu-id="c2eed-167">DistCp is limited to only one mapper per file.</span></span> <span data-ttu-id="c2eed-168">Por lo tanto, no debería tener más asignadores que archivos.</span><span class="sxs-lookup"><span data-stu-id="c2eed-168">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="c2eed-169">Como DistCp solo puede asignar a un asignador a un archivo, esto limita la cantidad de simultaneidad que puede usarse para copiar archivos de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="c2eed-169">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span></span>

* <span data-ttu-id="c2eed-170">Si tiene un número pequeño de archivos de gran tamaño, debe dividirlos en fragmentos de archivo de 256 MB para ofrecerle una mayor simultaneidad en potencia.</span><span class="sxs-lookup"><span data-stu-id="c2eed-170">If you have a small number of large files, then you should split them into 256MB file chunks to give you more potential concurrency.</span></span> 
 
* <span data-ttu-id="c2eed-171">Si va a copiar desde una cuenta de Azure Blob Storage, el trabajo de copia puede estar limitado por el lado del almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="c2eed-171">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span></span> <span data-ttu-id="c2eed-172">Como consecuencia, disminuirá el rendimiento de su trabajo de copia.</span><span class="sxs-lookup"><span data-stu-id="c2eed-172">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="c2eed-173">Para aprender sobre los límites de Azure Blob Storage, consulte la información al respecto en [Límites de suscripciones y servicios de Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="c2eed-173">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c2eed-174">Consulte también</span><span class="sxs-lookup"><span data-stu-id="c2eed-174">See also</span></span>
* [<span data-ttu-id="c2eed-175">Copiar datos de los blobs de almacenamiento de Azure en el Almacén Data Lake</span><span class="sxs-lookup"><span data-stu-id="c2eed-175">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="c2eed-176">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="c2eed-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="c2eed-177">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="c2eed-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="c2eed-178">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="c2eed-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
