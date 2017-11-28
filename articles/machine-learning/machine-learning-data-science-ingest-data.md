---
title: "datos de aaaLoad en entornos de almacenamiento de Azure para realizar análisis | Documentos de Microsoft"
description: Mover datos tooand desde el almacenamiento de blobs de Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="df559-103">Carga de datos en entornos de almacenamiento para el análisis</span><span class="sxs-lookup"><span data-stu-id="df559-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="df559-104">Hola proceso de ciencia de datos de equipo requiere que los datos estén ingestión o cargados en una serie de almacenamiento diferentes entornos toobe procesada o analizar de manera más adecuada de hello en cada fase del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="df559-104">hello Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments toobe processed or analyzed in hello most appropriate way in each stage of hello process.</span></span> <span data-ttu-id="df559-105">Entre los destinos de datos más usados para el procesamiento se incluyen el almacenamiento de blobs de Azure, las bases de datos SQL Azure, SQL Server en VM de Azure, HDInsight (Hadoop) y Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="df559-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="df559-106">Esto **menú** vincula tootopics que describen cómo tooingest datos en estos entornos donde se almacenan los datos de Hola y cómo se procesan como destino.</span><span class="sxs-lookup"><span data-stu-id="df559-106">This **menu** links tootopics that describe how tooingest data into these target environments where hello data is stored and processed.</span></span>

<span data-ttu-id="df559-107">Technical y necesidades empresariales, así como la ubicación inicial de hello, dar formato y tamaño de los datos determinarán los entornos de destino de hello en qué Hola datos necesitan toobe ingestión tooachieve Hola objetivos de su análisis.</span><span class="sxs-lookup"><span data-stu-id="df559-107">Technical and business needs, as well as hello initial location, format and size of your data will determine hello target environments into which hello data needs toobe ingested tooachieve hello goals of your analysis.</span></span> <span data-ttu-id="df559-108">No es raro que un toobe de datos de escenario toorequire movido entre varios entornos tooachieve Hola diversas tareas necesarias tooconstruct un modelo de predicción.</span><span class="sxs-lookup"><span data-stu-id="df559-108">It is not uncommon for a scenario toorequire data toobe moved between several environments tooachieve hello variety of tasks required tooconstruct a predictive model.</span></span> <span data-ttu-id="df559-109">En esta secuencia de tareas se puede incluir, por ejemplo, la exploración de datos, el procesamiento previo, la limpieza, el muestreo inferior y el entrenamiento del modelo.</span><span class="sxs-lookup"><span data-stu-id="df559-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

