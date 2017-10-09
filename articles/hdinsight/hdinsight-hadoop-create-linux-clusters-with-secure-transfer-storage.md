---
title: "clúster de Hadoop aaaCreate con cuentas de almacenamiento de transferencia segura de HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los clústeres de HDInsight de toocreate con transferencia segura habilita las cuentas de almacenamiento de Azure."
keywords: "introducción a hadoop,hadoop linux,inicio rápido de hadoop,transferencia segura,cuenta de almacenamiento de azure"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="b1a95-104">Creación de un clúster de Hadoop con cuentas de almacenamiento de transferencia segura en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1a95-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="b1a95-105">Hola [proteger la transferencia se necesitan](../storage/common/storage-require-secure-transfer.md) característica mejora la seguridad de saludo de la cuenta de almacenamiento de Azure mediante la aplicación de todas las solicitudes tooyour cuenta a través de una conexión segura.</span><span class="sxs-lookup"><span data-stu-id="b1a95-105">hello [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances hello security of your Azure Storage account by enforcing all requests tooyour account through a secure connection.</span></span> <span data-ttu-id="b1a95-106">Este esquema wasbs hello y la característica solo son compatibles con la versión de clúster de HDInsight 3,6 o versiones más reciente.</span><span class="sxs-lookup"><span data-stu-id="b1a95-106">This feature and hello wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b1a95-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b1a95-107">Prerequisites</span></span>
<span data-ttu-id="b1a95-108">Antes de empezar este tutorial, debe contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b1a95-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="b1a95-109">**Suscripción de Azure**: toocreate una cuenta de evaluación gratuita de un mes, examinar demasiado[azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="b1a95-109">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="b1a95-110">**Una cuenta de Azure Storage habilitada para transferencia segura**.</span><span class="sxs-lookup"><span data-stu-id="b1a95-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="b1a95-111">Para obtener instrucciones de hello, consulte [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) y [exigir la transferencia segura](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="b1a95-111">For hello instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="b1a95-112">**Un contenedor de blobs en la cuenta de almacenamiento de hello**.</span><span class="sxs-lookup"><span data-stu-id="b1a95-112">**A Blob container on hello storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="b1a95-113">Crear clúster</span><span class="sxs-lookup"><span data-stu-id="b1a95-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="b1a95-114">En esta sección, se crea un clúster de Hadoop en HDInsight mediante una [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b1a95-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="b1a95-115">plantilla de Hola se encuentra en [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="b1a95-115">hello template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="b1a95-116">No es necesario tener experiencia en el uso de la plantilla de Resource Manager para seguir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1a95-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="b1a95-117">Para otros métodos de creación del clúster y la comprensión de propiedades de hello usados en este tutorial, vea [HDInsight crear clústeres](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b1a95-117">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="b1a95-118">Haga clic en hello siguientes toosign de imagen en tooAzure y plantilla de administrador de recursos abiertos Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a95-118">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="b1a95-119">Sigue las instrucciones de hello toocreate clúster de hello con hello siguiendo las especificaciones:</span><span class="sxs-lookup"><span data-stu-id="b1a95-119">Follow hello instructions toocreate hello cluster with hello following specifications:</span></span> 

    - <span data-ttu-id="b1a95-120">Especifique la versión 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1a95-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="b1a95-121">versión predeterminada de Hello es 3.5.</span><span class="sxs-lookup"><span data-stu-id="b1a95-121">hello default version is 3.5.</span></span> <span data-ttu-id="b1a95-122">Se requiere la versión 3.6 o posterior.</span><span class="sxs-lookup"><span data-stu-id="b1a95-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="b1a95-123">Especifique una cuenta de almacenamiento habilitada para transferencia.</span><span class="sxs-lookup"><span data-stu-id="b1a95-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="b1a95-124">Utilice el nombre corto para la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1a95-124">Use short name for hello storage account.</span></span>
    - <span data-ttu-id="b1a95-125">Cuenta de almacenamiento de Hola y el contenedor de blobs de hello deben crearse con antelación.</span><span class="sxs-lookup"><span data-stu-id="b1a95-125">Both hello storage account and hello blob container must be created beforehand.</span></span> 

    <span data-ttu-id="b1a95-126">Para obtener instrucciones de hello, consulte [crear un clúster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="b1a95-126">For hello instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="b1a95-127">Si usas tooprovide de acción de secuencia de comandos en sus propios archivos de configuración, debe utilizar wasbs Hola después de configuración:</span><span class="sxs-lookup"><span data-stu-id="b1a95-127">If you use script action tooprovide your own configuration files, you must use wasbs in hello following settings:</span></span>

- <span data-ttu-id="b1a95-128">fs.defaultFS (sitio principal)</span><span class="sxs-lookup"><span data-stu-id="b1a95-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="b1a95-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="b1a95-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="b1a95-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="b1a95-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="b1a95-131">Adición de cuentas de almacenamiento adicionales</span><span class="sxs-lookup"><span data-stu-id="b1a95-131">Add additional storage accounts</span></span>

<span data-ttu-id="b1a95-132">Hay varias opciones tooadd transferencia segura adicional habilitada almacenamiento cuentas:</span><span class="sxs-lookup"><span data-stu-id="b1a95-132">There are several options tooadd additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="b1a95-133">Modificar plantilla de Azure Resource Manager hello en la última sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1a95-133">Modify hello Azure Resource Manager template in hello last section.</span></span>
- <span data-ttu-id="b1a95-134">Crear un clúster mediante hello [portal de Azure](https://portal.azure.com) y especifique la cuenta de almacenamiento vinculada.</span><span class="sxs-lookup"><span data-stu-id="b1a95-134">Create a cluster using hello [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="b1a95-135">Usar script acción tooadd adicional segura habilitado para transferencia de clúster de HDInsight existente de tooan de cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b1a95-135">Use script action tooadd additional secure transfer enabled storage accounts tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="b1a95-136">Para obtener más información, consulte [agregar almacenamiento adicional cuentas tooHDInsight](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b1a95-136">For more information, see [Add additional storage accounts tooHDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1a95-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b1a95-137">Next steps</span></span>
<span data-ttu-id="b1a95-138">En este tutorial, ha aprendido cómo toocreate un clúster de HDInsight y habilitar seguro de transferencia de las cuentas de almacenamiento de toohello.</span><span class="sxs-lookup"><span data-stu-id="b1a95-138">In this tutorial, you have learned how toocreate an HDInsight cluster, and enable secure transfer toohello storage accounts.</span></span>

<span data-ttu-id="b1a95-139">toolearn más información acerca de análisis de datos con HDInsight, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="b1a95-139">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="b1a95-140">toolearn más sobre el uso de Hive con HDInsight, incluido cómo las consultas tooperform Hive desde Visual Studio, vea [uso de Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="b1a95-140">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="b1a95-141">toolearn sobre Pig, datos tootransform de usar un idioma, vea [uso de Pig con HDInsight][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="b1a95-141">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="b1a95-142">toolearn sobre MapReduce, una manera toowrite los programas que procesan datos en Hadoop, vea [MapReduce de uso con HDInsight][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="b1a95-142">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="b1a95-143">toolearn sobre el uso de herramientas de HDInsight de Hola para los datos de Visual Studio tooanalyze en HDInsight, vea [Introducción al uso de Hadoop de Visual Studio tools para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b1a95-143">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="b1a95-144">más información acerca de cómo HDInsight almacena datos toolearn o datos tooget en HDInsight, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="b1a95-144">toolearn more about how HDInsight stores data or how tooget data into HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="b1a95-145">Para más información sobre cómo HDInsight usa Azure Storage, consulte [Uso de Azure Storage con HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b1a95-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="b1a95-146">Para obtener información acerca de cómo tooupload tooHDInsight de datos, vea [cargar datos tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="b1a95-146">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="b1a95-147">toolearn más información acerca de crear o administrar un clúster de HDInsight, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="b1a95-147">toolearn more about creating or managing an HDInsight cluster, see hello following articles:</span></span>

* <span data-ttu-id="b1a95-148">toolearn acerca de cómo administrar el clúster de HDInsight basados en Linux, consulte [HDInsight administrar clústeres con Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="b1a95-148">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="b1a95-149">toolearn más información acerca de las opciones de Hola que puede seleccionar al crear un clúster de HDInsight, vea [HDInsight crear en Linux con opciones personalizadas](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b1a95-149">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="b1a95-150">Si está familiarizado con Linux y Hadoop, pero desea tooknow detalles acerca de Hadoop en HDInsight de hello, consulte [trabajar con HDInsight en Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="b1a95-150">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="b1a95-151">Este artículo proporciona información como:</span><span class="sxs-lookup"><span data-stu-id="b1a95-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="b1a95-152">Direcciones URL para los servicios hospedados en clúster de hello, por ejemplo, Ambari y WebHCat</span><span class="sxs-lookup"><span data-stu-id="b1a95-152">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="b1a95-153">ubicación de Hola de ejemplos en el sistema de archivos local de Hola y archivos de Hadoop</span><span class="sxs-lookup"><span data-stu-id="b1a95-153">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="b1a95-154">uso de Hola de Azure Storage (WASB) en lugar de HDFS como almacén de datos predeterminado de Hola</span><span class="sxs-lookup"><span data-stu-id="b1a95-154">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


