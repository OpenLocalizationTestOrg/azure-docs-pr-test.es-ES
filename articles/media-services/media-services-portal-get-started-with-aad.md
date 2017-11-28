---
title: "Introducción a la autenticación de Azure AD mediante Azure Portal | Microsoft Docs"
description: "Obtenga información sobre cómo usar Azure Portal para acceder a la autenticación de Azure Active Directory (Azure AD) para utilizar la API de Azure Media Services."
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
ms.openlocfilehash: 829e0759f8aeb8758f6b8895b88b60b66ffb22ed
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-the-azure-portal"></a><span data-ttu-id="72bfa-103">Introducción a la autenticación de Azure AD mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="72bfa-103">Get started with Azure AD authentication by using the Azure portal</span></span>

<span data-ttu-id="72bfa-104">Obtenga información sobre cómo usar Azure Portal para acceder a la autenticación de Azure Active Directory (Azure AD) para tener acceso a la API de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="72bfa-104">Learn how to use the Azure portal to access Azure Active Directory (Azure AD) authentication to access the Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72bfa-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="72bfa-105">Prerequisites</span></span>

- <span data-ttu-id="72bfa-106">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="72bfa-106">An Azure account.</span></span> <span data-ttu-id="72bfa-107">Si no tiene cuenta, comience con una [evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72bfa-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="72bfa-108">Una cuenta de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="72bfa-108">A Media Services account.</span></span> <span data-ttu-id="72bfa-109">Para más información, vea [Creación de una cuenta de Azure Media Services mediante Azure Portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="72bfa-109">For more information, see [Create an Azure Media Services account by using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="72bfa-110">Asegúrese de revisar la [información general sobre el acceso a la API de Azure Media Services con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="72bfa-110">Make sure you review the [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="72bfa-111">Al utilizar la autenticación de Azure AD con Azure Media Services, tiene dos opciones de autenticación:</span><span class="sxs-lookup"><span data-stu-id="72bfa-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="72bfa-112">**Autenticación de usuario**.</span><span class="sxs-lookup"><span data-stu-id="72bfa-112">**User authentication**.</span></span> <span data-ttu-id="72bfa-113">Autenticar a una persona que está usando la aplicación para interactuar con los recursos de Media Services.</span><span class="sxs-lookup"><span data-stu-id="72bfa-113">Authenticate a person who is using the app to interact with Media Services resources.</span></span> <span data-ttu-id="72bfa-114">La aplicación interactiva en primer lugar debe solicitar al usuario las credenciales.</span><span class="sxs-lookup"><span data-stu-id="72bfa-114">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="72bfa-115">Un ejemplo es una aplicación de consola de administración que usan los usuarios autorizados para supervisar trabajos de codificación o streaming en vivo.</span><span class="sxs-lookup"><span data-stu-id="72bfa-115">An example is a management console app used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="72bfa-116">**Autenticación de entidad de servicio**.</span><span class="sxs-lookup"><span data-stu-id="72bfa-116">**Service principal authentication**.</span></span> <span data-ttu-id="72bfa-117">Autenticar un servicio.</span><span class="sxs-lookup"><span data-stu-id="72bfa-117">Authenticate a service.</span></span> <span data-ttu-id="72bfa-118">Las aplicaciones que normalmente utilizan este método de autenticación son aplicaciones que ejecutan servicios de demonio, servicios de nivel intermedio o trabajos programados: Web Apps, Function Apps, Logic Apps, API o un microservicio.</span><span class="sxs-lookup"><span data-stu-id="72bfa-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72bfa-119">Actualmente Media Services es compatible con el modelo de autenticación de Azure Access Control Service.</span><span class="sxs-lookup"><span data-stu-id="72bfa-119">Currently, Media Services supports the Azure Access Control service authentication model.</span></span> <span data-ttu-id="72bfa-120">Sin embargo, la autorización de Access Control dejará de usarse el 1 de junio de 2018.</span><span class="sxs-lookup"><span data-stu-id="72bfa-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="72bfa-121">Se recomienda migrar tan pronto como sea posible al modelo de autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72bfa-121">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span></span>

## <a name="select-the-authentication-method"></a><span data-ttu-id="72bfa-122">Selección del método de autenticación</span><span class="sxs-lookup"><span data-stu-id="72bfa-122">Select the authentication method</span></span>

1. <span data-ttu-id="72bfa-123">En [Azure Portal](https://portal.azure.com/), seleccione la cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="72bfa-123">In the [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="72bfa-124">Seleccione cómo conectarse a la API de Media Services.</span><span class="sxs-lookup"><span data-stu-id="72bfa-124">Select how to connect to the Media Services API.</span></span>

    ![Página de selección del método de conexión](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="72bfa-126">Autenticación de usuarios</span><span class="sxs-lookup"><span data-stu-id="72bfa-126">User authentication</span></span>

<span data-ttu-id="72bfa-127">Para conectarse a la API de Media Services mediante la opción de autenticación de usuario, la aplicación cliente debe solicitar un token de Azure AD que tiene los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="72bfa-127">To connect to the Media Services API by using the user authentication option, the client app needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="72bfa-128">Punto de conexión de inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="72bfa-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="72bfa-129">URI del recurso de Media Services</span><span class="sxs-lookup"><span data-stu-id="72bfa-129">Media Services resource URI</span></span>
* <span data-ttu-id="72bfa-130">Id. de cliente de aplicación de Media Services (nativo)</span><span class="sxs-lookup"><span data-stu-id="72bfa-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="72bfa-131">URI de redireccionamiento de aplicación de Media Services (nativo)</span><span class="sxs-lookup"><span data-stu-id="72bfa-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="72bfa-132">URI del recurso de Media Services de REST</span><span class="sxs-lookup"><span data-stu-id="72bfa-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="72bfa-133">Puede obtener los valores para estos parámetros en la página de la **API de Media Services con la autenticación de usuario**.</span><span class="sxs-lookup"><span data-stu-id="72bfa-133">You can get the values for these parameters on the **Media Services API with user authentication** page.</span></span> 

![Página de conexión con la autenticación de usuario](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="72bfa-135">Si se conecta a la API de Media Services mediante el SDK de Microsoft .NET para Media Services, los valores necesarios están disponibles como parte del SDK.</span><span class="sxs-lookup"><span data-stu-id="72bfa-135">If you connect to the Media Services API by using the Media Services Microsoft .NET SDK, the required values are available to you as part of the SDK.</span></span> <span data-ttu-id="72bfa-136">Para más información, vea [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md) (Uso de la autenticación de Azure AD para acceder a la API de Azure Media Services con .NET).</span><span class="sxs-lookup"><span data-stu-id="72bfa-136">For more information, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="72bfa-137">Si no usa el SDK del cliente .NET para Media Services, debe crear manualmente una solicitud de token de Azure AD con los parámetros descritos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="72bfa-137">If you're not using the Media Services .NET client SDK, you must manually create an Azure AD token request by using the parameters discussed earlier.</span></span> <span data-ttu-id="72bfa-138">Para más información, vea [Cómo usar la biblioteca de autenticación de Azure AD para obtener el token de Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="72bfa-138">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="72bfa-139">Autenticación de entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="72bfa-139">Service principal authentication</span></span>

<span data-ttu-id="72bfa-140">Para conectarse a la API de Media Services mediante la opción de la entidad de servicio, la aplicación de nivel intermedio (Web API o aplicación web) necesita solicitar un token de Azure AD que tenga los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="72bfa-140">To connect to the Media Services API by using the service principal option, your middle-tier app (web API or web application) needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="72bfa-141">Punto de conexión de inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="72bfa-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="72bfa-142">URI del recurso de Media Services</span><span class="sxs-lookup"><span data-stu-id="72bfa-142">Media Services resource URI</span></span> 
* <span data-ttu-id="72bfa-143">URI del recurso de Media Services de REST</span><span class="sxs-lookup"><span data-stu-id="72bfa-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="72bfa-144">Valores de aplicación de Azure AD: el **Id. de cliente** y el **secreto de cliente**</span><span class="sxs-lookup"><span data-stu-id="72bfa-144">Azure AD application values: the **client ID** and **client secret**</span></span>

<span data-ttu-id="72bfa-145">Puede obtener los valores para estos parámetros en la página de **conexión a la API de Media Services con la entidad de servicio**.</span><span class="sxs-lookup"><span data-stu-id="72bfa-145">You can get the values for these parameters on the **Connect to Media Services API with service principal** page.</span></span> <span data-ttu-id="72bfa-146">Utilice esta página para crear una aplicación de Azure AD o seleccionar una existente.</span><span class="sxs-lookup"><span data-stu-id="72bfa-146">Use this page to create a new Azure AD application or to select an existing one.</span></span> <span data-ttu-id="72bfa-147">Después de seleccionar la aplicación de Azure AD, puede obtener el identificador de cliente (identificador de aplicación) y generar los valores del secreto de cliente (clave).</span><span class="sxs-lookup"><span data-stu-id="72bfa-147">After you select the Azure AD app, you can get the client ID (Application ID) and generate the client secret (key) values.</span></span> 

![Página de conexión a la entidad de servicio](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="72bfa-149">Cuando la hoja **Entidad de servicio** se abre, se selecciona la primera aplicación de Azure AD que cumple los criterios siguientes:</span><span class="sxs-lookup"><span data-stu-id="72bfa-149">When the **Service Principal** blade opens, the first Azure AD application that meets the following criteria is selected:</span></span>

- <span data-ttu-id="72bfa-150">Se trata de una aplicación registrada de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72bfa-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="72bfa-151">Tiene permisos de control de acceso basado en roles de colaborador o propietario en la cuenta.</span><span class="sxs-lookup"><span data-stu-id="72bfa-151">It has Contributor or Owner Role-Based Access Control permissions on the account.</span></span>

<span data-ttu-id="72bfa-152">Después de crear o seleccionar una aplicación de Azure AD, puede crear y copiar un secreto de cliente (clave) y el identificador de cliente (identificador de aplicación).</span><span class="sxs-lookup"><span data-stu-id="72bfa-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and the client ID (Application ID).</span></span> <span data-ttu-id="72bfa-153">El secreto de cliente y el identificador de cliente son necesarios para obtener el token de acceso en este escenario.</span><span class="sxs-lookup"><span data-stu-id="72bfa-153">The client secret and client ID are required to get the access token in this scenario.</span></span>

<span data-ttu-id="72bfa-154">Si no tiene permisos para crear aplicaciones de Azure AD en su dominio, no se muestran los controles de la aplicación de Azure AD de la hoja y se muestra un mensaje de advertencia.</span><span class="sxs-lookup"><span data-stu-id="72bfa-154">If you don't have permissions to create Azure AD apps in your domain, the Azure AD app controls of the blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="72bfa-155">Si se conecta a la API de Media Services mediante el SDK de Media Services para .NET, vea [Usar autenticación de Azure AD para acceder a la API de Azure Media Services con .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="72bfa-155">If you connect to the Media Services API by using the Media Services .NET SDK, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="72bfa-156">Si no usa el SDK del cliente .NET para Media Services, debe crear manualmente una solicitud de token de Azure AD con los parámetros descritos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="72bfa-156">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD token request using the parameters discussed earlier.</span></span> <span data-ttu-id="72bfa-157">Para más información, vea [Cómo usar la biblioteca de autenticación de Azure AD para obtener el token de Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="72bfa-157">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-the-client-id-and-client-secret"></a><span data-ttu-id="72bfa-158">Obtención del identificador de cliente y del secreto de cliente</span><span class="sxs-lookup"><span data-stu-id="72bfa-158">Get the client ID and client secret</span></span>

<span data-ttu-id="72bfa-159">Después de seleccionar una aplicación de Azure AD existente o seleccionar la opción para crear una, aparecen los siguientes botones:</span><span class="sxs-lookup"><span data-stu-id="72bfa-159">After you select an existing Azure AD app or select the option to create a new one, the following buttons appear:</span></span>

![Botón Administrar permisos y botón Administrar aplicación](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="72bfa-161">Para abrir la hoja Aplicación de Azure AD, haga clic en **Administrar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="72bfa-161">To open the Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="72bfa-162">En la hoja **Administrar aplicación**, puede obtener el identificador de cliente de la aplicación (Id. de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="72bfa-162">On the **Manage application** blade, you can get the app's client ID (Application ID).</span></span> <span data-ttu-id="72bfa-163">Para generar un secreto de cliente (clave), seleccione **Claves**.</span><span class="sxs-lookup"><span data-stu-id="72bfa-163">To generate a client secret (key), select **Keys**.</span></span>

![Opción Claves de la hoja Administrar aplicación](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-the-application"></a><span data-ttu-id="72bfa-165">Administrar los permisos y la aplicación</span><span class="sxs-lookup"><span data-stu-id="72bfa-165">Manage permissions and the application</span></span>

<span data-ttu-id="72bfa-166">Después de seleccionar la aplicación de Azure AD, puede administrar la aplicación y los permisos.</span><span class="sxs-lookup"><span data-stu-id="72bfa-166">After you select the Azure AD application, you can manage the application and permissions.</span></span> <span data-ttu-id="72bfa-167">Para configurar la aplicación de Azure AD para acceder a otras aplicaciones, haga clic en **Administrar permisos**.</span><span class="sxs-lookup"><span data-stu-id="72bfa-167">To set up your Azure AD application to access other applications, click **Manage permissions**.</span></span> <span data-ttu-id="72bfa-168">Para las tareas de administración, como cambiar claves y direcciones URL de respuesta, o para editar el manifiesto de la aplicación, haga clic en **Administrar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="72bfa-168">For management tasks, such as changing keys and reply URLs, or to edit the application’s manifest, click **Manage application**.</span></span>

### <a name="edit-the-apps-settings-or-manifest"></a><span data-ttu-id="72bfa-169">Edición de la configuración o el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="72bfa-169">Edit the app's settings or manifest</span></span>

<span data-ttu-id="72bfa-170">Para editar la configuración o el manifiesto de la aplicación, haga clic en **Administrar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="72bfa-170">To edit the app's settings or manifest, click **Manage application**.</span></span>

![Página de Administrar aplicación](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="72bfa-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72bfa-172">Next steps</span></span>

<span data-ttu-id="72bfa-173">Empiece a trabajar en la [carga de archivos en la cuenta](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="72bfa-173">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
