---
title: "Autenticación de paso a través de Azure AD: limitaciones actuales | Microsoft Docs"
description: "En este artículo se describen las limitaciones actuales de la autenticación de paso a través de Azure Active Directory (Azure AD)."
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
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 37c0ea094d02208f2516a4a040f75894e046c670
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="9d34c-104">Autenticación de paso a través de Azure Active Directory: limitaciones actuales</span><span class="sxs-lookup"><span data-stu-id="9d34c-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="9d34c-105">La autenticación de paso a través de Azure AD se encuentra actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="9d34c-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="9d34c-106">Es una característica gratuita y no es necesario usar ninguna versión de pago de Azure AD para usarla.</span><span class="sxs-lookup"><span data-stu-id="9d34c-106">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="9d34c-107">La autenticación de paso a través solo está disponible en la instancia mundial de Azure AD y no en [Microsoft Cloud Alemania](http://www.microsoft.de/cloud-deutschland) ni en [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="9d34c-107">Pass-through Authentication is only available in the world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="9d34c-108">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="9d34c-108">Supported scenarios</span></span>

<span data-ttu-id="9d34c-109">Los siguientes escenarios son totalmente compatibles durante la versión preliminar:</span><span class="sxs-lookup"><span data-stu-id="9d34c-109">The following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="9d34c-110">Inicios de sesión de usuario en todas las aplicaciones basadas en explorador web.</span><span class="sxs-lookup"><span data-stu-id="9d34c-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="9d34c-111">Inicios de sesión de usuario en las aplicaciones cliente de Office 365 que admitan la [autenticación moderna](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="9d34c-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="9d34c-112">Azure AD Join para dispositivos con Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9d34c-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="9d34c-113">Compatibilidad con Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="9d34c-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="9d34c-114">Escenarios no admitidos</span><span class="sxs-lookup"><span data-stu-id="9d34c-114">Unsupported scenarios</span></span>

<span data-ttu-id="9d34c-115">En la versión preliminar, los siguientes escenarios _no_ se admiten:</span><span class="sxs-lookup"><span data-stu-id="9d34c-115">The following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="9d34c-116">Inicios de sesión de usuarios en aplicaciones cliente de Office heredadas (Office 2013 o versiones anteriores).</span><span class="sxs-lookup"><span data-stu-id="9d34c-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="9d34c-117">Se recomienda a las organizaciones que cambien a la autenticación moderna, en caso de que sea posible.</span><span class="sxs-lookup"><span data-stu-id="9d34c-117">Organizations are encouraged to switch to modern authentication, if possible.</span></span> <span data-ttu-id="9d34c-118">La autenticación moderna permite la compatibilidad de la autenticación de paso a través, pero también le ayuda a proteger sus cuentas de usuario mediante características de [acceso condicional](../active-directory-conditional-access.md) como Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="9d34c-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="9d34c-119">Inicios de sesión de usuarios en aplicaciones cliente de Skype Empresarial, incluido Skype Empresarial 2016.</span><span class="sxs-lookup"><span data-stu-id="9d34c-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="9d34c-120">Inicios de sesión de usuario en PowerShell v1.0.</span><span class="sxs-lookup"><span data-stu-id="9d34c-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="9d34c-121">Se recomienda que use PowerShell v2.0 en su lugar.</span><span class="sxs-lookup"><span data-stu-id="9d34c-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="9d34c-122">Como solución alternativa para escenarios no admitidos, habilite la sincronización de hash de contraseñas en la página [Características opcionales](active-directory-aadconnect-get-started-custom.md#optional-features) del asistente de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9d34c-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on the [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in the Azure AD Connect wizard.</span></span> <span data-ttu-id="9d34c-123">La sincronización de hash de contraseñas _solo_ actúa como reserva en los escenarios anteriores (y _no_ como reserva genérica en la autenticación de paso a través).</span><span class="sxs-lookup"><span data-stu-id="9d34c-123">Password Hash Synchronization acts as a fallback for the preceding scenarios _only_ (and _not_ as a generic fallback to Pass-through Authentication).</span></span> <span data-ttu-id="9d34c-124">Si no necesita estos escenarios, desactive la sincronización hash de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="9d34c-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d34c-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d34c-125">Next steps</span></span>
- <span data-ttu-id="9d34c-126">[**Inicio rápido** ](active-directory-aadconnect-pass-through-authentication-quick-start.md): desarrollo y ejecución de la autenticación de paso a través de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d34c-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="9d34c-127">[**Profundización técnica** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md): descripción del funcionamiento de esta característica.</span><span class="sxs-lookup"><span data-stu-id="9d34c-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="9d34c-128">[**Preguntas más frecuentes**](active-directory-aadconnect-pass-through-authentication-faq.md): obtenga respuestas a las preguntas más frecuentes.</span><span class="sxs-lookup"><span data-stu-id="9d34c-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="9d34c-129">[**Solución de problemas**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md): aprenda a resolver problemas comunes de esta característica.</span><span class="sxs-lookup"><span data-stu-id="9d34c-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="9d34c-130">[**SSO de conexión directa de Azure AD**](active-directory-aadconnect-sso.md): obtenga más información sobre esta característica complementaria.</span><span class="sxs-lookup"><span data-stu-id="9d34c-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="9d34c-131">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para rellenar solicitudes de características nuevas.</span><span class="sxs-lookup"><span data-stu-id="9d34c-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
