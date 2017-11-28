---
title: experiencias de aaaSign con Azure AD Identity Protection | Documentos de Microsoft
description: "Proporciona una visión general de la experiencia del usuario de hello cuando tiene mitiga o corregido un usuario o cuando se requiere la autenticación multifactor por una directiva de protección de identidad."
services: active-directory
keywords: "azure active directory identity protection, detección de aplicaciones en la nube, administración de aplicaciones, seguridad, riesgo, nivel de riesgo, punto vulnerable, directiva de seguridad"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="dede7-104">Experiencias de inicio de sesión con Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="dede7-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="dede7-105">Con Azure Active Directory Identity Protection, puede:</span><span class="sxs-lookup"><span data-stu-id="dede7-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="dede7-106">requerir a los usuarios tooregister para la autenticación multifactor</span><span class="sxs-lookup"><span data-stu-id="dede7-106">require users tooregister for multi-factor authentication</span></span>
* <span data-ttu-id="dede7-107">controlar inicios de sesión conflictivos y usuarios en peligro.</span><span class="sxs-lookup"><span data-stu-id="dede7-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="dede7-108">respuesta de Hola de problemas de toothese de sistema de Hola tiene un impacto en la experiencia de inicio de sesión del usuario porque solo directamente firma-en proporcionando un nombre de usuario y una contraseña no será posible ya.</span><span class="sxs-lookup"><span data-stu-id="dede7-108">hello response of hello system toothese issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="dede7-109">Pasos adicionales son tooget requiere que un usuario nuevo sin ningún riesgo en business.</span><span class="sxs-lookup"><span data-stu-id="dede7-109">Additional steps are required tooget a user safely back into business.</span></span>

<span data-ttu-id="dede7-110">En este tema se ofrece información general sobre la experiencia de inicio de sesión de usuario para todos los casos posibles.</span><span class="sxs-lookup"><span data-stu-id="dede7-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="dede7-111">**Multi-Factor Authentication**</span><span class="sxs-lookup"><span data-stu-id="dede7-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="dede7-112">Registro de la autenticación multifactor</span><span class="sxs-lookup"><span data-stu-id="dede7-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="dede7-113">**Inicio de sesión en peligro**</span><span class="sxs-lookup"><span data-stu-id="dede7-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="dede7-114">Recuperación de inicios de sesión peligrosos</span><span class="sxs-lookup"><span data-stu-id="dede7-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="dede7-115">Inicios de sesión peligrosos bloqueados</span><span class="sxs-lookup"><span data-stu-id="dede7-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="dede7-116">Registro de la autenticación multifactor durante un inicio de sesión peligroso</span><span class="sxs-lookup"><span data-stu-id="dede7-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="dede7-117">**Usuario en peligro**</span><span class="sxs-lookup"><span data-stu-id="dede7-117">**User at risk**</span></span>

* <span data-ttu-id="dede7-118">Recuperación de cuentas en peligro</span><span class="sxs-lookup"><span data-stu-id="dede7-118">Compromised account recovery</span></span>
* <span data-ttu-id="dede7-119">Cuenta en peligro bloqueada</span><span class="sxs-lookup"><span data-stu-id="dede7-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="dede7-120">Registro de la autenticación multifactor</span><span class="sxs-lookup"><span data-stu-id="dede7-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="dede7-121">Hola mejor experiencia de usuario para ambos, Hola flujo de recuperación de cuenta en peligro y Hola a riesgo flujo de inicio de sesión, es cuando el usuario Hola automática puede recuperar.</span><span class="sxs-lookup"><span data-stu-id="dede7-121">hello best user experience for both, hello compromised account recovery flow and hello risky sign-in flow, is when hello user can self-recover.</span></span> <span data-ttu-id="dede7-122">Si los usuarios se registren para la autenticación multifactor, ya tiene un número de teléfono asociado con su cuenta que puede ser utilizados toopass desafíos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="dede7-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used toopass security challenges.</span></span> <span data-ttu-id="dede7-123">Ninguna participación del departamento de soporte o el Administrador de ayuda es necesario toorecover contra los riesgos de cuenta.</span><span class="sxs-lookup"><span data-stu-id="dede7-123">No help desk or administrator involvement is needed toorecover from account compromise.</span></span> <span data-ttu-id="dede7-124">Por lo tanto, recomienda en absoluto tooget los usuarios registrados para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="dede7-124">Thus, it’s highly recommended tooget your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="dede7-125">Los administradores pueden:</span><span class="sxs-lookup"><span data-stu-id="dede7-125">Administrators can:</span></span>

* <span data-ttu-id="dede7-126">establecer una directiva que requiere tooset a los usuarios configurar sus cuentas para la comprobación de seguridad adicional.</span><span class="sxs-lookup"><span data-stu-id="dede7-126">set a policy that requires users tooset up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="dede7-127">dejar de omitir el registro de la autenticación multifactor para los días de too30, en caso de desean que los usuarios de toogive un período de gracia antes de registrar.</span><span class="sxs-lookup"><span data-stu-id="dede7-127">allow skipping multi-factor authentication registration for up too30 days, in case they want toogive users a grace period before registering.</span></span>

<span data-ttu-id="dede7-128">**registro de la autenticación multifactor de Hello consta de tres pasos:**</span><span class="sxs-lookup"><span data-stu-id="dede7-128">**hello multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="dede7-129">En el primer paso de hello, usuario de hello recibe una notificación acerca de la cuenta de hello requisito tooset Hola hacia arriba para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="dede7-129">In hello first step, hello user gets a notification about hello requirement tooset hello account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="dede7-130">![Corrección](./media/active-directory-identityprotection-flows/140.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="dede7-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="dede7-131">tooset la autenticación multifactor seguridad, necesita toolet Hola sistema sepa cómo desea toobe conectado.</span><span class="sxs-lookup"><span data-stu-id="dede7-131">tooset multi-factor authentication up, you need toolet hello system know how you want toobe contacted.</span></span>
   
    <span data-ttu-id="dede7-132">![Corrección](./media/active-directory-identityprotection-flows/141.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="dede7-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="dede7-133">sistema de Hello envía un desafío tooyou y deberá toorespond.</span><span class="sxs-lookup"><span data-stu-id="dede7-133">hello system submits a challenge tooyou and you need toorespond.</span></span>
   
    <span data-ttu-id="dede7-134">![Corrección](./media/active-directory-identityprotection-flows/142.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="dede7-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="dede7-135">Recuperación de inicios de sesión peligrosos</span><span class="sxs-lookup"><span data-stu-id="dede7-135">Risky sign-in recovery</span></span>
<span data-ttu-id="dede7-136">Cuando un administrador ha configurado una directiva para los riesgos de inicio de sesión, se notificación a los usuarios de hello afectado cuando lo intentan toosign en.</span><span class="sxs-lookup"><span data-stu-id="dede7-136">When an administrator has configured a policy for sign-in risks, hello affected users are notified when they try toosign-in.</span></span> 

<span data-ttu-id="dede7-137">**el flujo de inicio de sesión riesgo de Hello consta de dos pasos:**</span><span class="sxs-lookup"><span data-stu-id="dede7-137">**hello risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="dede7-138">usuario de Hola se informa de que se ha detectado la algo inusual sobre su inicio de sesión, como inicio de sesión desde una nueva ubicación, dispositivo o aplicación.</span><span class="sxs-lookup"><span data-stu-id="dede7-138">hello user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="dede7-139">![Corrección](./media/active-directory-identityprotection-flows/120.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="dede7-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="dede7-140">usuario de Hello es necesario tooprove su identidad para resolver un desafío de seguridad.</span><span class="sxs-lookup"><span data-stu-id="dede7-140">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="dede7-141">Si el usuario Hola está registrado para la autenticación multifactor necesitan tooround-un número de teléfono de tootheir de código de seguridad de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="dede7-141">If hello user is registered for multi-factor authentication they need tooround-trip a security code tootheir phone number.</span></span> <span data-ttu-id="dede7-142">Puesto que se trata de un solo un inicio de sesión arriesgado y no una cuenta en peligro, usuario de hello no tiene contraseña de hello toochange en este flujo.</span><span class="sxs-lookup"><span data-stu-id="dede7-142">Since this is a just a risky sign in and not a compromised account, hello user won’t have toochange hello password in this flow.</span></span> 
   
    <span data-ttu-id="dede7-143">![Corrección](./media/active-directory-identityprotection-flows/121.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="dede7-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="dede7-144">Inicios de sesión peligrosos bloqueados</span><span class="sxs-lookup"><span data-stu-id="dede7-144">Risky sign-in blocked</span></span>
<span data-ttu-id="dede7-145">Los administradores también pueden elegir tooset a los usuarios tooblock de directiva de riesgo de inicio de sesión tras el inicio de sesión en función de nivel de riesgo de Hola.</span><span class="sxs-lookup"><span data-stu-id="dede7-145">Administrators can also choose tooset a Sign-In Risk policy tooblock users upon sign-in depending on hello risk level.</span></span> <span data-ttu-id="dede7-146">tooget desbloqueado, los usuarios finales deben ponerse en contacto con un administrador o el departamento de soporte técnico, o puede intentar iniciar sesión desde una ubicación conocida o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dede7-146">tooget unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="dede7-147">La recuperación automática al resolver la autenticación multifactor no es una opción en este caso.</span><span class="sxs-lookup"><span data-stu-id="dede7-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="dede7-148">![Corrección](./media/active-directory-identityprotection-flows/200.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="dede7-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="dede7-149">Recuperación de cuentas en peligro</span><span class="sxs-lookup"><span data-stu-id="dede7-149">Compromised account recovery</span></span>
<span data-ttu-id="dede7-150">Cuando se ha configurado una directiva de seguridad de riesgo de usuario, los usuarios que cumplen usuario Hola el riesgo de nivel especificado en la directiva de hello (y, por tanto, se da por supuesto en peligro) debe pasar por el flujo de recuperación de compromiso de hello usuario antes de que puede iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="dede7-150">When a user risk security policy has been configured, users who meet hello user risk level specified in hello policy (and are therefore assumed compromised) must go through hello user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="dede7-151">**flujo de recuperación de compromiso de Hello usuario consta de tres pasos:**</span><span class="sxs-lookup"><span data-stu-id="dede7-151">**hello user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="dede7-152">se informa al usuario de Hola que su seguridad de la cuenta está en peligro debido a actividad sospechosa o filtren las credenciales.</span><span class="sxs-lookup"><span data-stu-id="dede7-152">hello user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="dede7-153">![Corrección](./media/active-directory-identityprotection-flows/101.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="dede7-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="dede7-154">usuario de Hello es necesario tooprove su identidad para resolver un desafío de seguridad.</span><span class="sxs-lookup"><span data-stu-id="dede7-154">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="dede7-155">Si el usuario Hola está registrado para la autenticación multifactor puede recuperar automáticamente se vean comprometidos.</span><span class="sxs-lookup"><span data-stu-id="dede7-155">If hello user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="dede7-156">Necesitará tooround-un número de teléfono de tootheir de código de seguridad de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="dede7-156">They will need tooround-trip a security code tootheir phone number.</span></span> 
   
   <span data-ttu-id="dede7-157">![Corrección](./media/active-directory-identityprotection-flows/110.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="dede7-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="dede7-158">Por último, Hola usuario es toochange forzada en su contraseña, ya que otra persona que haya tenido acceso tootheir cuenta.</span><span class="sxs-lookup"><span data-stu-id="dede7-158">Finally, hello user is forced toochange their password since someone else may have had access tootheir account.</span></span> 
   <span data-ttu-id="dede7-159">A continuación se muestran capturas de pantalla de esta experiencia.</span><span class="sxs-lookup"><span data-stu-id="dede7-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="dede7-160">![Corrección](./media/active-directory-identityprotection-flows/111.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="dede7-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="dede7-161">Cuenta en peligro bloqueada</span><span class="sxs-lookup"><span data-stu-id="dede7-161">Compromised account blocked</span></span>
<span data-ttu-id="dede7-162">tooget un usuario que se ha bloqueado por una directiva de seguridad de usuario riesgo desbloqueada, usuario Hola debe ponerse en contacto con un administrador o servicio de asistencia.</span><span class="sxs-lookup"><span data-stu-id="dede7-162">tooget a user that was blocked by a user risk security policy unblocked, hello user must contact an administrator or help desk.</span></span> <span data-ttu-id="dede7-163">La recuperación automática al resolver la autenticación multifactor no es una opción en este caso.</span><span class="sxs-lookup"><span data-stu-id="dede7-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="dede7-164">![Corrección](./media/active-directory-identityprotection-flows/104.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="dede7-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="dede7-165">Restablecer contraseña</span><span class="sxs-lookup"><span data-stu-id="dede7-165">Reset password</span></span>
<span data-ttu-id="dede7-166">Si se bloquea el inicio de sesión de los usuarios en peligro, un administrador puede generar una contraseña temporal para ellos,</span><span class="sxs-lookup"><span data-stu-id="dede7-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="dede7-167">los usuarios de Hello tendrán toochange su contraseña durante un inicio de sesión siguiente.</span><span class="sxs-lookup"><span data-stu-id="dede7-167">hello users will have toochange their password during a next sign-in.</span></span>

<span data-ttu-id="dede7-168">![Corrección](./media/active-directory-identityprotection-flows/160.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="dede7-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="dede7-169">Consulte también</span><span class="sxs-lookup"><span data-stu-id="dede7-169">See also</span></span>
* [<span data-ttu-id="dede7-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="dede7-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

