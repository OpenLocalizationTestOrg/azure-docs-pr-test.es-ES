---
title: "Análisis de datos de sensor usando Hive y Hadoop (Azure HDInsight) | Microsoft Docs"
description: Aprenda a analizar datos de sensor usando la Consola de consultas de Hive con HDInsight (Hadoop) y a visualizar los datos en Microsoft Excel con PowerView.
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
ms.openlocfilehash: 3abb71c12b4769bebd808276f8bdd832aad22d7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="1f740-103">Análisis de datos de sensor mediante la consola de consultas de Hive en Hadoop con HDInsight </span><span class="sxs-lookup"><span data-stu-id="1f740-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="1f740-104">Aprenda a analizar datos de sensor usando la consola de consultas de Hive con HDInsight (Hadoop) y a visualizar los datos en Microsoft Excel con Power View.</span><span class="sxs-lookup"><span data-stu-id="1f740-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f740-105">Los pasos de este tutorial solo se aplican a los clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="1f740-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1f740-106">HDInsight solo está disponible en Windows en versiones inferiores a la 3.4.</span><span class="sxs-lookup"><span data-stu-id="1f740-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="1f740-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="1f740-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1f740-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1f740-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="1f740-109">En esta muestra, usa Hive para procesar datos históricos e identificar problemas con sistemas de calefacción y aire acondicionado.</span><span class="sxs-lookup"><span data-stu-id="1f740-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="1f740-110">En concreto, se puedan identificar sistemas que no son capaces de mantener de forma confiable una temperatura fijada mediante la realización de las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="1f740-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span></span>

* <span data-ttu-id="1f740-111">Crear tablas de HIVE para consultar datos almacenados en archivos de valores separados por comas (CSV).</span><span class="sxs-lookup"><span data-stu-id="1f740-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="1f740-112">Crear consultas de HIVE para analizar los datos.</span><span class="sxs-lookup"><span data-stu-id="1f740-112">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="1f740-113">Para recuperar los datos analizados, use Microsoft Excel para conectarse a HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f740-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span></span>
* <span data-ttu-id="1f740-114">Para visualizar los datos, use Power View.</span><span class="sxs-lookup"><span data-stu-id="1f740-114">To visualize the data, use Power View.</span></span>

![Diagrama de la arquitectura de la solución](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="1f740-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1f740-116">Prerequisites</span></span>

* <span data-ttu-id="1f740-117">Un clúster de HDInsight (Hadoop): consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obtener información sobre la creación de un clúster.</span><span class="sxs-lookup"><span data-stu-id="1f740-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="1f740-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="1f740-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="1f740-119">Microsoft Excel se usa para la visualización de datos con [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="1f740-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="1f740-120">Microsoft Hive ODBC Driver</span><span class="sxs-lookup"><span data-stu-id="1f740-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a><span data-ttu-id="1f740-121">Para ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="1f740-121">To run the sample</span></span>

1. <span data-ttu-id="1f740-122">Desde el explorador web, navegue a la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="1f740-122">From your web browser, navigate to the following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="1f740-123">Reemplace `<clustername>` por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f740-123">Replace `<clustername>` with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="1f740-124">Cuando se le pida, autentíquese con el nombre de usuario y la contraseña de administrador que usó cuando aprovisionó este clúster.</span><span class="sxs-lookup"><span data-stu-id="1f740-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="1f740-125">En la página web que se abre, haga clic en la pestaña **Getting Started Gallery** (Galería de introducción) y, a continuación, en la categoría **Solutions with Sample Data** (Soluciones con datos de ejemplo), haga clic en el ejemplo **Análisis de datos del sensor**.</span><span class="sxs-lookup"><span data-stu-id="1f740-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span></span>

    ![Introducción a la galería de imágenes](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="1f740-127">Siga las instrucciones que se proporcionan en la página web para finalizar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1f740-127">Follow the instructions provided on the web page to finish the sample.</span></span>
