---
title: Procedimientos recomendados para el acceso condicional en Azure Active Directory | Microsoft Docs
description: "Obtenga información acerca de las cosas que debe saber y lo que se debe evitar hacer al configurar directivas de acceso condicional."
services: active-directory
keywords: acceso condicional a aplicaciones, acceso condicional con Azure AD, acceso seguro a recursos de empresa, directivas de acceso condicional
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
ms.openlocfilehash: 3e524c116479c1af6eb6a601c9b57d27a697c5a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="f3fc6-104">Procedimientos recomendados para el acceso condicional en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3fc6-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="f3fc6-105">En este tema se proporciona información acerca de las cosas que debe saber y lo que se debe evitar hacer al configurar directivas de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="f3fc6-106">Antes de leer este tema, debe familiarizarse con los conceptos y la terminología que se describe en [Acceso condicional en Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f3fc6-106">Before reading this topic, you should familiarize yourself with the concepts and the terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="f3fc6-107">Qué debería saber</span><span class="sxs-lookup"><span data-stu-id="f3fc6-107">What you should know</span></span>

### <a name="whats-required-to-make-a-policy-work"></a><span data-ttu-id="f3fc6-108">¿Cuáles son los requisitos para realizar un trabajo de directiva?</span><span class="sxs-lookup"><span data-stu-id="f3fc6-108">What’s required to make a policy work?</span></span>

<span data-ttu-id="f3fc6-109">Cuando crea una nueva directiva, no hay usuarios, grupos, aplicaciones o controles de acceso seleccionados.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Aplicaciones en la nube](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="f3fc6-111">Para realizar un trabajo de directiva, debe configurar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f3fc6-111">To make your policy work, you must configure the following:</span></span>


|<span data-ttu-id="f3fc6-112">Qué</span><span class="sxs-lookup"><span data-stu-id="f3fc6-112">What</span></span>           | <span data-ttu-id="f3fc6-113">Cómo</span><span class="sxs-lookup"><span data-stu-id="f3fc6-113">How</span></span>                                  | <span data-ttu-id="f3fc6-114">Porqué</span><span class="sxs-lookup"><span data-stu-id="f3fc6-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="f3fc6-115">**Aplicaciones en la nube**</span><span class="sxs-lookup"><span data-stu-id="f3fc6-115">**Cloud apps**</span></span> |<span data-ttu-id="f3fc6-116">Tiene que seleccionar una o más aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-116">You need to select one or more apps.</span></span>  | <span data-ttu-id="f3fc6-117">El objetivo de la directiva de acceso condicional es permitirle que realice un mejor ajuste sobre cómo los usuarios autorizados pueden acceder a sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-117">The goal of a conditional access policy is to enable you to fine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="f3fc6-118">**Usuarios y grupos**</span><span class="sxs-lookup"><span data-stu-id="f3fc6-118">**Users and groups**</span></span> | <span data-ttu-id="f3fc6-119">Tiene que seleccionar al menos un usuario o grupo que esté autorizado para acceder a las aplicaciones en la nube que haya seleccionado.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-119">You need to select at least one user or group that is authorized to access the cloud apps you have selected.</span></span> | <span data-ttu-id="f3fc6-120">Una directiva de acceso condicional que no tiene usuarios ni grupos asignados nunca se desencadena.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="f3fc6-121">**Controles de acceso**</span><span class="sxs-lookup"><span data-stu-id="f3fc6-121">**Access controls**</span></span> | <span data-ttu-id="f3fc6-122">Tiene que seleccionar al menos un control de acceso.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-122">You need to select at least one access control.</span></span> | <span data-ttu-id="f3fc6-123">El procesador de directivas tiene que saber qué hacer si se satisfacen las condiciones.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-123">Your policy processor needs to know what to do if your conditions are satisfied.</span></span>|


<span data-ttu-id="f3fc6-124">Además de estos requisitos básicos, en muchos casos, también debe configurar una condición.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-124">In addition to these basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="f3fc6-125">Cuando una directiva también funcione sin una condición configurada, las condiciones son el factor de conducción para el acceso de mejor ajuste a sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-125">While a policy would also work without a configured condition, conditions are the driving factor for fine-tuning access to your apps.</span></span>


![Aplicaciones en la nube](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="f3fc6-127">¿Cómo se evalúan las asignaciones?</span><span class="sxs-lookup"><span data-stu-id="f3fc6-127">How are assignments evaluated?</span></span>

<span data-ttu-id="f3fc6-128">A todas las asignaciones se les asigna **la operación lógica AND**.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="f3fc6-129">Si tiene más de una asignación configurada, se deben satisfacer todas las asignaciones para desencadenar una directiva.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-129">If you have more than one assignment configured, to trigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="f3fc6-130">Si debe configurar una condición de ubicación que se aplica a todas las conexiones realizadas desde fuera de la red de la organización, puede:</span><span class="sxs-lookup"><span data-stu-id="f3fc6-130">If you need to configure a location condition that applies to all connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="f3fc6-131">Incluir **todas las ubicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-131">Including **All locations**</span></span>
- <span data-ttu-id="f3fc6-132">Excluir **todas las direcciones IP de confianza**.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="f3fc6-133">¿Qué ocurre si tiene directivas configuradas en el Portal de Azure clásico y en Azure Portal?</span><span class="sxs-lookup"><span data-stu-id="f3fc6-133">What happens if you have policies in the Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="f3fc6-134">Las dos directivas se aplican mediante Azure Active Directory y el usuario obtiene acceso únicamente cuando se cumplen todos los requisitos.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-134">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a><span data-ttu-id="f3fc6-135">¿Qué sucede si tiene directivas en el portal de Intune Silverlight y en Azure Portal?</span><span class="sxs-lookup"><span data-stu-id="f3fc6-135">What happens if you have policies in the Intune Silverlight portal and the Azure Portal?</span></span>
<span data-ttu-id="f3fc6-136">Las dos directivas se aplican mediante Azure Active Directory y el usuario obtiene acceso únicamente cuando se cumplen todos los requisitos.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-136">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a><span data-ttu-id="f3fc6-137">¿Qué ocurre si tiene varias directivas configuradas para el mismo usuario?</span><span class="sxs-lookup"><span data-stu-id="f3fc6-137">What happens if I have multiple policies for the same user configured?</span></span>  
<span data-ttu-id="f3fc6-138">En cada inicio de sesión, Azure Active Directory evalúa todas las directivas y garantiza que se cumplan todos los requisitos antes de conceder acceso al usuario.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="f3fc6-139">¿Funciona el acceso condicional con Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="f3fc6-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="f3fc6-140">Sí, se puede usar Exchange ActiveSync en una directiva de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="f3fc6-141">¿Qué no debería hacer?</span><span class="sxs-lookup"><span data-stu-id="f3fc6-141">What you should avoid doing</span></span>

<span data-ttu-id="f3fc6-142">El marco de trabajo de acceso condicional le proporciona una flexibilidad de configuración excelente.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-142">The conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="f3fc6-143">Sin embargo, una gran flexibilidad también implica revisar cuidadosamente cada directiva de configuración antes de liberarla para evitar resultados no deseados.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-143">However, great flexibility  also means that you should carefully review each configuration policy prior to releasing it to avoid undesirable results.</span></span> <span data-ttu-id="f3fc6-144">En este contexto, debe prestar especial atención a las asignaciones que afectan a conjuntos completos, como **todos los usuarios / grupos / aplicaciones en la nube**.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-144">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="f3fc6-145">En su entorno, debería evitar las siguientes configuraciones:</span><span class="sxs-lookup"><span data-stu-id="f3fc6-145">In your environment, you should avoid the following configurations:</span></span>


<span data-ttu-id="f3fc6-146">**Para todos los usuarios, todas las aplicaciones en la nube:**</span><span class="sxs-lookup"><span data-stu-id="f3fc6-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="f3fc6-147">**Bloquear acceso**: esta configuración bloquea toda la organización, lo cual no es en absoluto una buena idea.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="f3fc6-148">**Requerir dispositivo compatible**: para usuarios que aún no han inscrito sus dispositivos, esta directiva bloquea todo el acceso, incluido el acceso al portal Intune.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span></span> <span data-ttu-id="f3fc6-149">Si es un administrador y no tiene un dispositivo inscrito, esta directiva le impide volver a acceder Azure Portal para cambiar la directiva.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span></span>

- <span data-ttu-id="f3fc6-150">**Requerir unión a un dominio** : este acceso al bloqueo de directivas también ofrece la posibilidad de bloquear el acceso a todos los usuarios de su organización si aún no tiene un dispositivo unido al dominio.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-150">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="f3fc6-151">**Para todos los usuarios, todas las aplicaciones en la nube, todas las plataformas de dispositivos:**</span><span class="sxs-lookup"><span data-stu-id="f3fc6-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="f3fc6-152">**Bloquear acceso**: esta configuración bloquea toda la organización, lo cual no es en absoluto una buena idea.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="f3fc6-153">Escenarios comunes</span><span class="sxs-lookup"><span data-stu-id="f3fc6-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="f3fc6-154">Exigir autenticación multifactor para las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f3fc6-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="f3fc6-155">Muchos entornos tienen aplicaciones que requieren un mayor nivel de protección que otras.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-155">Many environments have apps requiring a higher level of protection than the others.</span></span>
<span data-ttu-id="f3fc6-156">Este es, por ejemplo, el caso de aplicaciones que tienen acceso a datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-156">This is, for example, the case for apps that have access to sensitive data.</span></span>
<span data-ttu-id="f3fc6-157">Si quiere agregar otra capa de protección a estas aplicaciones, puede configurar una directiva de acceso condicional que exija autenticación multifactor cuando los usuarios accedan a estas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-157">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="f3fc6-158">Exigir autenticación multifactor para el acceso desde redes que no son de confianza</span><span class="sxs-lookup"><span data-stu-id="f3fc6-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="f3fc6-159">Este escenario es similar al escenario anterior porque agrega un requisito para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-159">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="f3fc6-160">Sin embargo, la diferencia principal es la condición de este requisito.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-160">However, the main difference is the condition for this requirement.</span></span>  
<span data-ttu-id="f3fc6-161">Mientras que el escenario anterior se centra en aplicaciones con acceso a datos confidenciales, este escenario se centra en ubicaciones de confianza.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-161">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="f3fc6-162">En otras palabras, podría tener un requisito de autenticación multifactor si un usuario accede a una aplicación desde una red que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="f3fc6-163">Solo los dispositivos de confianza pueden acceder a servicios de Office 365</span><span class="sxs-lookup"><span data-stu-id="f3fc6-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="f3fc6-164">Si usa Intune en su entorno, puede comenzar a usar inmediatamente la directiva de acceso condicional en la consola de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-164">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span></span>

<span data-ttu-id="f3fc6-165">Muchos clientes de Intune usan el acceso condicional para asegurarse de que solo los dispositivos de confianza puedan acceder a servicios de Office 365.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-165">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="f3fc6-166">Esto significa que los dispositivos móviles se inscriben con Intune y satisfacen los requisitos de la directiva de cumplimiento y que los equipos con Windows están unidos a un dominio local.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span></span> <span data-ttu-id="f3fc6-167">Una importante mejora es que no es necesario establecer la misma directiva para cada uno de los servicios de Office 365.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-167">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span></span>  <span data-ttu-id="f3fc6-168">Cuando cree una nueva directiva, configure las aplicaciones de nube para que incluyan cada una de las aplicaciones de Office 365 que quiere proteger con acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="f3fc6-168">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3fc6-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3fc6-169">Next steps</span></span>

<span data-ttu-id="f3fc6-170">Si quiere saber cómo configurar una directiva de acceso condicional, consulte [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md) (Introducción al acceso condicional en Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f3fc6-170">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
