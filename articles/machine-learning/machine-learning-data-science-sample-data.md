---
title: aaaSample datos en Azure, SQL Server, los contenedores de blobs y tablas de Hive | Documentos de Microsoft
description: "Cómo tooexplore datos almacenan en varios enviromnents de Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="90c14-103"><a name="heading"></a>Muestra de datos en contenedores de blob de Azure, SQL Server y tablas de Hive</span><span class="sxs-lookup"><span data-stu-id="90c14-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="90c14-104">Este documento se incluyen vínculos tootopics que cubre cómo toosample datos que se almacenan en uno de tres ubicaciones diferentes de Azure:</span><span class="sxs-lookup"><span data-stu-id="90c14-104">This document links tootopics that covers how toosample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="90c14-105">**datos del contenedor de blobs de Azure** descargándolos mediante programación y, a continuación, realizando un muestreo de ellos con el código Python de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="90c14-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="90c14-106">**Datos de SQL Server** se muestrean mediante SQL y el lenguaje de programación Python Hola.</span><span class="sxs-lookup"><span data-stu-id="90c14-106">**SQL Server data** is sampled using both SQL and hello Python Programming Language.</span></span> 
* <span data-ttu-id="90c14-107">**datos de las tablas de Hive** mediante consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="90c14-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="90c14-108">siguiente Hello **menú** vincula toohello temas que describen cómo toosample datos de cada uno de estos entornos de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="90c14-108">hello following **menu** links toohello topics that describe how toosample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="90c14-109">Esta tarea de muestreo es un paso en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="90c14-109">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="90c14-110">**Razones para el uso de datos de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="90c14-110">**Why sample data?**</span></span>

<span data-ttu-id="90c14-111">Si piensa tooanalyze de conjunto de datos de hello es grande, normalmente es un tooreduce de datos de ejemplo toodown Hola buena idea tooa más pequeño pero representativo y más fáciles de administrar el tamaño.</span><span class="sxs-lookup"><span data-stu-id="90c14-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="90c14-112">Esto facilita la comprensión y exploración de los datos, y el diseño de características.</span><span class="sxs-lookup"><span data-stu-id="90c14-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="90c14-113">Su función en el proceso de análisis de Cortana de hello es tooenable la creación de prototipos rápida de las funciones de procesamiento de datos de Hola y modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="90c14-113">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

