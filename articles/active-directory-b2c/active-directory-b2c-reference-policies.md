---
title: 'Azure Active Directory B2C: directivas integradas | Microsoft Docs'
description: "Tema sobre el marco de directiva extensible de Azure Active Directory B2C y sobre cómo crear distintos tipos de directiva"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: daad3af089afdf76b930053728bb11a5cf4c2a92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="bcde9-103">Azure Active Directory B2C: directivas integradas</span><span class="sxs-lookup"><span data-stu-id="bcde9-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="bcde9-104">El marco de directiva extensible de Azure Active Directory (Azure AD) B2C es la fortaleza esencial del servicio.</span><span class="sxs-lookup"><span data-stu-id="bcde9-104">The extensible policy framework of Azure Active Directory (Azure AD) B2C is the core strength of the service.</span></span> <span data-ttu-id="bcde9-105">Las directivas describen totalmente las experiencias de identidad del consumidor como el registro, el inicio de sesión y la edición de perfil.</span><span class="sxs-lookup"><span data-stu-id="bcde9-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="bcde9-106">Por ejemplo, una directiva de registro le permite controlar comportamientos configurando los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="bcde9-106">For instance, a sign-up policy allows you to control behaviors by configuring the following settings:</span></span>

* <span data-ttu-id="bcde9-107">Tipos de cuenta (cuentas sociales como Facebook, o cuentas locales como direcciones de correo electrónico) que los consumidores pueden usar para registrarse en la aplicación</span><span class="sxs-lookup"><span data-stu-id="bcde9-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use to sign up for the application</span></span>
* <span data-ttu-id="bcde9-108">Atributos (por ejemplo, nombre, código postal, número de calzado, etc.) que se recopilarán del consumidor durante el registro</span><span class="sxs-lookup"><span data-stu-id="bcde9-108">Attributes (for example, first name, postal code, and shoe size) to be collected from the consumer during sign-up</span></span>
* <span data-ttu-id="bcde9-109">Uso de Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="bcde9-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="bcde9-110">La apariencia de todas las páginas de registro</span><span class="sxs-lookup"><span data-stu-id="bcde9-110">The look and feel of all sign-up pages</span></span>
* <span data-ttu-id="bcde9-111">Información (que se manifiesta como notificaciones en un token) que recibe la aplicación cuando se completa la ejecución de la directiva.</span><span class="sxs-lookup"><span data-stu-id="bcde9-111">Information (which manifests as claims in a token) that the application receives when the policy run finishes</span></span>

<span data-ttu-id="bcde9-112">Puede crear varias directivas de diferentes tipos en su inquilino y usarlas en sus aplicaciones según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bcde9-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="bcde9-113">Las directivas se pueden volver a usar en todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bcde9-113">Policies can be reused across applications.</span></span> <span data-ttu-id="bcde9-114">Esta flexibilidad permite a los desarrolladores definir y modificar experiencias de identidad de consumidor con cambios mínimos o ningún cambio en su código.</span><span class="sxs-lookup"><span data-stu-id="bcde9-114">This flexibility enables developers to define and modify consumer identity experiences with minimal or no changes to their code.</span></span>

<span data-ttu-id="bcde9-115">Las directivas están disponibles para usarlas mediante una interfaz de usuario sencilla.</span><span class="sxs-lookup"><span data-stu-id="bcde9-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="bcde9-116">Su aplicación desencadena una directiva mediante una solicitud de autenticación HTTP estándar (pasando un parámetro de directiva en la solicitud) y recibe un token personalizado como respuesta.</span><span class="sxs-lookup"><span data-stu-id="bcde9-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in the request) and receives a customized token as response.</span></span> <span data-ttu-id="bcde9-117">Por ejemplo, la única diferencia que hay entre las solicitudes que invocan una directiva de registro y las que invocan una directiva de inicio de sesión es el nombre de la directiva que se usa en el parámetro de cadena de consulta "p":</span><span class="sxs-lookup"><span data-stu-id="bcde9-117">For example, the only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is the policy name that's used in the "p" query string parameter:</span></span>

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

<span data-ttu-id="bcde9-118">Para obtener más información sobre el marco de directivas, consulte [esta entrada de blog sobre Azure AD B2C en el Blog de Enterprise Mobility + Security](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="bcde9-118">For more information about the policy framework, see [this blog post about Azure AD B2C on the Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="bcde9-119">Creación de una directiva de registro o de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="bcde9-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="bcde9-120">Esta directiva controla las experiencias de registro y de inicio de sesión del cliente con una sola configuración.</span><span class="sxs-lookup"><span data-stu-id="bcde9-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="bcde9-121">A los consumidores se les lleva por la ruta correcta (registro o inicio de sesión) según el contexto.</span><span class="sxs-lookup"><span data-stu-id="bcde9-121">Consumers are led down the right path (sign-up or sign-in) depending on the context.</span></span> <span data-ttu-id="bcde9-122">También describe el contenido de los tokens que recibirá la aplicación cuando el registro o el inicio de sesión sean correctos.  [Aquí puede encontrar](active-directory-b2c-devquickstarts-web-dotnet-susi.md)código de ejemplo de la directiva de registro o de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="bcde9-122">It also describes the contents of tokens that the application will receive upon successful sign-ups or sign-ins.  A code sample for the sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="bcde9-123">Le recomendamos que use esta directiva en vez de una directiva de registro y una directiva de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="bcde9-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="bcde9-124">Creación de una directiva de registro</span><span class="sxs-lookup"><span data-stu-id="bcde9-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="bcde9-125">Uso de una directiva de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="bcde9-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="bcde9-126">Creación de una directiva de edición de perfil</span><span class="sxs-lookup"><span data-stu-id="bcde9-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="bcde9-127">Crear una directiva de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="bcde9-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="bcde9-128">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="bcde9-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="bcde9-129">¿Cómo puedo vincular una directiva de inicio de sesión o de registro con una directiva de restablecimiento de contraseña?</span><span class="sxs-lookup"><span data-stu-id="bcde9-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="bcde9-130">Al crear una directiva de inicio de sesión o de registro (con cuentas locales), verá el vínculo **¿Olvidó la contraseña?** en la primera página de la experiencia.</span><span class="sxs-lookup"><span data-stu-id="bcde9-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on the first page of the experience.</span></span> <span data-ttu-id="bcde9-131">Al hacer clic en este vínculo, no se desencadena automáticamente ninguna directiva de restablecimiento de contraseña,</span><span class="sxs-lookup"><span data-stu-id="bcde9-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="bcde9-132">sino que se devuelve a la aplicación el código de error **`AADB2C90118`**.</span><span class="sxs-lookup"><span data-stu-id="bcde9-132">Instead, the error code **`AADB2C90118`** is returned to your app.</span></span> <span data-ttu-id="bcde9-133">La aplicación debe controlar este código de error invocando una directiva de restablecimiento de contraseña específica.</span><span class="sxs-lookup"><span data-stu-id="bcde9-133">Your app needs to handle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="bcde9-134">Para obtener más información, consulte un [ejemplo en el que se muestra el método para vincular directivas](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="bcde9-134">For more information, see a [sample that demonstrates the approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="bcde9-135">¿Debo usar una directiva de inicio de sesión o de registro o una directiva de inicio de sesión y una directiva de registro?</span><span class="sxs-lookup"><span data-stu-id="bcde9-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="bcde9-136">Le recomendamos que use una directiva de inicio de sesión o de registro en vez de una directiva de inicio de sesión y una directiva de registro.</span><span class="sxs-lookup"><span data-stu-id="bcde9-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="bcde9-137">La directiva de inicio de sesión o de registro tiene más capacidades que la directiva de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="bcde9-137">The sign-up or sign-in policy has more capabilities than the sign-in policy.</span></span> <span data-ttu-id="bcde9-138">También le permite usar la personalización de la interfaz de usuario de la página y tiene una mejor compatibilidad con la localización.</span><span class="sxs-lookup"><span data-stu-id="bcde9-138">It also enables you to use page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="bcde9-139">La directiva de inicio de sesión se recomienda si no necesita localizar las directivas, solo necesita unas capacidades de personalización secundarias para la personalización de marca y quiere que el restablecimiento de contraseña esté integrado en ella.</span><span class="sxs-lookup"><span data-stu-id="bcde9-139">The sign-in policy is recommended if you don't need to localize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcde9-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bcde9-140">Next steps</span></span>
* [<span data-ttu-id="bcde9-141">Configuración de token, sesión e inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="bcde9-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="bcde9-142">Deshabilitación de la comprobación de correos electrónicos durante la suscripción de consumidores</span><span class="sxs-lookup"><span data-stu-id="bcde9-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

