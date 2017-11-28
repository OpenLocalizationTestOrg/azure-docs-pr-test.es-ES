---
title: "aaaVisualize y solucionar problemas de trabajos de análisis de transmisiones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toovisualize un trabajo de análisis de transmisiones de canalización para solución de problemas mediante la característica de diagrama de diagnósticos de Hola de autoservicio."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="419f2-103">Visualización y solución de problemas de trabajos de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="419f2-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="419f2-104">En el análisis de transmisiones, al igual que con otras tecnologías basadas en la nube, solución de problemas a veces es necesario toolook en ¿por qué un trabajo no genera salida de hello esperada (o ningún resultado para este propósito).</span><span class="sxs-lookup"><span data-stu-id="419f2-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed toolook into why a job does not produce hello expected output (or any output for that matter).</span></span> <span data-ttu-id="419f2-105">Con esto en mente, análisis de transmisiones proporciona capacidad de Hola para visualizar un trabajo de streaming.</span><span class="sxs-lookup"><span data-stu-id="419f2-105">With this in mind, Stream Analytics provides hello capability for visualizing a streaming job.</span></span> <span data-ttu-id="419f2-106">Esto también resulta útil como herramienta de modelado y tiene la ventaja colateral de Hola para aquellas que requieren que la documentación de su trabajo.</span><span class="sxs-lookup"><span data-stu-id="419f2-106">This is also handy as a modeling tool and has hello side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="419f2-107">En la visualización de hello son visibles, así como que se va a ejecutar la consulta de hello entradas de Hola de panel y, a continuación, todas las salidas de hello configuran.</span><span class="sxs-lookup"><span data-stu-id="419f2-107">In hello visualization panel hello inputs are visible as well as hello query being executed and then all hello outputs configured.</span></span> <span data-ttu-id="419f2-108">Problemas de conectividad o la configuración pueden resultan más evidentes y también puede ser útil toosee una representación visual de la configuración.</span><span class="sxs-lookup"><span data-stu-id="419f2-108">Connectivity or configuration issues can become more apparent and it can also be helpful toosee a visual representation of your configuration.</span></span>

## <a name="using-hello-diagnosis-diagram-tool"></a><span data-ttu-id="419f2-109">Utilizando la herramienta de diagramas de diagnóstico de Hola</span><span class="sxs-lookup"><span data-stu-id="419f2-109">Using hello diagnosis diagram tool</span></span>
<span data-ttu-id="419f2-110">tooaccess este visualizador, simplemente haga clic en hello en el botón de "Diagrama de diagnóstico" Hola hoja de "Configuración" de hello de trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="419f2-110">tooaccess this visualizer, simply click on hello “Diagnosis diagram” button in hello “Settings” blade of hello of hello Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="419f2-112">Cada entrada y salida es tooindicate codificadas mediante colores Hola estado actual de dicho componente, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="419f2-112">Every input and output is color coded tooindicate hello current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="419f2-114">Cuando el usuario de hello desea toolook en patrones de flujo de datos hello toounderstand de pasos intermedios de la consulta dentro de un trabajo, herramienta de visualización de hello proporciona una vista de desglose de Hola de consulta de hello en sus pasos de componente y la secuencia de flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="419f2-114">When hello user wants toolook at intermediate query steps toounderstand hello data flow patterns inside a job, hello visualization tool provides a view of hello breakdown of hello query into its component steps and hello flow sequence.</span></span> <span data-ttu-id="419f2-115">Al hacer clic en cada paso de consulta mostrará la sección correspondiente de hello en un panel, como se muestra de edición de consultas.</span><span class="sxs-lookup"><span data-stu-id="419f2-115">Clicking on each query step will show hello corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="419f2-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="419f2-117">Next steps</span></span>
* [<span data-ttu-id="419f2-118">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="419f2-118">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="419f2-119">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="419f2-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="419f2-120">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="419f2-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="419f2-121">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="419f2-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="419f2-122">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="419f2-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

