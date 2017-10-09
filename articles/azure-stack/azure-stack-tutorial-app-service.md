---
title: "aaaMake web, móviles y los usuarios de API aplicaciones disponibles tooyour pila de Azure | Documentos de Microsoft"
description: "Tutorial tooinstall Hola proveedor de recursos de servicio de aplicaciones y crear ofertas que proporcionan la pila de Azure a los usuarios Hola capacidad toocreate web, móviles y aplicaciones de API."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/03/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 62b86cf6288b8f629bc92dade003c712fe523187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="make-web-mobile-and-api-apps-available-tooyour-azure-stack-users"></a><span data-ttu-id="ccc0e-103">Asegúrese de web, móviles y los usuarios de API aplicaciones disponibles tooyour pila de Azure</span><span class="sxs-lookup"><span data-stu-id="ccc0e-103">Make web, mobile, and API apps available tooyour Azure Stack users</span></span>

<span data-ttu-id="ccc0e-104">Como administrador de la nube de Azure Stack, puede crear ofertas que permitan a los usuarios (inquilinos) crear aplicaciones web, móviles y de API, así como de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create Azure Functions and web, mobile, and API applications.</span></span> <span data-ttu-id="ccc0e-105">Si proporciona acceso a los usuarios de toothese a petición, en la nube aplicaciones tooyour, puede guardarlos tiempo y recursos.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-105">By providing access toothese on-demand, cloud-based apps tooyour users, you can save them time and resources.</span></span> <span data-ttu-id="ccc0e-106">tooset este servicio, tendrá que:</span><span class="sxs-lookup"><span data-stu-id="ccc0e-106">tooset this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ccc0e-107">Implementar Hola proveedor de recursos de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ccc0e-107">Deploy hello App Service resource provider</span></span>
> * <span data-ttu-id="ccc0e-108">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="ccc0e-108">Create an offer</span></span>
> * <span data-ttu-id="ccc0e-109">Oferta de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="ccc0e-109">Test hello offer</span></span>

## <a name="deploy-hello-app-service-resource-provider"></a><span data-ttu-id="ccc0e-110">Implementar Hola proveedor de recursos de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ccc0e-110">Deploy hello App Service resource provider</span></span>

1. <span data-ttu-id="ccc0e-111">[Preparar el host del Kit de desarrollo de Azure pila hello](azure-stack-app-service-before-you-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ccc0e-111">[Prepare hello Azure Stack Development Kit host](azure-stack-app-service-before-you-get-started.md).</span></span> <span data-ttu-id="ccc0e-112">Esto incluye la implementación de proveedor de recursos de SQL Server de hello, que es necesario para crear aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-112">This includes deploying hello SQL Server resource provider, which is required for creating some apps.</span></span>
2. <span data-ttu-id="ccc0e-113">[Descargar los scripts de instalador y la aplicación auxiliar de hello](azure-stack-app-service-deploy.md#download-the-required-components).</span><span class="sxs-lookup"><span data-stu-id="ccc0e-113">[Download hello installer and helper scripts](azure-stack-app-service-deploy.md#download-the-required-components).</span></span>
3. <span data-ttu-id="ccc0e-114">[Ejecutar script de aplicación auxiliar de hello toocreate requerido certificados](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="ccc0e-114">[Run hello helper script toocreate required certificates](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span></span>
4. <span data-ttu-id="ccc0e-115">[Instalar el proveedor de recursos de servicio de aplicaciones de hello](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (tardará tooinstall un par de horas y para todos los Hola tooappear de roles de trabajo).</span><span class="sxs-lookup"><span data-stu-id="ccc0e-115">[Install hello App Service resource provider](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (it will take a couple hours tooinstall and for all hello worker roles tooappear).</span></span>
5. <span data-ttu-id="ccc0e-116">[Validar la instalación de hello](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span><span class="sxs-lookup"><span data-stu-id="ccc0e-116">[Validate hello installation](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="ccc0e-117">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="ccc0e-117">Create an offer</span></span>

<span data-ttu-id="ccc0e-118">Por ejemplo, puede crear una oferta que permita a los usuarios crear sistemas de administración de contenido web DNN.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-118">As an example, you can create an offer that lets users create DNN web content management systems.</span></span> <span data-ttu-id="ccc0e-119">Requiere el servicio de SQL Server de Hola que ya ha habilitado mediante la instalación de proveedor de recursos de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-119">It requires hello SQL Server service which you already enabled by installing hello SQL Server resource provider.</span></span>

1.  <span data-ttu-id="ccc0e-120">[Establezca una cuota](azure-stack-setting-quotas.md) y asígnele el nombre *CuotaDeAppService*.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-120">[Set a quota](azure-stack-setting-quotas.md) and name it *AppServiceQuota*.</span></span> <span data-ttu-id="ccc0e-121">Seleccione **Microsoft.Web** para hello **Namespace** campo.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-121">Select **Microsoft.Web** for hello **Namespace** field.</span></span>
2.  <span data-ttu-id="ccc0e-122">[Cree un plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="ccc0e-122">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="ccc0e-123">Asígnele el nombre *TestAppServicePlan*, seleccione Hola Hola **Microsoft.SQL** servicio, y **cuota de servicio de aplicaciones** cuota.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-123">Name it *TestAppServicePlan*, select hello hello **Microsoft.SQL** service, and **AppService Quota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ccc0e-124">los usuarios de toolet crear otras aplicaciones, otros servicios pueden ser necesaria en el plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-124">toolet users create other apps, other services might be required in hello plan.</span></span> <span data-ttu-id="ccc0e-125">Por ejemplo, las funciones de Azure requiere ese plan Hola incluyen hello **almacenamiento de Microsoft** de servicio, mientras que requiere de Wordpress **Microsoft.MySQL**.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-125">For example, Azure Functions requires that hello plan     include hello **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQL**.</span></span>
    > 
    >

3.  <span data-ttu-id="ccc0e-126">[Crear una oferta](azure-stack-create-offer.md), asígnele el nombre **TestAppServiceOffer** y seleccione hello **TestAppServicePlan** plan.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-126">[Create an offer](azure-stack-create-offer.md), name it **TestAppServiceOffer** and select hello **TestAppServicePlan** plan.</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="ccc0e-127">Oferta de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="ccc0e-127">Test hello offer</span></span>

<span data-ttu-id="ccc0e-128">Ahora que ha implementado Hola proveedor de recursos de servicio de aplicaciones y crear una oferta, puede iniciar sesión como un usuario, suscribirse toohello oferta y crear una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-128">Now that you've deployed hello App Service resource provider and created an offer, you can sign in as a user, subscribe toohello offer, and create an app.</span></span> <span data-ttu-id="ccc0e-129">En este ejemplo, vamos a crear un sistema de administración de contenido de la plataforma DNN.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-129">For this example, we'll create a DNN Platform content management system.</span></span> <span data-ttu-id="ccc0e-130">Primero debe crear una base de datos SQL y, a continuación, aplicación web de hello DNN.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-130">You must first create a SQL database and then hello DNN web app.</span></span>

### <a name="subscribe-toohello-offer"></a><span data-ttu-id="ccc0e-131">Suscribirse toohello oferta</span><span class="sxs-lookup"><span data-stu-id="ccc0e-131">Subscribe toohello offer</span></span>
1. <span data-ttu-id="ccc0e-132">Inicie sesión en toohello portal de Azure pila (https://portal.local.azurestack.external) como un inquilino.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-132">Sign in toohello Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="ccc0e-133">Haga clic en **Obtener una suscripción** > escriba **SuscripciónDePruebaDeAppService** en **Nombre para mostrar** > **Seleccionar una oferta**  >  **OfertaDePruebaDeAppService** > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-133">Click **Get a subscription** > type **TestAppServiceSubscription** under **Display Name** > **Select an offer** > **TestAppServiceOffer** > **Create**.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="ccc0e-134">Creación de una base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="ccc0e-134">Create a SQL database</span></span>

1. <span data-ttu-id="ccc0e-135">Haga clic en **+** > **Datos y almacenamiento** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-135">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="ccc0e-136">Deje Hola los valores predeterminados para los campos de hello, excepto como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="ccc0e-136">Leave hello defaults for hello fields, except as follows:</span></span>
    - <span data-ttu-id="ccc0e-137">**Nombre de la base de datos**: DNNdb</span><span class="sxs-lookup"><span data-stu-id="ccc0e-137">**Database Name**: DNNdb</span></span>
    - <span data-ttu-id="ccc0e-138">**Tamaño máximo en MB**: 100</span><span class="sxs-lookup"><span data-stu-id="ccc0e-138">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="ccc0e-139">**Suscripción**: OfertaDePruebaDeAppService</span><span class="sxs-lookup"><span data-stu-id="ccc0e-139">**Subscription**: TestAppServiceOffer</span></span>
    - <span data-ttu-id="ccc0e-140">**Grupo de recursos**: DNN-RG</span><span class="sxs-lookup"><span data-stu-id="ccc0e-140">**Resource Group**: DNN-RG</span></span>
3. <span data-ttu-id="ccc0e-141">Haga clic en **configuración de inicio de sesión**, escriba las credenciales de base de datos de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-141">Click **Login Settings**, enter credentials for hello database, and then click **OK**.</span></span> <span data-ttu-id="ccc0e-142">Usará estas credenciales más adelante en estos pasos.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-142">You'll use these credentials later in these steps.</span></span>
4. <span data-ttu-id="ccc0e-143">Haga clic en **SKU** > seleccione Hola SQL SKU que ha creado para Hola de hospedaje de SQL Server > **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-143">Click **SKU** > select hello SQL SKU that you created for hello SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="ccc0e-144">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-144">Click **Create**.</span></span>

### <a name="create-a-dnn-app"></a><span data-ttu-id="ccc0e-145">Creación de una aplicación DNN</span><span class="sxs-lookup"><span data-stu-id="ccc0e-145">Create a DNN app</span></span>    

1. <span data-ttu-id="ccc0e-146">Haga clic en  **+**   >  **Ver todo** > **DNN Platform preview** (Versión preliminar de la plataforma DNN)  > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-146">Click **+** > **See all** > **DNN Platform preview** > **Create**.</span></span>
2. <span data-ttu-id="ccc0e-147">Escriba *AppDNN* en **Nombre de la aplicación** y seleccione **OfertaDePruebaDeAppService** en **Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-147">Type *DNNapp* under **App name** and select **TestAppServiceOffer** under **Subscription**.</span></span>
3. <span data-ttu-id="ccc0e-148">Haga clic en **Configurar los valores obligatorios** > **Crear nuevo** > escriba un nombre de **Plan de App Service**.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-148">Click **Configure required settings** > **Create New** > type an **App Service plan** name.</span></span>
4. <span data-ttu-id="ccc0e-149">Haga clic en **Nivel de precios** > **F1 gratuito** > **Seleccionar** > **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-149">Click **Pricing tier** > **F1 Free** > **Select** > **OK**.</span></span>
5. <span data-ttu-id="ccc0e-150">Haga clic en **base de datos** y especificar información de hello para la base de datos SQL de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-150">Click **Database** and enter hello information for hello SQL database you created earlier.</span></span>
6. <span data-ttu-id="ccc0e-151">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ccc0e-151">Click **Create**.</span></span>

<span data-ttu-id="ccc0e-152">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="ccc0e-152">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ccc0e-153">Implementar Hola proveedor de recursos de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ccc0e-153">Deploy hello App Service resource provider</span></span>
> * <span data-ttu-id="ccc0e-154">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="ccc0e-154">Create an offer</span></span>
> * <span data-ttu-id="ccc0e-155">Oferta de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="ccc0e-155">Test hello offer</span></span>

<span data-ttu-id="ccc0e-156">Avanzar toohello siguiente tutorial toolearn cómo para:</span><span class="sxs-lookup"><span data-stu-id="ccc0e-156">Advance toohello next tutorial toolearn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ccc0e-157">Implementar aplicaciones tooAzure y la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="ccc0e-157">Deploy apps tooAzure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)
