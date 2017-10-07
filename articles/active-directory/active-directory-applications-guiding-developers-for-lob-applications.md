---
title: aaaDevelop aplicaciones para Azure AD | Documentos de Microsoft
description: "Escrito para profesionales de TI de hello, este artículo proporciona instrucciones para la integración de aplicaciones de Azure con Active Directory."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="245c5-103">Desarrollo de aplicaciones de línea de negocio para Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="245c5-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="245c5-104">Esta guía proporciona información general sobre el desarrollo de aplicaciones de línea de negocio (LoB) de Azure Active Directory (AD) .hello pensado destinatarios son los administradores globales de Active Directory/Office 365.</span><span class="sxs-lookup"><span data-stu-id="245c5-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).hello intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="245c5-105">Información general</span><span class="sxs-lookup"><span data-stu-id="245c5-105">Overview</span></span>
<span data-ttu-id="245c5-106">La creación de aplicaciones integradas con Azure AD proporciona a los usuarios de la organización inicio de sesión único con Office 365.</span><span class="sxs-lookup"><span data-stu-id="245c5-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="245c5-107">Tiene la aplicación hello en Azure AD le permite que controlar a través de la directiva de autenticación de hello para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="245c5-107">Having hello application in Azure AD gives you control over hello authentication policy for hello application.</span></span> <span data-ttu-id="245c5-108">más información sobre el acceso condicional y cómo ver aplicaciones tooprotect con la autenticación multifactor (MFA) toolearn [configuración de las reglas de acceso](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="245c5-108">toolearn more about conditional access and how tooprotect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="245c5-109">Registrar su toouse aplicación Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="245c5-109">Register your application toouse Azure Active Directory.</span></span> <span data-ttu-id="245c5-110">Registrar la aplicación hello significa que los desarrolladores pueden usar usuarios de Azure AD tooauthenticate y solicitar acceso a los recursos de toouser como correo electrónico, calendario y documentos.</span><span class="sxs-lookup"><span data-stu-id="245c5-110">Registering hello application means that your developers can use Azure AD tooauthenticate users and request access toouser resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="245c5-111">Cualquier miembro del directorio (no invitados) puede registrar una aplicación, conocido también como *crear un objeto de aplicación*.</span><span class="sxs-lookup"><span data-stu-id="245c5-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="245c5-112">Registrar una aplicación, permite cualquier siguiente de hello toodo de usuario:</span><span class="sxs-lookup"><span data-stu-id="245c5-112">Registering an application allows any user toodo hello following:</span></span>

* <span data-ttu-id="245c5-113">Obtener una identidad para su aplicación que Azure AD reconoce</span><span class="sxs-lookup"><span data-stu-id="245c5-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="245c5-114">Obtener uno o más secretos o claves que Hola aplicación puede usar tooauthenticate propio tooAD</span><span class="sxs-lookup"><span data-stu-id="245c5-114">Get one or more secrets/keys that hello application can use tooauthenticate itself tooAD</span></span>
* <span data-ttu-id="245c5-115">Aplicación hello de marca en el portal de Azure con un nombre personalizado, logotipo, etcetera Hola.</span><span class="sxs-lookup"><span data-stu-id="245c5-115">Brand hello application in hello Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="245c5-116">Aplicar la aplicación de tootheir de características de autorización de Azure AD, incluidos:</span><span class="sxs-lookup"><span data-stu-id="245c5-116">Apply Azure AD authorization features tootheir app, including:</span></span>

  * <span data-ttu-id="245c5-117">Control de acceso basado en rol (RBAC)</span><span class="sxs-lookup"><span data-stu-id="245c5-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="245c5-118">Azure Active Directory como servidor de autorización de oAuth (proteger una API expuesta por la aplicación hello)</span><span class="sxs-lookup"><span data-stu-id="245c5-118">Azure Active Directory as oAuth authorization server (secure an API exposed by hello application)</span></span>
* <span data-ttu-id="245c5-119">Declarar permisos necesarios necesarios para toofunction de aplicación Hola según lo esperado, incluidos:</span><span class="sxs-lookup"><span data-stu-id="245c5-119">Declare required permissions necessary for hello application toofunction as expected, including:</span></span>

      - <span data-ttu-id="245c5-120">Permisos de la aplicación (solo administradores globales).</span><span class="sxs-lookup"><span data-stu-id="245c5-120">App permissions (global administrators only).</span></span> <span data-ttu-id="245c5-121">Por ejemplo: pertenencia a roles en otro Azure AD aplicación o rol pertenencia relativa tooan recursos de Azure, grupo de recursos, o suscripción</span><span class="sxs-lookup"><span data-stu-id="245c5-121">For example: Role membership in another Azure AD application or role membership relative tooan Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="245c5-122">Permisos delegados (cualquier usuario)</span><span class="sxs-lookup"><span data-stu-id="245c5-122">Delegated permissions (any user).</span></span> <span data-ttu-id="245c5-123">Por ejemplo: Azure AD, inicio de sesión y perfil de lectura</span><span class="sxs-lookup"><span data-stu-id="245c5-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="245c5-124">De forma predeterminada, cualquier miembro puede registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="245c5-124">By default, any member can register an application.</span></span> <span data-ttu-id="245c5-125">toolearn toorestrict permisos para el registro de los miembros de toospecific de aplicaciones, vea [cómo las aplicaciones se agregan tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="245c5-125">toolearn how toorestrict permissions for registering applications toospecific members, see [How applications are added tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="245c5-126">Aquí es lo que, administrador global de hello, necesitan toodo toohelp desarrolladores que su aplicación esté listo para producción:</span><span class="sxs-lookup"><span data-stu-id="245c5-126">Here’s what you, hello global administrator, need toodo toohelp developers make their application ready for production:</span></span>

* <span data-ttu-id="245c5-127">Configurar las reglas de acceso (directiva de acceso/MFA)</span><span class="sxs-lookup"><span data-stu-id="245c5-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="245c5-128">Configurar asignación de usuario de hello aplicación toorequire y asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="245c5-128">Configure hello app toorequire user assignment and assign users</span></span>
* <span data-ttu-id="245c5-129">Suprimir experiencia de consentimiento del usuario Hola predeterminado</span><span class="sxs-lookup"><span data-stu-id="245c5-129">Suppress hello default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="245c5-130">Configuración de las reglas de acceso</span><span class="sxs-lookup"><span data-stu-id="245c5-130">Configure access rules</span></span>
<span data-ttu-id="245c5-131">Configurar aplicaciones de SaaS de tooyour de reglas de acceso según la aplicación.</span><span class="sxs-lookup"><span data-stu-id="245c5-131">Configure per-application access rules tooyour SaaS apps.</span></span> <span data-ttu-id="245c5-132">Por ejemplo, puede requerir MFA o sólo permitir acceso toousers en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="245c5-132">For example, you can require MFA or only allow access toousers on trusted networks.</span></span> <span data-ttu-id="245c5-133">detalles de Hola para este están disponibles en el documento de hello [configuración de las reglas de acceso](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="245c5-133">hello details for this are available in hello document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a><span data-ttu-id="245c5-134">Configurar asignación de usuario de hello aplicación toorequire y asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="245c5-134">Configure hello app toorequire user assignment and assign users</span></span>
<span data-ttu-id="245c5-135">De forma predeterminada, los usuarios pueden acceder a las aplicaciones sin asignación previa.</span><span class="sxs-lookup"><span data-stu-id="245c5-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="245c5-136">Sin embargo, si la aplicación hello expone funciones o si desea que tooappear de aplicación hello en el panel de acceso de un usuario, debe requieren la asignación de usuario.</span><span class="sxs-lookup"><span data-stu-id="245c5-136">However, if hello application exposes roles or if you want hello application tooappear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="245c5-137">Necesidad de asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="245c5-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="245c5-138">Si es un suscriptor de Azure AD Premium o Enterprise Mobility Suite (EMS), se recomienda encarecidamente utilizar grupos.</span><span class="sxs-lookup"><span data-stu-id="245c5-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="245c5-139">Asignar grupos de aplicación de toohello permite a propietario del toohello management toodelegate un acceso continuo del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="245c5-139">Assigning groups toohello application allows you toodelegate ongoing access management toohello owner of hello group.</span></span> <span data-ttu-id="245c5-140">Puede crear grupo de Hola o pida a entidad responsable de hello en el grupo de organización toocreate hello mediante la utilidad de administración de grupo.</span><span class="sxs-lookup"><span data-stu-id="245c5-140">You can create hello group or ask hello responsible party in your organization toocreate hello group using your group management facility.</span></span>

[<span data-ttu-id="245c5-141">Asignación de usuarios tooan aplicación</span><span class="sxs-lookup"><span data-stu-id="245c5-141">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="245c5-142">Asignar grupos de aplicación de tooan</span><span class="sxs-lookup"><span data-stu-id="245c5-142">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="245c5-143">Supresión del consentimiento del usuario</span><span class="sxs-lookup"><span data-stu-id="245c5-143">Suppress user consent</span></span>
<span data-ttu-id="245c5-144">De forma predeterminada, cada usuario pasa por un toosign de experiencia de consentimiento en.</span><span class="sxs-lookup"><span data-stu-id="245c5-144">By default, each user goes through a consent experience toosign in.</span></span> <span data-ttu-id="245c5-145">experiencia de consentimiento de Hello, pidiendo a los usuarios permisos de toogrant tooan aplicación, puede ser desconcertante para los usuarios que no estén familiarizados con dichas decisiones.</span><span class="sxs-lookup"><span data-stu-id="245c5-145">hello consent experience, asking users toogrant permissions tooan application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="245c5-146">Para aplicaciones de confianza, puede simplificar la experiencia del usuario Hola consentimiento toohello aplicación en nombre de su organización.</span><span class="sxs-lookup"><span data-stu-id="245c5-146">For applications that you trust, you can simplify hello user experience by consenting toohello application on behalf of your organization.</span></span>

<span data-ttu-id="245c5-147">Para obtener más información sobre el consentimiento del usuario y consentimiento de hello experiencia en Azure, consulte [integración de aplicaciones con Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="245c5-147">For more information about user consent and hello consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="245c5-148">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="245c5-148">Related Articles</span></span>
* [<span data-ttu-id="245c5-149">Permitir que las aplicaciones de tooon local de acceso remoto seguro con el Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="245c5-149">Enable secure remote access tooon-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="245c5-150">Acceso condicional de Azure en versión de vista previa para aplicaciones SaaS</span><span class="sxs-lookup"><span data-stu-id="245c5-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="245c5-151">Administrar acceso tooapps con Azure AD</span><span class="sxs-lookup"><span data-stu-id="245c5-151">Managing access tooapps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="245c5-152">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="245c5-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
