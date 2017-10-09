---
title: "aaaTroubleshooting híbrido Azure Active Directory unido a dispositivos Windows 10 y Windows Server 2016 | Documentos de Microsoft"
description: "Solución de problemas de dispositivos híbridos de Windows 10 y Windows Server 2016 unidos a Azure Active Directory"
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="0e517-103">Solución de problemas de dispositivos híbridos de Windows 10 y Windows Server 2016 unidos a Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e517-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="0e517-104">Este tema es aplicable toohello después de los clientes:</span><span class="sxs-lookup"><span data-stu-id="0e517-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="0e517-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="0e517-105">Windows 10</span></span>
-   <span data-ttu-id="0e517-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="0e517-106">Windows Server 2016</span></span>

<span data-ttu-id="0e517-107">Para otros clientes Windows, consulte [Solución de problemas de dispositivos híbridos de nivel inferior unidos a Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="0e517-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="0e517-108">En este tema se da por supuesto que tiene [dispositivos Unidos a un híbrido configurado Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e517-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="0e517-109">Acceso condicional basado en dispositivos</span><span class="sxs-lookup"><span data-stu-id="0e517-109">Device-based conditional access</span></span>

- [<span data-ttu-id="0e517-110">Perfiles móviles de empresa</span><span class="sxs-lookup"><span data-stu-id="0e517-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="0e517-111">Windows Hello para empresas</span><span class="sxs-lookup"><span data-stu-id="0e517-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="0e517-112">Este documento proporciona instrucciones para solucionar problemas sobre cómo tooresolve posibles problemas.</span><span class="sxs-lookup"><span data-stu-id="0e517-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 


<span data-ttu-id="0e517-113">Actualizar de 10 de noviembre de 2015 para Windows 10 y Windows Server 2016, híbrida Hola de admite la combinación de Azure Active Directory Windows y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="0e517-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports hello Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="0e517-114">Se recomienda usar la actualización de aniversario de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e517-114">We recommend using hello Anniversary update.</span></span>

## <a name="step-1-retrieve-hello-join-status"></a><span data-ttu-id="0e517-115">Paso 1: Recuperar el estado de combinación de Hola</span><span class="sxs-lookup"><span data-stu-id="0e517-115">Step 1: Retrieve hello join status</span></span> 

<span data-ttu-id="0e517-116">**estado de combinación de Hola tooretrieve:**</span><span class="sxs-lookup"><span data-stu-id="0e517-116">**tooretrieve hello join status:**</span></span>

1. <span data-ttu-id="0e517-117">Hola abrir símbolo del sistema como administrador</span><span class="sxs-lookup"><span data-stu-id="0e517-117">Open hello command prompt as an administrator</span></span>

2. <span data-ttu-id="0e517-118">Escriba **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="0e517-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="0e517-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="0e517-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="0e517-120">EnterpriseJoined: Ningún Id. de dispositivo: huella digital de 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected de proveedor de cifrado de la plataforma de Microsoft: Sí KeySignTest:: debe ejecutar con permisos elevados tootest.</span><span class="sxs-lookup"><span data-stu-id="0e517-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="0e517-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="0e517-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="0e517-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="0e517-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="0e517-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="0e517-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-hello-join-status"></a><span data-ttu-id="0e517-124">Paso 2: Evaluar el estado de combinación de Hola</span><span class="sxs-lookup"><span data-stu-id="0e517-124">Step 2: Evaluate hello join status</span></span> 

<span data-ttu-id="0e517-125">Revise Hola después de campos y asegúrese de que tienen valores de hello esperados:</span><span class="sxs-lookup"><span data-stu-id="0e517-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="0e517-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="0e517-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="0e517-127">Este campo indica si el dispositivo de Hola se une con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e517-127">This field indicates whether hello device is joined with Azure AD.</span></span> <span data-ttu-id="0e517-128">Si el valor de hello es **n**, Hola tooAzure combinación AD no se ha completado todavía.</span><span class="sxs-lookup"><span data-stu-id="0e517-128">If hello value is **NO**, hello join tooAzure AD has not completed yet.</span></span> 

<span data-ttu-id="0e517-129">**Causas posibles:**</span><span class="sxs-lookup"><span data-stu-id="0e517-129">**Possible causes:**</span></span>

- <span data-ttu-id="0e517-130">Error de autenticación del equipo de hello para la combinación.</span><span class="sxs-lookup"><span data-stu-id="0e517-130">Authentication of hello computer for a join failed.</span></span>

- <span data-ttu-id="0e517-131">Hay un proxy HTTP en la organización de Hola que no se puede detectar por equipo Hola</span><span class="sxs-lookup"><span data-stu-id="0e517-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="0e517-132">Hola equipo no puede comunicarse con tooauthenticate de Azure AD o Azure DRS para el registro</span><span class="sxs-lookup"><span data-stu-id="0e517-132">hello computer cannot reach Azure AD tooauthenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="0e517-133">Hello equipo no esté en la red interna de la organización de Hola o en VPN con la línea de visión directa tooan controlador de dominio de AD local.</span><span class="sxs-lookup"><span data-stu-id="0e517-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="0e517-134">Si el equipo de hello tiene un TPM, puede estar en mal estado.</span><span class="sxs-lookup"><span data-stu-id="0e517-134">If hello computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="0e517-135">Puede haber un error de configuración en servicios de hello indicados en el documento de Hola que necesitará tooverify nuevo.</span><span class="sxs-lookup"><span data-stu-id="0e517-135">There might be a misconfiguration in hello services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="0e517-136">Los ejemplos comunes son:</span><span class="sxs-lookup"><span data-stu-id="0e517-136">Common examples are:</span></span>

    - <span data-ttu-id="0e517-137">El servidor de federación no tiene habilitados los puntos de conexión de WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="0e517-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="0e517-138">Es posible que el servidor de federación no permita la autenticación de entrada de equipos de la red mediante la autenticación integrada de Windows.</span><span class="sxs-lookup"><span data-stu-id="0e517-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="0e517-139">No hay ningún objeto de punto de conexión de servicio que señala el nombre de dominio verificado de tooyour en Azure AD en bosque de AD de Hola que pertenece el equipo de Hola a</span><span class="sxs-lookup"><span data-stu-id="0e517-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="0e517-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="0e517-140">DomainJoined : YES</span></span>  

<span data-ttu-id="0e517-141">Este campo indica si se une el dispositivo de hello tooan en Active Directory local o no.</span><span class="sxs-lookup"><span data-stu-id="0e517-141">This field indicates whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="0e517-142">Si el valor de hello es **n**, dispositivo hello no puede realizar una combinación de híbrida Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e517-142">If hello value is **NO**, hello device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="0e517-143">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="0e517-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="0e517-144">Este campo indica si el dispositivo de hello está registrado con Azure AD como un dispositivo personal (marcados como *al área de trabajo*).</span><span class="sxs-lookup"><span data-stu-id="0e517-144">This field indicates whether hello device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="0e517-145">Este valor debe ser **NO** para un equipo unido a un dominio que esté también unido a Azure AD híbrido.</span><span class="sxs-lookup"><span data-stu-id="0e517-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="0e517-146">Si el valor de hello es **Sí**, una cuenta profesional o educativa agregó finalización toohello anterior de combinación de hello híbrida Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e517-146">If hello value is **YES**, a work or school account was added prior toohello completion of hello hybrid Azure AD join.</span></span> <span data-ttu-id="0e517-147">En este caso, la cuenta de hello se omite cuando se usa la versión de actualización de aniversario de Hola de Windows 10 (1607).</span><span class="sxs-lookup"><span data-stu-id="0e517-147">In this case, hello account is ignored when using hello Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="0e517-148">WamDefaultSet : YES y AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="0e517-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="0e517-149">Estos campos indican si el usuario de hello autenticó correctamente tooAzure AD cuando inicien sesión en el dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="0e517-149">These fields indicate whether hello user has successfully authenticated tooAzure AD when signing in toohello device.</span></span> <span data-ttu-id="0e517-150">Si hay valores de hello **n**, podría ser debido:</span><span class="sxs-lookup"><span data-stu-id="0e517-150">If hello values are **NO**, it could be due:</span></span>

- <span data-ttu-id="0e517-151">Clave de almacenamiento incorrecto (STK) de TPM asociado Hola dispositivo tras el registro (comprobación de Hola KeySignTest mientras se ejecuta con privilegios elevados).</span><span class="sxs-lookup"><span data-stu-id="0e517-151">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="0e517-152">Id. de inicio de sesión alternativo</span><span class="sxs-lookup"><span data-stu-id="0e517-152">Alternate Login ID</span></span>

- <span data-ttu-id="0e517-153">No se ha encontrado el proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="0e517-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e517-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e517-154">Next steps</span></span>

<span data-ttu-id="0e517-155">Si tiene preguntas, consulte hello [preguntas más frecuentes sobre la administración de dispositivos](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="0e517-155">For questions, see hello [device management FAQ](device-management-faq.md)</span></span> 
