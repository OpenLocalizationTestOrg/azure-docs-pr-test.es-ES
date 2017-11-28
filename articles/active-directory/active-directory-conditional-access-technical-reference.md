---
title: "referencia técnica de acceso condicional de Active Directory aaaAzure | Documentos de Microsoft"
description: "Con control de acceso condicional, Azure Active Directory comprueba las condiciones específicas de Hola que elegir al autenticar usuario hello y antes de permitir el acceso toohello aplicación. Una vez que se cumplen estas condiciones, usuario de hello es autenticado y acceso toohello aplicación permitida."
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
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="03145-104">Referencia técnica del acceso condicional de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03145-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="03145-105">Servicios habilitados con acceso condicional</span><span class="sxs-lookup"><span data-stu-id="03145-105">Services enabled with conditional access</span></span>

<span data-ttu-id="03145-106">Las reglas de acceso condicional se admiten en varios tipos de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03145-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="03145-107">Esta lista incluye:</span><span class="sxs-lookup"><span data-stu-id="03145-107">This list includes:</span></span>


* <span data-ttu-id="03145-108">Aplicaciones registradas con hello Proxy de aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="03145-108">Applications registered with hello Azure Application Proxy</span></span>
* <span data-ttu-id="03145-109">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="03145-109">Azure Remote App</span></span>
* <span data-ttu-id="03145-110">Aplicaciones desarrolladas de línea de negocio y multiinquilino registradas con Azure AD</span><span class="sxs-lookup"><span data-stu-id="03145-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="03145-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="03145-111">Dynamics CRM</span></span>
* <span data-ttu-id="03145-112">Aplicaciones federadas de galería de aplicaciones de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="03145-112">Federated applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="03145-113">Yammer de Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="03145-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="03145-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="03145-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="03145-115">Microsoft Office 365 SharePoint Online (incluye OneDrive para la Empresa)</span><span class="sxs-lookup"><span data-stu-id="03145-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="03145-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="03145-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="03145-117">Aplicaciones de SSO de contraseña desde galería de aplicaciones de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="03145-117">Password SSO applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="03145-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="03145-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="03145-119">Equipos de Microsoft</span><span class="sxs-lookup"><span data-stu-id="03145-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="03145-120">Habilitación de reglas de acceso</span><span class="sxs-lookup"><span data-stu-id="03145-120">Enable access rules</span></span>
<span data-ttu-id="03145-121">Cada regla puede habilitarse o deshabilitarse en función de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03145-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="03145-122">Cuando las reglas son **ON** serán habilitados y se exige para los usuarios que acceden a la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="03145-122">When rules are **ON** they will be enabled and enforced for users accessing hello application.</span></span> <span data-ttu-id="03145-123">Cuando se encuentran **OFF** no se utilizará y firmará no los usuarios de Hola de impacto en experiencia.</span><span class="sxs-lookup"><span data-stu-id="03145-123">When they are **OFF** they will not be used and will not impact hello users sign in experience.</span></span>

## <a name="applying-rules-toospecific-users"></a><span data-ttu-id="03145-124">Aplicar a los usuarios de las reglas toospecific</span><span class="sxs-lookup"><span data-stu-id="03145-124">Applying rules toospecific users</span></span>
<span data-ttu-id="03145-125">Las reglas pueden ser toospecific aplicado conjuntos de usuarios basados en el grupo de seguridad estableciendo **aplicar a**.</span><span class="sxs-lookup"><span data-stu-id="03145-125">Rules can be applied toospecific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="03145-126">**Aplicar a** puede establecerse demasiado**todos los usuarios** o **grupos**.</span><span class="sxs-lookup"><span data-stu-id="03145-126">**Apply To** can be set too**All Users** or **Groups**.</span></span> <span data-ttu-id="03145-127">Cuando se establece demasiado**todos los usuarios** aplicarán a las reglas de hello tooany usuario con la aplicación de access toohello.</span><span class="sxs-lookup"><span data-stu-id="03145-127">When set too**All Users** hello rules will apply tooany user with access toohello application.</span></span> <span data-ttu-id="03145-128">Hola **grupos** opción permite la seguridad específica y toobe de grupos de distribución seleccionado, solo se aplicarán las reglas para estos grupos.</span><span class="sxs-lookup"><span data-stu-id="03145-128">hello **Groups** option allows specific security and distribution groups toobe selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="03145-129">Al implementar una regla, es común toofirst aplica un conjunto limitado de usuarios, que son miembros de un grupo piloto.</span><span class="sxs-lookup"><span data-stu-id="03145-129">When deploying a rule,  it is common toofirst apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="03145-130">Una vez que se pueden aplicar reglas de hello completa demasiado**todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="03145-130">Once complete hello rule can be applied too**All Users**.</span></span> <span data-ttu-id="03145-131">Esto hará que la regla de hello toobe obligatorio para todos los usuarios de la organización de Hola.</span><span class="sxs-lookup"><span data-stu-id="03145-131">This will cause hello rule toobe enforced for all users in hello organization.</span></span>

<span data-ttu-id="03145-132">Seleccione grupos también pueden excluirse de la directiva mediante hello **excepto** opción.</span><span class="sxs-lookup"><span data-stu-id="03145-132">Select groups may also be exempted from policy using hello **Except** option.</span></span> <span data-ttu-id="03145-133">Aunque aparezcan en un grupo incluido, todos los miembros de estos grupos quedarán excluidos.</span><span class="sxs-lookup"><span data-stu-id="03145-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="03145-134">Redes "en el trabajo"</span><span class="sxs-lookup"><span data-stu-id="03145-134">“At work” networks</span></span>
<span data-ttu-id="03145-135">Las reglas de acceso condicional que usan una red "en el trabajo", que se basan en confianza intervalos de direcciones IP que se han configurado en Azure AD, o el uso de Hola "dentro de la red corporativa" notificaciones de AD FS.</span><span class="sxs-lookup"><span data-stu-id="03145-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of hello "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="03145-136">Estas reglas incluyen:</span><span class="sxs-lookup"><span data-stu-id="03145-136">These rules include:</span></span>

* <span data-ttu-id="03145-137">Requerir autenticación multifactor fuera del trabajo</span><span class="sxs-lookup"><span data-stu-id="03145-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="03145-138">Bloquear el acceso fuera del trabajo</span><span class="sxs-lookup"><span data-stu-id="03145-138">Block access when not at work</span></span>

<span data-ttu-id="03145-139">Opciones para especificar redes "en el trabajo"</span><span class="sxs-lookup"><span data-stu-id="03145-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="03145-140">Configurar intervalos de direcciones IP de confianza en hello [página de configuración de la autenticación multifactor](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="03145-140">Configure trusted IP address ranges in hello [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="03145-141">Directiva de acceso condicional utilizará intervalos Hola configurado en cada solicitud y el token de emisión tooevaluate las reglas de autenticación.</span><span class="sxs-lookup"><span data-stu-id="03145-141">Conditional Access policy will use hello configured ranges on each authentication request and token issuance tooevaluate rules.</span></span> 
2. <span data-ttu-id="03145-142">Configurar el uso de hello dentro de notificación de la red corporativa, esta opción puede utilizarse con directorios federados, mediante AD FS.</span><span class="sxs-lookup"><span data-stu-id="03145-142">Configure use of hello inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="03145-143">toolearn más información acerca de hello dentro de notificaciones de la red corporativa, consulte [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="03145-143">toolearn more about hello inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="03145-144">Reglas basadas en la confidencialidad de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="03145-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="03145-145">Las reglas se configuran por aplicación lo que Hola valiosos servicios toobe protegida sin afectar a los servicios de acceso tooother.</span><span class="sxs-lookup"><span data-stu-id="03145-145">Rules are configured per application allowing hello high value services toobe secured without impacting access tooother services.</span></span> <span data-ttu-id="03145-146">Se pueden configurar reglas de acceso condicional en hello **configurar** pestaña de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="03145-146">Conditional access rules can be configured on hello  **Configure** tab of hello application.</span></span> 

<span data-ttu-id="03145-147">Reglas que se ofrecen actualmente:</span><span class="sxs-lookup"><span data-stu-id="03145-147">Rules currently offered:</span></span>

* <span data-ttu-id="03145-148">**Requerir autenticación multifactor**</span><span class="sxs-lookup"><span data-stu-id="03145-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="03145-149">Todos los usuarios que esta directiva se aplica toowill ser necesario tooauthenticate a través de la autenticación multifactor al menos una vez.</span><span class="sxs-lookup"><span data-stu-id="03145-149">All users that this policy is applied toowill be required tooauthenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="03145-150">**Requerir autenticación multifactor fuera del trabajo**</span><span class="sxs-lookup"><span data-stu-id="03145-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="03145-151">Si se aplica esta directiva, todos los usuarios será necesario toohave realiza la autenticación multifactor al menos una vez si tienen acceso a servicio de Hola desde una ubicación remota no laborables.</span><span class="sxs-lookup"><span data-stu-id="03145-151">If this policy is applied, all users will be required toohave performed multi-factor authentication at least once if they access hello service from a non-work remote location.</span></span> <span data-ttu-id="03145-152">Si mueve desde una ubicación de tooremote de trabajo, al obtener acceso a servicios de hello estará tooperform requiere la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="03145-152">If they move from a work tooremote location, they will be required tooperform multifactor authentication when accessing hello service.</span></span>
* <span data-ttu-id="03145-153">**Bloquear el acceso fuera del trabajo**</span><span class="sxs-lookup"><span data-stu-id="03145-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="03145-154">Cuando el usuario cambia de ubicación remota de tooa de trabajo, se bloqueará si directiva "Bloquear el acceso fuera del trabajo" hello es toothem aplicada.</span><span class="sxs-lookup"><span data-stu-id="03145-154">When users move from work tooa remote location, they will be blocked if hello "Block access when not at work" policy is applied toothem.</span></span>  <span data-ttu-id="03145-155">Se les volverá a permitir el acceso cuando estén en una ubicación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="03145-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="03145-156">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="03145-156">Related topics</span></span>
* [<span data-ttu-id="03145-157">Proteger el acceso tooOffice 365 y otras aplicaciones conectadas tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03145-157">Securing access tooOffice 365 and other apps connected tooAzure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="03145-158">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03145-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

