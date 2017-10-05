---
title: "Carga de datos en entornos de almacenamiento de Azure para el análisis | Microsoft Docs"
description: Mover datos hacia y desde el almacenamiento de blobs de Azure
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
ms.openlocfilehash: 7fbf3bfedca8fa57a5e9428c9399558992b4acbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="895d9-103">Carga de datos en entornos de almacenamiento para el análisis</span><span class="sxs-lookup"><span data-stu-id="895d9-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="895d9-104">El proceso de ciencia de datos en equipos requiere que los datos se introduzcan o se cargue en una variedad de entornos de almacenamiento diferentes para que se procesen o analicen de la manera más adecuada en cada fase del proceso.</span><span class="sxs-lookup"><span data-stu-id="895d9-104">The Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments to be processed or analyzed in the most appropriate way in each stage of the process.</span></span> <span data-ttu-id="895d9-105">Entre los destinos de datos más usados para el procesamiento se incluyen el almacenamiento de blobs de Azure, las bases de datos SQL Azure, SQL Server en VM de Azure, HDInsight (Hadoop) y Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="895d9-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="895d9-106">Este **menú** vincula a temas en los que se describe cómo introducir datos en estos entornos de destino donde se almacenan y se procesan los datos.</span><span class="sxs-lookup"><span data-stu-id="895d9-106">This **menu** links to topics that describe how to ingest data into these target environments where the data is stored and processed.</span></span>

<span data-ttu-id="895d9-107">Las necesidades técnicas y empresariales, así como la ubicación inicial, el formato y el tamaño de sus datos determinarán los entornos de destino en los que deben introducirse los datos para lograr los objetivos de su análisis.</span><span class="sxs-lookup"><span data-stu-id="895d9-107">Technical and business needs, as well as the initial location, format and size of your data will determine the target environments into which the data needs to be ingested to achieve the goals of your analysis.</span></span> <span data-ttu-id="895d9-108">No es raro que un escenario requiera que los datos se muevan entre varios entornos para lograr la variedad de las tareas necesarias para construir un modelo predictivo.</span><span class="sxs-lookup"><span data-stu-id="895d9-108">It is not uncommon for a scenario to require data to be moved between several environments to achieve the variety of tasks required to construct a predictive model.</span></span> <span data-ttu-id="895d9-109">En esta secuencia de tareas se puede incluir, por ejemplo, la exploración de datos, el procesamiento previo, la limpieza, el muestreo inferior y el entrenamiento del modelo.</span><span class="sxs-lookup"><span data-stu-id="895d9-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

