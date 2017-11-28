---
title: extremo de v2.0 de Active Directory aaaAzure | Documentos de Microsoft
description: "Una introducción toobuilding las aplicaciones con Microsoft Account y Azure Active Directory inicio de sesión."
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
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="bca82-103">Inicio de sesión de usuarios de cuentas de Microsoft y de Azure AD en una sola aplicación</span><span class="sxs-lookup"><span data-stu-id="bca82-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="bca82-104">Hola más allá, un desarrollador de aplicaciones que deseaban toosupport ambas cuentas de Microsoft personales y cuentas para el trabajo de Azure Active Directory era necesario toointegrate con dos sistemas independientes.</span><span class="sxs-lookup"><span data-stu-id="bca82-104">In hello past, an app developer who wanted toosupport both personal Microsoft accounts and work accounts from Azure Active Directory was required toointegrate with two separate systems.</span></span>  <span data-ttu-id="bca82-105">Hola **punto de conexión de Azure AD v2.0** presenta una nueva versión de API de autenticación que permite toosign en ambos tipos de cuentas mediante una integración sencilla.</span><span class="sxs-lookup"><span data-stu-id="bca82-105">hello **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you toosign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="bca82-106">Aplicaciones que usan el punto de conexión de hello v2.0 también pueden usar las API de REST de hello [Microsoft Graph](https://graph.microsoft.io) con cualquier tipo de cuenta.</span><span class="sxs-lookup"><span data-stu-id="bca82-106">Apps that use hello v2.0 endpoint can also consume REST APIs from hello [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="bca82-107">Introducción</span><span class="sxs-lookup"><span data-stu-id="bca82-107">Getting Started</span></span>
<span data-ttu-id="bca82-108">Elija la plataforma favoritos de hello sigue lista toobuild una aplicación con nuestras bibliotecas de código abierto y marcos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bca82-108">Choose your favorite platform from hello following list toobuild an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="bca82-109">Como alternativa, puede usar nuestro toosend de documentación del protocolo OAuth 2.0 y OpenID Connect y recibir mensajes de protocolo directamente sin utilizar una biblioteca de autenticación.</span><span class="sxs-lookup"><span data-stu-id="bca82-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation toosend & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="bca82-110">Novedades</span><span class="sxs-lookup"><span data-stu-id="bca82-110">What's New</span></span>
<span data-ttu-id="bca82-111">información de Hello aquí será útil para entender qué es & lo que no es posible con el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="bca82-111">hello information here will be useful in understanding what is & what isn't possible with hello v2.0 endpoint.</span></span>

* <span data-ttu-id="bca82-112">Obtenga información acerca de hello [tipos de aplicaciones puede crear con el punto de conexión de hello v2.0](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="bca82-112">Learn about hello [types of apps you can build with hello v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="bca82-113">Comprender hello [limitaciones y restricciones, las restricciones](active-directory-v2-limitations.md) con el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="bca82-113">Understand hello [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with hello v2.0 endpoint.</span></span>
* <span data-ttu-id="bca82-114">Este vídeo para el punto de conexión de hello v2.0 de información general, consulte:</span><span class="sxs-lookup"><span data-stu-id="bca82-114">Check out this overview video for hello v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="bca82-115">Referencia</span><span class="sxs-lookup"><span data-stu-id="bca82-115">Reference</span></span>
<span data-ttu-id="bca82-116">Estos vínculos le servirán para explorar la plataforma de hello en profundidad:</span><span class="sxs-lookup"><span data-stu-id="bca82-116">These links will be useful for exploring hello platform in depth:</span></span>

* [<span data-ttu-id="bca82-117">Referencia de protocolos de v2.0</span><span class="sxs-lookup"><span data-stu-id="bca82-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="bca82-118">Referencia de los tokens de v2.0</span><span class="sxs-lookup"><span data-stu-id="bca82-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="bca82-119">Referencia de la biblioteca de la versión 2.0</span><span class="sxs-lookup"><span data-stu-id="bca82-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="bca82-120">Ámbitos y consentimiento en el punto de conexión de hello v2.0</span><span class="sxs-lookup"><span data-stu-id="bca82-120">Scopes and Consent in hello v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="bca82-121">Hola Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="bca82-121">hello Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="bca82-122">Ayuda y soporte técnico</span><span class="sxs-lookup"><span data-stu-id="bca82-122">Help & Support</span></span>
<span data-ttu-id="bca82-123">Se trata de hello mejores lugares tooget ayuda con el desarrollo en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bca82-123">These are hello best places tooget help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="bca82-124">`azure-active-directory` de Stack Overflow y etiquetas `adal`</span><span class="sxs-lookup"><span data-stu-id="bca82-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="bca82-125">Comentarios sobre Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bca82-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="bca82-126">Si solo necesita toosign en cuentas profesionales o educativas de Azure Active Directory, debe comenzar con nuestras [Guía del desarrollador de Azure AD](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="bca82-126">If you only need toosign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="bca82-127">el punto de conexión de Hello v2.0 está diseñado para su uso por los desarrolladores que necesiten explícitamente toosign en cuentas personales de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bca82-127">hello v2.0 endpoint is intended for use by developers who explicitly need toosign in Microsoft personal accounts.</span></span>

