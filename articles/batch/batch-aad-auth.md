---
title: Uso de Azure Active Directory para autenticar soluciones de servicio de Azure Batch | Microsoft Docs
description: "Batch admite Azure AD para la autenticación desde el servicio de Batch."
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
ms.openlocfilehash: 9c03bde919c46cd301229255c0b12ee69dda6f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="a102e-103">Autenticación de soluciones de servicio de Batch con Active Directory</span><span class="sxs-lookup"><span data-stu-id="a102e-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="a102e-104">Azure Batch admite la autenticación con [Azure Active Directory][aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a102e-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="a102e-105">Azure Active Directory es el directorio basado en la nube multiinquilino y el servicio de administración de identidades de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a102e-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="a102e-106">El propio Azure usa Azure AD para la autenticación de sus clientes, administradores de servicios y usuarios de la organización.</span><span class="sxs-lookup"><span data-stu-id="a102e-106">Azure itself uses Azure AD to authenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="a102e-107">Al utilizar la autenticación de Azure AD con Azure Batch, puede autenticar de una de estas dos maneras:</span><span class="sxs-lookup"><span data-stu-id="a102e-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="a102e-108">Uso de **autenticación integrada** para autenticar un usuario que está interactuando con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-108">By using **integrated authentication** to authenticate a user that is interacting with the application.</span></span> <span data-ttu-id="a102e-109">Una aplicación que use la autenticación integrada recopila las credenciales de un usuario y las usa para autenticar el acceso a los recursos de Batch.</span><span class="sxs-lookup"><span data-stu-id="a102e-109">An application using integrated authentication gathers a user's credentials and uses those credentials to authenticate access to Batch resources.</span></span>
- <span data-ttu-id="a102e-110">Uso de una **entidad de servicio** para autenticar una aplicación desatendida.</span><span class="sxs-lookup"><span data-stu-id="a102e-110">By using a **service principal** to authenticate an unattended application.</span></span> <span data-ttu-id="a102e-111">Una entidad de servicio define la directiva y los permisos de una aplicación para representar la aplicación cuando se accede a los recursos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a102e-111">A service principal defines the policy and permissions for an application in order to represent the application when accessing resources at runtime.</span></span>

<span data-ttu-id="a102e-112">Para más información acerca de Azure AD, consulte la [Documentación de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="a102e-112">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="a102e-113">Modo de autenticación y de asignación de grupo</span><span class="sxs-lookup"><span data-stu-id="a102e-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="a102e-114">Al crear una cuenta de Batch, puede especificar dónde se deben asignar los grupos creados para esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="a102e-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="a102e-115">Puede asignar grupos en la suscripción al servicio de Batch predeterminada o en una suscripción de usuario.</span><span class="sxs-lookup"><span data-stu-id="a102e-115">You can choose to allocate pools either in the default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="a102e-116">Su elección afecta a cómo se autentica el acceso a los recursos de esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="a102e-116">Your choice affects how you authenticate access to resources in that account.</span></span>

- <span data-ttu-id="a102e-117">**Suscripción al servicio de Batch**.</span><span class="sxs-lookup"><span data-stu-id="a102e-117">**Batch service subscription**.</span></span> <span data-ttu-id="a102e-118">De forma predeterminada, los grupos de Batch se asignan en una suscripción del servicio Batch.</span><span class="sxs-lookup"><span data-stu-id="a102e-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="a102e-119">Si elige esta opción, puede autenticar el acceso a los recursos de esa cuenta con [clave compartida](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) o con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a102e-119">If you choose this option, you can authenticate access to resources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="a102e-120">**Suscripción de usuario**.</span><span class="sxs-lookup"><span data-stu-id="a102e-120">**User subscription.**</span></span> <span data-ttu-id="a102e-121">Puede asignar grupos de Batch en una suscripción de usuario que especifique.</span><span class="sxs-lookup"><span data-stu-id="a102e-121">You can choose to allocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="a102e-122">Si elige esta opción, debe autenticarse con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a102e-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="a102e-123">Puntos de conexión para autenticación</span><span class="sxs-lookup"><span data-stu-id="a102e-123">Endpoints for authentication</span></span>

<span data-ttu-id="a102e-124">Para autenticar aplicaciones de Batch con Azure AD, debe incluir algunos puntos de conexión conocidos en el código.</span><span class="sxs-lookup"><span data-stu-id="a102e-124">To authenticate Batch applications with Azure AD, you need to include some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="a102e-125">Punto de conexión de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a102e-125">Azure AD endpoint</span></span>

<span data-ttu-id="a102e-126">El punto de conexión de la autoridad de Azure AD básico es:</span><span class="sxs-lookup"><span data-stu-id="a102e-126">The base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="a102e-127">Para autenticar con Azure AD, use este punto de conexión junto con el identificador de inquilino (identificador del directorio).</span><span class="sxs-lookup"><span data-stu-id="a102e-127">To authenticate with Azure AD, you use this endpoint together with the tenant ID (directory ID).</span></span> <span data-ttu-id="a102e-128">El identificador de inquilino identifica el inquilino de Azure AD que se usará para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="a102e-128">The tenant ID identifies the Azure AD tenant to use for authentication.</span></span> <span data-ttu-id="a102e-129">Para recuperar el identificador de inquilino, siga los pasos descritos en [Obtención del identificador de inquilino de Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="a102e-129">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="a102e-130">El punto de conexión específico del inquilino es necesario al autenticar con una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="a102e-130">The tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="a102e-131">El punto de conexión específico del inquilino es opcional, aunque recomendable, al autenticar mediante autenticación integrada.</span><span class="sxs-lookup"><span data-stu-id="a102e-131">The tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="a102e-132">Sin embargo, también puede utilizar el punto de conexión común de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a102e-132">However, you can also use the Azure AD common endpoint.</span></span> <span data-ttu-id="a102e-133">El punto de conexión común proporciona una interfaz genérica de recopilación de credenciales cuando no se proporciona un inquilino específico.</span><span class="sxs-lookup"><span data-stu-id="a102e-133">The common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="a102e-134">El punto de conexión común es `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="a102e-134">The common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="a102e-135">Para más información sobre los puntos de conexión de Azure AD, consulte [Escenarios de autenticación para Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="a102e-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="a102e-136">Punto de conexión de recursos de Batch</span><span class="sxs-lookup"><span data-stu-id="a102e-136">Batch resource endpoint</span></span>

<span data-ttu-id="a102e-137">Use el **punto de conexión de recursos de Azure Batch** para adquirir un token para autenticar las solicitudes al servicio de Batch:</span><span class="sxs-lookup"><span data-stu-id="a102e-137">Use the **Azure Batch resource endpoint** to acquire a token for authenticating requests to the Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="a102e-138">Registro de la aplicación con un inquilino</span><span class="sxs-lookup"><span data-stu-id="a102e-138">Register your application with a tenant</span></span>

<span data-ttu-id="a102e-139">El primer paso para usar Azure AD para autenticar es registrar la aplicación en un inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a102e-139">The first step in using Azure AD to authenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="a102e-140">El registro de la aplicación le permite llamar a la [biblioteca de autenticación de Active Directory] [ aad_adal] (ADAL) de Azure desde el código.</span><span class="sxs-lookup"><span data-stu-id="a102e-140">Registering your application enables you to call the Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="a102e-141">La ADAL proporciona una API para autenticar con Azure AD desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-141">The ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="a102e-142">La aplicación debe registrarse tanto si tiene previsto usar la autenticación integrada como una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="a102e-142">Registering your application is required whether you plan to use integrated authentication or a service principal.</span></span>

<span data-ttu-id="a102e-143">Al registrar la aplicación, facilita información acerca de la aplicación a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a102e-143">When you register your application, you supply information about your application to Azure AD.</span></span> <span data-ttu-id="a102e-144">Azure AD proporciona un identificador de aplicación que se utiliza para asociar la aplicación con Azure AD en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a102e-144">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="a102e-145">Para conocer más detalles acerca del identificador de la aplicación, consulte [Objetos de aplicación y de entidad de servicio de Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="a102e-145">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="a102e-146">Siga los pasos que aparecen en la sección [Incorporación de una aplicación](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) en [Integración de aplicaciones con Azure Active Directory][aad_integrate] para registrar la aplicación de Batch.</span><span class="sxs-lookup"><span data-stu-id="a102e-146">To register your Batch application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="a102e-147">Si registra la aplicación como una aplicación nativa, puede especificar cualquier URI válido para el **URI de redirección**.</span><span class="sxs-lookup"><span data-stu-id="a102e-147">If you register your application as a Native Application, you can specify any valid URI for the **Redirect URI**.</span></span> <span data-ttu-id="a102e-148">No es necesario que sea un punto de conexión real.</span><span class="sxs-lookup"><span data-stu-id="a102e-148">It does not need to be a real endpoint.</span></span>

<span data-ttu-id="a102e-149">Una vez registrada la aplicación, verá el identificador de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="a102e-149">After you've registered your application, you'll see the application ID:</span></span>

![Registro de la aplicación de Batch con Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="a102e-151">Para más información sobre el registro de una aplicación, consulte [Escenarios de autenticación para Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="a102e-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-the-tenant-id-for-your-active-directory"></a><span data-ttu-id="a102e-152">Obtención del identificador de inquilino para Active Directory</span><span class="sxs-lookup"><span data-stu-id="a102e-152">Get the tenant ID for your Active Directory</span></span>

<span data-ttu-id="a102e-153">El identificador de inquilino identifica al inquilino de Azure AD que proporciona servicios de autenticación a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-153">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="a102e-154">Para obtener el identificador de inquilino, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a102e-154">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="a102e-155">En Azure Portal, seleccione Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a102e-155">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="a102e-156">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="a102e-156">Click **Properties**.</span></span>
3. <span data-ttu-id="a102e-157">Copie el valor GUID proporcionado para el identificador de directorio.</span><span class="sxs-lookup"><span data-stu-id="a102e-157">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="a102e-158">Este valor también se denomina identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="a102e-158">This value is also called the tenant ID.</span></span>

![Copia del identificador del directorio](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="a102e-160">Uso de autenticación integrada</span><span class="sxs-lookup"><span data-stu-id="a102e-160">Use integrated authentication</span></span>

<span data-ttu-id="a102e-161">Para autenticar mediante autenticación integrada, deberá conceder a la aplicación permisos para conectarse a la API del servicio de Batch.</span><span class="sxs-lookup"><span data-stu-id="a102e-161">To authenticate with integrated authentication, you need to grant your application permissions to connect to the Batch service API.</span></span> <span data-ttu-id="a102e-162">Este paso permite a la aplicación autenticar llamadas en la API del servicio de Batch con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a102e-162">This step enables your application to authenticate calls to the Batch service API with Azure AD.</span></span>

<span data-ttu-id="a102e-163">Una vez que haya [registrado la aplicación](#register-your-application-with-an-azure-ad-tenant), siga estos pasos en Azure Portal para concederle acceso al servicio de Batch:</span><span class="sxs-lookup"><span data-stu-id="a102e-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in the Azure portal to grant it access to the Batch service:</span></span>

1. <span data-ttu-id="a102e-164">En el panel de navegación izquierdo de Azure Portal, elija **Más servicios** y haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a102e-164">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="a102e-165">Busque el nombre de la aplicación en la lista de registros de aplicación:</span><span class="sxs-lookup"><span data-stu-id="a102e-165">Search for the name of your application in the list of app registrations:</span></span>

    ![Buscar el nombre de la aplicación](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="a102e-167">Abra la hoja **Configuración** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-167">Open the **Settings** blade for your application.</span></span> <span data-ttu-id="a102e-168">En la sección **Acceso de API**, seleccione **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="a102e-168">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="a102e-169">En la hoja **Permisos necesarios**, haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a102e-169">In the **Required permissions** blade, click the **Add** button.</span></span>
5. <span data-ttu-id="a102e-170">En el paso 1, busque Batch API.</span><span class="sxs-lookup"><span data-stu-id="a102e-170">In step 1, search for the Batch API.</span></span> <span data-ttu-id="a102e-171">Busque cada una de estas cadenas hasta que encuentre la API:</span><span class="sxs-lookup"><span data-stu-id="a102e-171">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="a102e-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="a102e-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="a102e-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="a102e-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="a102e-174">Los inquilinos más recientes de Azure AD pueden utilizar este nombre.</span><span class="sxs-lookup"><span data-stu-id="a102e-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="a102e-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** es el identificador de Batch API.</span><span class="sxs-lookup"><span data-stu-id="a102e-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 
6. <span data-ttu-id="a102e-176">Una vez que encuentre Batch API, selecciónela y haga clic en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="a102e-176">Once you find the Batch API, select it and click the **Select** button.</span></span>
6. <span data-ttu-id="a102e-177">En el paso 2, active la casilla de verificación situada junto a **Acceder al servicio Azure Batch** y haga clic en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="a102e-177">In step 2, select the check box next to **Access Azure Batch Service** and click the **Select** button.</span></span>
7. <span data-ttu-id="a102e-178">Haga clic en el botón **Listo**.</span><span class="sxs-lookup"><span data-stu-id="a102e-178">Click the **Done** button.</span></span>

<span data-ttu-id="a102e-179">La hoja **Permisos necesarios** muestra ahora que la aplicación de Azure AD tiene acceso tanto a ADAL como a la API de servicio de Batch.</span><span class="sxs-lookup"><span data-stu-id="a102e-179">The **Required Permissions** blade now shows that your Azure AD application has access to both ADAL and the Batch service API.</span></span> <span data-ttu-id="a102e-180">La primera vez que registra la aplicación con Azure AD, se conceden permisos a ADAL automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a102e-180">Permissions are granted to ADAL automatically when you first register your app with Azure AD.</span></span>

![Concesión de permisos de API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="a102e-182">Uso de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="a102e-182">Use a service principal</span></span> 

<span data-ttu-id="a102e-183">Para autenticar una aplicación que se ejecute desatendida, utilice una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="a102e-183">To authenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="a102e-184">Una vez que haya registrado la aplicación, siga estos pasos en Azure Portal para configurar una entidad de servicio:</span><span class="sxs-lookup"><span data-stu-id="a102e-184">After you've registered your application, follow these steps in the Azure portal to configure a service principal:</span></span>

1. <span data-ttu-id="a102e-185">Solicite una clave secreta para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="a102e-186">Asigne un rol RBAC a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-186">Assign an RBAC role to your application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="a102e-187">Solicitud de una clave secreta para la aplicación</span><span class="sxs-lookup"><span data-stu-id="a102e-187">Request a secret key for your application</span></span>

<span data-ttu-id="a102e-188">Cuando la aplicación se autentica con una entidad de servicio, envía el identificador de la aplicación y una clave secreta a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a102e-188">When your application authenticates with a service principal, it sends both the application ID and a secret key to Azure AD.</span></span> <span data-ttu-id="a102e-189">Debe crear y copiar la clave secreta que usará desde el código.</span><span class="sxs-lookup"><span data-stu-id="a102e-189">You'll need to create and copy the secret key to use from your code.</span></span>

<span data-ttu-id="a102e-190">Siga estos pasos en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="a102e-190">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="a102e-191">En el panel de navegación izquierdo de Azure Portal, elija **Más servicios** y haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a102e-191">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="a102e-192">Busque el nombre de la aplicación en la lista de registros de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a102e-192">Search for the name of your application in the list of app registrations.</span></span>
3. <span data-ttu-id="a102e-193">Se mostrará la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="a102e-193">Display the **Settings** blade.</span></span> <span data-ttu-id="a102e-194">En la sección **Acceso de API**, seleccione **Claves**.</span><span class="sxs-lookup"><span data-stu-id="a102e-194">In the **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="a102e-195">Para crear una clave, escriba una descripción de la clave.</span><span class="sxs-lookup"><span data-stu-id="a102e-195">To create a key, enter a description for the key.</span></span> <span data-ttu-id="a102e-196">A continuación, seleccione una duración para la clave de uno o dos años.</span><span class="sxs-lookup"><span data-stu-id="a102e-196">Then select a duration for the key of either one or two years.</span></span> 
5. <span data-ttu-id="a102e-197">Haga clic en el botón **Guardar** para crear y mostrar la clave.</span><span class="sxs-lookup"><span data-stu-id="a102e-197">Click the **Save** button to create and display the key.</span></span> <span data-ttu-id="a102e-198">Copie el valor de la clave en un lugar seguro, puesto que no podrá acceder a ella nuevamente después de abandonar la hoja.</span><span class="sxs-lookup"><span data-stu-id="a102e-198">Copy the key value to a safe place, as you won't be able to access it again after you leave the blade.</span></span> 

    ![Creación de una clave secreta](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-to-your-application"></a><span data-ttu-id="a102e-200">Asignación de un rol RBAC a la aplicación</span><span class="sxs-lookup"><span data-stu-id="a102e-200">Assign an RBAC role to your application</span></span>

<span data-ttu-id="a102e-201">Para autenticarse con una entidad de servicio, debe asignar un rol RBAC a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-201">To authenticate with a service principal, you need to assign an RBAC role to your application.</span></span> <span data-ttu-id="a102e-202">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a102e-202">Follow these steps:</span></span>

1. <span data-ttu-id="a102e-203">En Azure Portal, vaya a la cuenta de Batch utilizada por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-203">In the Azure portal, navigate to the Batch account used by your application.</span></span>
2. <span data-ttu-id="a102e-204">En la hoja **Configuración** de la cuenta de Batch, seleccione **Control de acceso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="a102e-204">In the **Settings** blade for the Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="a102e-205">Haga clic en el botón **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="a102e-205">Click the **Add** button.</span></span> 
4. <span data-ttu-id="a102e-206">En el menú desplegable **Rol**, elija el rol _Colaborador_ o _Lector_ para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-206">From the **Role** drop-down, choose either the _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="a102e-207">Para más información sobre estos roles, consulte [Introducción al control de acceso basado en roles en Azure Portal](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="a102e-207">For more information on these roles, see [Get started with Role-Based Access Control in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="a102e-208">Escriba el nombre de la aplicación en el campo **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="a102e-208">In the **Select** field, enter the name of your application.</span></span> <span data-ttu-id="a102e-209">Seleccione la aplicación de la lista y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a102e-209">Select your application from the list, and click **Save**.</span></span>

<span data-ttu-id="a102e-210">La aplicación debe aparecer ahora en la configuración de control de acceso con un rol RBAC asignado.</span><span class="sxs-lookup"><span data-stu-id="a102e-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Asignación de un rol RBAC a la aplicación](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-the-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="a102e-212">Obtención del identificador de inquilino para Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a102e-212">Get the tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="a102e-213">El identificador de inquilino identifica al inquilino de Azure AD que proporciona servicios de autenticación a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-213">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="a102e-214">Para obtener el identificador de inquilino, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a102e-214">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="a102e-215">En Azure Portal, seleccione Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a102e-215">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="a102e-216">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="a102e-216">Click **Properties**.</span></span>
3. <span data-ttu-id="a102e-217">Copie el valor GUID proporcionado para el identificador de directorio.</span><span class="sxs-lookup"><span data-stu-id="a102e-217">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="a102e-218">Este valor también se denomina identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="a102e-218">This value is also called the tenant ID.</span></span>

![Copia del identificador del directorio](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="a102e-220">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="a102e-220">Code examples</span></span>

<span data-ttu-id="a102e-221">Los ejemplos de código de esta sección muestran cómo autenticar con Azure AD mediante la autenticación integrada y con una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="a102e-221">The code examples in this section show how to authenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="a102e-222">Estos ejemplos de código usan .NET, pero los conceptos son similares para otros lenguajes.</span><span class="sxs-lookup"><span data-stu-id="a102e-222">These code examples use .NET, but the concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="a102e-223">Un token de autenticación de Azure AD expira después de una hora.</span><span class="sxs-lookup"><span data-stu-id="a102e-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="a102e-224">Cuando se usa un objeto **BatchClient** de larga duración, se recomienda que recupere un token de ADAL en cada solicitud para asegurarse de que siempre tiene un token válido.</span><span class="sxs-lookup"><span data-stu-id="a102e-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request to ensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="a102e-225">Para lograr esto en. NET, escriba un método que recupere el token de Azure AD y pase ese método a un objeto **BatchTokenCredentials** como un delegado.</span><span class="sxs-lookup"><span data-stu-id="a102e-225">To achieve this in .NET, write a method that retrieves the token from Azure AD and pass that method to a **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="a102e-226">El método delegado se llama en cada solicitud al servicio Batch para asegurarse de que se proporciona un token válido.</span><span class="sxs-lookup"><span data-stu-id="a102e-226">The delegate method is called on every request to the Batch service to ensure that a valid token is provided.</span></span> <span data-ttu-id="a102e-227">De forma predeterminada ADAL almacena en caché los tokens, por lo que solo se recuperará un nuevo token de Azure AD si es necesario.</span><span class="sxs-lookup"><span data-stu-id="a102e-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="a102e-228">Para más información, consulte [Escenarios de autenticación para Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="a102e-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="a102e-229">Ejemplo de código: uso de la autenticación integrada de Azure AD con .NET de Batch</span><span class="sxs-lookup"><span data-stu-id="a102e-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="a102e-230">Para autenticar mediante la autenticación integrada de .NET de Batch, consulte el paquete de [.NET de Azure Batch](https://www.nuget.org/packages/Azure.Batch/) y el paquete de [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).</span><span class="sxs-lookup"><span data-stu-id="a102e-230">To authenticate with integrated authentication from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="a102e-231">Incluya las siguientes instrucciones `using` en el código:</span><span class="sxs-lookup"><span data-stu-id="a102e-231">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="a102e-232">Haga referencia al punto de conexión de Azure AD en el código, incluido el identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="a102e-232">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="a102e-233">Para recuperar el identificador de inquilino, siga los pasos descritos en [Obtención del identificador de inquilino de Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="a102e-233">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="a102e-234">Haga referencia al punto de conexión del recurso para el servicio de Batch:</span><span class="sxs-lookup"><span data-stu-id="a102e-234">Reference the Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="a102e-235">Haga referencia a la cuenta de Batch:</span><span class="sxs-lookup"><span data-stu-id="a102e-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="a102e-236">Especifique el identificador (Id. de cliente) de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-236">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="a102e-237">El identificador de la aplicación está disponible en el registro de la aplicación en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="a102e-237">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="a102e-238">Copie también el URI de redirección especificado durante el proceso de registro.</span><span class="sxs-lookup"><span data-stu-id="a102e-238">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="a102e-239">El URI de redireccionamiento especificado en el código debe coincidir con el URI de redireccionamiento que proporcionó al registrar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="a102e-239">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="a102e-240">Escriba un método de devolución de llamada para adquirir el token de autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a102e-240">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="a102e-241">El método de devolución de llamada **GetAuthenticationTokenAsync** que se menciona aquí llama a ADAL para autenticar a un usuario que está interactuando con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-241">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL to authenticate a user who is interacting with the application.</span></span> <span data-ttu-id="a102e-242">El método **AcquireTokenAsync** proporcionado por ADAL solicita al usuario sus credenciales y la aplicación se inicia una vez que el usuario las proporciona (a menos que ya tenga credenciales en caché):</span><span class="sxs-lookup"><span data-stu-id="a102e-242">The **AcquireTokenAsync** method provided by ADAL prompts the user for their credentials, and the application proceeds once the user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire the authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="a102e-243">Construya un objeto **BatchTokenCredentials** que tome el delegado como parámetro.</span><span class="sxs-lookup"><span data-stu-id="a102e-243">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="a102e-244">Use esas credenciales para abrir un objeto **BatchClient**.</span><span class="sxs-lookup"><span data-stu-id="a102e-244">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="a102e-245">Puede usar ese objeto **BatchClient** para las operaciones posteriores del servicio de Batch:</span><span class="sxs-lookup"><span data-stu-id="a102e-245">You can use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

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

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="a102e-246">Ejemplo de código: uso de una entidad de servicio de Azure AD con .NET de Batch</span><span class="sxs-lookup"><span data-stu-id="a102e-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="a102e-247">Para autenticar mediante una entidad de servicio de .NET de Batch, consulte el paquete de [.NET de Azure Batch](https://www.nuget.org/packages/Azure.Batch/) y el paquete de [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).</span><span class="sxs-lookup"><span data-stu-id="a102e-247">To authenticate with a service principal from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="a102e-248">Incluya las siguientes instrucciones `using` en el código:</span><span class="sxs-lookup"><span data-stu-id="a102e-248">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="a102e-249">Haga referencia al punto de conexión de Azure AD en el código, incluido el identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="a102e-249">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="a102e-250">Cuando se usa una entidad de servicio, debe proporcionar un punto de conexión específico del inquilino.</span><span class="sxs-lookup"><span data-stu-id="a102e-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="a102e-251">Para recuperar el identificador de inquilino, siga los pasos descritos en [Obtención del identificador de inquilino de Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="a102e-251">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="a102e-252">Haga referencia al punto de conexión del recurso para el servicio de Batch:</span><span class="sxs-lookup"><span data-stu-id="a102e-252">Reference the Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="a102e-253">Haga referencia a la cuenta de Batch:</span><span class="sxs-lookup"><span data-stu-id="a102e-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="a102e-254">Especifique el identificador (Id. de cliente) de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a102e-254">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="a102e-255">El identificador de la aplicación está disponible en el registro de la aplicación en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="a102e-255">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="a102e-256">Especifique la clave secreta que copió de Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="a102e-256">Specify the secret key that you copied from the Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="a102e-257">Escriba un método de devolución de llamada para adquirir el token de autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a102e-257">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="a102e-258">El método de devolución de llamada **GetAuthenticationTokenAsync** que se menciona aquí llama a ADAL para una autenticación desatendida:</span><span class="sxs-lookup"><span data-stu-id="a102e-258">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="a102e-259">Construya un objeto **BatchTokenCredentials** que tome el delegado como parámetro.</span><span class="sxs-lookup"><span data-stu-id="a102e-259">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="a102e-260">Use esas credenciales para abrir un objeto **BatchClient**.</span><span class="sxs-lookup"><span data-stu-id="a102e-260">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="a102e-261">A continuación, puede usar ese objeto **BatchClient** para las operaciones posteriores del servicio de Batch:</span><span class="sxs-lookup"><span data-stu-id="a102e-261">You can then use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a102e-262">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a102e-262">Next steps</span></span>

<span data-ttu-id="a102e-263">Para más información acerca de Azure AD, consulte la [Documentación de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="a102e-263">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="a102e-264">Puede consultar los ejemplos detallados sobre el uso de ADAL que están disponibles en la biblioteca de [ejemplos de código de Azure](https://azure.microsoft.com/resources/samples/?service=active-directory).</span><span class="sxs-lookup"><span data-stu-id="a102e-264">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="a102e-265">Para más información acerca de las entidades de servicio, consulte [Objetos de aplicación y de entidad de servicio de Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="a102e-265">To learn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="a102e-266">Para crear una entidad de servicio mediante Azure Portal, consulte [Uso del portal para crear una aplicación de Azure Active Directory y una entidad de servicio con acceso a los recursos](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a102e-266">To create a service principal using the Azure portal, see [Use portal to create Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="a102e-267">Las entidades de servicio también se pueden crear con PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="a102e-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="a102e-268">Para autenticar aplicaciones de administración de Batch con Azure AD, consulte [Autenticación de soluciones de administración de Batch con Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="a102e-268">To authenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

<span data-ttu-id="a102e-269">[aad_about]: ../active-directory/active-directory-whatis.md "¿Qué es Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="a102e-269">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="a102e-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Escenarios de autenticación para Azure AD"</span><span class="sxs-lookup"><span data-stu-id="a102e-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="a102e-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integración de aplicaciones con Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="a102e-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[azure_portal]: http://portal.azure.com
