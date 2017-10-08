---
title: "prácticas recomendadas de aaaBest para el acceso condicional en Active Directory de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de las cosas que debe saber y lo que se debe evitar hacer al configurar directivas de acceso condicional."
services: active-directory
keywords: tooapps de acceso condicional, el acceso condicional con Azure AD, proteger el acceso toocompany recursos, las directivas de acceso condicional
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="f13c5-104">Procedimientos recomendados para el acceso condicional en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f13c5-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="f13c5-105">En este tema se proporciona información acerca de las cosas que debe saber y lo que se debe evitar hacer al configurar directivas de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="f13c5-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="f13c5-106">Antes de leer este tema, debe familiarizarse con los conceptos de Hola y terminología de Hola que se describe en [acceso condicional en Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f13c5-106">Before reading this topic, you should familiarize yourself with hello concepts and hello terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="f13c5-107">Qué debería saber</span><span class="sxs-lookup"><span data-stu-id="f13c5-107">What you should know</span></span>

### <a name="whats-required-toomake-a-policy-work"></a><span data-ttu-id="f13c5-108">¿Qué le ha exigido toomake un trabajo de directiva?</span><span class="sxs-lookup"><span data-stu-id="f13c5-108">What’s required toomake a policy work?</span></span>

<span data-ttu-id="f13c5-109">Cuando crea una nueva directiva, no hay usuarios, grupos, aplicaciones o controles de acceso seleccionados.</span><span class="sxs-lookup"><span data-stu-id="f13c5-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Aplicaciones de nube](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="f13c5-111">toomake funcionan de la directiva, debe configurar los siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="f13c5-111">toomake your policy work, you must configure hello following:</span></span>


|<span data-ttu-id="f13c5-112">Qué</span><span class="sxs-lookup"><span data-stu-id="f13c5-112">What</span></span>           | <span data-ttu-id="f13c5-113">Cómo</span><span class="sxs-lookup"><span data-stu-id="f13c5-113">How</span></span>                                  | <span data-ttu-id="f13c5-114">Porqué</span><span class="sxs-lookup"><span data-stu-id="f13c5-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="f13c5-115">**Aplicaciones en la nube**</span><span class="sxs-lookup"><span data-stu-id="f13c5-115">**Cloud apps**</span></span> |<span data-ttu-id="f13c5-116">Debe tooselect una o más aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f13c5-116">You need tooselect one or more apps.</span></span>  | <span data-ttu-id="f13c5-117">objetivo de Hola de una directiva de acceso condicional es tooenable toofine optimizar cómo los usuarios autorizados pueden tener acceso a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f13c5-117">hello goal of a conditional access policy is tooenable you toofine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="f13c5-118">**Usuarios y grupos**</span><span class="sxs-lookup"><span data-stu-id="f13c5-118">**Users and groups**</span></span> | <span data-ttu-id="f13c5-119">Necesita tooselect al menos un usuario o grupo que está autorizado tooaccess hello las aplicaciones de nube que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="f13c5-119">You need tooselect at least one user or group that is authorized tooaccess hello cloud apps you have selected.</span></span> | <span data-ttu-id="f13c5-120">Una directiva de acceso condicional que no tiene usuarios ni grupos asignados nunca se desencadena.</span><span class="sxs-lookup"><span data-stu-id="f13c5-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="f13c5-121">**Controles de acceso**</span><span class="sxs-lookup"><span data-stu-id="f13c5-121">**Access controls**</span></span> | <span data-ttu-id="f13c5-122">Necesita tooselect al menos un control de acceso.</span><span class="sxs-lookup"><span data-stu-id="f13c5-122">You need tooselect at least one access control.</span></span> | <span data-ttu-id="f13c5-123">El procesador de directivas necesita tooknow qué toodo si se cumplen las condiciones.</span><span class="sxs-lookup"><span data-stu-id="f13c5-123">Your policy processor needs tooknow what toodo if your conditions are satisfied.</span></span>|


<span data-ttu-id="f13c5-124">Suma toothese básica en requisitos en, en muchos casos, también debe configurar una condición.</span><span class="sxs-lookup"><span data-stu-id="f13c5-124">In addition toothese basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="f13c5-125">Mientras una directiva también funcionará sin una condición configurada, las condiciones son un factor determinante para optimizar las aplicaciones de acceso tooyour Hola.</span><span class="sxs-lookup"><span data-stu-id="f13c5-125">While a policy would also work without a configured condition, conditions are hello driving factor for fine-tuning access tooyour apps.</span></span>


![Aplicaciones de nube](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="f13c5-127">¿Cómo se evalúan las asignaciones?</span><span class="sxs-lookup"><span data-stu-id="f13c5-127">How are assignments evaluated?</span></span>

<span data-ttu-id="f13c5-128">A todas las asignaciones se les asigna **la operación lógica AND**.</span><span class="sxs-lookup"><span data-stu-id="f13c5-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="f13c5-129">Si tiene más de una asignación configurada, tootrigger una directiva, deben cumplirse todas las asignaciones.</span><span class="sxs-lookup"><span data-stu-id="f13c5-129">If you have more than one assignment configured, tootrigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="f13c5-130">Si necesita tooconfigure una condición de ubicación que se aplica a las conexiones de tooall realizadas desde fuera de la red de su organización, puede hacerlo mediante:</span><span class="sxs-lookup"><span data-stu-id="f13c5-130">If you need tooconfigure a location condition that applies tooall connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="f13c5-131">Incluir **todas las ubicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f13c5-131">Including **All locations**</span></span>
- <span data-ttu-id="f13c5-132">Excluir **todas las direcciones IP de confianza**.</span><span class="sxs-lookup"><span data-stu-id="f13c5-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="f13c5-133">¿Qué ocurre si tiene las directivas de hello portal de Azure clásico y portal de Azure configurado?</span><span class="sxs-lookup"><span data-stu-id="f13c5-133">What happens if you have policies in hello Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="f13c5-134">Las dos directivas se aplican mediante Azure Active Directory usuario hello, obteniendo así acceso únicamente cuando se cumplen todos los requisitos.</span><span class="sxs-lookup"><span data-stu-id="f13c5-134">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a><span data-ttu-id="f13c5-135">¿Qué ocurre si tiene las directivas de Intune Silverlight portal Hola y Hola Portal de Azure?</span><span class="sxs-lookup"><span data-stu-id="f13c5-135">What happens if you have policies in hello Intune Silverlight portal and hello Azure Portal?</span></span>
<span data-ttu-id="f13c5-136">Las dos directivas se aplican mediante Azure Active Directory usuario hello, obteniendo así acceso únicamente cuando se cumplen todos los requisitos.</span><span class="sxs-lookup"><span data-stu-id="f13c5-136">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a><span data-ttu-id="f13c5-137">¿Qué ocurre si tengo varias directivas para hello configurada por el mismo usuario?</span><span class="sxs-lookup"><span data-stu-id="f13c5-137">What happens if I have multiple policies for hello same user configured?</span></span>  
<span data-ttu-id="f13c5-138">Para cada inicio de sesión, Azure Active Directory evalúa todas las directivas y se asegura de que se cumplen todos los requisitos antes de concedidos a los usuarios acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="f13c5-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access toohello user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="f13c5-139">¿Funciona el acceso condicional con Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="f13c5-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="f13c5-140">Sí, se puede usar Exchange ActiveSync en una directiva de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="f13c5-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="f13c5-141">¿Qué no debería hacer?</span><span class="sxs-lookup"><span data-stu-id="f13c5-141">What you should avoid doing</span></span>

<span data-ttu-id="f13c5-142">marco de trabajo de acceso condicional de Hello proporciona una flexibilidad de configuración excelente.</span><span class="sxs-lookup"><span data-stu-id="f13c5-142">hello conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="f13c5-143">Sin embargo, gran flexibilidad significa también que debe revisar cuidadosamente cada tooreleasing anteriores de directiva de configuración tooavoid de resultados no deseados.</span><span class="sxs-lookup"><span data-stu-id="f13c5-143">However, great flexibility  also means that you should carefully review each configuration policy prior tooreleasing it tooavoid undesirable results.</span></span> <span data-ttu-id="f13c5-144">En este contexto, debe prestar tooassignments atención especial que afecte a los conjuntos completos como **todos los usuarios / grupos y aplicaciones de la nube**.</span><span class="sxs-lookup"><span data-stu-id="f13c5-144">In this context, you should pay special attention tooassignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="f13c5-145">En su entorno, debería evitar Hola siguiendo configuraciones:</span><span class="sxs-lookup"><span data-stu-id="f13c5-145">In your environment, you should avoid hello following configurations:</span></span>


<span data-ttu-id="f13c5-146">**Para todos los usuarios, todas las aplicaciones en la nube:**</span><span class="sxs-lookup"><span data-stu-id="f13c5-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="f13c5-147">**Bloquear acceso**: esta configuración bloquea toda la organización, lo cual no es en absoluto una buena idea.</span><span class="sxs-lookup"><span data-stu-id="f13c5-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="f13c5-148">**Esta opción requiere un dispositivo compatible con** : para los usuarios que no se han inscrito sus dispositivos aún, esta directiva bloquea todo el acceso incluido acceso toohello Intune portal.</span><span class="sxs-lookup"><span data-stu-id="f13c5-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access toohello Intune portal.</span></span> <span data-ttu-id="f13c5-149">Si eres un administrador sin un dispositivo inscrito, esta directiva bloquea de vuelta a la directiva de hello toochange portal Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="f13c5-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into hello Azure portal toochange hello policy.</span></span>

- <span data-ttu-id="f13c5-150">**Requerir unión a un dominio** : este bloque de directivas acceso tiene también Hola posibles tooblock acceso para todos los usuarios de su organización si todavía no tienes un dispositivo unido al dominio.</span><span class="sxs-lookup"><span data-stu-id="f13c5-150">**Require domain join** - This policy block access has also hello potential tooblock access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="f13c5-151">**Para todos los usuarios, todas las aplicaciones en la nube, todas las plataformas de dispositivos:**</span><span class="sxs-lookup"><span data-stu-id="f13c5-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="f13c5-152">**Bloquear acceso**: esta configuración bloquea toda la organización, lo cual no es en absoluto una buena idea.</span><span class="sxs-lookup"><span data-stu-id="f13c5-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="f13c5-153">Escenarios comunes</span><span class="sxs-lookup"><span data-stu-id="f13c5-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="f13c5-154">Exigir autenticación multifactor para las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f13c5-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="f13c5-155">Muchos entornos tienen las aplicaciones que requieren un mayor nivel de protección que Hola otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="f13c5-155">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="f13c5-156">Esto sucede, por ejemplo, hello para aplicaciones que tienen acceso a los datos toosensitive.</span><span class="sxs-lookup"><span data-stu-id="f13c5-156">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="f13c5-157">Si desea tooadd otro nivel de protección toothese aplicaciones, puede configurar una directiva de acceso condicional que requiere la autenticación multifactor cuando los usuarios tienen acceso a estas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f13c5-157">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="f13c5-158">Exigir autenticación multifactor para el acceso desde redes que no son de confianza</span><span class="sxs-lookup"><span data-stu-id="f13c5-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="f13c5-159">Este escenario es similar toohello anterior porque agrega un requisito para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="f13c5-159">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="f13c5-160">Sin embargo, Hola principal diferencia es condición Hola para este requisito.</span><span class="sxs-lookup"><span data-stu-id="f13c5-160">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="f13c5-161">Mientras se estaba foco Hola del escenario anterior hello en aplicaciones con acceso a los datos toosensitve, Hola de este escenario es ubicaciones de confianza.</span><span class="sxs-lookup"><span data-stu-id="f13c5-161">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="f13c5-162">En otras palabras, podría tener un requisito de autenticación multifactor si un usuario accede a una aplicación desde una red que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="f13c5-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="f13c5-163">Solo los dispositivos de confianza pueden acceder a servicios de Office 365</span><span class="sxs-lookup"><span data-stu-id="f13c5-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="f13c5-164">Si usa Intune en su entorno, inmediatamente puede comenzar a usar la interfaz de directiva de acceso condicional de Hola Hola consola de Azure.</span><span class="sxs-lookup"><span data-stu-id="f13c5-164">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="f13c5-165">Muchos clientes de Intune usa tooensure de acceso condicional que solo los dispositivos de confianza pueden tener acceso a servicios de Office 365.</span><span class="sxs-lookup"><span data-stu-id="f13c5-165">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="f13c5-166">Esto significa que los dispositivos móviles inscriben con Intune y cumplan los requisitos de directiva de cumplimiento de normas y que los equipos con Windows son tooan Unidos a un dominio de local.</span><span class="sxs-lookup"><span data-stu-id="f13c5-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="f13c5-167">Una importante mejora es que no haya tooset Hola misma directiva para cada uno de los servicios de hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="f13c5-167">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="f13c5-168">Cuando se crea una nueva directiva, configure hello en la nube aplicaciones tooinclude cada de las aplicaciones de Office 365 Hola que desee tooprotect con el acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="f13c5-168">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f13c5-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f13c5-169">Next steps</span></span>

<span data-ttu-id="f13c5-170">Si desea tooknow tooconfigure una directiva de acceso condicional, vea [empezar a trabajar con el acceso condicional en Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f13c5-170">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
