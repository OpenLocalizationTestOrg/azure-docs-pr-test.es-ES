---
title: "inicio de sesión en aaaAzure MFA con la verificacion | Documentos de Microsoft"
description: "Esta página le proporcionará instrucciones en donde toogo toosee Hola distintos inicio de sesión métodos disponibles con Azure MFA."
keywords: "autenticación de usuario, experiencia de inicio de sesión, inicio de sesión con el teléfono móvil, inicio de sesión con el teléfono del trabajo"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="cca82-104">experiencia de inicio de sesión de Hello con autenticación multifactor de Azure</span><span class="sxs-lookup"><span data-stu-id="cca82-104">hello sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="cca82-105">Hola de este artículo sirve toowalk a través de una experiencia de inicio de sesión típica.</span><span class="sxs-lookup"><span data-stu-id="cca82-105">hello purpose of this article is toowalk through a typical sign-in experience.</span></span> <span data-ttu-id="cca82-106">Para obtener ayuda con el inicio de sesión o tootroubleshoot problemas, consulte [tenga problemas con la autenticación multifactor Azure](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="cca82-106">For help with signing in, or tootroubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="cca82-107">¿Cómo se presenta la experiencia de inicio de sesión?</span><span class="sxs-lookup"><span data-stu-id="cca82-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="cca82-108">La experiencia de inicio de sesión depende de cuál sea su elección toouse como el segundo factor: una llamada de teléfono, una aplicación de autenticación o textos.</span><span class="sxs-lookup"><span data-stu-id="cca82-108">Your sign-in experience differs depending on what you choose toouse as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="cca82-109">Elija la opción de Hola que mejor describa lo que está haciendo:</span><span class="sxs-lookup"><span data-stu-id="cca82-109">Choose hello option that best describes what you are doing:</span></span>

| <span data-ttu-id="cca82-110">¿Cómo se puede iniciar sesión?</span><span class="sxs-lookup"><span data-stu-id="cca82-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="cca82-111">Con un teléfono móvil o de office del toomy de llamada de teléfono</span><span class="sxs-lookup"><span data-stu-id="cca82-111">With a phone call toomy mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="cca82-112">Con un toomy texto a teléfono móvil</span><span class="sxs-lookup"><span data-stu-id="cca82-112">With a text toomy mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="cca82-113">Con las notificaciones de la aplicación de Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="cca82-113">With notifications from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="cca82-114">Con los códigos de verificación de aplicación de Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="cca82-114">With verification codes from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="cca82-115">Con un método alternativo, ya que ahora no puedo usar mi método preferido</span><span class="sxs-lookup"><span data-stu-id="cca82-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="cca82-116">Inicio de sesión con una llamada de teléfono</span><span class="sxs-lookup"><span data-stu-id="cca82-116">Signing in with a phone call</span></span>
<span data-ttu-id="cca82-117">Hola siguiente información describe hello en dos pasos comprobación experiencia con un tooyour de llamada de teléfono móvil o teléfono del trabajo.</span><span class="sxs-lookup"><span data-stu-id="cca82-117">hello following information describes hello two-step verification experience with a call tooyour mobile or office phone.</span></span>

1. <span data-ttu-id="cca82-118">Inicie sesión en tooan aplicación o servicio, como Office 365 con su nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="cca82-118">Sign in tooan application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="cca82-119">Microsoft lo llamará.</span><span class="sxs-lookup"><span data-stu-id="cca82-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="cca82-120">Responda Hola teléfono y pulse Hola # tecla.</span><span class="sxs-lookup"><span data-stu-id="cca82-120">Answer hello phone and hit hello # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="cca82-121">Inicio de sesión con un mensaje de texto</span><span class="sxs-lookup"><span data-stu-id="cca82-121">Signing in with a text message</span></span>
<span data-ttu-id="cca82-122">Hola siguiente información describe la experiencia de comprobación de dos pasos de hello con un mensaje texto tooyour a teléfono móvil:</span><span class="sxs-lookup"><span data-stu-id="cca82-122">hello following information describes hello two-step verification experience with a text message tooyour mobile phone:</span></span>

1. <span data-ttu-id="cca82-123">Inicie sesión en tooan aplicación o servicio, como Office 365 con su nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="cca82-123">Sign in tooan application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="cca82-124">Microsoft envía un mensaje de texto que contiene un código numérico.</span><span class="sxs-lookup"><span data-stu-id="cca82-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="cca82-125">Escriba el código de hello en cuadro Hola proporcionada en página de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="cca82-125">Enter hello code in hello box provided on hello sign-in page.</span></span> 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="cca82-126">Inicio de sesión con la aplicación de Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="cca82-126">Signing in with hello Microsoft Authenticator app</span></span> 
<span data-ttu-id="cca82-127">Hello siguiente información describe Hola experiencia de usuario de aplicación de Microsoft Authenticator hello para comprobaciones de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="cca82-127">hello following information describes hello experience of using hello Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="cca82-128">Hay dos maneras diferentes toouse Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="cca82-128">There are two different ways toouse hello app.</span></span> <span data-ttu-id="cca82-129">Puede recibir notificaciones de inserción en el dispositivo, o puede abrir Hola aplicación tooget un código de comprobación.</span><span class="sxs-lookup"><span data-stu-id="cca82-129">You can receive push notifications on your device, or you can open hello app tooget a verification code.</span></span>

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a><span data-ttu-id="cca82-130">toosign con una notificación de aplicación de Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="cca82-130">toosign in with a notification from hello Microsoft Authenticator app</span></span>
1. <span data-ttu-id="cca82-131">Inicie sesión en tooan aplicación o servicio, como Office 365 con su nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="cca82-131">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="cca82-132">Microsoft envía una aplicación de Microsoft Authenticator toohello de notificación en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cca82-132">Microsoft sends a notification toohello Microsoft Authenticator app on your device.</span></span>

  ![Microsoft envía una notificación](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="cca82-134">Notificación de hello abierto en su teléfono y seleccione hello **compruebe** clave.</span><span class="sxs-lookup"><span data-stu-id="cca82-134">Open hello notification on your phone and select hello **Verify** key.</span></span> <span data-ttu-id="cca82-135">Si su empresa requiere un PIN, escríbalo aquí.</span><span class="sxs-lookup"><span data-stu-id="cca82-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="cca82-136">Con esto debe haber iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="cca82-136">You should now be signed in.</span></span>

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="cca82-137">toosign sesión utilizando un código de comprobación con la aplicación de Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="cca82-137">toosign in using a verification code with hello Microsoft Authenticator app</span></span>

<span data-ttu-id="cca82-138">Si utiliza códigos de verificación de hello Microsoft Authenticator aplicación tooget, a continuación, cuando se abre la aplicación hello aparece un número en su nombre de cuenta.</span><span class="sxs-lookup"><span data-stu-id="cca82-138">If you use hello Microsoft Authenticator app tooget verification codes, then when you open hello app you see a number under your account name.</span></span> <span data-ttu-id="cca82-139">Este número cambia cada 30 segundos para que no use Hola mismo número dos veces.</span><span class="sxs-lookup"><span data-stu-id="cca82-139">This number changes every 30 seconds so that you don't use hello same number twice.</span></span> <span data-ttu-id="cca82-140">Cuando se le pregunte para un código de comprobación, abra la aplicación hello y usar cualquier número se muestra actualmente.</span><span class="sxs-lookup"><span data-stu-id="cca82-140">When you're asked for a verification code, open hello app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="cca82-141">Inicie sesión en tooan aplicación o servicio, como Office 365 con su nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="cca82-141">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="cca82-142">Microsoft le pedirá un código de verificación.</span><span class="sxs-lookup"><span data-stu-id="cca82-142">Microsoft prompts you for a verification code.</span></span>

  ![Escribir el código de comprobación](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="cca82-144">Abra la aplicación de Microsoft Authenticator hello en el teléfono y escriba el código de hello en donde va a iniciar sesión en el cuadro de Hola.</span><span class="sxs-lookup"><span data-stu-id="cca82-144">Open hello Microsoft Authenticator app on your phone and enter hello code in hello box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="cca82-145">Inicio de sesión con un método alternativo</span><span class="sxs-lookup"><span data-stu-id="cca82-145">Signing in with an alternate method</span></span>
<span data-ttu-id="cca82-146">En ocasiones, no tienes teléfono de Hola o dispositivo que configuró como método de comprobación preferida.</span><span class="sxs-lookup"><span data-stu-id="cca82-146">Sometimes you don't have hello phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="cca82-147">Esta situación es el motivo por el que se recomienda configurar métodos de copia de seguridad para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="cca82-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="cca82-148">Hello siguiente sección muestra cómo toosign con un método alternativo en su método principal podría no estar disponible.</span><span class="sxs-lookup"><span data-stu-id="cca82-148">hello following section shows you how toosign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="cca82-149">Inicie sesión en tooan aplicación o servicio, como Office 365 con su nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="cca82-149">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="cca82-150">Seleccione **Usar otra opción de comprobación**.</span><span class="sxs-lookup"><span data-stu-id="cca82-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="cca82-151">Verá distintas opciones de comprobación en función del número de ellas que haya configurado.</span><span class="sxs-lookup"><span data-stu-id="cca82-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="cca82-152">Elija un método alternativo e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="cca82-152">Choose an alternate method and sign in.</span></span>

  ![Usar método alternativo](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="cca82-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cca82-154">Next steps</span></span>

<span data-ttu-id="cca82-155">Si tiene problemas para iniciar sesión con la verificación en dos pasos, obtenga más información en [Problemas con Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="cca82-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="cca82-156">Obtenga información acerca de cómo demasiado[administrar la configuración de comprobación de dos pasos](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="cca82-156">Learn how too[Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="cca82-157">Obtener información sobre cómo demasiado[Introducción a la aplicación de Microsoft Authenticator hello](microsoft-authenticator-app-how-to.md) para que pueda utilizar toosign de notificaciones, en lugar de textos y llamadas de teléfono.</span><span class="sxs-lookup"><span data-stu-id="cca82-157">Find out how too[Get started with hello Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications toosign in, instead of texts and phone calls.</span></span> 
