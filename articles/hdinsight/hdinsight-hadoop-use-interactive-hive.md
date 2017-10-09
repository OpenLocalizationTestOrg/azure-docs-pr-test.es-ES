---
title: aaaUse interactivo de Hive en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse interactivo Hive (Hive en LLAP) en HDInsight."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="d5cc3-103">Uso de Interactive Hive en HDInsight (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="d5cc3-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="d5cc3-104">Interactive Hive (también conocido como</span><span class="sxs-lookup"><span data-stu-id="d5cc3-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="d5cc3-105">"[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP))" es un nuevo [tipo de clúster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="d5cc3-106">Interactive Hive permite el almacenamiento en caché en memoria, con lo que las consultas de Hive serán mucho más interactivas y rápidas.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="d5cc3-107">Esta nueva característica permite HDInsight uno de hello soluciones del mundo mayoría eficiente, flexibles y abiertas grandes cantidades de datos en la nube de hello con cachés en memoria (con Hive y Spark) y advanced analytics a través de la integración con R Services.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-107">This new feature makes HDInsight one of hello world’s most performant, flexible, and open Big Data solutions on hello cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="d5cc3-108">clúster de Hive interactivo de Hello es diferente del clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-108">hello Interactive Hive cluster is different from hello Hadoop cluster.</span></span> <span data-ttu-id="d5cc3-109">Solo contiene servicio de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-109">It only contains hello Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="d5cc3-110">MapReduce, Pig, Sqoop, Oozie y otros servicios se quitarán pronto de este tipo de clúster.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="d5cc3-111">Hola subárbol servicio en clúster de Hive interactivo de hello solo es accesible a través de hello vista del subárbol de Ambari, Beeline y Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-111">hello Hive service in hello Interactive Hive cluster is only accessible via hello Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="d5cc3-112">No se puede acceder mediante la consola de Hive, Templeton, la CLI de Azure y Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="d5cc3-113">Creación de un clúster de Interactive Hive</span><span class="sxs-lookup"><span data-stu-id="d5cc3-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="d5cc3-114">El clúster de Interactive Hive solo es compatible con los clústeres basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="d5cc3-115">Para obtener más información sobre cómo crear clústeres de HDInsight, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="d5cc3-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="d5cc3-116">Ejecución de Hive desde Interactive Hive</span><span class="sxs-lookup"><span data-stu-id="d5cc3-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="d5cc3-117">Hay diferentes opciones en lo que respecta a cómo ejecutar consultas de Hive:</span><span class="sxs-lookup"><span data-stu-id="d5cc3-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="d5cc3-118">Ejecutar Hive con hello Ambari Hive vista</span><span class="sxs-lookup"><span data-stu-id="d5cc3-118">Run Hive using hello Ambari Hive view</span></span>
  
    <span data-ttu-id="d5cc3-119">Para obtener información de hello acerca del uso de hello Hive vista, consulte [Hola Use vista Hive con Hadoop en HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="d5cc3-119">For hello information about using hello Hive View, see [Use hello Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="d5cc3-120">Ejecución de Hive mediante Beeline</span><span class="sxs-lookup"><span data-stu-id="d5cc3-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="d5cc3-121">Para obtener información sobre el uso de Beeline en HDInsight hello, consulte [uso de Hive con Hadoop en HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="d5cc3-121">For hello information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="d5cc3-122">Utilice Beeline desde el nodo principal de Hola o un nodo del borde vacío.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-122">You use Beeline from either hello headnode or an empty edge node.</span></span>  <span data-ttu-id="d5cc3-123">Se recomienda usar Beeline en un nodo perimetral vacío.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="d5cc3-124">Para obtener información sobre cómo crear un clúster de HDInsight con un nodo perimetral vacío, consulte [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) (Uso de nodos perimetrales vacíos en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="d5cc3-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="d5cc3-125">Ejecución de Hive mediante Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="d5cc3-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="d5cc3-126">Encontrará información sobre el uso de Hive ODBC hello [tooHadoop Excel conectarse con el controlador de Microsoft ODBC Hive hello](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="d5cc3-126">For hello information on using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="d5cc3-127">**Hola toofind cadena de conexión de JDBC:**</span><span class="sxs-lookup"><span data-stu-id="d5cc3-127">**toofind hello JDBC connection string:**</span></span>

1. <span data-ttu-id="d5cc3-128">Inicio de sesión tooAmbari con hello después de la dirección URL: https://<ClusterName>. AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-128">Sign on tooAmbari using hello following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="d5cc3-129">Haga clic en **Hive** desde el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-129">Click **Hive** from hello left menu.</span></span>
3. <span data-ttu-id="d5cc3-130">Haga clic en la dirección URL de hello resaltado icono toocopy Hola:</span><span class="sxs-lookup"><span data-stu-id="d5cc3-130">Click hello highlighted icon toocopy hello URL:</span></span>
   
   ![Cadena de conexión de JDBC para Interactive Hive con LLAP (Hadoop de HDInsight)](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="d5cc3-132">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d5cc3-132">See also</span></span>
* <span data-ttu-id="d5cc3-133">[Crear clústeres de Linux-based Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Obtenga información acerca de cómo los clústeres de toocreate interactivo de Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how toocreate Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="d5cc3-134">[Usar el subárbol con Hadoop en HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md): Obtenga información acerca de cómo las consultas de Hive de toouse Beeline toosubmit.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how toouse Beeline toosubmit Hive queries.</span></span>
* <span data-ttu-id="d5cc3-135">[Conectar Excel tooHadoop con hello Hive controlador ODBC de Microsoft](hdinsight-connect-excel-hive-odbc-driver.md): Obtenga información acerca de cómo tooconnect tooHive de Excel.</span><span class="sxs-lookup"><span data-stu-id="d5cc3-135">[Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how tooconnect Excel tooHive.</span></span>

