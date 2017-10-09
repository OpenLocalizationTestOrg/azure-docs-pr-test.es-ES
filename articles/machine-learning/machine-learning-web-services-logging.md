---
title: "aaaLogging para servicios web de aprendizaje automático | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable el registro para el aprendizaje automático web services. El registro proporciona información adicional toohelp solucionar Hola API."
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
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="b4b17-104">Habilitar el registro para los servicios web de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="b4b17-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="b4b17-105">Este documento proporciona información sobre Hola registro capacidad de servicios web de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="b4b17-105">This document provides information on hello logging capability of Machine Learning web services.</span></span> <span data-ttu-id="b4b17-106">El registro proporciona información adicional, más allá de solo un número de error y un mensaje, que puede ayudarle a solucionar problemas de su toohello de llamadas API de aprendizaje de máquina.</span><span class="sxs-lookup"><span data-stu-id="b4b17-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls toohello Machine Learning APIs.</span></span>  

## <a name="how-tooenable-logging-for-a-web-service"></a><span data-ttu-id="b4b17-107">¿Cómo registro tooenable para un servicio Web</span><span class="sxs-lookup"><span data-stu-id="b4b17-107">How tooenable logging for a Web service</span></span>

<span data-ttu-id="b4b17-108">Para habilitar el registro de hello [servicios Web de Azure Machine Learning](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="b4b17-108">You enable logging from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="b4b17-109">Inicie sesión en el portal de servicios Web de Azure Machine Learning toohello en [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="b4b17-109">Sign in toohello Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="b4b17-110">Para un servicio web clásico, también puede obtener toohello portal, haga clic en **nueva experiencia de servicios Web** en la página de servicios Web de aprendizaje de máquina de hello en estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="b4b17-110">For a Classic web service, you can also get toohello portal by clicking **New Web Services Experience** on hello Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Nuevo vínculo a la experiencia de servicios web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="b4b17-112">En la barra de menús superior hello, haga clic en **servicios Web** para un nuevo servicio web o haga clic en **clásico servicios Web** para un clásico de servicio web.</span><span class="sxs-lookup"><span data-stu-id="b4b17-112">On hello top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Selección de servicios web nuevos o clásicos](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="b4b17-114">Para un nuevo servicio web, haga clic en el nombre del servicio web Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b17-114">For a New web service, click hello web service name.</span></span> <span data-ttu-id="b4b17-115">Para un servicio web clásico, haga clic en el nombre del servicio web hello y, a continuación, en la página siguiente de hello, haga clic en punto de conexión adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b17-115">For a Classic web service, click hello web service name and then on hello next page click hello appropriate endpoint.</span></span>

4. <span data-ttu-id="b4b17-116">En la barra de menús superior hello, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="b4b17-116">On hello top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="b4b17-117">Conjunto hello **Habilitar registro** opción demasiado*Error* (toolog solo errores) o *todos los* (para el registro completo).</span><span class="sxs-lookup"><span data-stu-id="b4b17-117">Set hello **Enable Logging** option too*Error* (toolog only errors) or *All* (for full logging).</span></span>

   ![Selección del nivel de registro](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="b4b17-119">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b4b17-119">Click **Save**.</span></span>

7. <span data-ttu-id="b4b17-120">Para los servicios web estándar, crear hello **ml diagnósticos** contenedor.</span><span class="sxs-lookup"><span data-stu-id="b4b17-120">For Classic web services, create hello **ml-diagnostics** container.</span></span>

   <span data-ttu-id="b4b17-121">Todos los registros del servicio web se conservan en un contenedor de blobs denominado **ml diagnósticos** en hello cuenta de almacenamiento asociada con el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b17-121">All web service logs are kept in a blob container named **ml-diagnostics** in hello storage account associated with hello web service.</span></span> <span data-ttu-id="b4b17-122">Para los nuevos servicios web, este contenedor se crea Hola primera vez que acceda a servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b17-122">For New web services, this container is created hello first time you access hello web service.</span></span> <span data-ttu-id="b4b17-123">Para los servicios web estándar, deberá contenedor de hello toocreate si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="b4b17-123">For Classic web services, you need toocreate hello container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="b4b17-124">Hola [portal de Azure](https://portal.azure.com), vaya toohello cuenta de almacenamiento asociada con el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b17-124">In hello [Azure portal](https://portal.azure.com), go toohello storage account associated with hello web service.</span></span>

   2. <span data-ttu-id="b4b17-125">En **Blob service**, haga clic en **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="b4b17-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="b4b17-126">Si el contenedor de hello **diagnósticos de aprendizaje automático** no existe, haga clic en **+ contenedor**, asigne Hola contenedor Hola nombre "ml-diagnostics" y seleccione hello **tipo de acceso** como "Blob".</span><span class="sxs-lookup"><span data-stu-id="b4b17-126">If hello container **ml-diagnostics** doesn't exist, click **+Container**, give hello container hello name "ml-diagnostics", and select hello **Access type** as "Blob".</span></span> <span data-ttu-id="b4b17-127">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b4b17-127">Click **OK**.</span></span>

      ![Selección del nivel de registro](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="b4b17-129">Para un servicio web clásico, Hola panel de servicios Web en estudio de aprendizaje automático también tiene un registro de tooenable de conmutador.</span><span class="sxs-lookup"><span data-stu-id="b4b17-129">For a Classic web service, hello Web Services Dashboard in Machine Learning Studio also has a switch tooenable logging.</span></span> <span data-ttu-id="b4b17-130">Sin embargo, dado que el registro ahora se administra a través del portal de servicios Web de hello, debe tooenable registro a través del portal de hello, tal como se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="b4b17-130">However, because logging is now managed through hello Web Services portal, you need tooenable logging through hello portal as described in this article.</span></span> <span data-ttu-id="b4b17-131">Si ha habilitado el registro en Studio, en el Portal de servicios Web de hello, deshabilitar el registro y vuelva a habilitarla.</span><span class="sxs-lookup"><span data-stu-id="b4b17-131">If you already enabled logging in Studio, then in hello Web Services Portal, disable logging and enable it again.</span></span>


## <a name="hello-effects-of-enabling-logging"></a><span data-ttu-id="b4b17-132">efectos de Hello habilitación del registro</span><span class="sxs-lookup"><span data-stu-id="b4b17-132">hello effects of enabling logging</span></span>
<span data-ttu-id="b4b17-133">Cuando se habilita el registro, diagnósticos de Hola y errores de extremo de servicio web de Hola se registran en hello **ml diagnósticos** contenedor de blobs en hello cuenta de almacenamiento de Azure vinculado con el área de trabajo del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b17-133">When logging is enabled, hello diagnostics and errors from hello web service endpoint are logged in hello **ml-diagnostics** blob container in hello Azure Storage Account linked with hello user’s workspace.</span></span> <span data-ttu-id="b4b17-134">Este contenedor contiene toda la información de diagnóstico de Hola para todos los extremos de servicio web de Hola para todas las áreas de trabajo de hello asociadas a esta cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b4b17-134">This container holds all hello diagnostics information for all hello web service endpoints for all hello workspaces associated with this storage account.</span></span>

<span data-ttu-id="b4b17-135">Hola registros pueden verse mediante cualquiera de hello tooexplore disponibles de varias herramientas una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b17-135">hello logs can be viewed using any of hello several tools available tooexplore an Azure Storage Account.</span></span> <span data-ttu-id="b4b17-136">Hola más sencilla puede ser toonavigate toohello cuenta de almacenamiento en hello portal de Azure, haga clic en **contenedores**y, a continuación, haga clic en el contenedor de hello **ml diagnósticos**.</span><span class="sxs-lookup"><span data-stu-id="b4b17-136">hello easiest may be toonavigate toohello storage account in hello Azure portal, click **Containers**, and then click hello container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="b4b17-137">Información detallada sobre el blob de registro</span><span class="sxs-lookup"><span data-stu-id="b4b17-137">Log blob detail information</span></span>
<span data-ttu-id="b4b17-138">Cada blob en contenedor de hello contiene información de diagnóstico de Hola para exactamente uno de hello siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="b4b17-138">Each blob in hello container holds hello diagnostics information for exactly one of hello following actions:</span></span>

* <span data-ttu-id="b4b17-139">Una ejecución del método hello ejecución por lotes</span><span class="sxs-lookup"><span data-stu-id="b4b17-139">An execution of hello Batch-Execution method</span></span>  
* <span data-ttu-id="b4b17-140">Una ejecución del método hello solicitudes y respuestas</span><span class="sxs-lookup"><span data-stu-id="b4b17-140">An execution of hello Request-Response method</span></span>  
* <span data-ttu-id="b4b17-141">Inicialización de un contenedor Request-Response</span><span class="sxs-lookup"><span data-stu-id="b4b17-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="b4b17-142">nombre de Hola de cada blob tiene un prefijo de hello siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="b4b17-142">hello name of each blob has a prefix of hello following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="b4b17-143">Donde _tipo de registro_ es uno de hello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="b4b17-143">Where _Log type_ is one of hello following values:</span></span>  

* <span data-ttu-id="b4b17-144">proceso por lotes</span><span class="sxs-lookup"><span data-stu-id="b4b17-144">batch</span></span>  
* <span data-ttu-id="b4b17-145">puntuación/solicitudes</span><span class="sxs-lookup"><span data-stu-id="b4b17-145">score/requests</span></span>  
* <span data-ttu-id="b4b17-146">puntuación/inic</span><span class="sxs-lookup"><span data-stu-id="b4b17-146">score/init</span></span>  

