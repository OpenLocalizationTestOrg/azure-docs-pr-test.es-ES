---
title: Desarrollo de aplicaciones para Azure AD | Microsoft Docs
description: "Escrito para los profesionales de TI, este artículo ofrece instrucciones para integrar las aplicaciones de Azure con Active Directory."
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
ms.openlocfilehash: 6b119be9c06d8c1ccc8e747168429e6c2d2e7a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="89aa9-103">Desarrollo de aplicaciones de línea de negocio para Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89aa9-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="89aa9-104">Esta guía proporciona información general sobre el desarrollo de aplicaciones de línea de negocio (LoB) para Azure Active Directory (AD) y se ha diseñado expresamente para administradores globales de Active Directory y Office 365.</span><span class="sxs-lookup"><span data-stu-id="89aa9-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).The intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="89aa9-105">Información general</span><span class="sxs-lookup"><span data-stu-id="89aa9-105">Overview</span></span>
<span data-ttu-id="89aa9-106">La creación de aplicaciones integradas con Azure AD proporciona a los usuarios de la organización inicio de sesión único con Office 365.</span><span class="sxs-lookup"><span data-stu-id="89aa9-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="89aa9-107">Si tiene la aplicación en Azure AD, podrá controlar la directiva de autenticación de dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="89aa9-107">Having the application in Azure AD gives you control over the authentication policy for the application.</span></span> <span data-ttu-id="89aa9-108">Para obtener más información sobre el acceso condicional y cómo proteger las aplicaciones con Multi-Factor Authentication (MFA), consulte [Configuración de las reglas de acceso](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="89aa9-108">To learn more about conditional access and how to protect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="89aa9-109">Registro de la aplicación para utilizar Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89aa9-109">Register your application to use Azure Active Directory.</span></span> <span data-ttu-id="89aa9-110">Registrar la aplicación significa que los programadores pueden usar Azure AD para autenticar usuarios y solicitar acceso a recursos de usuarios; por ejemplo, correo electrónico, calendario y documentos.</span><span class="sxs-lookup"><span data-stu-id="89aa9-110">Registering the application means that your developers can use Azure AD to authenticate users and request access to user resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="89aa9-111">Cualquier miembro del directorio (no invitados) puede registrar una aplicación, conocido también como *crear un objeto de aplicación*.</span><span class="sxs-lookup"><span data-stu-id="89aa9-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="89aa9-112">El registro de una aplicación permite a cualquier usuario hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="89aa9-112">Registering an application allows any user to do the following:</span></span>

* <span data-ttu-id="89aa9-113">Obtener una identidad para su aplicación que Azure AD reconoce</span><span class="sxs-lookup"><span data-stu-id="89aa9-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="89aa9-114">Obtener uno o más secretos o claves que la aplicación puede usar para autenticarse a sí misma en AD</span><span class="sxs-lookup"><span data-stu-id="89aa9-114">Get one or more secrets/keys that the application can use to authenticate itself to AD</span></span>
* <span data-ttu-id="89aa9-115">Identificar la aplicación, por ejemplo, con un nombre o logotipo personalizado en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="89aa9-115">Brand the application in the Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="89aa9-116">Aplicar las características de autorización de Azure AD en su aplicación, como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="89aa9-116">Apply Azure AD authorization features to their app, including:</span></span>

  * <span data-ttu-id="89aa9-117">Control de acceso basado en rol (RBAC)</span><span class="sxs-lookup"><span data-stu-id="89aa9-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="89aa9-118">Azure Active Directory como servidor de autorización de OAuth (proteger una API expuesta por la aplicación)</span><span class="sxs-lookup"><span data-stu-id="89aa9-118">Azure Active Directory as oAuth authorization server (secure an API exposed by the application)</span></span>
* <span data-ttu-id="89aa9-119">Indicar los permisos necesarios para que la aplicación funcione según lo previsto, como:</span><span class="sxs-lookup"><span data-stu-id="89aa9-119">Declare required permissions necessary for the application to function as expected, including:</span></span>

      - <span data-ttu-id="89aa9-120">Permisos de la aplicación (solo administradores globales).</span><span class="sxs-lookup"><span data-stu-id="89aa9-120">App permissions (global administrators only).</span></span> <span data-ttu-id="89aa9-121">Por ejemplo: pertenencia a roles en otra aplicación de Azure AD o respecto a una suscripción, un grupo de recursos o un recurso de Azure</span><span class="sxs-lookup"><span data-stu-id="89aa9-121">For example: Role membership in another Azure AD application or role membership relative to an Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="89aa9-122">Permisos delegados (cualquier usuario)</span><span class="sxs-lookup"><span data-stu-id="89aa9-122">Delegated permissions (any user).</span></span> <span data-ttu-id="89aa9-123">Por ejemplo: Azure AD, inicio de sesión y perfil de lectura</span><span class="sxs-lookup"><span data-stu-id="89aa9-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="89aa9-124">De forma predeterminada, cualquier miembro puede registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="89aa9-124">By default, any member can register an application.</span></span> <span data-ttu-id="89aa9-125">Para obtener información sobre cómo restringir permisos de registro de aplicaciones a miembros específicos, consulte [Cómo se agregan aplicaciones a Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="89aa9-125">To learn how to restrict permissions for registering applications to specific members, see [How applications are added to Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="89aa9-126">A continuación, se indica lo que el administrador global tendrá que hacer para ayudar a los desarrolladores a que su aplicación esté lista para la producción:</span><span class="sxs-lookup"><span data-stu-id="89aa9-126">Here’s what you, the global administrator, need to do to help developers make their application ready for production:</span></span>

* <span data-ttu-id="89aa9-127">Configurar las reglas de acceso (directiva de acceso/MFA)</span><span class="sxs-lookup"><span data-stu-id="89aa9-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="89aa9-128">Configurar la aplicación para requerir asignación de usuarios y asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="89aa9-128">Configure the app to require user assignment and assign users</span></span>
* <span data-ttu-id="89aa9-129">Suprimir la experiencia de consentimiento del usuario predeterminada</span><span class="sxs-lookup"><span data-stu-id="89aa9-129">Suppress the default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="89aa9-130">Configuración de las reglas de acceso</span><span class="sxs-lookup"><span data-stu-id="89aa9-130">Configure access rules</span></span>
<span data-ttu-id="89aa9-131">Configure las reglas de acceso por aplicación a las aplicaciones SaaS.</span><span class="sxs-lookup"><span data-stu-id="89aa9-131">Configure per-application access rules to your SaaS apps.</span></span> <span data-ttu-id="89aa9-132">Por ejemplo, puede obligar a utilizar MFA o solo permitir el acceso a usuarios de redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="89aa9-132">For example, you can require MFA or only allow access to users on trusted networks.</span></span> <span data-ttu-id="89aa9-133">En el documento de [configuración de las reglas de acceso](active-directory-conditional-access-azuread-connected-apps.md)se muestran los detalles pertinentes.</span><span class="sxs-lookup"><span data-stu-id="89aa9-133">The details for this are available in the document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-the-app-to-require-user-assignment-and-assign-users"></a><span data-ttu-id="89aa9-134">Configurar la aplicación para requerir asignación de usuarios y asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="89aa9-134">Configure the app to require user assignment and assign users</span></span>
<span data-ttu-id="89aa9-135">De forma predeterminada, los usuarios pueden acceder a las aplicaciones sin asignación previa.</span><span class="sxs-lookup"><span data-stu-id="89aa9-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="89aa9-136">Sin embargo, si la aplicación expone roles o si quiere que aparezca en el panel de acceso de un usuario, debe requerir la asignación de usuarios.</span><span class="sxs-lookup"><span data-stu-id="89aa9-136">However, if the application exposes roles or if you want the application to appear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="89aa9-137">Necesidad de asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="89aa9-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="89aa9-138">Si es un suscriptor de Azure AD Premium o Enterprise Mobility Suite (EMS), se recomienda encarecidamente utilizar grupos.</span><span class="sxs-lookup"><span data-stu-id="89aa9-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="89aa9-139">La asignación de grupos a la aplicación permite delegar la administración del acceso continuo al propietario del grupo.</span><span class="sxs-lookup"><span data-stu-id="89aa9-139">Assigning groups to the application allows you to delegate ongoing access management to the owner of the group.</span></span> <span data-ttu-id="89aa9-140">Puede crear el grupo o pedir a la parte responsable de la organización que lo haga usando sus recursos de administración de grupos.</span><span class="sxs-lookup"><span data-stu-id="89aa9-140">You can create the group or ask the responsible party in your organization to create the group using your group management facility.</span></span>

[<span data-ttu-id="89aa9-141">Asignación de usuarios a una aplicación</span><span class="sxs-lookup"><span data-stu-id="89aa9-141">Assigning users to an application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="89aa9-142">Asignación de grupos a una aplicación</span><span class="sxs-lookup"><span data-stu-id="89aa9-142">Assigning groups to an application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="89aa9-143">Supresión del consentimiento del usuario</span><span class="sxs-lookup"><span data-stu-id="89aa9-143">Suppress user consent</span></span>
<span data-ttu-id="89aa9-144">De forma predeterminada, los usuarios otorgan su consentimiento para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="89aa9-144">By default, each user goes through a consent experience to sign in.</span></span> <span data-ttu-id="89aa9-145">El consentimiento, que se solicita para conceder permisos a una aplicación, puede desconcertar a los usuarios que no estén familiarizados con la toma de este tipo de decisiones.</span><span class="sxs-lookup"><span data-stu-id="89aa9-145">The consent experience, asking users to grant permissions to an application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="89aa9-146">Para aplicaciones de confianza, puede otorgar el consentimiento para la aplicación en nombre de su organización con el fin de simplificar la experiencia de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="89aa9-146">For applications that you trust, you can simplify the user experience by consenting to the application on behalf of your organization.</span></span>

<span data-ttu-id="89aa9-147">Para obtener más información sobre el consentimiento de usuarios y cómo se utiliza esta característica en Azure, consulte [Integración de aplicaciones con Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="89aa9-147">For more information about user consent and the consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="89aa9-148">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="89aa9-148">Related Articles</span></span>
* [<span data-ttu-id="89aa9-149">Provisión de acceso remoto seguro a aplicaciones locales</span><span class="sxs-lookup"><span data-stu-id="89aa9-149">Enable secure remote access to on-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="89aa9-150">Acceso condicional de Azure en versión de vista previa para aplicaciones SaaS</span><span class="sxs-lookup"><span data-stu-id="89aa9-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="89aa9-151">Administración del acceso a las aplicaciones con Azure AD</span><span class="sxs-lookup"><span data-stu-id="89aa9-151">Managing access to apps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="89aa9-152">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89aa9-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
