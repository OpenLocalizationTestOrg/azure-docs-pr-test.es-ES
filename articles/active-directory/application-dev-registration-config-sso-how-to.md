---
title: "aaaHow tooconfigure una nueva aplicación de varios inquilinos | Documentos de Microsoft"
description: "¿Cómo tooconfigure inicio de sesión único para una aplicación personalizada desarrolla y registrar con Azure AD."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a><span data-ttu-id="b7de9-103">¿Cómo tooconfigure una nueva aplicación de varios inquilinos</span><span class="sxs-lookup"><span data-stu-id="b7de9-103">How tooconfigure a new multi-tenant application</span></span>

<span data-ttu-id="b7de9-104">El inicio de sesión único federado (SSO) de la aplicación se habilita automáticamente cuando la federación se realiza a través de Azure AD para OpenID Connect, SAML 2.0, o WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="b7de9-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="b7de9-105">Si los usuarios finales tienen toosign a pesar de que ya cuentan con una sesión existente con Azure AD, es probable que la aplicación que esté mal configurada.</span><span class="sxs-lookup"><span data-stu-id="b7de9-105">If your end users are having toosign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="b7de9-106">Si usa AAL/MSAL, asegúrese de que tiene **PromptBehavior** establecido demasiado**automática** en lugar de **siempre**.</span><span class="sxs-lookup"><span data-stu-id="b7de9-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set too**Auto** rather than **Always**.</span></span>

* <span data-ttu-id="b7de9-107">Si va a compilar una aplicación móvil, debe configuraciones adicionales tooenable asíncrona o SSO no es asíncrona.</span><span class="sxs-lookup"><span data-stu-id="b7de9-107">If you’re building a mobile app, you may need additional configurations tooenable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="b7de9-108">En el caso de Android, consulte [Habilitación de SSO entre aplicaciones en Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="b7de9-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="b7de9-109">En el caso de iOS, consulte [Habilitación del inicio de sesión único entre aplicaciones en iOS ](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="b7de9-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7de9-110">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b7de9-110">Next steps</span></span>

[<span data-ttu-id="b7de9-111">SSO en Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7de9-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="b7de9-112">Habilitación de SSO entre aplicaciones en Android</span><span class="sxs-lookup"><span data-stu-id="b7de9-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="b7de9-113">Habilitación del inicio de sesión único entre aplicaciones en iOS</span><span class="sxs-lookup"><span data-stu-id="b7de9-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="b7de9-114">Integración de aplicaciones tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="b7de9-114">Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="b7de9-115">Consentimiento y permisos para las aplicaciones convergentes v2.0 de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7de9-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="b7de9-116">Azure AD en StackOverflow</span><span class="sxs-lookup"><span data-stu-id="b7de9-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
