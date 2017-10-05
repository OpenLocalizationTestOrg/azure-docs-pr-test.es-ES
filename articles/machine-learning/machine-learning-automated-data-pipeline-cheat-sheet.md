---
title: "Hoja de referencia rápida de canalización de datos automatizada Azure Machine Learning | Microsoft Docs"
description: "Una hoja de referencia rápida imprimible en la que se muestra cómo configurar una canalización de datos automatizada para el servicio web de Azure Machine Learning, si los datos son locales, se transmiten, o se encuentran en Azure o en un servicio en la nube de terceros."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 22674d6b-4491-4805-a3ac-d423611177bb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: mithal;garye
ms.openlocfilehash: e212b2c935eb0ae64ed1cd2e6dc1564f8fcd503b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="cheat-sheet-for-an-automated-data-pipeline-for-azure-machine-learning-predictions"></a><span data-ttu-id="c9cbf-103">Hoja de referencia rápida de una canalización de datos automatizada para las predicciones de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="c9cbf-103">Cheat sheet for an automated data pipeline for Azure Machine Learning predictions</span></span>
<span data-ttu-id="c9cbf-104">La **hoja de referencia rápida de canalización de datos automatizada de aprendizaje automático de Microsoft Azure** le ayuda a navegar por la tecnología que puede usar para obtener sus datos para su servicio web de aprendizaje automático donde se puede puntuar por su modelo de análisis predictivo.</span><span class="sxs-lookup"><span data-stu-id="c9cbf-104">The **Microsoft Azure Machine Learning automated data pipeline cheat sheet** helps you navigate through the technology you can use to get your data to your Machine Learning web service where it can be scored by your predictive analytics model.</span></span>

<span data-ttu-id="c9cbf-105">En función de si los datos se encuentran en local, en la nube o en streaming en tiempo real, existen distintos mecanismos disponibles para mover los datos a su punto de conexión de servicio web para la puntuación.</span><span class="sxs-lookup"><span data-stu-id="c9cbf-105">Depending on whether your data is on-premises, in the cloud, or streaming real-time, there are different mechanisms available to move the data to your web service endpoint for scoring.</span></span>
<span data-ttu-id="c9cbf-106">Esta hoja de referencia rápida lo guía por las decisiones que deberá tomar y ofrece vínculos a los artículos que lo ayudarán a desarrollar su solución.</span><span class="sxs-lookup"><span data-stu-id="c9cbf-106">This cheat sheet walks you through the decisions you need to make, and it offers links to articles that can help you develop your solution.</span></span>

## <a name="download-the-machine-learning-automated-data-pipeline-cheat-sheet"></a><span data-ttu-id="c9cbf-107">Descargar la hoja de referencia rápida de canalización de datos automatizada de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="c9cbf-107">Download the Machine Learning automated data pipeline cheat sheet</span></span>
<span data-ttu-id="c9cbf-108">Cuando descargue la hoja de referencia rápida, puede imprimirla en tamaño tabloide (11 x 17 pulg.).</span><span class="sxs-lookup"><span data-stu-id="c9cbf-108">Once you download the cheat sheet, you can print it in tabloid size (11 x 17 in.).</span></span>

<span data-ttu-id="c9cbf-109">Descargar aquí la hoja de referencia rápida: **[hoja de referencia rápida de canalización de datos automatizada de aprendizaje automático de Microsoft Azure](http://download.microsoft.com/download/C/C/7/CC726F8B-2E6F-4C20-9B6F-AFBEE8253023/microsoft-machine-learning-operationalization-cheat-sheet_v1.pdf)**</span><span class="sxs-lookup"><span data-stu-id="c9cbf-109">Download the cheat sheet here: **[Microsoft Azure Machine Learning automated data pipeline cheat sheet](http://download.microsoft.com/download/C/C/7/CC726F8B-2E6F-4C20-9B6F-AFBEE8253023/microsoft-machine-learning-operationalization-cheat-sheet_v1.pdf)**</span></span>

![Información general de las funcionalidades de Estudio de aprendizaje automático de Microsoft Azure][op-cheat-sheet]

[op-cheat-sheet]: ./media/machine-learning-automated-data-pipeline-cheat-sheet/machine-learning-automated-data-pipeline-cheat-sheet_v1.1.png


## <a name="more-help-with-machine-learning-studio"></a><span data-ttu-id="c9cbf-111">Más ayuda con Estudio de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="c9cbf-111">More help with Machine Learning Studio</span></span>
* <span data-ttu-id="c9cbf-112">Para información general sobre Aprendizaje automático de Microsoft Azure, vea [Introducción a Aprendizaje automático en Microsoft Azure](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="c9cbf-112">For an overview of Microsoft Azure Machine Learning, see [Introduction to machine learning on Microsoft Azure](machine-learning-what-is-machine-learning.md).</span></span>
* <span data-ttu-id="c9cbf-113">Para una explicación de cómo implementar un servicio web de puntuación, vea [Implementación de un servicio web de Aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="c9cbf-113">For an explanation of how to deploy a scoring web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="c9cbf-114">Para obtener una explicación de cómo utilizar un servicio web de puntuación, vea [Cómo consumir un servicio web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="c9cbf-114">For a discussion of how to consume a scoring web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

