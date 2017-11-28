---
title: "Solución de problemas de registro automático de equipos unidos a un dominio Azure AD para Windows 10 y Windows Server 2016 | Microsoft Docs"
description: "Solución de problemas de registro automático de equipos unidos a un dominio Azure AD para Windows 10 y Windows Server 2016."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="6f2e0-103">Solución de problemas de registro automático de equipos unidos a un dominio en Azure AD: Windows 10 y Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="6f2e0-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="6f2e0-104">Este tema es aplicable a los siguientes clientes:</span><span class="sxs-lookup"><span data-stu-id="6f2e0-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="6f2e0-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="6f2e0-105">Windows 10</span></span>
-   <span data-ttu-id="6f2e0-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="6f2e0-106">Windows Server 2016</span></span>

<span data-ttu-id="6f2e0-107">Para otros clientes Windows, vea [Solución de problemas de registro automático de equipos unidos a un dominio en Azure AD para clientes de nivel inferior de Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="6f2e0-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="6f2e0-108">En este tema se supone que ha configurado el registro automático de dispositivos unidos a un dominio como se describe en [Configuración del registro automático de dispositivos unidos a un dominio de Windows con Azure Active Directory](active-directory-device-registration-get-started.md) para admitir los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="6f2e0-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span></span>

- [<span data-ttu-id="6f2e0-109">Acceso condicional basado en dispositivos</span><span class="sxs-lookup"><span data-stu-id="6f2e0-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="6f2e0-110">Perfiles móviles de empresa</span><span class="sxs-lookup"><span data-stu-id="6f2e0-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="6f2e0-111">Windows Hello para empresas</span><span class="sxs-lookup"><span data-stu-id="6f2e0-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="6f2e0-112">En este documento se proporcionan instrucciones sobre cómo resolver problemas potenciales.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 

<span data-ttu-id="6f2e0-113">El registro se admite en la actualización de noviembre de 2015 de Windows 10 y en versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-113">The registration is supported in the Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="6f2e0-114">Se recomienda usar la Actualización de aniversario para habilitar los escenarios anteriores.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-114">We recommend using the Anniversary Update for enabling the scenarios above.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="6f2e0-115">Paso 1: Recuperar el estado del registro</span><span class="sxs-lookup"><span data-stu-id="6f2e0-115">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="6f2e0-116">**Para recuperar el estado del registro:**</span><span class="sxs-lookup"><span data-stu-id="6f2e0-116">**To retrieve the registration status:**</span></span>

1. <span data-ttu-id="6f2e0-117">Abra el símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-117">Open the command prompt as an administrator.</span></span>

2. <span data-ttu-id="6f2e0-118">Escriba **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="6f2e0-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="6f2e0-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="6f2e0-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="6f2e0-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="6f2e0-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="6f2e0-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="6f2e0-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="6f2e0-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="6f2e0-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="6f2e0-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="6f2e0-124">Paso 2: Evaluar el estado del registro</span><span class="sxs-lookup"><span data-stu-id="6f2e0-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="6f2e0-125">Revise los siguientes campos y asegúrese de que tengan los valores esperados:</span><span class="sxs-lookup"><span data-stu-id="6f2e0-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="6f2e0-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="6f2e0-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="6f2e0-127">En este campo se muestra si el dispositivo está registrado en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-127">This field shows whether the device is registered with Azure AD.</span></span> <span data-ttu-id="6f2e0-128">Si el valor se muestra como "NO", el registro no ha terminado.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-128">If the value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="6f2e0-129">**Causas posibles:**</span><span class="sxs-lookup"><span data-stu-id="6f2e0-129">**Possible causes:**</span></span>

- <span data-ttu-id="6f2e0-130">Error de autenticación del equipo para el registro.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-130">Authentication of the computer for registration failed.</span></span>

- <span data-ttu-id="6f2e0-131">Hay un servidor proxy HTTP en la organización que el equipo no puede detectar.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="6f2e0-132">El equipo no puede llegar a Azure AD para la autenticación o a DRS de Azure para el registro.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="6f2e0-133">Es posible que el equipo no esté en la red interna de la organización o en una VPN con conexión directa a una implementación local del controlador de dominio de AD.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="6f2e0-134">Si el equipo tiene un TPM, su estado puede ser incorrecto.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-134">If the computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="6f2e0-135">Puede haber un error de configuración en los servicios indicados en el documento anterior que necesita volver a verificar.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="6f2e0-136">Los ejemplos comunes son:</span><span class="sxs-lookup"><span data-stu-id="6f2e0-136">Common examples are:</span></span>

    - <span data-ttu-id="6f2e0-137">El servidor de federación no tiene habilitados los puntos de conexión de WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="6f2e0-138">Es posible que el servidor de federación no pueda permitir la autenticación de entrada de equipos de la red mediante la autenticación integrada de Windows.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="6f2e0-139">No hay ningún objeto de punto de conexión de servicio que haga referencia a su nombre de dominio comprobado en Azure AD en el bosque de AD al que pertenece el equipo.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="6f2e0-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="6f2e0-140">DomainJoined : YES</span></span>  

<span data-ttu-id="6f2e0-141">Este campo muestra si el dispositivo está unido o no a una implementación local de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="6f2e0-142">Si el valor se muestra como **NO**, el dispositivo no se puede registrar automáticamente en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="6f2e0-143">Primero compruebe que el dispositivo está unido a una implementación local de Active Directory antes de registrarlo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="6f2e0-144">Si desea unir el equipo a Azure AD directamente, vaya a la información sobre las funcionalidades de la unión a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="6f2e0-145">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="6f2e0-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="6f2e0-146">En este campo se muestra si el dispositivo está registrado en Azure AD, pero como un dispositivo personal (marcado como “Unido al área de trabajo”).</span><span class="sxs-lookup"><span data-stu-id="6f2e0-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="6f2e0-147">Si este valor debería aparecer como "NO" para un equipo unido a un dominio registrado en Azure AD, pero se muestra como YES, significa que se ha agregado una cuenta profesional o educativa antes de que el equipo termine el registro.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span></span> <span data-ttu-id="6f2e0-148">En este caso, la cuenta se ignora si se usa la versión Actualización de aniversario de Windows 10 (1607 cuando se ejecuta el comando WinVer en la ventaja “Ejecutar” o una ventana del símbolo del sistema).</span><span class="sxs-lookup"><span data-stu-id="6f2e0-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="6f2e0-149">WamDefaultSet : YES y AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="6f2e0-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="6f2e0-150">En estos campos se muestra que el usuario se ha autenticado correctamente en Azure AD al iniciar sesión en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6f2e0-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span></span> <span data-ttu-id="6f2e0-151">Si aparece “NO”, las causas posibles son:</span><span class="sxs-lookup"><span data-stu-id="6f2e0-151">If they show ‘NO’ the following are possible causes:</span></span>

- <span data-ttu-id="6f2e0-152">Clave de almacenamiento incorrecta (STK) en TPM asociada con el dispositivo tras el registro (comprobar KeySignTest mientras se ejecuta con privilegios elevados).</span><span class="sxs-lookup"><span data-stu-id="6f2e0-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="6f2e0-153">Id. de inicio de sesión alternativo</span><span class="sxs-lookup"><span data-stu-id="6f2e0-153">Alternate Login ID</span></span>

- <span data-ttu-id="6f2e0-154">No se ha encontrado el proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="6f2e0-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f2e0-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6f2e0-155">Next steps</span></span>

<span data-ttu-id="6f2e0-156">Para más información, vea [Preguntas más frecuentes sobre el registro automático de dispositivos](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="6f2e0-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 