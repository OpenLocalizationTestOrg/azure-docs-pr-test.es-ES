---
title: "Azure Active Directory B2C: restablecimiento de contraseña de autoservicio | Microsoft Docs"
description: "Un tema que muestra cómo restablece tooset la contraseña de autoservicio para los consumidores en Azure Active Directory B2C"
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
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="4b9d3-103">Azure Active Directory B2C: configurar el autoservicio de restablecimiento de contraseña para los consumidores</span><span class="sxs-lookup"><span data-stu-id="4b9d3-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="4b9d3-104">Con hello característica de restablecimiento de contraseña de autoservicio, los consumidores (que se suscribieron para cuentas locales) pueden restablecer sus contraseñas por sí solas.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-104">With hello self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="4b9d3-105">Esto reduce considerablemente carga hello en su personal de soporte técnico, sobre todo si la aplicación tiene millones de los consumidores que usan de forma regular.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-105">This significantly reduces hello burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="4b9d3-106">Actualmente, solo se admite como método de recuperación el uso de una dirección de correo electrónico comprobada.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="4b9d3-107">Métodos de recuperación adicionales (número de teléfono comprobado, preguntas de seguridad, etc.) se agregará en un futuro Hola.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-107">We will add additional recovery methods (verified phone number, security questions, etc.) in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="4b9d3-108">Este artículo aplica la contraseña del servicio tooself restablecimiento utilizado en el contexto de Hola de una directiva de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-108">This article applies tooself-service password reset used in hello context of a sign-in policy.</span></span> <span data-ttu-id="4b9d3-109">Si necesita invocar directivas de restablecimiento de contraseña totalmente personalizables desde su aplicación, consulte [este artículo](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="4b9d3-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="4b9d3-110">De forma predeterminada, el directorio no tendrá activado el autoservicio de restablecimiento de contraseña.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="4b9d3-111">Use Hola siguientes pasos tooturn en:</span><span class="sxs-lookup"><span data-stu-id="4b9d3-111">Use hello following steps tooturn it on:</span></span>

1. <span data-ttu-id="4b9d3-112">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) como Hola Administrador de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-112">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) as hello Subscription Administrator.</span></span> <span data-ttu-id="4b9d3-113">Se trata de hello mismo trabajo o educativa cuenta u Hola la misma cuenta de Microsoft que usa toocreate su directorio.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-113">This is hello same work or school account or hello same Microsoft account that you used toocreate your directory.</span></span>
2. <span data-ttu-id="4b9d3-114">Navegue toohello extensión de Active Directory en la barra de navegación de hello en el lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-114">Navigate toohello Active Directory extension on hello navigation bar on hello left side.</span></span>
3. <span data-ttu-id="4b9d3-115">Buscar el directorio en hello **Directory** ficha y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-115">Find your directory under hello **Directory** tab and click it.</span></span>
4. <span data-ttu-id="4b9d3-116">Haga clic en hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-116">Click hello **Configure** tab.</span></span>
5. <span data-ttu-id="4b9d3-117">Desplácese hacia abajo toohello **políticas para restablecer contraseñas de usuario** sección y alternar hello **usuarios habilitados para restablecer la contraseña** opción demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-117">Scroll down toohello **User password reset policy** section and toggle hello **Users enabled for password reset** option too**YES**.</span></span> <span data-ttu-id="4b9d3-118">Tenga en cuenta que hello **dirección de correo electrónico alternativa** opción está activada; dejarlo tal cual.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-118">Notice that hello **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Restablecimiento de la contraseña de autoservicio](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="4b9d3-120">Haga clic en **guardar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-120">Click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="4b9d3-121">¡Y ya está!</span><span class="sxs-lookup"><span data-stu-id="4b9d3-121">You're done!</span></span>

<span data-ttu-id="4b9d3-122">tootest, característica de "Ejecutar ahora" hello de uso en cualquier directiva de inicio de sesión que tiene las cuentas locales como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-122">tootest, use hello "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="4b9d3-123">En el inicio de sesión de cuenta local de hello página (donde se introducirán una dirección de correo electrónico y contraseña, o un nombre de usuario y una contraseña), haga clic en **no se puede acceder a su cuenta?** experiencia del consumidor tooverify Hola.</span><span class="sxs-lookup"><span data-stu-id="4b9d3-123">On hello local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** tooverify hello consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="4b9d3-124">Hello páginas de restablecimiento de contraseña de autoservicio pueden personalizarse mediante el uso de hello [característica de personalización de marca de empresa](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="4b9d3-124">hello self-service password reset pages can be customized by using hello [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

