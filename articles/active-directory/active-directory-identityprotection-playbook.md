---
title: "Guía de Azure Active Directory Identity Protection | Microsoft Docs"
description: "Aprenda cómo Azure AD Identity Protection permite limitar la capacidad de un atacante para aprovechar una identidad o un dispositivo en peligro y asegurar una identidad o un dispositivo que antes fue sospechoso o que se sabe que estuvo en peligro."
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
ms.openlocfilehash: 2ecd07faed785fa6aa179ac1cca35a70d965e1dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="28f9a-104">Guía de Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="28f9a-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="28f9a-105">Esta guía le ayudará a:</span><span class="sxs-lookup"><span data-stu-id="28f9a-105">This playbook helps you to:</span></span>

* <span data-ttu-id="28f9a-106">Rellenar los datos en el entorno de Identity Protection mediante la simulación de vulnerabilidades y eventos de riesgo</span><span class="sxs-lookup"><span data-stu-id="28f9a-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="28f9a-107">Configurar directivas de acceso condicional en función del riesgo y probar el impacto de estas directivas</span><span class="sxs-lookup"><span data-stu-id="28f9a-107">Set up risk-based conditional access policies and test the impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="28f9a-108">Simulación de eventos de riesgo</span><span class="sxs-lookup"><span data-stu-id="28f9a-108">Simulating Risk Events</span></span>
<span data-ttu-id="28f9a-109">En esta sección se indican los pasos para simular los siguientes tipos de eventos de riesgo:</span><span class="sxs-lookup"><span data-stu-id="28f9a-109">This section provides you with steps for simulating the following risk event types:</span></span>

* <span data-ttu-id="28f9a-110">Inicios de sesión desde direcciones IP anónimas (fácil)</span><span class="sxs-lookup"><span data-stu-id="28f9a-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="28f9a-111">Inicios de sesión desde ubicaciones desconocidas (moderada)</span><span class="sxs-lookup"><span data-stu-id="28f9a-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="28f9a-112">Viaje imposible a ubicaciones inusuales (difícil)</span><span class="sxs-lookup"><span data-stu-id="28f9a-112">Impossible travel to atypical locations (difficult)</span></span>

<span data-ttu-id="28f9a-113">Otros eventos de riesgo no se pueden simular de forma segura.</span><span class="sxs-lookup"><span data-stu-id="28f9a-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="28f9a-114">Inicios de sesión desde direcciones IP anónimas</span><span class="sxs-lookup"><span data-stu-id="28f9a-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="28f9a-115">Este tipo de evento de riesgo identifica los usuarios que han iniciado sesión correctamente desde una dirección IP que se ha identificado como una dirección IP de proxy anónima.</span><span class="sxs-lookup"><span data-stu-id="28f9a-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="28f9a-116">A menudo, estos servidores proxy los usan los usuarios que desean ocultar la dirección IP del dispositivo y es posible que se usen con fines malintencionados.</span><span class="sxs-lookup"><span data-stu-id="28f9a-116">These proxies are used by people who want to hide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="28f9a-117">**Para simular un inicio de sesión desde una IP anónima, realice los siguientes pasos**:</span><span class="sxs-lookup"><span data-stu-id="28f9a-117">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span></span>

1. <span data-ttu-id="28f9a-118">Descargue el [explorador Tor](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="28f9a-118">Download the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="28f9a-119">Mediante el explorador Tor, vaya a [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="28f9a-119">Using the Tor Browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="28f9a-120">Escriba las credenciales de la cuenta que desee que aparezcan en el informe **Inicios de sesión desde direcciones IP anónimas** .</span><span class="sxs-lookup"><span data-stu-id="28f9a-120">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="28f9a-121">El inicio de sesión se mostrará en el panel de Identity Protection en un plazo máximo de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="28f9a-121">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="28f9a-122">Inicios de sesión desde ubicaciones desconocidas</span><span class="sxs-lookup"><span data-stu-id="28f9a-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="28f9a-123">El riesgo de ubicaciones desconocidas es un mecanismo de evaluación de inicios de sesión en tiempo real que tiene en cuenta las ubicaciones de inicio de sesión anteriores (IP, latitud/longitud y ASN) para determinar las ubicaciones nuevas o desconocidas.</span><span class="sxs-lookup"><span data-stu-id="28f9a-123">The unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="28f9a-124">El sistema almacena las direcciones IP, la latitud/longitud y las ASN anteriores, y considera que son ubicaciones conocidas.</span><span class="sxs-lookup"><span data-stu-id="28f9a-124">The system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these to be familiar locations.</span></span> <span data-ttu-id="28f9a-125">Una ubicación de inicio de sesión se considera desconocida si la ubicación de inicio de sesión no coincide con ninguna de las ubicaciones conocidas existentes.</span><span class="sxs-lookup"><span data-stu-id="28f9a-125">A sign-in location is considered unfamiliar if the sign-in location does not match any of the existing familiar locations.</span></span>

<span data-ttu-id="28f9a-126">Azure Active Directory Identity Protection:</span><span class="sxs-lookup"><span data-stu-id="28f9a-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="28f9a-127">Tiene un período de aprendizaje inicial de 14 días, durante el cual no marca ninguna nueva ubicación como ubicación desconocida.</span><span class="sxs-lookup"><span data-stu-id="28f9a-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="28f9a-128">Omite los inicios de sesión desde dispositivos conocidos y ubicaciones geográficamente cercanas a una ubicación familiar existente </span><span class="sxs-lookup"><span data-stu-id="28f9a-128">ignores sign-ins from familiar devices and locations that are geographically close to an existing familiar location.</span></span>

<span data-ttu-id="28f9a-129">Para simular ubicaciones desconocidas, debe iniciar sesión desde una ubicación y un dispositivo desde los que no se haya iniciado sesión en esa cuenta antes.</span><span class="sxs-lookup"><span data-stu-id="28f9a-129">To simulate unfamiliar locations, you have to sign in from a location and device that the account has not signed in from before.</span></span> 

<span data-ttu-id="28f9a-130">**Para simular un inicio de sesión desde una ubicación desconocida, realice los siguientes pasos**:</span><span class="sxs-lookup"><span data-stu-id="28f9a-130">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span></span>

1. <span data-ttu-id="28f9a-131">Elija una cuenta que tenga al menos un historial de inicios de sesión de 14 días.</span><span class="sxs-lookup"><span data-stu-id="28f9a-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="28f9a-132">Realice uno de estos pasos:</span><span class="sxs-lookup"><span data-stu-id="28f9a-132">Do either:</span></span>
   
   <span data-ttu-id="28f9a-133">a.</span><span class="sxs-lookup"><span data-stu-id="28f9a-133">a.</span></span> <span data-ttu-id="28f9a-134">Mientras usa una VPN, vaya a [https://myapps.microsoft.com](https://myapps.microsoft.com) y escriba las credenciales de la cuenta para la que desea simular el evento de riesgo.</span><span class="sxs-lookup"><span data-stu-id="28f9a-134">While using a VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of the account you want to simulate the risk event for.</span></span>
   
   <span data-ttu-id="28f9a-135">b.</span><span class="sxs-lookup"><span data-stu-id="28f9a-135">b.</span></span> <span data-ttu-id="28f9a-136">Pida a un colaborador en otra ubicación que inicie sesión con las credenciales de la cuenta (no recomendado).</span><span class="sxs-lookup"><span data-stu-id="28f9a-136">Ask an associate in a different location to sign in using the account’s credentials (not recommended).</span></span>

<span data-ttu-id="28f9a-137">El inicio de sesión se mostrará en el panel de Identity Protection en un plazo máximo de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="28f9a-137">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-to-atypical-location"></a><span data-ttu-id="28f9a-138">Viaje imposible a una ubicación inusual</span><span class="sxs-lookup"><span data-stu-id="28f9a-138">Impossible travel to atypical location</span></span>
<span data-ttu-id="28f9a-139">Simular la condición de viaje imposible es complicado porque el algoritmo utiliza el aprendizaje automático para descartar falsos positivos, como un viaje imposible desde dispositivos conocidos o inicios de sesión de VPN usadas por otros usuarios del directorio.</span><span class="sxs-lookup"><span data-stu-id="28f9a-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span></span> <span data-ttu-id="28f9a-140">Además, el algoritmo requiere un historial de inicios de sesión del usuario de 3 a 14 días antes de que comience a generar eventos de riesgo.</span><span class="sxs-lookup"><span data-stu-id="28f9a-140">Additionally, the algorithm requires a sign-in history of 3 to 14 days for the user before it begins generating risk events.</span></span>

<span data-ttu-id="28f9a-141">**Para simular un viaje imposible a una ubicación inusual, realice los pasos siguientes**:</span><span class="sxs-lookup"><span data-stu-id="28f9a-141">**To simulate an impossible travel to atypical location, perform the following steps**:</span></span>

1. <span data-ttu-id="28f9a-142">Mediante el explorador estándar, vaya a [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="28f9a-142">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="28f9a-143">Escriba las credenciales de la cuenta para la que desea generar un evento de riesgo de viaje imposible.</span><span class="sxs-lookup"><span data-stu-id="28f9a-143">Enter the credentials of the account you want to generate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="28f9a-144">Cambie el agente de usuario.</span><span class="sxs-lookup"><span data-stu-id="28f9a-144">Change your user agent.</span></span> <span data-ttu-id="28f9a-145">Puede cambiar el agente de usuario en Internet Explorer desde Herramientas de desarrollo, o bien en Firefox o Chrome con un complemento modificador del agente de usuario.</span><span class="sxs-lookup"><span data-stu-id="28f9a-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="28f9a-146">Cambie la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="28f9a-146">Change your IP address.</span></span> <span data-ttu-id="28f9a-147">Puede cambiar la dirección IP mediante una VPN, un complemento de Tor, o iniciando una máquina nueva en Azure en otro centro de datos.</span><span class="sxs-lookup"><span data-stu-id="28f9a-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="28f9a-148">Inicie sesión en [https://myapps.microsoft.com](https://myapps.microsoft.com) con las mismas credenciales que antes y pocos minutos después del inicio de sesión anterior.</span><span class="sxs-lookup"><span data-stu-id="28f9a-148">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span></span>

<span data-ttu-id="28f9a-149">El inicio de sesión se mostrará en el panel de Identity Protection entre 2 y 4 horas después.</span><span class="sxs-lookup"><span data-stu-id="28f9a-149">The sign-in will show up in the Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="28f9a-150">Debido a los complejo modelos de aprendizaje automático implicados, es posible que no se detecte.</span><span class="sxs-lookup"><span data-stu-id="28f9a-150">Because of the complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="28f9a-151">Puede replicar estos pasos para varias cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28f9a-151">You might want to replicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="28f9a-152">Simulación de puntos vulnerables</span><span class="sxs-lookup"><span data-stu-id="28f9a-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="28f9a-153">Los puntos vulnerables son puntos débiles de un entorno de Azure AD que puede ser aprovechados por un actor perjudicial.</span><span class="sxs-lookup"><span data-stu-id="28f9a-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="28f9a-154">Actualmente se exponen 3 tipos de puntos vulnerables en Azure AD Identity Protection que aprovechan otras características de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28f9a-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="28f9a-155">Estos puntos vulnerables se mostrará en el panel de Identity Protection automáticamente una vez configuradas estas características.</span><span class="sxs-lookup"><span data-stu-id="28f9a-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="28f9a-156">Azure AD [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="28f9a-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="28f9a-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28f9a-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="28f9a-158">[Privileged Identity Management](active-directory-privileged-identity-management-configure.md)de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28f9a-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="28f9a-159">Riesgo de compromiso de usuario</span><span class="sxs-lookup"><span data-stu-id="28f9a-159">User compromise risk</span></span>
<span data-ttu-id="28f9a-160">**Para probar el riesgo de compromiso de usuario, realice los pasos siguientes**:</span><span class="sxs-lookup"><span data-stu-id="28f9a-160">**To test User compromise risk, perform the following steps**:</span></span>

1. <span data-ttu-id="28f9a-161">Inicie sesión en [https://portal.azure.com](https://portal.azure.com) con las credenciales de administrador global para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="28f9a-161">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="28f9a-162">Vaya a **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-162">Navigate to **Identity Protection**.</span></span> 
3. <span data-ttu-id="28f9a-163">En la hoja principal de **Azure AD Identity Protection**, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-163">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="28f9a-164">En la hoja **Configuración del portal**, en **Reglas de seguridad**, haga clic en **Riesgo de compromiso de usuario**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-164">On the **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="28f9a-165">En la hoja **Riesgo de inicio de sesión**, desactive **Habilitar regla** y, a continuación, haga clic en **Guardar** la configuración.</span><span class="sxs-lookup"><span data-stu-id="28f9a-165">On the **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="28f9a-166">Para una cuenta de usuario determinada, simule un evento de riesgo de ubicaciones desconocidas o IP anónima.</span><span class="sxs-lookup"><span data-stu-id="28f9a-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="28f9a-167">Esto eleva el nivel de riesgo del usuario para ese usuario a **Medio**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-167">This will elevate the user risk level for that user to **Medium**.</span></span>
7. <span data-ttu-id="28f9a-168">Espere unos minutos y después compruebe que el nivel de usuario para el usuario sea **Medio**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="28f9a-169">Vaya a la hoja **Configuración del portal** .</span><span class="sxs-lookup"><span data-stu-id="28f9a-169">Go to the **Portal Settings** blade.</span></span>
9. <span data-ttu-id="28f9a-170">En la hoja **Riesgo de compromiso de usuario**, en **Habilitar regla**, seleccione **Activado**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-170">On the **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="28f9a-171">Seleccione una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="28f9a-171">Select one of the following options:</span></span>
    
    <span data-ttu-id="28f9a-172">a.</span><span class="sxs-lookup"><span data-stu-id="28f9a-172">a.</span></span> <span data-ttu-id="28f9a-173">Para bloquearlo, seleccione **Medio** en **Bloquear inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-173">To block, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="28f9a-174">b.</span><span class="sxs-lookup"><span data-stu-id="28f9a-174">b.</span></span> <span data-ttu-id="28f9a-175">Para aplicar el cambio de contraseña segura, seleccione **Medio** en **Requerir autenticación multifactor**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-175">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="28f9a-176">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-176">Click **Save**.</span></span>
12. <span data-ttu-id="28f9a-177">Ahora puede probar el acceso condicional basado en riesgos mediante un inicio de sesión con un usuario con un nivel de riesgo elevado.</span><span class="sxs-lookup"><span data-stu-id="28f9a-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="28f9a-178">Si el riesgo del usuario es Medio, en función de la directiva que establezca, se bloqueará el inicio de sesión o se forzará el cambio de contraseña.</span><span class="sxs-lookup"><span data-stu-id="28f9a-178">If the user risk is Medium, depending on the configuration of your policy, your sign-in is be either blocked or you are forced to change your password.</span></span> 
    <br><br><span data-ttu-id="28f9a-179">
    ![Guía de](./media/active-directory-identityprotection-playbook/201.png "guía")
    </span><span class="sxs-lookup"><span data-stu-id="28f9a-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="28f9a-180">Riesgo de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="28f9a-180">Sign-in risk</span></span>
<span data-ttu-id="28f9a-181">**Para probar el riesgo de inicio de sesión, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="28f9a-181">**To test a sign in risk, perform the following steps:**</span></span>

1. <span data-ttu-id="28f9a-182">Inicie sesión en [https://portal.azure.com ](https://portal.azure.com) con las credenciales de administrador global para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="28f9a-182">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="28f9a-183">Vaya a **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-183">Navigate to **Identity Protection**.</span></span>
3. <span data-ttu-id="28f9a-184">En la hoja principal de **Azure AD Identity Protection**, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-184">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="28f9a-185">En la hoja **Configuración del portal**, en **Reglas de seguridad**, haga clic en **Riesgo de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-185">On the **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="28f9a-186">En el ** iniciar sesión en riesgo ** hoja, seleccione **en** en **Habilitar regla**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-186">On the **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="28f9a-187">Seleccione una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="28f9a-187">Select one of the following options:</span></span>
   
   <span data-ttu-id="28f9a-188">a.</span><span class="sxs-lookup"><span data-stu-id="28f9a-188">a.</span></span> <span data-ttu-id="28f9a-189">Para bloquearlo, seleccione **Medio** en **Bloquear inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-189">To block, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="28f9a-190">b.</span><span class="sxs-lookup"><span data-stu-id="28f9a-190">b.</span></span> <span data-ttu-id="28f9a-191">Para aplicar el cambio de contraseña segura, seleccione **Medio** en **Requerir autenticación multifactor**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-191">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="28f9a-192">Para bloquearlo, seleccione Medio en Bloquear inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="28f9a-192">To block, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="28f9a-193">Para aplicar la autenticación multifactor, seleccione **Medio** en **Requerir autenticación multifactor**.</span><span class="sxs-lookup"><span data-stu-id="28f9a-193">To enforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="28f9a-194">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="28f9a-194">Click on **Save**.</span></span>
10. <span data-ttu-id="28f9a-195">Ahora puede probar el acceso condicional basado en riesgos mediante la simulación de los eventos de riesgo de IP anónima o ubicaciones desconocidas, porque son eventos de riesgo **Medio** .</span><span class="sxs-lookup"><span data-stu-id="28f9a-195">You can now test risk-based conditional access by simulating the unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="28f9a-196">![Guía de](./media/active-directory-identityprotection-playbook/200.png "Guía")</span><span class="sxs-lookup"><span data-stu-id="28f9a-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="28f9a-197">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="28f9a-197">See also</span></span>
* [<span data-ttu-id="28f9a-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="28f9a-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

