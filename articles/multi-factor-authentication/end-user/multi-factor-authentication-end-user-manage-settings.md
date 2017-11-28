---
title: "aaaManage la configuración de comprobación de dos pasos | Documentos de Microsoft"
description: "Administre cómo usar Azure Multi-Factor Authentication, incluida la modificación de la información de contacto o la configuración de los dispositivos."
services: multi-factor-authentication
keywords: "cliente de multi-factor authentication, problema de autenticación, identificador de correlación"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="fdd7e-104">Administración de la configuración de la comprobación en dos pasos</span><span class="sxs-lookup"><span data-stu-id="fdd7e-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="fdd7e-105">Este artículo ofrece respuestas a preguntas acerca de cómo tooupdate configuración para la autenticación de dos pasos de verificación o multifactor.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-105">This article answers questions about how tooupdate settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="fdd7e-106">Si tiene problemas para iniciar sesión en la cuenta de tooyour, consulte demasiado[tiene problemas con la verificacion](multi-factor-authentication-end-user-troubleshoot.md) de ayuda para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-106">If you are having issues signing in tooyour account, refer too[Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-toofind-hello-settings-page"></a><span data-ttu-id="fdd7e-107">Donde toofind Hola página de configuración</span><span class="sxs-lookup"><span data-stu-id="fdd7e-107">Where toofind hello settings page</span></span>
<span data-ttu-id="fdd7e-108">Según cómo su compañía configure Azure Multi-Factor Authentication, existen algunos lugares donde puede cambiar los ajustes, como su número de teléfono.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="fdd7e-109">Si el Administrador de TI envía una dirección URL específica o verificacion de pasos toomanage, siga estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-109">If your IT admin sent out a specific URL or steps toomanage two-step verification, follow those instructions.</span></span> <span data-ttu-id="fdd7e-110">En caso contrario, debería funcionar Hola siguiendo las instrucciones para los demás.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-110">Otherwise, hello following instructions should work for everybody else.</span></span> <span data-ttu-id="fdd7e-111">Si se siguen estos pasos, pero no ve hello las mismas opciones, lo que significa que su trabajo o escuela personaliza su propio portal.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-111">If you follow these steps but don't see hello same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="fdd7e-112">Pida al administrador de portal de Azure la autenticación multifactor de hello vínculo tooyour.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-112">Ask your admin for hello link tooyour Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="fdd7e-113">Inicie sesión en demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="fdd7e-113">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="fdd7e-114">Seleccione el nombre de cuenta en hello parte superior derecha, a continuación, seleccione **perfil**.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-114">Select your account name in hello top right, then select **profile**.</span></span>  
3. <span data-ttu-id="fdd7e-115">Seleccione **Comprobación de seguridad adicional**.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-115">Select **Additional security verification**.</span></span>  

    ![MyApps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="fdd7e-117">página de comprobación de seguridad adicionales de Hello carga con la configuración.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-117">hello Additional security verification page loads with your settings.</span></span>

    ![Página de proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="fdd7e-119">Desea toochange mi número de teléfono o agregar un número secundario</span><span class="sxs-lookup"><span data-stu-id="fdd7e-119">I want toochange my phone number, or add a secondary number</span></span>
<span data-ttu-id="fdd7e-120">Es importante tooconfigure un número de teléfono de autenticación secundaria.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-120">It is important tooconfigure a secondary authentication phone number.</span></span>  <span data-ttu-id="fdd7e-121">Dado que su aplicación móvil y número de teléfono de su objeto principal son probablemente en hello igual de teléfono, número de teléfono secundario de hello es una única manera de hello estará tooget pueda volver a tu cuenta si se pierde o le roban el teléfono.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-121">Because your primary phone number and your mobile app are probably on hello same phone, hello secondary phone number is hello only way you will be able tooget back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="fdd7e-122">Si no tiene el número de teléfono principal de acceso tooyour y necesita ayuda para obtener en tooyour cuenta, consulte nuestro temas de ayuda en [tiene problemas con la verificacion](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="fdd7e-122">If you don't have access tooyour primary phone number, and need help getting in tooyour account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="fdd7e-123">**toochange número de teléfono principal:**</span><span class="sxs-lookup"><span data-stu-id="fdd7e-123">**toochange your primary phone number:**</span></span>  

1. <span data-ttu-id="fdd7e-124">En la página de comprobación de seguridad adicionales de hello, seleccione el cuadro de texto de hello con el número de teléfono actual y modifíquelo con el nuevo número de teléfono.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-124">On hello Additional security verification page, select hello text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="fdd7e-125">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-125">Select **Save**.</span></span>  
3. <span data-ttu-id="fdd7e-126">Si este es el número de Hola que utiliza para la opción de comprobación preferida, tendrá nuevo número de tooverify Hola antes de que se puede guardar.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-126">If this is hello number that you use for your preferred verification option, you have tooverify hello new number before you can save it.</span></span>  

<span data-ttu-id="fdd7e-127">**tooadd un número de teléfono secundario:**</span><span class="sxs-lookup"><span data-stu-id="fdd7e-127">**tooadd a secondary phone number:**</span></span>  

1. <span data-ttu-id="fdd7e-128">En la página de comprobación de seguridad adicionales de hello, casilla Hola junto demasiado**teléfono de autenticación alternativo.**</span><span class="sxs-lookup"><span data-stu-id="fdd7e-128">On hello Additional security verification page, check hello box next too**Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="fdd7e-129">Escriba el número de teléfono secundario en el cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-129">Enter your secondary phone number in hello text box.</span></span>  
3. <span data-ttu-id="fdd7e-130">Seleccione **Guardar** y los cambios habrán finalizado.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="fdd7e-131">Requisito de nueva verificación en dos pasos en un dispositivo marcado como de confianza</span><span class="sxs-lookup"><span data-stu-id="fdd7e-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="fdd7e-132">Dependiendo de la configuración de la organización, es posible que tenga una casilla que indica "Don't ask again for **X** days" (No volver a preguntar en X días) al realizar la verificación en dos pasos en el explorador.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="fdd7e-133">Si esta casilla de verificación y, a continuación, pierden su dispositivo o cree que su cuenta se ve comprometida, debe restaurar tooall de comprobación de dos pasos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification tooall your devices.</span></span> 

1. <span data-ttu-id="fdd7e-134">En la página de comprobación de seguridad adicionales de hello, seleccione **restaurar la autenticación multifactor en dispositivos de confianza anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-134">On hello Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="fdd7e-135">Hello próxima vez que inicie sesión en cualquier dispositivo, podrá verificacion de tooperform solicitadas.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-135">hello next time you sign in on any device, you'll be prompted tooperform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a><span data-ttu-id="fdd7e-136">¿Cómo limpiar Microsoft Authenticator desde mi dispositivo anterior y mover tooa uno nuevo?</span><span class="sxs-lookup"><span data-stu-id="fdd7e-136">How do I clean up Microsoft Authenticator from my old device and move tooa new one?</span></span>
<span data-ttu-id="fdd7e-137">Cuando se desinstala la aplicación hello desde su dispositivo o restablecer Hola dispositivo, no quita la activación de hello en back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-137">When you uninstall hello app from your device or reset hello device, it does not remove hello activation on hello back end.</span></span> <span data-ttu-id="fdd7e-138">Para más información, vea [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="fdd7e-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdd7e-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fdd7e-139">Next steps</span></span>
* <span data-ttu-id="fdd7e-140">Obtener sugerencias para solucionar problemas y necesita ayuda [Problemas con la comprobación en dos pasos](multi-factor-authentication-end-user-troubleshoot.md)</span><span class="sxs-lookup"><span data-stu-id="fdd7e-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="fdd7e-141">Configure [contraseñas de aplicación](multi-factor-authentication-end-user-app-passwords.md) para las aplicaciones que no admiten la comprobación en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="fdd7e-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
