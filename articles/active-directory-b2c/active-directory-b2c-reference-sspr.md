---
title: "Azure Active Directory B2C: restablecimiento de contraseña de autoservicio | Microsoft Docs"
description: "Tema en el que se demuestra cómo configurar el autoservicio de restablecimiento de contraseña para los consumidores en Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 0508868e3b00c5771cc26038a3dd71fde6625a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="9bb38-103">Azure Active Directory B2C: configurar el autoservicio de restablecimiento de contraseña para los consumidores</span><span class="sxs-lookup"><span data-stu-id="9bb38-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="9bb38-104">Con la característica de autoservicio de restablecimiento de contraseña, los consumidores que se registraron para obtener cuentas locales pueden restablecer sus contraseñas ellos mismos.</span><span class="sxs-lookup"><span data-stu-id="9bb38-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="9bb38-105">De esta manera se reduce significativamente la carga del personal de soporte técnico, especialmente si la aplicación tiene millones de consumidores que la usan de forma periódica.</span><span class="sxs-lookup"><span data-stu-id="9bb38-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="9bb38-106">Actualmente, solo se admite como método de recuperación el uso de una dirección de correo electrónico comprobada.</span><span class="sxs-lookup"><span data-stu-id="9bb38-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="9bb38-107">Agregaremos métodos de recuperación adicionales (número de teléfono comprobado, preguntas de seguridad, etc.) en el futuro.</span><span class="sxs-lookup"><span data-stu-id="9bb38-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="9bb38-108">Este artículo se aplica a la operación de autoservicio de restablecimiento de contraseña empleada en el contexto de una directiva de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9bb38-108">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="9bb38-109">Si necesita invocar directivas de restablecimiento de contraseña totalmente personalizables desde su aplicación, consulte [este artículo](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="9bb38-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="9bb38-110">De forma predeterminada, el directorio no tendrá activado el autoservicio de restablecimiento de contraseña.</span><span class="sxs-lookup"><span data-stu-id="9bb38-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="9bb38-111">Para activarlo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9bb38-111">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="9bb38-112">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com/) como administrador de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="9bb38-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="9bb38-113">Esta cuenta es la misma cuenta profesional o educativa o la misma cuenta Microsoft que usó para crear el directorio.</span><span class="sxs-lookup"><span data-stu-id="9bb38-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="9bb38-114">Vaya a la extensión de Active Directory en la barra de navegación del lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="9bb38-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span></span>
3. <span data-ttu-id="9bb38-115">Busque su directorio en la pestaña **Directorio** y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="9bb38-115">Find your directory under the **Directory** tab and click it.</span></span>
4. <span data-ttu-id="9bb38-116">Haga clic en la pestaña **Configure** .</span><span class="sxs-lookup"><span data-stu-id="9bb38-116">Click the **Configure** tab.</span></span>
5. <span data-ttu-id="9bb38-117">Baje hasta la sección **Políticas para restablecer la contraseña del usuario** y cambie el valor de la opción **Usuarios habilitados para restablecer la contraseña** a **SÍ**.</span><span class="sxs-lookup"><span data-stu-id="9bb38-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span></span> <span data-ttu-id="9bb38-118">Observe que la opción **Dirección de correo electrónico alternativa** está activada; déjela así.</span><span class="sxs-lookup"><span data-stu-id="9bb38-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Restablecimiento de la contraseña de autoservicio](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="9bb38-120">Haga clic en **Guardar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="9bb38-120">Click **Save** at the bottom of the page.</span></span> <span data-ttu-id="9bb38-121">¡Y ya está!</span><span class="sxs-lookup"><span data-stu-id="9bb38-121">You're done!</span></span>

<span data-ttu-id="9bb38-122">Para probar, use la característica "Ejecutar ahora" en cualquier directiva de inicio de sesión que tenga cuentas locales como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="9bb38-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="9bb38-123">En la página de inicio de sesión de la cuenta local (donde escribe la dirección de correo electrónico y la contraseña, o bien el nombre de usuario y la contraseña), haga clic en **¿No se puede tener acceso a la cuenta?** para comprobar la experiencia del consumidor.</span><span class="sxs-lookup"><span data-stu-id="9bb38-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="9bb38-124">Las páginas del autoservicio de restablecimiento de contraseña se pueden personalizar con la [característica de personalización de marca de empresa](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="9bb38-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

