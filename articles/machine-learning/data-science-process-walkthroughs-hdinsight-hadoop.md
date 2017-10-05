---
title: Tutoriales de ciencia de datos de HDInsight Hadoop con Hive en Azure | Microsoft Docs
description: "Ejemplos del proceso de ciencia de datos en equipo donde se examina el uso de Hive en Azure HDInsight Hadoop para la realización de análisis predictivo."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: fb06c3c1b1ae30d970a2e4d45a49e22e9d78b876
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="af3a5-103">Tutoriales de ciencia de datos de HDInsight Hadoop con Hive en Azure</span><span class="sxs-lookup"><span data-stu-id="af3a5-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="af3a5-104">En estos tutoriales se usa Hive con un clúster de HDInsight Hadoop para realizar análisis predictivo.</span><span class="sxs-lookup"><span data-stu-id="af3a5-104">These walkthroughs use Hive with an HDInsight Hadoop cluster to do predictive analytics.</span></span> <span data-ttu-id="af3a5-105">En ellos se siguen los pasos descritos en el proceso de ciencia de datos en equipo.</span><span class="sxs-lookup"><span data-stu-id="af3a5-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="af3a5-106">Para obtener información general sobre el proceso de ciencia de datos en equipo, consulte [Proceso de ciencia de datos](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af3a5-106">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="af3a5-107">Para ver una introducción a Azure HDInsight, consulte [Introducción a Azure HDInsight, la pila de tecnología de Hadoop y los clústeres de Hadoop](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="af3a5-107">For an introduction to Azure HDInsight, see [Introduction to Azure HDInsight, the Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="af3a5-108">Los otros tutoriales de ciencia de datos donde se ejecuta el proceso de ciencia de datos en equipo se agrupan por la **plataforma** que usan:</span><span class="sxs-lookup"><span data-stu-id="af3a5-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="af3a5-109">Predicción de propinas para taxis mediante Hive con HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="af3a5-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="af3a5-110">En el tutorial [Uso de clústeres de HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) se usan datos de taxis de New York para predecir:</span><span class="sxs-lookup"><span data-stu-id="af3a5-110">The [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis to predict:</span></span> 

- <span data-ttu-id="af3a5-111">Si se da una propina</span><span class="sxs-lookup"><span data-stu-id="af3a5-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="af3a5-112">La distribución de los importes de propina</span><span class="sxs-lookup"><span data-stu-id="af3a5-112">The distribution of tip amounts</span></span>

<span data-ttu-id="af3a5-113">El escenario se implementa mediante Hive con un [clúster de Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="af3a5-113">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="af3a5-114">Aprenderá a almacenar, explorar y realizar la ingeniería de características con un conjunto de datos de carreras y tarifas de taxis de Nueva York.</span><span class="sxs-lookup"><span data-stu-id="af3a5-114">You learn how to store, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="af3a5-115">También usará Azure Machine Learning para crear e implementar los modelos.</span><span class="sxs-lookup"><span data-stu-id="af3a5-115">You also use Azure Machine Learning to build and deploy the models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="af3a5-116">Predicción de clics de anuncio mediante Hive con HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="af3a5-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="af3a5-117">En el tutorial [Uso de un clúster de Hadoop de HDInsight de Azure en un conjunto de datos de 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md) se usa un conjunto de datos de clics de [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/), que está disponible públicamente, para predecir si se da una propina y el intervalo de importes esperado.</span><span class="sxs-lookup"><span data-stu-id="af3a5-117">The [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset to predict whether a tip is paid and the range of amounts expected.</span></span> <span data-ttu-id="af3a5-118">El escenario se implementa mediante Hive con un [clúster de Azure HDInsight Hadoop ](https://azure.microsoft.com/services/hdinsight/) para almacenar, explorar, realizar la ingeniería de características y reducir el tamaño de los datos.</span><span class="sxs-lookup"><span data-stu-id="af3a5-118">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="af3a5-119">Se emplea Azure Machine Learning para crear, entrenar y puntuar un modelo de clasificación binario que predice si un usuario hace clic en un anuncio.</span><span class="sxs-lookup"><span data-stu-id="af3a5-119">It uses Azure Machine Learning to build, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="af3a5-120">Para concluir el tutorial, se muestra cómo publicar uno de estos modelos como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="af3a5-120">The walkthrough concludes showing how to publish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="af3a5-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af3a5-121">Next steps</span></span>

<span data-ttu-id="af3a5-122">Para obtener una explicación de los componentes clave que conforman el proceso de ciencia de datos en equipo, consulte [Información general del proceso de ciencia de datos en equipo](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af3a5-122">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="af3a5-123">Para obtener una explicación del ciclo de vida del proceso de ciencia de datos en equipo que puede usar para estructurar los proyectos de ciencia de datos, consulte [Team Data Science Process lifecycle](data-science-process-lifecycle.md) (Ciclo de vida del proceso de ciencia de datos en equipo).</span><span class="sxs-lookup"><span data-stu-id="af3a5-123">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="af3a5-124">El ciclo de vida describe el proceso, de principio a fin, que suelen seguir los proyectos al ejecutarlos.</span><span class="sxs-lookup"><span data-stu-id="af3a5-124">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 

