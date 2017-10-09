---
title: "equipos Unidos de aaaTroubleshooting Hola el registro automático de dominio de Azure AD para Windows 10 y Windows Server 2016 | Documentos de Microsoft"
description: "Solución de problemas de registro automático de Hola de dominio de Azure AD los equipos Unidos para Windows 10 y Windows Server 2016."
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
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="a01d7-103">Solución de problemas de registro automático de dominio unido equipos tooAzure AD – Windows 10 y Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a01d7-103">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="a01d7-104">Este tema es aplicable toohello después de los clientes:</span><span class="sxs-lookup"><span data-stu-id="a01d7-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="a01d7-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="a01d7-105">Windows 10</span></span>
-   <span data-ttu-id="a01d7-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a01d7-106">Windows Server 2016</span></span>

<span data-ttu-id="a01d7-107">Para otros clientes de Windows, vea [solución de problemas de registro automático de dominio unido equipos tooAzure AD para clientes de nivel inferior de Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="a01d7-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="a01d7-108">En este tema se da por supuesto que ha configurado el registro automático de dispositivos Unidos a un dominio como se ha descrito en se describe en [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-device-registration-get-started.md) Hola de toosupport los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="a01d7-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello following scenarios:</span></span>

- [<span data-ttu-id="a01d7-109">Acceso condicional basado en dispositivos</span><span class="sxs-lookup"><span data-stu-id="a01d7-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="a01d7-110">Perfiles móviles de empresa</span><span class="sxs-lookup"><span data-stu-id="a01d7-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="a01d7-111">Windows Hello para empresas</span><span class="sxs-lookup"><span data-stu-id="a01d7-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="a01d7-112">Este documento proporciona instrucciones para solucionar problemas sobre cómo tooresolve posibles problemas.</span><span class="sxs-lookup"><span data-stu-id="a01d7-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 

<span data-ttu-id="a01d7-113">Hello el registro se admite en Windows hello actualizar 10 de noviembre de 2015 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="a01d7-113">hello registration is supported in hello Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="a01d7-114">Se recomienda usar actualización de aniversario de Hola para habilitar escenarios de hello anteriores.</span><span class="sxs-lookup"><span data-stu-id="a01d7-114">We recommend using hello Anniversary Update for enabling hello scenarios above.</span></span>

## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="a01d7-115">Paso 1: Recuperar el estado de registro de hello</span><span class="sxs-lookup"><span data-stu-id="a01d7-115">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="a01d7-116">**estado de registro de hello tooretrieve:**</span><span class="sxs-lookup"><span data-stu-id="a01d7-116">**tooretrieve hello registration status:**</span></span>

1. <span data-ttu-id="a01d7-117">Abra el símbolo del sistema de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="a01d7-117">Open hello command prompt as an administrator.</span></span>

2. <span data-ttu-id="a01d7-118">Escriba **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="a01d7-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="a01d7-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="a01d7-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="a01d7-120">EnterpriseJoined: Ningún Id. de dispositivo: huella digital de 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected de proveedor de cifrado de la plataforma de Microsoft: Sí KeySignTest:: debe ejecutar con permisos elevados tootest.</span><span class="sxs-lookup"><span data-stu-id="a01d7-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="a01d7-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="a01d7-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="a01d7-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="a01d7-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="a01d7-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="a01d7-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="a01d7-124">Paso 2: Evaluar el estado de registro de hello</span><span class="sxs-lookup"><span data-stu-id="a01d7-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="a01d7-125">Revise Hola después de campos y asegúrese de que tienen valores de hello esperados:</span><span class="sxs-lookup"><span data-stu-id="a01d7-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="a01d7-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="a01d7-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="a01d7-127">Este campo muestra si el dispositivo de hello está registrado con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a01d7-127">This field shows whether hello device is registered with Azure AD.</span></span> <span data-ttu-id="a01d7-128">Si el valor de Hola se muestra como "NO", el registro no ha terminado.</span><span class="sxs-lookup"><span data-stu-id="a01d7-128">If hello value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="a01d7-129">**Causas posibles:**</span><span class="sxs-lookup"><span data-stu-id="a01d7-129">**Possible causes:**</span></span>

- <span data-ttu-id="a01d7-130">Error de autenticación del equipo de hello para el registro.</span><span class="sxs-lookup"><span data-stu-id="a01d7-130">Authentication of hello computer for registration failed.</span></span>

- <span data-ttu-id="a01d7-131">Hay un proxy HTTP en la organización de Hola que no se puede detectar por equipo Hola</span><span class="sxs-lookup"><span data-stu-id="a01d7-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="a01d7-132">equipo de Hello no puede establecer comunicación con Azure AD para la autenticación o DRS de Azure para el registro</span><span class="sxs-lookup"><span data-stu-id="a01d7-132">hello computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="a01d7-133">Hello equipo no esté en la red interna de la organización de Hola o en VPN con la línea de visión directa tooan controlador de dominio de AD local.</span><span class="sxs-lookup"><span data-stu-id="a01d7-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="a01d7-134">Si el equipo de hello tiene un TPM, puede estar en mal estado.</span><span class="sxs-lookup"><span data-stu-id="a01d7-134">If hello computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="a01d7-135">Puede haber un error de configuración en los servicios indicados en el documento de Hola que necesitará tooverify nuevo.</span><span class="sxs-lookup"><span data-stu-id="a01d7-135">There may be a misconfiguration in services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="a01d7-136">Los ejemplos comunes son:</span><span class="sxs-lookup"><span data-stu-id="a01d7-136">Common examples are:</span></span>

    - <span data-ttu-id="a01d7-137">El servidor de federación no tiene habilitados los puntos de conexión de WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="a01d7-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="a01d7-138">Es posible que el servidor de federación no pueda permitir la autenticación de entrada de equipos de la red mediante la autenticación integrada de Windows.</span><span class="sxs-lookup"><span data-stu-id="a01d7-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="a01d7-139">No hay ningún objeto de punto de conexión de servicio que señala el nombre de dominio verificado de tooyour en Azure AD en bosque de AD de Hola que pertenece el equipo de Hola a</span><span class="sxs-lookup"><span data-stu-id="a01d7-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="a01d7-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="a01d7-140">DomainJoined : YES</span></span>  

<span data-ttu-id="a01d7-141">Este campo muestra si el dispositivo de hello es tooan unido a Active Directory local o no.</span><span class="sxs-lookup"><span data-stu-id="a01d7-141">This field shows whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="a01d7-142">Si el valor de hello muestra como **n**, dispositivo hello no se registran automáticamente con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a01d7-142">If hello value shows as **NO**, hello device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="a01d7-143">Comprobar primero que toohello de combinaciones de dispositivo de hello en Active Directory local antes de que se puede registrar con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a01d7-143">Check first that hello device joins toohello on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="a01d7-144">Si desea unir el equipo tooAzure AD de hello directamente, vaya tooLearn acerca de las capacidades de Azure Active Directory Join.</span><span class="sxs-lookup"><span data-stu-id="a01d7-144">If you are looking for joining hello computer tooAzure AD directly, please go tooLearn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="a01d7-145">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="a01d7-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="a01d7-146">Este campo muestra si el dispositivo de hello está registrado con Azure AD, sino como un dispositivo personal (marcado como 'Unido al área de trabajo').</span><span class="sxs-lookup"><span data-stu-id="a01d7-146">This field shows whether hello device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="a01d7-147">Si este valor debería aparecer como "NO" para un equipo unido a un dominio registrado con Azure AD, sin embargo si muestra como Sí significa que una cuenta profesional o educativa fue agregado toohello anterior equipo al completarse el registro.</span><span class="sxs-lookup"><span data-stu-id="a01d7-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior toohello computer completing registration.</span></span> <span data-ttu-id="a01d7-148">En este caso la cuenta de hello se omitirá si utiliza la versión de actualización de aniversario de Hola de Windows 10 (1607 cuando ejecuta el comando WinVer de hello en Hola "Run" ventana o una ventana de símbolo del sistema).</span><span class="sxs-lookup"><span data-stu-id="a01d7-148">In this case hello account will be ignored if using hello Anniversary Update version of Windows 10 (1607 when running hello WinVer command in hello ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="a01d7-149">WamDefaultSet : YES y AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="a01d7-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="a01d7-150">Estos campos muestran que autentica correctamente ese usuario hello tooAzure AD tras iniciar sesión en el dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="a01d7-150">These fields show that hello user has successfully authenticated tooAzure AD upon signing in toohello device.</span></span> <span data-ttu-id="a01d7-151">Si muestra "NO" siguiente hello las causas posibles es:</span><span class="sxs-lookup"><span data-stu-id="a01d7-151">If they show ‘NO’ hello following are possible causes:</span></span>

- <span data-ttu-id="a01d7-152">Clave de almacenamiento incorrecto (STK) de TPM asociado Hola dispositivo tras el registro (comprobación de Hola KeySignTest mientras se ejecuta con privilegios elevados).</span><span class="sxs-lookup"><span data-stu-id="a01d7-152">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="a01d7-153">Id. de inicio de sesión alternativo</span><span class="sxs-lookup"><span data-stu-id="a01d7-153">Alternate Login ID</span></span>

- <span data-ttu-id="a01d7-154">No se ha encontrado el proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="a01d7-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="a01d7-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a01d7-155">Next steps</span></span>

<span data-ttu-id="a01d7-156">Para obtener más información, vea hello [registro automático de dispositivos preguntas más frecuentes](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="a01d7-156">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
