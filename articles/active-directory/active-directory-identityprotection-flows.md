---
title: "Experiencias de inicio de sesión con Azure AD Identity Protection | Microsoft Docs"
description: "Proporciona información general sobre la experiencia de usuario cuando Identity Protection ha mitigado o corregido los problemas relacionados con un usuario, o cuando una directiva exige la autenticación multifactor."
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
ms.openlocfilehash: e45936280b51fb2e54012a688fceddcc8dabe984
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="f62a5-104">Experiencias de inicio de sesión con Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f62a5-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="f62a5-105">Con Azure Active Directory Identity Protection, puede:</span><span class="sxs-lookup"><span data-stu-id="f62a5-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="f62a5-106">exigir a los usuarios que se registren en la autenticación multifactor y</span><span class="sxs-lookup"><span data-stu-id="f62a5-106">require users to register for multi-factor authentication</span></span>
* <span data-ttu-id="f62a5-107">controlar inicios de sesión conflictivos y usuarios en peligro.</span><span class="sxs-lookup"><span data-stu-id="f62a5-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="f62a5-108">La respuesta del sistema a estos problemas tiene un impacto en la experiencia de inicio de sesión del usuario, puesto que ya no se podrá iniciar sesión directamente introduciendo un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="f62a5-108">The response of the system to these issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="f62a5-109">Se requieren pasos adicionales para que los usuarios vuelvan a sus actividades con seguridad.</span><span class="sxs-lookup"><span data-stu-id="f62a5-109">Additional steps are required to get a user safely back into business.</span></span>

<span data-ttu-id="f62a5-110">En este tema se ofrece información general sobre la experiencia de inicio de sesión de usuario para todos los casos posibles.</span><span class="sxs-lookup"><span data-stu-id="f62a5-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="f62a5-111">**Multi-Factor Authentication**</span><span class="sxs-lookup"><span data-stu-id="f62a5-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="f62a5-112">Registro de la autenticación multifactor</span><span class="sxs-lookup"><span data-stu-id="f62a5-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="f62a5-113">**Inicio de sesión en peligro**</span><span class="sxs-lookup"><span data-stu-id="f62a5-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="f62a5-114">Recuperación de inicios de sesión peligrosos</span><span class="sxs-lookup"><span data-stu-id="f62a5-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="f62a5-115">Inicios de sesión peligrosos bloqueados</span><span class="sxs-lookup"><span data-stu-id="f62a5-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="f62a5-116">Registro de la autenticación multifactor durante un inicio de sesión peligroso</span><span class="sxs-lookup"><span data-stu-id="f62a5-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="f62a5-117">**Usuario en peligro**</span><span class="sxs-lookup"><span data-stu-id="f62a5-117">**User at risk**</span></span>

* <span data-ttu-id="f62a5-118">Recuperación de cuentas en peligro</span><span class="sxs-lookup"><span data-stu-id="f62a5-118">Compromised account recovery</span></span>
* <span data-ttu-id="f62a5-119">Cuenta en peligro bloqueada</span><span class="sxs-lookup"><span data-stu-id="f62a5-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="f62a5-120">Registro de la autenticación multifactor</span><span class="sxs-lookup"><span data-stu-id="f62a5-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="f62a5-121">La mejor experiencia de usuario en ambos casos: el flujo de recuperación de la cuenta en peligro y el flujo de inicio de sesión peligroso, es cuando el usuario puede realizar su recuperación.</span><span class="sxs-lookup"><span data-stu-id="f62a5-121">The best user experience for both, the compromised account recovery flow and the risky sign-in flow, is when the user can self-recover.</span></span> <span data-ttu-id="f62a5-122">Si los usuarios están registrados para la autenticación multifactor, ya tienen un número de teléfono asociado a sus cuentas que pueden usar para pasar comprobaciones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f62a5-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used to pass security challenges.</span></span> <span data-ttu-id="f62a5-123">No es necesaria ninguna participación del administrador o el departamento de soporte técnico para recuperar la cuenta puesta en peligro.</span><span class="sxs-lookup"><span data-stu-id="f62a5-123">No help desk or administrator involvement is needed to recover from account compromise.</span></span> <span data-ttu-id="f62a5-124">Por lo tanto, se recomienda encarecidamente a los usuarios que se registren en la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="f62a5-124">Thus, it’s highly recommended to get your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="f62a5-125">Los administradores pueden:</span><span class="sxs-lookup"><span data-stu-id="f62a5-125">Administrators can:</span></span>

* <span data-ttu-id="f62a5-126">Establecer una directiva que requiere que los usuarios configuren sus cuentas para una verificación de seguridad adicional.</span><span class="sxs-lookup"><span data-stu-id="f62a5-126">set a policy that requires users to set up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="f62a5-127">Permitir que se omita el registro de la autenticación multifactor durante 30 días, en caso de que deseen dar a los usuarios un período de gracia antes de registrarse.</span><span class="sxs-lookup"><span data-stu-id="f62a5-127">allow skipping multi-factor authentication registration for up to 30 days, in case they want to give users a grace period before registering.</span></span>

<span data-ttu-id="f62a5-128">**El registro de la autenticación multifactor consta de tres pasos:**</span><span class="sxs-lookup"><span data-stu-id="f62a5-128">**The multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="f62a5-129">En el primer paso, el usuario recibe una notificación sobre la necesidad de configurar la cuenta para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="f62a5-129">In the first step, the user gets a notification about the requirement to set the account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="f62a5-130">![Corrección](./media/active-directory-identityprotection-flows/140.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="f62a5-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="f62a5-131">Para configurar la autenticación multifactor, debe indicar al sistema cómo desea que se pongan en contacto con usted.</span><span class="sxs-lookup"><span data-stu-id="f62a5-131">To set multi-factor authentication up, you need to let the system know how you want to be contacted.</span></span>
   
    <span data-ttu-id="f62a5-132">![Corrección](./media/active-directory-identityprotection-flows/141.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="f62a5-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="f62a5-133">El sistema envía una comprobación que debe responder.</span><span class="sxs-lookup"><span data-stu-id="f62a5-133">The system submits a challenge to you and you need to respond.</span></span>
   
    <span data-ttu-id="f62a5-134">![Corrección](./media/active-directory-identityprotection-flows/142.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="f62a5-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="f62a5-135">Recuperación de inicios de sesión peligrosos</span><span class="sxs-lookup"><span data-stu-id="f62a5-135">Risky sign-in recovery</span></span>
<span data-ttu-id="f62a5-136">Cuando un administrador ha configurado una directiva de riesgo de inicio de sesión, se notifica a los usuarios afectados cuando intentan iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="f62a5-136">When an administrator has configured a policy for sign-in risks, the affected users are notified when they try to sign-in.</span></span> 

<span data-ttu-id="f62a5-137">**El flujo de inicio de sesión peligroso consta de dos pasos:**</span><span class="sxs-lookup"><span data-stu-id="f62a5-137">**The risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="f62a5-138">Se informa al usuario de que se ha detectado algún aspecto inusual en su inicio de sesión, como que se haya realizado desde una nueva ubicación, dispositivo o aplicación.</span><span class="sxs-lookup"><span data-stu-id="f62a5-138">The user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="f62a5-139">![Corrección](./media/active-directory-identityprotection-flows/120.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="f62a5-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="f62a5-140">Para demostrar su identidad, el usuario debe resolver un desafío de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f62a5-140">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="f62a5-141">Si el usuario está registrado para la autenticación multifactor necesitan devolver un código de seguridad enviado a su número de teléfono.</span><span class="sxs-lookup"><span data-stu-id="f62a5-141">If the user is registered for multi-factor authentication they need to round-trip a security code to their phone number.</span></span> <span data-ttu-id="f62a5-142">Puesto que solo se trata de un inicio de sesión peligroso, y no de una cuenta en peligro, el usuario no tendrá que cambiar la contraseña en este flujo.</span><span class="sxs-lookup"><span data-stu-id="f62a5-142">Since this is a just a risky sign in and not a compromised account, the user won’t have to change the password in this flow.</span></span> 
   
    <span data-ttu-id="f62a5-143">![Corrección](./media/active-directory-identityprotection-flows/121.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="f62a5-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="f62a5-144">Inicios de sesión peligrosos bloqueados</span><span class="sxs-lookup"><span data-stu-id="f62a5-144">Risky sign-in blocked</span></span>
<span data-ttu-id="f62a5-145">Los administradores también pueden elegir establecer una directiva de seguridad de riesgo de inicio de sesión para bloquear a los usuarios al iniciar sesión en función del nivel de riesgo.</span><span class="sxs-lookup"><span data-stu-id="f62a5-145">Administrators can also choose to set a Sign-In Risk policy to block users upon sign-in depending on the risk level.</span></span> <span data-ttu-id="f62a5-146">Para ser desbloqueados, los usuarios finales deben ponerse en contacto con un administrador o el departamento de soporte técnico, o bien pueden intentar iniciar sesión desde una ubicación o dispositivo conocidos.</span><span class="sxs-lookup"><span data-stu-id="f62a5-146">To get unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="f62a5-147">La recuperación automática al resolver la autenticación multifactor no es una opción en este caso.</span><span class="sxs-lookup"><span data-stu-id="f62a5-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="f62a5-148">![Corrección](./media/active-directory-identityprotection-flows/200.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="f62a5-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="f62a5-149">Recuperación de cuentas en peligro</span><span class="sxs-lookup"><span data-stu-id="f62a5-149">Compromised account recovery</span></span>
<span data-ttu-id="f62a5-150">Cuando se ha configurado una directiva de seguridad de riesgo del usuario, los usuarios que cumplen el nivel especificado en dicha directiva (y, por tanto, se supone que está en peligro) deben pasar por el flujo de recuperación del peligro antes de poder iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="f62a5-150">When a user risk security policy has been configured, users who meet the user risk level specified in the policy (and are therefore assumed compromised) must go through the user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="f62a5-151">**El flujo de recuperación de usuarios puestos en peligro consta de tres pasos:**</span><span class="sxs-lookup"><span data-stu-id="f62a5-151">**The user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="f62a5-152">Se informa al usuario que la seguridad de su cuenta está en peligro debido a actividad sospechosa o credenciales con fugas.</span><span class="sxs-lookup"><span data-stu-id="f62a5-152">The user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="f62a5-153">![Corrección](./media/active-directory-identityprotection-flows/101.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="f62a5-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="f62a5-154">Para demostrar su identidad, el usuario debe resolver un desafío de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f62a5-154">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="f62a5-155">Si el usuario está registrado para la autenticación multifactor, puede recuperarse automáticamente cuando está en peligro.</span><span class="sxs-lookup"><span data-stu-id="f62a5-155">If the user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="f62a5-156">Necesitará devolver un código de seguridad enviado a su número de teléfono.</span><span class="sxs-lookup"><span data-stu-id="f62a5-156">They will need to round-trip a security code to their phone number.</span></span> 
   
   <span data-ttu-id="f62a5-157">![Corrección](./media/active-directory-identityprotection-flows/110.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="f62a5-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="f62a5-158">Por último, el usuario debe cambiar su contraseña, ya que es posible que otra persona haya tenido acceso a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="f62a5-158">Finally, the user is forced to change their password since someone else may have had access to their account.</span></span> 
   <span data-ttu-id="f62a5-159">A continuación se muestran capturas de pantalla de esta experiencia.</span><span class="sxs-lookup"><span data-stu-id="f62a5-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="f62a5-160">![Corrección](./media/active-directory-identityprotection-flows/111.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="f62a5-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="f62a5-161">Cuenta en peligro bloqueada</span><span class="sxs-lookup"><span data-stu-id="f62a5-161">Compromised account blocked</span></span>
<span data-ttu-id="f62a5-162">Para desbloquear un usuario bloqueado por una directiva de seguridad de riesgo del usuario, el usuario debe ponerse en contacto con un administrador o el departamento de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="f62a5-162">To get a user that was blocked by a user risk security policy unblocked, the user must contact an administrator or help desk.</span></span> <span data-ttu-id="f62a5-163">La recuperación automática al resolver la autenticación multifactor no es una opción en este caso.</span><span class="sxs-lookup"><span data-stu-id="f62a5-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="f62a5-164">![Corrección](./media/active-directory-identityprotection-flows/104.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="f62a5-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="f62a5-165">Restablecer contraseña</span><span class="sxs-lookup"><span data-stu-id="f62a5-165">Reset password</span></span>
<span data-ttu-id="f62a5-166">Si se bloquea el inicio de sesión de los usuarios en peligro, un administrador puede generar una contraseña temporal para ellos,</span><span class="sxs-lookup"><span data-stu-id="f62a5-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="f62a5-167">quienes tendrán que cambiar las contraseñas en el siguiente inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f62a5-167">The users will have to change their password during a next sign-in.</span></span>

<span data-ttu-id="f62a5-168">![Corrección](./media/active-directory-identityprotection-flows/160.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="f62a5-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="f62a5-169">Consulte también</span><span class="sxs-lookup"><span data-stu-id="f62a5-169">See also</span></span>
* [<span data-ttu-id="f62a5-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f62a5-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

