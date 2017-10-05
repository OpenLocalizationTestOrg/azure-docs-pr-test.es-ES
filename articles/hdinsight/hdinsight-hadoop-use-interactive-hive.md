---
title: Uso de Interactive Hive en HDInsight - Azure | Microsoft Docs
description: Aprenda a usar Interactive Hive (Hive en LLAP) en HDInsight.
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
ms.openlocfilehash: e7874b55fc72f14d8e2c801872359e823cb2ba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="0b0af-103">Uso de Interactive Hive en HDInsight (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="0b0af-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="0b0af-104">Interactive Hive (también conocido como</span><span class="sxs-lookup"><span data-stu-id="0b0af-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="0b0af-105">"[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP))" es un nuevo [tipo de clúster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0b0af-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="0b0af-106">Interactive Hive permite el almacenamiento en caché en memoria, con lo que las consultas de Hive serán mucho más interactivas y rápidas.</span><span class="sxs-lookup"><span data-stu-id="0b0af-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="0b0af-107">Esta nueva característica convierte HDInsight en una de las soluciones de macrodatos en la nube más abiertas, flexibles y eficaces del mercado con almacenamiento caché en memoria (con Hive y Spark) y análisis avanzados gracias a la integración con R Services.</span><span class="sxs-lookup"><span data-stu-id="0b0af-107">This new feature makes HDInsight one of the world’s most performant, flexible, and open Big Data solutions on the cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="0b0af-108">El clúster de Interactive Hive es diferente al de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0b0af-108">The Interactive Hive cluster is different from the Hadoop cluster.</span></span> <span data-ttu-id="0b0af-109">Solo contiene el servicio de Hive.</span><span class="sxs-lookup"><span data-stu-id="0b0af-109">It only contains the Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="0b0af-110">MapReduce, Pig, Sqoop, Oozie y otros servicios se quitarán pronto de este tipo de clúster.</span><span class="sxs-lookup"><span data-stu-id="0b0af-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="0b0af-111">Al servicio de Hive en el clúster de Interactive Hive solo puede accederse a través de la vista de Ambari Hive, Beeline y Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="0b0af-111">The Hive service in the Interactive Hive cluster is only accessible via the Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="0b0af-112">No se puede acceder mediante la consola de Hive, Templeton, la CLI de Azure y Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0b0af-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="0b0af-113">Creación de un clúster de Interactive Hive</span><span class="sxs-lookup"><span data-stu-id="0b0af-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="0b0af-114">El clúster de Interactive Hive solo es compatible con los clústeres basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="0b0af-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="0b0af-115">Para obtener más información sobre cómo crear clústeres de HDInsight, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0b0af-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="0b0af-116">Ejecución de Hive desde Interactive Hive</span><span class="sxs-lookup"><span data-stu-id="0b0af-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="0b0af-117">Hay diferentes opciones en lo que respecta a cómo ejecutar consultas de Hive:</span><span class="sxs-lookup"><span data-stu-id="0b0af-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="0b0af-118">Ejecución de Hive mediante la vista de Ambari Hive</span><span class="sxs-lookup"><span data-stu-id="0b0af-118">Run Hive using the Ambari Hive view</span></span>
  
    <span data-ttu-id="0b0af-119">Para ver la información sobre cómo usar la vista de Hive, consulte [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md) (Uso de la vista de Hive con Hadoop en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="0b0af-119">For the information about using the Hive View, see [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="0b0af-120">Ejecución de Hive mediante Beeline</span><span class="sxs-lookup"><span data-stu-id="0b0af-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="0b0af-121">Para obtener más información sobre cómo utilizar Beeline en HDInsight, consulte [Uso de Hive con Hadoop en HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="0b0af-121">For the information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="0b0af-122">Utilice Beeline en el nodo principal o en uno perimetral vacío.</span><span class="sxs-lookup"><span data-stu-id="0b0af-122">You use Beeline from either the headnode or an empty edge node.</span></span>  <span data-ttu-id="0b0af-123">Se recomienda usar Beeline en un nodo perimetral vacío.</span><span class="sxs-lookup"><span data-stu-id="0b0af-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="0b0af-124">Para obtener información sobre cómo crear un clúster de HDInsight con un nodo perimetral vacío, consulte [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) (Uso de nodos perimetrales vacíos en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="0b0af-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="0b0af-125">Ejecución de Hive mediante Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="0b0af-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="0b0af-126">Para obtener información sobre cómo usar Hive ODBC, consulte [Conexión de Excel a Hadoop con Microsoft Hive ODBC Driver](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="0b0af-126">For the information on using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="0b0af-127">**Para encontrar la cadena de conexión de JBDC, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="0b0af-127">**To find the JDBC connection string:**</span></span>

1. <span data-ttu-id="0b0af-128">Inicie sesión en Ambari con la siguiente dirección URL: https://<ClusterName>. AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="0b0af-128">Sign on to Ambari using the following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="0b0af-129">Haga clic en **Hive** en el menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="0b0af-129">Click **Hive** from the left menu.</span></span>
3. <span data-ttu-id="0b0af-130">Haga clic en el icono resaltado para copiar la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="0b0af-130">Click the highlighted icon to copy the URL:</span></span>
   
   ![Cadena de conexión de JDBC para Interactive Hive con LLAP (Hadoop de HDInsight)](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="0b0af-132">Consulte también</span><span class="sxs-lookup"><span data-stu-id="0b0af-132">See also</span></span>
* <span data-ttu-id="0b0af-133">[Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md): aprenda a crear clústeres de Interactive Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0b0af-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how to create Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="0b0af-134">[Uso de Hive con Hadoop en HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md): obtenga información sobre cómo usar Beeline para enviar consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="0b0af-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how to use Beeline to submit Hive queries.</span></span>
* <span data-ttu-id="0b0af-135">[Conexión de Excel a Hadoop con Microsoft Hive ODBC Driver](hdinsight-connect-excel-hive-odbc-driver.md): aprenda a conectar Excel con Hive.</span><span class="sxs-lookup"><span data-stu-id="0b0af-135">[Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how to connect Excel to Hive.</span></span>

