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
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="f501b-104">Uso de Data Lake Store con clústeres de Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f501b-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="f501b-105">datos de tooanalyze de clúster de HDInsight, puede almacenar datos de Hola o en [el almacenamiento de Azure](../storage/common/storage-introduction.md), [almacén de Azure Data Lake](../data-lake-store/data-lake-store-overview.md), o ambos.</span><span class="sxs-lookup"><span data-stu-id="f501b-105">tooanalyze data in HDInsight cluster, you can store hello data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="f501b-106">Ambas opciones de almacenamiento le permiten eliminar toosafely clústeres de HDInsight que se usan para el cálculo sin perder los datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="f501b-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="f501b-107">En este artículo, aprenderá cómo funciona Data Lake Store con clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f501b-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="f501b-108">toolearn cómo funciona el almacenamiento de Azure con los clústeres de HDInsight, vea [Use el almacenamiento de Azure con HDInsight de Azure clústeres](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f501b-108">toolearn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="f501b-109">Consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obtener información sobre la creación de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f501b-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f501b-110">Para acceder a Azure Data Lake Store siempre se usa un canal seguro, así que no hay ningún nombre de esquema de sistema de archivos `adls`.</span><span class="sxs-lookup"><span data-stu-id="f501b-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="f501b-111">Usa siempre `adl`.</span><span class="sxs-lookup"><span data-stu-id="f501b-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="f501b-112">Disponibilidades para clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="f501b-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="f501b-113">Hadoop admite una noción de sistema de archivos predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="f501b-113">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="f501b-114">sistema de archivos predeterminado de Hello implica un esquema predeterminado y la entidad.</span><span class="sxs-lookup"><span data-stu-id="f501b-114">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="f501b-115">También puede ser tooresolve usa rutas de acceso relativas.</span><span class="sxs-lookup"><span data-stu-id="f501b-115">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="f501b-116">Durante el proceso de creación de clúster de HDInsight de hello, puede especificar un contenedor de blobs en almacenamiento de Azure como sistema de archivos predeterminado de Hola o con HDInsight 3.5 y versiones más recientes, puede seleccionar el almacenamiento de Azure o almacén de Azure Data Lake como sistema de archivos predeterminado de hello con un algunas excepciones.</span><span class="sxs-lookup"><span data-stu-id="f501b-116">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> 

<span data-ttu-id="f501b-117">Los clústeres de HDInsight pueden usar Data Lake Store de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="f501b-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="f501b-118">Como almacenamiento predeterminado de Hola</span><span class="sxs-lookup"><span data-stu-id="f501b-118">As hello default storage</span></span>
* <span data-ttu-id="f501b-119">Como almacenamiento adicional, con Azure Storage Blob como almacenamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f501b-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="f501b-120">A partir de ahora, solo algunas de ellas hello HDInsight clúster tipos/compatibles con las versiones con el almacén de Data Lake como almacenamiento predeterminado y cuentas de almacenamiento adicionales:</span><span class="sxs-lookup"><span data-stu-id="f501b-120">As of now, only some of hello HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="f501b-121">Tipo de clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="f501b-121">HDInsight cluster type</span></span> | <span data-ttu-id="f501b-122">Data Lake Store como almacenamiento predeterminado</span><span class="sxs-lookup"><span data-stu-id="f501b-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="f501b-123">Data Lake Store como almacenamiento adicional</span><span class="sxs-lookup"><span data-stu-id="f501b-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="f501b-124">Notas</span><span class="sxs-lookup"><span data-stu-id="f501b-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="f501b-125">HDInsight versión 3.6</span><span class="sxs-lookup"><span data-stu-id="f501b-125">HDInsight version 3.6</span></span> | <span data-ttu-id="f501b-126">Sí</span><span class="sxs-lookup"><span data-stu-id="f501b-126">Yes</span></span> | <span data-ttu-id="f501b-127">Sí</span><span class="sxs-lookup"><span data-stu-id="f501b-127">Yes</span></span> | |
| <span data-ttu-id="f501b-128">Versión de HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="f501b-128">HDInsight version 3.5</span></span> | <span data-ttu-id="f501b-129">Sí</span><span class="sxs-lookup"><span data-stu-id="f501b-129">Yes</span></span> | <span data-ttu-id="f501b-130">Sí</span><span class="sxs-lookup"><span data-stu-id="f501b-130">Yes</span></span> | <span data-ttu-id="f501b-131">Con excepción de Hola de HBase</span><span class="sxs-lookup"><span data-stu-id="f501b-131">With hello exception of HBase</span></span>|
| <span data-ttu-id="f501b-132">Versión de HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="f501b-132">HDInsight version 3.4</span></span> | <span data-ttu-id="f501b-133">No</span><span class="sxs-lookup"><span data-stu-id="f501b-133">No</span></span> | <span data-ttu-id="f501b-134">Sí</span><span class="sxs-lookup"><span data-stu-id="f501b-134">Yes</span></span> | |
| <span data-ttu-id="f501b-135">HDInsight versión 3.3</span><span class="sxs-lookup"><span data-stu-id="f501b-135">HDInsight version 3.3</span></span> | <span data-ttu-id="f501b-136">No</span><span class="sxs-lookup"><span data-stu-id="f501b-136">No</span></span> | <span data-ttu-id="f501b-137">No</span><span class="sxs-lookup"><span data-stu-id="f501b-137">No</span></span> | |
| <span data-ttu-id="f501b-138">HDInsight versión 3.2</span><span class="sxs-lookup"><span data-stu-id="f501b-138">HDInsight version 3.2</span></span> | <span data-ttu-id="f501b-139">No</span><span class="sxs-lookup"><span data-stu-id="f501b-139">No</span></span> | <span data-ttu-id="f501b-140">Sí</span><span class="sxs-lookup"><span data-stu-id="f501b-140">Yes</span></span> | |
| <span data-ttu-id="f501b-141">HDInsight Premium (nivel)</span><span class="sxs-lookup"><span data-stu-id="f501b-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="f501b-142">No</span><span class="sxs-lookup"><span data-stu-id="f501b-142">No</span></span> | <span data-ttu-id="f501b-143">No</span><span class="sxs-lookup"><span data-stu-id="f501b-143">No</span></span> | |
| <span data-ttu-id="f501b-144">Storm</span><span class="sxs-lookup"><span data-stu-id="f501b-144">Storm</span></span> | | |<span data-ttu-id="f501b-145">Puede usar datos de almacén de Data Lake toowrite de una topología de Storm.</span><span class="sxs-lookup"><span data-stu-id="f501b-145">You can use Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="f501b-146">Puede usar Data Lake Store para datos de referencia que luego puede leer una topología de Storm.</span><span class="sxs-lookup"><span data-stu-id="f501b-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="f501b-147">Usar almacén de Data Lake como una cuenta de almacenamiento adicional no afecten al rendimiento o tooread de capacidad de Hola o escribir tooAzure almacenamiento en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="f501b-147">Using Data Lake Store as an additional storage account does not affect performance or hello ability tooread or write tooAzure storage from hello cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="f501b-148">Uso de Data Lake Store como almacenamiento predeterminado</span><span class="sxs-lookup"><span data-stu-id="f501b-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="f501b-149">Cuando HDInsight se implementa con el almacén de Data Lake como almacenamiento de forma predeterminada, los archivos relacionados con el clúster de Hola se almacenan en el almacén de Data Lake en hello ubicación siguiente:</span><span class="sxs-lookup"><span data-stu-id="f501b-149">When HDInsight is deployed with Data Lake Store as default storage, hello cluster-related files are stored in Data Lake Store in hello following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="f501b-150">donde `<cluster_root_path>` es el nombre de Hola de una carpeta se crea en el almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f501b-150">where `<cluster_root_path>` is hello name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="f501b-151">Al especificar una ruta de acceso raíz para cada clúster, puede usar Hola la misma cuenta de almacén de Data Lake para más de un clúster.</span><span class="sxs-lookup"><span data-stu-id="f501b-151">By specifying a root path for each cluster, you can use hello same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="f501b-152">Por lo tanto, puede tener una configuración donde:</span><span class="sxs-lookup"><span data-stu-id="f501b-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="f501b-153">Cluster1 puede usar la ruta de acceso de Hola`adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="f501b-153">Cluster1 can use hello path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="f501b-154">Usar ruta de acceso de hello Cluster2`adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="f501b-154">Cluster2 can use hello path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="f501b-155">Observe que ambos Hola de uso de clústeres Hola misma cuenta de almacén de Data Lake **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="f501b-155">Notice that both hello clusters use hello same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="f501b-156">Cada clúster tiene acceso tooits posee filesystem raíz en el almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f501b-156">Each cluster has access tooits own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="f501b-157">Hola experiencia de implementación de portal de Azure en particular le pide que toouse un nombre de carpeta como **/clusters/\<clustername >** para la ruta de acceso de hello raíz.</span><span class="sxs-lookup"><span data-stu-id="f501b-157">hello Azure portal deployment experience in particular prompts you toouse a folder name such as **/clusters/\<clustername>** for hello root path.</span></span>

<span data-ttu-id="f501b-158">toouse toobe capaz de un almacén de Data Lake como almacenamiento predeterminado, debe conceder toohello de acceso principal de servicio de hello siguiendo las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="f501b-158">toobe able toouse a Data Lake Store as default storage, you must grant hello service principal access toohello following paths:</span></span>

- <span data-ttu-id="f501b-159">raíz de cuenta de almacén de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="f501b-159">hello Data Lake Store account root.</span></span>  <span data-ttu-id="f501b-160">Por ejemplo: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="f501b-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="f501b-161">carpeta de Hola para todas las carpetas de clúster.</span><span class="sxs-lookup"><span data-stu-id="f501b-161">hello folder for all cluster folders.</span></span>  <span data-ttu-id="f501b-162">Por ejemplo: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="f501b-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="f501b-163">carpeta de Hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="f501b-163">hello folder for hello cluster.</span></span>  <span data-ttu-id="f501b-164">Por ejemplo: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="f501b-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="f501b-165">Para más información sobre cómo crear la entidad de servicio y concederle acceso, consulte [Configuración del acceso a Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="f501b-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="f501b-166">Uso de Data Lake Store como almacenamiento adicional</span><span class="sxs-lookup"><span data-stu-id="f501b-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="f501b-167">Puede usar almacén de Data Lake como almacenamiento adicional para clúster de hello así.</span><span class="sxs-lookup"><span data-stu-id="f501b-167">You can use Data Lake Store as additional storage for hello cluster as well.</span></span> <span data-ttu-id="f501b-168">En tales casos, almacenamiento de hello clúster predeterminado puede ser un Blob de almacenamiento de Azure o una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f501b-168">In such cases, hello cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="f501b-169">Si se ejecutan trabajos de HDInsight con datos de hello almacenados en el almacén de Data Lake como almacenamiento adicional, debe usar archivos de toohello de ruta de acceso completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="f501b-169">If you are running HDInsight jobs against hello data stored in Data Lake Store as additional storage, you must use hello fully-qualified path toohello files.</span></span> <span data-ttu-id="f501b-170">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f501b-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="f501b-171">Tenga en cuenta que no hay ningún **cluster_root_path** en dirección URL de hello ahora.</span><span class="sxs-lookup"><span data-stu-id="f501b-171">Note that there's no **cluster_root_path** in hello URL now.</span></span> <span data-ttu-id="f501b-172">Eso es porque el almacén de Data Lake un almacenamiento predeterminado en este caso no es por lo que todo lo que necesita toodo es proporcionar a los archivos de toohello de ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="f501b-172">That's because Data Lake Store is not a default storage in this case so all you need toodo is provide hello path toohello files.</span></span>

<span data-ttu-id="f501b-173">toouse toobe capaz de un almacén de Data Lake como almacenamiento adicional, solo necesita toogrant Hola servicio principal toohello las rutas de acceso donde se almacenan los archivos.</span><span class="sxs-lookup"><span data-stu-id="f501b-173">toobe able toouse a Data Lake Store as additional storage, you only need toogrant hello service principal access toohello paths where your files are stored.</span></span>  <span data-ttu-id="f501b-174">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f501b-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="f501b-175">Para más información sobre cómo crear la entidad de servicio y concederle acceso, consulte [Configuración del acceso a Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="f501b-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="f501b-176">Uso de más de una cuenta de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f501b-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="f501b-177">Agregar una cuenta de almacén de Data Lake como adicionales y agregar más de un almacén de Data Lake cuentas se llevan a cabo por da permiso al clúster HDInsight hello en los datos en una o más cuentas de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f501b-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving hello HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="f501b-178">Consulte [Configuración del acceso a Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="f501b-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="f501b-179">Configuración del acceso a Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f501b-179">Configure Data Lake store access</span></span>

<span data-ttu-id="f501b-180">tooconfigure acceso al almacén de Data Lake desde el clúster de HDInsight, debe tener una entidad de servicio de Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f501b-180">tooconfigure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="f501b-181">Solo un administrador de Azure AD puede crear una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="f501b-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="f501b-182">entidad de servicio de Hello debe crearse con un certificado.</span><span class="sxs-lookup"><span data-stu-id="f501b-182">hello service principal must be created with a certificate.</span></span> <span data-ttu-id="f501b-183">Para más información, consulte [Configuración del acceso a Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) y [Creación de una entidad de servicio con un certificado autofirmado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="f501b-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="f501b-184">Si va a almacén de toouse Azure Data Lake como almacenamiento adicional para el clúster de HDInsight, se recomienda hacer esto al crear el clúster de hello tal como se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="f501b-184">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="f501b-185">Agregar almacén de Azure Data Lake como almacenamiento adicional tooan clúster de HDInsight existente es un proceso complicado y propensa a tooerrors.</span><span class="sxs-lookup"><span data-stu-id="f501b-185">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

## <a name="access-files-from-hello-cluster"></a><span data-ttu-id="f501b-186">Acceder a los archivos del clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="f501b-186">Access files from hello cluster</span></span>

<span data-ttu-id="f501b-187">Hay varias maneras se pueden acceder a archivos de hello en el almacén de Data Lake desde un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f501b-187">There are several ways you can access hello files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="f501b-188">**Con el nombre completo de hello**.</span><span class="sxs-lookup"><span data-stu-id="f501b-188">**Using hello fully qualified name**.</span></span> <span data-ttu-id="f501b-189">Con este enfoque, se proporcionan archivos de toohello de ruta de acceso completa de Hola que desea tooaccess.</span><span class="sxs-lookup"><span data-stu-id="f501b-189">With this approach, you provide hello full path toohello file that you want tooaccess.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="f501b-190">**Con formato de ruta de acceso abreviada hello**.</span><span class="sxs-lookup"><span data-stu-id="f501b-190">**Using hello shortened path format**.</span></span> <span data-ttu-id="f501b-191">Con este enfoque, reemplace la ruta de acceso de Hola de raíz de clúster toohello con adl: / / /.</span><span class="sxs-lookup"><span data-stu-id="f501b-191">With this approach, you replace hello path up toohello cluster root with adl:///.</span></span> <span data-ttu-id="f501b-192">Por lo tanto, en el ejemplo de Hola anterior, puede reemplazar `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` con `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="f501b-192">So, in hello example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="f501b-193">**Usar ruta de acceso relativa de hello**.</span><span class="sxs-lookup"><span data-stu-id="f501b-193">**Using hello relative path**.</span></span> <span data-ttu-id="f501b-194">Con este enfoque, sólo se proporcionan archivos de toohello de ruta de acceso relativa de Hola que desea tooaccess.</span><span class="sxs-lookup"><span data-stu-id="f501b-194">With this approach, you only provide hello relative path toohello file that you want tooaccess.</span></span> <span data-ttu-id="f501b-195">Por ejemplo, si hello archivo toohello de ruta de acceso completa es:</span><span class="sxs-lookup"><span data-stu-id="f501b-195">For example, if hello complete path toohello file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="f501b-196">Puede tener acceso a Hola mismo archivo sample.log mediante esta ruta de acceso relativa en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f501b-196">You can access hello same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a><span data-ttu-id="f501b-197">Crear clústeres de HDInsight con acceso a almacén de tooData Lake</span><span class="sxs-lookup"><span data-stu-id="f501b-197">Create HDInsight clusters with access tooData Lake Store</span></span>

<span data-ttu-id="f501b-198">Usar hello siguientes vínculos para obtener instrucciones detalladas en forma de toocreate clústeres de HDInsight con acceso a tooData Lake almacén.</span><span class="sxs-lookup"><span data-stu-id="f501b-198">Use hello following links for detailed instructions on how toocreate HDInsight clusters with access tooData Lake Store.</span></span>

* [<span data-ttu-id="f501b-199">Uso del Portal</span><span class="sxs-lookup"><span data-stu-id="f501b-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="f501b-200">Uso de PowerShell (con Data Lake Store como almacenamiento predeterminado)</span><span class="sxs-lookup"><span data-stu-id="f501b-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="f501b-201">Uso de PowerShell (con Data Lake Store como almacenamiento adicional)</span><span class="sxs-lookup"><span data-stu-id="f501b-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="f501b-202">Uso de plantillas de Azure</span><span class="sxs-lookup"><span data-stu-id="f501b-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="f501b-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f501b-203">Next steps</span></span>
<span data-ttu-id="f501b-204">En este artículo, se habrá aprendido cómo toouse almacén de Data Lake HDFS compatible con Azure con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f501b-204">In this article, you learned how toouse HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="f501b-205">Esto le permite toobuild escalable y a largo plazo, archivado soluciones de adquisición de datos y usar información de hello toounlock de HDInsight dentro de hello almacenado estructurado y datos no estructurados.</span><span class="sxs-lookup"><span data-stu-id="f501b-205">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="f501b-206">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="f501b-206">For more information, see:</span></span>

* <span data-ttu-id="f501b-207">[Introducción a Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="f501b-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="f501b-208">Introducción Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f501b-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="f501b-209">[Cargar datos tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="f501b-209">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="f501b-210">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f501b-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="f501b-211">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="f501b-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="f501b-212">[Usar firmas de acceso compartido de almacenamiento de Azure toorestrict acceso toodata con HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="f501b-212">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
