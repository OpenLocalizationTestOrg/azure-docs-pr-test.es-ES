---
title: soluciones de servicios de Azure Batch de aaaUse Azure Active Directory tooauthenticate | Documentos de Microsoft
description: "Proceso por lotes es compatible con Azure AD para la autenticación de hello servicio por lotes."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="48c86-103">Autenticación de soluciones de servicio de Batch con Active Directory</span><span class="sxs-lookup"><span data-stu-id="48c86-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="48c86-104">Azure Batch admite la autenticación con [Azure Active Directory][aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48c86-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="48c86-105">Azure Active Directory es el directorio basado en la nube multiinquilino y el servicio de administración de identidades de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48c86-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="48c86-106">Azure por sí mismo utiliza Azure AD tooauthenticate sus clientes, los administradores de servicios y usuarios de la organización.</span><span class="sxs-lookup"><span data-stu-id="48c86-106">Azure itself uses Azure AD tooauthenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="48c86-107">Al utilizar la autenticación de Azure AD con Azure Batch, puede autenticar de una de estas dos maneras:</span><span class="sxs-lookup"><span data-stu-id="48c86-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="48c86-108">Mediante el uso de **la autenticación integrada de** tooauthenticate un usuario que está interactuando con la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="48c86-108">By using **integrated authentication** tooauthenticate a user that is interacting with hello application.</span></span> <span data-ttu-id="48c86-109">Una aplicación mediante la autenticación integrada recopila las credenciales del usuario y utiliza esas credenciales tooauthenticate acceder a tooBatch los recursos.</span><span class="sxs-lookup"><span data-stu-id="48c86-109">An application using integrated authentication gathers a user's credentials and uses those credentials tooauthenticate access tooBatch resources.</span></span>
- <span data-ttu-id="48c86-110">Mediante el uso de un **entidad de servicio** tooauthenticate una aplicación de modo desatendida.</span><span class="sxs-lookup"><span data-stu-id="48c86-110">By using a **service principal** tooauthenticate an unattended application.</span></span> <span data-ttu-id="48c86-111">Una entidad de servicio define Hola directiva y los permisos para una aplicación en la aplicación hello de orden toorepresent al tener acceso a recursos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="48c86-111">A service principal defines hello policy and permissions for an application in order toorepresent hello application when accessing resources at runtime.</span></span>

<span data-ttu-id="48c86-112">toolearn más información acerca de Azure AD, vea hello [documentación de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="48c86-112">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="48c86-113">Modo de autenticación y de asignación de grupo</span><span class="sxs-lookup"><span data-stu-id="48c86-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="48c86-114">Al crear una cuenta de Batch, puede especificar dónde se deben asignar los grupos creados para esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="48c86-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="48c86-115">Puede elegir tooallocate grupos en la suscripción al servicio de lote Hola predeterminado o en una suscripción de usuario.</span><span class="sxs-lookup"><span data-stu-id="48c86-115">You can choose tooallocate pools either in hello default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="48c86-116">Su elección afecta a cómo autenticar acceso tooresources en esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="48c86-116">Your choice affects how you authenticate access tooresources in that account.</span></span>

- <span data-ttu-id="48c86-117">**Suscripción al servicio de Batch**.</span><span class="sxs-lookup"><span data-stu-id="48c86-117">**Batch service subscription**.</span></span> <span data-ttu-id="48c86-118">De forma predeterminada, los grupos de Batch se asignan en una suscripción del servicio Batch.</span><span class="sxs-lookup"><span data-stu-id="48c86-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="48c86-119">Si elige esta opción, puede autenticar acceso tooresources en esa cuenta con [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) o con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c86-119">If you choose this option, you can authenticate access tooresources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="48c86-120">**Suscripción de usuario**.</span><span class="sxs-lookup"><span data-stu-id="48c86-120">**User subscription.**</span></span> <span data-ttu-id="48c86-121">Puede elegir tooallocate grupos de proceso por lotes en una suscripción de usuario que especifique.</span><span class="sxs-lookup"><span data-stu-id="48c86-121">You can choose tooallocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="48c86-122">Si elige esta opción, debe autenticarse con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c86-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="48c86-123">Puntos de conexión para autenticación</span><span class="sxs-lookup"><span data-stu-id="48c86-123">Endpoints for authentication</span></span>

<span data-ttu-id="48c86-124">aplicaciones de lote tooauthenticate con Azure AD, necesita tooinclude algunos puntos de conexión conocidos en el código.</span><span class="sxs-lookup"><span data-stu-id="48c86-124">tooauthenticate Batch applications with Azure AD, you need tooinclude some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="48c86-125">Punto de conexión de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48c86-125">Azure AD endpoint</span></span>

<span data-ttu-id="48c86-126">Hola base es el extremo de la autoridad de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="48c86-126">hello base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="48c86-127">tooauthenticate con Azure AD, use este extremo junto con el Id. de inquilino de hello (Id. de directorio).</span><span class="sxs-lookup"><span data-stu-id="48c86-127">tooauthenticate with Azure AD, you use this endpoint together with hello tenant ID (directory ID).</span></span> <span data-ttu-id="48c86-128">Id. de inquilino de Hello identifica hello toouse de inquilino de Azure AD para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="48c86-128">hello tenant ID identifies hello Azure AD tenant toouse for authentication.</span></span> <span data-ttu-id="48c86-129">tooretrieve Hola Id. de inquilino, siga los pasos de hello descritos en [obtener Id. de inquilino de Hola para Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="48c86-129">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="48c86-130">extremo específico del inquilino de Hello es necesaria cuando se autentica con una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="48c86-130">hello tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="48c86-131">extremo específico del inquilino de Hello es opcional cuando se autentica mediante la autenticación integrada, pero se recomienda.</span><span class="sxs-lookup"><span data-stu-id="48c86-131">hello tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="48c86-132">Sin embargo, también puede utilizar el punto de conexión común de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c86-132">However, you can also use hello Azure AD common endpoint.</span></span> <span data-ttu-id="48c86-133">punto de conexión común Hola proporciona una credencial genérica recopilación interfaz cuando no se ha proporcionado un específicos del inquilino.</span><span class="sxs-lookup"><span data-stu-id="48c86-133">hello common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="48c86-134">punto de conexión común de Hello es `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="48c86-134">hello common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="48c86-135">Para más información sobre los puntos de conexión de Azure AD, consulte [Escenarios de autenticación para Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="48c86-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="48c86-136">Punto de conexión de recursos de Batch</span><span class="sxs-lookup"><span data-stu-id="48c86-136">Batch resource endpoint</span></span>

<span data-ttu-id="48c86-137">Hola de uso **punto de conexión de recursos de Azure Batch** tooacquire un token para autenticar solicitudes de servicio por lotes de toohello:</span><span class="sxs-lookup"><span data-stu-id="48c86-137">Use hello **Azure Batch resource endpoint** tooacquire a token for authenticating requests toohello Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="48c86-138">Registro de la aplicación con un inquilino</span><span class="sxs-lookup"><span data-stu-id="48c86-138">Register your application with a tenant</span></span>

<span data-ttu-id="48c86-139">primer paso de Hola para utilizar Azure AD tooauthenticate está registrando su aplicación en un inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c86-139">hello first step in using Azure AD tooauthenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="48c86-140">Registrar la aplicación le permite toocall hello Azure [biblioteca de autenticación de Active Directory] [ aad_adal] (AAL) desde el código.</span><span class="sxs-lookup"><span data-stu-id="48c86-140">Registering your application enables you toocall hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="48c86-141">Hola AAL proporciona una API para autenticar con Azure AD desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48c86-141">hello ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="48c86-142">Registrando su aplicación es necesario si tiene previsto toouse la autenticación integrada o una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="48c86-142">Registering your application is required whether you plan toouse integrated authentication or a service principal.</span></span>

<span data-ttu-id="48c86-143">Al registrar la aplicación, se facilita información sobre su tooAzure aplicación AD.</span><span class="sxs-lookup"><span data-stu-id="48c86-143">When you register your application, you supply information about your application tooAzure AD.</span></span> <span data-ttu-id="48c86-144">Azure AD, a continuación, proporciona un identificador de la aplicación usa tooassociate de su aplicación con Azure AD en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="48c86-144">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="48c86-145">vea toolearn más información sobre el identificador de la aplicación hello [aplicación y objetos de entidad de servicio en Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="48c86-145">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="48c86-146">tooregister la aplicación de lote, siga los pasos de Hola Hola [agregar una aplicación](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sección [integrar aplicaciones con Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="48c86-146">tooregister your Batch application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="48c86-147">Si se registra la aplicación como una aplicación nativa, puede especificar cualquier URI válido para hello **URI de redireccionamiento**.</span><span class="sxs-lookup"><span data-stu-id="48c86-147">If you register your application as a Native Application, you can specify any valid URI for hello **Redirect URI**.</span></span> <span data-ttu-id="48c86-148">No es necesario toobe un punto de conexión real.</span><span class="sxs-lookup"><span data-stu-id="48c86-148">It does not need toobe a real endpoint.</span></span>

<span data-ttu-id="48c86-149">Después de registrar la aplicación, verá el identificador de la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="48c86-149">After you've registered your application, you'll see hello application ID:</span></span>

![Registro de la aplicación de Batch con Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="48c86-151">Para más información sobre el registro de una aplicación, consulte [Escenarios de autenticación para Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="48c86-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-hello-tenant-id-for-your-active-directory"></a><span data-ttu-id="48c86-152">Obtener Id. de inquilino de Hola de su Active Directory</span><span class="sxs-lookup"><span data-stu-id="48c86-152">Get hello tenant ID for your Active Directory</span></span>

<span data-ttu-id="48c86-153">Id. de inquilino de Hello identifica el inquilino de Azure AD de Hola que proporciona servicios de autenticación tooyour aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="48c86-153">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="48c86-154">tooget Hola Id. de inquilino, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="48c86-154">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="48c86-155">Hola portal de Azure, seleccione su Active Directory.</span><span class="sxs-lookup"><span data-stu-id="48c86-155">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="48c86-156">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="48c86-156">Click **Properties**.</span></span>
3. <span data-ttu-id="48c86-157">Copiar valor GUID de hello previsto Hola Id. de directorio.</span><span class="sxs-lookup"><span data-stu-id="48c86-157">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="48c86-158">Este valor también se denomina identificador del inquilino Hola.</span><span class="sxs-lookup"><span data-stu-id="48c86-158">This value is also called hello tenant ID.</span></span>

![Id. de directorio Hola](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="48c86-160">Uso de autenticación integrada</span><span class="sxs-lookup"><span data-stu-id="48c86-160">Use integrated authentication</span></span>

<span data-ttu-id="48c86-161">tooauthenticate con la autenticación integrada, deberá toogrant la toohello de tooconnect de permisos de aplicación API de servicio de lote.</span><span class="sxs-lookup"><span data-stu-id="48c86-161">tooauthenticate with integrated authentication, you need toogrant your application permissions tooconnect toohello Batch service API.</span></span> <span data-ttu-id="48c86-162">Este paso permite que la API de servicio de aplicación tooauthenticate llamadas toohello por lotes con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c86-162">This step enables your application tooauthenticate calls toohello Batch service API with Azure AD.</span></span>

<span data-ttu-id="48c86-163">Una vez que se haya [registrar la aplicación](#register-your-application-with-an-azure-ad-tenant), siga estos pasos en hello Azure toogrant portal que tener acceso el servicio por lotes toohello:</span><span class="sxs-lookup"><span data-stu-id="48c86-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in hello Azure portal toogrant it access toohello Batch service:</span></span>

1. <span data-ttu-id="48c86-164">En el panel de navegación izquierdo de Hola de hello portal de Azure, elija **más servicios**, haga clic en **registros de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="48c86-164">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="48c86-165">Busque el nombre de saludo de la aplicación en la lista de Hola de registros de aplicación:</span><span class="sxs-lookup"><span data-stu-id="48c86-165">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Buscar el nombre de la aplicación](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="48c86-167">Abra hello **configuración** hoja para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48c86-167">Open hello **Settings** blade for your application.</span></span> <span data-ttu-id="48c86-168">Hola **el acceso de API** sección, seleccione **los permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="48c86-168">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="48c86-169">Hola **los permisos necesarios** hoja, haga clic en hello **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="48c86-169">In hello **Required permissions** blade, click hello **Add** button.</span></span>
5. <span data-ttu-id="48c86-170">En el paso 1, busque Hola API de lote.</span><span class="sxs-lookup"><span data-stu-id="48c86-170">In step 1, search for hello Batch API.</span></span> <span data-ttu-id="48c86-171">Buscar cada una de estas cadenas hasta que encuentre Hola API:</span><span class="sxs-lookup"><span data-stu-id="48c86-171">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="48c86-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="48c86-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="48c86-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="48c86-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="48c86-174">Los inquilinos más recientes de Azure AD pueden utilizar este nombre.</span><span class="sxs-lookup"><span data-stu-id="48c86-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="48c86-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** es Id. de Hola para hello API de lote.</span><span class="sxs-lookup"><span data-stu-id="48c86-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 
6. <span data-ttu-id="48c86-176">Una vez que encuentre Hola API de lote, selecciónelo y haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="48c86-176">Once you find hello Batch API, select it and click hello **Select** button.</span></span>
6. <span data-ttu-id="48c86-177">En el paso 2, seleccione Hola casilla de verificación junto demasiado**servicio de lote de Azure de acceso** y haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="48c86-177">In step 2, select hello check box next too**Access Azure Batch Service** and click hello **Select** button.</span></span>
7. <span data-ttu-id="48c86-178">Haga clic en hello **realiza** botón.</span><span class="sxs-lookup"><span data-stu-id="48c86-178">Click hello **Done** button.</span></span>

<span data-ttu-id="48c86-179">Hola **permisos necesarios** hoja ahora muestra que la aplicación de Azure AD tiene acceso a tooboth AAL y Hola API del servicio de lote.</span><span class="sxs-lookup"><span data-stu-id="48c86-179">hello **Required Permissions** blade now shows that your Azure AD application has access tooboth ADAL and hello Batch service API.</span></span> <span data-ttu-id="48c86-180">Los permisos se conceden tooADAL automáticamente al registrar primero la aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c86-180">Permissions are granted tooADAL automatically when you first register your app with Azure AD.</span></span>

![Concesión de permisos de API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="48c86-182">Uso de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="48c86-182">Use a service principal</span></span> 

<span data-ttu-id="48c86-183">tooauthenticate una aplicación que se ejecuta desatendida, utilice a una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="48c86-183">tooauthenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="48c86-184">Una vez que ha registrado su aplicación, siga estos pasos en hello tooconfigure portal Azure una entidad de servicio:</span><span class="sxs-lookup"><span data-stu-id="48c86-184">After you've registered your application, follow these steps in hello Azure portal tooconfigure a service principal:</span></span>

1. <span data-ttu-id="48c86-185">Solicite una clave secreta para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48c86-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="48c86-186">Asignar una aplicación de tooyour de rol RBAC.</span><span class="sxs-lookup"><span data-stu-id="48c86-186">Assign an RBAC role tooyour application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="48c86-187">Solicitud de una clave secreta para la aplicación</span><span class="sxs-lookup"><span data-stu-id="48c86-187">Request a secret key for your application</span></span>

<span data-ttu-id="48c86-188">Cuando la aplicación se autentica con una entidad de servicio, envía Hola Id. de aplicación y un secreto tooAzure clave AD.</span><span class="sxs-lookup"><span data-stu-id="48c86-188">When your application authenticates with a service principal, it sends both hello application ID and a secret key tooAzure AD.</span></span> <span data-ttu-id="48c86-189">Podrá necesita toocreate y copiar toouse de clave secreta de Hola desde el código.</span><span class="sxs-lookup"><span data-stu-id="48c86-189">You'll need toocreate and copy hello secret key toouse from your code.</span></span>

<span data-ttu-id="48c86-190">Siga estos pasos en hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="48c86-190">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="48c86-191">En el panel de navegación izquierdo de Hola de hello portal de Azure, elija **más servicios**, haga clic en **registros de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="48c86-191">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="48c86-192">Buscar Hola nombre de la aplicación en la lista de Hola de registros de aplicación.</span><span class="sxs-lookup"><span data-stu-id="48c86-192">Search for hello name of your application in hello list of app registrations.</span></span>
3. <span data-ttu-id="48c86-193">Hola de presentación **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="48c86-193">Display hello **Settings** blade.</span></span> <span data-ttu-id="48c86-194">Hola **el acceso de API** sección, seleccione **claves**.</span><span class="sxs-lookup"><span data-stu-id="48c86-194">In hello **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="48c86-195">toocreate una clave, escriba una descripción para la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="48c86-195">toocreate a key, enter a description for hello key.</span></span> <span data-ttu-id="48c86-196">A continuación, seleccione una duración para la clave de Hola de uno o dos años.</span><span class="sxs-lookup"><span data-stu-id="48c86-196">Then select a duration for hello key of either one or two years.</span></span> 
5. <span data-ttu-id="48c86-197">Haga clic en hello **guardar** botón toocreate y mostrar hello clave.</span><span class="sxs-lookup"><span data-stu-id="48c86-197">Click hello **Save** button toocreate and display hello key.</span></span> <span data-ttu-id="48c86-198">Copie lugar seguro de hello clave-valor tooa, no será capaz de tooaccess nuevo después de deje de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="48c86-198">Copy hello key value tooa safe place, as you won't be able tooaccess it again after you leave hello blade.</span></span> 

    ![Creación de una clave secreta](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a><span data-ttu-id="48c86-200">Asignar una aplicación de RBAC rol tooyour</span><span class="sxs-lookup"><span data-stu-id="48c86-200">Assign an RBAC role tooyour application</span></span>

<span data-ttu-id="48c86-201">tooauthenticate con una entidad de servicio, necesita una aplicación de RBAC rol tooyour tooassign.</span><span class="sxs-lookup"><span data-stu-id="48c86-201">tooauthenticate with a service principal, you need tooassign an RBAC role tooyour application.</span></span> <span data-ttu-id="48c86-202">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="48c86-202">Follow these steps:</span></span>

1. <span data-ttu-id="48c86-203">Hola portal de Azure, navegue toohello cuenta de lote utilizado por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48c86-203">In hello Azure portal, navigate toohello Batch account used by your application.</span></span>
2. <span data-ttu-id="48c86-204">Hola **configuración** hoja de cuenta de lote de hello, seleccione **Control de acceso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="48c86-204">In hello **Settings** blade for hello Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="48c86-205">Haga clic en hello **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="48c86-205">Click hello **Add** button.</span></span> 
4. <span data-ttu-id="48c86-206">De hello **rol** lista desplegable, elija cualquier hello _colaborador_ o _lector_ rol para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48c86-206">From hello **Role** drop-down, choose either hello _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="48c86-207">Para obtener más información sobre estas funciones, vea [empezar a trabajar con Control de acceso basado en roles en el portal de Azure hello](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="48c86-207">For more information on these roles, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="48c86-208">Hola **seleccione** , escriba el nombre de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48c86-208">In hello **Select** field, enter hello name of your application.</span></span> <span data-ttu-id="48c86-209">Seleccione la aplicación de lista de Hola y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="48c86-209">Select your application from hello list, and click **Save**.</span></span>

<span data-ttu-id="48c86-210">La aplicación debe aparecer ahora en la configuración de control de acceso con un rol RBAC asignado.</span><span class="sxs-lookup"><span data-stu-id="48c86-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Asignar una aplicación de RBAC rol tooyour](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="48c86-212">Obtener Id. de inquilino de Hola para Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48c86-212">Get hello tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="48c86-213">Id. de inquilino de Hello identifica el inquilino de Azure AD de Hola que proporciona servicios de autenticación tooyour aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="48c86-213">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="48c86-214">tooget Hola Id. de inquilino, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="48c86-214">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="48c86-215">Hola portal de Azure, seleccione su Active Directory.</span><span class="sxs-lookup"><span data-stu-id="48c86-215">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="48c86-216">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="48c86-216">Click **Properties**.</span></span>
3. <span data-ttu-id="48c86-217">Copiar valor GUID de hello previsto Hola Id. de directorio.</span><span class="sxs-lookup"><span data-stu-id="48c86-217">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="48c86-218">Este valor también se denomina identificador del inquilino Hola.</span><span class="sxs-lookup"><span data-stu-id="48c86-218">This value is also called hello tenant ID.</span></span>

![Id. de directorio Hola](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="48c86-220">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="48c86-220">Code examples</span></span>

<span data-ttu-id="48c86-221">ejemplos de código de Hello en esta sección muestran cómo tooauthenticate con Azure AD mediante la autenticación integrada y con una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="48c86-221">hello code examples in this section show how tooauthenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="48c86-222">Estos ejemplos de código usa .NET pero Hola conceptos son similares para otros idiomas.</span><span class="sxs-lookup"><span data-stu-id="48c86-222">These code examples use .NET, but hello concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="48c86-223">Un token de autenticación de Azure AD expira después de una hora.</span><span class="sxs-lookup"><span data-stu-id="48c86-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="48c86-224">Cuando se usa una larga duración **BatchClient** de objeto, se recomienda que recuperar un token de ADAL en cada solicitud tooensure siempre tiene un token válido.</span><span class="sxs-lookup"><span data-stu-id="48c86-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request tooensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="48c86-225">tooachieve en. NET, escribir un método que recupera Hola símbolo (token) de Azure AD y pasa ese método tooa **BatchTokenCredentials** objeto como un delegado.</span><span class="sxs-lookup"><span data-stu-id="48c86-225">tooachieve this in .NET, write a method that retrieves hello token from Azure AD and pass that method tooa **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="48c86-226">se llama el método de delegado de Hello en cada tooensure servicio de lote toohello de la solicitud que se proporciona un token válido.</span><span class="sxs-lookup"><span data-stu-id="48c86-226">hello delegate method is called on every request toohello Batch service tooensure that a valid token is provided.</span></span> <span data-ttu-id="48c86-227">De forma predeterminada ADAL almacena en caché los tokens, por lo que solo se recuperará un nuevo token de Azure AD si es necesario.</span><span class="sxs-lookup"><span data-stu-id="48c86-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="48c86-228">Para más información, consulte [Escenarios de autenticación para Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="48c86-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="48c86-229">Ejemplo de código: uso de la autenticación integrada de Azure AD con .NET de Batch</span><span class="sxs-lookup"><span data-stu-id="48c86-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="48c86-230">tooauthenticate con la autenticación integrada de .NET de lote, Hola referencia [.NET de lote de Azure](https://www.nuget.org/packages/Azure.Batch/) hello y paquete [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) paquete.</span><span class="sxs-lookup"><span data-stu-id="48c86-230">tooauthenticate with integrated authentication from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="48c86-231">Hola siguientes `using` las instrucciones en el código:</span><span class="sxs-lookup"><span data-stu-id="48c86-231">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="48c86-232">Id. de inquilino de hello referencia extremo de Azure AD en el código, incluidas Hola</span><span class="sxs-lookup"><span data-stu-id="48c86-232">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="48c86-233">tooretrieve Hola Id. de inquilino, siga los pasos de hello descritos en [obtener Id. de inquilino de Hola para Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="48c86-233">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="48c86-234">Extremo del recurso de servicio de referencia Hola por lotes:</span><span class="sxs-lookup"><span data-stu-id="48c86-234">Reference hello Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="48c86-235">Haga referencia a la cuenta de Batch:</span><span class="sxs-lookup"><span data-stu-id="48c86-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="48c86-236">Especifique el Id. de aplicación de hello (Id. de cliente) para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48c86-236">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="48c86-237">Identificador de la aplicación Hello está disponible desde el registro de una aplicación Hola portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="48c86-237">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="48c86-238">Copie también URI especificado durante el proceso de registro de hello de redirección de Hola.</span><span class="sxs-lookup"><span data-stu-id="48c86-238">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="48c86-239">Hola redirección URI especificado en el código debe coincidir con el URI que proporcionó al registrar la aplicación hello de redirección de hello:</span><span class="sxs-lookup"><span data-stu-id="48c86-239">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="48c86-240">Escribir un token de autenticación de devolución de llamada método tooacquire Hola de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c86-240">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="48c86-241">Hola **GetAuthenticationTokenAsync** método de devolución de llamada que se muestra a continuación llama a un usuario que está interactuando con la aplicación hello tooauthenticate ADAL.</span><span class="sxs-lookup"><span data-stu-id="48c86-241">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL tooauthenticate a user who is interacting with hello application.</span></span> <span data-ttu-id="48c86-242">Hola **AcquireTokenAsync** método proporcionado por AAL indicaciones Hola usuario sus credenciales y aplicación hello una vez continúa usuario Hola les proporciona (a menos que ya ha almacenado en caché de credenciales):</span><span class="sxs-lookup"><span data-stu-id="48c86-242">hello **AcquireTokenAsync** method provided by ADAL prompts hello user for their credentials, and hello application proceeds once hello user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="48c86-243">Construir un **BatchTokenCredentials** objeto que toma el delegado de Hola como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="48c86-243">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="48c86-244">Usar esas credenciales tooopen un **BatchClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="48c86-244">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="48c86-245">También puede usarlo **BatchClient** objeto para las operaciones posteriores contra Hola servicio por lotes:</span><span class="sxs-lookup"><span data-stu-id="48c86-245">You can use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="48c86-246">Ejemplo de código: uso de una entidad de servicio de Azure AD con .NET de Batch</span><span class="sxs-lookup"><span data-stu-id="48c86-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="48c86-247">tooauthenticate con una entidad de servicio de lote de. NET, Hola de referencia [.NET de lote de Azure](https://www.nuget.org/packages/Azure.Batch/) hello y paquete [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) paquete.</span><span class="sxs-lookup"><span data-stu-id="48c86-247">tooauthenticate with a service principal from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="48c86-248">Hola siguientes `using` las instrucciones en el código:</span><span class="sxs-lookup"><span data-stu-id="48c86-248">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="48c86-249">Id. de inquilino de hello referencia extremo de Azure AD en el código, incluidas Hola</span><span class="sxs-lookup"><span data-stu-id="48c86-249">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="48c86-250">Cuando se usa una entidad de servicio, debe proporcionar un punto de conexión específico del inquilino.</span><span class="sxs-lookup"><span data-stu-id="48c86-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="48c86-251">tooretrieve Hola Id. de inquilino, siga los pasos de hello descritos en [obtener Id. de inquilino de Hola para Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="48c86-251">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="48c86-252">Extremo del recurso de servicio de referencia Hola por lotes:</span><span class="sxs-lookup"><span data-stu-id="48c86-252">Reference hello Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="48c86-253">Haga referencia a la cuenta de Batch:</span><span class="sxs-lookup"><span data-stu-id="48c86-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="48c86-254">Especifique el Id. de aplicación de hello (Id. de cliente) para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48c86-254">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="48c86-255">Identificador de la aplicación Hello está disponible desde el registro de una aplicación Hola portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="48c86-255">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="48c86-256">Especifique la clave secreta de Hola que copió de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="48c86-256">Specify hello secret key that you copied from hello Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="48c86-257">Escribir un token de autenticación de devolución de llamada método tooacquire Hola de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c86-257">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="48c86-258">Hola **GetAuthenticationTokenAsync** método de devolución de llamada que se muestra aquí llamadas AAL para la autenticación desatendida:</span><span class="sxs-lookup"><span data-stu-id="48c86-258">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="48c86-259">Construir un **BatchTokenCredentials** objeto que toma el delegado de Hola como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="48c86-259">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="48c86-260">Usar esas credenciales tooopen un **BatchClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="48c86-260">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="48c86-261">A continuación, puede usar **BatchClient** objeto para las operaciones posteriores contra Hola servicio por lotes:</span><span class="sxs-lookup"><span data-stu-id="48c86-261">You can then use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="48c86-262">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="48c86-262">Next steps</span></span>

<span data-ttu-id="48c86-263">toolearn más información acerca de Azure AD, vea hello [documentación de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="48c86-263">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="48c86-264">Ejemplos detallados que muestran cómo toouse AAL está disponible en hello [ejemplos de código de Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="48c86-264">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="48c86-265">toolearn más información acerca de las entidades de seguridad de servicio, consulte [aplicación y objetos de entidad de servicio en Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="48c86-265">toolearn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="48c86-266">toocreate un servicio principal mediante hello Azure portal, vea [usar la aplicación de portal toocreate Active Directory y la entidad de servicio que puede tener acceso a recursos](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="48c86-266">toocreate a service principal using hello Azure portal, see [Use portal toocreate Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="48c86-267">Las entidades de servicio también se pueden crear con PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="48c86-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="48c86-268">las aplicaciones de administración de lotes tooauthenticate mediante Azure AD, vea [soluciones de administración de lote autenticarse con Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="48c86-268">tooauthenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

[aad_about]: ../active-directory/active-directory-whatis.md "¿Qué es Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Escenarios de autenticación para Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integración de aplicaciones con Azure Active Directory"
[azure_portal]: http://portal.azure.com
