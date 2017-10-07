---
title: "Azure AD Connect: funcionamiento del inicio de sesión único de conexión directa | Microsoft Docs"
description: "Este artículo describe cómo funciona la característica de Azure Active Directory sin problemas Single Sign-On Hola."
services: active-directory
keywords: "qué es Azure AD Connect, instalar Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="c5781-104">Inicio de sesión único de conexión directa de Azure Active Directory: información técnica detallada</span><span class="sxs-lookup"><span data-stu-id="c5781-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="c5781-105">Este artículo proporciona detalles técnicos en cómo funciona la característica de Azure Active Directory sin problemas Single Sign-On (SSO sin problemas) Hola.</span><span class="sxs-lookup"><span data-stu-id="c5781-105">This article gives you technical details into how hello Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c5781-106">característica de SSO sin problemas de Hello está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="c5781-106">hello Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="c5781-107">¿Cómo funciona SSO de conexión directa?</span><span class="sxs-lookup"><span data-stu-id="c5781-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="c5781-108">En esta sección tiene tooit de dos partes:</span><span class="sxs-lookup"><span data-stu-id="c5781-108">This section has two parts tooit:</span></span>
1. <span data-ttu-id="c5781-109">programa de instalación de Hola de característica de hello SSO sin problemas.</span><span class="sxs-lookup"><span data-stu-id="c5781-109">hello setup of hello Seamless SSO feature.</span></span>
2. <span data-ttu-id="c5781-110">Funcionamiento de una transacción de inicio de sesión de usuario único con SSO de conexión directa.</span><span class="sxs-lookup"><span data-stu-id="c5781-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="c5781-111">¿Cómo funciona la configuración?</span><span class="sxs-lookup"><span data-stu-id="c5781-111">How does set up work?</span></span>

<span data-ttu-id="c5781-112">SSO de conexión directa se habilita a través de Azure AD Connect tal como se muestra [aquí](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="c5781-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="c5781-113">Al habilitar la característica de hello, se produce Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c5781-113">While enabling hello feature, hello following steps occur:</span></span>
- <span data-ttu-id="c5781-114">Una cuenta de equipo denominada `AZUREADSSOACCT` (que representa a Azure AD) se crea en la instancia local de Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="c5781-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="c5781-115">clave de descifrado de Kerberos de la cuenta de equipo de Hola se comparte de forma segura con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5781-115">hello computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="c5781-116">Además, los nombres de entidad de seguridad de servicio (SPN) dos de Kerberos se crean toorepresent dos direcciones URL que se usan durante el inicio de sesión en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5781-116">In addition, two Kerberos service principal names (SPNs) are created toorepresent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="c5781-117">cuenta de equipo de Hola y Hola SPN de Kerberos se crean en cada bosque de AD sincronizar tooAzure AD (mediante Azure AD Connect) y para cuyos usuarios desea SSO sin problemas.</span><span class="sxs-lookup"><span data-stu-id="c5781-117">hello computer account and hello Kerberos SPNs are created in each AD forest you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="c5781-118">Mover hello `AZUREADSSOACCT` tooan de cuenta de equipo unidad organizativa (OU) donde otras cuentas de equipo son tooensure almacenado que se administran en Hola misma manera y no se elimina.</span><span class="sxs-lookup"><span data-stu-id="c5781-118">Move hello `AZUREADSSOACCT` computer account tooan Organization Unit (OU) where other computer accounts are stored tooensure that it is managed in hello same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c5781-119">Es muy recomendable que se [clave de descifrado de hello Kerberos se sustituyen](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) de hello `AZUREADSSOACCT` cuenta de equipo al menos cada 30 días.</span><span class="sxs-lookup"><span data-stu-id="c5781-119">We highly recommend that you [roll over hello Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of hello `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="c5781-120">¿Cómo funciona el inicio de sesión con SSO de conexión directa?</span><span class="sxs-lookup"><span data-stu-id="c5781-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="c5781-121">Una vez completada la instalación de hello, SSO sin problemas funciona Hola mismo modo que con cualquier otra sesión que usa autenticación integrada de Windows (IWA).</span><span class="sxs-lookup"><span data-stu-id="c5781-121">Once hello set-up is complete, Seamless SSO works hello same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="c5781-122">flujo de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="c5781-122">hello flow is as follows:</span></span>

1. <span data-ttu-id="c5781-123">usuario de Hello intente tooaccess una aplicación (por ejemplo, Hola Outlook Web App - https://outlook.office365.com/owa/) desde un dispositivo corporativo Unidos a un dominio dentro de su red corporativa.</span><span class="sxs-lookup"><span data-stu-id="c5781-123">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="c5781-124">Si el usuario de hello no ha iniciado ya sesión, usuario de hello es página de inicio de sesión de Azure AD de toohello redirigida.</span><span class="sxs-lookup"><span data-stu-id="c5781-124">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="c5781-125">Si una solicitud de inicio de sesión hello Azure AD incluye un `domain_hint` (identificar su inquilino: por ejemplo, contoso.onmicrosoft.com) o `login_hint` (identificación de usuario de hello - por ejemplo, user@contoso.onmicrosoft.com o user@contoso.com) se omite el parámetro y, a continuación, paso 2.</span><span class="sxs-lookup"><span data-stu-id="c5781-125">If hello Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying hello user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="c5781-126">tipos de usuario de Hello en su nombre de usuario en la página de inicio de sesión de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5781-126">hello user types in their user name into hello Azure AD sign-in page.</span></span>
4. <span data-ttu-id="c5781-127">Usar JavaScript en segundo plano de hello, Azure AD desafíos de explorador hello, a través de una respuesta 401 no autorizado, tooprovide un vale de Kerberos.</span><span class="sxs-lookup"><span data-stu-id="c5781-127">Using JavaScript in hello background, Azure AD challenges hello browser, via a 401 Unauthorized response, tooprovide a Kerberos ticket.</span></span>
5. <span data-ttu-id="c5781-128">Explorador de Hello, a su vez, solicita un vale desde Active Directory para hello `AZUREADSSOACCT` cuenta de equipo (representado por Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5781-128">hello browser, in turn, requests a ticket from Active Directory for hello `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="c5781-129">Active Directory localiza la cuenta de equipo de Hola y devuelve un explorador de toohello de vale de Kerberos cifrado con el secreto de la cuenta de equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5781-129">Active Directory locates hello computer account and returns a Kerberos ticket toohello browser encrypted with hello computer account's secret.</span></span>
7. <span data-ttu-id="c5781-130">Explorador de Hello reenvía el vale de Kerberos de hello obtenido de Active Directory tooAzure AD (en uno de hello [las direcciones URL de Azure AD agregan previamente la configuración de zona de Intranet del explorador toohello](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="c5781-130">hello browser forwards hello Kerberos ticket it acquired from Active Directory tooAzure AD (on one of hello [Azure AD URLs previously added toohello browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="c5781-131">Azure AD descifra Hola vale de Kerberos, que incluye Hola identidad de hello usuario inició sesión en el dispositivo corporativo de hello, utilizaba anteriormente Hola clave compartida.</span><span class="sxs-lookup"><span data-stu-id="c5781-131">Azure AD decrypts hello Kerberos ticket, which includes hello identity of hello user signed into hello corporate device, using hello previously shared key.</span></span>
9. <span data-ttu-id="c5781-132">Después de la evaluación, Azure AD devuelve una aplicación de símbolo (token) toohello atrás o solicita Hola usuario tooperform pruebas adicionales, como la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="c5781-132">After evaluation, Azure AD either returns a token back toohello application or asks hello user tooperform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="c5781-133">Si el inicio de sesión de usuario de hello es correcta, usuario de Hola es tooaccess capaz de aplicación de hello.</span><span class="sxs-lookup"><span data-stu-id="c5781-133">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="c5781-134">Hello siguiente diagrama muestra todos los componentes de Hola y pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="c5781-134">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Inicio de sesión único de conexión directa](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="c5781-136">SSO sin problemas es oportunista, lo que significa que si se produce un error, experiencia de inicio de sesión de hello vuelve comportamiento normal tooits: es decir, Hola su toosign de contraseña en el usuario tiene tooenter.</span><span class="sxs-lookup"><span data-stu-id="c5781-136">Seamless SSO is opportunistic, which means if it fails, hello sign-in experience falls back tooits regular behavior - i.e, hello user needs tooenter their password toosign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5781-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5781-137">Next steps</span></span>

- <span data-ttu-id="c5781-138">[**Inicio rápido**](active-directory-aadconnect-sso-quick-start.md): desarrollo y ejecución de SSO de conexión directa de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5781-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="c5781-139">[**Preguntas más frecuentes** ](active-directory-aadconnect-sso-faq.md) -responde toofrequently preguntas más frecuentes.</span><span class="sxs-lookup"><span data-stu-id="c5781-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="c5781-140">[**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5781-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="c5781-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para la tramitación de solicitudes de nuevas características.</span><span class="sxs-lookup"><span data-stu-id="c5781-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
