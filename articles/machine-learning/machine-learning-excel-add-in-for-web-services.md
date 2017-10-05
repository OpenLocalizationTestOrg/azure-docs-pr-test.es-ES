---
title: Complemento de Excel para los servicios web Machine Learning | Microsoft Docs
description: "Uso de los servicios web Azure Machine Learning directamente en Excel sin escribir código."
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
ms.openlocfilehash: 0d60dd87bbdd4d3eafac0f8876cc9e41412a53ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="2ee62-103">Complemento de Excel para servicios web de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="2ee62-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="2ee62-104">Excel facilita la llamada a servicios web directamente sin necesidad de escribir ningún código.</span><span class="sxs-lookup"><span data-stu-id="2ee62-104">Excel makes it easy to call web services directly without the need to write any code.</span></span>

## <a name="steps-to-use-an-existing-web-service-in-the-workbook"></a><span data-ttu-id="2ee62-105">Pasos para usar un servicio web existente en el libro</span><span class="sxs-lookup"><span data-stu-id="2ee62-105">Steps to Use an Existing web service in the Workbook</span></span>

1. <span data-ttu-id="2ee62-106">Abra el [archivo de Excel de ejemplo](http://aka.ms/amlexcel-sample-2)que contiene el complemento de Excel y los datos acerca de los pasajeros del Titanic.</span><span class="sxs-lookup"><span data-stu-id="2ee62-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span></span>
2. <span data-ttu-id="2ee62-107">Elija el servicio web haciendo clic en él, "Predictor de supervivientes del Titanic (complemento de Excel de ejemplo) [puntuación]" en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2ee62-107">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Seleccionar un servicio web][01]
3. <span data-ttu-id="2ee62-109">Esto le lleva a la sección **Predicción**.</span><span class="sxs-lookup"><span data-stu-id="2ee62-109">This takes you to the **Predict** section.</span></span>  <span data-ttu-id="2ee62-110">Este libro ya contiene datos de ejemplo, pero para un libro en blanco también puede seleccionar una celda en Excel y hacer clic en **Usar datos de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="2ee62-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="2ee62-111">Seleccione los datos con encabezados y haga clic en el icono del intervalo de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="2ee62-111">Select the data with headers and click the input data range icon.</span></span>  <span data-ttu-id="2ee62-112">Asegúrese de que está activada la casilla "Mis datos tienen encabezados".</span><span class="sxs-lookup"><span data-stu-id="2ee62-112">Make sure the "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="2ee62-113">En **Resultado**, escriba el número de la celda donde desea que se muestre el resultado, por ejemplo, "H1" aquí.</span><span class="sxs-lookup"><span data-stu-id="2ee62-113">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span></span>
6. <span data-ttu-id="2ee62-114">Haga clic en **Predicción**.</span><span class="sxs-lookup"><span data-stu-id="2ee62-114">Click **Predict**.</span></span>
   
    ![Sección Predicción][02]

<span data-ttu-id="2ee62-116">Implemente un servicio web o use uno existente.</span><span class="sxs-lookup"><span data-stu-id="2ee62-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="2ee62-117">Para obtener más información sobre cómo implementar un servicio web, consulte el [paso 5 del tutorial: Implementación del servicio web Azure Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="2ee62-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="2ee62-118">Obtenga la clave de API del servicio web.</span><span class="sxs-lookup"><span data-stu-id="2ee62-118">Get the API key for your web service.</span></span> <span data-ttu-id="2ee62-119">Realizará esta acción en un sitio u otro en función de si publicó un servicio web Machine Learning clásico o uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="2ee62-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="2ee62-120">**Uso de un servicio web clásico**</span><span class="sxs-lookup"><span data-stu-id="2ee62-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="2ee62-121">En el Estudio de aprendizaje automático, haga clic en la sección **SERVICIOS WEB** en el panel izquierdo y, luego, seleccione el servicio web.</span><span class="sxs-lookup"><span data-stu-id="2ee62-121">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span></span>
   
    ![Seleccionar un servicio web de Studio][04]
2. <span data-ttu-id="2ee62-123">Copie la clave de API del servicio web.</span><span class="sxs-lookup"><span data-stu-id="2ee62-123">Copy the API key for the web service.</span></span>
   
    ![Clave de API de Studio][05]
3. <span data-ttu-id="2ee62-125">En la pestaña **PANEL** del servicio web, haga clic en el vínculo **SOLICITUD-RESPUESTA**.</span><span class="sxs-lookup"><span data-stu-id="2ee62-125">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="2ee62-126">Busque la sección **URI de solicitud** .</span><span class="sxs-lookup"><span data-stu-id="2ee62-126">Look for the **Request URI** section.</span></span>  <span data-ttu-id="2ee62-127">Copie y guarde la URL.</span><span class="sxs-lookup"><span data-stu-id="2ee62-127">Copy and save the URL.</span></span>

> [!NOTE]
> <span data-ttu-id="2ee62-128">Ahora se puede iniciar sesión en el portal [Servicios web Azure Machine Learning](https://services.azureml.net) para obtener la clave de API de un servicio web Machine Learning clásico.</span><span class="sxs-lookup"><span data-stu-id="2ee62-128">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="2ee62-129">**Uso de un servicio web nuevo**</span><span class="sxs-lookup"><span data-stu-id="2ee62-129">**Use a New web service**</span></span>

1. <span data-ttu-id="2ee62-130">En el portal [Servicios web Azure Machine Learning](https://services.azureml.net), haga clic en **Servicios web** y seleccione su servicio web.</span><span class="sxs-lookup"><span data-stu-id="2ee62-130">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="2ee62-131">Haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="2ee62-131">Click **Consume**.</span></span>
3. <span data-ttu-id="2ee62-132">Busque la sección **Basic consumption info** (Información básica de consumo).</span><span class="sxs-lookup"><span data-stu-id="2ee62-132">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="2ee62-133">Copie y guarde la **clave principal** y la URL de **solicitud-respuesta**.</span><span class="sxs-lookup"><span data-stu-id="2ee62-133">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>

## <a name="steps-to-add-a-new-web-service"></a><span data-ttu-id="2ee62-134">Pasos para agregar un nuevo servicio web</span><span class="sxs-lookup"><span data-stu-id="2ee62-134">Steps to Add a New web service</span></span>

1. <span data-ttu-id="2ee62-135">Implemente un servicio web o use uno existente.</span><span class="sxs-lookup"><span data-stu-id="2ee62-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="2ee62-136">Para obtener más información sobre cómo implementar un servicio web, consulte el [paso 5 del tutorial: Implementación del servicio web Azure Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="2ee62-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="2ee62-137">Haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="2ee62-137">Click **Consume**.</span></span>
3. <span data-ttu-id="2ee62-138">Busque la sección **Basic consumption info** (Información básica de consumo).</span><span class="sxs-lookup"><span data-stu-id="2ee62-138">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="2ee62-139">Copie y guarde la **clave principal** y la URL de **solicitud-respuesta**.</span><span class="sxs-lookup"><span data-stu-id="2ee62-139">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>
4. <span data-ttu-id="2ee62-140">En Excel, vaya a la sección **Servicios web** (si se encuentra en la sección **Predicción**, haga clic en la flecha Atrás para ir a la lista de servicios web).</span><span class="sxs-lookup"><span data-stu-id="2ee62-140">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span></span>
   
    ![Ir a la selección de servicios web][03]
5. <span data-ttu-id="2ee62-142">Haga clic en **Agregar servicio web**.</span><span class="sxs-lookup"><span data-stu-id="2ee62-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="2ee62-143">Pegue la URL en el cuadro de texto de complemento de Excel denominado " **URL**".</span><span class="sxs-lookup"><span data-stu-id="2ee62-143">Paste the URL into the Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="2ee62-144">Pegue la clave principal o de API en el cuadro de texto denominado **Clave de API**.</span><span class="sxs-lookup"><span data-stu-id="2ee62-144">Paste the API/Primary key into the text box labeled **API key**.</span></span>
8. <span data-ttu-id="2ee62-145">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2ee62-145">Click **Add**.</span></span>
   
    ![Dirección URL y clave de API y de un servicio web clásico.][06]
9. <span data-ttu-id="2ee62-147">Para usar el servicio web, siga las instrucciones anteriores, "Pasos para usar un servicio web existente".</span><span class="sxs-lookup"><span data-stu-id="2ee62-147">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="2ee62-148">Compartir el libro</span><span class="sxs-lookup"><span data-stu-id="2ee62-148">Sharing Your Workbook</span></span>
<span data-ttu-id="2ee62-149">Si guarda el libro, también se guardarán la clave principal o de API de los servicios web que también ha guardado.</span><span class="sxs-lookup"><span data-stu-id="2ee62-149">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span></span> <span data-ttu-id="2ee62-150">Esto significa que solo debe compartir el libro con personas de confianza.</span><span class="sxs-lookup"><span data-stu-id="2ee62-150">That means you should only share the workbook with individuals you trust.</span></span>

<span data-ttu-id="2ee62-151">Plantee cualquier pregunta que le surja en la sección de comentarios a continuación o en nuestro [foro](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="2ee62-151">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
