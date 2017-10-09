---
title: "complemento aaaExcel para servicios Web de aprendizaje de máquina | Documentos de Microsoft"
description: "Cómo toouse Azure Machine Learning Web services directamente en Excel sin escribir ningún código."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="fbc88-103">Complemento de Excel para servicios web de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="fbc88-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="fbc88-104">Excel resulta fácil toocall los servicios web directamente sin Hola necesita toowrite cualquier código.</span><span class="sxs-lookup"><span data-stu-id="fbc88-104">Excel makes it easy toocall web services directly without hello need toowrite any code.</span></span>

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a><span data-ttu-id="fbc88-105">Pasos tooUse un servicio web de Existing en hello libro</span><span class="sxs-lookup"><span data-stu-id="fbc88-105">Steps tooUse an Existing web service in hello Workbook</span></span>

1. <span data-ttu-id="fbc88-106">Abra hello [archivo de Excel de ejemplo](http://aka.ms/amlexcel-sample-2), que contiene Hola Excel complemento y datos acerca de los pasajeros en Hola Titanic.</span><span class="sxs-lookup"><span data-stu-id="fbc88-106">Open hello [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains hello Excel add-in and data about passengers on hello Titanic.</span></span>
2. <span data-ttu-id="fbc88-107">Elija el servicio web de hello haciendo clic en él: "Titanic Predictor de permanencia (complemento de Excel de ejemplo) [puntuación]" en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="fbc88-107">Choose hello web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Seleccionar un servicio web][01]
3. <span data-ttu-id="fbc88-109">Esto le llevará toohello **Predict** sección.</span><span class="sxs-lookup"><span data-stu-id="fbc88-109">This takes you toohello **Predict** section.</span></span>  <span data-ttu-id="fbc88-110">Este libro ya contiene datos de ejemplo, pero para un libro en blanco también puede seleccionar una celda en Excel y hacer clic en **Usar datos de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="fbc88-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="fbc88-111">Seleccione datos Hola con los encabezados y haga clic en el icono de rango de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbc88-111">Select hello data with headers and click hello input data range icon.</span></span>  <span data-ttu-id="fbc88-112">Asegúrese de que está activada la casilla de "Mis datos tienen encabezados" de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbc88-112">Make sure hello "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="fbc88-113">En **salida**, escriba el número de células Hola donde desea Hola toobe de salida, por ejemplo "H1" aquí.</span><span class="sxs-lookup"><span data-stu-id="fbc88-113">Under **Output**, enter hello cell number where you want hello output toobe, for example "H1" here.</span></span>
6. <span data-ttu-id="fbc88-114">Haga clic en **Predicción**.</span><span class="sxs-lookup"><span data-stu-id="fbc88-114">Click **Predict**.</span></span>
   
    ![Sección Predicción][02]

<span data-ttu-id="fbc88-116">Implemente un servicio web o use uno existente.</span><span class="sxs-lookup"><span data-stu-id="fbc88-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="fbc88-117">Para obtener más información acerca de cómo implementar un servicio web, consulte [tutorial paso 5: implementar el servicio Web de aprendizaje de máquina de Azure de hello](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="fbc88-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="fbc88-118">Obtener clave de API de hello para el servicio web.</span><span class="sxs-lookup"><span data-stu-id="fbc88-118">Get hello API key for your web service.</span></span> <span data-ttu-id="fbc88-119">Realizará esta acción en un sitio u otro en función de si publicó un servicio web Machine Learning clásico o uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="fbc88-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="fbc88-120">**Uso de un servicio web clásico**</span><span class="sxs-lookup"><span data-stu-id="fbc88-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="fbc88-121">En estudio de aprendizaje automático, haga clic en hello **servicios WEB** sección en el panel izquierdo de hello y, a continuación, seleccione el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbc88-121">In Machine Learning Studio, click hello **WEB SERVICES** section in hello left pane, and then select hello web service.</span></span>
   
    ![Seleccionar un servicio web de Studio][04]
2. <span data-ttu-id="fbc88-123">Copie la clave de API de hello para el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbc88-123">Copy hello API key for hello web service.</span></span>
   
    ![Clave de API de Studio][05]
3. <span data-ttu-id="fbc88-125">En hello **panel** para el servicio web de hello, haga clic en hello **solicitud/respuesta** vínculo.</span><span class="sxs-lookup"><span data-stu-id="fbc88-125">On hello **DASHBOARD** tab for hello web service, click hello **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="fbc88-126">Busque hello **URI de solicitud** sección.</span><span class="sxs-lookup"><span data-stu-id="fbc88-126">Look for hello **Request URI** section.</span></span>  <span data-ttu-id="fbc88-127">Copie y guarde la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbc88-127">Copy and save hello URL.</span></span>

> [!NOTE]
> <span data-ttu-id="fbc88-128">Ahora es posible toosign en hello [servicios Web de Azure Machine Learning](https://services.azureml.net) clave de API de hello tooobtain portal para un servicio web de aprendizaje automático clásico.</span><span class="sxs-lookup"><span data-stu-id="fbc88-128">It is now possible toosign into hello [Azure Machine Learning Web Services](https://services.azureml.net) portal tooobtain hello API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="fbc88-129">**Uso de un servicio web nuevo**</span><span class="sxs-lookup"><span data-stu-id="fbc88-129">**Use a New web service**</span></span>

1. <span data-ttu-id="fbc88-130">Hola [servicios Web de Azure Machine Learning](https://services.azureml.net) portal, haga clic en **servicios Web**, a continuación, seleccione el servicio web.</span><span class="sxs-lookup"><span data-stu-id="fbc88-130">In hello [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="fbc88-131">Haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="fbc88-131">Click **Consume**.</span></span>
3. <span data-ttu-id="fbc88-132">Busque hello **información básica de consumo** sección.</span><span class="sxs-lookup"><span data-stu-id="fbc88-132">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="fbc88-133">Copie y guarde hello **Primary Key** hello y **solicitud-respuesta** dirección URL.</span><span class="sxs-lookup"><span data-stu-id="fbc88-133">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>

## <a name="steps-tooadd-a-new-web-service"></a><span data-ttu-id="fbc88-134">Pasos tooAdd un nuevo servicio web</span><span class="sxs-lookup"><span data-stu-id="fbc88-134">Steps tooAdd a New web service</span></span>

1. <span data-ttu-id="fbc88-135">Implemente un servicio web o use uno existente.</span><span class="sxs-lookup"><span data-stu-id="fbc88-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="fbc88-136">Para obtener más información acerca de cómo implementar un servicio web, consulte [tutorial paso 5: implementar el servicio Web de aprendizaje de máquina de Azure de hello](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="fbc88-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="fbc88-137">Haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="fbc88-137">Click **Consume**.</span></span>
3. <span data-ttu-id="fbc88-138">Busque hello **información básica de consumo** sección.</span><span class="sxs-lookup"><span data-stu-id="fbc88-138">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="fbc88-139">Copie y guarde hello **Primary Key** hello y **solicitud-respuesta** dirección URL.</span><span class="sxs-lookup"><span data-stu-id="fbc88-139">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>
4. <span data-ttu-id="fbc88-140">En Excel, vaya toohello **servicios Web** sección (si se encuentra en hello **Predict** sección, haga clic en hello flecha atrás toogo toohello lista de servicios web).</span><span class="sxs-lookup"><span data-stu-id="fbc88-140">In Excel, go toohello **Web Services** section (if you are in hello **Predict** section, click hello back arrow toogo toohello list of web services).</span></span>
   
    ![Vaya tooWeb selección de servicio][03]
5. <span data-ttu-id="fbc88-142">Haga clic en **Agregar servicio web**.</span><span class="sxs-lookup"><span data-stu-id="fbc88-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="fbc88-143">Pegue la URL de hello en hello la etiqueta de cuadro de texto de complemento de Excel **URL**.</span><span class="sxs-lookup"><span data-stu-id="fbc88-143">Paste hello URL into hello Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="fbc88-144">Clave de API/primario pegar hello en el cuadro de texto hello con la etiqueta **clave de API**.</span><span class="sxs-lookup"><span data-stu-id="fbc88-144">Paste hello API/Primary key into hello text box labeled **API key**.</span></span>
8. <span data-ttu-id="fbc88-145">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fbc88-145">Click **Add**.</span></span>
   
    ![Dirección URL y clave de API y de un servicio web clásico.][06]
9. <span data-ttu-id="fbc88-147">servicio web de toouse hello, siga Hola anterior direcciones, "Pasos tooUse un servicio web de existente."</span><span class="sxs-lookup"><span data-stu-id="fbc88-147">toouse hello web service, follow hello preceding directions, "Steps tooUse an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="fbc88-148">Compartir el libro</span><span class="sxs-lookup"><span data-stu-id="fbc88-148">Sharing Your Workbook</span></span>
<span data-ttu-id="fbc88-149">Si guarda el libro, clave de API principal de Hola para servicios web de hello que ha agregado también se guarda.</span><span class="sxs-lookup"><span data-stu-id="fbc88-149">If you save your workbook, then hello API/Primary key for hello web services you have added is also saved.</span></span> <span data-ttu-id="fbc88-150">Esto significa que solo deben compartir el libro Hola con personas de que confianza.</span><span class="sxs-lookup"><span data-stu-id="fbc88-150">That means you should only share hello workbook with individuals you trust.</span></span>

<span data-ttu-id="fbc88-151">Hacer preguntas en hello después de la sección de comentarios o en nuestros [foro](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="fbc88-151">Ask any questions in hello following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
