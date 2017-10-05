---
title: Consumo de un servicio web Machine Learning de Excel | Microsoft Docs
description: "Consumir un servicio web de Aprendizaje automático de Azure de Excel"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: 9f1aac04d54221888ee9374317be339400dcf085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="fd7dc-103">Consumo de un servicio web de Aprendizaje automático de Azure de Excel</span><span class="sxs-lookup"><span data-stu-id="fd7dc-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="fd7dc-104">Estudio de aprendizaje automático de Azure facilita la llamada a servicios web directamente desde Excel sin necesidad de escribir ningún código.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-104">Azure Machine Learning Studio makes it easy to call web services directly from Excel without the need to write any code.</span></span>

<span data-ttu-id="fd7dc-105">Si utiliza Excel 2013 (o posterior) o Excel Online, le recomendamos que use el [complemento de Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="fd7dc-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use the Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="fd7dc-106">Pasos</span><span class="sxs-lookup"><span data-stu-id="fd7dc-106">Steps</span></span>
<span data-ttu-id="fd7dc-107">Publicar un servicio web.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-107">Publish a web service.</span></span> <span data-ttu-id="fd7dc-108">[esta página](machine-learning-walkthrough-5-publish-web-service.md) se explica cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how to do it.</span></span> <span data-ttu-id="fd7dc-109">Actualmente, la función de libro de Excel solo se admite para los servicios de solicitud/respuesta que tienen una salida única (es decir, una etiqueta de puntuación única).</span><span class="sxs-lookup"><span data-stu-id="fd7dc-109">Currently the Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="fd7dc-110">Una vez que tenga un servicio web, haga clic en la sección **SERVICIOS WEB** que se encuentra a la izquierda del estudio y, luego, seleccione el servicio web que se va a usar desde Excel.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-110">Once you have a web service, click on the **WEB SERVICES** section on the left of the studio, and then select the web service to consume from Excel.</span></span>

<span data-ttu-id="fd7dc-111">**Servicio web clásico**</span><span class="sxs-lookup"><span data-stu-id="fd7dc-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="fd7dc-112">En la pestaña **PANEL** del servicio web se encuentra una fila para el servicio **SOLICITUD/RESPUESTA**.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-112">On the **DASHBOARD** tab for the web service is a row for the **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="fd7dc-113">Si este servicio tenía una salida única, deberá consultar el vínculo **Descargar el libro de Excel** de esa fila.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-113">If this service had a single output, you should see the **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="fd7dc-114">Haga clic en **Descargar el libro de Excel**.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="fd7dc-115">**Servicio web nuevo**</span><span class="sxs-lookup"><span data-stu-id="fd7dc-115">**New Web Service**</span></span>

1. <span data-ttu-id="fd7dc-116">En el portal de servicios web de Aprendizaje automático de Azure, seleccione **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="fd7dc-116">In the Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="fd7dc-117">En la página de consumo, en la sección **Web service consumption options** (Opciones de consumo del servicio web), haga clic en el icono de Excel.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-117">On the Consume page, in the **Web service consumption options** section, click the Excel icon.</span></span>

<span data-ttu-id="fd7dc-118">**Uso del libro**</span><span class="sxs-lookup"><span data-stu-id="fd7dc-118">**Using the workbook**</span></span>

1. <span data-ttu-id="fd7dc-119">Abra el libro.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-119">Open the workbook.</span></span>
2. <span data-ttu-id="fd7dc-120">Aparecerá una advertencia de seguridad; haga clic en el botón **Habilitar edición** .</span><span class="sxs-lookup"><span data-stu-id="fd7dc-120">A Security Warning appears; click on the **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="fd7dc-121">Aparecerá una advertencia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-121">A Security Warning appears.</span></span> <span data-ttu-id="fd7dc-122">Haga clic en el botón **Habilitar contenido** para ejecutar macros en la hoja de cálculo.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-122">Click on the **Enable Content** button to run macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="fd7dc-123">Una vez que las macros están habilitadas, se generará una tabla.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="fd7dc-124">Las columnas en azul son necesarias como entrada al servicio web RRS, o como **PARÁMETROS**.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-124">Columns in blue are required as input into the RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="fd7dc-125">Tenga en cuenta la salida del servicio RRS, los **VALORES PREDICHOS** en verde.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-125">Note the output of the RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="fd7dc-126">Cuando se llenan todas las columnas de una fila determinada, el libro llama a la API de puntuación automáticamente y muestra los resultados con puntuación.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-126">When all columns for a given row are filled, the workbook automatically calls the scoring API, and displays the scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="fd7dc-127">Para puntuar más de una fila, rellene la segunda fila con datos y se generarán los valores predichos.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-127">To score more than one row, fill the second row with data and the predicted values are produced.</span></span> <span data-ttu-id="fd7dc-128">Incluso puede pegar varias filas a la vez.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="fd7dc-129">Puede utilizar cualquiera de las funciones de Excel (gráficos, asignación de energía, formato condicional, etc.) con los valores de predicción como ayuda para visualizar los datos.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-129">You can use any of the Excel features (graphs, power map, conditional formatting, etc.) with the predicted values to help visualize the data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="fd7dc-130">Compartir el libro</span><span class="sxs-lookup"><span data-stu-id="fd7dc-130">Sharing your workbook</span></span>
<span data-ttu-id="fd7dc-131">Para que las macros funcionen, la clave de API debe formar parte de la hoja de cálculo.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-131">For the macros to work, your API Key must be part of the spreadsheet.</span></span> <span data-ttu-id="fd7dc-132">Esto significa que debe compartir el libro con las entidades e individuos de su confianza.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-132">That means that you should share the workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="fd7dc-133">Actualizaciones automáticas</span><span class="sxs-lookup"><span data-stu-id="fd7dc-133">Automatic updates</span></span>
<span data-ttu-id="fd7dc-134">En las siguientes dos situaciones se realiza una llamada a RRS:</span><span class="sxs-lookup"><span data-stu-id="fd7dc-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="fd7dc-135">La primera vez que una fila tiene contenido en todos sus **PARÁMETROS**</span><span class="sxs-lookup"><span data-stu-id="fd7dc-135">The first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="fd7dc-136">Cada vez que cualquiera de los **PARÁMETROS** cambia en una fila en la que se habían especificado todos sus **PARÁMETROS**.</span><span class="sxs-lookup"><span data-stu-id="fd7dc-136">Any time any of the **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
