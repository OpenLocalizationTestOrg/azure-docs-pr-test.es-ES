---
title: Aplicaciones, permisos y consentimiento en Azure Active Directory | Microsoft Docs
description: "Azure AD Connect integrará sus directorios locales con Azure Active Directory. Esto le permite proporcionar una identidad común para las aplicaciones de Office 365, Azure y SaaS integradas con Azure AD."
keywords: "introducción a Azure AD, aplicaciones, qué es Azure AD Connect, instalación de active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 6f6baf5e1538fb280a899065c64ca5688473c04a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="9ea18-105">Aplicaciones, permisos y consentimiento en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ea18-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="9ea18-106">Dentro de Azure Active Directory puede agregar aplicaciones a su directorio.</span><span class="sxs-lookup"><span data-stu-id="9ea18-106">Within Azure Active Directory, you can add applications to your directory.</span></span>  <span data-ttu-id="9ea18-107">Las aplicaciones pueden variar según el tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9ea18-107">The applications can vary depending on the type of application.</span></span>  <span data-ttu-id="9ea18-108">Para ver las aplicaciones en el portal clásico, seleccione un directorio y elija las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9ea18-108">To view applications in the classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="9ea18-109">Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="9ea18-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="9ea18-110">Tipos de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="9ea18-110">Types of apps</span></span>

1. <span data-ttu-id="9ea18-111">**Aplicaciones de inquilino único**</span><span class="sxs-lookup"><span data-stu-id="9ea18-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="9ea18-112">**Aplicaciones de inquilino único**: a menudo denominadas también aplicaciones de línea de negocio (LOB).</span><span class="sxs-lookup"><span data-stu-id="9ea18-112">**Single-tenant apps** - Often referred to as line-of-business (LOB) apps.</span></span> <span data-ttu-id="9ea18-113">Este es el caso en el que alguien de la organización desarrolla su propia aplicación y quiere que otros usuarios de esta puedan iniciar sesión en ella.</span><span class="sxs-lookup"><span data-stu-id="9ea18-113">This is the case where someone within your organization develops their own app, and would like users in the organization to be able to sign in to the app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="9ea18-114">**Aplicaciones de proxy de aplicación**: al exponer una aplicación local con el proxy de aplicación de Azure AD, se registra una aplicación de inquilino único en su inquilino (además del servicio de proxy de aplicación).</span><span class="sxs-lookup"><span data-stu-id="9ea18-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition to the App Proxy service).</span></span> <span data-ttu-id="9ea18-115">Esta aplicación es la que representará la aplicación local en todas las interacciones en la nube (por ejemplo, en la autenticación).</span><span class="sxs-lookup"><span data-stu-id="9ea18-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="9ea18-116">(Proxy de aplicación requiere Azure AD Basic o superior).</span><span class="sxs-lookup"><span data-stu-id="9ea18-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="9ea18-117">**Aplicaciones multiinquilino**</span><span class="sxs-lookup"><span data-stu-id="9ea18-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="9ea18-118">**Aplicaciones multiinquilino a las que otras personas puedan dar su consentimiento**: son parecidas a las "aplicaciones de inquilino único que desarrolla la organización".</span><span class="sxs-lookup"><span data-stu-id="9ea18-118">**Multi-tenant apps which others can consent to** - similar to “single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="9ea18-119">La diferencia principal (además de la lógica de la propia aplicación) es que los usuarios de otros inquilinos pueden también dar su consentimiento e iniciar sesión en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9ea18-119">The main difference (besides the logic in the app itself) is that users from other tenants can also consent to and sign in to the app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="9ea18-120">**Aplicaciones multiinquilino que desarrollan otros, a las que Contoso puede dar consentimiento**.</span><span class="sxs-lookup"><span data-stu-id="9ea18-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="9ea18-121">(O "aplicaciones consentidas", para abreviar). Esto es el otro lado de las "aplicaciones multiinquilino que desarrolla su organización".</span><span class="sxs-lookup"><span data-stu-id="9ea18-121">(Or “consented apps”, for short.) This is the flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="9ea18-122">Cuando otra organización desarrolla una aplicación multiinquilino, los usuarios de su organización pueden dar consentimiento a la aplicación e iniciar sesión en ella.</span><span class="sxs-lookup"><span data-stu-id="9ea18-122">When another organization develops a multi-tenant app, users of your organization can consent to the app and sign in to it.</span></span>
    - <span data-ttu-id="9ea18-123">**Aplicaciones propias de Microsoft**: las aplicaciones que representan los servicios de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9ea18-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="9ea18-124">El consentimiento se basa en el hecho de que debe registrarse para acceder al servicio.</span><span class="sxs-lookup"><span data-stu-id="9ea18-124">Consent is driven by the fact that you sign up for the service.</span></span> <span data-ttu-id="9ea18-125">Algunas veces existe una lógica y una experiencia de usuario para determinadas aplicaciones propias que se usa a menudo a la hora de establecer directivas relacionadas con el acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9ea18-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access to the app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="9ea18-126">**Aplicaciones integradas previamente**: aplicaciones disponibles en la Galería de aplicaciones de Azure AD que puede agregar a su directorio para proporcionar un inicio de sesión único (y en algunos casos, aprovisionamiento) en aplicaciones SaaS populares.</span><span class="sxs-lookup"><span data-stu-id="9ea18-126">**Pre-integrated apps** - Apps available in the Azure AD App Gallery, which you can add to your directory to provide single sign-on (and in some cases, provisioning) to popular SaaS apps.</span></span>
    - <span data-ttu-id="9ea18-127">**Inicio de sesión único de Azure AD**: inicio de sesión único "real" para las aplicaciones que se pueden integrar con Azure AD, mediante un protocolo de inicio de sesión compatible como SAML 2.0 o OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="9ea18-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="9ea18-128">El asistente le guiará a través del proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="9ea18-128">The wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="9ea18-129">**Inicio de sesión único con contraseña**: Azure AD almacena de forma segura las credenciales del usuario para la aplicación, y la extensión del explorador de acceso de la aplicación de Azure AD "inserta" estas credenciales en el formulario de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9ea18-129">**Password single sign-on**: Azure AD securely stores the user’s credentials for the app, and the credentials are “injected” into the sign-in form by the Azure AD App Access browser extension.</span></span> <span data-ttu-id="9ea18-130">A este proceso también se le conoce como "almacenamiento de contraseñas".</span><span class="sxs-lookup"><span data-stu-id="9ea18-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="9ea18-131">Permisos</span><span class="sxs-lookup"><span data-stu-id="9ea18-131">Permissions</span></span>

<span data-ttu-id="9ea18-132">Cuando se registra una aplicación, el usuario que realiza el registro (es decir, el desarrollador) define los permisos y recursos a los que la aplicación necesita acceder.</span><span class="sxs-lookup"><span data-stu-id="9ea18-132">When an app is registered, the user performing the app registration (that is, the developer) defines which permissions the app needs access to, and which resources.</span></span> <span data-ttu-id="9ea18-133">(Los recursos, por sí mismos, se definen como otras aplicaciones). Por ejemplo, alguien que está compilando una aplicación de lector de correo electrónico, puede indicar que su aplicación requiere el permiso de "Acceso a los buzones como el usuario que inició sesión" en el recurso "Office 365 Exchange Online":</span><span class="sxs-lookup"><span data-stu-id="9ea18-133">(The resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires the “Access mailboxes as the signed-in user” permission in the “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="9ea18-134">Para que una aplicación (el cliente) solicite un permiso determinado desde otra aplicación (el recurso), el desarrollador de la aplicación del recurso debe definir los permisos que existen.</span><span class="sxs-lookup"><span data-stu-id="9ea18-134">In order for one app (the client) to request a certain permission from another app (the resource), the developer of the resource app defines the permissions that exist.</span></span> <span data-ttu-id="9ea18-135">En nuestro ejemplo, Microsoft, el propietario de la aplicación del recurso "Office 365 Exchange Online", ha definido un permiso denominado "Acceso a los buzones como el usuario que inició sesión".</span><span class="sxs-lookup"><span data-stu-id="9ea18-135">In our example, Microsoft, the owner of the “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as the signed-in user”.</span></span>

<span data-ttu-id="9ea18-136">Al definir los permisos, el desarrollador de la aplicación debe definir si se puede dar consentimiento al permiso o si se requiere el consentimiento del administrador.</span><span class="sxs-lookup"><span data-stu-id="9ea18-136">When defining permissions, the app developer must define if the permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="9ea18-137">Esto permite a los desarrolladores que los usuarios puedan dar consentimiento a sus propias aplicaciones solicitando únicamente permisos con bajo nivel de confidencialidad, pero requiere que los administradores den el consentimiento para permisos de mayor nivel.</span><span class="sxs-lookup"><span data-stu-id="9ea18-137">This allows developers to allow users to consent on their own to apps requesting only low-sensitivity permissions, but require admins to consent to more sensitive permissions.</span></span> <span data-ttu-id="9ea18-138">Por ejemplo, se ha definido la aplicación del recurso "Azure Active Directory" para que los usuarios pueden dar consentimiento a las aplicaciones, solicitando permisos limitados de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="9ea18-138">For example, the “Azure Active Directory” resource app, has been defined, so users can consent to apps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="9ea18-139">Sin embargo, se requiere el consentimiento del administrador para conseguir permisos completos de lectura y para todos los permisos de escritura.</span><span class="sxs-lookup"><span data-stu-id="9ea18-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="9ea18-140">Puesto que no se autentican clientes nativos, una aplicación que se define como una aplicación de cliente nativo solo puede solicitar permisos delegados.</span><span class="sxs-lookup"><span data-stu-id="9ea18-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="9ea18-141">Esto significa que siempre debe haber un usuario real implicado en la obtención de un token.</span><span class="sxs-lookup"><span data-stu-id="9ea18-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="9ea18-142">Las aplicaciones web y API web (clientes confidenciales), siempre se deben autenticar con Azure AD al acceder a un token.</span><span class="sxs-lookup"><span data-stu-id="9ea18-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="9ea18-143">Esto significa que también tienen la posibilidad de solicitar permisos de solo aplicación.</span><span class="sxs-lookup"><span data-stu-id="9ea18-143">Meaning they also have the possibility of requesting app-only permissions.</span></span> <span data-ttu-id="9ea18-144">Por ejemplo, si un servicio back-end necesita autenticarse en otro servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="9ea18-144">For example, if one back-end service needs to authenticate to another back-end service.</span></span> <span data-ttu-id="9ea18-145">Las aplicaciones que solicitan permisos de solo aplicación requieren siempre el consentimiento del administrador.</span><span class="sxs-lookup"><span data-stu-id="9ea18-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="9ea18-146">En resumen:</span><span class="sxs-lookup"><span data-stu-id="9ea18-146">Summarizing:</span></span>



- <span data-ttu-id="9ea18-147">Una aplicación (cliente) indica los permisos que necesita para otras aplicaciones (recursos).</span><span class="sxs-lookup"><span data-stu-id="9ea18-147">An app (client) states the permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="9ea18-148">Una aplicación (recurso) indica qué permisos se exponen a otras aplicaciones (clientes).</span><span class="sxs-lookup"><span data-stu-id="9ea18-148">An app (resource) states what permissions are exposed to other apps (clients).</span></span>
- <span data-ttu-id="9ea18-149">Un permiso puede ser un permiso de solo aplicación o un permiso delegado.</span><span class="sxs-lookup"><span data-stu-id="9ea18-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="9ea18-150">Un permiso delegado se puede marcar para indicar que "permite el consentimiento del usuario" o que "requiere el consentimiento del administrador".</span><span class="sxs-lookup"><span data-stu-id="9ea18-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="9ea18-151">Una aplicación puede comportarse como un cliente (declarando que requiere permisos a un recurso), como un recurso (declarando los permisos que expone) o como ambos.</span><span class="sxs-lookup"><span data-stu-id="9ea18-151">An app can behave as a client (by declaring that it needs permissions to a resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="9ea18-152">Controles</span><span class="sxs-lookup"><span data-stu-id="9ea18-152">Controls</span></span>

<span data-ttu-id="9ea18-153">La siguiente es una lista de los diferentes controles de administración disponibles para este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="9ea18-153">The following is a list of the different admin controls available for all this behavior.</span></span> <span data-ttu-id="9ea18-154">Se puede obtener acceso a los controles de administración en el portal clásico desde la opción de configuración del directorio.</span><span class="sxs-lookup"><span data-stu-id="9ea18-154">The admin controls can be accessed in the classic portal from configure under the directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="9ea18-155">En Azure Portal en **Administrar**, **Configuración de usuario**.</span><span class="sxs-lookup"><span data-stu-id="9ea18-155">In the Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="9ea18-156">Puede controlar si los usuarios pueden dar consentimiento a aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="9ea18-156">You can control whether users can consent to apps:</span></span>

<span data-ttu-id="9ea18-157">En el portal clásico, seleccione **Users may give applications permissions to access their data**(Los usuarios pueden otorgar permisos para la aplicación para tener acceso a los datos).
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="9ea18-157">In the classic portal, select **Users may give applications permissions to access their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="9ea18-158">En Azure Portal, seleccione **Los usuarios pueden permitir que las aplicaciones accedan a sus datos**.</span><span class="sxs-lookup"><span data-stu-id="9ea18-158">In the Azure portal, select **users can allow apps to access their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="9ea18-159">Puede controlar si los usuarios pueden registrar sus propias aplicaciones de línea de negocio de inquilino único: en el portal clásico, seleccione **Los usuarios pueden agregar aplicaciones integradas**.
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="9ea18-159">You can control whether users can register their own single-tenant LOB apps: In the classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="9ea18-160">En Azure Portal, seleccione **Los usuarios pueden permitir que las aplicaciones accedan a sus datos**.</span><span class="sxs-lookup"><span data-stu-id="9ea18-160">In the Azure portal, select **users can allow apps to access their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="9ea18-161">Incluso si permite que los usuarios registren las aplicaciones de línea de negocio de inquilino único, hay límites en lo que se puede registrar.</span><span class="sxs-lookup"><span data-stu-id="9ea18-161">Even if you do allow users to register single-tenant LOB apps, there are limits to what can be registered.</span></span>  
><span data-ttu-id="9ea18-162">Por ejemplo, los desarrolladores que no son administradores de directorios.</span><span class="sxs-lookup"><span data-stu-id="9ea18-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="9ea18-163">Los usuarios no pueden hacer que una aplicación de inquilino único se convierta en una aplicación multiinquilino.</span><span class="sxs-lookup"><span data-stu-id="9ea18-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="9ea18-164">Al registrar aplicaciones de línea de negocio de inquilino único, los usuarios no pueden solicitar permisos de solo aplicación para otras aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9ea18-164">When registering single-tenant LOB apps, users cannot request app-only permissions to other apps.</span></span>
>- <span data-ttu-id="9ea18-165">Al registrar aplicaciones de línea de negocio de inquilino único, los usuarios no pueden solicitar permisos delegados para otras aplicaciones si esos permisos requieren el consentimiento del administrador.</span><span class="sxs-lookup"><span data-stu-id="9ea18-165">When registering single-tenant LOB apps, users cannot request delegated permissions to other apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="9ea18-166">Los usuarios no pueden realizar cambios en las aplicaciones de las que no son propietarios.</span><span class="sxs-lookup"><span data-stu-id="9ea18-166">Users cannot make changes to apps that they are not owners of.</span></span>



- <span data-ttu-id="9ea18-167">Puede controlar si los usuarios pueden por sí mismos agregar aplicaciones previamente integradas que utilizan el inicio de sesión único con contraseña (proceso también conocido como "almacenamiento de contraseña") ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="9ea18-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="9ea18-168">Puede controlar en qué condiciones se puede tener acceso a las aplicaciones (es decir, un acceso condicional).</span><span class="sxs-lookup"><span data-stu-id="9ea18-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="9ea18-169">Tenga en cuenta que esto se aplica a la aplicación cliente y a la aplicación de recurso.</span><span class="sxs-lookup"><span data-stu-id="9ea18-169">Be aware this applies both to the client app and to the resource app.</span></span> <span data-ttu-id="9ea18-170">Por tanto, supongamos que establece una directiva de acceso condicional que indica que solo se puede acceder a la aplicación "Office 365 Exchange Online" desde máquinas que sean compatibles.</span><span class="sxs-lookup"><span data-stu-id="9ea18-170">So, say you set a conditional access policy that says that the “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="9ea18-171">Esta directiva también se activará si un usuario intenta usar una aplicación cliente que solicita permisos para Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="9ea18-171">This policy will also kick in when a user attempts to use a client app which requests permissions to Exchange Online.</span></span>



- <span data-ttu-id="9ea18-172">De esta forma, tiene visibilidad para ver a qué aplicaciones se le ha dado consentimiento y cuáles se están usando.</span><span class="sxs-lookup"><span data-stu-id="9ea18-172">You have visibility into which apps have been consented to and which ones are being used.</span></span>

1.  <span data-ttu-id="9ea18-173">Cuando un usuario da su consentimiento a una aplicación, se crea un objeto ServicePrincipal en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="9ea18-173">When a user consents to an app, a ServicePrincipal object is created in the tenant.</span></span> <span data-ttu-id="9ea18-174">La creación de ServicePrincipal se incluye en el informe de auditoría.</span><span class="sxs-lookup"><span data-stu-id="9ea18-174">ServicePrincipal creation is included in the audit report.</span></span>
2.  <span data-ttu-id="9ea18-175">Los informes de actividad de inicio de sesión del usuario le indican en qué aplicación está iniciando sesión el usuario.</span><span class="sxs-lookup"><span data-stu-id="9ea18-175">User sign-in activity reports tell you which app the user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="9ea18-176">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9ea18-176">Example</span></span>

<span data-ttu-id="9ea18-177">Por ejemplo, tomemos la aplicación "FabrikamMail para Office 365", en la que ha observado que los usuarios de su inquilino están iniciando sesión.</span><span class="sxs-lookup"><span data-stu-id="9ea18-177">As an example, let’s take the “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="9ea18-178">"FabrikamMail" es una aplicación de lector de correo electrónico para Android, publicada por "Fabrikam, Inc.".</span><span class="sxs-lookup"><span data-stu-id="9ea18-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="9ea18-179">Esta aplicación puede incluirse en la categoría de "aplicaciones multiinquilino que desarrollan otros, a las que Contoso puede dar consentimiento".</span><span class="sxs-lookup"><span data-stu-id="9ea18-179">This falls into the “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="9ea18-180">Si se permite que los usuarios pueden dar consentimiento, estos recibirán una solicitud de consentimiento la primera vez que inicien sesión: ![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="9ea18-180">If users are allowed to consent, they get a consent prompt the first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="9ea18-181">"Acceso a los buzones" es la cadena de consentimiento del usuario para el permiso "Acceso a los buzones como el usuario que inició sesión" expuesto por "Office 365 Exchange Online" (es decir, Exchange).</span><span class="sxs-lookup"><span data-stu-id="9ea18-181">“Access your mailboxes” is the user-facing consent string for the “Access mailboxes as the signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="9ea18-182">Puede ver los permisos. Para ello, busque el objeto ServicePrincipal de Exchange (el recurso), que se agregó al suscribirse a Office 365.</span><span class="sxs-lookup"><span data-stu-id="9ea18-182">You can see the permissions by looking up the ServicePrincipal object for Exchange (the resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="9ea18-183">Puede pensar en el objeto ServicePrincipal como una "instancia" de la aplicación en su inquilino que se usa para registrar las diferentes opciones y configuraciones.</span><span class="sxs-lookup"><span data-stu-id="9ea18-183">You can think of the ServicePrincipal object of an “instance” of the app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="9ea18-184">Se puede ver mediante `Get-AzureADServicePrincipal` en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ea18-184">You can see this by using the `Get-AzureADServicePrincipal` in PowerShell.</span></span>

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows the app to have the same access to mailboxes as the signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as the signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows the app full access to your mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

<span data-ttu-id="9ea18-185">El consentimiento se inicia cuando el usuario hace clic en "Aceptar".</span><span class="sxs-lookup"><span data-stu-id="9ea18-185">Consent is initiated when the user clicks “Accept”.</span></span> <span data-ttu-id="9ea18-186">En primer lugar, se crea un objeto ServicePrincipal para "FabrikamMail para Office 365" en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="9ea18-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in the tenant.</span></span> <span data-ttu-id="9ea18-187">El objeto ServicePrincipal tiene un aspecto parecido a este:</span><span class="sxs-lookup"><span data-stu-id="9ea18-187">The ServicePrincipal looks something like this:</span></span>

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

<span data-ttu-id="9ea18-188">El consentimiento a una aplicación creará un vínculo Oauth2PermissionGrant entre lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9ea18-188">Consenting to an app creates an Oauth2PermissionGrant link between the following:</span></span>
  
- <span data-ttu-id="9ea18-189">el objeto de usuario</span><span class="sxs-lookup"><span data-stu-id="9ea18-189">the user object</span></span>
- <span data-ttu-id="9ea18-190">el objeto ServicePrincipalName de las aplicaciones cliente (SPN)</span><span class="sxs-lookup"><span data-stu-id="9ea18-190">the client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="9ea18-191">el objeto ServicePrincipalName de las aplicaciones de recursos (SPN)</span><span class="sxs-lookup"><span data-stu-id="9ea18-191">the resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="9ea18-192">los permisos de la aplicación de recursos.</span><span class="sxs-lookup"><span data-stu-id="9ea18-192">permissions in the resource app.</span></span>  

<span data-ttu-id="9ea18-193">En el caso de FabrikamMail, se parece a esto:</span><span class="sxs-lookup"><span data-stu-id="9ea18-193">In the case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="9ea18-194">(**ClientId** es el identificador de objeto de la entidad de servicio de FabrikamMail (que se acaba de crear), **PrincipalId** es el identificador de objeto del usuario (el usuario que ha dado consentimiento), **ResourceId** es el identificador de objeto de la entidad de servicio de Exchange, y Scope es el permiso de Exchange para el que se ha dado consentimiento.</span><span class="sxs-lookup"><span data-stu-id="9ea18-194">(**ClientId** is FabrikamMail’s service principal object ID (the one that just got created), **PrincipalId** is the user object ID (of the user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is the permission in Exchange that was consented to).</span></span>

<span data-ttu-id="9ea18-195">Si no se permite a los usuarios dar consentimiento, verá una pantalla que indica que se necesita permiso.</span><span class="sxs-lookup"><span data-stu-id="9ea18-195">If users are not allowed to consent, they will see a screen that says that permission is required.</span></span>

