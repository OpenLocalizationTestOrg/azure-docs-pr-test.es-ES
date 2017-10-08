---
title: "Azure AD Connect: funcionamiento de la autenticación de paso a través | Microsoft Docs"
description: "En este artículo se describe el funcionamiento de la autenticación de paso a través de Azure Active Directory."
services: active-directory
keywords: "Autenticación de paso a través de Azure AD Connect, instalación de Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="a9405-105">Autenticación de paso a través de Azure Active Directory: información técnica detallada</span><span class="sxs-lookup"><span data-stu-id="a9405-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="a9405-106">La autenticación de paso a través de Azure AD se encuentra actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="a9405-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="a9405-107">Funcionamiento de la autenticación de paso a través de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9405-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="a9405-108">Cuando un usuario intenta toosign en una aplicación protegida por Azure Active Directory (Azure AD) y si está habilitada la autenticación de paso a través en el inquilino de hello, Hola se producen los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a9405-108">When a user attempts toosign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on hello tenant, hello following steps occur:</span></span>

1. <span data-ttu-id="a9405-109">usuario de Hello intente tooaccess una aplicación (por ejemplo, Hola Outlook Web App - https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="a9405-109">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="a9405-110">Si el usuario de hello no ha iniciado ya sesión, usuario de hello es página de inicio de sesión de Azure AD de toohello redirigida.</span><span class="sxs-lookup"><span data-stu-id="a9405-110">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>
3. <span data-ttu-id="a9405-111">usuario de Hello entra en su nombre de usuario y contraseña en la página de inicio de sesión de Azure AD de Hola y hace clic en el botón de "Iniciar sesión" Hola.</span><span class="sxs-lookup"><span data-stu-id="a9405-111">hello user enters their username and password into hello Azure AD sign-in page and clicks hello "Sign in" button.</span></span>
4. <span data-ttu-id="a9405-112">Azure AD, al recibir la solicitud de inicio de sesión hello, coloca Hola nombre de usuario y contraseña (cifrada con una clave pública) en una cola.</span><span class="sxs-lookup"><span data-stu-id="a9405-112">Azure AD, on receiving hello sign-in request, places hello username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="a9405-113">Un agente de autenticación de paso a través de local hace que una cola de toohello llamada saliente y recupera el nombre de usuario de hello y una contraseña cifrada.</span><span class="sxs-lookup"><span data-stu-id="a9405-113">An on-premises Pass-through Authentication agent makes an outbound call toohello queue and retrieves hello username and encrypted password.</span></span>
6. <span data-ttu-id="a9405-114">agente de Hello descifra contraseña Hola usando su clave privada.</span><span class="sxs-lookup"><span data-stu-id="a9405-114">hello agent decrypts hello password using its private key.</span></span>
7. <span data-ttu-id="a9405-115">agente de Hello, a continuación, valida Hola username y password con Active Directory mediante la API estándar de Windows (un toowhat mecanismo similar es utilizado por los servicios de federación de Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a9405-115">hello agent then validates hello username and password against Active Directory using standard Windows APIs (a similar mechanism toowhat is used by Active Directory Federation Services).</span></span> <span data-ttu-id="a9405-116">Hello nombre de usuario puede ser cualquier nombre de usuario de hello local predeterminado (normalmente `userPrincipalName`) o de otro atributo configurado en Azure AD Connect (conocido como `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="a9405-116">hello username can be either hello on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="a9405-117">Hola controlador de dominio de Active Directory (DC) local, a continuación, evalúa la solicitud de Hola y devuelve Hola respuesta adecuada (correcto, error, contraseña expirada o usuario bloqueado) toohello agente.</span><span class="sxs-lookup"><span data-stu-id="a9405-117">hello on-premises Active Directory Domain Controller (DC) then evaluates hello request and returns hello appropriate response (success, failure, password expired or user locked out) toohello agent.</span></span>
9. <span data-ttu-id="a9405-118">agente de Hello, a su vez, devuelve este tooAzure de espera de respuesta AD.</span><span class="sxs-lookup"><span data-stu-id="a9405-118">hello agent, in turn, returns this response back tooAzure AD.</span></span>
10. <span data-ttu-id="a9405-119">Azure AD se evalúa como respuesta de Hola y responde toohello usuario según corresponda; por ejemplo, inicia el usuario de hello inmediatamente o las solicitudes para la autenticación multifactor (MFA).</span><span class="sxs-lookup"><span data-stu-id="a9405-119">Azure AD evaluates hello response and responds toohello user as appropriate - for example, it either signs hello user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="a9405-120">Si el inicio de sesión de usuario de hello es correcta, usuario de Hola es tooaccess capaz de aplicación de hello.</span><span class="sxs-lookup"><span data-stu-id="a9405-120">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="a9405-121">Hello siguiente diagrama muestra todos los componentes de Hola y pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="a9405-121">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Autenticación de paso a través](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="a9405-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9405-123">Next steps</span></span>
- <span data-ttu-id="a9405-124">[**Limitaciones actuales**](active-directory-aadconnect-pass-through-authentication-current-limitations.md): esta funcionalidad actualmente está en su versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="a9405-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="a9405-125">Obtenga información acerca de qué escenarios se admiten y cuáles no.</span><span class="sxs-lookup"><span data-stu-id="a9405-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="a9405-126">[**Inicio rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md): desarrollo y ejecución de la autenticación de paso a través de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9405-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="a9405-127">[**Preguntas más frecuentes** ](active-directory-aadconnect-pass-through-authentication-faq.md) -responde toofrequently preguntas más frecuentes.</span><span class="sxs-lookup"><span data-stu-id="a9405-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="a9405-128">[**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9405-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="a9405-129">[**SSO de conexión directa de Azure AD**](active-directory-aadconnect-sso.md): obtenga más información sobre esta característica complementaria.</span><span class="sxs-lookup"><span data-stu-id="a9405-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="a9405-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para rellenar solicitudes de características nuevas.</span><span class="sxs-lookup"><span data-stu-id="a9405-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
