---
title: datos del sensor aaaAnalyze con Hive y Hadoop - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooanalyze datos de sensor mediante Hola consola de consultas de Hive con HDInsight (Hadoop), a continuación, visualizar los datos de hello en Microsoft Excel con PowerView."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="4f636-103">Analizar datos de sensor mediante Hola consola de consultas de Hive en Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f636-103">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="4f636-104">Obtenga información acerca de cómo tooanalyze datos de sensor mediante Hola consola de consultas de Hive con HDInsight (Hadoop), a continuación, visualizar datos de hello en Microsoft Excel mediante el uso de Power View.</span><span class="sxs-lookup"><span data-stu-id="4f636-104">Learn how tooanalyze sensor data by using hello Hive Query Console with HDInsight (Hadoop), then visualize hello data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f636-105">Hola pasos de este trabajo único documento con clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="4f636-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="4f636-106">HDInsight solo está disponible en Windows en versiones inferiores a la 3.4.</span><span class="sxs-lookup"><span data-stu-id="4f636-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="4f636-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="4f636-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4f636-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4f636-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="4f636-109">En este ejemplo, usa datos históricos de Hive tooprocess e identifica los problemas con los sistemas de calefacción y aire acondicionado.</span><span class="sxs-lookup"><span data-stu-id="4f636-109">In this sample, you use Hive tooprocess historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="4f636-110">En concreto, se puedan identificar sistemas se tooreliably no se puede mantener una temperatura de conjunto mediante la realización de hello siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="4f636-110">Specifically, you identify systems are not able tooreliably maintain a set temperature by performing hello following tasks:</span></span>

* <span data-ttu-id="4f636-111">Crear tablas de HIVE tooquery los datos almacenados en archivos de valores separados por comas (CSV).</span><span class="sxs-lookup"><span data-stu-id="4f636-111">Create HIVE tables tooquery data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="4f636-112">Crear consultas de HIVE tooanalyze datos de saludo.</span><span class="sxs-lookup"><span data-stu-id="4f636-112">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="4f636-113">datos de hello analizado de tooretrieve, usar Microsoft Excel tooconnect tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f636-113">tooretrieve hello analyzed data, use Microsoft Excel tooconnect tooHDInsight.</span></span>
* <span data-ttu-id="4f636-114">datos de hello toovisualize, use Power View.</span><span class="sxs-lookup"><span data-stu-id="4f636-114">toovisualize hello data, use Power View.</span></span>

![Un diagrama de arquitectura de la solución de Hola](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="4f636-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4f636-116">Prerequisites</span></span>

* <span data-ttu-id="4f636-117">Un clúster de HDInsight (Hadoop): consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obtener información sobre la creación de un clúster.</span><span class="sxs-lookup"><span data-stu-id="4f636-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="4f636-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="4f636-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="4f636-119">Microsoft Excel se usa para la visualización de datos con [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="4f636-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="4f636-120">Microsoft Hive ODBC Driver</span><span class="sxs-lookup"><span data-stu-id="4f636-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a><span data-ttu-id="4f636-121">ejemplo de Hola a toorun</span><span class="sxs-lookup"><span data-stu-id="4f636-121">toorun hello sample</span></span>

1. <span data-ttu-id="4f636-122">Desde el explorador web, desplácese toohello después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="4f636-122">From your web browser, navigate toohello following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="4f636-123">Reemplace `<clustername>` con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f636-123">Replace `<clustername>` with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="4f636-124">Cuando se le solicite, autenticar mediante nombre de usuario de administrador de Hola y la contraseña que usó al aprovisionar este clúster.</span><span class="sxs-lookup"><span data-stu-id="4f636-124">When prompted, authenticate by using hello administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="4f636-125">Desde Hola página web que se abre, haga clic en hello **la Galería de introducción** ficha y, a continuación, en hello **soluciones con datos de ejemplo** categoría, haga clic en hello **análisis de datos de Sensor** ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4f636-125">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Sensor Data Analysis** sample.</span></span>

    ![Introducción a la galería de imágenes](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="4f636-127">Siga las instrucciones de hello proporcionadas en el ejemplo de Hola Hola a toofinish página web.</span><span class="sxs-lookup"><span data-stu-id="4f636-127">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>
