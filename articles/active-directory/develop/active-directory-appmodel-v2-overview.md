---
title: "Punto de conexión v2.0 de Azure Active Directory | Documentos de Microsoft"
description: "Introducción a la creación de aplicaciones con inicio de sesión de cuentas de Microsoft y de Azure Active Directory."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1e286044fb1a1b367fcac2dc14c47f68d5ed120d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="b0ceb-103">Inicio de sesión de usuarios de cuentas de Microsoft y de Azure AD en una sola aplicación</span><span class="sxs-lookup"><span data-stu-id="b0ceb-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="b0ceb-104">Antes, un desarrollador de aplicaciones que deseara admitir cuentas de Microsoft personales y profesionales de Azure Active Directory debía realizar la integración con dos sistemas independientes.</span><span class="sxs-lookup"><span data-stu-id="b0ceb-104">In the past, an app developer who wanted to support both personal Microsoft accounts and work accounts from Azure Active Directory was required to integrate with two separate systems.</span></span>  <span data-ttu-id="b0ceb-105">El **punto de conexión v2.0 de Azure AD** incorpora una nueva versión de API de autenticación que le permite iniciar sesión con ambos tipos de cuentas mediante una sencilla integración.</span><span class="sxs-lookup"><span data-stu-id="b0ceb-105">The **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you to sign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="b0ceb-106">Las aplicaciones que usan el punto de conexión v2.0 también pueden usar las API de REST de [Microsoft Graph](https://graph.microsoft.io) con cualquier tipo de cuenta.</span><span class="sxs-lookup"><span data-stu-id="b0ceb-106">Apps that use the v2.0 endpoint can also consume REST APIs from the [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b0ceb-107">Introducción</span><span class="sxs-lookup"><span data-stu-id="b0ceb-107">Getting Started</span></span>
<span data-ttu-id="b0ceb-108">Elija su plataforma favorita de la lista siguiente para compilar una aplicación mediante nuestros marcos y bibliotecas de código abierto.</span><span class="sxs-lookup"><span data-stu-id="b0ceb-108">Choose your favorite platform from the following list to build an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="b0ceb-109">Como alternativa, puede usar la documentación del protocolo OAuth 2.0 y OpenID Connect para enviar y recibir directamente mensajes de protocolo sin usar una biblioteca de autenticación.</span><span class="sxs-lookup"><span data-stu-id="b0ceb-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation to send & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="b0ceb-110">Novedades</span><span class="sxs-lookup"><span data-stu-id="b0ceb-110">What's New</span></span>
<span data-ttu-id="b0ceb-111">La información que se describe aquí será útil para comprender qué se puede y no se puede hacer con el punto de conexión v2.0.</span><span class="sxs-lookup"><span data-stu-id="b0ceb-111">The information here will be useful in understanding what is & what isn't possible with the v2.0 endpoint.</span></span>

* <span data-ttu-id="b0ceb-112">Obtenga información sobre los [tipos de aplicaciones que puede compilar con la versión 2.0 del punto de conexión](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="b0ceb-112">Learn about the [types of apps you can build with the v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="b0ceb-113">Conozca las [limitaciones y restricciones](active-directory-v2-limitations.md) de la versión 2.0 del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="b0ceb-113">Understand the [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with the v2.0 endpoint.</span></span>
* <span data-ttu-id="b0ceb-114">Eche un vistazo a este vídeo introductorio del punto de conexión v2.0:</span><span class="sxs-lookup"><span data-stu-id="b0ceb-114">Check out this overview video for the v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="b0ceb-115">Referencia</span><span class="sxs-lookup"><span data-stu-id="b0ceb-115">Reference</span></span>
<span data-ttu-id="b0ceb-116">Estos vínculos le servirán para explorar la plataforma en profundidad:</span><span class="sxs-lookup"><span data-stu-id="b0ceb-116">These links will be useful for exploring the platform in depth:</span></span>

* [<span data-ttu-id="b0ceb-117">Referencia de protocolos de v2.0</span><span class="sxs-lookup"><span data-stu-id="b0ceb-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="b0ceb-118">Referencia de los tokens de v2.0</span><span class="sxs-lookup"><span data-stu-id="b0ceb-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="b0ceb-119">Referencia de la biblioteca de la versión 2.0</span><span class="sxs-lookup"><span data-stu-id="b0ceb-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="b0ceb-120">Ámbitos y consentimiento en el punto de conexión v2.0</span><span class="sxs-lookup"><span data-stu-id="b0ceb-120">Scopes and Consent in the v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="b0ceb-121">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="b0ceb-121">The Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="b0ceb-122">Ayuda y soporte técnico</span><span class="sxs-lookup"><span data-stu-id="b0ceb-122">Help & Support</span></span>
<span data-ttu-id="b0ceb-123">Estos son los mejores lugares para obtener ayuda con el desarrollo en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b0ceb-123">These are the best places to get help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="b0ceb-124">`azure-active-directory` de Stack Overflow y etiquetas `adal`</span><span class="sxs-lookup"><span data-stu-id="b0ceb-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="b0ceb-125">Comentarios sobre Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0ceb-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="b0ceb-126">Si solo tiene que iniciar sesión en cuentas profesionales o educativas de Azure Active Directory, debería comenzar con nuestra [Guía del desarrollador de Azure AD](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b0ceb-126">If you only need to sign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="b0ceb-127">El punto de conexión v2.0 está diseñado para que lo usen desarrolladores que deban iniciar sesión explícitamente en cuentas personales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b0ceb-127">The v2.0 endpoint is intended for use by developers who explicitly need to sign in Microsoft personal accounts.</span></span>

