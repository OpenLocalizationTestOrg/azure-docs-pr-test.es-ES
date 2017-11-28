---
title: Registro para servicios web Machine Learning | Microsoft Docs
description: "Aprenda cómo habilitar el registro para los servicios web de Aprendizaje automático. El registro proporciona información adicional para ayudar a solucionar las API."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: 7d0b2db01427430d6b0a317cdfefc265dd4b06e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="4b66c-104">Habilitar el registro para los servicios web de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="4b66c-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="4b66c-105">Este documento proporciona información sobre la funcionalidad de registro de los servicios web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4b66c-105">This document provides information on the logging capability of Machine Learning web services.</span></span> <span data-ttu-id="4b66c-106">El registro ofrece información adicional, más allá de simplemente un número de error y un mensaje, que puede ayudarle a solucionar problemas con las llamadas a las API de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4b66c-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span></span>  

## <a name="how-to-enable-logging-for-a-web-service"></a><span data-ttu-id="4b66c-107">Habilitación del registro para un servicio web</span><span class="sxs-lookup"><span data-stu-id="4b66c-107">How to enable logging for a Web service</span></span>

<span data-ttu-id="4b66c-108">El registro se habilita desde el portal de [servicios web de Azure Machine Learning](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="4b66c-108">You enable logging from the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="4b66c-109">Inicie sesión en el portal de servicios web de Machine Learning en [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="4b66c-109">Sign in to the Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="4b66c-110">Para servicios web clásicos, también puede llegar al portal si hace clic en **New Web Services Experience** (Nueva experiencia de servicios web) en la página de servicios web de Machine Learning en Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4b66c-110">For a Classic web service, you can also get to the portal by clicking **New Web Services Experience** on the Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Nuevo vínculo a la experiencia de servicios web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="4b66c-112">En la barra de menús superior, haga clic en **Servicios web** si es un nuevo servicio web o en **Classic Web Services** (Servicios web clásicos) si es un servicio web clásico.</span><span class="sxs-lookup"><span data-stu-id="4b66c-112">On the top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Selección de servicios web nuevos o clásicos](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="4b66c-114">Si es un nuevo servicio web, haga clic en el nombre del servicio web.</span><span class="sxs-lookup"><span data-stu-id="4b66c-114">For a New web service, click the web service name.</span></span> <span data-ttu-id="4b66c-115">Si es un servicio web clásico, haga clic en el nombre del servicio web y, a continuación, en la siguiente página, haga clic en el punto de conexión adecuado.</span><span class="sxs-lookup"><span data-stu-id="4b66c-115">For a Classic web service, click the web service name and then on the next page click the appropriate endpoint.</span></span>

4. <span data-ttu-id="4b66c-116">En la barra de menús superior, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="4b66c-116">On the top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="4b66c-117">Establezca la opción **Habilitar registro** en *Error* (para registrar solo los errores) o en *Todo* (para realizar un registro completo).</span><span class="sxs-lookup"><span data-stu-id="4b66c-117">Set the **Enable Logging** option to *Error* (to log only errors) or *All* (for full logging).</span></span>

   ![Selección del nivel de registro](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="4b66c-119">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4b66c-119">Click **Save**.</span></span>

7. <span data-ttu-id="4b66c-120">En servicios web clásicos, cree el contenedor **ml-diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="4b66c-120">For Classic web services, create the **ml-diagnostics** container.</span></span>

   <span data-ttu-id="4b66c-121">Todos los registros de servicios web se mantienen en un contenedor de blobs llamado **ml-diagnostics** en la cuenta de almacenamiento asociada con el servicio web.</span><span class="sxs-lookup"><span data-stu-id="4b66c-121">All web service logs are kept in a blob container named **ml-diagnostics** in the storage account associated with the web service.</span></span> <span data-ttu-id="4b66c-122">En nuevos servicios web, este contenedor se crea la primera vez que se accede al servicio web.</span><span class="sxs-lookup"><span data-stu-id="4b66c-122">For New web services, this container is created the first time you access the web service.</span></span> <span data-ttu-id="4b66c-123">En servicios web clásicos, debe crear el contenedor si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="4b66c-123">For Classic web services, you need to create the container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="4b66c-124">En [Azure Portal](https://portal.azure.com), vaya a la cuenta de almacenamiento asociada con el servicio web.</span><span class="sxs-lookup"><span data-stu-id="4b66c-124">In the [Azure portal](https://portal.azure.com), go to the storage account associated with the web service.</span></span>

   2. <span data-ttu-id="4b66c-125">En **Blob service**, haga clic en **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="4b66c-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="4b66c-126">Si el contenedor **ml-diagnostics** no existe, haga clic en **+Contenedor**, proporcione al contenedor el nombre "ml-diagnostics" y seleccione "Blob" como el **Tipo de acceso**.</span><span class="sxs-lookup"><span data-stu-id="4b66c-126">If the container **ml-diagnostics** doesn't exist, click **+Container**, give the container the name "ml-diagnostics", and select the **Access type** as "Blob".</span></span> <span data-ttu-id="4b66c-127">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4b66c-127">Click **OK**.</span></span>

      ![Selección del nivel de registro](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="4b66c-129">En servicios web clásicos, el panel de servicios web de Machine Learning Studio tiene también un conmutador para habilitar el registro.</span><span class="sxs-lookup"><span data-stu-id="4b66c-129">For a Classic web service, the Web Services Dashboard in Machine Learning Studio also has a switch to enable logging.</span></span> <span data-ttu-id="4b66c-130">Sin embargo, puesto que el registro se administra ahora mediante el portal de servicios web, deberá habilitarlo en dicho portal, como se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="4b66c-130">However, because logging is now managed through the Web Services portal, you need to enable logging through the portal as described in this article.</span></span> <span data-ttu-id="4b66c-131">Si ya habilitó el registro en Studio, en el portal de servicios web deshabilítelo y vuelva a habilitarlo.</span><span class="sxs-lookup"><span data-stu-id="4b66c-131">If you already enabled logging in Studio, then in the Web Services Portal, disable logging and enable it again.</span></span>


## <a name="the-effects-of-enabling-logging"></a><span data-ttu-id="4b66c-132">Consecuencias de habilitar el registro</span><span class="sxs-lookup"><span data-stu-id="4b66c-132">The effects of enabling logging</span></span>
<span data-ttu-id="4b66c-133">Cuando el registro está habilitado, el diagnóstico y los errores del punto de conexión de servicio Web se registran en el contenedor de blobs **ml-diagnostics** en la cuenta de Azure Storage vinculada al área de trabajo del usuario.</span><span class="sxs-lookup"><span data-stu-id="4b66c-133">When logging is enabled, the diagnostics and errors from the web service endpoint are logged in the **ml-diagnostics** blob container in the Azure Storage Account linked with the user’s workspace.</span></span> <span data-ttu-id="4b66c-134">Este contenedor incluye toda la información de diagnóstico de todos los puntos de conexión de servicio Web relativos a todas las áreas de trabajo asociadas a esta cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4b66c-134">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this storage account.</span></span>

<span data-ttu-id="4b66c-135">Los registros pueden verse mediante cualquiera de las diversas herramientas disponibles para explorar una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4b66c-135">The logs can be viewed using any of the several tools available to explore an Azure Storage Account.</span></span> <span data-ttu-id="4b66c-136">Lo más sencillo puede ser desplazarse a la cuenta de almacenamiento en el portal de Azure, hacer clic en **Contenedores** y luego en el contenedor **ml-diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="4b66c-136">The easiest may be to navigate to the storage account in the Azure portal, click **Containers**, and then click the container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="4b66c-137">Información detallada sobre el blob de registro</span><span class="sxs-lookup"><span data-stu-id="4b66c-137">Log blob detail information</span></span>
<span data-ttu-id="4b66c-138">Cada blob del contenedor incluye la información de diagnóstico de exactamente una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="4b66c-138">Each blob in the container holds the diagnostics information for exactly one of the following actions:</span></span>

* <span data-ttu-id="4b66c-139">Una ejecución del método Batch-Execution</span><span class="sxs-lookup"><span data-stu-id="4b66c-139">An execution of the Batch-Execution method</span></span>  
* <span data-ttu-id="4b66c-140">Una ejecución del método Request-Response</span><span class="sxs-lookup"><span data-stu-id="4b66c-140">An execution of the Request-Response method</span></span>  
* <span data-ttu-id="4b66c-141">Inicialización de un contenedor Request-Response</span><span class="sxs-lookup"><span data-stu-id="4b66c-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="4b66c-142">El nombre de cada blob tiene un prefijo con la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b66c-142">The name of each blob has a prefix of the following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="4b66c-143">Donde el _tipo de registro_ es uno de los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="4b66c-143">Where _Log type_ is one of the following values:</span></span>  

* <span data-ttu-id="4b66c-144">proceso por lotes</span><span class="sxs-lookup"><span data-stu-id="4b66c-144">batch</span></span>  
* <span data-ttu-id="4b66c-145">puntuación/solicitudes</span><span class="sxs-lookup"><span data-stu-id="4b66c-145">score/requests</span></span>  
* <span data-ttu-id="4b66c-146">puntuación/inic</span><span class="sxs-lookup"><span data-stu-id="4b66c-146">score/init</span></span>  

