---
title: "Referencia técnica del acceso condicional de Azure Active Directory | Microsoft Docs"
description: "Con el control de acceso condicional, Azure Active Directory comprueba las condiciones específicas que se eligen al autenticar al usuario y antes de permitirle acceso a la aplicación. Si se cumplen las condiciones, el usuario queda autenticado y se le permite el acceso a la aplicación."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca16a5399f94fd1ab267e0798cade3fd83f75b13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="1dab5-104">Referencia técnica del acceso condicional de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1dab5-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="1dab5-105">Servicios habilitados con acceso condicional</span><span class="sxs-lookup"><span data-stu-id="1dab5-105">Services enabled with conditional access</span></span>

<span data-ttu-id="1dab5-106">Las reglas de acceso condicional se admiten en varios tipos de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dab5-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="1dab5-107">Esta lista incluye:</span><span class="sxs-lookup"><span data-stu-id="1dab5-107">This list includes:</span></span>


* <span data-ttu-id="1dab5-108">Aplicaciones registradas con el proxy de aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="1dab5-108">Applications registered with the Azure Application Proxy</span></span>
* <span data-ttu-id="1dab5-109">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="1dab5-109">Azure Remote App</span></span>
* <span data-ttu-id="1dab5-110">Aplicaciones desarrolladas de línea de negocio y multiinquilino registradas con Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dab5-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="1dab5-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="1dab5-111">Dynamics CRM</span></span>
* <span data-ttu-id="1dab5-112">Aplicaciones federadas de la Galería de aplicaciones de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dab5-112">Federated applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="1dab5-113">Yammer de Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="1dab5-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="1dab5-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="1dab5-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="1dab5-115">Microsoft Office 365 SharePoint Online (incluye OneDrive para la Empresa)</span><span class="sxs-lookup"><span data-stu-id="1dab5-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="1dab5-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="1dab5-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="1dab5-117">Aplicaciones de inicio de sesión único con contraseña de la Galería de aplicaciones de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dab5-117">Password SSO applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="1dab5-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="1dab5-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="1dab5-119">Equipos de Microsoft</span><span class="sxs-lookup"><span data-stu-id="1dab5-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="1dab5-120">Habilitación de reglas de acceso</span><span class="sxs-lookup"><span data-stu-id="1dab5-120">Enable access rules</span></span>
<span data-ttu-id="1dab5-121">Cada regla puede habilitarse o deshabilitarse en función de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1dab5-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="1dab5-122">Cuando las reglas estén **ACTIVADAS** , se habilitarán y se aplicarán a los usuarios que accedan a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1dab5-122">When rules are **ON** they will be enabled and enforced for users accessing the application.</span></span> <span data-ttu-id="1dab5-123">Cuando estén **DESACTIVADAS** , no se usarán ni afectarán a la experiencia de inicio de sesión de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1dab5-123">When they are **OFF** they will not be used and will not impact the users sign in experience.</span></span>

## <a name="applying-rules-to-specific-users"></a><span data-ttu-id="1dab5-124">Aplicación de reglas a usuarios específicos</span><span class="sxs-lookup"><span data-stu-id="1dab5-124">Applying rules to specific users</span></span>
<span data-ttu-id="1dab5-125">Las reglas se pueden aplicar a conjuntos específicos de usuarios basados enun grupo de seguridad mediante la configuración de **Aplicar a**.</span><span class="sxs-lookup"><span data-stu-id="1dab5-125">Rules can be applied to specific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="1dab5-126">**Aplicar a** puede establecerse en **Todos los usuarios** o **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="1dab5-126">**Apply To** can be set to **All Users** or **Groups**.</span></span> <span data-ttu-id="1dab5-127">Cuando esté establecido en **Todos los usuarios** , las reglas se aplicarán a cualquier usuario con acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1dab5-127">When set to **All Users** the rules will apply to any user with access to the application.</span></span> <span data-ttu-id="1dab5-128">La opción **Grupos** permite seleccionar grupos de seguridad y distribución específicos; las reglas solo se aplicarán a estos grupos.</span><span class="sxs-lookup"><span data-stu-id="1dab5-128">The **Groups** option allows specific security and distribution groups to be selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="1dab5-129">Al implementar una regla, se suele aplicar primero a un conjunto limitado de usuarios que sean miembros de grupos piloto.</span><span class="sxs-lookup"><span data-stu-id="1dab5-129">When deploying a rule,  it is common to first apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="1dab5-130">Una vez finalizada la regla, puede aplicarse a **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1dab5-130">Once complete the rule can be applied to **All Users**.</span></span> <span data-ttu-id="1dab5-131">Esto hará que la regla se pueda exigir a todos los usuarios de la organización.</span><span class="sxs-lookup"><span data-stu-id="1dab5-131">This will cause the rule to be enforced for all users in the organization.</span></span>

<span data-ttu-id="1dab5-132">Asimismo, se pueden excluir de la directiva grupos seleccionados mediante la opción **Excepto** .</span><span class="sxs-lookup"><span data-stu-id="1dab5-132">Select groups may also be exempted from policy using the **Except** option.</span></span> <span data-ttu-id="1dab5-133">Aunque aparezcan en un grupo incluido, todos los miembros de estos grupos quedarán excluidos.</span><span class="sxs-lookup"><span data-stu-id="1dab5-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="1dab5-134">Redes "en el trabajo"</span><span class="sxs-lookup"><span data-stu-id="1dab5-134">“At work” networks</span></span>
<span data-ttu-id="1dab5-135">Las reglas de acceso condicional que utilizan una red "en el trabajo" dependen de intervalos de direcciones IP de confianza que se han configurado en Azure AD, o del uso de la notificación "dentro de la red corporativa" de AD FS.</span><span class="sxs-lookup"><span data-stu-id="1dab5-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of the "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="1dab5-136">Estas reglas incluyen:</span><span class="sxs-lookup"><span data-stu-id="1dab5-136">These rules include:</span></span>

* <span data-ttu-id="1dab5-137">Requerir autenticación multifactor fuera del trabajo</span><span class="sxs-lookup"><span data-stu-id="1dab5-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="1dab5-138">Bloquear el acceso fuera del trabajo</span><span class="sxs-lookup"><span data-stu-id="1dab5-138">Block access when not at work</span></span>

<span data-ttu-id="1dab5-139">Opciones para especificar redes "en el trabajo"</span><span class="sxs-lookup"><span data-stu-id="1dab5-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="1dab5-140">Configurar intervalos de direcciones IP de confianza en la [página de configuración de la autenticación multifactor](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="1dab5-140">Configure trusted IP address ranges in the [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="1dab5-141">La directiva de acceso condicional usará los intervalos configurados en cada solicitud de autenticación y emisión de tokens para evaluar las reglas.</span><span class="sxs-lookup"><span data-stu-id="1dab5-141">Conditional Access policy will use the configured ranges on each authentication request and token issuance to evaluate rules.</span></span> 
2. <span data-ttu-id="1dab5-142">Configurar el uso de la notificación "dentro de la red corporativa"; esta opción se puede usar con directorios federados mediante AD FS.</span><span class="sxs-lookup"><span data-stu-id="1dab5-142">Configure use of the inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="1dab5-143">Para obtener más información sobre las notificaciones internas de corpnet , consulte [IP de confianza](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="1dab5-143">To learn more about the inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="1dab5-144">Reglas basadas en la confidencialidad de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="1dab5-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="1dab5-145">Las reglas se configuran por aplicación, lo que permite a los servicios de alto valor estar protegidos sin que se vea afectado el acceso a otros servicios.</span><span class="sxs-lookup"><span data-stu-id="1dab5-145">Rules are configured per application allowing the high value services to be secured without impacting access to other services.</span></span> <span data-ttu-id="1dab5-146">Se pueden configurar reglas de acceso condicional en la pestaña **Configurar** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1dab5-146">Conditional access rules can be configured on the  **Configure** tab of the application.</span></span> 

<span data-ttu-id="1dab5-147">Reglas que se ofrecen actualmente:</span><span class="sxs-lookup"><span data-stu-id="1dab5-147">Rules currently offered:</span></span>

* <span data-ttu-id="1dab5-148">**Requerir autenticación multifactor**</span><span class="sxs-lookup"><span data-stu-id="1dab5-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="1dab5-149">Todos los usuarios a los que se aplica la directiva deberán autenticarse mediante la autenticación multifactor al menos una vez.</span><span class="sxs-lookup"><span data-stu-id="1dab5-149">All users that this policy is applied to will be required to authenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="1dab5-150">**Requerir autenticación multifactor fuera del trabajo**</span><span class="sxs-lookup"><span data-stu-id="1dab5-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="1dab5-151">Si se aplica esta directiva, se exigirá a todos los usuarios que realicen la autenticación multifactor al menos una vez si acceden al servicio desde una ubicación remota fuera del trabajo.</span><span class="sxs-lookup"><span data-stu-id="1dab5-151">If this policy is applied, all users will be required to have performed multi-factor authentication at least once if they access the service from a non-work remote location.</span></span> <span data-ttu-id="1dab5-152">Si pasan de una ubicación en el trabajo a una ubicación remota, se les exigirá que realicen la autenticación multifactor cuando accedan al servicio.</span><span class="sxs-lookup"><span data-stu-id="1dab5-152">If they move from a work to remote location, they will be required to perform multifactor authentication when accessing the service.</span></span>
* <span data-ttu-id="1dab5-153">**Bloquear el acceso fuera del trabajo**</span><span class="sxs-lookup"><span data-stu-id="1dab5-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="1dab5-154">Cuando los usuarios pasan de una ubicación en el trabajo a una ubicación remota, se les bloqueará si se les aplica la directiva "Bloquear acceso cuando no está en el trabajo".</span><span class="sxs-lookup"><span data-stu-id="1dab5-154">When users move from work to a remote location, they will be blocked if the "Block access when not at work" policy is applied to them.</span></span>  <span data-ttu-id="1dab5-155">Se les volverá a permitir el acceso cuando estén en una ubicación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1dab5-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="1dab5-156">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="1dab5-156">Related topics</span></span>
* [<span data-ttu-id="1dab5-157">Protección del acceso a Office 365 y otras aplicaciones conectadas a Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1dab5-157">Securing access to Office 365 and other apps connected to Azure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="1dab5-158">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1dab5-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

