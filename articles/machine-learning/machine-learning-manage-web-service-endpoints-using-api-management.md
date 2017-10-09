---
title: "aaaLearn cómo utiliza la API de administración de servicios de toomanage web de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Una guía que muestra cómo utiliza la API de administración de servicios de toomanage web de aprendizaje automático de Azure."
keywords: "aprendizaje automático, administración de api"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a><span data-ttu-id="6c8b1-104">Obtenga información acerca de cómo utiliza la API de administración de servicios de toomanage web de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="6c8b1-104">Learn how toomanage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="6c8b1-105">Información general</span><span class="sxs-lookup"><span data-stu-id="6c8b1-105">Overview</span></span>
<span data-ttu-id="6c8b1-106">Esta guía le mostrará cómo tooquickly Introducción al uso de administración de API toomanage los servicios web de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-106">This guide shows you how tooquickly get started using API Management toomanage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="6c8b1-107">¿Qué es la Administración de API de Azure?</span><span class="sxs-lookup"><span data-stu-id="6c8b1-107">What is Azure API Management?</span></span>
<span data-ttu-id="6c8b1-108">Administración de API de Azure es un servicio de Azure que le permite administrar los extremos de la API de REST al definir el acceso del usuario, el límite de uso y la supervisión de panel.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="6c8b1-109">Haga clic [aquí](https://azure.microsoft.com/services/api-management/) para obtener más información sobre Administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="6c8b1-110">Haga clic en [aquí](../api-management/api-management-get-started.md) para obtener una guía sobre cómo tooget comenzar con la administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-110">Click [here](../api-management/api-management-get-started.md) for a guide on how tooget started with Azure API Management.</span></span> <span data-ttu-id="6c8b1-111">Esta otra guía, en la que está basada esta guía, aborda más temas, incluidos las configuraciones de notificación, el nivel de precios, el control de respuestas, la autenticación de los usuarios, la creación de productos, las suscripciones de desarrollador y los paneles de uso.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="6c8b1-112">¿Qué es AzureML?</span><span class="sxs-lookup"><span data-stu-id="6c8b1-112">What is AzureML?</span></span>
<span data-ttu-id="6c8b1-113">Aprendizaje automático de Azure es un servicio de Azure para el aprendizaje automático que permite la compilación tooeasily, implementar y compartir las soluciones de análisis avanzado.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-113">AzureML is an Azure service for machine learning that enables you tooeasily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="6c8b1-114">Haga clic en [aquí](https://azure.microsoft.com/services/machine-learning/) para obtener información detallada sobre AzureML.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c8b1-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6c8b1-115">Prerequisites</span></span>
<span data-ttu-id="6c8b1-116">toocomplete esta guía, debe:</span><span class="sxs-lookup"><span data-stu-id="6c8b1-116">toocomplete this guide, you need:</span></span>

* <span data-ttu-id="6c8b1-117">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-117">An Azure account.</span></span> <span data-ttu-id="6c8b1-118">Si no tienes una cuenta de Azure, haga clic en [aquí](https://azure.microsoft.com/pricing/free-trial/) para obtener más información acerca de cómo toocreate una cuenta de prueba gratuita.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="6c8b1-119">Una cuenta de AzureML.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-119">An AzureML account.</span></span> <span data-ttu-id="6c8b1-120">Si no tiene una cuenta de aprendizaje automático de Azure, haga clic en [aquí](https://studio.azureml.net/) para obtener más información acerca de cómo toocreate una cuenta de prueba gratuita.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="6c8b1-121">área de trabajo de Hello, el servicio y api_key para un experimento de aprendizaje automático de Azure que se implementa como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-121">hello workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="6c8b1-122">Haga clic en [aquí](machine-learning-create-experiment.md) para obtener más información sobre cómo probar toocreate un aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-122">Click [here](machine-learning-create-experiment.md) for details on how toocreate an AzureML experiment.</span></span> <span data-ttu-id="6c8b1-123">Haga clic en [aquí](machine-learning-publish-a-machine-learning-web-service.md) para obtener más información sobre cómo probar toodeploy un aprendizaje automático de Azure como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how toodeploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="6c8b1-124">Como alternativa, el apéndice A contiene instrucciones para toocreate y probar un aprendizaje automático de Azure simple experimentación e implementación como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-124">Alternately, Appendix A has instructions for how toocreate and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="6c8b1-125">Creación de una instancia de Administración de API</span><span class="sxs-lookup"><span data-stu-id="6c8b1-125">Create an API Management instance</span></span>
<span data-ttu-id="6c8b1-126">A continuación se muestran los pasos de hello para el uso de administración de API toomanage el servicio web de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-126">Below are hello steps for using API Management toomanage your AzureML web service.</span></span> <span data-ttu-id="6c8b1-127">En primer lugar, cree una instancia del servicio.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-127">First create a service instance.</span></span> <span data-ttu-id="6c8b1-128">Inicie sesión en toohello [Portal clásico](https://manage.windowsazure.com/) y haga clic en **New** > **servicios de aplicaciones** > **administración de API**  >  **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-128">Log in toohello [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="6c8b1-130">Especifique una **dirección URL**única.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-130">Specify a unique **URL**.</span></span> <span data-ttu-id="6c8b1-131">Esta guía se usan **demoazureml** – debe toochoose algo diferente.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-131">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="6c8b1-132">Elija Hola deseado **suscripción** y **región** para la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-132">Choose hello desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="6c8b1-133">Después de realizar las selecciones, haga clic en el botón siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-133">After making your selections, click hello next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="6c8b1-135">Especifique un valor para hello **nombreDeOrganización**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-135">Specify a value for hello **Organization Name**.</span></span> <span data-ttu-id="6c8b1-136">Esta guía se usan **demoazureml** – debe toochoose algo diferente.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-136">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="6c8b1-137">Escriba su dirección de correo electrónico en hello **correo electrónico del administrador** campo.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-137">Enter your email address in hello **administrator e-mail** field.</span></span> <span data-ttu-id="6c8b1-138">Esta dirección de correo electrónico se usa para recibir notificaciones del sistema de administración de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-138">This email address is used for notifications from hello API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="6c8b1-140">Haga clic en hello casilla toocreate su instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-140">Click hello check box toocreate your service instance.</span></span> <span data-ttu-id="6c8b1-141">*Ocupe toothirty minutos para una nueva toobe de servicio creado*.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-141">*It takes up toothirty minutes for a new service toobe created*.</span></span>

## <a name="create-hello-api"></a><span data-ttu-id="6c8b1-142">Crear API Hola</span><span class="sxs-lookup"><span data-stu-id="6c8b1-142">Create hello API</span></span>
<span data-ttu-id="6c8b1-143">Una vez creada la instancia de servicio de hello, Hola siguiente paso es toocreate Hola API.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-143">Once hello service instance is created, hello next step is toocreate hello API.</span></span> <span data-ttu-id="6c8b1-144">Una API consta de un conjunto de operaciones que se pueden invocar desde una aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="6c8b1-145">Las operaciones de API son servicios de tooexisting procesadas por el proxy web.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-145">API operations are proxied tooexisting web services.</span></span> <span data-ttu-id="6c8b1-146">Esta guía crea las API que toohello proxy AzureML RRS y BES servicios web existentes.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-146">This guide creates APIs that proxy toohello existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="6c8b1-147">Las API se crean y configuran desde el portal para desarrolladores de API hello, que se obtiene acceso a través de hello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-147">APIs are created and configured from hello API publisher portal, which is accessed through hello Azure Classic Portal.</span></span> <span data-ttu-id="6c8b1-148">tooreach Hola seleccione portal, publicador de la instancia del servicio.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-148">tooreach hello publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="6c8b1-150">Haga clic en **administrar** Hola Portal clásico de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-150">Click **Manage** in hello Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="6c8b1-152">Haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **agregar API**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-152">Click **APIs** from hello **API Management** menu on hello left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="6c8b1-154">Tipo de **API de demostración de aprendizaje automático de Azure** como hello **nombre de la API de Web**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-154">Type **AzureML Demo API** as hello **Web API name**.</span></span> <span data-ttu-id="6c8b1-155">Tipo de **https://ussouthcentral.services.azureml.net** como hello **dirección URL del servicio Web**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-155">Type **https://ussouthcentral.services.azureml.net** as hello **Web service URL**.</span></span> <span data-ttu-id="6c8b1-156">Tipo de **azureml-demo** como hello **sufijo de URL de la API de Web**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-156">Type **azureml-demo** as hello **Web API URL suffix**.</span></span> <span data-ttu-id="6c8b1-157">Comprobar **HTTPS** como hello **URL de la API de Web** esquema.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-157">Check **HTTPS** as hello **Web API URL** scheme.</span></span> <span data-ttu-id="6c8b1-158">Seleccione **Starter** en **Productos**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="6c8b1-159">Cuando termine, haga clic en **guardar** toocreate Hola API.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-159">When finished, click **Save** toocreate hello API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a><span data-ttu-id="6c8b1-161">Las operaciones de Hola para agregar</span><span class="sxs-lookup"><span data-stu-id="6c8b1-161">Add hello operations</span></span>
<span data-ttu-id="6c8b1-162">Haga clic en **Agregar operación** tooadd operations toothis API.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-162">Click **Add operation** tooadd operations toothis API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="6c8b1-164">Hola **nueva operación** ventana se mostrarán y Hola **firma** ficha se seleccionará de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-164">hello **New operation** window will be displayed and hello **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="6c8b1-165">Adición de una operación de registro de recursos</span><span class="sxs-lookup"><span data-stu-id="6c8b1-165">Add RRS Operation</span></span>
<span data-ttu-id="6c8b1-166">Cree primero una operación de servicio de AzureML RRS Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-166">First create an operation for hello AzureML RRS service.</span></span> <span data-ttu-id="6c8b1-167">Seleccione **POST** como hello **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-167">Select **POST** as hello **HTTP verb**.</span></span> <span data-ttu-id="6c8b1-168">Tipo de **/workspaces/ {área de} trabajo {servicio} / ejecutar? api-version = {valor apiversion} & detalles = {detalles}** como hello **plantilla de dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as hello **URL template**.</span></span> <span data-ttu-id="6c8b1-169">Tipo de **ejecutar RR** como hello **nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-169">Type **RRS Execute** as hello **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="6c8b1-171">Haga clic en **respuestas** > **agregar** en hello izquierdo y seleccione **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-171">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="6c8b1-172">Haga clic en **guardar** toosave esta operación.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-172">Click **Save** toosave this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="6c8b1-174">Adición de operaciones BES</span><span class="sxs-lookup"><span data-stu-id="6c8b1-174">Add BES Operations</span></span>
<span data-ttu-id="6c8b1-175">No se incluyen con fines capturas de pantalla Hola operaciones BES tal como están toothose muy similar para agregar la operación de Hola RR.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-175">Screenshots are not included for hello BES operations as they are very similar toothose for adding hello RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="6c8b1-176">Envío (pero no inicio) de un trabajo de ejecución por lotes</span><span class="sxs-lookup"><span data-stu-id="6c8b1-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="6c8b1-177">Haga clic en **Agregar operación** tooadd Hola BES de aprendizaje automático de Azure operación toohello API.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-177">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="6c8b1-178">Seleccione **POST** para hello **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-178">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="6c8b1-179">Tipo de **/workspaces/ {área de} trabajo {servicio} / trabajos? api-version = {valor apiversion}** para hello **plantilla de dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="6c8b1-180">Tipo de **BES enviar** para hello **nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-180">Type **BES Submit** for hello **Display name**.</span></span> <span data-ttu-id="6c8b1-181">Haga clic en **respuestas** > **agregar** en hello izquierdo y seleccione **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-181">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="6c8b1-182">Haga clic en **guardar** toosave esta operación.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-182">Click **Save** toosave this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="6c8b1-183">Inicio de un trabajo de ejecución por lotes</span><span class="sxs-lookup"><span data-stu-id="6c8b1-183">Start a Batch Execution job</span></span>
<span data-ttu-id="6c8b1-184">Haga clic en **Agregar operación** tooadd Hola BES de aprendizaje automático de Azure operación toohello API.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-184">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="6c8b1-185">Seleccione **POST** para hello **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-185">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="6c8b1-186">Tipo de **/workspaces/ {área de} trabajo {servicio} /jobs/ {jobid} / iniciar? api-version = {valor apiversion}** para hello **plantilla de dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="6c8b1-187">Tipo de **BES iniciar** para hello **nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-187">Type **BES Start** for hello **Display name**.</span></span> <span data-ttu-id="6c8b1-188">Haga clic en **respuestas** > **agregar** en hello izquierdo y seleccione **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-188">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="6c8b1-189">Haga clic en **guardar** toosave esta operación.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-189">Click **Save** toosave this operation.</span></span>

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="6c8b1-190">Obtener estado de Hola o el resultado de un trabajo de ejecución por lotes</span><span class="sxs-lookup"><span data-stu-id="6c8b1-190">Get hello status or result of a Batch Execution job</span></span>
<span data-ttu-id="6c8b1-191">Haga clic en **Agregar operación** tooadd Hola BES de aprendizaje automático de Azure operación toohello API.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-191">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="6c8b1-192">Seleccione **obtener** para hello **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-192">Select **GET** for hello **HTTP verb**.</span></span> <span data-ttu-id="6c8b1-193">Tipo de **/workspaces/ {área de} trabajo {servicio} /jobs/ {jobid}? api-version = {valor apiversion}** para hello **plantilla de dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="6c8b1-194">Tipo de **estado BES** para hello **nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-194">Type **BES Status** for hello **Display name**.</span></span> <span data-ttu-id="6c8b1-195">Haga clic en **respuestas** > **agregar** en hello izquierdo y seleccione **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-195">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="6c8b1-196">Haga clic en **guardar** toosave esta operación.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-196">Click **Save** toosave this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="6c8b1-197">Eliminación de un trabajo de ejecución por lotes</span><span class="sxs-lookup"><span data-stu-id="6c8b1-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="6c8b1-198">Haga clic en **Agregar operación** tooadd Hola BES de aprendizaje automático de Azure operación toohello API.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-198">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="6c8b1-199">Seleccione **eliminar** para hello **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-199">Select **DELETE** for hello **HTTP verb**.</span></span> <span data-ttu-id="6c8b1-200">Tipo de **/workspaces/ {área de} trabajo {servicio} /jobs/ {jobid}? api-version = {valor apiversion}** para hello **plantilla de dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="6c8b1-201">Tipo de **BES eliminar** para hello **nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-201">Type **BES Delete** for hello **Display name**.</span></span> <span data-ttu-id="6c8b1-202">Haga clic en **respuestas** > **agregar** en hello izquierdo y seleccione **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-202">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="6c8b1-203">Haga clic en **guardar** toosave esta operación.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-203">Click **Save** toosave this operation.</span></span>

## <a name="call-an-operation-from-hello-developer-portal"></a><span data-ttu-id="6c8b1-204">Llamar a una operación de hello Portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="6c8b1-204">Call an operation from hello Developer Portal</span></span>
<span data-ttu-id="6c8b1-205">Las operaciones pueden llamarse directamente desde el portal para desarrolladores de hello, que proporciona una manera cómoda de tooview y pruebe las operaciones de Hola de una API.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-205">Operations can be called directly from hello Developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="6c8b1-206">En este paso de la guía llamará Hola **ejecutar RR** método que se agregó toohello **API de aprendizaje automático de Azure demostración**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-206">In this guide step you will call hello **RRS Execute** method that was added toohello **AzureML Demo API**.</span></span> <span data-ttu-id="6c8b1-207">Haga clic en **portal para desarrolladores de** desde el menú de Hola Hola parte superior derecha de hello Portal clásico.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-207">Click **Developer portal** from hello menu at hello top right of hello Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="6c8b1-209">Haga clic en **API** desde el menú superior de hello y, a continuación, haga clic en **API de demostración de aprendizaje automático de Azure** operaciones de hello toosee disponibles.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-209">Click **APIs** from hello top menu, and then click **AzureML Demo API** toosee hello operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="6c8b1-211">Seleccione **RR ejecutar** para la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-211">Select **RRS Execute** for hello operation.</span></span> <span data-ttu-id="6c8b1-212">Haga clic en **Pruébelo**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-212">Click **Try It**.</span></span>

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="6c8b1-214">Para los parámetros de solicitud, escriba su **área de trabajo**, **servicio**, **2.0** para hello **el elemento apiversion**, y **true**para hello **detalles**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-214">For Request parameters, type your **workspace**,  **service**, **2.0** for hello **apiversion**, and  **true** for hello **details**.</span></span> <span data-ttu-id="6c8b1-215">Puede encontrar el **área de trabajo** y **servicio** en panel de servicio de web de aprendizaje automático de Azure de hello (vea **probar hello web servicio** en el apéndice A).</span><span class="sxs-lookup"><span data-stu-id="6c8b1-215">You can find your **workspace** and **service** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="6c8b1-216">Para los encabezados de solicitud, haga clic en **Agregar encabezado** y escriba **Content-Type** y **application/json**, después haga clic en **Agregar encabezado** y escriba **Autorización** y **Portador <YOUR AZUREML SERVICE API-KEY>**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="6c8b1-217">Puede encontrar el **clave de api** en panel de servicio de web de aprendizaje automático de Azure de hello (vea **probar hello web servicio** en el apéndice A).</span><span class="sxs-lookup"><span data-stu-id="6c8b1-217">You can find your **api key** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="6c8b1-218">Tipo de **{"Entradas": {"Entrada1": {"ColumnNames": "Valores" ["Col2"]: [["Esto es un buen día"]]}}, "GlobalParameters": {}}** Hola cuerpo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for hello request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="6c8b1-220">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-220">Click **Send**.</span></span>

![Enviar](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="6c8b1-222">Después de invoca una operación, el portal para desarrolladores de hello muestra hello **dirección URL solicitada** de servicio de back-end de hello, Hola **estado de respuesta**, hello **encabezados de respuesta**, y cualquier **contenido de la respuesta**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-222">After an operation is invoked, hello developer portal displays hello **Requested URL** from hello back-end service, hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="6c8b1-224">Apéndice A: Creación y prueba de un servicio web sencillo de AzureML</span><span class="sxs-lookup"><span data-stu-id="6c8b1-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-hello-experiment"></a><span data-ttu-id="6c8b1-225">Crear experimento Hola</span><span class="sxs-lookup"><span data-stu-id="6c8b1-225">Creating hello experiment</span></span>
<span data-ttu-id="6c8b1-226">A continuación se muestran los pasos de Hola para crear un experimento de aprendizaje automático de Azure sencillo e implementar como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-226">Below are hello steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="6c8b1-227">Hola web servicio toma como entrada una columna de texto arbitrario y devuelve un conjunto de características representadas como enteros.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-227">hello web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="6c8b1-228">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6c8b1-228">For example:</span></span>

| <span data-ttu-id="6c8b1-229">Texto</span><span class="sxs-lookup"><span data-stu-id="6c8b1-229">Text</span></span> | <span data-ttu-id="6c8b1-230">Texto con hash</span><span class="sxs-lookup"><span data-stu-id="6c8b1-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="6c8b1-231">Este es un buen día</span><span class="sxs-lookup"><span data-stu-id="6c8b1-231">This is a good day</span></span> |<span data-ttu-id="6c8b1-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="6c8b1-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="6c8b1-233">En primer lugar, mediante un explorador de su elección, navegue hasta: [https://studio.azureml.net/](https://studio.azureml.net/) y escriba su toolog de credenciales en.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials toolog in.</span></span> <span data-ttu-id="6c8b1-234">Después, cree un nuevo experimento en blanco.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="6c8b1-236">Cambiar el nombre demasiado**SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-236">Rename it too**SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="6c8b1-237">Expanda **Conjuntos de datos guardados** y arrastre **Reseñas de libros de Amazon** al experimento.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="6c8b1-239">Expanda **Transformación de datos** y **Manipulación** y arrastre **Seleccionar columnas de conjunto de datos** al experimento.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="6c8b1-240">Conectar **reseñas de libros de Amazon** demasiado**seleccionar columnas de conjunto de datos**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-240">Connect **Book Reviews from Amazon** too**Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="6c8b1-242">Haga clic en **Seleccionar columnas de conjunto de datos** y después haga clic en **Iniciar el selector de columnas** y seleccione **Col2**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="6c8b1-243">Haga clic en tooapply de marca de verificación de hello estos cambios.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-243">Click hello checkmark tooapply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="6c8b1-245">Expanda **análisis de texto** y arrastre **hash de características** en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-245">Expand **Text Analytics** and drag **Feature Hashing** onto hello experiment.</span></span> <span data-ttu-id="6c8b1-246">Conectar **seleccionar columnas de conjunto de datos** demasiado**hash de características**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-246">Connect **Select Columns in Dataset** too**Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="6c8b1-248">Tipo de **3** para hello **hash de tamaño de bits**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-248">Type **3** for hello **Hashing bitsize**.</span></span> <span data-ttu-id="6c8b1-249">Se crearán 8 (23) columnas.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="6c8b1-251">En este momento, puede que desee tooclick **ejecutar** experimento de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-251">At this point, you may want tooclick **Run** tootest hello experiment.</span></span>

![Ejecutar](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="6c8b1-253">Creación de un servicio web</span><span class="sxs-lookup"><span data-stu-id="6c8b1-253">Create a web service</span></span>
<span data-ttu-id="6c8b1-254">Ahora va a crear un servicio web.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-254">Now create a web service.</span></span> <span data-ttu-id="6c8b1-255">Expanda **Servicio web** y arrastre **Entrada** al experimento.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="6c8b1-256">Conectar **entrada** demasiado**hash de características**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-256">Connect **Input** too**Feature Hashing**.</span></span> <span data-ttu-id="6c8b1-257">Arrastre también **Resultado** al experimento.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="6c8b1-258">Conectar **salida** demasiado**hash de características**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-258">Connect **Output** too**Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="6c8b1-260">Haga clic en **Publicar servicio web**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="6c8b1-262">Haga clic en **Sí** experimento de hello toopublish.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-262">Click **Yes** toopublish hello experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a><span data-ttu-id="6c8b1-264">Servicio web de Hola de prueba</span><span class="sxs-lookup"><span data-stu-id="6c8b1-264">Test hello web service</span></span>
<span data-ttu-id="6c8b1-265">Un servicio web de AzureML consta de los extremos RRS (servicio de solicitud/respuesta) y BES (servicio de ejecución por lotes).</span><span class="sxs-lookup"><span data-stu-id="6c8b1-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="6c8b1-266">RRS sirve para la ejecución sincrónica.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="6c8b1-267">BES sirve para la ejecución por lotes asincrónica.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="6c8b1-268">tootest su sitio web de servicio con el origen de Python de ejemplo de Hola a continuación, quizás necesite toodownload y Hola instalar Azure SDK para Python (Véase: [cómo tooinstall Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="6c8b1-268">tootest your web service with hello sample Python source below, you may need toodownload and install hello Azure SDK for Python (see: [How tooinstall Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="6c8b1-269">También necesitará hello **área de trabajo**, **servicio**, y **api_key** de su experimento para el origen de ejemplo de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-269">You will also need hello **workspace**, **service**, and **api_key** of your experiment for hello sample source below.</span></span> <span data-ttu-id="6c8b1-270">Puede encontrar el área de trabajo de Hola y el servicio haciendo clic en **solicitud/respuesta** o **ejecución por lotes** para el experimento en el panel del servicio web Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-270">You can find hello workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in hello web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="6c8b1-272">Puede encontrar Hola **api_key** haciendo clic en el experimento en el panel del servicio web Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-272">You can find hello **api_key** by clicking your experiment in hello web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="6c8b1-274">Prueba del extremo RRS</span><span class="sxs-lookup"><span data-stu-id="6c8b1-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="6c8b1-275">Botón Probar</span><span class="sxs-lookup"><span data-stu-id="6c8b1-275">Test button</span></span>
<span data-ttu-id="6c8b1-276">Un punto de conexión de manera sencilla tootest Hola RR es tooclick **prueba** en el panel del servicio web Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-276">An easy way tootest hello RRS endpoint is tooclick **Test** on hello web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="6c8b1-278">Escriba **Este es un buen día** para **col2**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="6c8b1-279">Haga clic en la marca de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-279">Click hello checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="6c8b1-281">Verá algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c8b1-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="6c8b1-283">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6c8b1-283">Sample Code</span></span>
<span data-ttu-id="6c8b1-284">Tootest de otra manera el RR es desde el código de cliente.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-284">Another way tootest your RRS is from your client code.</span></span> <span data-ttu-id="6c8b1-285">Si hace clic en **solicitud/respuesta** en hello panel y desplácese toohello parte inferior, verá el código de ejemplo para C#, Python y R. También verá sintaxis Hola de Hola RR solicitud, incluidos los URI de solicitud de hello, encabezados y cuerpo.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-285">If you click **Request/response** on hello dashboard and scroll toohello bottom, you will see sample code for C#, Python, and R. You will also see hello syntax of hello RRS request, including hello request URI, headers, and body.</span></span>

<span data-ttu-id="6c8b1-286">Esta guía muestra un ejemplo de Python en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-286">This guide shows a working Python example.</span></span> <span data-ttu-id="6c8b1-287">Deberá toomodify con hello **área de trabajo**, **servicio**, y **api_key** de su experimento.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-287">You will need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span>

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="6c8b1-288">Prueba de extremo BES</span><span class="sxs-lookup"><span data-stu-id="6c8b1-288">Test BES endpoint</span></span>
<span data-ttu-id="6c8b1-289">Haga clic en **ejecución por lotes** en hello panel y desplazamiento toohello inferior.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-289">Click **Batch execution** on hello dashboard and scroll toohello bottom.</span></span> <span data-ttu-id="6c8b1-290">Verá el código de ejemplo de C#, Python y R. También verá sintaxis Hola de Hola BES solicitudes toosubmit un trabajo, iniciar un trabajo, obtener el estado de Hola o los resultados de un trabajo y eliminar un trabajo.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-290">You will see sample code for C#, Python, and R. You will also see hello syntax of hello BES requests toosubmit a job, start a job, get hello status or results of a job, and delete a job.</span></span>

<span data-ttu-id="6c8b1-291">Esta guía muestra un ejemplo de Python en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-291">This guide shows a working Python example.</span></span> <span data-ttu-id="6c8b1-292">Necesita toomodify con hello **área de trabajo**, **servicio**, y **api_key** de su experimento.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-292">You need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="6c8b1-293">Además, es necesario hello toomodify **nombre de la cuenta de almacenamiento**, **clave de la cuenta de almacenamiento**, y **el nombre del contenedor de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-293">Additionally, you need toomodify hello **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="6c8b1-294">Por último, necesitará la ubicación de hello toomodify de hello **archivo de entrada** y la ubicación de Hola de hello **archivo de salida**.</span><span class="sxs-lookup"><span data-stu-id="6c8b1-294">Lastly, you will need toomodify hello location of hello **input file** and hello location of hello **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
