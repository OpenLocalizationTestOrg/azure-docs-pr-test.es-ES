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
ms.openlocfilehash: d34ccd40082edbe036d963ad548bff648119bdd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="9e97b-105">Autenticación de paso a través de Azure Active Directory: información técnica detallada</span><span class="sxs-lookup"><span data-stu-id="9e97b-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="9e97b-106">La autenticación de paso a través de Azure AD se encuentra actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="9e97b-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="9e97b-107">Funcionamiento de la autenticación de paso a través de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e97b-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="9e97b-108">Cuando un usuario intenta iniciar sesión en una aplicación protegida mediante Azure Active Directory (Azure AD), y si la autenticación de paso a través está habilitada en el inquilino, se producen los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9e97b-108">When a user attempts to sign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on the tenant, the following steps occur:</span></span>

1. <span data-ttu-id="9e97b-109">El usuario intenta acceder a una aplicación (por ejemplo, Outlook Web App en https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="9e97b-109">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="9e97b-110">Si el usuario todavía no inicia sesión, se le redirige a la página de inicio de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e97b-110">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>
3. <span data-ttu-id="9e97b-111">El usuario escribe su nombre de usuario y contraseña en la página de inicio de sesión de Azure AD y hace clic en el botón "Iniciar sesión".</span><span class="sxs-lookup"><span data-stu-id="9e97b-111">The user enters their username and password into the Azure AD sign-in page and clicks the "Sign in" button.</span></span>
4. <span data-ttu-id="9e97b-112">Cuando Azure AD recibe la solicitud de inicio de sesión, pone el nombre de usuario y la contraseña (cifrada mediante una clave pública) en una cola.</span><span class="sxs-lookup"><span data-stu-id="9e97b-112">Azure AD, on receiving the sign-in request, places the username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="9e97b-113">Un agente de autenticación de paso a través local hace una llamada saliente a la cola y recupera el nombre de usuario y la contraseña cifrada.</span><span class="sxs-lookup"><span data-stu-id="9e97b-113">An on-premises Pass-through Authentication agent makes an outbound call to the queue and retrieves the username and encrypted password.</span></span>
6. <span data-ttu-id="9e97b-114">El agente descifra la contraseña con su clave privada.</span><span class="sxs-lookup"><span data-stu-id="9e97b-114">The agent decrypts the password using its private key.</span></span>
7. <span data-ttu-id="9e97b-115">Después, el agente valida el nombre de usuario y la contraseña en Active Directory mediante las API de Windows (un mecanismo similar al que se usa en Servicios de federación de Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9e97b-115">The agent then validates the username and password against Active Directory using standard Windows APIs (a similar mechanism to what is used by Active Directory Federation Services).</span></span> <span data-ttu-id="9e97b-116">El nombre de usuario puede ser el nombre de usuario predeterminado local (normalmente, `userPrincipalName`) u otro atributo (conocido como `Alternate ID`) configurado en Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9e97b-116">The username can be either the on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="9e97b-117">Luego, el controlador de dominio (DC) de Active Directory local evalúa la solicitud y devuelve la respuesta adecuada (correcto, error, contraseña expirada o bloqueo de usuario) al agente</span><span class="sxs-lookup"><span data-stu-id="9e97b-117">The on-premises Active Directory Domain Controller (DC) then evaluates the request and returns the appropriate response (success, failure, password expired or user locked out) to the agent.</span></span>
9. <span data-ttu-id="9e97b-118">que, a su vez, la devuelve a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e97b-118">The agent, in turn, returns this response back to Azure AD.</span></span>
10. <span data-ttu-id="9e97b-119">Azure AD evalúa la respuesta y responde al usuario según corresponda, por ejemplo, inicia la sesión del usuario de inmediato o solicita la autenticación multifactor (MFA).</span><span class="sxs-lookup"><span data-stu-id="9e97b-119">Azure AD evaluates the response and responds to the user as appropriate - for example, it either signs the user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="9e97b-120">Si el inicio de sesión del usuario se realiza correctamente, el usuario puede acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9e97b-120">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="9e97b-121">En el diagrama siguiente se ilustran todos los componentes y los pasos implicados.</span><span class="sxs-lookup"><span data-stu-id="9e97b-121">The following diagram illustrates all the components and the steps involved.</span></span>

![Autenticación de paso a través](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="9e97b-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9e97b-123">Next steps</span></span>
- <span data-ttu-id="9e97b-124">[**Limitaciones actuales**](active-directory-aadconnect-pass-through-authentication-current-limitations.md): esta funcionalidad actualmente está en su versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="9e97b-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="9e97b-125">Obtenga información acerca de qué escenarios se admiten y cuáles no.</span><span class="sxs-lookup"><span data-stu-id="9e97b-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="9e97b-126">[**Inicio rápido** ](active-directory-aadconnect-pass-through-authentication-quick-start.md): desarrollo y ejecución de la autenticación de paso a través de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e97b-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="9e97b-127">[**Preguntas más frecuentes**](active-directory-aadconnect-pass-through-authentication-faq.md): obtenga respuestas a las preguntas más frecuentes.</span><span class="sxs-lookup"><span data-stu-id="9e97b-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="9e97b-128">[**Solución de problemas**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md): aprenda a resolver problemas comunes de esta característica.</span><span class="sxs-lookup"><span data-stu-id="9e97b-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="9e97b-129">[**SSO de conexión directa de Azure AD**](active-directory-aadconnect-sso.md): obtenga más información sobre esta característica complementaria.</span><span class="sxs-lookup"><span data-stu-id="9e97b-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="9e97b-130">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para rellenar solicitudes de características nuevas.</span><span class="sxs-lookup"><span data-stu-id="9e97b-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
