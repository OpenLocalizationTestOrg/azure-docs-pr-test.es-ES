---
title: "Azure AD Connect: funcionamiento del inicio de sesión único de conexión directa | Microsoft Docs"
description: "En este artículo se describe el funcionamiento de la característica Inicio de sesión único de conexión directa de Azure Active Directory."
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
ms.openlocfilehash: f0bcbdb03fbb70ff91ac3a56974a88eb1b26c245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="16366-104">Inicio de sesión único de conexión directa de Azure Active Directory: información técnica detallada</span><span class="sxs-lookup"><span data-stu-id="16366-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="16366-105">En este artículo se proporcionan los detalles técnicos sobre cómo funciona la característica Inicio de sesión único de conexión directa (SSO de conexión directa) de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16366-105">This article gives you technical details into how the Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="16366-106">La característica de SSO de conexión directa está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="16366-106">The Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="16366-107">¿Cómo funciona SSO de conexión directa?</span><span class="sxs-lookup"><span data-stu-id="16366-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="16366-108">Esta sección tiene dos partes:</span><span class="sxs-lookup"><span data-stu-id="16366-108">This section has two parts to it:</span></span>
1. <span data-ttu-id="16366-109">La configuración de la característica SSO de conexión directa.</span><span class="sxs-lookup"><span data-stu-id="16366-109">The setup of the Seamless SSO feature.</span></span>
2. <span data-ttu-id="16366-110">Funcionamiento de una transacción de inicio de sesión de usuario único con SSO de conexión directa.</span><span class="sxs-lookup"><span data-stu-id="16366-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="16366-111">¿Cómo funciona la configuración?</span><span class="sxs-lookup"><span data-stu-id="16366-111">How does set up work?</span></span>

<span data-ttu-id="16366-112">SSO de conexión directa se habilita a través de Azure AD Connect tal como se muestra [aquí](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="16366-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="16366-113">Cuando se habilita la característica, se producen los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="16366-113">While enabling the feature, the following steps occur:</span></span>
- <span data-ttu-id="16366-114">Una cuenta de equipo denominada `AZUREADSSOACCT` (que representa a Azure AD) se crea en la instancia local de Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="16366-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="16366-115">La clave de descifrado de Kerberos de la cuenta de equipo se comparte de manera segura con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16366-115">The computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="16366-116">Además, se crean dos nombres de entidad de seguridad de servicio (SPN) de Kerberos que representan las dos direcciones URL que se usan en el inicio de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16366-116">In addition, two Kerberos service principal names (SPNs) are created to represent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="16366-117">La cuenta de equipo y los SPN de Kerberos se crean en cada bosque de AD que sincronice con Azure AD (a través de Azure AD Connect) y para cuyos usuarios desee SSO de conexión directa.</span><span class="sxs-lookup"><span data-stu-id="16366-117">The computer account and the Kerberos SPNs are created in each AD forest you synchronize to Azure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="16366-118">Migre la cuenta de equipo `AZUREADSSOACCT` a una unidad organizativa (UO) donde se almacenen otras cuentas de equipo para garantizar que se administre de la misma manera y que no se elimine.</span><span class="sxs-lookup"><span data-stu-id="16366-118">Move the `AZUREADSSOACCT` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="16366-119">Se recomienda encarecidamente [sustituir la clave de descifrado de Kerberos](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) de la cuenta de equipo de `AZUREADSSOACCT` al menos cada 30 días.</span><span class="sxs-lookup"><span data-stu-id="16366-119">We highly recommend that you [roll over the Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of the `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="16366-120">¿Cómo funciona el inicio de sesión con SSO de conexión directa?</span><span class="sxs-lookup"><span data-stu-id="16366-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="16366-121">Una vez que se completa la instalación, SSO de conexión directa funcionan del mismo modo que cualquier otro inicio de sesión que usa la autenticación integrada de Windows (IWA).</span><span class="sxs-lookup"><span data-stu-id="16366-121">Once the set-up is complete, Seamless SSO works the same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="16366-122">El flujo es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="16366-122">The flow is as follows:</span></span>

1. <span data-ttu-id="16366-123">El usuario intenta acceder a una aplicación (por ejemplo, Outlook Web App en https://outlook.office365.com/owa/) desde un dispositivo corporativo unido a un dominio dentro de la red corporativa.</span><span class="sxs-lookup"><span data-stu-id="16366-123">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="16366-124">Si el usuario todavía no inicia sesión, se le redirige a la página de inicio de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16366-124">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="16366-125">Si la solicitud de inicio de sesión de Azure AD incluye un parámetro `domain_hint` (que identifica al inquilino, por ejemplo, contoso.onmicrosoft.com) o `login_hint` (que identifica al usuario, por ejemplo, user@contoso.onmicrosoft.com o user@contoso.com) se omite el paso 2.</span><span class="sxs-lookup"><span data-stu-id="16366-125">If the Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying the user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="16366-126">El usuario escribe su nombre de usuario en la página de inicio de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16366-126">The user types in their user name into the Azure AD sign-in page.</span></span>
4. <span data-ttu-id="16366-127">Con JavaScript en segundo plano, Azure AD desafía al explorador, a través de una respuesta 401 No autorizado, a que proporcione un vale de Kerberos.</span><span class="sxs-lookup"><span data-stu-id="16366-127">Using JavaScript in the background, Azure AD challenges the browser, via a 401 Unauthorized response, to provide a Kerberos ticket.</span></span>
5. <span data-ttu-id="16366-128">A su vez, el explorador solicita un vale desde Active Directory para la cuenta de equipo `AZUREADSSOACCT` (que representa a Azure AD).</span><span class="sxs-lookup"><span data-stu-id="16366-128">The browser, in turn, requests a ticket from Active Directory for the `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="16366-129">Active Directory busca la cuenta de equipo y devuelve al explorador un vale Kerberos cifrado con el secreto de la cuenta de equipo.</span><span class="sxs-lookup"><span data-stu-id="16366-129">Active Directory locates the computer account and returns a Kerberos ticket to the browser encrypted with the computer account's secret.</span></span>
7. <span data-ttu-id="16366-130">El explorador reenvía el vale de Kerberos que adquirió desde Active Directory a Azure AD (en una de las [direcciones URL de Azure AD que se agregó previamente a la configuración de la zona de intranet del explorador](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="16366-130">The browser forwards the Kerberos ticket it acquired from Active Directory to Azure AD (on one of the [Azure AD URLs previously added to the browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="16366-131">Azure AD descifra el vale de Kerberos, que incluye la identidad del usuario que inició sesión en el dispositivo corporativo, mediante la clave compartida previamente.</span><span class="sxs-lookup"><span data-stu-id="16366-131">Azure AD decrypts the Kerberos ticket, which includes the identity of the user signed into the corporate device, using the previously shared key.</span></span>
9. <span data-ttu-id="16366-132">Después de la evaluación, Azure AD devuelve un token a la aplicación o le pide al usuario que realice pruebas adicionales, como la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="16366-132">After evaluation, Azure AD either returns a token back to the application or asks the user to perform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="16366-133">Si el inicio de sesión del usuario se realiza correctamente, el usuario puede acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16366-133">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="16366-134">En el diagrama siguiente se ilustran todos los componentes y los pasos implicados.</span><span class="sxs-lookup"><span data-stu-id="16366-134">The following diagram illustrates all the components and the steps involved.</span></span>

![Inicio de sesión único de conexión directa](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="16366-136">SSO de conexión directa es una característica oportunista, lo que significa que, si se genera un error, la experiencia de inicio de sesión se revierte a su comportamiento habitual, es decir, el usuario deberá escribir su contraseña para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="16366-136">Seamless SSO is opportunistic, which means if it fails, the sign-in experience falls back to its regular behavior - i.e, the user needs to enter their password to sign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16366-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16366-137">Next steps</span></span>

- <span data-ttu-id="16366-138">[**Inicio rápido** ](active-directory-aadconnect-sso-quick-start.md): desarrollo y ejecución de SSO de conexión directa de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16366-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="16366-139">[**Preguntas más frecuentes**](active-directory-aadconnect-sso-faq.md): obtenga respuestas a las preguntas más frecuentes.</span><span class="sxs-lookup"><span data-stu-id="16366-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="16366-140">[**Solución de problemas**](active-directory-aadconnect-troubleshoot-sso.md): aprenda a resolver problemas comunes de esta característica.</span><span class="sxs-lookup"><span data-stu-id="16366-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="16366-141">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para la tramitación de solicitudes de nuevas características.</span><span class="sxs-lookup"><span data-stu-id="16366-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
