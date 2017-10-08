---
title: "Guía de Active Directory Identity Protection aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo Azure AD Identity Protection permite capacidad de hello toolimit de un tooexploit atacante una identidad en peligro o el dispositivo y toosecure una identidad o un dispositivo que era toobe sospechosa o conocido en peligro."
services: active-directory
keywords: "azure active directory identity protection, detección de aplicaciones en la nube, administración de aplicaciones, seguridad, riesgo, nivel de riesgo, punto vulnerable, directiva de seguridad"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="916f4-104">Guía de Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="916f4-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="916f4-105">Esta guía le ayudará a:</span><span class="sxs-lookup"><span data-stu-id="916f4-105">This playbook helps you to:</span></span>

* <span data-ttu-id="916f4-106">Rellenar los datos en el entorno de protección de identidad de hello vulnerabilidades y simular eventos de riesgo</span><span class="sxs-lookup"><span data-stu-id="916f4-106">Populate data in hello Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="916f4-107">Configurar directivas de acceso condicional basado en riesgo y Hola impacto de estas directivas en las pruebas</span><span class="sxs-lookup"><span data-stu-id="916f4-107">Set up risk-based conditional access policies and test hello impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="916f4-108">Simulación de eventos de riesgo</span><span class="sxs-lookup"><span data-stu-id="916f4-108">Simulating Risk Events</span></span>
<span data-ttu-id="916f4-109">En esta sección se proporciona los pasos necesarios para simular Hola siguientes tipos de eventos de riesgo:</span><span class="sxs-lookup"><span data-stu-id="916f4-109">This section provides you with steps for simulating hello following risk event types:</span></span>

* <span data-ttu-id="916f4-110">Inicios de sesión desde direcciones IP anónimas (fácil)</span><span class="sxs-lookup"><span data-stu-id="916f4-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="916f4-111">Inicios de sesión desde ubicaciones desconocidas (moderada)</span><span class="sxs-lookup"><span data-stu-id="916f4-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="916f4-112">Viaje imposible tooatypical ubicaciones (difíciles)</span><span class="sxs-lookup"><span data-stu-id="916f4-112">Impossible travel tooatypical locations (difficult)</span></span>

<span data-ttu-id="916f4-113">Otros eventos de riesgo no se pueden simular de forma segura.</span><span class="sxs-lookup"><span data-stu-id="916f4-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="916f4-114">Inicios de sesión desde direcciones IP anónimas</span><span class="sxs-lookup"><span data-stu-id="916f4-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="916f4-115">Este tipo de evento de riesgo identifica los usuarios que han iniciado sesión correctamente desde una dirección IP que se ha identificado como una dirección IP de proxy anónima.</span><span class="sxs-lookup"><span data-stu-id="916f4-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="916f4-116">Estos servidores proxy son la utilizan los usuarios que quieran toohide dirección IP de su dispositivo y puede utilizarse de forma malintencionada.</span><span class="sxs-lookup"><span data-stu-id="916f4-116">These proxies are used by people who want toohide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="916f4-117">**toosimulate en un inicio de sesión desde una IP anónima, realizar pasos de Hola**:</span><span class="sxs-lookup"><span data-stu-id="916f4-117">**toosimulate a sign-in from an anonymous IP, perform hello following steps**:</span></span>

1. <span data-ttu-id="916f4-118">Descargar hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="916f4-118">Download hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="916f4-119">Utilice Hola Tor Browser, para navegar demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="916f4-119">Using hello Tor Browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="916f4-120">Escriba las credenciales de Hola de cuenta de hello que desea tooappear Hola **inicios de sesión desde direcciones IP anónimas** informes.</span><span class="sxs-lookup"><span data-stu-id="916f4-120">Enter hello credentials of hello account you want tooappear in hello **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="916f4-121">inicio de sesión de Hola se mostrará en el panel de la protección de la identidad de Hola intervalos de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="916f4-121">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="916f4-122">Inicios de sesión desde ubicaciones desconocidas</span><span class="sxs-lookup"><span data-stu-id="916f4-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="916f4-123">riesgo de ubicaciones desconocidas Hello es un mecanismo de evaluación de inicio de sesión en tiempo real que considera más allá de las ubicaciones de inicio de sesión (IP, latitud y longitud y ASN) toodetermine nuevo / familiarizado ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="916f4-123">hello unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) toodetermine new / unfamiliar locations.</span></span> <span data-ttu-id="916f4-124">sistema Hola almacena direcciones IP anterior, latitud o longitud y ASN de un usuario y tiene en cuenta estas ubicaciones familiarizado toobe.</span><span class="sxs-lookup"><span data-stu-id="916f4-124">hello system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these toobe familiar locations.</span></span> <span data-ttu-id="916f4-125">Una ubicación de inicio de sesión se considera familiarizada si hello ubicación de inicio de sesión no coincide con ninguno de ubicaciones Hola existente.</span><span class="sxs-lookup"><span data-stu-id="916f4-125">A sign-in location is considered unfamiliar if hello sign-in location does not match any of hello existing familiar locations.</span></span>

<span data-ttu-id="916f4-126">Azure Active Directory Identity Protection:</span><span class="sxs-lookup"><span data-stu-id="916f4-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="916f4-127">Tiene un período de aprendizaje inicial de 14 días, durante el cual no marca ninguna nueva ubicación como ubicación desconocida.</span><span class="sxs-lookup"><span data-stu-id="916f4-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="916f4-128">omite los inicios de sesión desde dispositivos conocidos y ubicaciones geográficamente cerrar tooan existente familiarizado ubicación.</span><span class="sxs-lookup"><span data-stu-id="916f4-128">ignores sign-ins from familiar devices and locations that are geographically close tooan existing familiar location.</span></span>

<span data-ttu-id="916f4-129">toosimulate ubicaciones desconocidas, tiene toosign en desde una ubicación y un dispositivo que cuenta hello no ha firmado en de antes.</span><span class="sxs-lookup"><span data-stu-id="916f4-129">toosimulate unfamiliar locations, you have toosign in from a location and device that hello account has not signed in from before.</span></span> 

<span data-ttu-id="916f4-130">**toosimulate un inicio de sesión de desde una ubicación familiarizado, realizar pasos de Hola**:</span><span class="sxs-lookup"><span data-stu-id="916f4-130">**toosimulate a sign-in from an unfamiliar location, perform hello following steps**:</span></span>

1. <span data-ttu-id="916f4-131">Elija una cuenta que tenga al menos un historial de inicios de sesión de 14 días.</span><span class="sxs-lookup"><span data-stu-id="916f4-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="916f4-132">Realice uno de estos pasos:</span><span class="sxs-lookup"><span data-stu-id="916f4-132">Do either:</span></span>
   
   <span data-ttu-id="916f4-133">a.</span><span class="sxs-lookup"><span data-stu-id="916f4-133">a.</span></span> <span data-ttu-id="916f4-134">Al usar una VPN, navegue demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com) y escriba Hola credenciales de cuenta de hello que desea eventos de riesgo de hello toosimulate para.</span><span class="sxs-lookup"><span data-stu-id="916f4-134">While using a VPN, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com) and enter hello credentials of hello account you want toosimulate hello risk event for.</span></span>
   
   <span data-ttu-id="916f4-135">b.</span><span class="sxs-lookup"><span data-stu-id="916f4-135">b.</span></span> <span data-ttu-id="916f4-136">Pide a un colaborador en un toosign de otra ubicación con credenciales de la cuenta de hello (no recomendadas).</span><span class="sxs-lookup"><span data-stu-id="916f4-136">Ask an associate in a different location toosign in using hello account’s credentials (not recommended).</span></span>

<span data-ttu-id="916f4-137">inicio de sesión de Hola se mostrará en el panel de la protección de la identidad de Hola intervalos de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="916f4-137">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-tooatypical-location"></a><span data-ttu-id="916f4-138">Viaje imposible tooatypical ubicación</span><span class="sxs-lookup"><span data-stu-id="916f4-138">Impossible travel tooatypical location</span></span>
<span data-ttu-id="916f4-139">Simular la condición de viaje imposible hello es difícil porque algoritmo hello usa tooweed de aprendizaje de máquina out falsos positivos como viaje imposible desde dispositivos conocidos, o inicios de sesión de VPN que se utilizan por otros usuarios en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="916f4-139">Simulating hello impossible travel condition is difficult because hello algorithm uses machine learning tooweed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in hello directory.</span></span> <span data-ttu-id="916f4-140">Además, el algoritmo de Hola requiere un historial de inicio de sesión de 3 días de too14 para usuario de hello antes de comenzar la generación de eventos de riesgo.</span><span class="sxs-lookup"><span data-stu-id="916f4-140">Additionally, hello algorithm requires a sign-in history of 3 too14 days for hello user before it begins generating risk events.</span></span>

<span data-ttu-id="916f4-141">**toosimulate una ubicación de tooatypical viaje imposible, realizar pasos de Hola**:</span><span class="sxs-lookup"><span data-stu-id="916f4-141">**toosimulate an impossible travel tooatypical location, perform hello following steps**:</span></span>

1. <span data-ttu-id="916f4-142">Mediante el explorador estándar, navegue demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="916f4-142">Using your standard browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="916f4-143">Escriba Hola credenciales de cuenta de hello para que desea toogenerate un evento de riesgo de viaje imposible.</span><span class="sxs-lookup"><span data-stu-id="916f4-143">Enter hello credentials of hello account you want toogenerate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="916f4-144">Cambie el agente de usuario.</span><span class="sxs-lookup"><span data-stu-id="916f4-144">Change your user agent.</span></span> <span data-ttu-id="916f4-145">Puede cambiar el agente de usuario en Internet Explorer desde Herramientas de desarrollo, o bien en Firefox o Chrome con un complemento modificador del agente de usuario.</span><span class="sxs-lookup"><span data-stu-id="916f4-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="916f4-146">Cambie la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="916f4-146">Change your IP address.</span></span> <span data-ttu-id="916f4-147">Puede cambiar la dirección IP mediante una VPN, un complemento de Tor, o iniciando una máquina nueva en Azure en otro centro de datos.</span><span class="sxs-lookup"><span data-stu-id="916f4-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="916f4-148">Inicio de sesión en demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com) utilizando Hola mismas credenciales como antes y dentro de unos minutos después de inicio de sesión anterior en Hola.</span><span class="sxs-lookup"><span data-stu-id="916f4-148">Sign-in too[https://myapps.microsoft.com](https://myapps.microsoft.com) using hello same credentials as before and within a few minutes after hello previous sign-in.</span></span>

<span data-ttu-id="916f4-149">inicio de sesión de Hola se mostrará en el panel de protección de la identidad de hello dentro de 2 a 4 horas.</span><span class="sxs-lookup"><span data-stu-id="916f4-149">hello sign-in will show up in hello Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="916f4-150">Debido a la máquina complejas de hello implicados modelos de aprendizaje, es probable que no obtenga recogerán.</span><span class="sxs-lookup"><span data-stu-id="916f4-150">Because of hello complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="916f4-151">Conviene tooreplicate estos pasos para varias cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="916f4-151">You might want tooreplicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="916f4-152">Simulación de puntos vulnerables</span><span class="sxs-lookup"><span data-stu-id="916f4-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="916f4-153">Los puntos vulnerables son puntos débiles de un entorno de Azure AD que puede ser aprovechados por un actor perjudicial.</span><span class="sxs-lookup"><span data-stu-id="916f4-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="916f4-154">Actualmente se exponen 3 tipos de puntos vulnerables en Azure AD Identity Protection que aprovechan otras características de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="916f4-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="916f4-155">Estas vulnerabilidades se mostrará en el panel de la protección de la identidad de hello automáticamente una vez que se configuran estas características.</span><span class="sxs-lookup"><span data-stu-id="916f4-155">These Vulnerabilities will be displayed on hello Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="916f4-156">Azure AD [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="916f4-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="916f4-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="916f4-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="916f4-158">[Privileged Identity Management](active-directory-privileged-identity-management-configure.md)de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="916f4-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="916f4-159">Riesgo de compromiso de usuario</span><span class="sxs-lookup"><span data-stu-id="916f4-159">User compromise risk</span></span>
<span data-ttu-id="916f4-160">**tootest riesgo del compromiso de usuario, realizar pasos de Hola**:</span><span class="sxs-lookup"><span data-stu-id="916f4-160">**tootest User compromise risk, perform hello following steps**:</span></span>

1. <span data-ttu-id="916f4-161">Inicio de sesión en demasiado[https://portal.azure.com](https://portal.azure.com) con credenciales de administrador global para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="916f4-161">Sign-in too[https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="916f4-162">Navegue demasiado**Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="916f4-162">Navigate too**Identity Protection**.</span></span> 
3. <span data-ttu-id="916f4-163">En hello principal **Azure AD Identity Protection** hoja, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="916f4-163">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="916f4-164">En hello **configuración del Portal** hoja, en **las reglas de seguridad**, haga clic en **riesgo del compromiso de usuario**.</span><span class="sxs-lookup"><span data-stu-id="916f4-164">On hello **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="916f4-165">En hello **iniciar sesión en riesgo** hoja, activar **Habilitar regla** desactivada y, a continuación, haga clic en **guardar** configuración.</span><span class="sxs-lookup"><span data-stu-id="916f4-165">On hello **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="916f4-166">Para una cuenta de usuario determinada, simule un evento de riesgo de ubicaciones desconocidas o IP anónima.</span><span class="sxs-lookup"><span data-stu-id="916f4-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="916f4-167">Esto elevará nivel de riesgo de usuario de Hola para ese usuario demasiado**medio**.</span><span class="sxs-lookup"><span data-stu-id="916f4-167">This will elevate hello user risk level for that user too**Medium**.</span></span>
7. <span data-ttu-id="916f4-168">Espere unos minutos y después compruebe que el nivel de usuario para el usuario sea **Medio**.</span><span class="sxs-lookup"><span data-stu-id="916f4-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="916f4-169">Vaya toohello **configuración del Portal** hoja.</span><span class="sxs-lookup"><span data-stu-id="916f4-169">Go toohello **Portal Settings** blade.</span></span>
9. <span data-ttu-id="916f4-170">En hello **riesgo del compromiso de usuario** hoja, en **Habilitar regla**, seleccione **en** .</span><span class="sxs-lookup"><span data-stu-id="916f4-170">On hello **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="916f4-171">Seleccione una de las siguientes opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="916f4-171">Select one of hello following options:</span></span>
    
    <span data-ttu-id="916f4-172">a.</span><span class="sxs-lookup"><span data-stu-id="916f4-172">a.</span></span> <span data-ttu-id="916f4-173">tooblock, seleccione **medio** en **bloque iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="916f4-173">tooblock, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="916f4-174">b.</span><span class="sxs-lookup"><span data-stu-id="916f4-174">b.</span></span> <span data-ttu-id="916f4-175">cambio de contraseña segura tooenforce, seleccione **medio** en **requerir la autenticación multifactor**.</span><span class="sxs-lookup"><span data-stu-id="916f4-175">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="916f4-176">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="916f4-176">Click **Save**.</span></span>
12. <span data-ttu-id="916f4-177">Ahora puede probar el acceso condicional basado en riesgos mediante un inicio de sesión con un usuario con un nivel de riesgo elevado.</span><span class="sxs-lookup"><span data-stu-id="916f4-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="916f4-178">Si el riesgo de usuario de hello es medio, dependiendo de la directiva de configuración de hello, el inicio de sesión es bloqueará cualquiera o se convierten obligatoriamente toochange su contraseña.</span><span class="sxs-lookup"><span data-stu-id="916f4-178">If hello user risk is Medium, depending on hello configuration of your policy, your sign-in is be either blocked or you are forced toochange your password.</span></span> 
    <br><br><span data-ttu-id="916f4-179">
    ![Guía de](./media/active-directory-identityprotection-playbook/201.png "guía")
    </span><span class="sxs-lookup"><span data-stu-id="916f4-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="916f4-180">Riesgo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="916f4-180">Sign-in risk</span></span>
<span data-ttu-id="916f4-181">**tootest un inicio de sesión en riesgo, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="916f4-181">**tootest a sign in risk, perform hello following steps:**</span></span>

1. <span data-ttu-id="916f4-182">Inicio de sesión en demasiado[https://portal.azure.com ](https://portal.azure.com) con credenciales de administrador global para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="916f4-182">Sign-in too[https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="916f4-183">Navegue demasiado**Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="916f4-183">Navigate too**Identity Protection**.</span></span>
3. <span data-ttu-id="916f4-184">En hello principal **Azure AD Identity Protection** hoja, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="916f4-184">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="916f4-185">En hello **configuración del Portal** hoja, en **las reglas de seguridad**, haga clic en **iniciar sesión en riesgo**.</span><span class="sxs-lookup"><span data-stu-id="916f4-185">On hello **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="916f4-186">En Hola ** iniciar sesión en riesgo ** hoja, seleccione **en** en **Habilitar regla**.</span><span class="sxs-lookup"><span data-stu-id="916f4-186">On hello **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="916f4-187">Seleccione una de las siguientes opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="916f4-187">Select one of hello following options:</span></span>
   
   <span data-ttu-id="916f4-188">a.</span><span class="sxs-lookup"><span data-stu-id="916f4-188">a.</span></span> <span data-ttu-id="916f4-189">tooblock, seleccione **medio** en **bloque iniciar sesión en**</span><span class="sxs-lookup"><span data-stu-id="916f4-189">tooblock, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="916f4-190">b.</span><span class="sxs-lookup"><span data-stu-id="916f4-190">b.</span></span> <span data-ttu-id="916f4-191">cambio de contraseña segura tooenforce, seleccione **medio** en **requerir la autenticación multifactor**.</span><span class="sxs-lookup"><span data-stu-id="916f4-191">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="916f4-192">tooblock, seleccione medio en el bloque de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="916f4-192">tooblock, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="916f4-193">tooenforce la autenticación multifactor, seleccione **medio** en **requerir la autenticación multifactor**.</span><span class="sxs-lookup"><span data-stu-id="916f4-193">tooenforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="916f4-194">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="916f4-194">Click on **Save**.</span></span>
10. <span data-ttu-id="916f4-195">Ahora puede probar el acceso condicional basado en riesgo mediante la simulación de ubicaciones desconocidas de Hola o IP anónima el riesgo de eventos porque son ambos **medio** el riesgo de eventos.</span><span class="sxs-lookup"><span data-stu-id="916f4-195">You can now test risk-based conditional access by simulating hello unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="916f4-196">![Guía de](./media/active-directory-identityprotection-playbook/200.png "Guía")</span><span class="sxs-lookup"><span data-stu-id="916f4-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="916f4-197">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="916f4-197">See also</span></span>
* [<span data-ttu-id="916f4-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="916f4-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

