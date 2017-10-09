---
title: "aaaGet inició con autenticación de Azure AD mediante Hola portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse hello Azure tooaccess portal tooconsume de autenticación de Azure Active Directory (Azure AD) Hola API de servicios multimedia de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a><span data-ttu-id="d557f-103">Empezar a trabajar con autenticación de Azure AD mediante el uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d557f-103">Get started with Azure AD authentication by using hello Azure portal</span></span>

<span data-ttu-id="d557f-104">Obtenga información acerca de cómo toouse hello Azure tooaccess portal Azure Active Directory (Azure AD) autenticación tooaccess Hola API de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="d557f-104">Learn how toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) authentication tooaccess hello Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d557f-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d557f-105">Prerequisites</span></span>

- <span data-ttu-id="d557f-106">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d557f-106">An Azure account.</span></span> <span data-ttu-id="d557f-107">Si no tiene cuenta, comience con una [evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d557f-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="d557f-108">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="d557f-108">A Media Services account.</span></span> <span data-ttu-id="d557f-109">Para obtener más información, consulte [crear una cuenta de servicios multimedia de Azure mediante el portal de Azure de Hola](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d557f-109">For more information, see [Create an Azure Media Services account by using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="d557f-110">Asegúrese de revisar hello [obtiene acceso a la API de los servicios de multimedia de Azure con información general de autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d557f-110">Make sure you review hello [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="d557f-111">Al utilizar la autenticación de Azure AD con Azure Media Services, tiene dos opciones de autenticación:</span><span class="sxs-lookup"><span data-stu-id="d557f-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="d557f-112">**Autenticación de usuario**.</span><span class="sxs-lookup"><span data-stu-id="d557f-112">**User authentication**.</span></span> <span data-ttu-id="d557f-113">Autenticar a una persona que usa Hola aplicación toointeract con recursos de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="d557f-113">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="d557f-114">aplicación interactiva de Hello en primer lugar debe solicitarle las credenciales de usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="d557f-114">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="d557f-115">Un ejemplo es una aplicación de consola de administración que usan los trabajos de codificación de los usuarios autorizados toomonitor o streaming en directo.</span><span class="sxs-lookup"><span data-stu-id="d557f-115">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="d557f-116">**Autenticación de entidad de servicio**.</span><span class="sxs-lookup"><span data-stu-id="d557f-116">**Service principal authentication**.</span></span> <span data-ttu-id="d557f-117">Autenticar un servicio.</span><span class="sxs-lookup"><span data-stu-id="d557f-117">Authenticate a service.</span></span> <span data-ttu-id="d557f-118">Las aplicaciones que normalmente utilizan este método de autenticación son aplicaciones que ejecutan servicios de demonio, servicios de nivel intermedio o trabajos programados: Web Apps, Function Apps, Logic Apps, API o un microservicio.</span><span class="sxs-lookup"><span data-stu-id="d557f-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d557f-119">Actualmente, servicios multimedia admite el modelo de autenticación de servicio de Control de acceso de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="d557f-119">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="d557f-120">Sin embargo, la autorización de Access Control dejará de usarse el 1 de junio de 2018.</span><span class="sxs-lookup"><span data-stu-id="d557f-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="d557f-121">Se recomienda que migre modelo de autenticación de Azure AD toohello tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="d557f-121">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

## <a name="select-hello-authentication-method"></a><span data-ttu-id="d557f-122">Seleccionar método de autenticación de Hola</span><span class="sxs-lookup"><span data-stu-id="d557f-122">Select hello authentication method</span></span>

1. <span data-ttu-id="d557f-123">Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="d557f-123">In hello [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="d557f-124">Seleccione cómo tooconnect toohello API de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="d557f-124">Select how tooconnect toohello Media Services API.</span></span>

    ![Página de selección del método de conexión](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="d557f-126">Autenticación de usuarios</span><span class="sxs-lookup"><span data-stu-id="d557f-126">User authentication</span></span>

<span data-ttu-id="d557f-127">Hola a tooconnect toohello API de servicios multimedia mediante el uso de la opción de autenticación de usuario, la aplicación de cliente de hello debe toorequest un token de Azure AD que ha Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="d557f-127">tooconnect toohello Media Services API by using hello user authentication option, hello client app needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="d557f-128">Punto de conexión de inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d557f-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="d557f-129">URI del recurso de Media Services</span><span class="sxs-lookup"><span data-stu-id="d557f-129">Media Services resource URI</span></span>
* <span data-ttu-id="d557f-130">Id. de cliente de aplicación de Media Services (nativo)</span><span class="sxs-lookup"><span data-stu-id="d557f-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="d557f-131">URI de redireccionamiento de aplicación de Media Services (nativo)</span><span class="sxs-lookup"><span data-stu-id="d557f-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="d557f-132">URI del recurso de Media Services de REST</span><span class="sxs-lookup"><span data-stu-id="d557f-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="d557f-133">Puede obtener valores de hello para estos parámetros en hello **API de servicios multimedia con la autenticación de usuario** página.</span><span class="sxs-lookup"><span data-stu-id="d557f-133">You can get hello values for these parameters on hello **Media Services API with user authentication** page.</span></span> 

![Página de conexión con la autenticación de usuario](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="d557f-135">Si se conecta toohello API de servicios multimedia mediante el uso de hello Media Services Microsoft .NET SDK, Hola requiere valores son tooyou disponible como parte del SDK de Hola.</span><span class="sxs-lookup"><span data-stu-id="d557f-135">If you connect toohello Media Services API by using hello Media Services Microsoft .NET SDK, hello required values are available tooyou as part of hello SDK.</span></span> <span data-ttu-id="d557f-136">Para obtener más información, consulte [tooaccess de autenticación de uso de Azure AD Hola API de servicios multimedia de Azure con .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="d557f-136">For more information, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="d557f-137">Si no está usando el SDK de cliente de .NET de los servicios multimedia de hello, debe crear manualmente una solicitud de token de Azure AD mediante parámetros de Hola que se analizaron anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d557f-137">If you're not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using hello parameters discussed earlier.</span></span> <span data-ttu-id="d557f-138">Para obtener más información, consulte [cómo toouse hello Azure AD biblioteca de autenticación tooget Hola token de Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="d557f-138">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="d557f-139">Autenticación de entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="d557f-139">Service principal authentication</span></span>

<span data-ttu-id="d557f-140">tooconnect toohello API de servicios multimedia mediante el uso de Hola opción principal de servicio, la aplicación de nivel intermedio (API de web o aplicación web) debe toorequest un token de Azure AD que ha Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="d557f-140">tooconnect toohello Media Services API by using hello service principal option, your middle-tier app (web API or web application) needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="d557f-141">Punto de conexión de inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d557f-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="d557f-142">URI del recurso de Media Services</span><span class="sxs-lookup"><span data-stu-id="d557f-142">Media Services resource URI</span></span> 
* <span data-ttu-id="d557f-143">URI del recurso de Media Services de REST</span><span class="sxs-lookup"><span data-stu-id="d557f-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="d557f-144">Los valores de aplicación de Azure AD: Hola **Id. de cliente** y **secreto de cliente**</span><span class="sxs-lookup"><span data-stu-id="d557f-144">Azure AD application values: hello **client ID** and **client secret**</span></span>

<span data-ttu-id="d557f-145">Puede obtener valores de hello para estos parámetros en hello **conectar tooMedia API de servicios con la entidad de servicio** página.</span><span class="sxs-lookup"><span data-stu-id="d557f-145">You can get hello values for these parameters on hello **Connect tooMedia Services API with service principal** page.</span></span> <span data-ttu-id="d557f-146">Utilice este toocreate página un nuevo Azure aplicación AD o tooselect uno ya existente.</span><span class="sxs-lookup"><span data-stu-id="d557f-146">Use this page toocreate a new Azure AD application or tooselect an existing one.</span></span> <span data-ttu-id="d557f-147">Después de seleccionar la aplicación de Azure AD de hello, puede obtener identificador de cliente de hello (Id. de aplicación) y generar valores de hello cliente secreto (clave).</span><span class="sxs-lookup"><span data-stu-id="d557f-147">After you select hello Azure AD app, you can get hello client ID (Application ID) and generate hello client secret (key) values.</span></span> 

![Página de conexión a la entidad de servicio](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="d557f-149">Cuando Hola **entidad de servicio** hoja se abre, se selecciona la primera aplicación de Azure AD de Hola que cumpla Hola siguiendo criterios:</span><span class="sxs-lookup"><span data-stu-id="d557f-149">When hello **Service Principal** blade opens, hello first Azure AD application that meets hello following criteria is selected:</span></span>

- <span data-ttu-id="d557f-150">Se trata de una aplicación registrada de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d557f-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="d557f-151">Permisos de Control de acceso de Owner Role-Based o colaborador tiene en cuenta Hola.</span><span class="sxs-lookup"><span data-stu-id="d557f-151">It has Contributor or Owner Role-Based Access Control permissions on hello account.</span></span>

<span data-ttu-id="d557f-152">Después de crear o seleccionar una aplicación de Azure AD, puede crear y copiar un secreto de cliente (clave) y Hola Id. de cliente (identificador de aplicación).</span><span class="sxs-lookup"><span data-stu-id="d557f-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and hello client ID (Application ID).</span></span> <span data-ttu-id="d557f-153">Identificador de cliente y secreto de cliente Hello son el token de acceso de hello tooget necesario en este escenario.</span><span class="sxs-lookup"><span data-stu-id="d557f-153">hello client secret and client ID are required tooget hello access token in this scenario.</span></span>

<span data-ttu-id="d557f-154">Si no tiene aplicaciones de Azure AD de toocreate de permisos en el dominio, no se muestran los controles de la aplicación hello Azure AD de hoja de Hola y se muestra un mensaje de advertencia.</span><span class="sxs-lookup"><span data-stu-id="d557f-154">If you don't have permissions toocreate Azure AD apps in your domain, hello Azure AD app controls of hello blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="d557f-155">Si se conecta toohello API de servicios multimedia mediante el uso de hello Media Services .NET SDK, vea [tooaccess de autenticación de uso de Azure AD Hola API de servicios multimedia de Azure con .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="d557f-155">If you connect toohello Media Services API by using hello Media Services .NET SDK, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="d557f-156">Si no utiliza el SDK de cliente de .NET de los servicios multimedia de hello, debe crear manualmente una solicitud de token de Azure AD con parámetros de Hola que se analizaron anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d557f-156">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request using hello parameters discussed earlier.</span></span> <span data-ttu-id="d557f-157">Para obtener más información, consulte [cómo toouse hello Azure AD biblioteca de autenticación tooget Hola token de Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="d557f-157">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-hello-client-id-and-client-secret"></a><span data-ttu-id="d557f-158">Obtener a cliente hello secreto de cliente y el Id.</span><span class="sxs-lookup"><span data-stu-id="d557f-158">Get hello client ID and client secret</span></span>

<span data-ttu-id="d557f-159">Después de seleccionar una aplicación de Azure AD existente u Hola seleccione opción toocreate uno nuevo, aparece Hola siguientes botones:</span><span class="sxs-lookup"><span data-stu-id="d557f-159">After you select an existing Azure AD app or select hello option toocreate a new one, hello following buttons appear:</span></span>

![Botón Administrar permisos y botón Administrar aplicación](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="d557f-161">Hola tooopen hoja de aplicaciones de Azure AD, haga clic en **administrar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="d557f-161">tooopen hello Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="d557f-162">En hello **administrar aplicación** hoja, puede obtener el identificador de cliente de la aplicación hello (Id. de aplicación).</span><span class="sxs-lookup"><span data-stu-id="d557f-162">On hello **Manage application** blade, you can get hello app's client ID (Application ID).</span></span> <span data-ttu-id="d557f-163">toogenerate un secreto de cliente (clave), seleccione **claves**.</span><span class="sxs-lookup"><span data-stu-id="d557f-163">toogenerate a client secret (key), select **Keys**.</span></span>

![Opción Claves de la hoja Administrar aplicación](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a><span data-ttu-id="d557f-165">Administrar los permisos y la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="d557f-165">Manage permissions and hello application</span></span>

<span data-ttu-id="d557f-166">Después de seleccionar la aplicación de Azure AD de hello, puede administrar permisos y la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d557f-166">After you select hello Azure AD application, you can manage hello application and permissions.</span></span> <span data-ttu-id="d557f-167">tooset seguridad su tooaccess de aplicación de Azure AD otras aplicaciones, haga clic en **administrar permisos**.</span><span class="sxs-lookup"><span data-stu-id="d557f-167">tooset up your Azure AD application tooaccess other applications, click **Manage permissions**.</span></span> <span data-ttu-id="d557f-168">Para las tareas de administración, como el cambio de claves y direcciones URL de respuesta o tooedit Hola manifiesto de aplicación, haga clic en **administrar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="d557f-168">For management tasks, such as changing keys and reply URLs, or tooedit hello application’s manifest, click **Manage application**.</span></span>

### <a name="edit-hello-apps-settings-or-manifest"></a><span data-ttu-id="d557f-169">Editar la configuración de la aplicación hello o en el manifiesto</span><span class="sxs-lookup"><span data-stu-id="d557f-169">Edit hello app's settings or manifest</span></span>

<span data-ttu-id="d557f-170">aplicación de hello tooedit valores de configuración o manifiesto, haga clic en **administrar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="d557f-170">tooedit hello app's settings or manifest, click **Manage application**.</span></span>

![Página de Administrar aplicación](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="d557f-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d557f-172">Next steps</span></span>

<span data-ttu-id="d557f-173">Empezar a trabajar con [cargar archivos tooyour cuenta](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="d557f-173">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
