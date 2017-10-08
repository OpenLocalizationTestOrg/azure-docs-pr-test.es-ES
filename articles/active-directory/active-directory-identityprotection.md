---
title: Active Directory Identity Protection aaaAzure | Documentos de Microsoft
description: "Obtenga información acerca de cómo Azure AD Identity Protection permite capacidad de hello toolimit de un tooexploit atacante una identidad en peligro o el dispositivo y toosecure una identidad o un dispositivo que era toobe sospechosa o conocido en peligro."
services: active-directory
keywords: "azure active directory identity protection, detección de aplicaciones en la nube, administración de aplicaciones, seguridad, riesgo, nivel de riesgo, punto vulnerable, directiva de seguridad"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="a4974-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a4974-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="a4974-105">Azure Active Directory Identity Protection es una característica de edición de hello Azure AD Premium P2 que le permite:</span><span class="sxs-lookup"><span data-stu-id="a4974-105">Azure Active Directory Identity Protection is a feature of hello Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="a4974-106">Detectar posibles vulnerabilidades que afectan a las identidades de la organización</span><span class="sxs-lookup"><span data-stu-id="a4974-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="a4974-107">Configurar respuestas automatizadas toodetected sospechosa acciones de identidades de la organización de tooyour relacionados</span><span class="sxs-lookup"><span data-stu-id="a4974-107">Configure automated responses toodetected suspicious actions that are related tooyour organization’s identities</span></span>  

- <span data-ttu-id="a4974-108">Investigar incidentes sospechosos y tome las medidas adecuadas tooresolve ellos</span><span class="sxs-lookup"><span data-stu-id="a4974-108">Investigate suspicious incidents and take appropriate action tooresolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="a4974-109">Introducción</span><span class="sxs-lookup"><span data-stu-id="a4974-109">Getting started</span></span>

<span data-ttu-id="a4974-110">Microsoft protege identidades basadas en la nube desde hace más de una década.</span><span class="sxs-lookup"><span data-stu-id="a4974-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="a4974-111">Con Azure Active Directory Identity Protection, en su entorno, puede usar Hola mismos sistemas de protección Microsoft utiliza identidades toosecure.</span><span class="sxs-lookup"><span data-stu-id="a4974-111">With Azure Active Directory Identity Protection, in your environment, you can use hello same protection systems Microsoft uses toosecure identities.</span></span>

<span data-ttu-id="a4974-112">mayoría de Hola de toman las infracciones de seguridad colocar cuando los atacantes tuvieran el entorno de acceso tooan por robo de identidad de un usuario.</span><span class="sxs-lookup"><span data-stu-id="a4974-112">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="a4974-113">En años de hello, los atacantes han convertido en cada vez más eficaces para aprovechar las infracciones de otros fabricantes y usen ataques de phishing sofisticadas.</span><span class="sxs-lookup"><span data-stu-id="a4974-113">Over hello years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="a4974-114">En cuanto un atacante obtiene acceso a las cuentas de usuario con pocos privilegios tooeven, es relativamente fácil para ellos toogain acceder a los recursos de empresa de tooimportant a través de un movimiento lateral.</span><span class="sxs-lookup"><span data-stu-id="a4974-114">As soon as an attacker gains access tooeven low privileged user accounts, it is relatively easy for them toogain access tooimportant company resources through lateral movement.</span></span>

<span data-ttu-id="a4974-115">Como consecuencia de esto, debe:</span><span class="sxs-lookup"><span data-stu-id="a4974-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="a4974-116">Proteger todas las identidades independientemente de su nivel de privilegios</span><span class="sxs-lookup"><span data-stu-id="a4974-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="a4974-117">Evitar de forma proactiva que se haga mal uso de las identidades que están en peligro.</span><span class="sxs-lookup"><span data-stu-id="a4974-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="a4974-118">Descubrir las identidades en peligro no es tarea fácil.</span><span class="sxs-lookup"><span data-stu-id="a4974-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="a4974-119">Azure Active Directory utiliza algoritmos de aprendizaje automático adaptable y las anomalías de toodetect heurística e incidentes sospechosos que indican potencialmente en riesgo identidades.</span><span class="sxs-lookup"><span data-stu-id="a4974-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="a4974-120">Con estos datos, Identity Protection genera informes y alertas que permiten tooevaluate Hola detectan problemas y toman mitigación adecuada o acciones correctoras.</span><span class="sxs-lookup"><span data-stu-id="a4974-120">Using this data, Identity Protection generates reports and alerts that enable you tooevaluate hello detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="a4974-121">Azure Active Directory Identity Protection es más que una herramienta de supervisión e informes.</span><span class="sxs-lookup"><span data-stu-id="a4974-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="a4974-122">tooprotect las identidades de su organización, puede configurar las directivas basadas en el riesgo que responden automáticamente toodetected problemas cuando se ha alcanzado un nivel de riesgo especificado.</span><span class="sxs-lookup"><span data-stu-id="a4974-122">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="a4974-123">Estas directivas además tooother condicional tener acceso a controles proporcionados por Azure Active Directory y EMS, puede bloquear de forma automática o iniciar acciones de corrección adaptable entre ellos los restablecimientos de contraseña y la aplicación de la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="a4974-123">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="a4974-124">Funcionalidades de Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a4974-124">Identity Protection capabilities</span></span>

<span data-ttu-id="a4974-125">**Detección de vulnerabilidades y cuentas peligrosas:**</span><span class="sxs-lookup"><span data-stu-id="a4974-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="a4974-126">Proporcionar recomendaciones personalizadas tooimprove condiciones globales de seguridad resaltando las vulnerabilidades</span><span class="sxs-lookup"><span data-stu-id="a4974-126">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="a4974-127">Cálculo de los niveles de riesgo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="a4974-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="a4974-128">Calcular los niveles de riesgo del usuario</span><span class="sxs-lookup"><span data-stu-id="a4974-128">Calculating user risk levels</span></span>


<span data-ttu-id="a4974-129">**Investigación de los eventos de riesgo:**</span><span class="sxs-lookup"><span data-stu-id="a4974-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="a4974-130">Enviar notificaciones de los eventos de riesgo</span><span class="sxs-lookup"><span data-stu-id="a4974-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="a4974-131">Investigar los eventos de riesgo con información pertinente y contextual</span><span class="sxs-lookup"><span data-stu-id="a4974-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="a4974-132">Proporcionar flujos de trabajo básicos de las investigaciones de tootrack</span><span class="sxs-lookup"><span data-stu-id="a4974-132">Providing basic workflows tootrack investigations</span></span>
* <span data-ttu-id="a4974-133">Proporciona un acceso sencillo tooremediation acciones como el restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="a4974-133">Providing easy access tooremediation actions such as password reset</span></span>

<span data-ttu-id="a4974-134">**Directivas de acceso condicional basadas en riesgos:**</span><span class="sxs-lookup"><span data-stu-id="a4974-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="a4974-135">Directiva toomitigate arriesgados inicios de sesión bloqueando inicios de sesión o solicitando retos de la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="a4974-135">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="a4974-136">Directiva tooblock o cuentas de usuario de riesgo segura</span><span class="sxs-lookup"><span data-stu-id="a4974-136">Policy tooblock or secure risky user accounts</span></span>
* <span data-ttu-id="a4974-137">Directiva toorequire usuarios tooregister para la autenticación multifactor</span><span class="sxs-lookup"><span data-stu-id="a4974-137">Policy toorequire users tooregister for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="a4974-138">Roles de Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a4974-138">Identity Protection roles</span></span>

<span data-ttu-id="a4974-139">actividades de administración de tooload saldo Hola alrededor de su implementación de protección de identidad, puede asignar varios roles.</span><span class="sxs-lookup"><span data-stu-id="a4974-139">tooload balance hello management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="a4974-140">Azure AD Identity Protection admite tres roles de directorio:</span><span class="sxs-lookup"><span data-stu-id="a4974-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="a4974-141">Rol</span><span class="sxs-lookup"><span data-stu-id="a4974-141">Role</span></span>                         | <span data-ttu-id="a4974-142">Puede hacer</span><span class="sxs-lookup"><span data-stu-id="a4974-142">Can do</span></span>                          | <span data-ttu-id="a4974-143">No puede hacer</span><span class="sxs-lookup"><span data-stu-id="a4974-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="a4974-144">Administrador global</span><span class="sxs-lookup"><span data-stu-id="a4974-144">Global administrator</span></span>         | <span data-ttu-id="a4974-145">Acceso completo tooIdentity protección, incorporar Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a4974-145">Full access tooIdentity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="a4974-146">Administrador de seguridad</span><span class="sxs-lookup"><span data-stu-id="a4974-146">Security administrator</span></span>       | <span data-ttu-id="a4974-147">TooIdentity protección de acceso completo</span><span class="sxs-lookup"><span data-stu-id="a4974-147">Full access tooIdentity Protection</span></span> | <span data-ttu-id="a4974-148">Incorporar Identity Protection, restablecer contraseñas para un usuario</span><span class="sxs-lookup"><span data-stu-id="a4974-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="a4974-149">Lector de seguridad</span><span class="sxs-lookup"><span data-stu-id="a4974-149">Security reader</span></span>              | <span data-ttu-id="a4974-150">Protección del acceso de solo tooIdentity</span><span class="sxs-lookup"><span data-stu-id="a4974-150">Ready-only access tooIdentity Protection</span></span> | <span data-ttu-id="a4974-151">Incorporar Identity Protection, remediar usuarios, configurar directivas, restablecer contraseñas</span><span class="sxs-lookup"><span data-stu-id="a4974-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="a4974-152">Para obtener más detalles, consulte [Asignación de roles de administrador en Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a4974-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="a4974-153">Detección</span><span class="sxs-lookup"><span data-stu-id="a4974-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="a4974-154">Puntos vulnerables</span><span class="sxs-lookup"><span data-stu-id="a4974-154">Vulnerabilities</span></span>

<span data-ttu-id="a4974-155">Azure Active Directory Identity Protection analiza la configuración y detecta las vulnerabilidades que pueden afectar a las identidades de usuario.</span><span class="sxs-lookup"><span data-stu-id="a4974-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="a4974-156">Para conocer más detalles, consulte [Vulnerabilidades detectadas por Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="a4974-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="a4974-157">Eventos de riesgo</span><span class="sxs-lookup"><span data-stu-id="a4974-157">Risk events</span></span>

<span data-ttu-id="a4974-158">Azure Active Directory utiliza algoritmos y heurística toodetect sospechosas acciones identidades del usuario tooyour relacionados de aprendizaje de automático adaptable.</span><span class="sxs-lookup"><span data-stu-id="a4974-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user's identities.</span></span> <span data-ttu-id="a4974-159">sistema de Hello crea un registro para cada acción sospechosa detectada.</span><span class="sxs-lookup"><span data-stu-id="a4974-159">hello system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="a4974-160">Estos registros se conocen también como eventos de riesgo.</span><span class="sxs-lookup"><span data-stu-id="a4974-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="a4974-161">Para más información, consulte [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md) (Eventos de riesgo de Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a4974-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="a4974-162">Investigación</span><span class="sxs-lookup"><span data-stu-id="a4974-162">Investigation</span></span>
<span data-ttu-id="a4974-163">Su viaje a través de la protección de identidad suele iniciarse con el panel de la protección de la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4974-163">Your journey through Identity Protection typically starts with hello Identity Protection dashboard.</span></span>

<span data-ttu-id="a4974-164">![Corrección](./media/active-directory-identityprotection/1000.png "Corrección")</span><span class="sxs-lookup"><span data-stu-id="a4974-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="a4974-165">panel de Hello le da acceso a:</span><span class="sxs-lookup"><span data-stu-id="a4974-165">hello dashboard gives you access to:</span></span>

* <span data-ttu-id="a4974-166">Informes como **Usuarios marcados en riesgo**, **Eventos de riesgo** y **Vulnerabilidades**.</span><span class="sxs-lookup"><span data-stu-id="a4974-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="a4974-167">Configuración como la configuración de Hola de su **las directivas de seguridad**, **notificaciones** y **el registro de la autenticación multifactor**</span><span class="sxs-lookup"><span data-stu-id="a4974-167">Settings such as hello configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="a4974-168">Normalmente es el punto de partida para la investigación, que es el proceso de Hola de revisión de las actividades de hello, los registros y otra información relevante relacionado tooa el riesgo de evento toodecide si son necesarios pasos de mitigación o corrección, y la identidad de hello era en peligro y entender cómo hello en peligro la identidad se usó.</span><span class="sxs-lookup"><span data-stu-id="a4974-168">It is typically your starting point for investigation, which is hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary,  and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

<span data-ttu-id="a4974-169">Se puede asociar su toohello de actividades de investigación [notificaciones](active-directory-identityprotection-notifications.md) protección de Azure Active Directory envía por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="a4974-169">You can tie your investigation activities toohello [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="a4974-170">Hello las secciones siguientes proporcionan más detalles y pasos de hello investigación tooan relacionados.</span><span class="sxs-lookup"><span data-stu-id="a4974-170">hello following sections provide you with more details and hello steps that are related tooan investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="a4974-171">Inicios de sesión no seguros</span><span class="sxs-lookup"><span data-stu-id="a4974-171">Risky sign-ins</span></span>

<span data-ttu-id="a4974-172">Azure Active Directory detecta [tipos de eventos de riesgo](active-directory-reporting-risk-events.md#risk-event-types) en tiempo real y sin conexión.</span><span class="sxs-lookup"><span data-stu-id="a4974-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="a4974-173">Cada evento de riesgo que se ha detectado para un inicio de sesión de un usuario contribuye tooa concepto lógico que se denomina sesión arriesgado.</span><span class="sxs-lookup"><span data-stu-id="a4974-173">Each risk event that has been detected for a sign-in of a user contributes tooa logical concept called risky sign-in.</span></span> <span data-ttu-id="a4974-174">Un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que no es posible que se han realizado por propietario legítimo de Hola de una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="a4974-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by hello legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="a4974-175">Nivel de riesgo del inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="a4974-175">Sign-in risk level</span></span>

<span data-ttu-id="a4974-176">Un nivel de riesgo de inicio de sesión es una indicación (alto, medio o bajo) de probabilidad de Hola que no ha realizado un intento de inicio de sesión propietario legítimo de Hola de una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="a4974-176">A sign-in risk level is an indication (High, Medium, or Low) of hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="a4974-177">Mitigación de eventos de riesgo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="a4974-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="a4974-178">Una mitigación es una capacidad de Hola de toolimit de acción de un atacante tooexploit una identidad en peligro o un dispositivo sin estado de restauración Hola identidad o dispositivo tooa seguro.</span><span class="sxs-lookup"><span data-stu-id="a4974-178">A mitigation is an action toolimit hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="a4974-179">Una mitigación no resuelve los eventos de inicio de sesión en riesgo anteriores asociados con la identidad de Hola o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a4974-179">A mitigation does not resolve previous sign-in risk events associated with hello identity or device.</span></span>

<span data-ttu-id="a4974-180">inicios de sesión de riesgo toomitigate automáticamente, puede configurar policicies de seguridad de inicio de sesión en riesgo.</span><span class="sxs-lookup"><span data-stu-id="a4974-180">toomitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="a4974-181">Mediante estas directivas, considere la posibilidad de nivel de riesgo de saludo del usuario de Hola u Hola inicio de sesión tooblock de riesgo de inicios de sesión o requerir Hola usuario tooperform la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="a4974-181">Using these policies, you consider hello risk level of hello user or hello sign-in tooblock risky sign-ins or require hello user tooperform multi-factor authentication.</span></span> <span data-ttu-id="a4974-182">Estas acciones pueden evitar que un atacante use un daño toocause de robo de identidad y pueden provocar alguna identidad de hello toosecure de tiempo.</span><span class="sxs-lookup"><span data-stu-id="a4974-182">These actions may prevent an attacker from exploiting a stolen identity toocause damage, and may give you some time toosecure hello identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="a4974-183">Directiva de seguridad de riesgo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="a4974-183">Sign-in risk security policy</span></span>
<span data-ttu-id="a4974-184">Una directiva de inicio de sesión riesgo es una directiva de acceso condicional que evalúa Hola riesgo tooa inicio de sesión en concreta y se aplica a las mitigaciones según las reglas y condiciones predefinidas.</span><span class="sxs-lookup"><span data-stu-id="a4974-184">A sign-in risk policy is a conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="a4974-185">![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1014.png "Directiva de riesgo de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="a4974-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="a4974-186">Azure AD Identity Protection ayuda a administrar mitigación Hola de riesgo de inicios de sesión por lo que le permite:</span><span class="sxs-lookup"><span data-stu-id="a4974-186">Azure AD Identity Protection helps you manage hello mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="a4974-187">Establecer Hola usuarios y grupos Hola la directiva se aplica a:</span><span class="sxs-lookup"><span data-stu-id="a4974-187">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="a4974-188">![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1015.png "Directiva de riesgo de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="a4974-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="a4974-189">Establezca Hola riesgo de inicio de sesión de nivel umbral (bajo, medio o alto) que desencadena la directiva de hello:</span><span class="sxs-lookup"><span data-stu-id="a4974-189">Set hello sign-in risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="a4974-190">![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1016.png "Directiva de riesgo de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="a4974-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="a4974-191">Conjunto Hola controles toobe aplicado cuando la directiva de hello desencadena:</span><span class="sxs-lookup"><span data-stu-id="a4974-191">Set hello controls toobe enforced when hello policy triggers:</span></span>  

    <span data-ttu-id="a4974-192">![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1017.png "Directiva de riesgo de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="a4974-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="a4974-193">Cambiar estado de saludo de la directiva:</span><span class="sxs-lookup"><span data-stu-id="a4974-193">Switch hello state of your policy:</span></span>

    <span data-ttu-id="a4974-194">![Registro MFA](./media/active-directory-identityprotection/403.png "Registro MFA")</span><span class="sxs-lookup"><span data-stu-id="a4974-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="a4974-195">Revisar y evaluar el impacto de Hola de un cambio antes de activarlo:</span><span class="sxs-lookup"><span data-stu-id="a4974-195">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="a4974-196">![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1018.png "Directiva de riesgo de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="a4974-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-tooknow"></a><span data-ttu-id="a4974-197">Lo que necesita tooknow</span><span class="sxs-lookup"><span data-stu-id="a4974-197">What you need tooknow</span></span>
<span data-ttu-id="a4974-198">Puede configurar una inicio de sesión riesgo seguridad Directiva toorequire la autenticación multifactor:</span><span class="sxs-lookup"><span data-stu-id="a4974-198">You can configure a sign-in risk security policy toorequire multi-factor authentication:</span></span>

<span data-ttu-id="a4974-199">![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1017.png "Directiva de riesgo de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="a4974-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="a4974-200">Sin embargo, por seguridad, esta configuración solo funciona para los usuarios que ya se hayan registrado para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="a4974-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="a4974-201">Si no se cumple Hola condición toorequire la autenticación multifactor para un usuario que no se ha registrado para la autenticación multifactor, usuario de hello está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="a4974-201">If hello condition toorequire multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, hello user is blocked.</span></span>

<span data-ttu-id="a4974-202">Como práctica recomendada, si desea que toorequire la autenticación multifactor para inicios de sesión riesgos, debe:</span><span class="sxs-lookup"><span data-stu-id="a4974-202">As a best practice, if you want toorequire multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="a4974-203">Habilitar hello [directiva de registro de la autenticación multifactor](#multi-factor-authentication-registration-policy) Hola afecta a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a4974-203">Enable hello [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for hello affected users.</span></span>
2. <span data-ttu-id="a4974-204">Requerir Hola afectados toologin de usuarios en una sesión no es arriesgado tooperform un registro MFA</span><span class="sxs-lookup"><span data-stu-id="a4974-204">Require hello affected users toologin in a non-risky session tooperform a MFA registration</span></span>

<span data-ttu-id="a4974-205">Tras completar estos pasos, se garantiza que la autenticación multifactor sea necesaria para un inicio de sesión de riesgo.</span><span class="sxs-lookup"><span data-stu-id="a4974-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="a4974-206">Prácticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="a4974-206">Best practices</span></span>
<span data-ttu-id="a4974-207">Elegir un **alta** umbral reduce el número de Hola de veces que una directiva se desencadena y minimiza Hola impacto toousers.</span><span class="sxs-lookup"><span data-stu-id="a4974-207">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>  

<span data-ttu-id="a4974-208">Sin embargo, excluye **bajo** y **medio** etiquetado como inicios de sesión para el riesgo de directiva de hello, que no se puede bloquear un atacante pueda aprovechar una identidad en peligro.</span><span class="sxs-lookup"><span data-stu-id="a4974-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from hello policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="a4974-209">Cuando la configuración de Hola directiva,</span><span class="sxs-lookup"><span data-stu-id="a4974-209">When setting hello policy,</span></span>

* <span data-ttu-id="a4974-210">Excluya a los usuarios que no tengan o no puedan tener la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="a4974-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="a4974-211">Exclusión de usuarios en configuraciones regionales donde no es práctico si quiere habilitar Directiva de hello (por ejemplo, no toohelpdesk de acceso)</span><span class="sxs-lookup"><span data-stu-id="a4974-211">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="a4974-212">Excluir los usuarios que son probable toogenerate una gran cantidad de falsos positivos (los desarrolladores, analistas de seguridad)</span><span class="sxs-lookup"><span data-stu-id="a4974-212">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="a4974-213">Utilice un umbral **Alto** durante la puesta en servicio inicial de la directiva, o bien si debe minimizar los desafíos que ven los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="a4974-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="a4974-214">Use un umbral **Bajo** si su organización requiere un mayor grado de seguridad.</span><span class="sxs-lookup"><span data-stu-id="a4974-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="a4974-215">Seleccionar un umbral **Bajo** presenta desafíos adicionales de inicio de sesión del usuario, pero aumenta la seguridad.</span><span class="sxs-lookup"><span data-stu-id="a4974-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="a4974-216">Hola, valor predeterminado recomendado para la mayoría de las organizaciones es tooconfigure una regla para un **medio** umbral toostrike un equilibrio entre la facilidad de uso y seguridad.</span><span class="sxs-lookup"><span data-stu-id="a4974-216">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="a4974-217">Directiva de inicio de sesión en riesgo de Hello es:</span><span class="sxs-lookup"><span data-stu-id="a4974-217">hello sign-in risk policy is:</span></span>

* <span data-ttu-id="a4974-218">El tráfico del explorador tooall aplicado y usan autenticación moderna de inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="a4974-218">Applied tooall browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="a4974-219">Tooapplications no aplicada mediante protocolos de seguridad anteriores al deshabilitar punto de conexión de WS-Trust de hello en IDP Hola federado, por ejemplo, AD FS.</span><span class="sxs-lookup"><span data-stu-id="a4974-219">Not applied tooapplications using older security protocols by disabling hello WS-Trust endpoint at hello federated IDP, such as ADFS.</span></span>

<span data-ttu-id="a4974-220">Hola **eventos de riesgo** página en la consola de protección de la identidad de hello enumera todos los eventos:</span><span class="sxs-lookup"><span data-stu-id="a4974-220">hello **Risk Events** page in hello Identity Protection console lists all events:</span></span>

* <span data-ttu-id="a4974-221">A los que se aplicó esta directiva.</span><span class="sxs-lookup"><span data-stu-id="a4974-221">This policy was applied to</span></span>
* <span data-ttu-id="a4974-222">Puede revisar la actividad hello y determinar si la acción de hello fue adecuado o no</span><span class="sxs-lookup"><span data-stu-id="a4974-222">You can review hello activity and determine whether hello action was appropriate or not</span></span>

<span data-ttu-id="a4974-223">Para obtener información general de hello relacionados con la experiencia del usuario, consulte:</span><span class="sxs-lookup"><span data-stu-id="a4974-223">For an overview of hello related user experience, see:</span></span>

* [<span data-ttu-id="a4974-224">Recuperación de inicios de sesión peligrosos</span><span class="sxs-lookup"><span data-stu-id="a4974-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="a4974-225">Inicios de sesión peligrosos bloqueados</span><span class="sxs-lookup"><span data-stu-id="a4974-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="a4974-226">Experiencias de inicio de sesión con Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a4974-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="a4974-227">**cuadro de diálogo de configuración relacionados de Hola de tooopen**:</span><span class="sxs-lookup"><span data-stu-id="a4974-227">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="a4974-228">En hello **Azure AD Identity Protection** hoja en hello **configurar** sección, haga clic en **inicio de sesión de la directiva de riesgo**.</span><span class="sxs-lookup"><span data-stu-id="a4974-228">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="a4974-229">![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1014.png "Directiva de riesgo de usuario")</span><span class="sxs-lookup"><span data-stu-id="a4974-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="a4974-230">Usuarios marcados con riesgo</span><span class="sxs-lookup"><span data-stu-id="a4974-230">Users flagged for risk</span></span>

<span data-ttu-id="a4974-231">Todos los activos [el riesgo de eventos](active-directory-identity-protection-risk-events.md) que se detectaron por Azure Active Directory para un usuario contribuyen tooa concepto lógico llamada riesgo de usuario.</span><span class="sxs-lookup"><span data-stu-id="a4974-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute tooa logical concept called user risk.</span></span> <span data-ttu-id="a4974-232">Un usuario marcado como en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro.</span><span class="sxs-lookup"><span data-stu-id="a4974-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Usuarios marcados con riesgo](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="a4974-234">Nivel de riesgo del usuario</span><span class="sxs-lookup"><span data-stu-id="a4974-234">User risk level</span></span>

<span data-ttu-id="a4974-235">Un nivel de riesgo de usuario es una indicación (alto, medio o bajo) de probabilidad de Hola que está en peligro la identidad del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4974-235">A user risk level is an indication (High, Medium, or Low) of hello likelihood that hello user’s identity has been compromised.</span></span> <span data-ttu-id="a4974-236">Se calcula basándose en eventos de riesgo de usuario de Hola que están asociados con una identidad de usuario.</span><span class="sxs-lookup"><span data-stu-id="a4974-236">It is calculated based on hello user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="a4974-237">Hello estado de un evento de riesgo sea **Active** o **cerrado**.</span><span class="sxs-lookup"><span data-stu-id="a4974-237">hello status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="a4974-238">Solo el riesgo de eventos que son **Active** contribuir toohello cálculo de nivel de riesgo de usuario.</span><span class="sxs-lookup"><span data-stu-id="a4974-238">Only risk events that are **Active** contribute toohello user risk level calculation.</span></span>

<span data-ttu-id="a4974-239">nivel de riesgo de usuario de Hola se calcula mediante Hola siguientes entradas:</span><span class="sxs-lookup"><span data-stu-id="a4974-239">hello user risk level is calculated using hello following inputs:</span></span>

* <span data-ttu-id="a4974-240">Eventos de los riesgos activos que afectan a los usuarios de Hola</span><span class="sxs-lookup"><span data-stu-id="a4974-240">Active risk events impacting hello user</span></span>
* <span data-ttu-id="a4974-241">Nivel de riesgo de estos eventos</span><span class="sxs-lookup"><span data-stu-id="a4974-241">Risk level of these events</span></span>
* <span data-ttu-id="a4974-242">Si se ha tomado alguna acción de corrección</span><span class="sxs-lookup"><span data-stu-id="a4974-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="a4974-243">![Riesgos de usuario](./media/active-directory-identityprotection/1031.png "Riesgos de usuario")</span><span class="sxs-lookup"><span data-stu-id="a4974-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="a4974-244">Puede usar Hola usuario riesgo niveles toocreate directivas de acceso condicional que bloquear arriesgado a los usuarios iniciar sesión en, u obligarlos toosecurely cambiar su contraseña.</span><span class="sxs-lookup"><span data-stu-id="a4974-244">You can use hello user risk levels toocreate conditional access policies that block risky users from signing in, or force them toosecurely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="a4974-245">Cierre manual de eventos de riesgo</span><span class="sxs-lookup"><span data-stu-id="a4974-245">Closing risk events manually</span></span>

<span data-ttu-id="a4974-246">En la mayoría de los casos, ejecutará las acciones de corrección, como eventos de cierre de riesgo de tooautomatically de restablecimiento de una contraseña segura.</span><span class="sxs-lookup"><span data-stu-id="a4974-246">In most cases, you will take remediation actions such as a secure password reset tooautomatically close risk events.</span></span> <span data-ttu-id="a4974-247">Sin embargo, esto no siempre es posible.</span><span class="sxs-lookup"><span data-stu-id="a4974-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="a4974-248">Esto sucede, por ejemplo, hello, cuando:</span><span class="sxs-lookup"><span data-stu-id="a4974-248">This is, for example, hello case, when:</span></span>

* <span data-ttu-id="a4974-249">Un usuario con eventos de riesgo en estado Activo se ha eliminado.</span><span class="sxs-lookup"><span data-stu-id="a4974-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="a4974-250">Una investigación revela que se ha realizar un evento de riesgo notificado por usuario legítimo Hola</span><span class="sxs-lookup"><span data-stu-id="a4974-250">An investigation reveals that a reported risk event has been perform by hello legitimate user</span></span>

<span data-ttu-id="a4974-251">Dado que los eventos de riesgo que son **Active** contribuir cálculo de riesgo de usuario toohello, es posible que tenga toomanually disminuir un nivel de riesgo al cerrar manualmente los eventos de riesgo.</span><span class="sxs-lookup"><span data-stu-id="a4974-251">Because risk events that are **Active** contribute toohello user risk calculation, you may have toomanually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="a4974-252">Durante el transcurso de Hola de investigación, puede elegir tootake cualquiera de estas acciones toochange Hola estado de un riesgo evento:</span><span class="sxs-lookup"><span data-stu-id="a4974-252">During hello course of investigation, you can choose tootake any of these actions toochange hello status of a risk event:</span></span>

<span data-ttu-id="a4974-253">![Acciones](./media/active-directory-identityprotection/34.png "Acciones")</span><span class="sxs-lookup"><span data-stu-id="a4974-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="a4974-254">**Resolver** : Si después de investigar un evento de riesgo, ha realizado una acción de corrección adecuado fuera de la protección de identidad y cree ese evento de riesgo Hola debe tenerse en cuenta cerrada, eventos de hello marca como resuelto.</span><span class="sxs-lookup"><span data-stu-id="a4974-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that hello risk event should be considered closed, mark hello event as Resolved.</span></span> <span data-ttu-id="a4974-255">Eventos resueltos establecerá tooClosed de estado del evento del riesgo de Hola y eventos de riesgo de hello ya no tendrá en cuenta toouser riesgo.</span><span class="sxs-lookup"><span data-stu-id="a4974-255">Resolved events will set hello risk event’s status tooClosed and hello risk event will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="a4974-256">**Marcar como falso positivo** : en algunos casos, puede investigar un evento de riesgo y detectar que se ha marcado incorrectamente como peligroso.</span><span class="sxs-lookup"><span data-stu-id="a4974-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="a4974-257">Puede ayudar a reducir el número de Hola de estas situaciones marcando eventos de riesgo de hello como falsos positivos.</span><span class="sxs-lookup"><span data-stu-id="a4974-257">You can help reduce hello number of such occurrences by marking hello risk event as False-positive.</span></span> <span data-ttu-id="a4974-258">Esto le ayudará a máquina Hola clasificación de hello tooimprove de algoritmos de eventos similares en hello futuras de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="a4974-258">This will help hello machine learning algorithms tooimprove hello classification of similar events in hello future.</span></span> <span data-ttu-id="a4974-259">estado de Hola de eventos de falsos positivos es demasiado**cerrado** y ya no aportará toouser riesgo.</span><span class="sxs-lookup"><span data-stu-id="a4974-259">hello status of false-positive events is too**Closed** and they will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="a4974-260">**Omitir** : si no se ha realizado una acción de corrección, pero desea Hola a riesgo eventos toobe quitado de la lista activa de hello, puede marcar un evento de riesgo omitir y estado de evento Hola se cerrará.</span><span class="sxs-lookup"><span data-stu-id="a4974-260">**Ignore** - If you have not taken any remediation action, but want hello risk event toobe removed from hello active list, you can mark a risk event Ignore and hello event status will be Closed.</span></span> <span data-ttu-id="a4974-261">Eventos omitidos no contribuyen toouser riesgo.</span><span class="sxs-lookup"><span data-stu-id="a4974-261">Ignored events do not contribute toouser risk.</span></span> <span data-ttu-id="a4974-262">Esta opción solo debe utilizarse en circunstancias inusuales.</span><span class="sxs-lookup"><span data-stu-id="a4974-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="a4974-263">**Reactivar** -el riesgo de eventos que se cierra manualmente (eligiendo **resolver**, **falso positivo**, o **omitir**) se pueden reactivar, establecer Hola estado de evento de vuelta demasiado**Active**.</span><span class="sxs-lookup"><span data-stu-id="a4974-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting hello event status back too**Active**.</span></span> <span data-ttu-id="a4974-264">Eventos de riesgo reactivados contribuyen toohello cálculo de nivel de riesgo de usuario.</span><span class="sxs-lookup"><span data-stu-id="a4974-264">Reactivated risk events contribute toohello user risk level calculation.</span></span> <span data-ttu-id="a4974-265">Los eventos de riesgo cerrados mediante una corrección (como el restablecimiento de una contraseña segura) no se pueden reactivar.</span><span class="sxs-lookup"><span data-stu-id="a4974-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="a4974-266">**cuadro de diálogo de configuración relacionados de Hola de tooopen**:</span><span class="sxs-lookup"><span data-stu-id="a4974-266">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="a4974-267">En hello **Azure AD Identity Protection** hoja, en **investigar**, haga clic en **el riesgo de eventos**.</span><span class="sxs-lookup"><span data-stu-id="a4974-267">On hello **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="a4974-268">![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1002.png "Restablecimiento manual de la contraseña")</span><span class="sxs-lookup"><span data-stu-id="a4974-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="a4974-269">Hola **el riesgo de eventos** lista, haga clic en un riesgo.</span><span class="sxs-lookup"><span data-stu-id="a4974-269">In hello **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="a4974-270">![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1003.png "Restablecimiento manual de la contraseña")</span><span class="sxs-lookup"><span data-stu-id="a4974-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="a4974-271">En la hoja de riesgo de hello, haga clic en un usuario.</span><span class="sxs-lookup"><span data-stu-id="a4974-271">On hello risk blade, right-click a user.</span></span>

    <span data-ttu-id="a4974-272">![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1004.png "Restablecimiento manual de la contraseña")</span><span class="sxs-lookup"><span data-stu-id="a4974-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="a4974-273">Cierre manual de todos los eventos de riesgo de un usuario</span><span class="sxs-lookup"><span data-stu-id="a4974-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="a4974-274">En lugar de manualmente cerrar individualmente los eventos de riesgo para un usuario, Azure Active Directory Identity Protection también proporciona un método tooclose todos los eventos para un usuario con un solo clic.</span><span class="sxs-lookup"><span data-stu-id="a4974-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method tooclose all events for a user with one click.</span></span>

<span data-ttu-id="a4974-275">![Acciones](./media/active-directory-identityprotection/2222.png "Acciones")</span><span class="sxs-lookup"><span data-stu-id="a4974-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="a4974-276">Al hacer clic en **descartar todos los eventos**, se cierran todos los eventos y usuario Hola afectado ya no está en peligro.</span><span class="sxs-lookup"><span data-stu-id="a4974-276">When you click **Dismiss all events**, all events are closed and hello affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="a4974-277">Corrección de eventos de riesgo del usuario</span><span class="sxs-lookup"><span data-stu-id="a4974-277">Remediating user risk events</span></span>

<span data-ttu-id="a4974-278">Una solución es un toosecure de acción en peligro una identidad o un dispositivo que se sospecha o conoce toobe anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a4974-278">A remediation is an action toosecure an identity or a device that was previously suspected or known toobe compromised.</span></span> <span data-ttu-id="a4974-279">Una acción correctora restaura Hola identidad o dispositivo tooa seguro estado y resuelve los eventos de riesgo anteriores asociados con la identidad de Hola o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a4974-279">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

<span data-ttu-id="a4974-280">eventos de riesgo de usuario de tooremediate, hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a4974-280">tooremediate user risk events, you can:</span></span>

* <span data-ttu-id="a4974-281">Realizar manualmente una eventos de riesgo de usuario de contraseña segura restablecimiento tooremediate</span><span class="sxs-lookup"><span data-stu-id="a4974-281">Perform a secure password reset tooremediate user risk events manually</span></span>
* <span data-ttu-id="a4974-282">Configurar una toomitigate de directiva de seguridad de usuario riesgo o corregir automáticamente los eventos de riesgo de usuario</span><span class="sxs-lookup"><span data-stu-id="a4974-282">Configure a user risk security policy toomitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="a4974-283">Dispositivo de hello infectado recrear la imagen</span><span class="sxs-lookup"><span data-stu-id="a4974-283">Re-image hello infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="a4974-284">Restablecimiento manual de una contraseña segura</span><span class="sxs-lookup"><span data-stu-id="a4974-284">Manual secure password reset</span></span>
<span data-ttu-id="a4974-285">Para restablecer una contraseña segura es una solución eficaz para muchos eventos de riesgo y cuando se lleva a cabo, automáticamente se cierra estos eventos de riesgo y vuelve a calcular el nivel de riesgo de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4974-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates hello user risk level.</span></span> <span data-ttu-id="a4974-286">Puede usar Hola Identity Protection panel tooinitiate restablezca la contraseña de un usuario de riesgo.</span><span class="sxs-lookup"><span data-stu-id="a4974-286">You can use hello Identity Protection dashboard tooinitiate a password reset for a risky user.</span></span>

<span data-ttu-id="a4974-287">cuadro de diálogo relacionado Hola proporciona una contraseña de tooreset de dos métodos diferentes:</span><span class="sxs-lookup"><span data-stu-id="a4974-287">hello related dialog provides two different methods tooreset a password:</span></span>

<span data-ttu-id="a4974-288">**Restablecimiento de contraseñas** : seleccione esta opción **requieren Hola usuario tooreset su contraseña** tooallow Hola tooself-recuperación de usuario si Hola usuario ha registrado para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="a4974-288">**Reset password** - Select **Require hello user tooreset their password** tooallow hello user tooself-recover if hello user has registered for multi-factor authentication.</span></span> <span data-ttu-id="a4974-289">Durante el saludo siguiente inicio de sesión de usuario, usuario de hello será toosolve requiere una autenticación multifactor correctamente desafío y la contraseña de hello toochange forzado, a continuación.</span><span class="sxs-lookup"><span data-stu-id="a4974-289">During hello user's next sign-in, hello user will be required toosolve a multi-factor authentication challenge successfully and then, forced toochange hello password.</span></span> <span data-ttu-id="a4974-290">Esta opción no está disponible si la cuenta de usuario de hello ya no está registrada la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="a4974-290">This option isn't available if hello user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="a4974-291">**Contraseña temporal** : seleccione esta opción **generar una contraseña temporal** tooimmediately invalidar la contraseña existente de Hola y crear una nueva contraseña temporal para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4974-291">**Temporary password** - Select **Generate a temporary password** tooimmediately invalidate hello existing password, and create a new temporary password for hello user.</span></span> <span data-ttu-id="a4974-292">Enviar Hola nueva contraseña temporal tooan dirección de correo alternativa para el usuario de Hola o administrador del usuario toohello.</span><span class="sxs-lookup"><span data-stu-id="a4974-292">Send hello new temporary password tooan alternate email address for hello user or toohello user's manager.</span></span> <span data-ttu-id="a4974-293">Como contraseña de hello es temporal, usuario de hello será toochange solicitadas Hola contraseña para inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a4974-293">Because hello password is temporary, hello user will be prompted toochange hello password upon sign-in.</span></span>

<span data-ttu-id="a4974-294">![Directiva](./media/active-directory-identityprotection/1005.png "Directiva")</span><span class="sxs-lookup"><span data-stu-id="a4974-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="a4974-295">**cuadro de diálogo de configuración relacionados de Hola de tooopen**:</span><span class="sxs-lookup"><span data-stu-id="a4974-295">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="a4974-296">En hello **Azure AD Identity Protection** hoja, haga clic en **usuarios marcan para su riesgo**.</span><span class="sxs-lookup"><span data-stu-id="a4974-296">On hello **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="a4974-297">![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1006.png "Restablecimiento manual de la contraseña")</span><span class="sxs-lookup"><span data-stu-id="a4974-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="a4974-298">En la lista Hola de usuarios, seleccione un usuario con eventos de al menos un riesgo.</span><span class="sxs-lookup"><span data-stu-id="a4974-298">From hello list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="a4974-299">![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1007.png "Restablecimiento manual de la contraseña")</span><span class="sxs-lookup"><span data-stu-id="a4974-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="a4974-300">En la hoja de usuario de hello, haga clic en **de restablecimiento de contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a4974-300">On hello user blade, click **Reset password**.</span></span>

    <span data-ttu-id="a4974-301">![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1008.png "Restablecimiento manual de la contraseña")</span><span class="sxs-lookup"><span data-stu-id="a4974-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="a4974-302">Directiva de seguridad de riesgo del usuario</span><span class="sxs-lookup"><span data-stu-id="a4974-302">User risk security policy</span></span>
<span data-ttu-id="a4974-303">Una directiva de seguridad de usuario riesgo es una directiva de acceso condicional que se evalúa como usuario específico de tooa nivel de riesgo de Hola y aplica acciones de corrección y mitigación según las reglas y condiciones predefinidas.</span><span class="sxs-lookup"><span data-stu-id="a4974-303">A user risk security policy is a conditional access policy that evaluates hello risk level tooa specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="a4974-304">![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1009.png "Directiva de riesgo de usuario")</span><span class="sxs-lookup"><span data-stu-id="a4974-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="a4974-305">Azure AD Identity Protection ayuda a administrar la mitigación de Hola y corrección de los usuarios marcados para riesgo por lo que le permite:</span><span class="sxs-lookup"><span data-stu-id="a4974-305">Azure AD Identity Protection helps you manage hello mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="a4974-306">Establecer Hola usuarios y grupos Hola la directiva se aplica a:</span><span class="sxs-lookup"><span data-stu-id="a4974-306">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="a4974-307">![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1010.png "Directiva de riesgo de usuario")</span><span class="sxs-lookup"><span data-stu-id="a4974-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="a4974-308">Establecer Hola usuario nivel umbral de riesgo (bajo, medio o alto) que desencadena la directiva de hello:</span><span class="sxs-lookup"><span data-stu-id="a4974-308">Set hello user risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="a4974-309">![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1011.png "Directiva de riesgo de usuario")</span><span class="sxs-lookup"><span data-stu-id="a4974-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="a4974-310">Conjunto Hola controles toobe aplicado cuando la directiva de hello desencadena:</span><span class="sxs-lookup"><span data-stu-id="a4974-310">Set hello controls toobe enforced when hello policy triggers:</span></span>

    <span data-ttu-id="a4974-311">![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1012.png "Directiva de riesgo de usuario")</span><span class="sxs-lookup"><span data-stu-id="a4974-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="a4974-312">Cambiar estado de saludo de la directiva:</span><span class="sxs-lookup"><span data-stu-id="a4974-312">Switch hello state of your policy:</span></span>

    <span data-ttu-id="a4974-313">![Directiva de riesgo de usuario](./media/active-directory-identityprotection/403.png "Registro MFA")</span><span class="sxs-lookup"><span data-stu-id="a4974-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="a4974-314">Revisar y evaluar el impacto de Hola de un cambio antes de activarlo:</span><span class="sxs-lookup"><span data-stu-id="a4974-314">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="a4974-315">![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1013.png "Directiva de riesgo de usuario")</span><span class="sxs-lookup"><span data-stu-id="a4974-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="a4974-316">Elegir un **alta** umbral reduce el número de Hola de veces que una directiva se desencadena y minimiza Hola impacto toousers.</span><span class="sxs-lookup"><span data-stu-id="a4974-316">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>
<span data-ttu-id="a4974-317">Sin embargo, excluye **bajo** y **medio** usuarios marcados para el riesgo de directiva de hello, que puede no proteger identidades o dispositivos que previamente se sospecha o conocidos toobe puesto en peligro.</span><span class="sxs-lookup"><span data-stu-id="a4974-317">However, it excludes **Low** and **Medium** users flagged for risk from hello policy, which may not secure identities or devices that were previously suspected or known toobe compromised.</span></span>

<span data-ttu-id="a4974-318">Cuando la configuración de Hola directiva,</span><span class="sxs-lookup"><span data-stu-id="a4974-318">When setting hello policy,</span></span>

* <span data-ttu-id="a4974-319">Excluir los usuarios que son probable toogenerate una gran cantidad de falsos positivos (los desarrolladores, analistas de seguridad)</span><span class="sxs-lookup"><span data-stu-id="a4974-319">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="a4974-320">Exclusión de usuarios en configuraciones regionales donde no es práctico si quiere habilitar Directiva de hello (por ejemplo, no toohelpdesk de acceso)</span><span class="sxs-lookup"><span data-stu-id="a4974-320">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="a4974-321">Utilice un umbral **Alto** durante la puesta en servicio inicial de la directiva, o bien si debe minimizar los desafíos que ven los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="a4974-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="a4974-322">Utilice un umbral **Bajo** si su organización requiere un mayor grado de seguridad.</span><span class="sxs-lookup"><span data-stu-id="a4974-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="a4974-323">Seleccionar un umbral **Bajo** presenta desafíos adicionales de inicio de sesión del usuario, pero aumenta la seguridad.</span><span class="sxs-lookup"><span data-stu-id="a4974-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="a4974-324">Hola, valor predeterminado recomendado para la mayoría de las organizaciones es tooconfigure una regla para un **medio** umbral toostrike un equilibrio entre la facilidad de uso y seguridad.</span><span class="sxs-lookup"><span data-stu-id="a4974-324">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="a4974-325">Para obtener información general de hello relacionados con la experiencia del usuario, consulte:</span><span class="sxs-lookup"><span data-stu-id="a4974-325">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="a4974-326">[Flujo de recuperación de cuentas en peligro](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="a4974-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="a4974-327">[Flujo de cuentas en peligro bloqueadas](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="a4974-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="a4974-328">**cuadro de diálogo de configuración relacionados de Hola de tooopen**:</span><span class="sxs-lookup"><span data-stu-id="a4974-328">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="a4974-329">En hello **Azure AD Identity Protection** hoja en hello **configurar** sección, haga clic en **directiva de usuario de riesgo**.</span><span class="sxs-lookup"><span data-stu-id="a4974-329">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="a4974-330">![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1009.png "Directiva de riesgo de usuario")</span><span class="sxs-lookup"><span data-stu-id="a4974-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="a4974-331">Mitigación de los eventos de riesgo del usuario</span><span class="sxs-lookup"><span data-stu-id="a4974-331">Mitigating user risk events</span></span>
<span data-ttu-id="a4974-332">Los administradores pueden configurar un usuario riesgo directiva tooblock los usuarios de seguridad al inicio de sesión en función de nivel de riesgo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4974-332">Administrators can set a user risk security policy tooblock users upon sign-in depending on hello risk level.</span></span>

<span data-ttu-id="a4974-333">El bloqueo de un inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="a4974-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="a4974-334">Evita Hola generación de nuevos eventos de riesgo de usuario para el usuario de hello afectado</span><span class="sxs-lookup"><span data-stu-id="a4974-334">Prevents hello generation of new user risk events for hello affected user</span></span>
* <span data-ttu-id="a4974-335">Habilita los administradores toomanually corregir los eventos de riesgo de Hola que afectan a la identidad del usuario de Hola y restaurar estado seguro tooa</span><span class="sxs-lookup"><span data-stu-id="a4974-335">Enables administrators toomanually remediate hello risk events affecting hello user's identity and restore it tooa secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="a4974-336">Directiva de registro de la autenticación multifactor</span><span class="sxs-lookup"><span data-stu-id="a4974-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="a4974-337">La autenticación multifactor Azure es un método para comprobar quién es usted que requiera el uso de Hola de algo más que un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="a4974-337">Azure multi-factor authentication is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="a4974-338">Proporciona una segunda capa de inicios de sesión de seguridad toouser y las transacciones.</span><span class="sxs-lookup"><span data-stu-id="a4974-338">It provides a second layer of security toouser sign-ins and transactions.</span></span>  
<span data-ttu-id="a4974-339">Se recomienda requerir Azure Multi-Factor Authentication en los inicios de sesión de usuario por los siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="a4974-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="a4974-340">Ofrece autenticación segura con una gama de opciones de comprobación sencillas.</span><span class="sxs-lookup"><span data-stu-id="a4974-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="a4974-341">Desempeña un papel fundamental en la preparación de su organización tooprotect y recuperarse de los peligros de cuenta</span><span class="sxs-lookup"><span data-stu-id="a4974-341">Plays a key role in preparing your organization tooprotect and recover from account compromises</span></span>

<span data-ttu-id="a4974-342">![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1019.png "Directiva de riesgo de usuario")</span><span class="sxs-lookup"><span data-stu-id="a4974-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="a4974-343">Para obtener más información, consulte [Qué es Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a4974-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="a4974-344">Azure AD Identity Protection ayuda a administrar Hola puesta en servicio de registro de la autenticación multifactor mediante la configuración de una directiva que le permite:</span><span class="sxs-lookup"><span data-stu-id="a4974-344">Azure AD Identity Protection helps you manage hello roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="a4974-345">Establecer Hola usuarios y grupos Hola la directiva se aplica a:</span><span class="sxs-lookup"><span data-stu-id="a4974-345">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="a4974-346">![Directiva de MFA](./media/active-directory-identityprotection/1020.png "Directiva de MFA")</span><span class="sxs-lookup"><span data-stu-id="a4974-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="a4974-347">Conjunto Hola controles toobe aplicado cuando la directiva de hello desencadena::</span><span class="sxs-lookup"><span data-stu-id="a4974-347">Set hello controls toobe enforced when hello policy triggers::</span></span>  

    <span data-ttu-id="a4974-348">![Directiva de MFA](./media/active-directory-identityprotection/1021.png "Directiva de MFA")</span><span class="sxs-lookup"><span data-stu-id="a4974-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="a4974-349">Cambiar estado de saludo de la directiva:</span><span class="sxs-lookup"><span data-stu-id="a4974-349">Switch hello state of your policy:</span></span>

    <span data-ttu-id="a4974-350">![Directiva de MFA](./media/active-directory-identityprotection/403.png "Directiva de MFA")</span><span class="sxs-lookup"><span data-stu-id="a4974-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="a4974-351">Ver el estado de registro de hello actual:</span><span class="sxs-lookup"><span data-stu-id="a4974-351">View hello current registration status:</span></span>

    <span data-ttu-id="a4974-352">![Directiva de MFA](./media/active-directory-identityprotection/1022.png "Directiva de MFA")</span><span class="sxs-lookup"><span data-stu-id="a4974-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="a4974-353">Para obtener información general de hello relacionados con la experiencia del usuario, consulte:</span><span class="sxs-lookup"><span data-stu-id="a4974-353">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="a4974-354">[Flujo de registro de autenticación multifactor](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="a4974-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="a4974-355">[Experiencias de inicio de sesión con Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="a4974-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="a4974-356">**cuadro de diálogo de configuración relacionados de Hola de tooopen**:</span><span class="sxs-lookup"><span data-stu-id="a4974-356">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="a4974-357">En hello **Azure AD Identity Protection** hoja en hello **configurar** sección, haga clic en **registro de la autenticación multifactor**.</span><span class="sxs-lookup"><span data-stu-id="a4974-357">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="a4974-358">![Directiva de MFA](./media/active-directory-identityprotection/1019.png "Directiva de MFA")</span><span class="sxs-lookup"><span data-stu-id="a4974-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4974-359">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a4974-359">Next steps</span></span>
* [<span data-ttu-id="a4974-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview (Channel 9: Presentación de Azure AD e Identity: versión preliminar de Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="a4974-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="a4974-361">Habilitación de Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a4974-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="a4974-362">Vulnerabilities detected by Azure Active Directory Identity Protection (Vulnerabilidades detectadas por Azure Active Directory Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="a4974-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="a4974-363">Eventos de riesgo de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4974-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="a4974-364">Azure Active Directory Identity Protection notifications (Notificaciones de Azure Active Directory Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="a4974-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="a4974-365">Azure Active Directory Identity Protection playbook (Guía de Azure Active Directory Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="a4974-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="a4974-366">Azure Active Directory Identity Protection glossary (Glosario de Azure Active Directory Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="a4974-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="a4974-367">Experiencias de inicio de sesión con Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a4974-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="a4974-368">Azure Active Directory Identity Protection - cómo los usuarios de toounblock</span><span class="sxs-lookup"><span data-stu-id="a4974-368">Azure Active Directory Identity Protection - How toounblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="a4974-369">Introducción a Azure Active Directory Identity Protection y Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="a4974-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
