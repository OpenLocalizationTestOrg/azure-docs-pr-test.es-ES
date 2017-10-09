---
title: "Azure Active Directory B2C: Página de aterrizaje de directivas personalizadas | Microsoft Docs"
description: Desarrollo de aplicaciones orientadas al consumidor con Azure Active Directory B2C mediante directivas personalizadas
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f2079f53-a637-4f2d-b3a0-61a9647ad433
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 5/06/2017
ms.author: parakhj
ms.openlocfilehash: 28a39f282488b81fc9e2ab7841b5f2cb4cd58715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-up-and-sign-in-consumers-in-your-applications-using-custom-policies"></a><span data-ttu-id="a3a85-103">Azure Active Directory B2C: Registro e inicio de sesión de los consumidores en sus aplicaciones mediante directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="a3a85-103">Azure Active Directory B2C: Sign up and sign in consumers in your applications using custom policies</span></span>
<span data-ttu-id="a3a85-104">Las directivas personalizadas son archivos de configuración que definen el comportamiento de Hola de su inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a3a85-104">Custom policies are configuration files that define hello behavior of your Azure AD B2C tenant.</span></span> <span data-ttu-id="a3a85-105">Se pueden editar totalmente por un toocomplete de desarrollador de identidad un número casi ilimitado de tareas.</span><span class="sxs-lookup"><span data-stu-id="a3a85-105">They can be fully edited by an identity developer toocomplete a near unlimited number of tasks.</span></span>

## <a name="how-tooarticles"></a><span data-ttu-id="a3a85-106">Cómo tooarticles</span><span class="sxs-lookup"><span data-stu-id="a3a85-106">How-tooarticles</span></span>
<span data-ttu-id="a3a85-107">Obtenga información acerca de cómo toouse determinadas características de Azure Active Directory B2C:</span><span class="sxs-lookup"><span data-stu-id="a3a85-107">Learn how toouse specific Azure Active Directory B2C features:</span></span>

* [<span data-ttu-id="a3a85-108">Introducción</span><span class="sxs-lookup"><span data-stu-id="a3a85-108">Get Started</span></span>](active-directory-b2c-overview-custom.md)
* <span data-ttu-id="a3a85-109">Configurar proveedores de OIDC como [Azure AD](active-directory-b2c-setup-aad-custom.md)</span><span class="sxs-lookup"><span data-stu-id="a3a85-109">Configure OIDC Providers such as [Azure AD](active-directory-b2c-setup-aad-custom.md).</span></span>
* <span data-ttu-id="a3a85-110">Configurar proveedores de SAML como [Salesforce](active-directory-b2c-setup-sf-app-custom.md)</span><span class="sxs-lookup"><span data-stu-id="a3a85-110">Configure SAML Providers such as [Salesforce](active-directory-b2c-setup-sf-app-custom.md).</span></span>
* <span data-ttu-id="a3a85-111">Integración de las API de RESTful:</span><span class="sxs-lookup"><span data-stu-id="a3a85-111">Integrate RESTful APIs:</span></span>
    * <span data-ttu-id="a3a85-112">[Obtención de notificaciones adicionales](active-directory-b2c-rest-api-step-custom.md)</span><span class="sxs-lookup"><span data-stu-id="a3a85-112">[Obtain additional claims](active-directory-b2c-rest-api-step-custom.md).</span></span>
    * <span data-ttu-id="a3a85-113">[Validación de entradas de usuario](active-directory-b2c-rest-api-validation-custom.md)</span><span class="sxs-lookup"><span data-stu-id="a3a85-113">[Validate user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>
* <span data-ttu-id="a3a85-114">Personalización del inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="a3a85-114">Customize Login:</span></span>
    * [<span data-ttu-id="a3a85-115">Configuración de entrada de usuario</span><span class="sxs-lookup"><span data-stu-id="a3a85-115">Configure User Input</span></span>](active-directory-b2c-configure-signup-self-asserted-custom.md)
    * [<span data-ttu-id="a3a85-116">Personalización de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="a3a85-116">Customize UI</span></span>](active-directory-b2c-ui-customization-custom.md)
    * [<span data-ttu-id="a3a85-117">Personalización de tokens</span><span class="sxs-lookup"><span data-stu-id="a3a85-117">Customize Token</span></span>](active-directory-b2c-reference-manage-sso-and-token-configuration.md)
* <span data-ttu-id="a3a85-118">Solucionar problemas [recopilando registros con Application Insights](active-directory-b2c-troubleshoot-custom.md)</span><span class="sxs-lookup"><span data-stu-id="a3a85-118">Troubleshoot by [collecting logs using Application Insights](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="whats-new"></a><span data-ttu-id="a3a85-119">Novedades</span><span class="sxs-lookup"><span data-stu-id="a3a85-119">What's new</span></span>
<span data-ttu-id="a3a85-120">Vuelva a comprobar a menudo toolearn sobre cambios futuros toohello Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="a3a85-120">Check back here often toolearn about future changes toohello Azure Active Directory B2C.</span></span> <span data-ttu-id="a3a85-121">También enviaremos tweets acerca de las actualizaciones mediante @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="a3a85-121">We'll also tweet about any updates by using @AzureAD.</span></span>



