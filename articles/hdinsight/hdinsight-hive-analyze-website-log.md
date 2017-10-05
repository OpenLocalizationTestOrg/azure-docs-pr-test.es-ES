---
title: "Uso de Hive con Hadoop para el análisis de registros de sitios web: Azure HDInsight | Microsoft Docs"
description: "Vea cómo usar Hive con HDInsight para analizar registros de sitios web. Usará un archivo de registro como entrada en una tabla de HDInsight y HiveQL para consultar los datos."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: e1cdb786bb6049980aafc0213abf53013e342618
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-hive-with-windows-based-hdinsight-to-analyze-logs-from-websites"></a><span data-ttu-id="aa48c-104">Uso de Hive con HDInsight basado en Windows para analizar registros de sitios web</span><span class="sxs-lookup"><span data-stu-id="aa48c-104">Use Hive with Windows-based HDInsight to analyze logs from websites</span></span>
<span data-ttu-id="aa48c-105">Vea cómo usar HiveQL con HDInsight para analizar registros de un sitio web.</span><span class="sxs-lookup"><span data-stu-id="aa48c-105">Learn how to use HiveQL with HDInsight to analyze logs from a website.</span></span> <span data-ttu-id="aa48c-106">El análisis de registros de sitios web se puede usar para segmentar su público en función de actividades parecidas, clasificar los visitantes a los sitios por datos demográficos, descubrir el contenido que ven, los sitios web de los que proceden, etc.</span><span class="sxs-lookup"><span data-stu-id="aa48c-106">Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa48c-107">Los pasos de este tutorial solo se aplican a los clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="aa48c-107">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="aa48c-108">HDInsight solo está disponible en Windows en versiones inferiores a la 3.4.</span><span class="sxs-lookup"><span data-stu-id="aa48c-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="aa48c-109">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="aa48c-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aa48c-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="aa48c-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="aa48c-111">En este ejemplo, usará un clúster de HDInsight para analizar archivos de registro de sitios web a fin de conocer la frecuencia de las visitas al sitio web en un día desde sitios web externos en un día.</span><span class="sxs-lookup"><span data-stu-id="aa48c-111">In this sample, you will use an HDInsight cluster to analyze website log files to get insight into the frequency of visits to the website from external websites in a day.</span></span> <span data-ttu-id="aa48c-112">También generará un resumen de errores de sitios web que experimentan los usuarios.</span><span class="sxs-lookup"><span data-stu-id="aa48c-112">You'll also generate a summary of website errors that the users experience.</span></span> <span data-ttu-id="aa48c-113">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="aa48c-113">You will learn how to:</span></span>

* <span data-ttu-id="aa48c-114">Conectarse a un almacenamiento de blobs de Azure, que contiene archivos de registro de sitios web.</span><span class="sxs-lookup"><span data-stu-id="aa48c-114">Connect to a Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="aa48c-115">Crear tablas de HIVE para consultar esos registros.</span><span class="sxs-lookup"><span data-stu-id="aa48c-115">Create HIVE tables to query those logs.</span></span>
* <span data-ttu-id="aa48c-116">Crear consultas de HIVE para analizar los datos.</span><span class="sxs-lookup"><span data-stu-id="aa48c-116">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="aa48c-117">Usar Microsoft Excel para conectarse a HDInsight (usando conectividad abierta de base de datos, ODBC) para recuperar los datos analizados.</span><span class="sxs-lookup"><span data-stu-id="aa48c-117">Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="aa48c-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aa48c-119">Prerequisites</span></span>
* <span data-ttu-id="aa48c-120">Debe aprovisionar un clúster de Hadoop en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa48c-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="aa48c-121">Para obtener instrucciones, consulte [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="aa48c-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="aa48c-122">Debe tener instalado Microsoft Excel 2013 o Excel 2010.</span><span class="sxs-lookup"><span data-stu-id="aa48c-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="aa48c-123">Debe tener [Microsoft Hive ODBC Driver para](http://www.microsoft.com/download/details.aspx?id=40886) importar datos de Hive en Excel.</span><span class="sxs-lookup"><span data-stu-id="aa48c-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) to import data from Hive into Excel.</span></span>

## <a name="to-run-the-sample"></a><span data-ttu-id="aa48c-124">Para ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="aa48c-124">To run the sample</span></span>
1. <span data-ttu-id="aa48c-125">En el [Portal de Azure](https://portal.azure.com/), en el panel de inicio (si ancló el clúster allí), haga clic en el icono de clúster en el que quiera ejecutar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="aa48c-125">From the [Azure Portal](https://portal.azure.com/), from the Startboard (if you pinned the cluster there), click the cluster tile on which you want to run the sample.</span></span>
2. <span data-ttu-id="aa48c-126">En la hoja del clúster, en **Vínculos rápidos**, haga clic en el **panel del clúster** y luego, en la hoja **Panel de clúster**, haga clic en el **panel del clúster de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="aa48c-126">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="aa48c-127">También puede abrir directamente el panel con la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="aa48c-127">Alternatively, you can directly open the dashboard by using the following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="aa48c-128">Cuando se le pida, autentíquese con el nombre de usuario y la contraseña de administrador que usó cuando aprovisionó el clúster.</span><span class="sxs-lookup"><span data-stu-id="aa48c-128">When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.</span></span>
3. <span data-ttu-id="aa48c-129">En la página web que se abre, haga clic en la pestaña **Galería de introducción** y, a continuación, en la categoría **Soluciones con datos de ejemplo**, haga clic en el ejemplo **Análisis de registro del sitio web**.</span><span class="sxs-lookup"><span data-stu-id="aa48c-129">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="aa48c-130">Siga las instrucciones que se proporcionan en la página web para finalizar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="aa48c-130">Follow the instructions provided on the web page to finish the sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa48c-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aa48c-131">Next steps</span></span>
<span data-ttu-id="aa48c-132">Pruebe el siguiente ejemplo: [Análisis de datos de sensor usando Hive con HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="aa48c-132">Try the following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
