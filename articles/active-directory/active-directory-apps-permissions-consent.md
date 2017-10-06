---
title: Aplicaciones, permisos y consentimiento en Azure Active Directory | Microsoft Docs
description: "Azure AD Connect integrará sus directorios locales con Azure Active Directory. Esto le permite tooprovide una identidad común para las aplicaciones de Office 365, Azure y SaaS integrada con Azure AD."
keywords: "Introducción tooAzure AD, aplicaciones, ¿qué es Azure AD Connect, instalar active directory"
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
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="87dad-105">Aplicaciones, permisos y consentimiento en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87dad-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="87dad-106">Dentro de Azure Active Directory, puede agregar el directorio de aplicaciones tooyour.</span><span class="sxs-lookup"><span data-stu-id="87dad-106">Within Azure Active Directory, you can add applications tooyour directory.</span></span>  <span data-ttu-id="87dad-107">las aplicaciones de Hello pueden variar según el tipo de Hola de aplicación.</span><span class="sxs-lookup"><span data-stu-id="87dad-107">hello applications can vary depending on hello type of application.</span></span>  <span data-ttu-id="87dad-108">tooview aplicaciones en portal clásico de hello, seleccione un directorio y elija aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="87dad-108">tooview applications in hello classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="87dad-109">Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="87dad-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="87dad-110">Tipos de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="87dad-110">Types of apps</span></span>

1. <span data-ttu-id="87dad-111">**Aplicaciones de inquilino único**</span><span class="sxs-lookup"><span data-stu-id="87dad-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="87dad-112">**Aplicaciones de inquilinos solo** -a menudo se conoce tooas aplicaciones de línea de negocio (LOB).</span><span class="sxs-lookup"><span data-stu-id="87dad-112">**Single-tenant apps** - Often referred tooas line-of-business (LOB) apps.</span></span> <span data-ttu-id="87dad-113">Esto es así de Hola donde alguien de su organización desarrolla su propia aplicación y desea que los usuarios en hello organización toobe puede toosign en toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="87dad-113">This is hello case where someone within your organization develops their own app, and would like users in hello organization toobe able toosign in toohello app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="87dad-114">**Aplicaciones de Proxy de aplicación** : al exponer una aplicación local con el Proxy de aplicación de Azure AD, una aplicación único inquilino esté registrada en el inquilino (en el servicio de Proxy de aplicación de suma toohello).</span><span class="sxs-lookup"><span data-stu-id="87dad-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition toohello App Proxy service).</span></span> <span data-ttu-id="87dad-115">Esta aplicación es la que representará la aplicación local en todas las interacciones en la nube (por ejemplo, en la autenticación).</span><span class="sxs-lookup"><span data-stu-id="87dad-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="87dad-116">(Proxy de aplicación requiere Azure AD Basic o superior).</span><span class="sxs-lookup"><span data-stu-id="87dad-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="87dad-117">**Aplicaciones multiinquilino**</span><span class="sxs-lookup"><span data-stu-id="87dad-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="87dad-118">**Aplicaciones de varios inquilinos que otras personas puedan permitir** : similar demasiado "único inquilino de aplicaciones que desarrolla la organización".</span><span class="sxs-lookup"><span data-stu-id="87dad-118">**Multi-tenant apps which others can consent to** - similar too“single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="87dad-119">Hola principal diferencia (además de la lógica de hello en la propia aplicación Hola) es que los usuarios de otros inquilinos también pueden dar su consentimiento tooand de inicio de sesión toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="87dad-119">hello main difference (besides hello logic in hello app itself) is that users from other tenants can also consent tooand sign in toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="87dad-120">**Aplicaciones multiinquilino que desarrollan otros, a las que Contoso puede dar consentimiento**.</span><span class="sxs-lookup"><span data-stu-id="87dad-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="87dad-121">(O "aplicaciones consentidas", para abreviar). Se trata de hello flip lado de "de su organización desarrolla aplicaciones multiempresa".</span><span class="sxs-lookup"><span data-stu-id="87dad-121">(Or “consented apps”, for short.) This is hello flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="87dad-122">Cuando otra organización desarrolla una aplicación de varios inquilinos, los usuarios de su organización pueden dar su consentimiento toohello aplicación e inicie sesión tooit.</span><span class="sxs-lookup"><span data-stu-id="87dad-122">When another organization develops a multi-tenant app, users of your organization can consent toohello app and sign in tooit.</span></span>
    - <span data-ttu-id="87dad-123">**Aplicaciones propias de Microsoft**: las aplicaciones que representan los servicios de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="87dad-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="87dad-124">Consentimiento está controlado por el hecho de Hola que se registra para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="87dad-124">Consent is driven by hello fact that you sign up for hello service.</span></span> <span data-ttu-id="87dad-125">A veces hay especial UX y la lógica para ciertas aplicaciones de cookies que se suele utilizar al establecimiento de directivas de aplicación de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="87dad-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="87dad-126">**Aplicaciones integradas previamente** -aplicaciones disponibles en la Galería de aplicaciones de Azure AD, que puede agregar hello tooyour directory tooprovide single sign-on (y en algunos casos, el aprovisionamiento) toopopular aplicaciones de SaaS.</span><span class="sxs-lookup"><span data-stu-id="87dad-126">**Pre-integrated apps** - Apps available in hello Azure AD App Gallery, which you can add tooyour directory tooprovide single sign-on (and in some cases, provisioning) toopopular SaaS apps.</span></span>
    - <span data-ttu-id="87dad-127">**Inicio de sesión único de Azure AD**: inicio de sesión único "real" para las aplicaciones que se pueden integrar con Azure AD, mediante un protocolo de inicio de sesión compatible como SAML 2.0 o OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="87dad-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="87dad-128">Hola asistente le guiará a través de su configuración.</span><span class="sxs-lookup"><span data-stu-id="87dad-128">hello wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="87dad-129">**Inicio de sesión único en la contraseña**: Azure AD guarda las credenciales del usuario de hello para la aplicación hello y credenciales de Hola se "insertadas" en el formulario de inicio de sesión de Hola por hello extensión del explorador de acceso de la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87dad-129">**Password single sign-on**: Azure AD securely stores hello user’s credentials for hello app, and hello credentials are “injected” into hello sign-in form by hello Azure AD App Access browser extension.</span></span> <span data-ttu-id="87dad-130">A este proceso también se le conoce como "almacenamiento de contraseñas".</span><span class="sxs-lookup"><span data-stu-id="87dad-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="87dad-131">Permisos</span><span class="sxs-lookup"><span data-stu-id="87dad-131">Permissions</span></span>

<span data-ttu-id="87dad-132">Cuando se registra una aplicación, usuario de hello realizando el registro de aplicación Hola (es decir, el desarrollador de hello) define qué aplicación de hello permisos necesita tener acceso a y qué recursos.</span><span class="sxs-lookup"><span data-stu-id="87dad-132">When an app is registered, hello user performing hello app registration (that is, hello developer) defines which permissions hello app needs access to, and which resources.</span></span> <span data-ttu-id="87dad-133">(recursos de hello son, por sí mismos, definido como otras aplicaciones). Por ejemplo, alguien compilar una aplicación de lector de correo electrónico, podría indicar que su aplicación requiere el permiso de "Acceso a los buzones como usuario con sesión iniciada Hola" Hola Hola "Office 365 Exchange Online" recursos:</span><span class="sxs-lookup"><span data-stu-id="87dad-133">(hello resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires hello “Access mailboxes as hello signed-in user” permission in hello “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="87dad-134">En orden para una aplicación (cliente hello) toorequest cierto permiso desde otra aplicación (recurso hello), desarrollador Hola de aplicación de recursos de hello define los permisos de Hola que existen.</span><span class="sxs-lookup"><span data-stu-id="87dad-134">In order for one app (hello client) toorequest a certain permission from another app (hello resource), hello developer of hello resource app defines hello permissions that exist.</span></span> <span data-ttu-id="87dad-135">En nuestro ejemplo, Microsoft, propietario de Hola de aplicación de recursos "Office 365 Exchange Online" hello, ha definido un permiso denominado "Acceso a los buzones como usuario con sesión iniciada Hola".</span><span class="sxs-lookup"><span data-stu-id="87dad-135">In our example, Microsoft, hello owner of hello “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as hello signed-in user”.</span></span>

<span data-ttu-id="87dad-136">Al definir los permisos, debe definir desarrollador de aplicaciones de hello si puede ser consentido permiso hello, o si se requiere el consentimiento del administrador.</span><span class="sxs-lookup"><span data-stu-id="87dad-136">When defining permissions, hello app developer must define if hello permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="87dad-137">Esto permite a los desarrolladores tooallow tooconsent de los usuarios en sus propios tooapps solicita solo baja sensibilidad permisos, pero requieren permisos de administradores tooconsent toomore confidenciales.</span><span class="sxs-lookup"><span data-stu-id="87dad-137">This allows developers tooallow users tooconsent on their own tooapps requesting only low-sensitivity permissions, but require admins tooconsent toomore sensitive permissions.</span></span> <span data-ttu-id="87dad-138">Por ejemplo, Hola "Azure Active Directory" aplicación de recurso, se ha definido, por lo que los usuarios pueden consentir tooapps, solicitar permisos limitados de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="87dad-138">For example, hello “Azure Active Directory” resource app, has been defined, so users can consent tooapps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="87dad-139">Sin embargo, se requiere el consentimiento del administrador para conseguir permisos completos de lectura y para todos los permisos de escritura.</span><span class="sxs-lookup"><span data-stu-id="87dad-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="87dad-140">Puesto que no se autentican clientes nativos, una aplicación que se define como una aplicación de cliente nativo solo puede solicitar permisos delegados.</span><span class="sxs-lookup"><span data-stu-id="87dad-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="87dad-141">Esto significa que siempre debe haber un usuario real implicado en la obtención de un token.</span><span class="sxs-lookup"><span data-stu-id="87dad-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="87dad-142">Las aplicaciones web y API web (clientes confidenciales), siempre se deben autenticar con Azure AD al acceder a un token.</span><span class="sxs-lookup"><span data-stu-id="87dad-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="87dad-143">Lo que significa que tienen también la posibilidad de hello de la solicitud de permisos solo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="87dad-143">Meaning they also have hello possibility of requesting app-only permissions.</span></span> <span data-ttu-id="87dad-144">Por ejemplo, si un servicio back-end necesita servicio back-end de tooauthenticate tooanother.</span><span class="sxs-lookup"><span data-stu-id="87dad-144">For example, if one back-end service needs tooauthenticate tooanother back-end service.</span></span> <span data-ttu-id="87dad-145">Las aplicaciones que solicitan permisos de solo aplicación requieren siempre el consentimiento del administrador.</span><span class="sxs-lookup"><span data-stu-id="87dad-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="87dad-146">En resumen:</span><span class="sxs-lookup"><span data-stu-id="87dad-146">Summarizing:</span></span>



- <span data-ttu-id="87dad-147">Una aplicación (cliente) indica que los permisos de Hola que necesita para otras aplicaciones (recursos).</span><span class="sxs-lookup"><span data-stu-id="87dad-147">An app (client) states hello permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="87dad-148">Una aplicación (recurso) indica qué permisos son tooother expuesto aplicaciones (clientes).</span><span class="sxs-lookup"><span data-stu-id="87dad-148">An app (resource) states what permissions are exposed tooother apps (clients).</span></span>
- <span data-ttu-id="87dad-149">Un permiso puede ser un permiso de solo aplicación o un permiso delegado.</span><span class="sxs-lookup"><span data-stu-id="87dad-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="87dad-150">Un permiso delegado se puede marcar para indicar que "permite el consentimiento del usuario" o que "requiere el consentimiento del administrador".</span><span class="sxs-lookup"><span data-stu-id="87dad-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="87dad-151">Una aplicación puede comportarse como un cliente (declarando que requiere recursos de tooa de permisos), como un recurso (mediante la declaración de los permisos que expone) o como ambos.</span><span class="sxs-lookup"><span data-stu-id="87dad-151">An app can behave as a client (by declaring that it needs permissions tooa resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="87dad-152">Controles</span><span class="sxs-lookup"><span data-stu-id="87dad-152">Controls</span></span>

<span data-ttu-id="87dad-153">Hola mostramos una lista de controles de administración diferentes Hola disponibles para todos los este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="87dad-153">hello following is a list of hello different admin controls available for all this behavior.</span></span> <span data-ttu-id="87dad-154">Hola, administrador pueden tener acceso a controles en el portal clásico de Hola desde configurar directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="87dad-154">hello admin controls can be accessed in hello classic portal from configure under hello directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="87dad-155">Hola Azure portal, en **administrar**, **configuración de usuario**.</span><span class="sxs-lookup"><span data-stu-id="87dad-155">In hello Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="87dad-156">Puede controlar si los usuarios pueden consentir tooapps:</span><span class="sxs-lookup"><span data-stu-id="87dad-156">You can control whether users can consent tooapps:</span></span>

<span data-ttu-id="87dad-157">En el portal clásico de hello, seleccione **los usuarios pueden permitir aplicaciones permisos tooaccess sus datos.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="87dad-157">In hello classic portal, select **Users may give applications permissions tooaccess their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="87dad-158">Hola portal de Azure, seleccione **a los usuarios pueden permitir aplicaciones tooaccess sus datos**.</span><span class="sxs-lookup"><span data-stu-id="87dad-158">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="87dad-159">Puede controlar si los usuarios pueden registrar sus propias aplicaciones LOB único inquilino: en Seleccione portal clásico de hello **los usuarios pueden agregar aplicaciones integradas.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="87dad-159">You can control whether users can register their own single-tenant LOB apps: In hello classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="87dad-160">Hola portal de Azure, seleccione **a los usuarios pueden permitir aplicaciones tooaccess sus datos**.</span><span class="sxs-lookup"><span data-stu-id="87dad-160">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="87dad-161">Incluso si permitir a los usuarios de las aplicaciones LOB de tooregister único inquilino, hay límites se pueden registrar toowhat.</span><span class="sxs-lookup"><span data-stu-id="87dad-161">Even if you do allow users tooregister single-tenant LOB apps, there are limits toowhat can be registered.</span></span>  
><span data-ttu-id="87dad-162">Por ejemplo, los desarrolladores que no son administradores de directorios.</span><span class="sxs-lookup"><span data-stu-id="87dad-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="87dad-163">Los usuarios no pueden hacer que una aplicación de inquilino único se convierta en una aplicación multiinquilino.</span><span class="sxs-lookup"><span data-stu-id="87dad-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="87dad-164">Al registrar las aplicaciones LOB único inquilino, los usuarios no pueden solicitar permisos de solo aplicación tooother aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="87dad-164">When registering single-tenant LOB apps, users cannot request app-only permissions tooother apps.</span></span>
>- <span data-ttu-id="87dad-165">Al registrar las aplicaciones LOB único inquilino, los usuarios no pueden solicitar permisos delegados tooother aplicaciones si esos permisos requieren consentimiento del administrador.</span><span class="sxs-lookup"><span data-stu-id="87dad-165">When registering single-tenant LOB apps, users cannot request delegated permissions tooother apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="87dad-166">Los usuarios no pueden realizar cambios tooapps que no son propietarios de.</span><span class="sxs-lookup"><span data-stu-id="87dad-166">Users cannot make changes tooapps that they are not owners of.</span></span>



- <span data-ttu-id="87dad-167">Puede controlar si los usuarios pueden por sí mismos agregar aplicaciones previamente integradas que utilizan el inicio de sesión único con contraseña (proceso también conocido como "almacenamiento de contraseña") ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="87dad-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="87dad-168">Puede controlar en qué condiciones se puede tener acceso a las aplicaciones (es decir, un acceso condicional).</span><span class="sxs-lookup"><span data-stu-id="87dad-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="87dad-169">Tenga en cuenta que esto aplica toohello aplicación de cliente y de aplicación de recursos de toohello.</span><span class="sxs-lookup"><span data-stu-id="87dad-169">Be aware this applies both toohello client app and toohello resource app.</span></span> <span data-ttu-id="87dad-170">Por lo tanto, supongamos que establece una directiva de acceso condicional que dice "Office 365 Exchange Online" aplicación Hola solo puede tener acceso desde máquinas, que son compatibles.</span><span class="sxs-lookup"><span data-stu-id="87dad-170">So, say you set a conditional access policy that says that hello “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="87dad-171">Esta directiva también se activa cuando un usuario intenta toouse una aplicación cliente que solicita permisos tooExchange en línea.</span><span class="sxs-lookup"><span data-stu-id="87dad-171">This policy will also kick in when a user attempts toouse a client app which requests permissions tooExchange Online.</span></span>



- <span data-ttu-id="87dad-172">Tener visibilidad en la que las aplicaciones han sido tooand con consentimiento cuáles se utilizan.</span><span class="sxs-lookup"><span data-stu-id="87dad-172">You have visibility into which apps have been consented tooand which ones are being used.</span></span>

1.  <span data-ttu-id="87dad-173">Cuando un usuario acepta tooan aplicación, se crea un objeto ServicePrincipal en el inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="87dad-173">When a user consents tooan app, a ServicePrincipal object is created in hello tenant.</span></span> <span data-ttu-id="87dad-174">Creación de ServicePrincipal se incluye en el informe de auditoría de Hola.</span><span class="sxs-lookup"><span data-stu-id="87dad-174">ServicePrincipal creation is included in hello audit report.</span></span>
2.  <span data-ttu-id="87dad-175">Informes de actividad de inicio de sesión de usuario saber qué usuario Hola de aplicación es iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="87dad-175">User sign-in activity reports tell you which app hello user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="87dad-176">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="87dad-176">Example</span></span>

<span data-ttu-id="87dad-177">Por ejemplo, echemos aplicación de "FabrikamMail para Office 365" hello, que haya observado los usuarios de su inquilino de sesión en.</span><span class="sxs-lookup"><span data-stu-id="87dad-177">As an example, let’s take hello “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="87dad-178">"FabrikamMail" es una aplicación de lector de correo electrónico para Android, publicada por "Fabrikam, Inc.".</span><span class="sxs-lookup"><span data-stu-id="87dad-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="87dad-179">Esto entra Hola "aplicaciones de varios inquilinos otros desarrolle, que puede dar el consentimiento Contoso".</span><span class="sxs-lookup"><span data-stu-id="87dad-179">This falls into hello “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="87dad-180">Si los usuarios pueden tooconsent, obtienen un Hola solicitar consentimiento primera vez que inicien sesión en:![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="87dad-180">If users are allowed tooconsent, they get a consent prompt hello first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="87dad-181">"Tener acceso a los buzones de correo" es la cadena de hello orientadas al usuario su consentimiento para permisos de "Acceso a los buzones como usuario con sesión iniciada Hola" hello expuestos por "Office 365 Exchange Online" (es decir, Exchange).</span><span class="sxs-lookup"><span data-stu-id="87dad-181">“Access your mailboxes” is hello user-facing consent string for hello “Access mailboxes as hello signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="87dad-182">Puede ver los permisos de hello buscando objeto ServicePrincipal de Hola para Exchange (recurso hello), que se agregó al suscribirse a Office 365.</span><span class="sxs-lookup"><span data-stu-id="87dad-182">You can see hello permissions by looking up hello ServicePrincipal object for Exchange (hello resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="87dad-183">Se puede considerar objeto ServicePrincipal de Hola de una "instancia" de la aplicación hello en su inquilino, que se usa para registrar las configuraciones y opciones diferentes.</span><span class="sxs-lookup"><span data-stu-id="87dad-183">You can think of hello ServicePrincipal object of an “instance” of hello app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="87dad-184">Puede ver mediante el uso de hello `Get-AzureADServicePrincipal` en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87dad-184">You can see this by using hello `Get-AzureADServicePrincipal` in PowerShell.</span></span>

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
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
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

<span data-ttu-id="87dad-185">Consentimiento se inicia cuando el usuario de Hola, haga clic en "Aceptar".</span><span class="sxs-lookup"><span data-stu-id="87dad-185">Consent is initiated when hello user clicks “Accept”.</span></span> <span data-ttu-id="87dad-186">En primer lugar, se crea un objeto ServicePrincipal para "FabrikamMail para Office 365" en inquilinos Hola.</span><span class="sxs-lookup"><span data-stu-id="87dad-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in hello tenant.</span></span> <span data-ttu-id="87dad-187">Hola ServicePrincipal tiene un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="87dad-187">hello ServicePrincipal looks something like this:</span></span>

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

<span data-ttu-id="87dad-188">Consentimiento tooan aplicación creará un vínculo de Oauth2PermissionGrant entre siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="87dad-188">Consenting tooan app creates an Oauth2PermissionGrant link between hello following:</span></span>
  
- <span data-ttu-id="87dad-189">objeto de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="87dad-189">hello user object</span></span>
- <span data-ttu-id="87dad-190">aplicaciones cliente Hello ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="87dad-190">hello client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="87dad-191">aplicaciones de recursos de Hello ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="87dad-191">hello resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="87dad-192">permisos de aplicación de recursos de hello.</span><span class="sxs-lookup"><span data-stu-id="87dad-192">permissions in hello resource app.</span></span>  

<span data-ttu-id="87dad-193">En caso de hello de FabrikamMail, parece algo parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="87dad-193">In hello case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="87dad-194">(**ClientId** es el identificador de objeto de entidad de servicio del FabrikamMail (Hola que simplemente se llegó a crear), **PrincipalId** es el Id. de objeto de usuario de hello (Hola del usuario de que dado su consentimiento), **ResourceId**es servicio de Exchange Id. de objeto principal, el ámbito es el permiso de hello en Exchange que se ha dado su consentimiento para).</span><span class="sxs-lookup"><span data-stu-id="87dad-194">(**ClientId** is FabrikamMail’s service principal object ID (hello one that just got created), **PrincipalId** is hello user object ID (of hello user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is hello permission in Exchange that was consented to).</span></span>

<span data-ttu-id="87dad-195">Si los usuarios no pueden tooconsent, verá una pantalla que dice ese permiso es necesaria.</span><span class="sxs-lookup"><span data-stu-id="87dad-195">If users are not allowed tooconsent, they will see a screen that says that permission is required.</span></span>

