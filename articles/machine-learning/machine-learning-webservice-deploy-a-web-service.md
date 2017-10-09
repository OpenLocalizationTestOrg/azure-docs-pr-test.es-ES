---
title: "aaaDeploying un nuevo servicio web de aprendizaje automático de Azure | Documentos de Microsoft"
description: "flujo de trabajo de saludo de la implementación de un BRAZO en función de servicio web"
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
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="980bc-103">Implementación de servicios web nuevos</span><span class="sxs-lookup"><span data-stu-id="980bc-103">Deploy a new web service</span></span>
<span data-ttu-id="980bc-104">Microsoft Azure Machine learning ahora proporciona servicios web que se basan en [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) permitiendo nuevas opciones del plan de facturación y la implementación de las áreas de toomultiple del servicio web.</span><span class="sxs-lookup"><span data-stu-id="980bc-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service toomultiple regions.</span></span>

<span data-ttu-id="980bc-105">flujo de trabajo general de Hello toodeploy un servicio web mediante servicios Web de Microsoft Azure Machine Learning es:</span><span class="sxs-lookup"><span data-stu-id="980bc-105">hello general workflow toodeploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="980bc-106">Crear un experimento predictivo</span><span class="sxs-lookup"><span data-stu-id="980bc-106">Create a predictive experiment</span></span>
* <span data-ttu-id="980bc-107">Implementarlo</span><span class="sxs-lookup"><span data-stu-id="980bc-107">deploy it</span></span>
* <span data-ttu-id="980bc-108">Configurar su nombre</span><span class="sxs-lookup"><span data-stu-id="980bc-108">configure its name</span></span>
* <span data-ttu-id="980bc-109">plan de facturación</span><span class="sxs-lookup"><span data-stu-id="980bc-109">billing plan</span></span>
* <span data-ttu-id="980bc-110">Probarlo</span><span class="sxs-lookup"><span data-stu-id="980bc-110">test it</span></span>
* <span data-ttu-id="980bc-111">Utilizarlo</span><span class="sxs-lookup"><span data-stu-id="980bc-111">consume it.</span></span>

<span data-ttu-id="980bc-112">Hola siguiente gráfico ilustra el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="980bc-112">hello following graphic illustrates hello workflow.</span></span>

![Flujo de trabajo de implementación de servicios web][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="980bc-114">Implementación de servicios web desde Studio</span><span class="sxs-lookup"><span data-stu-id="980bc-114">Deploy web service from Studio</span></span>
<span data-ttu-id="980bc-115">toodeploy un experimento como un nuevo servicio web.</span><span class="sxs-lookup"><span data-stu-id="980bc-115">toodeploy an experiment as a new web service.</span></span> <span data-ttu-id="980bc-116">Inicie sesión en estudio de aprendizaje automático de Hola y crear un nuevo servicio web de predicción.</span><span class="sxs-lookup"><span data-stu-id="980bc-116">Sign into hello Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="980bc-117">**Nota**: Si ya ha implementado un experimento como servicio web clásico, no se podrá implementar como nuevo.</span><span class="sxs-lookup"><span data-stu-id="980bc-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="980bc-118">Haga clic en **ejecutar** final Hola de hello experimentar el lienzo y, a continuación, haga clic en **implementar el servicio de Web** y **implementar [New] servicio Web**.</span><span class="sxs-lookup"><span data-stu-id="980bc-118">Click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="980bc-119">se abrirá la página de implementación de Hello del administrador del servicio Web de aprendizaje de máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="980bc-119">hello deployment page of hello Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="980bc-120">Página de implementación de experimentos del administrador de servicios web de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="980bc-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="980bc-121">En página de experimento implementar hello, escriba un nombre para el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="980bc-121">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="980bc-122">Seleccione un plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="980bc-122">Select a pricing plan.</span></span> <span data-ttu-id="980bc-123">En caso contrario, si tiene un plan de precios existente que seleccione la plantilla, debe crear un nuevo plan de precios para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="980bc-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span> 

1. <span data-ttu-id="980bc-124">Hola **Plan de precios** de lista desplegable, seleccione un plan existente o hello **seleccione Nuevo plan** opción.</span><span class="sxs-lookup"><span data-stu-id="980bc-124">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="980bc-125">En **el nombre del Plan**, escriba un nombre que identificará el plan de hello en la factura.</span><span class="sxs-lookup"><span data-stu-id="980bc-125">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="980bc-126">Seleccione uno de hello **mensual niveles planear**.</span><span class="sxs-lookup"><span data-stu-id="980bc-126">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="980bc-127">Tenga en cuenta que los niveles de plan de hello predeterminado toohello planes para la región predeterminada y el servicio web es la región de toothat implementado.</span><span class="sxs-lookup"><span data-stu-id="980bc-127">Note that hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="980bc-128">Haga clic en **implementar** y se abre la página de inicio rápido de hello para el servicio web.</span><span class="sxs-lookup"><span data-stu-id="980bc-128">Click **Deploy** and hello Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="980bc-129">Página Inicio rápido</span><span class="sxs-lookup"><span data-stu-id="980bc-129">Quickstart page</span></span>
<span data-ttu-id="980bc-130">página de inicio rápido del servicio de Hello web proporciona acceso e instrucciones sobre las tareas más comunes de hello que llevará a cabo después de crear un nuevo servicio web.</span><span class="sxs-lookup"><span data-stu-id="980bc-130">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="980bc-131">Desde aquí puede acceder fácilmente ambos hello **prueba** página y **Consume** página.</span><span class="sxs-lookup"><span data-stu-id="980bc-131">From here you can easily access both hello **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="980bc-132">Pruebas del servicio web</span><span class="sxs-lookup"><span data-stu-id="980bc-132">Testing your web service</span></span>
<span data-ttu-id="980bc-133">Desde la página de inicio rápido de hello, haga clic en servicio web de prueba en las tareas comunes.</span><span class="sxs-lookup"><span data-stu-id="980bc-133">From hello Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="980bc-134">servicio web de hello tootest como un servicio de solicitud-respuesta (RR):</span><span class="sxs-lookup"><span data-stu-id="980bc-134">tootest hello web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="980bc-135">Haga clic en **prueba** en la barra de menús de Hola.</span><span class="sxs-lookup"><span data-stu-id="980bc-135">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="980bc-136">Haga clic en **Request-Response**(Solicitud-respuesta).</span><span class="sxs-lookup"><span data-stu-id="980bc-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="980bc-137">Escriba los valores adecuados para las columnas de entrada de su experimento Hola.</span><span class="sxs-lookup"><span data-stu-id="980bc-137">Enter appropriate values for hello input columns of your experiment.</span></span>
* <span data-ttu-id="980bc-138">Haga clic en **Test Request-Response**(Probar solicitud-respuesta).</span><span class="sxs-lookup"><span data-stu-id="980bc-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="980bc-139">Resultados se muestran en hello lado derecho de la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="980bc-139">You results will display on hello right hand side of hello page.</span></span>

<span data-ttu-id="980bc-140">tootest un servicio web de servicio de ejecución de lotes (BES), se utilizará un archivo CSV:</span><span class="sxs-lookup"><span data-stu-id="980bc-140">tootest a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="980bc-141">Haga clic en **prueba** en la barra de menús de Hola.</span><span class="sxs-lookup"><span data-stu-id="980bc-141">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="980bc-142">Haga clic en **Lotes**.</span><span class="sxs-lookup"><span data-stu-id="980bc-142">Click **Batch**.</span></span>
* <span data-ttu-id="980bc-143">En la entrada, haga clic en Examinar y navegar por el archivo de datos de ejemplo de tooyour.</span><span class="sxs-lookup"><span data-stu-id="980bc-143">Under your input, click Browse and navigate tooyour sample data file.</span></span>
* <span data-ttu-id="980bc-144">Haga clic en **Probar**.</span><span class="sxs-lookup"><span data-stu-id="980bc-144">Click **Test**.</span></span>

<span data-ttu-id="980bc-145">estado de saludo de la prueba se muestra bajo **probar los trabajos por lotes**.</span><span class="sxs-lookup"><span data-stu-id="980bc-145">hello status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="980bc-146">Uso de servicios web</span><span class="sxs-lookup"><span data-stu-id="980bc-146">Consuming your Web Service</span></span>
<span data-ttu-id="980bc-147">Cuando se implementa como servicio web, los experimentos de Aprendizaje automático de Azure proporcionan una API de REST que puede ser consumida por una amplia gama de dispositivos y plataformas.</span><span class="sxs-lookup"><span data-stu-id="980bc-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="980bc-148">Esto es porque los mensajes con formato Hola simple API de REST acepta y responde con JSON.</span><span class="sxs-lookup"><span data-stu-id="980bc-148">This is because hello simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="980bc-149">portal de aprendizaje automático de Azure Hello proporciona código que se puede usar toocall Hola servicio web en R, C# y Python.</span><span class="sxs-lookup"><span data-stu-id="980bc-149">hello Azure Machine Learning portal provides code that can be used toocall hello web service in R, C#, and Python.</span></span>

<span data-ttu-id="980bc-150">En la página de hello Consuming encontrará:</span><span class="sxs-lookup"><span data-stu-id="980bc-150">On hello Consuming page you can find:</span></span>

* <span data-ttu-id="980bc-151">clave de API de Hola y el URI para consumir el servicio web en aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="980bc-151">hello API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="980bc-152">Tookick de plantillas de aplicación web y Excel inicie el proceso de consumo.</span><span class="sxs-lookup"><span data-stu-id="980bc-152">Excel and web app templates tookick start your consumption process.</span></span>
* <span data-ttu-id="980bc-153">Código de ejemplo en C#, python y R tooget ha iniciado.</span><span class="sxs-lookup"><span data-stu-id="980bc-153">Sample code in C#, python, and R tooget you started.</span></span>

<span data-ttu-id="980bc-154">Para obtener más información sobre el consumo de servicios web, consulte [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="980bc-154">For more information on consuming web services, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="980bc-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="980bc-155">Next Steps</span></span>
<span data-ttu-id="980bc-156">Para más información sobre el consumo de servicios web, consulte:</span><span class="sxs-lookup"><span data-stu-id="980bc-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="980bc-157">¿Cómo tooconsume un servicio Web de aprendizaje de máquina de Azure</span><span class="sxs-lookup"><span data-stu-id="980bc-157">How tooconsume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="980bc-158">Servicios web Azure Machine Learning: Implementación y consumo</span><span class="sxs-lookup"><span data-stu-id="980bc-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
