---
title: Aprenda a administrar los servicios web de AzureML mediante API Management | Microsoft Docs
description: "Una guía que muestra cómo administrar los servicios web de AzureML mediante la Administración de API."
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
ms.openlocfilehash: 65eff3f4971f79886a840bb19bf76aaab48878de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a><span data-ttu-id="22a60-104">Aprenda a administrar los servicios de web de AzureML mediante la Administración de API</span><span class="sxs-lookup"><span data-stu-id="22a60-104">Learn how to manage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="22a60-105">Información general</span><span class="sxs-lookup"><span data-stu-id="22a60-105">Overview</span></span>
<span data-ttu-id="22a60-106">En esta guía se muestra cómo empezar a usar rápidamente la Administración de API para administrar los servicios web de AzureML.</span><span class="sxs-lookup"><span data-stu-id="22a60-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="22a60-107">¿Qué es la Administración de API de Azure?</span><span class="sxs-lookup"><span data-stu-id="22a60-107">What is Azure API Management?</span></span>
<span data-ttu-id="22a60-108">Administración de API de Azure es un servicio de Azure que le permite administrar los extremos de la API de REST al definir el acceso del usuario, el límite de uso y la supervisión de panel.</span><span class="sxs-lookup"><span data-stu-id="22a60-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="22a60-109">Haga clic [aquí](https://azure.microsoft.com/services/api-management/) para obtener más información sobre Administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="22a60-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="22a60-110">Haga clic [aquí](../api-management/api-management-get-started.md) para obtener una guía sobre cómo empezar a trabajar con Administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="22a60-110">Click [here](../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span></span> <span data-ttu-id="22a60-111">Esta otra guía, en la que está basada esta guía, aborda más temas, incluidos las configuraciones de notificación, el nivel de precios, el control de respuestas, la autenticación de los usuarios, la creación de productos, las suscripciones de desarrollador y los paneles de uso.</span><span class="sxs-lookup"><span data-stu-id="22a60-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="22a60-112">¿Qué es AzureML?</span><span class="sxs-lookup"><span data-stu-id="22a60-112">What is AzureML?</span></span>
<span data-ttu-id="22a60-113">AzureML es un servicio de Azure para el aprendizaje automático que permite crear, implementar y compartir fácilmente las soluciones de análisis avanzado.</span><span class="sxs-lookup"><span data-stu-id="22a60-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="22a60-114">Haga clic en [aquí](https://azure.microsoft.com/services/machine-learning/) para obtener información detallada sobre AzureML.</span><span class="sxs-lookup"><span data-stu-id="22a60-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22a60-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="22a60-115">Prerequisites</span></span>
<span data-ttu-id="22a60-116">Para completar a esta guía, necesita:</span><span class="sxs-lookup"><span data-stu-id="22a60-116">To complete this guide, you need:</span></span>

* <span data-ttu-id="22a60-117">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="22a60-117">An Azure account.</span></span> <span data-ttu-id="22a60-118">Si no tiene una cuenta de Azure, haga clic [aquí](https://azure.microsoft.com/pricing/free-trial/) para obtener más información sobre cómo crear una cuenta de evaluación gratuita.</span><span class="sxs-lookup"><span data-stu-id="22a60-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="22a60-119">Una cuenta de AzureML.</span><span class="sxs-lookup"><span data-stu-id="22a60-119">An AzureML account.</span></span> <span data-ttu-id="22a60-120">Si no dispone de una cuenta de Aprendizaje automático de Azure, haga clic [aquí](https://studio.azureml.net/) para obtener más información sobre cómo crear una cuenta de evaluación gratuita.</span><span class="sxs-lookup"><span data-stu-id="22a60-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="22a60-121">El área de trabajo, el servicio y la api_key para un experimento de Aprendizaje automático de Azure implementado como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="22a60-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="22a60-122">Haga clic [aquí](machine-learning-create-experiment.md) para obtener más información sobre cómo crear un experimento de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="22a60-122">Click [here](machine-learning-create-experiment.md) for details on how to create an AzureML experiment.</span></span> <span data-ttu-id="22a60-123">Haga clic [aquí](machine-learning-publish-a-machine-learning-web-service.md) para obtener más información sobre cómo implementar un experimento de Aprendizaje automático de Azure como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="22a60-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="22a60-124">Además, el Apéndice A contiene instrucciones sobre cómo crear y probar un experimento de Aprendizaje automático de Azure sencillo e implementarlo como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="22a60-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="22a60-125">Creación de una instancia de Administración de API</span><span class="sxs-lookup"><span data-stu-id="22a60-125">Create an API Management instance</span></span>
<span data-ttu-id="22a60-126">A continuación se muestran los pasos para usar Administración de API para administrar el servicio web de AzureML.</span><span class="sxs-lookup"><span data-stu-id="22a60-126">Below are the steps for using API Management to manage your AzureML web service.</span></span> <span data-ttu-id="22a60-127">En primer lugar, cree una instancia del servicio.</span><span class="sxs-lookup"><span data-stu-id="22a60-127">First create a service instance.</span></span> <span data-ttu-id="22a60-128">Inicie sesión en [Portal clásico](https://manage.windowsazure.com/) y haga clic en **Nuevo** > **App Services** > **API Management** > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="22a60-128">Log in to the [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="22a60-130">Especifique una **dirección URL**única.</span><span class="sxs-lookup"><span data-stu-id="22a60-130">Specify a unique **URL**.</span></span> <span data-ttu-id="22a60-131">Esta guía usa **demoazureml** , por lo que deberá elegir algo diferente.</span><span class="sxs-lookup"><span data-stu-id="22a60-131">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="22a60-132">Elija la **suscripción** y la **región** deseadas para la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="22a60-132">Choose the desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="22a60-133">Después de realizar las selecciones pertinentes, haga clic en el botón Siguiente.</span><span class="sxs-lookup"><span data-stu-id="22a60-133">After making your selections, click the next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="22a60-135">Especifique un valor para **Nombre de la organización**.</span><span class="sxs-lookup"><span data-stu-id="22a60-135">Specify a value for the **Organization Name**.</span></span> <span data-ttu-id="22a60-136">Esta guía usa **demoazureml** , por lo que deberá elegir algo diferente.</span><span class="sxs-lookup"><span data-stu-id="22a60-136">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="22a60-137">Escriba su dirección de correo electrónico en el campo **correo electrónico del administrador** .</span><span class="sxs-lookup"><span data-stu-id="22a60-137">Enter your email address in the **administrator e-mail** field.</span></span> <span data-ttu-id="22a60-138">Esta dirección de correo electrónico se utiliza para notificaciones por parte del sistema Administración de API.</span><span class="sxs-lookup"><span data-stu-id="22a60-138">This email address is used for notifications from the API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="22a60-140">Haga clic en la casilla para crear su instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="22a60-140">Click the check box to create your service instance.</span></span> <span data-ttu-id="22a60-141">*Tarda hasta treinta minutos en crear un nuevo servicio*.</span><span class="sxs-lookup"><span data-stu-id="22a60-141">*It takes up to thirty minutes for a new service to be created*.</span></span>

## <a name="create-the-api"></a><span data-ttu-id="22a60-142">Creación de la API</span><span class="sxs-lookup"><span data-stu-id="22a60-142">Create the API</span></span>
<span data-ttu-id="22a60-143">Una vez creada la instancia de servicio, el paso siguiente es crear la API.</span><span class="sxs-lookup"><span data-stu-id="22a60-143">Once the service instance is created, the next step is to create the API.</span></span> <span data-ttu-id="22a60-144">Una API consta de un conjunto de operaciones que se pueden invocar desde una aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="22a60-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="22a60-145">Las operaciones API se realizan con proxy en servicios web existentes.</span><span class="sxs-lookup"><span data-stu-id="22a60-145">API operations are proxied to existing web services.</span></span> <span data-ttu-id="22a60-146">Esta guía crea las API que representan los servicios web de AzureML RRS y BES existentes.</span><span class="sxs-lookup"><span data-stu-id="22a60-146">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="22a60-147">Las API se crean y se configuran desde el portal para editores de API, al que se obtiene acceso a través del Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="22a60-147">APIs are created and configured from the API publisher portal, which is accessed through the Azure Classic Portal.</span></span> <span data-ttu-id="22a60-148">Para ponerse en contacto con el portal para editores, seleccione la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="22a60-148">To reach the publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="22a60-150">Haga clic en **Administrar** en el Portal de Azure clásico en el servicio de Administración de la API.</span><span class="sxs-lookup"><span data-stu-id="22a60-150">Click **Manage** in the Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="22a60-152">Haga clic en **API** en el menú **API Management** de la izquierda y haga clic en **Agregar API**.</span><span class="sxs-lookup"><span data-stu-id="22a60-152">Click **APIs** from the **API Management** menu on the left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="22a60-154">Escriba **API de demostración de AzureML** como el **nombre de API web**.</span><span class="sxs-lookup"><span data-stu-id="22a60-154">Type **AzureML Demo API** as the **Web API name**.</span></span> <span data-ttu-id="22a60-155">Escriba **https://ussouthcentral.services.azureml.net** como la **dirección URL del servicio web**.</span><span class="sxs-lookup"><span data-stu-id="22a60-155">Type **https://ussouthcentral.services.azureml.net** as the **Web service URL**.</span></span> <span data-ttu-id="22a60-156">Escriba **azureml-demo** como el **sufijo de la dirección URL de la API web**.</span><span class="sxs-lookup"><span data-stu-id="22a60-156">Type **azureml-demo** as the **Web API URL suffix**.</span></span> <span data-ttu-id="22a60-157">Seleccione **HTTPS** como el esquema de la **dirección URL de la API web**.</span><span class="sxs-lookup"><span data-stu-id="22a60-157">Check **HTTPS** as the **Web API URL** scheme.</span></span> <span data-ttu-id="22a60-158">Seleccione **Starter** en **Productos**.</span><span class="sxs-lookup"><span data-stu-id="22a60-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="22a60-159">Cuando haya finalizado, haga clic en **Guardar** para crear la API.</span><span class="sxs-lookup"><span data-stu-id="22a60-159">When finished, click **Save** to create the API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-the-operations"></a><span data-ttu-id="22a60-161">Adición de operaciones</span><span class="sxs-lookup"><span data-stu-id="22a60-161">Add the operations</span></span>
<span data-ttu-id="22a60-162">Haga clic en **Agregar operación** para agregar operaciones a esta API.</span><span class="sxs-lookup"><span data-stu-id="22a60-162">Click **Add operation** to add operations to this API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="22a60-164">Se mostrará la ventana **Nueva operación** y la pestaña **Firma** se seleccionará de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="22a60-164">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="22a60-165">Adición de una operación de registro de recursos</span><span class="sxs-lookup"><span data-stu-id="22a60-165">Add RRS Operation</span></span>
<span data-ttu-id="22a60-166">En primer lugar cree una operación para el servicio RRS de AzureML.</span><span class="sxs-lookup"><span data-stu-id="22a60-166">First create an operation for the AzureML RRS service.</span></span> <span data-ttu-id="22a60-167">Seleccione **POST** como **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="22a60-167">Select **POST** as the **HTTP verb**.</span></span> <span data-ttu-id="22a60-168">Escriba **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** como **modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="22a60-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as the **URL template**.</span></span> <span data-ttu-id="22a60-169">Escriba **Ejecución de RRS** como **Nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="22a60-169">Type **RRS Execute** as the **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="22a60-171">Haga clic en **Respuestas** > **AGREGAR** a la izquierda y seleccione **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="22a60-171">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="22a60-172">Haga clic en **Guardar** para guardar esta operación.</span><span class="sxs-lookup"><span data-stu-id="22a60-172">Click **Save** to save this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="22a60-174">Adición de operaciones BES</span><span class="sxs-lookup"><span data-stu-id="22a60-174">Add BES Operations</span></span>
<span data-ttu-id="22a60-175">No se incluyen capturas de pantalla para las operaciones BES ya que son muy similares a las de agregar la operación RRS.</span><span class="sxs-lookup"><span data-stu-id="22a60-175">Screenshots are not included for the BES operations as they are very similar to those for adding the RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="22a60-176">Envío (pero no inicio) de un trabajo de ejecución por lotes</span><span class="sxs-lookup"><span data-stu-id="22a60-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="22a60-177">Haga clic en **Agregar operación** para agregar la operación BES de AzureML a la API.</span><span class="sxs-lookup"><span data-stu-id="22a60-177">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="22a60-178">Seleccione **POST** para el **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="22a60-178">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="22a60-179">Escriba **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** para el **modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="22a60-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="22a60-180">Escriba **Envío de BES** en el **Nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="22a60-180">Type **BES Submit** for the **Display name**.</span></span> <span data-ttu-id="22a60-181">Haga clic en **Respuestas** > **AGREGAR** a la izquierda y seleccione **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="22a60-181">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="22a60-182">Haga clic en **Guardar** para guardar esta operación.</span><span class="sxs-lookup"><span data-stu-id="22a60-182">Click **Save** to save this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="22a60-183">Inicio de un trabajo de ejecución por lotes</span><span class="sxs-lookup"><span data-stu-id="22a60-183">Start a Batch Execution job</span></span>
<span data-ttu-id="22a60-184">Haga clic en **Agregar operación** para agregar la operación BES de AzureML a la API.</span><span class="sxs-lookup"><span data-stu-id="22a60-184">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="22a60-185">Seleccione **POST** para el **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="22a60-185">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="22a60-186">Escriba **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** para el **modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="22a60-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="22a60-187">Escriba **Inicio de BES** en el **Nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="22a60-187">Type **BES Start** for the **Display name**.</span></span> <span data-ttu-id="22a60-188">Haga clic en **Respuestas** > **AGREGAR** a la izquierda y seleccione **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="22a60-188">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="22a60-189">Haga clic en **Guardar** para guardar esta operación.</span><span class="sxs-lookup"><span data-stu-id="22a60-189">Click **Save** to save this operation.</span></span>

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="22a60-190">Obtener el estado o el resultado de un trabajo de ejecución por lotes</span><span class="sxs-lookup"><span data-stu-id="22a60-190">Get the status or result of a Batch Execution job</span></span>
<span data-ttu-id="22a60-191">Haga clic en **Agregar operación** para agregar la operación BES de AzureML a la API.</span><span class="sxs-lookup"><span data-stu-id="22a60-191">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="22a60-192">Seleccione **GET** para el **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="22a60-192">Select **GET** for the **HTTP verb**.</span></span> <span data-ttu-id="22a60-193">Escriba **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** para el **modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="22a60-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="22a60-194">Escriba **Estado de BES** en el **Nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="22a60-194">Type **BES Status** for the **Display name**.</span></span> <span data-ttu-id="22a60-195">Haga clic en **Respuestas** > **AGREGAR** a la izquierda y seleccione **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="22a60-195">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="22a60-196">Haga clic en **Guardar** para guardar esta operación.</span><span class="sxs-lookup"><span data-stu-id="22a60-196">Click **Save** to save this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="22a60-197">Eliminación de un trabajo de ejecución por lotes</span><span class="sxs-lookup"><span data-stu-id="22a60-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="22a60-198">Haga clic en **Agregar operación** para agregar la operación BES de AzureML a la API.</span><span class="sxs-lookup"><span data-stu-id="22a60-198">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="22a60-199">Seleccione **DELETE** para el **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="22a60-199">Select **DELETE** for the **HTTP verb**.</span></span> <span data-ttu-id="22a60-200">Escriba **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** para el **modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="22a60-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="22a60-201">Escriba **Eliminación de BES** en el **Nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="22a60-201">Type **BES Delete** for the **Display name**.</span></span> <span data-ttu-id="22a60-202">Haga clic en **Respuestas** > **AGREGAR** a la izquierda y seleccione **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="22a60-202">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="22a60-203">Haga clic en **Guardar** para guardar esta operación.</span><span class="sxs-lookup"><span data-stu-id="22a60-203">Click **Save** to save this operation.</span></span>

## <a name="call-an-operation-from-the-developer-portal"></a><span data-ttu-id="22a60-204">Llamada a una operación desde el portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="22a60-204">Call an operation from the Developer Portal</span></span>
<span data-ttu-id="22a60-205">Se puede llamar a las operaciones directamente desde el portal para desarrolladores, lo que proporciona una forma cómoda de ver y probar las operaciones de una API.</span><span class="sxs-lookup"><span data-stu-id="22a60-205">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="22a60-206">En este paso de la guía llamará al método **Ejecución de RRS** que se agregó a la **API de demostración de AzureML**.</span><span class="sxs-lookup"><span data-stu-id="22a60-206">In this guide step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span></span> <span data-ttu-id="22a60-207">Haga clic en **Portal para desarrolladores** , en el menú que se encuentra en la parte superior derecha del Portal clásico.</span><span class="sxs-lookup"><span data-stu-id="22a60-207">Click **Developer portal** from the menu at the top right of the Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="22a60-209">Haga clic en **API** en el menú superior y, a continuación, haga clic en **API de demostración de AzureML** para ver las operaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="22a60-209">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="22a60-211">Seleccione **Ejecución de RRS** para la operación.</span><span class="sxs-lookup"><span data-stu-id="22a60-211">Select **RRS Execute** for the operation.</span></span> <span data-ttu-id="22a60-212">Haga clic en **Pruébelo**.</span><span class="sxs-lookup"><span data-stu-id="22a60-212">Click **Try It**.</span></span>

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="22a60-214">Para los parámetros de solicitud, escriba su **área de trabajo**,  **servicio**, **2.0** para **apiversion** y  **true** para **detalles**.</span><span class="sxs-lookup"><span data-stu-id="22a60-214">For Request parameters, type your **workspace**,  **service**, **2.0** for the **apiversion**, and  **true** for the **details**.</span></span> <span data-ttu-id="22a60-215">Puede encontrar el **área de trabajo** y el **servicio** en el panel del servicio web AzureML (consulte **Prueba del servicio web** en el apéndice A).</span><span class="sxs-lookup"><span data-stu-id="22a60-215">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="22a60-216">Para los encabezados de solicitud, haga clic en **Agregar encabezado** y escriba **Content-Type** y **application/json**, después haga clic en **Agregar encabezado** y escriba **Autorización** y **Portador <YOUR AZUREML SERVICE API-KEY>**.</span><span class="sxs-lookup"><span data-stu-id="22a60-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="22a60-217">Puede encontrar su **clave de API** en el panel del servicio web AzureML (consulte **Prueba del servicio web** en el apéndice A).</span><span class="sxs-lookup"><span data-stu-id="22a60-217">You can find your **api key** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="22a60-218">Escriba **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["Este es un buen día"]]}}, "GlobalParameters": {}}** para el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="22a60-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for the request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="22a60-220">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="22a60-220">Click **Send**.</span></span>

![Enviar](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="22a60-222">Después de invocar una operación, el portal para desarrolladores mostrará el campo **Dirección URL solicitada** en el servicio de back-end, así como los campos **Estado de respuesta**, **Encabezados de respuesta** y **Contenido de respuesta**.</span><span class="sxs-lookup"><span data-stu-id="22a60-222">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="22a60-224">Apéndice A: Creación y prueba de un servicio web sencillo de AzureML</span><span class="sxs-lookup"><span data-stu-id="22a60-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-the-experiment"></a><span data-ttu-id="22a60-225">Creación del experimento</span><span class="sxs-lookup"><span data-stu-id="22a60-225">Creating the experiment</span></span>
<span data-ttu-id="22a60-226">A continuación se muestran los pasos para crear un experimento de Aprendizaje automático de Azure sencillo e implementarlo como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="22a60-226">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="22a60-227">El servicio web toma como entrada una columna de texto arbitrario de entrada y devuelve un conjunto de características representadas como números enteros.</span><span class="sxs-lookup"><span data-stu-id="22a60-227">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="22a60-228">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="22a60-228">For example:</span></span>

| <span data-ttu-id="22a60-229">Texto</span><span class="sxs-lookup"><span data-stu-id="22a60-229">Text</span></span> | <span data-ttu-id="22a60-230">Texto con hash</span><span class="sxs-lookup"><span data-stu-id="22a60-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="22a60-231">Este es un buen día</span><span class="sxs-lookup"><span data-stu-id="22a60-231">This is a good day</span></span> |<span data-ttu-id="22a60-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="22a60-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="22a60-233">En primer lugar, mediante el explorador que prefiera, vaya a: [https://studio.azureml.net/](https://studio.azureml.net/) y escriba sus credenciales para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="22a60-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span></span> <span data-ttu-id="22a60-234">Después, cree un nuevo experimento en blanco.</span><span class="sxs-lookup"><span data-stu-id="22a60-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="22a60-236">Cambie su nombre a **SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="22a60-236">Rename it to **SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="22a60-237">Expanda **Conjuntos de datos guardados** y arrastre **Reseñas de libros de Amazon** al experimento.</span><span class="sxs-lookup"><span data-stu-id="22a60-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="22a60-239">Expanda **Transformación de datos** y **Manipulación** y arrastre **Seleccionar columnas de conjunto de datos** al experimento.</span><span class="sxs-lookup"><span data-stu-id="22a60-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="22a60-240">Conecte **Reseñas de libros de Amazon** a **Seleccionar columnas de conjunto de datos**.</span><span class="sxs-lookup"><span data-stu-id="22a60-240">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="22a60-242">Haga clic en **Seleccionar columnas de conjunto de datos** y después haga clic en **Iniciar el selector de columnas** y seleccione **Col2**.</span><span class="sxs-lookup"><span data-stu-id="22a60-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="22a60-243">Haga clic en la marca de verificación para aplicar estos cambios.</span><span class="sxs-lookup"><span data-stu-id="22a60-243">Click the checkmark to apply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="22a60-245">Expanda **Análisis de texto** y arrastre **Hash de características** al experimento.</span><span class="sxs-lookup"><span data-stu-id="22a60-245">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span></span> <span data-ttu-id="22a60-246">Conecte **Seleccionar columnas de conjunto de datos** a **Hash de características**.</span><span class="sxs-lookup"><span data-stu-id="22a60-246">Connect **Select Columns in Dataset** to **Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="22a60-248">Escriba **3** en **Tamaño de bits de hash**.</span><span class="sxs-lookup"><span data-stu-id="22a60-248">Type **3** for the **Hashing bitsize**.</span></span> <span data-ttu-id="22a60-249">Se crearán 8 (23) columnas.</span><span class="sxs-lookup"><span data-stu-id="22a60-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="22a60-251">En este punto, quizá quiera hacer clic en **Ejecutar** para probar el experimento.</span><span class="sxs-lookup"><span data-stu-id="22a60-251">At this point, you may want to click **Run** to test the experiment.</span></span>

![Ejecutar](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="22a60-253">Creación de un servicio web</span><span class="sxs-lookup"><span data-stu-id="22a60-253">Create a web service</span></span>
<span data-ttu-id="22a60-254">Ahora va a crear un servicio web.</span><span class="sxs-lookup"><span data-stu-id="22a60-254">Now create a web service.</span></span> <span data-ttu-id="22a60-255">Expanda **Servicio web** y arrastre **Entrada** al experimento.</span><span class="sxs-lookup"><span data-stu-id="22a60-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="22a60-256">Conecte **Entrada** a **Hash de características**.</span><span class="sxs-lookup"><span data-stu-id="22a60-256">Connect **Input** to **Feature Hashing**.</span></span> <span data-ttu-id="22a60-257">Arrastre también **Resultado** al experimento.</span><span class="sxs-lookup"><span data-stu-id="22a60-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="22a60-258">Conecte **Resultado** a **Hash de características**.</span><span class="sxs-lookup"><span data-stu-id="22a60-258">Connect **Output** to **Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="22a60-260">Haga clic en **Publicar servicio web**.</span><span class="sxs-lookup"><span data-stu-id="22a60-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="22a60-262">Haga clic en **Sí** para publicar el experimento.</span><span class="sxs-lookup"><span data-stu-id="22a60-262">Click **Yes** to publish the experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a><span data-ttu-id="22a60-264">Prueba del servicio web</span><span class="sxs-lookup"><span data-stu-id="22a60-264">Test the web service</span></span>
<span data-ttu-id="22a60-265">Un servicio web de AzureML consta de los extremos RRS (servicio de solicitud/respuesta) y BES (servicio de ejecución por lotes).</span><span class="sxs-lookup"><span data-stu-id="22a60-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="22a60-266">RRS sirve para la ejecución sincrónica.</span><span class="sxs-lookup"><span data-stu-id="22a60-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="22a60-267">BES sirve para la ejecución por lotes asincrónica.</span><span class="sxs-lookup"><span data-stu-id="22a60-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="22a60-268">Para probar el servicio web con el origen de Python del ejemplo siguiente, puede que necesite descargar e instalar el SDK de Azure para Python (consulte: [Cómo instalar Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="22a60-268">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="22a60-269">También necesitará el **área de trabajo**, el **servicio** y la **api_key** del experimento para el origen de ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="22a60-269">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span></span> <span data-ttu-id="22a60-270">Puede encontrar el área de trabajo y el servicio haciendo clic en **Solicitud-respuesta** o en **Ejecución de lotes** del experimento en el panel del servicio web.</span><span class="sxs-lookup"><span data-stu-id="22a60-270">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="22a60-272">Puede encontrar la **api_key** haciendo clic en el experimento del panel del servicio web.</span><span class="sxs-lookup"><span data-stu-id="22a60-272">You can find the **api_key** by clicking your experiment in the web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="22a60-274">Prueba del extremo RRS</span><span class="sxs-lookup"><span data-stu-id="22a60-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="22a60-275">Botón Probar</span><span class="sxs-lookup"><span data-stu-id="22a60-275">Test button</span></span>
<span data-ttu-id="22a60-276">Una manera fácil de probar el extremo RRS es hacer clic en **Probar** en el panel del servicio web.</span><span class="sxs-lookup"><span data-stu-id="22a60-276">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="22a60-278">Escriba **Este es un buen día** para **col2**.</span><span class="sxs-lookup"><span data-stu-id="22a60-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="22a60-279">Haga clic en la marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="22a60-279">Click the checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="22a60-281">Verá algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="22a60-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="22a60-283">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="22a60-283">Sample Code</span></span>
<span data-ttu-id="22a60-284">Otra forma de probar el RRS es desde el código de cliente.</span><span class="sxs-lookup"><span data-stu-id="22a60-284">Another way to test your RRS is from your client code.</span></span> <span data-ttu-id="22a60-285">Si hace clic en **Solicitud-respuesta** en el panel y se desplaza hasta la parte inferior, verá el código de ejemplo de C#, Python y R. También verá la sintaxis de la solicitud de RRS, incluidos el URI de solicitud, los encabezados y el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="22a60-285">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span></span>

<span data-ttu-id="22a60-286">Esta guía muestra un ejemplo de Python en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="22a60-286">This guide shows a working Python example.</span></span> <span data-ttu-id="22a60-287">Necesitará modificarlo con el **área de trabajo**, el **servicio** y la **api_key** del experimento.</span><span class="sxs-lookup"><span data-stu-id="22a60-287">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span>

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
        print("The request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="22a60-288">Prueba de extremo BES</span><span class="sxs-lookup"><span data-stu-id="22a60-288">Test BES endpoint</span></span>
<span data-ttu-id="22a60-289">Haga clic en **Ejecución de lotes** en el panel y desplácese hasta la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="22a60-289">Click **Batch execution** on the dashboard and scroll to the bottom.</span></span> <span data-ttu-id="22a60-290">Verá el código de ejemplo de C#, Python y R. También verá la sintaxis de las solicitudes BES para enviar un trabajo, iniciar un trabajo, obtener el estado o los resultados de un trabajo y eliminar un trabajo.</span><span class="sxs-lookup"><span data-stu-id="22a60-290">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span></span>

<span data-ttu-id="22a60-291">Esta guía muestra un ejemplo de Python en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="22a60-291">This guide shows a working Python example.</span></span> <span data-ttu-id="22a60-292">Debe modificarlo con el **área de trabajo**, el **servicio** y la **api_key** del experimento.</span><span class="sxs-lookup"><span data-stu-id="22a60-292">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="22a60-293">Además, deberá modificar el **nombre de la cuenta de almacenamiento**, la **clave de la cuenta de almacenamiento** y el **nombre de contenedor de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="22a60-293">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="22a60-294">Por último, deberá modificar la ubicación del **archivo de entrada** y la ubicación del **archivo de salida**.</span><span class="sxs-lookup"><span data-stu-id="22a60-294">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH THE API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH THE LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH THE LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("The request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading the result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written to the file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("The results for " + outputName + " are available at the following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "The results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading the input to blob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded the input to blob storage"
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
    print("Submitting the job...")
    # submit the job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove the enclosing double-quotes
    print("Job ID: " + job_id)
    # start the job
    print("Starting the job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking the job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in the follwing code
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