---
title: "aaaUse Hive con Hadoop para análisis de registros de sitio Web - HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se registra toouse Hive con el sitio Web de tooanalyze de HDInsight. Podrá utilizar un archivo de registro como entrada en una tabla de HDInsight y usar datos de HiveQL tooquery Hola."
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
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a><span data-ttu-id="ee0ce-104">Usar el subárbol con registros de tooanalyze de HDInsight basados en Windows de sitios Web</span><span class="sxs-lookup"><span data-stu-id="ee0ce-104">Use Hive with Windows-based HDInsight tooanalyze logs from websites</span></span>
<span data-ttu-id="ee0ce-105">Obtenga información acerca de cómo se registra toouse HiveQL con HDInsight tooanalyze desde un sitio Web.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-105">Learn how toouse HiveQL with HDInsight tooanalyze logs from a website.</span></span> <span data-ttu-id="ee0ce-106">Análisis de registro del sitio Web que pueden ser utilizado toosegment la audiencia basada en actividades similares, clasificar los visitantes del sitio por datos demográficos y toofind contenido Hola vean, los sitios Web de hello provienen de y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-106">Website log analysis can be used toosegment your audience based on similar activities, categorize site visitors by demographics, and toofind out hello content they view, hello websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee0ce-107">Hola pasos de este trabajo único documento con clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-107">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="ee0ce-108">HDInsight solo está disponible en Windows en versiones inferiores a la 3.4.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="ee0ce-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ee0ce-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ee0ce-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="ee0ce-111">En este ejemplo, usará una HDInsight clúster tooanalyze sitio Web registro archivos tooget una visión general de frecuencia de Hola de toohello visita el sitio Web de sitios Web externos en un día.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-111">In this sample, you will use an HDInsight cluster tooanalyze website log files tooget insight into hello frequency of visits toohello website from external websites in a day.</span></span> <span data-ttu-id="ee0ce-112">También generará un resumen de errores de sitio Web que los usuarios de hello experimentar.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-112">You'll also generate a summary of website errors that hello users experience.</span></span> <span data-ttu-id="ee0ce-113">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="ee0ce-113">You will learn how to:</span></span>

* <span data-ttu-id="ee0ce-114">Conectar tooa almacenamiento de blobs de Azure, que contiene los archivos de registro del sitio Web.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-114">Connect tooa Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="ee0ce-115">Crear tablas de HIVE tooquery esos registros.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-115">Create HIVE tables tooquery those logs.</span></span>
* <span data-ttu-id="ee0ce-116">Crear consultas de HIVE tooanalyze datos de saludo.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-116">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="ee0ce-117">Usar Microsoft Excel tooconnect tooHDInsight (mediante datos de abrir base de datos ODBC (conectividad) tooretrieve Hola analizado.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-117">Use Microsoft Excel tooconnect tooHDInsight (by using open database connectivity (ODBC) tooretrieve hello analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="ee0ce-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ee0ce-119">Prerequisites</span></span>
* <span data-ttu-id="ee0ce-120">Debe aprovisionar un clúster de Hadoop en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="ee0ce-121">Para obtener instrucciones, consulte [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="ee0ce-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="ee0ce-122">Debe tener instalado Microsoft Excel 2013 o Excel 2010.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="ee0ce-123">Debe tener [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport datos de Hive en Excel.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport data from Hive into Excel.</span></span>

## <a name="toorun-hello-sample"></a><span data-ttu-id="ee0ce-124">ejemplo de Hola a toorun</span><span class="sxs-lookup"><span data-stu-id="ee0ce-124">toorun hello sample</span></span>
1. <span data-ttu-id="ee0ce-125">De hello [Portal de Azure](https://portal.azure.com/), de hello panel de inicio (si está anclado clúster de hello no existe), haga clic en el icono de clúster de Hola que servirá de ejemplo de Hola a toorun.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-125">From hello [Azure Portal](https://portal.azure.com/), from hello Startboard (if you pinned hello cluster there), click hello cluster tile on which you want toorun hello sample.</span></span>
2. <span data-ttu-id="ee0ce-126">De hello clúster hoja, en **vínculos rápidos**, haga clic en **panel clúster**y, a continuación, desde hello **panel clúster** hoja, haga clic en **clúster de HDInsight Panel**.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-126">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from hello **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="ee0ce-127">Como alternativa, puede abrir directamente panel hello mediante Hola después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="ee0ce-127">Alternatively, you can directly open hello dashboard by using hello following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="ee0ce-128">Cuando se le solicite, autenticar mediante nombre de usuario de administrador de Hola y la contraseña que usó al aprovisionar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-128">When prompted, authenticate by using hello administrator user name and password you used when provisioning hello cluster.</span></span>
3. <span data-ttu-id="ee0ce-129">Desde Hola página web que se abre, haga clic en hello **Galería de introducción** ficha y, a continuación, en hello **soluciones con datos de ejemplo** categoría, haga clic en hello **análisis de registro del sitio Web** ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-129">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="ee0ce-130">Siga las instrucciones de hello proporcionadas en el ejemplo de Hola Hola a toofinish página web.</span><span class="sxs-lookup"><span data-stu-id="ee0ce-130">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee0ce-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee0ce-131">Next steps</span></span>
<span data-ttu-id="ee0ce-132">Intente Hola según muestra: [analizar datos de sensor con Hive con HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="ee0ce-132">Try hello following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
