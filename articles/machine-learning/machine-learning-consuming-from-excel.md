---
title: "un servicio Web de aprendizaje de máquina desde Excel aaaConsume | Documentos de Microsoft"
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
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="89d06-103">Consumo de un servicio web de Aprendizaje automático de Azure de Excel</span><span class="sxs-lookup"><span data-stu-id="89d06-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="89d06-104">Estudio de aprendizaje automático de Azure hace fácil toocall los servicios web directamente desde Excel sin Hola necesita toowrite cualquier código.</span><span class="sxs-lookup"><span data-stu-id="89d06-104">Azure Machine Learning Studio makes it easy toocall web services directly from Excel without hello need toowrite any code.</span></span>

<span data-ttu-id="89d06-105">Si utiliza Excel 2013 (o posterior) o Excel Online, se recomienda que use Excel hello [complemento de Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="89d06-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use hello Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="89d06-106">Pasos</span><span class="sxs-lookup"><span data-stu-id="89d06-106">Steps</span></span>
<span data-ttu-id="89d06-107">Publicar un servicio web.</span><span class="sxs-lookup"><span data-stu-id="89d06-107">Publish a web service.</span></span> <span data-ttu-id="89d06-108">[Esta página](machine-learning-walkthrough-5-publish-web-service.md) explica cómo toodo lo.</span><span class="sxs-lookup"><span data-stu-id="89d06-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how toodo it.</span></span> <span data-ttu-id="89d06-109">Actualmente la característica de libro de Excel de hello solo se admite para los servicios de solicitud/respuesta que tienen una salida única (es decir, una etiqueta de puntuación única).</span><span class="sxs-lookup"><span data-stu-id="89d06-109">Currently hello Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="89d06-110">Una vez que tenga un servicio web, haga clic en hello **servicios WEB** sección izquierda Hola de studio hello y, a continuación, seleccione tooconsume de servicio web de Hola desde Excel.</span><span class="sxs-lookup"><span data-stu-id="89d06-110">Once you have a web service, click on hello **WEB SERVICES** section on hello left of hello studio, and then select hello web service tooconsume from Excel.</span></span>

<span data-ttu-id="89d06-111">**Servicio web clásico**</span><span class="sxs-lookup"><span data-stu-id="89d06-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="89d06-112">En hello **panel** ficha servicio web de hello es una fila para hello **solicitud/respuesta** servicio.</span><span class="sxs-lookup"><span data-stu-id="89d06-112">On hello **DASHBOARD** tab for hello web service is a row for hello **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="89d06-113">Si este servicio tiene una salida única, debería ver Hola **descargar el libro de Excel** vínculo en esa fila.</span><span class="sxs-lookup"><span data-stu-id="89d06-113">If this service had a single output, you should see hello **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="89d06-114">Haga clic en **Descargar el libro de Excel**.</span><span class="sxs-lookup"><span data-stu-id="89d06-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="89d06-115">**Servicio web nuevo**</span><span class="sxs-lookup"><span data-stu-id="89d06-115">**New Web Service**</span></span>

1. <span data-ttu-id="89d06-116">En el portal de servicio Web de Azure Machine Learning hello, seleccione **usar**.</span><span class="sxs-lookup"><span data-stu-id="89d06-116">In hello Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="89d06-117">En página de consumir hello, Hola **opciones de consumo del servicio Web** sección, haga clic en el icono de Excel de Hola.</span><span class="sxs-lookup"><span data-stu-id="89d06-117">On hello Consume page, in hello **Web service consumption options** section, click hello Excel icon.</span></span>

<span data-ttu-id="89d06-118">**Utilizando el libro de Hola**</span><span class="sxs-lookup"><span data-stu-id="89d06-118">**Using hello workbook**</span></span>

1. <span data-ttu-id="89d06-119">Libro de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="89d06-119">Open hello workbook.</span></span>
2. <span data-ttu-id="89d06-120">Aparece una advertencia de seguridad; Haga clic en hello **Habilitar edición** botón.</span><span class="sxs-lookup"><span data-stu-id="89d06-120">A Security Warning appears; click on hello **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="89d06-121">Aparecerá una advertencia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="89d06-121">A Security Warning appears.</span></span> <span data-ttu-id="89d06-122">Haga clic en hello **Habilitar contenido** botón toorun macros en la hoja de cálculo.</span><span class="sxs-lookup"><span data-stu-id="89d06-122">Click on hello **Enable Content** button toorun macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="89d06-123">Una vez que las macros están habilitadas, se generará una tabla.</span><span class="sxs-lookup"><span data-stu-id="89d06-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="89d06-124">Columnas en azul son necesarias como entrada en hello servicio web de RR, o **parámetros**.</span><span class="sxs-lookup"><span data-stu-id="89d06-124">Columns in blue are required as input into hello RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="89d06-125">Tenga en cuenta la salida de hello de hello servicio RR, **valores PREDICHOS** en verde.</span><span class="sxs-lookup"><span data-stu-id="89d06-125">Note hello output of hello RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="89d06-126">Cuando se llenan todas las columnas de una fila determinada, libro Hola llama Hola API de puntuación y muestra hello resultados puntuado.</span><span class="sxs-lookup"><span data-stu-id="89d06-126">When all columns for a given row are filled, hello workbook automatically calls hello scoring API, and displays hello scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="89d06-127">tooscore más de una fila, la segunda fila de Hola de relleno con los datos y Hola predecir se generan los valores.</span><span class="sxs-lookup"><span data-stu-id="89d06-127">tooscore more than one row, fill hello second row with data and hello predicted values are produced.</span></span> <span data-ttu-id="89d06-128">Incluso puede pegar varias filas a la vez.</span><span class="sxs-lookup"><span data-stu-id="89d06-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="89d06-129">Puede usar cualquiera de las características de Excel hello (gráficos, asignación de energía, condicional formato, etc.) con hello predicha valores toohelp visualizar datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="89d06-129">You can use any of hello Excel features (graphs, power map, conditional formatting, etc.) with hello predicted values toohelp visualize hello data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="89d06-130">Compartir el libro</span><span class="sxs-lookup"><span data-stu-id="89d06-130">Sharing your workbook</span></span>
<span data-ttu-id="89d06-131">Para hello macros toowork, la clave de API debe formar parte de la hoja de cálculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="89d06-131">For hello macros toowork, your API Key must be part of hello spreadsheet.</span></span> <span data-ttu-id="89d06-132">Que significa que deben compartir libro Hola únicamente con personas o entidades de confianza.</span><span class="sxs-lookup"><span data-stu-id="89d06-132">That means that you should share hello workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="89d06-133">Actualizaciones automáticas</span><span class="sxs-lookup"><span data-stu-id="89d06-133">Automatic updates</span></span>
<span data-ttu-id="89d06-134">En las siguientes dos situaciones se realiza una llamada a RRS:</span><span class="sxs-lookup"><span data-stu-id="89d06-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="89d06-135">Hola la primera vez que una fila tiene contenido en todos sus **parámetros**</span><span class="sxs-lookup"><span data-stu-id="89d06-135">hello first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="89d06-136">Cada vez que cualquiera de hello **parámetros** cambios en una fila que tenían todos sus **parámetros** especificado.</span><span class="sxs-lookup"><span data-stu-id="89d06-136">Any time any of hello **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
