---
title: aaaUse Phoenix Apache & ardilla con HBase - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Phoenix Apache en HDInsight y cómo tooinstall y configurar ardilla en el clúster de estación de trabajo tooconnect tooan HBase en HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="cd64a-103">Uso de Apache Phoenix con clústeres de HBase basados en Linux en HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd64a-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="cd64a-104">Obtenga información acerca de cómo toouse [Apache Phoenix](http://phoenix.apache.org/) en HDInsight y cómo toouse SQLLine.</span><span class="sxs-lookup"><span data-stu-id="cd64a-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how toouse SQLLine.</span></span> <span data-ttu-id="cd64a-105">Para obtener más información acerca de Phoenix, consulte [Phoenix en 15 minutos o menos](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="cd64a-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="cd64a-106">Hola gramática de Phoenix, encontrará [gramática de Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="cd64a-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="cd64a-107">Para obtener información de versión de Phoenix en HDInsight de hello, consulte [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="cd64a-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="cd64a-108">Uso de SQLLine</span><span class="sxs-lookup"><span data-stu-id="cd64a-108">Use SQLLine</span></span>
<span data-ttu-id="cd64a-109">[SQLLine](http://sqlline.sourceforge.net/) es un tooexecute de utilidad de línea de comandos SQL.</span><span class="sxs-lookup"><span data-stu-id="cd64a-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cd64a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cd64a-110">Prerequisites</span></span>
<span data-ttu-id="cd64a-111">Para poder usar SQLLine, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="cd64a-111">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="cd64a-112">**Un clúster de HBase en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cd64a-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="cd64a-113">Para obtener información sobre el aprovisionamiento del clúster de HBase, consulte [Introducción a HBase Apache en HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="cd64a-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="cd64a-114">**Conectar el clúster de HBase toohello a través del protocolo de escritorio remoto de hello**.</span><span class="sxs-lookup"><span data-stu-id="cd64a-114">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="cd64a-115">Para obtener instrucciones, consulte [Hadoop administrar clústeres de HDInsight mediante el uso de Hola portal de Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="cd64a-115">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="cd64a-116">Cuando se conecta el clúster de HBase tooan, deberá tooconnect tooone de hello Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="cd64a-116">When you connect tooan HBase cluster, you need tooconnect tooone of hello Zookeepers.</span></span> <span data-ttu-id="cd64a-117">Cada clúster de HDInsight tiene tres Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="cd64a-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="cd64a-118">**toofind el nombre de host de hello Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="cd64a-118">**toofind out hello Zookeeper host name**</span></span>

1. <span data-ttu-id="cd64a-119">Abra Ambari examinando demasiado**https://<ClusterName>. azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="cd64a-119">Open Ambari by browsing too**https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="cd64a-120">Escriba hello toologin de nombre de usuario y contraseña HTTP (clúster).</span><span class="sxs-lookup"><span data-stu-id="cd64a-120">Enter hello HTTP (cluster) username and password toologin.</span></span>
3. <span data-ttu-id="cd64a-121">Haga clic en **ZooKeeper** desde el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="cd64a-121">Click **ZooKeeper** from hello left menu.</span></span> <span data-ttu-id="cd64a-122">Verá una lista con los tres **servidores de ZooKeeper**.</span><span class="sxs-lookup"><span data-stu-id="cd64a-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="cd64a-123">Haga clic en uno de hello **ZooKeeper Server** aparece.</span><span class="sxs-lookup"><span data-stu-id="cd64a-123">Click one of hello **ZooKeeper Server** listed.</span></span> <span data-ttu-id="cd64a-124">En el panel de resumen de hello, busque hello **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="cd64a-124">On hello Summary pane, find hello **Hostname**.</span></span> <span data-ttu-id="cd64a-125">Es similar demasiado*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="cd64a-125">It is similar too*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="cd64a-126">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="cd64a-126">**toouse SQLLine**</span></span>

1. <span data-ttu-id="cd64a-127">Conecte el clúster toohello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="cd64a-127">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="cd64a-128">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cd64a-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="cd64a-129">De SSH, ejecute hello después comandos toorun SQLLine:</span><span class="sxs-lookup"><span data-stu-id="cd64a-129">From SSH, run hello following commands toorun SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="cd64a-130">Ejecute hello después comandos toocreate una tabla HBase e insertar algunos datos:</span><span class="sxs-lookup"><span data-stu-id="cd64a-130">Run hello following commands toocreate a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="cd64a-131">Para más información, consulte el [manual de SQLLine](http://sqlline.sourceforge.net/#manual) y la [gramática de Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="cd64a-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd64a-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd64a-132">Next steps</span></span>
<span data-ttu-id="cd64a-133">En este artículo, ha aprendido cómo toouse Phoenix Apache en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd64a-133">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="cd64a-134">toolearn más información, vea:</span><span class="sxs-lookup"><span data-stu-id="cd64a-134">toolearn more, see:</span></span>

* <span data-ttu-id="cd64a-135">[Información general de HBase de HDInsight][hdinsight-hbase-overview]: HBase es una base de datos NoSQL de código abierto Apache basada en Hadoop que proporciona acceso aleatorio y una coherencia sólida para grandes cantidades de datos no estructurados y semiestructurados.</span><span class="sxs-lookup"><span data-stu-id="cd64a-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="cd64a-136">[Aprovisionar clústeres de HBase en red Virtual de Azure][hdinsight-hbase-provision-vnet]: con la integración de red virtual, clústeres de HBase pueden ser implementado toohello mismo virtual de red así como las aplicaciones que las aplicaciones pueden comunicarse con HBase directamente.</span><span class="sxs-lookup"><span data-stu-id="cd64a-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="cd64a-137">[Configurar la replicación de HBase en HDInsight](hdinsight-hbase-replication.md): Obtenga información acerca de cómo tooconfigure HBase replicación entre dos centros de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd64a-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="cd64a-138">[Analizar la opinión de Twitter con HBase en HDInsight][hbase-twitter-sentiment]: Obtenga información acerca de cómo toodo en tiempo real [análisis de opiniones](http://en.wikipedia.org/wiki/Sentiment_analysis) de grandes cantidades de datos mediante el uso de HBase en un clúster de Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd64a-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
