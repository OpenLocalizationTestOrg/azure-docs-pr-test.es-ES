---
title: "Implementación de un nuevo servicio web en Azure Machine Learning | Microsoft Docs"
description: "Flujo de trabajo de la implementación de un servicio web basado en ARM"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: TRUE
ms.openlocfilehash: 1415709f9da2bb2cce859af9feb0ec15c1fa5801
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="e2444-103">Implementación de servicios web nuevos</span><span class="sxs-lookup"><span data-stu-id="e2444-103">Deploy a new web service</span></span>
<span data-ttu-id="e2444-104">Ahora, Microsoft Azure Machine Learning proporciona servicios web basados en [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) , con lo que se pueden usar nuevas opciones de planes de facturación e implementar el servicio web en varias regiones.</span><span class="sxs-lookup"><span data-stu-id="e2444-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service to multiple regions.</span></span>

<span data-ttu-id="e2444-105">El flujo de trabajo general para implementar un servicio web mediante el portal de servicios web de Aprendizaje automático de Microsoft Azure Machine es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="e2444-105">The general workflow to deploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="e2444-106">Crear un experimento predictivo</span><span class="sxs-lookup"><span data-stu-id="e2444-106">Create a predictive experiment</span></span>
* <span data-ttu-id="e2444-107">Implementarlo</span><span class="sxs-lookup"><span data-stu-id="e2444-107">deploy it</span></span>
* <span data-ttu-id="e2444-108">Configurar su nombre</span><span class="sxs-lookup"><span data-stu-id="e2444-108">configure its name</span></span>
* <span data-ttu-id="e2444-109">plan de facturación</span><span class="sxs-lookup"><span data-stu-id="e2444-109">billing plan</span></span>
* <span data-ttu-id="e2444-110">Probarlo</span><span class="sxs-lookup"><span data-stu-id="e2444-110">test it</span></span>
* <span data-ttu-id="e2444-111">Utilizarlo</span><span class="sxs-lookup"><span data-stu-id="e2444-111">consume it.</span></span>

<span data-ttu-id="e2444-112">En el siguiente gráfico se ilustra el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e2444-112">The following graphic illustrates the workflow.</span></span>

![Flujo de trabajo de implementación de servicios web][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="e2444-114">Implementación de servicios web desde Studio</span><span class="sxs-lookup"><span data-stu-id="e2444-114">Deploy web service from Studio</span></span>
<span data-ttu-id="e2444-115">Para implementar un experimento como servicio web nuevo,</span><span class="sxs-lookup"><span data-stu-id="e2444-115">To deploy an experiment as a new web service.</span></span> <span data-ttu-id="e2444-116">inicie sesión en Estudio de aprendizaje automático de Microsoft Azure y cree un nuevo servicio web predictivo.</span><span class="sxs-lookup"><span data-stu-id="e2444-116">Sign into the Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="e2444-117">**Nota**: Si ya ha implementado un experimento como servicio web clásico, no se podrá implementar como nuevo.</span><span class="sxs-lookup"><span data-stu-id="e2444-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="e2444-118">Haga clic en la opción **Ejecutar** de la parte inferior del lienzo del experimento y luego en **Deploy Web Service** (Implementar servicio web) y en **Deploy Web Service [New]** (Implementar servicio web [nuevo]).</span><span class="sxs-lookup"><span data-stu-id="e2444-118">Click **Run** at the bottom of the experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="e2444-119">Se abrirá la página de implementación del administrador de servicios web de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="e2444-119">The deployment page of the Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="e2444-120">Página de implementación de experimentos del administrador de servicios web de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="e2444-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="e2444-121">En la página de implementación de experimentos, escriba un nombre para el servicio web.</span><span class="sxs-lookup"><span data-stu-id="e2444-121">On the Deploy Experiment page, enter a name for the web service.</span></span>
<span data-ttu-id="e2444-122">Seleccione un plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="e2444-122">Select a pricing plan.</span></span> <span data-ttu-id="e2444-123">Si ya tiene uno, puede seleccionarlo; si no, debe crear uno nuevo para el servicio.</span><span class="sxs-lookup"><span data-stu-id="e2444-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for the service.</span></span> 

1. <span data-ttu-id="e2444-124">En el menú desplegable **Price Plan** (Plan de precios), seleccione un plan existente o elija la opción **Select new plan** (Seleccionar nuevo plan).</span><span class="sxs-lookup"><span data-stu-id="e2444-124">In the **Price Plan** drop down, select an existing plan or select the **Select new plan** option.</span></span>
2. <span data-ttu-id="e2444-125">En **Nombre del plan**, escriba un nombre que identifique el plan en la factura.</span><span class="sxs-lookup"><span data-stu-id="e2444-125">In **Plan Name**, type a name that will identify the plan on your bill.</span></span>
3. <span data-ttu-id="e2444-126">Seleccione uno de los **niveles de planes mensuales**.</span><span class="sxs-lookup"><span data-stu-id="e2444-126">Select one of the **Monthly Plan Tiers**.</span></span> <span data-ttu-id="e2444-127">Tenga en cuenta que los niveles de los planes predeterminados son los de la región predeterminada y que el servicio web se implementa en dicha región.</span><span class="sxs-lookup"><span data-stu-id="e2444-127">Note that the plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

<span data-ttu-id="e2444-128">Haga clic en las páginas **Implementar** e Inicio rápido del servicio web que se abre.</span><span class="sxs-lookup"><span data-stu-id="e2444-128">Click **Deploy** and the Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="e2444-129">Página Inicio rápido</span><span class="sxs-lookup"><span data-stu-id="e2444-129">Quickstart page</span></span>
<span data-ttu-id="e2444-130">A través de la página Inicio rápido del servicio web podrá acceder a las tareas más comunes que se realizarán después de crear un servicio web nuevo, así como instrucciones sobre cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="e2444-130">The web service Quickstart page gives you access and guidance on the most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="e2444-131">Desde aquí, también puede acceder fácilmente a las páginas **Prueba** y **Consume** (Consumo).</span><span class="sxs-lookup"><span data-stu-id="e2444-131">From here you can easily access both the **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="e2444-132">Pruebas del servicio web</span><span class="sxs-lookup"><span data-stu-id="e2444-132">Testing your web service</span></span>
<span data-ttu-id="e2444-133">En la página Inicio rápido, haga clic en la opción Test web service (Probar servicio web) de las tareas comunes.</span><span class="sxs-lookup"><span data-stu-id="e2444-133">From the Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="e2444-134">Para probar el servicio web como servicio de solicitud-respuesta (RRS), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e2444-134">To test the web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="e2444-135">Haga clic en **Probar** en la barra de menús.</span><span class="sxs-lookup"><span data-stu-id="e2444-135">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="e2444-136">Haga clic en **Request-Response**(Solicitud-respuesta).</span><span class="sxs-lookup"><span data-stu-id="e2444-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="e2444-137">Escriba los valores adecuados para las columnas de entrada del experimento.</span><span class="sxs-lookup"><span data-stu-id="e2444-137">Enter appropriate values for the input columns of your experiment.</span></span>
* <span data-ttu-id="e2444-138">Haga clic en **Test Request-Response**(Probar solicitud-respuesta).</span><span class="sxs-lookup"><span data-stu-id="e2444-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="e2444-139">Los resultados se mostrarán en el lado derecho de la página.</span><span class="sxs-lookup"><span data-stu-id="e2444-139">You results will display on the right hand side of the page.</span></span>

<span data-ttu-id="e2444-140">Para probar un servicio web de servicio de ejecución de lotes (BES), hay que utilizar un archivo CSV:</span><span class="sxs-lookup"><span data-stu-id="e2444-140">To test a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="e2444-141">Haga clic en **Probar** en la barra de menús.</span><span class="sxs-lookup"><span data-stu-id="e2444-141">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="e2444-142">Haga clic en **Lotes**.</span><span class="sxs-lookup"><span data-stu-id="e2444-142">Click **Batch**.</span></span>
* <span data-ttu-id="e2444-143">En la entrada, haga clic en Examinar y vaya hasta al archivo de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e2444-143">Under your input, click Browse and navigate to your sample data file.</span></span>
* <span data-ttu-id="e2444-144">Haga clic en **Probar**.</span><span class="sxs-lookup"><span data-stu-id="e2444-144">Click **Test**.</span></span>

<span data-ttu-id="e2444-145">El estado de la prueba se muestra en **Test Batch Jobs**(Trabajos de pruebas por lotes).</span><span class="sxs-lookup"><span data-stu-id="e2444-145">The status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="e2444-146">Uso de servicios web</span><span class="sxs-lookup"><span data-stu-id="e2444-146">Consuming your Web Service</span></span>
<span data-ttu-id="e2444-147">Cuando se implementa como servicio web, los experimentos de Aprendizaje automático de Azure proporcionan una API de REST que puede ser consumida por una amplia gama de dispositivos y plataformas.</span><span class="sxs-lookup"><span data-stu-id="e2444-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="e2444-148">Esto es porque la sencilla API de REST acepta y responde con mensajes de formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e2444-148">This is because the simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="e2444-149">El portal de Aprendizaje automático de Azure proporciona código que se puede utilizar para llamar al servicio web en R, C# y Python.</span><span class="sxs-lookup"><span data-stu-id="e2444-149">The Azure Machine Learning portal provides code that can be used to call the web service in R, C#, and Python.</span></span>

<span data-ttu-id="e2444-150">En la página Consuming (Consumo), puede encontrar la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="e2444-150">On the Consuming page you can find:</span></span>

* <span data-ttu-id="e2444-151">La clave de API y los URI para utilizar servicios web en aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e2444-151">The API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="e2444-152">Plantillas de aplicaciones web y de Excel para iniciar rápidamente el proceso de consumo.</span><span class="sxs-lookup"><span data-stu-id="e2444-152">Excel and web app templates to kick start your consumption process.</span></span>
* <span data-ttu-id="e2444-153">El código de ejemplo en C#, Python y R para poder comenzar.</span><span class="sxs-lookup"><span data-stu-id="e2444-153">Sample code in C#, python, and R to get you started.</span></span>

<span data-ttu-id="e2444-154">Para más información sobre el consumo de servicios web, vea [Cómo consumir un servicio web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="e2444-154">For more information on consuming web services, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2444-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2444-155">Next Steps</span></span>
<span data-ttu-id="e2444-156">Para más información sobre el consumo de servicios web, consulte:</span><span class="sxs-lookup"><span data-stu-id="e2444-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="e2444-157">Cómo consumir un servicio web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e2444-157">How to consume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="e2444-158">Servicios web Azure Machine Learning: Implementación y consumo</span><span class="sxs-lookup"><span data-stu-id="e2444-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
