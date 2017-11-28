---
title: "versión más reciente del tooa de clúster HDInsight aaaUpgrade-Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooUpgrade HDInsight clúster tooa de versión más reciente."
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
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a><span data-ttu-id="1afc9-103">Actualizar la versión más reciente de tooa de clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1afc9-103">Upgrade HDInsight cluster tooa newer version</span></span>
<span data-ttu-id="1afc9-104">tootake aprovechar Hola características más recientes de HDInsight, se recomienda que los clústeres de HDInsight sea versión toolatest actualizado.</span><span class="sxs-lookup"><span data-stu-id="1afc9-104">tootake advantage of hello latest HDInsight features, we recommend that HDInsight clusters be upgraded toolatest version.</span></span> <span data-ttu-id="1afc9-105">Siga hello debajo directrices tooupgrade las versiones del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1afc9-105">Follow hello below guidelines tooupgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="1afc9-106">Los clústeres de HDInsight de las versiones 3.2 y 3.3 se están acercando a la fecha de retirada.</span><span class="sxs-lookup"><span data-stu-id="1afc9-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="1afc9-107">Para más información sobre las versiones admitidas de HDInsight, consulte [Versiones de los componentes de HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="1afc9-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="1afc9-108">Tareas de actualización</span><span class="sxs-lookup"><span data-stu-id="1afc9-108">Upgrade tasks</span></span>
<span data-ttu-id="1afc9-109">tooupgrade de flujo de trabajo de Hola clúster de HDInsight es como sigue.</span><span class="sxs-lookup"><span data-stu-id="1afc9-109">hello workflow tooupgrade HDInsight Cluster is as follows.</span></span>

![Diagrama de flujo de trabajo de actualización](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="1afc9-111">Leer cada sección de este documento toounderstand cambios que podrían ser necesarios cuando se actualiza el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1afc9-111">Read each section of this document toounderstand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="1afc9-112">Cree un clúster como entorno de control de calidad o de pruebas.</span><span class="sxs-lookup"><span data-stu-id="1afc9-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="1afc9-113">Para obtener más información acerca de cómo crear un clúster, consulte [Obtenga información acerca de cómo toocreate HDInsight basados en Linux clústeres](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="1afc9-113">For more information on creating a cluster, see [Learn how toocreate Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="1afc9-114">Copia receptores toohello nuevo entorno, orígenes de datos y trabajos existentes.</span><span class="sxs-lookup"><span data-stu-id="1afc9-114">Copy existing jobs, data sources, and sinks toohello new environment.</span></span> <span data-ttu-id="1afc9-115">Vea [copiar datos tooTest entorno](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="1afc9-115">See [Copy Data tooTest Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="1afc9-116">Realizar pruebas toomake seguro de que los trabajos funcionan según lo previsto en el nuevo clúster de Hola de validación.</span><span class="sxs-lookup"><span data-stu-id="1afc9-116">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>


<span data-ttu-id="1afc9-117">Una vez haya comprobado que todo funciona según lo esperado, programe el tiempo de inactividad para la migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="1afc9-117">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="1afc9-118">Durante este tiempo de inactividad, Hola acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="1afc9-118">During this downtime, do hello following actions:</span></span>

1.  <span data-ttu-id="1afc9-119">Realizar una copia de los datos transitorios almacenados localmente en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="1afc9-119">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="1afc9-120">Por ejemplo, si tiene datos que se almacenan directamente en un nodo principal.</span><span class="sxs-lookup"><span data-stu-id="1afc9-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="1afc9-121">Eliminar el clúster existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1afc9-121">Delete hello existing cluster.</span></span>
3.  <span data-ttu-id="1afc9-122">Crear un clúster de Hola misma red virtual subred con más reciente (o compatibles) HDI versión mediante Hola mismo almacén de datos predeterminada que Hola anterior clúster utilizado.</span><span class="sxs-lookup"><span data-stu-id="1afc9-122">Create a cluster in hello same VNET subnet with latest (or supported) HDI version using hello same default data store that hello previous cluster used.</span></span> <span data-ttu-id="1afc9-123">Esto permite Hola nuevo clúster toocontinue trabajan con los datos de producción existentes.</span><span class="sxs-lookup"><span data-stu-id="1afc9-123">This allows hello new cluster toocontinue working against your existing production data.</span></span>
4.  <span data-ttu-id="1afc9-124">Importe los datos transitorios cuya copia de seguridad realizó.</span><span class="sxs-lookup"><span data-stu-id="1afc9-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="1afc9-125">Iniciar trabajos/continuar procesando usando Hola nuevo clúster.</span><span class="sxs-lookup"><span data-stu-id="1afc9-125">Start jobs/continue processing using hello new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1afc9-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1afc9-126">Next Steps</span></span>
* [<span data-ttu-id="1afc9-127">Obtenga información acerca de cómo toocreate HDInsight basados en Linux clústeres</span><span class="sxs-lookup"><span data-stu-id="1afc9-127">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="1afc9-128">Conectar tooHDInsight mediante SSH</span><span class="sxs-lookup"><span data-stu-id="1afc9-128">Connect tooHDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="1afc9-129">Administración de un clúster basado en Linux mediante Ambari</span><span class="sxs-lookup"><span data-stu-id="1afc9-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

