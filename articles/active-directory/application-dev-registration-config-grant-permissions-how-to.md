---
title: aaaHow toogrant permisos tooa desarrollados de forma personalizada de aplicaciones | Documentos de Microsoft
description: "¿Cómo toogrant permisos tooyour aplicaciones personalizadas mediante Hola portal de Azure AD o un parámetro de dirección URL"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a><span data-ttu-id="8bbfd-103">¿Cómo toogrant permisos tooa desarrollados de forma personalizada aplicación</span><span class="sxs-lookup"><span data-stu-id="8bbfd-103">How toogrant permissions tooa custom-developed application</span></span>

<span data-ttu-id="8bbfd-104">Si desea toogrant consentimiento de forma preferente en la aplicación o se ejecuta en un error que no ha dado su consentimiento tooan aplicación, pruebe lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="8bbfd-104">If you want toogrant consent preemptively on your app or are running into an error that you have not consented tooan app, try these steps below.</span></span>

## <a name="how-tooperform-admin-consent-for-your-application"></a><span data-ttu-id="8bbfd-105">¿Cómo tooperform consentimiento del Administrador de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8bbfd-105">How tooperform Admin Consent for your application</span></span>

<span data-ttu-id="8bbfd-106">Esto tiene el efecto de hello de la concesión de consentimiento toohello aplicación para todos los usuarios de su organización.</span><span class="sxs-lookup"><span data-stu-id="8bbfd-106">This has hello effect of granting consent toohello application for all users in your organization.</span></span>

1. <span data-ttu-id="8bbfd-107">Navegue toohello **registros de aplicaciones** hoja como una **administrador global**, a continuación, seleccione aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8bbfd-107">Navigate toohello **App Registrations** blade as a **global administrator**, then select hello app.</span></span>

2. <span data-ttu-id="8bbfd-108">Seleccione **permisos necesarios**y por último, pulse hello **conceder permisos** situado en la parte superior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="8bbfd-108">Select **Required Permissions**, and finally hit hello **Grant Permissions** button at hello top of hello blade.</span></span>

<span data-ttu-id="8bbfd-109">Como alternativa, puede construir una solicitud demasiado*login.microsoftonline.com* con sus configuraciones de aplicación y anexar en *& prompt = admin\_consentimiento*.</span><span class="sxs-lookup"><span data-stu-id="8bbfd-109">Alternatively, you can construct a request too*login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="8bbfd-110">Después de iniciar sesión con credenciales de administrador, aplicación hello ha concedido consentimiento para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8bbfd-110">After signing in with admin credentials, hello app has been granted consent for all users.</span></span>

## <a name="how-tooforce-user-consent-for-your-application"></a><span data-ttu-id="8bbfd-111">¿Cómo tooforce usuario dar su consentimiento para la aplicación</span><span class="sxs-lookup"><span data-stu-id="8bbfd-111">How tooforce User Consent for your application</span></span>

* <span data-ttu-id="8bbfd-112">Anexar a las solicitudes de autenticación *& prompt = consentimiento* que requiere que los usuarios finales tooconsent cada vez que se autentiquen.</span><span class="sxs-lookup"><span data-stu-id="8bbfd-112">Append onto auth requests *&prompt=consent* which require end users tooconsent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bbfd-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8bbfd-113">Next steps</span></span>

[<span data-ttu-id="8bbfd-114">Integración de aplicaciones y consentimiento tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="8bbfd-114">Consent and Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="8bbfd-115">Consentimiento y permisos para las aplicaciones convergentes v2.0 de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bbfd-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="8bbfd-116">Azure AD en StackOverflow</span><span class="sxs-lookup"><span data-stu-id="8bbfd-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
