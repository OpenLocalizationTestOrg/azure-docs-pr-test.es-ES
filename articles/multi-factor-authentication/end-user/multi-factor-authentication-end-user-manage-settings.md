---
title: "Administrar la configuración de verificación en dos pasos | Microsoft Docs"
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
ms.openlocfilehash: f752fb19e4ff2f831d50104e9c7d5f42cc3486d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="98fbe-104">Administración de la configuración de la comprobación en dos pasos</span><span class="sxs-lookup"><span data-stu-id="98fbe-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="98fbe-105">Este artículo ofrece respuestas a preguntas acerca de cómo actualizar la configuración de actualización en dos pasos o la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="98fbe-105">This article answers questions about how to update settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="98fbe-106">Si tiene problemas para iniciar sesión en su cuenta, consulte [Problemas con la comprobación en dos pasos](multi-factor-authentication-end-user-troubleshoot.md) para obtener ayuda para la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="98fbe-106">If you are having issues signing in to your account, refer to [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-to-find-the-settings-page"></a><span data-ttu-id="98fbe-107">Dónde encontrar la página de configuración</span><span class="sxs-lookup"><span data-stu-id="98fbe-107">Where to find the settings page</span></span>
<span data-ttu-id="98fbe-108">Según cómo su compañía configure Azure Multi-Factor Authentication, existen algunos lugares donde puede cambiar los ajustes, como su número de teléfono.</span><span class="sxs-lookup"><span data-stu-id="98fbe-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="98fbe-109">Si el administrador de TI envía una dirección URL específica o pasos para administrar la comprobación en dos pasos, siga las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="98fbe-109">If your IT admin sent out a specific URL or steps to manage two-step verification, follow those instructions.</span></span> <span data-ttu-id="98fbe-110">De lo contrario, las instrucciones siguientes deben funcionar para los demás.</span><span class="sxs-lookup"><span data-stu-id="98fbe-110">Otherwise, the following instructions should work for everybody else.</span></span> <span data-ttu-id="98fbe-111">Si se siguen estos pasos, pero no ve las mismas opciones, significa que su trabajo o escuela personalizó su propio portal.</span><span class="sxs-lookup"><span data-stu-id="98fbe-111">If you follow these steps but don't see the same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="98fbe-112">Consulte al administrador para obtener el vínculo a su portal de Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="98fbe-112">Ask your admin for the link to your Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="98fbe-113">Inicie sesión en [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="98fbe-113">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="98fbe-114">Seleccione el nombre de cuenta en la parte superior derecha y, después, seleccione **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="98fbe-114">Select your account name in the top right, then select **profile**.</span></span>  
3. <span data-ttu-id="98fbe-115">Seleccione **Comprobación de seguridad adicional**.</span><span class="sxs-lookup"><span data-stu-id="98fbe-115">Select **Additional security verification**.</span></span>  

    ![MyApps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="98fbe-117">La página de comprobación de seguridad adicional se carga con la configuración.</span><span class="sxs-lookup"><span data-stu-id="98fbe-117">The Additional security verification page loads with your settings.</span></span>

    ![Página de proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="98fbe-119">Deseo cambiar mi número de teléfono o agregar un número secundario</span><span class="sxs-lookup"><span data-stu-id="98fbe-119">I want to change my phone number, or add a secondary number</span></span>
<span data-ttu-id="98fbe-120">Es importante configurar un número de teléfono de autenticación secundario.</span><span class="sxs-lookup"><span data-stu-id="98fbe-120">It is important to configure a secondary authentication phone number.</span></span>  <span data-ttu-id="98fbe-121">Debido a que el número de teléfono principal y la aplicación móvil probablemente se encuentran en el mismo teléfono, el número de teléfono secundario es la única forma que tiene para volver a tener acceso a su cuenta si se le pierde el teléfono o si se lo robaron.</span><span class="sxs-lookup"><span data-stu-id="98fbe-121">Because your primary phone number and your mobile app are probably on the same phone, the secondary phone number is the only way you will be able to get back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="98fbe-122">Si no dispone de acceso a su número de teléfono principal y necesita ayuda para encontrar su cuenta, vea nuestros temas de ayuda [Problemas con la comprobación en dos pasos](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="98fbe-122">If you don't have access to your primary phone number, and need help getting in to your account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="98fbe-123">**Para cambiar el número de teléfono principal:**</span><span class="sxs-lookup"><span data-stu-id="98fbe-123">**To change your primary phone number:**</span></span>  

1. <span data-ttu-id="98fbe-124">En la página de comprobación de seguridad adicional, seleccione el cuadro de texto con el número de teléfono actual y modifíquelo con el nuevo número de teléfono.</span><span class="sxs-lookup"><span data-stu-id="98fbe-124">On the Additional security verification page, select the text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="98fbe-125">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="98fbe-125">Select **Save**.</span></span>  
3. <span data-ttu-id="98fbe-126">Si este es el número que se utiliza para la opción de comprobación preferida, tiene que comprobar el nuevo número para poder guardarlo.</span><span class="sxs-lookup"><span data-stu-id="98fbe-126">If this is the number that you use for your preferred verification option, you have to verify the new number before you can save it.</span></span>  

<span data-ttu-id="98fbe-127">**Para agregar un número de teléfono secundario:**</span><span class="sxs-lookup"><span data-stu-id="98fbe-127">**To add a secondary phone number:**</span></span>  

1. <span data-ttu-id="98fbe-128">En la página de comprobación de seguridad adicional, active la casilla junto al **teléfono de autenticación alternativo.**</span><span class="sxs-lookup"><span data-stu-id="98fbe-128">On the Additional security verification page, check the box next to **Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="98fbe-129">En el cuadro de texto, escriba el número de teléfono secundario.</span><span class="sxs-lookup"><span data-stu-id="98fbe-129">Enter your secondary phone number in the text box.</span></span>  
3. <span data-ttu-id="98fbe-130">Seleccione **Guardar** y los cambios habrán finalizado.</span><span class="sxs-lookup"><span data-stu-id="98fbe-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="98fbe-131">Requisito de nueva verificación en dos pasos en un dispositivo marcado como de confianza</span><span class="sxs-lookup"><span data-stu-id="98fbe-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="98fbe-132">Dependiendo de la configuración de la organización, es posible que tenga una casilla que indica "Don't ask again for **X** days" (No volver a preguntar en X días) al realizar la verificación en dos pasos en el explorador.</span><span class="sxs-lookup"><span data-stu-id="98fbe-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="98fbe-133">Si marca este cuadro y pierde el dispositivo o piensa que se ha comprometido la seguridad de su cuenta, debe restaurar la verificación en dos pasos en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="98fbe-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification to all your devices.</span></span> 

1. <span data-ttu-id="98fbe-134">En la página Comprobación de seguridad adicional, seleccione **Restaurar Multi-Factor Authentication en dispositivos en los que se confió anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="98fbe-134">On the Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="98fbe-135">La próxima vez que inicie sesión en cualquier dispositivo, se le pedirá que realice la verificación en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="98fbe-135">The next time you sign in on any device, you'll be prompted to perform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a><span data-ttu-id="98fbe-136">¿Cómo puedo quitar Microsoft Authenticator del dispositivo anterior y moverlo a uno nuevo?</span><span class="sxs-lookup"><span data-stu-id="98fbe-136">How do I clean up Microsoft Authenticator from my old device and move to a new one?</span></span>
<span data-ttu-id="98fbe-137">Cuando desinstala la aplicación del dispositivo o restablece el dispositivo, no se quita la activación en el back-end.</span><span class="sxs-lookup"><span data-stu-id="98fbe-137">When you uninstall the app from your device or reset the device, it does not remove the activation on the back end.</span></span> <span data-ttu-id="98fbe-138">Para más información, vea [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="98fbe-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="98fbe-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="98fbe-139">Next steps</span></span>
* <span data-ttu-id="98fbe-140">Obtener sugerencias para solucionar problemas y necesita ayuda [Problemas con la comprobación en dos pasos](multi-factor-authentication-end-user-troubleshoot.md)</span><span class="sxs-lookup"><span data-stu-id="98fbe-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="98fbe-141">Configure [contraseñas de aplicación](multi-factor-authentication-end-user-app-passwords.md) para las aplicaciones que no admiten la comprobación en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="98fbe-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
