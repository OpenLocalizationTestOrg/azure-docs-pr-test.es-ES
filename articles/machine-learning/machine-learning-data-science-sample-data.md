---
title: Muestra de datos en contenedores de blob de Azure, SQL Server y tablas de Hive | Microsoft Docs
description: "Exploración de datos almacenados en diversos entornos de Azure"
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
ms.openlocfilehash: 0683be564a88ef54882e8d882d196851ecac243d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="5656b-103"><a name="heading"></a>Muestra de datos en contenedores de blob de Azure, SQL Server y tablas de Hive</span><span class="sxs-lookup"><span data-stu-id="5656b-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="5656b-104">Este documento incluye vínculos a temas que trata cómo muestrear los datos que se almacenan en una de las tres diferentes ubicaciones de Azure:</span><span class="sxs-lookup"><span data-stu-id="5656b-104">This document links to topics that covers how to sample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="5656b-105">**datos del contenedor de blobs de Azure** descargándolos mediante programación y, a continuación, realizando un muestreo de ellos con el código Python de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5656b-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="5656b-106">**datos de SQL Server** con SQL y el lenguaje de programación Python.</span><span class="sxs-lookup"><span data-stu-id="5656b-106">**SQL Server data** is sampled using both SQL and the Python Programming Language.</span></span> 
* <span data-ttu-id="5656b-107">**datos de las tablas de Hive** mediante consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="5656b-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="5656b-108">El **menú** siguiente vincula a temas que describen cómo se realiza el muestreo de datos desde cada uno de estos entornos de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5656b-108">The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="5656b-109">Esta tarea de muestreo es un paso en el [proceso de ciencia de datos en equipos (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="5656b-109">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="5656b-110">**Razones para el uso de datos de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="5656b-110">**Why sample data?**</span></span>

<span data-ttu-id="5656b-111">Si el conjunto de datos que pretende analizar es grande, es recomendable reducirlo a un tamaño más pequeño, pero representativo, que sea más manejable.</span><span class="sxs-lookup"><span data-stu-id="5656b-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="5656b-112">Esto facilita la comprensión y exploración de los datos, y el diseño de características.</span><span class="sxs-lookup"><span data-stu-id="5656b-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="5656b-113">Su rol en el proceso de análisis de Cortana es permitir la rápida creación de prototipos de las funciones de procesamiento de datos y de los modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="5656b-113">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

