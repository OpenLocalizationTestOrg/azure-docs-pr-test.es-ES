---
title: "Actualización del clúster de HDInsight a una versión más reciente: Azure | Microsoft Docs"
description: "Sepa cómo actualizar el clúster de HDInsight a una versión más reciente."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: fa2e37bd922690322ccc3d8f68128180d013b701
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a><span data-ttu-id="d6d5c-103">Actualización del clúster de HDInsight a una versión más reciente</span><span class="sxs-lookup"><span data-stu-id="d6d5c-103">Upgrade HDInsight cluster to a newer version</span></span>
<span data-ttu-id="d6d5c-104">Para aprovechar las ventajas de las características más recientes de HDInsight, se recomienda que los clústeres de HDInsight se actualicen a la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span></span> <span data-ttu-id="d6d5c-105">Siga las directrices que aparecen a continuación para actualizar las versiones del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="d6d5c-106">Los clústeres de HDInsight de las versiones 3.2 y 3.3 se están acercando a la fecha de retirada.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="d6d5c-107">Para más información sobre las versiones admitidas de HDInsight, consulte [Versiones de los componentes de HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="d6d5c-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="d6d5c-108">Tareas de actualización</span><span class="sxs-lookup"><span data-stu-id="d6d5c-108">Upgrade tasks</span></span>
<span data-ttu-id="d6d5c-109">El flujo de trabajo para actualizar el clúster de HDInsight es el siguiente.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-109">The workflow to upgrade HDInsight Cluster is as follows.</span></span>

![Diagrama de flujo de trabajo de actualización](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="d6d5c-111">Lea cada sección de este documento para entender los cambios que pueden ser necesarios al actualizar el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-111">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="d6d5c-112">Cree un clúster como entorno de control de calidad o de pruebas.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="d6d5c-113">Para más información sobre cómo crear un clúster, consulte [Más información sobre cómo crear clústeres de HDInsight basados en Linux](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="d6d5c-113">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="d6d5c-114">Copie los trabajos, los orígenes de datos y los receptores existentes en el nuevo entorno.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-114">Copy existing jobs, data sources, and sinks to the new environment.</span></span> <span data-ttu-id="d6d5c-115">Consulte la sección [Copia de datos en el entorno de prueba](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) para más información.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-115">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="d6d5c-116">Realice pruebas de validación para asegurarse de que los trabajos funcionan como se esperaba en el nuevo clúster.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-116">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>


<span data-ttu-id="d6d5c-117">Cuando haya comprobado que todo funciona según lo esperado, programe el tiempo de inactividad para la migración.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-117">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="d6d5c-118">Durante este tiempo de inactividad, realice las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="d6d5c-118">During this downtime, do the following actions:</span></span>

1.  <span data-ttu-id="d6d5c-119">Haga copia de seguridad de todos los datos transitorios almacenados localmente en los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-119">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="d6d5c-120">Por ejemplo, si tiene datos que se almacenan directamente en un nodo principal.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="d6d5c-121">Elimine el clúster existente.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-121">Delete the existing cluster.</span></span>
3.  <span data-ttu-id="d6d5c-122">Cree un clúster en la misma subred de red virtual con la versión de HDI más reciente (o compatible) con el mismo almacén de datos predeterminado que usaba el clúster anterior.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-122">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span></span> <span data-ttu-id="d6d5c-123">Esto permitirá que el nuevo clúster siga trabajando con los datos de producción existentes.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-123">This allows the new cluster to continue working against your existing production data.</span></span>
4.  <span data-ttu-id="d6d5c-124">Importe los datos transitorios cuya copia de seguridad realizó.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="d6d5c-125">Inicie trabajos o continúe el procesamiento con el nuevo clúster.</span><span class="sxs-lookup"><span data-stu-id="d6d5c-125">Start jobs/continue processing using the new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6d5c-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6d5c-126">Next Steps</span></span>
* [<span data-ttu-id="d6d5c-127">Más información sobre cómo crear clústeres de HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="d6d5c-127">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="d6d5c-128">Conexión a HDInsight mediante SSH</span><span class="sxs-lookup"><span data-stu-id="d6d5c-128">Connect to HDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="d6d5c-129">Administración de un clúster basado en Linux mediante Ambari</span><span class="sxs-lookup"><span data-stu-id="d6d5c-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

