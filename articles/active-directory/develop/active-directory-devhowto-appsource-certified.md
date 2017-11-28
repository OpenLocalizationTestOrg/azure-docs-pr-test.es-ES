---
title: aaaHow tooget AppSource certificada para Azure Active Directory | Documentos de Microsoft
description: "Información detallada sobre cómo tooget su aplicación AppSource certificada para Azure Active Directory."
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="377c6-103">Cómo tooget AppSource certificadas para Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="377c6-103">How tooget AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="377c6-104">[Microsoft AppSource](https://appsource.microsoft.com/) es un destino para toodiscover de los usuarios empresariales, pruebe y administrar aplicaciones de SaaS de línea de negocio (independiente SaaS y un complemento tooexisting Microsoft SaaS productos).</span><span class="sxs-lookup"><span data-stu-id="377c6-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users toodiscover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on tooexisting Microsoft SaaS products).</span></span>

<span data-ttu-id="377c6-105">toolist una aplicación de SaaS en AppSource independiente, la aplicación debe aceptar un inicio de sesión único de cuentas para el trabajo desde cualquier empresa u organización con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="377c6-105">toolist a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="377c6-106">proceso de inicio de sesión Hola debe usar hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) o [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocolos.</span><span class="sxs-lookup"><span data-stu-id="377c6-106">hello sign-in process must use hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="377c6-107">La integración de SAML no se acepta como certificación de AppSource.</span><span class="sxs-lookup"><span data-stu-id="377c6-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="377c6-108">Guías y ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="377c6-108">Guides and code samples</span></span>
<span data-ttu-id="377c6-109">Si desea toolearn sobre cómo toointegrate su aplicación con Azure Active Directory con Openid connect, siga nuestras guías y ejemplos de hello de código [Guía del desarrollador de Azure Active Directory](./active-directory-developers-guide.md#get-started "empezar a trabajar con Azure AD para los desarrolladores").</span><span class="sxs-lookup"><span data-stu-id="377c6-109">If you want toolearn about how toointegrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in hello [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="377c6-110">Aplicaciones multiinquilino</span><span class="sxs-lookup"><span data-stu-id="377c6-110">Multi-tenant applications</span></span>

<span data-ttu-id="377c6-111">Una aplicación que acepta inicios de sesión de usuarios de cualquier compañía u organización que tenga Azure Active Directory sin que se requiera otra instancia, configuración o implementación se denomina *aplicación multiempresa*.</span><span class="sxs-lookup"><span data-stu-id="377c6-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="377c6-112">AppSource recomienda que las aplicaciones implementan Hola multiempresa tooenable *con un solo clic* liberar una experiencia de evaluación.</span><span class="sxs-lookup"><span data-stu-id="377c6-112">AppSource recommends that applications implement multi-tenancy tooenable hello *single-click* free trial experience.</span></span>

<span data-ttu-id="377c6-113">En orden tooenable multiempresa en su aplicación:</span><span class="sxs-lookup"><span data-stu-id="377c6-113">In order tooenable multi-tenancy on your application:</span></span>
- <span data-ttu-id="377c6-114">Establecer `Multi-Tenanted` propiedad demasiado`Yes` en información del registro de la aplicación hello [Portal de Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (de forma predeterminada, las aplicaciones creadas en Portal de Azure Hola están configuradas como *único inquilino*)</span><span class="sxs-lookup"><span data-stu-id="377c6-114">Set `Multi-Tenanted` property too`Yes` on your application registration's information in hello [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in hello Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="377c6-115">Actualizar la toohello de las solicitudes de código toosend '`common`' punto de conexión (actualizar el extremo de Hola de *https://login.microsoftonline.com/ {yourtenant}* demasiado*https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="377c6-115">Update your code toosend requests toohello '`common`' endpoint (update hello endpoint from *https://login.microsoftonline.com/{yourtenant}* too*https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="377c6-116">Para algunas plataformas, como ASP.NET, debe también tooupdate su tooaccept código varios emisores</span><span class="sxs-lookup"><span data-stu-id="377c6-116">For some platforms, like ASP.NET, you need also tooupdate your code tooaccept multiple issuers</span></span>

<span data-ttu-id="377c6-117">Para obtener más información acerca de la arquitectura multiempresa, consulte: [cómo toosign en cualquier usuario de Azure Active Directory (AD) mediante Hola patrón de aplicación de varios inquilinos](./active-directory-devhowto-multi-tenant-overview.md).</span><span class="sxs-lookup"><span data-stu-id="377c6-117">For more information about multi-tenancy, see: [How toosign in any Azure Active Directory (AD) user using hello multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="377c6-118">Aplicaciones de inquilino único</span><span class="sxs-lookup"><span data-stu-id="377c6-118">Single-tenant applications</span></span>
<span data-ttu-id="377c6-119">Las aplicaciones que solo aceptan inicios de sesión de usuarios de una instancia de Azure Active Directory definida se denominan *aplicaciones de inquilino único*.</span><span class="sxs-lookup"><span data-stu-id="377c6-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="377c6-120">Los usuarios externos (incluidas las cuentas de trabajo o la escuela de otras organizaciones o cuenta personal) pueden iniciar sesión en la aplicación de inquilino único tooa después de agregar cada usuario como *cuenta de invitado* toohello Azure Active Directory de la instancia que se registra la aplicación Hello.</span><span class="sxs-lookup"><span data-stu-id="377c6-120">External users (including Work or School accounts from other organizations, or personal account) can sign in tooa single-tenant application after adding each user as *guest account* toohello Azure Active Directory instance that hello application is registered.</span></span> <span data-ttu-id="377c6-121">Puede agregar usuarios como tooan de cuentas de invitado Azure Active Directory a través de hello [ *colaboración B2B de Azure AD* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - y que es posible [mediante programación](../active-directory-b2b-code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="377c6-121">You can add users as guest accounts tooan Azure Active Directory via hello [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="377c6-122">Cuando se agrega un usuario como cuenta de invitado tooan Azure Active Directory, un correo electrónico de invitación se envía toohello usuario, que tiene la invitación de hello tooaccept haciendo clic en el vínculo de hello en correo electrónico de invitación de Hola.</span><span class="sxs-lookup"><span data-stu-id="377c6-122">When you add a user as guest account tooan Azure Active Directory, an invitation email is sent toohello user, who has tooaccept hello invitation by clicking on hello link in hello invitation email.</span></span> <span data-ttu-id="377c6-123">Las invitaciones que se enviaron tooan adicional del usuario en una organización invitar a que también es un miembro de la organización del asociado de hello son tooaccept no se requiere un toosign de invitación en.</span><span class="sxs-lookup"><span data-stu-id="377c6-123">Invitations that are sent tooan additional user in an inviting organization that is also a member of hello partner organization are not required tooaccept an invitation toosign in.</span></span>

<span data-ttu-id="377c6-124">Las aplicaciones de inquilinos solo pueden habilitar hello *contacto Me* experiencia, pero si desea tooenable Hola con un solo clic / libre una experiencia de evaluación que recomienda AppSource, habilite la arquitectura multiempresa en la aplicación en su lugar.</span><span class="sxs-lookup"><span data-stu-id="377c6-124">Single-tenant applications can enable hello *Contact Me* experience, but if you want tooenable hello single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="377c6-125">Experiencias de evaluación gratuita de AppSource</span><span class="sxs-lookup"><span data-stu-id="377c6-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="377c6-126">Evaluación gratuita (experiencia de evaluación dirigida por el usuario)</span><span class="sxs-lookup"><span data-stu-id="377c6-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="377c6-127">Hola *orientada a los clientes de prueba* es experiencia Hola que AppSource recomienda ya que ofrecen una aplicación de tooyour de acceso con un solo clic.</span><span class="sxs-lookup"><span data-stu-id="377c6-127">hello *customer-led trial* is hello experience that AppSource recommends as it offers a single-click access tooyour application.</span></span> <span data-ttu-id="377c6-128">Vea a continuación una ilustración del aspecto que tiene esta experiencia:</span><span class="sxs-lookup"><span data-stu-id="377c6-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="377c6-129">El usuario busca su aplicación en el sitio web de AppSource</span><span class="sxs-lookup"><span data-stu-id="377c6-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="377c6-130">Selecciona la opción "Evaluación gratuita"</span><span class="sxs-lookup"><span data-stu-id="377c6-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="377c6-131">AppSource redirige la dirección URL de tooa de usuario en el sitio web</span><span class="sxs-lookup"><span data-stu-id="377c6-131">AppSource redirects user tooa URL in your web site</span></span></li><li><span data-ttu-id="377c6-132">El sitio web inicia hello <i>single-sign-on</i> proceso automáticamente (al cargar la página)</span><span class="sxs-lookup"><span data-stu-id="377c6-132">Your web site starts hello <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="377c6-133">Usuario es página redirigidos tooMicrosoft inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="377c6-133">User is redirected tooMicrosoft Sign-in page</span></span></li><li><span data-ttu-id="377c6-134">El usuario proporciona credenciales toosign en</span><span class="sxs-lookup"><span data-stu-id="377c6-134">User provides credentials toosign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="377c6-135">El usuario le da su consentimiento en la aplicación</span><span class="sxs-lookup"><span data-stu-id="377c6-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="377c6-136">En el inicio de sesión se completa y el usuario es redirigido tooyour back-sitio de web</span><span class="sxs-lookup"><span data-stu-id="377c6-136">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="377c6-137">Usuario inicia la prueba gratuita de Hola</span><span class="sxs-lookup"><span data-stu-id="377c6-137">User starts hello free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="377c6-138">Ponerse en contacto conmigo (experiencia de evaluación dirigida por el partner)</span><span class="sxs-lookup"><span data-stu-id="377c6-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="377c6-139">Hola *una experiencia de evaluación de socios comerciales* puede usarse cuando un manual o una operación de larga duración necesita usuario Hola de toohappen tooprovision / compañía: por ejemplo, la aplicación necesita tooprovision las máquinas virtuales, instancias de base de datos, o operaciones que toman mucho tiempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="377c6-139">hello *partner trial experience* can be used when a manual or a long-term operation needs toohappen tooprovision hello user/ company: for example, your application needs tooprovision virtual machines, database instances, or operations that take much time toocomplete.</span></span> <span data-ttu-id="377c6-140">En este caso, después de usuario selecciona hello *solicitud de versión de prueba* botón y rellena un formulario, AppSource envía Hola información de contacto del usuario.</span><span class="sxs-lookup"><span data-stu-id="377c6-140">In this case, after user selects hello *'Request Trial'* button and fills out a form, AppSource sends you hello user's contact information.</span></span> <span data-ttu-id="377c6-141">Al recibir esta información, que, a continuación, aprovisionar el entorno de Hola y enviar al usuario de toohello Hola instrucciones sobre cómo tooaccess Hola una experiencia de evaluación:</span><span class="sxs-lookup"><span data-stu-id="377c6-141">Upon receiving this information, you then provision hello environment and send hello instructions toohello user on how tooaccess hello trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="377c6-142">El usuario busca su aplicación en el sitio web de AppSource</span><span class="sxs-lookup"><span data-stu-id="377c6-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="377c6-143">Selecciona la opción "Ponerse en contacto conmigo"</span><span class="sxs-lookup"><span data-stu-id="377c6-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="377c6-144">Rellena un formulario con información de contacto</span><span class="sxs-lookup"><span data-stu-id="377c6-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="377c6-145">Usted recibe la información del usuario</span><span class="sxs-lookup"><span data-stu-id="377c6-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="377c6-146">Configura el entorno</span><span class="sxs-lookup"><span data-stu-id="377c6-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="377c6-147">Se pone en contacto con el usuario con información de la versión de evaluación</span><span class="sxs-lookup"><span data-stu-id="377c6-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="377c6-148">Usted recibe la información del usuario y configura la instancia de evaluación</span><span class="sxs-lookup"><span data-stu-id="377c6-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="377c6-149">Enviar Hola hipervínculo tooaccess su usuario de toohello la aplicación</span><span class="sxs-lookup"><span data-stu-id="377c6-149">You send hello hyperlink tooaccess your application toohello user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="377c6-150">Usuario tiene acceso a la aplicación y el proceso de inicio de sesión único de hello completa</span><span class="sxs-lookup"><span data-stu-id="377c6-150">User accesses your application and complete hello single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="377c6-151">El usuario le da su consentimiento en la aplicación</span><span class="sxs-lookup"><span data-stu-id="377c6-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="377c6-152">En el inicio de sesión se completa y el usuario es redirigido tooyour back-sitio de web</span><span class="sxs-lookup"><span data-stu-id="377c6-152">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="377c6-153">Usuario inicia la prueba gratuita de Hola</span><span class="sxs-lookup"><span data-stu-id="377c6-153">User starts hello free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="377c6-154">Más información</span><span class="sxs-lookup"><span data-stu-id="377c6-154">More information</span></span>
<span data-ttu-id="377c6-155">Para obtener más información acerca de la experiencia de evaluación de hello AppSource, consulte [este vídeo](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="377c6-155">For more information about hello AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="377c6-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="377c6-156">Next Steps</span></span>

- <span data-ttu-id="377c6-157">Para más información sobre cómo generar aplicaciones que admitan inicios de sesión de Azure Active Directory, vea [Escenarios de autenticación para Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span><span class="sxs-lookup"><span data-stu-id="377c6-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="377c6-158">Para obtener información sobre cómo toolist la aplicación de SaaS en AppSource, visite [AppSource información de socio comercial](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="377c6-158">For information on how toolist your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="377c6-159">Obtención de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="377c6-159">Get Support</span></span>
<span data-ttu-id="377c6-160">Para la integración de Azure Active Directory, usamos [desbordamiento de la pila](http://stackoverflow.com/questions/tagged/azure-active-directory) con soporte técnico de hello Comunidad tooprovide.</span><span class="sxs-lookup"><span data-stu-id="377c6-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with hello community tooprovide support.</span></span> 

<span data-ttu-id="377c6-161">Se recomienda encarecidamente que haga sus preguntas acerca del desbordamiento de pila en primer lugar y examinar existente toosee problemas si alguien ha realizado su pregunta antes.</span><span class="sxs-lookup"><span data-stu-id="377c6-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues toosee if someone has asked your question before.</span></span> <span data-ttu-id="377c6-162">Asegúrese de que sus preguntas o comentarios se etiquetan con `[azure-active-directory]`.</span><span class="sxs-lookup"><span data-stu-id="377c6-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="377c6-163">Usar hello después de comentarios de tooprovide de sección de comentarios y nos ayudan a refinar y dar forma a nuestro contenido.</span><span class="sxs-lookup"><span data-stu-id="377c6-163">Use hello following comments section tooprovide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->