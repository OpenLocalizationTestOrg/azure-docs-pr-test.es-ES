---
title: tutoriales de ciencia de datos aaaHDInsight Hadoop con Hive en Azure | Documentos de Microsoft
description: "Ejemplos de hello proceso de ciencia de datos de equipo que le guiarán a través del uso de Hola de Hive en análisis predictivos de toodo de Hadoop de HDInsight de Azure."
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
ms.openlocfilehash: 77efbe4ea6377f309987849d9f44e8b2b859ae9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="7a766-103">Tutoriales de ciencia de datos de HDInsight Hadoop con Hive en Azure</span><span class="sxs-lookup"><span data-stu-id="7a766-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="7a766-104">Estos tutoriales utiliza con un análisis predictivos de Hadoop de HDInsight clúster toodo Hive.</span><span class="sxs-lookup"><span data-stu-id="7a766-104">These walkthroughs use Hive with an HDInsight Hadoop cluster toodo predictive analytics.</span></span> <span data-ttu-id="7a766-105">Siguen pasos Hola descritos en hello proceso de ciencia de datos de equipo.</span><span class="sxs-lookup"><span data-stu-id="7a766-105">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="7a766-106">Para obtener información general de hello proceso de ciencia de datos de equipo, consulte [proceso de ciencia de datos](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7a766-106">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="7a766-107">Para una tooAzure Introducción HDInsight, vea [tooAzure Introducción HDInsight, Hola pila de tecnología de Hadoop y clústeres de Hadoop](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7a766-107">For an introduction tooAzure HDInsight, see [Introduction tooAzure HDInsight, hello Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="7a766-108">Tutoriales de ciencia de datos adicionales que se ejecutan Hola proceso de ciencia de datos de equipo se agrupan por hello **plataforma** que utilizan:</span><span class="sxs-lookup"><span data-stu-id="7a766-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="7a766-109">Predicción de propinas para taxis mediante Hive con HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="7a766-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="7a766-110">Hola [clústeres de Hadoop de HDInsight de uso](machine-learning-data-science-process-hive-walkthrough.md) tutorial usa datos de Nueva York taxis toopredict:</span><span class="sxs-lookup"><span data-stu-id="7a766-110">hello [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis toopredict:</span></span> 

- <span data-ttu-id="7a766-111">Si se da una propina</span><span class="sxs-lookup"><span data-stu-id="7a766-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="7a766-112">distribución de Hola de cantidades de sugerencia</span><span class="sxs-lookup"><span data-stu-id="7a766-112">hello distribution of tip amounts</span></span>

<span data-ttu-id="7a766-113">escenario de Hola se implementa mediante Hive con una [clúster de HDInsight Hadoop de Azure](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7a766-113">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="7a766-114">Obtenga información acerca de cómo explorar, toostore y datos de ingeniería de un recorrido de taxi NYC disponible públicamente de características y resultados son el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="7a766-114">You learn how toostore, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="7a766-115">También utilice toobuild de aprendizaje automático de Azure e implementar modelos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7a766-115">You also use Azure Machine Learning toobuild and deploy hello models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="7a766-116">Predicción de clics de anuncio mediante Hive con HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="7a766-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="7a766-117">Hola [usar clústeres de Hadoop de HDInsight de Azure en un conjunto de datos de 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md) tutorial utiliza disponible públicamente [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) haga clic en toopredict de conjunto de datos si una sugerencia se paga y Hola intervalo de cantidades se esperaba.</span><span class="sxs-lookup"><span data-stu-id="7a766-117">hello [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset toopredict whether a tip is paid and hello range of amounts expected.</span></span> <span data-ttu-id="7a766-118">escenario de Hola se implementa mediante Hive con una [clúster de HDInsight Hadoop de Azure](https://azure.microsoft.com/services/hdinsight/) toostore, explorar, ingeniero de características y el detalle de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7a766-118">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="7a766-119">Usa toobuild de aprendizaje automático de Azure, entrenar y puntuar un modelo de clasificación binaria predecir si un usuario hace clic en un anuncio.</span><span class="sxs-lookup"><span data-stu-id="7a766-119">It uses Azure Machine Learning toobuild, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="7a766-120">Tutorial de Hello concluye que muestra cómo toopublish uno de estos modelos como un servicio Web.</span><span class="sxs-lookup"><span data-stu-id="7a766-120">hello walkthrough concludes showing how toopublish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7a766-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7a766-121">Next steps</span></span>

<span data-ttu-id="7a766-122">Para obtener una explicación de los componentes clave de Hola que componen Hola proceso de ciencia de datos de equipo, consulte [información general del proceso de ciencia de datos de equipo](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7a766-122">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="7a766-123">Para obtener una descripción que se puede usar toostructure el ciclo de vida del proceso de ciencia de datos de equipo Hola de los proyectos de ciencia de datos, vea [ciclo de vida del proceso de ciencia de datos de equipo](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="7a766-123">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="7a766-124">ciclo de vida de Hello describe los pasos de hello, de toofinish de inicio, que los proyectos suelen seguir cuando se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="7a766-124">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 

