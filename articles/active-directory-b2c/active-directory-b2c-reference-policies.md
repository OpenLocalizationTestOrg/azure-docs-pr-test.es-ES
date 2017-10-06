---
title: 'Azure Active Directory B2C: directivas integradas | Microsoft Docs'
description: "Un tema de marco de directivas extensible Hola de Azure Active Directory B2C y cómo toocreate diversos tipos de directiva"
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
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="aa0d8-103">Azure Active Directory B2C: directivas integradas</span><span class="sxs-lookup"><span data-stu-id="aa0d8-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="aa0d8-104">marco de directivas extensible Hola de Azure Active Directory (Azure AD) B2C es intensidad de núcleo de hello del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-104">hello extensible policy framework of Azure Active Directory (Azure AD) B2C is hello core strength of hello service.</span></span> <span data-ttu-id="aa0d8-105">Las directivas describen totalmente las experiencias de identidad del consumidor como el registro, el inicio de sesión y la edición de perfil.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="aa0d8-106">Por ejemplo, una directiva de inicio de sesión permite toocontrol comportamientos configurando Hola después de configuración:</span><span class="sxs-lookup"><span data-stu-id="aa0d8-106">For instance, a sign-up policy allows you toocontrol behaviors by configuring hello following settings:</span></span>

* <span data-ttu-id="aa0d8-107">Tipos (cuentas sociales como Facebook) o las cuentas locales, como las direcciones de correo electrónico que los consumidores pueden usar toosign hacia arriba para la aplicación hello de cuenta</span><span class="sxs-lookup"><span data-stu-id="aa0d8-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use toosign up for hello application</span></span>
* <span data-ttu-id="aa0d8-108">Atributos (por ejemplo, nombre, código postal y calzado) toobe recopila de consumidor de Hola durante el inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="aa0d8-108">Attributes (for example, first name, postal code, and shoe size) toobe collected from hello consumer during sign-up</span></span>
* <span data-ttu-id="aa0d8-109">Uso de Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="aa0d8-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="aa0d8-110">Hola apariencia y funcionamiento de todas las páginas de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="aa0d8-110">hello look and feel of all sign-up pages</span></span>
* <span data-ttu-id="aa0d8-111">Información (que se manifiesta como notificaciones en un token) que Hola aplicación recibe cuando finaliza la ejecución de la directiva de Hola</span><span class="sxs-lookup"><span data-stu-id="aa0d8-111">Information (which manifests as claims in a token) that hello application receives when hello policy run finishes</span></span>

<span data-ttu-id="aa0d8-112">Puede crear varias directivas de diferentes tipos en su inquilino y usarlas en sus aplicaciones según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="aa0d8-113">Las directivas se pueden volver a usar en todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-113">Policies can be reused across applications.</span></span> <span data-ttu-id="aa0d8-114">Esta flexibilidad permite a los desarrolladores toodefine y modificar ningún código de tootheir de cambios o las experiencias de identidad de consumidor con mínimo.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-114">This flexibility enables developers toodefine and modify consumer identity experiences with minimal or no changes tootheir code.</span></span>

<span data-ttu-id="aa0d8-115">Las directivas están disponibles para usarlas mediante una interfaz de usuario sencilla.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="aa0d8-116">La aplicación desencadena una directiva mediante una solicitud de autenticación HTTP estándar (pasar un parámetro de directiva de solicitud de saludo) y recibe un token personalizado como respuesta.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in hello request) and receives a customized token as response.</span></span> <span data-ttu-id="aa0d8-117">Por ejemplo, hello única diferencia entre las solicitudes que invocación una directiva de inicio de sesión y las solicitudes que invocación una directiva de inicio de sesión es nombre de la directiva de Hola que se utiliza en el parámetro de cadena de consulta de Hola "p":</span><span class="sxs-lookup"><span data-stu-id="aa0d8-117">For example, hello only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is hello policy name that's used in hello "p" query string parameter:</span></span>

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

<span data-ttu-id="aa0d8-118">Para obtener más información sobre el marco de directivas de hello, consulte [esta entrada de blog sobre Azure AD B2C en hello la movilidad empresarial y el Blog de seguridad](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa0d8-118">For more information about hello policy framework, see [this blog post about Azure AD B2C on hello Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="aa0d8-119">Creación de una directiva de registro o de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="aa0d8-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="aa0d8-120">Esta directiva controla las experiencias de registro y de inicio de sesión del cliente con una sola configuración.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="aa0d8-121">Se ha llevado a los consumidores hacia abajo Hola ruta de acceso correcta (inicio de sesión o inicio de sesión) según el contexto de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-121">Consumers are led down hello right path (sign-up or sign-in) depending on hello context.</span></span> <span data-ttu-id="aa0d8-122">También se describe el contenido de Hola de tokens que van a recibir aplicación hello al inicio de sesión de seguridad correcta o inicios de sesión.  Es un ejemplo de código de directiva de inicio de sesión o inicio de sesión de hello [disponible aquí](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="aa0d8-122">It also describes hello contents of tokens that hello application will receive upon successful sign-ups or sign-ins.  A code sample for hello sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="aa0d8-123">Le recomendamos que use esta directiva en vez de una directiva de registro y una directiva de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="aa0d8-124">Creación de una directiva de registro</span><span class="sxs-lookup"><span data-stu-id="aa0d8-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="aa0d8-125">Uso de una directiva de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="aa0d8-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="aa0d8-126">Creación de una directiva de edición de perfil</span><span class="sxs-lookup"><span data-stu-id="aa0d8-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="aa0d8-127">Crear una directiva de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="aa0d8-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="aa0d8-128">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="aa0d8-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="aa0d8-129">¿Cómo puedo vincular una directiva de inicio de sesión o de registro con una directiva de restablecimiento de contraseña?</span><span class="sxs-lookup"><span data-stu-id="aa0d8-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="aa0d8-130">Cuando se crea una directiva de inicio de sesión o inicio de sesión (con las cuentas locales), verá un **contraseña olvidada?** vínculo en la primera página de Hola de experiencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on hello first page of hello experience.</span></span> <span data-ttu-id="aa0d8-131">Al hacer clic en este vínculo, no se desencadena automáticamente ninguna directiva de restablecimiento de contraseña,</span><span class="sxs-lookup"><span data-stu-id="aa0d8-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="aa0d8-132">Hola en su lugar, el código de error  **`AADB2C90118`**  se devuelve tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-132">Instead, hello error code **`AADB2C90118`** is returned tooyour app.</span></span> <span data-ttu-id="aa0d8-133">La aplicación debe toohandle este código de error mediante la invocación de una directiva de restablecimiento de contraseña específica.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-133">Your app needs toohandle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="aa0d8-134">Para obtener más información, vea un [ejemplo que muestra el enfoque de Hola de vinculación de las directivas](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="aa0d8-134">For more information, see a [sample that demonstrates hello approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="aa0d8-135">¿Debo usar una directiva de inicio de sesión o de registro o una directiva de inicio de sesión y una directiva de registro?</span><span class="sxs-lookup"><span data-stu-id="aa0d8-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="aa0d8-136">Le recomendamos que use una directiva de inicio de sesión o de registro en vez de una directiva de inicio de sesión y una directiva de registro.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="aa0d8-137">Directiva de inicio de sesión o inicio de sesión de Hello tiene más capacidades que la directiva de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-137">hello sign-up or sign-in policy has more capabilities than hello sign-in policy.</span></span> <span data-ttu-id="aa0d8-138">También habilita la personalización de interfaz de usuario de página de toouse y tiene una mejor compatibilidad para la localización.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-138">It also enables you toouse page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="aa0d8-139">Directiva de inicio de sesión de Hola se recomienda si no es necesario toolocalize las directivas, solo necesita las capacidades de personalización secundaria para la personalización de marca y desea contraseña restablecimiento que se crean en ella.</span><span class="sxs-lookup"><span data-stu-id="aa0d8-139">hello sign-in policy is recommended if you don't need toolocalize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa0d8-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aa0d8-140">Next steps</span></span>
* [<span data-ttu-id="aa0d8-141">Configuración de token, sesión e inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="aa0d8-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="aa0d8-142">Deshabilitación de la comprobación de correos electrónicos durante la suscripción de consumidores</span><span class="sxs-lookup"><span data-stu-id="aa0d8-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

