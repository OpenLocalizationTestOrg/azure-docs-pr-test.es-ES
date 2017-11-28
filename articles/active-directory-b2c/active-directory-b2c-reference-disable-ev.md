---
title: "Azure Active Directory B2C: Deshabilitación de la comprobación de correos electrónicos durante la suscripción de consumidores | Microsoft Docs"
description: "Un tema que muestra cómo toodisable enviar por correo electrónico de comprobación durante el inicio de sesión en Azure Active Directory B2C consumidor"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="9bdd4-103">Azure Active Directory B2C: Deshabilitación de la comprobación de correos electrónicos durante la suscripción de consumidores</span><span class="sxs-lookup"><span data-stu-id="9bdd4-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="9bdd4-104">Cuando se habilita, B2C de Azure Active Directory (Azure AD) proporciona un consumidor Hola toosign de capacidad para las aplicaciones al proporcionar una dirección de correo electrónico y crear una cuenta local.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer hello ability toosign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="9bdd4-105">B2C de Azure AD garantiza direcciones de correo electrónico válida al exigir a los consumidores tooverify usarlas durante el proceso de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-105">Azure AD B2C ensures valid email addresses by requiring consumers tooverify them during hello sign-up process.</span></span> <span data-ttu-id="9bdd4-106">También impide que un proceso automatizado malintencionado generar falsas cuentas para aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-106">It also prevents a malicious automated process from generating fake accounts for hello applications.</span></span>

<span data-ttu-id="9bdd4-107">Algunos desarrolladores de aplicaciones prefieren tooskip comprobación de correo electrónico durante el proceso de registro de hello y en su lugar, tiene que los consumidores comprobar la dirección de correo electrónico de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-107">Some application developers prefer tooskip email verification during hello sign-up process and instead have consumers verify hello email address later.</span></span> <span data-ttu-id="9bdd4-108">toosupport, Azure AD B2C puede ser configurado toodisable comprobación de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-108">toosupport this, Azure AD B2C can be configured toodisable email verification.</span></span> <span data-ttu-id="9bdd4-109">Si lo hace, crea un proceso de inicio de sesión más suave y ofrece a los desarrolladores Hola flexibilidad toodifferentiate Hola los consumidores que han comprobado su dirección de correo electrónico de los consumidores que no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-109">Doing so creates a smoother sign-up process and gives developers hello flexibility toodifferentiate hello consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="9bdd4-110">De forma predeterminada, las directivas de inicio de sesión tienen activada la comprobación de correos electrónicos.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="9bdd4-111">Use Hola siguientes pasos tooturn desactivada:</span><span class="sxs-lookup"><span data-stu-id="9bdd4-111">Use hello following steps tooturn it off:</span></span>

1. <span data-ttu-id="9bdd4-112">[Siga estos módulos de características de pasos toonavigate toohello B2C en hello portal de Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="9bdd4-112">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="9bdd4-113">Haga clic en **Sign-up policies** (Directivas de registro) o **Sign-up or sign-in policies** (Directivas de inicio de sesión o registro) dependiendo de lo que haya configurado para el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="9bdd4-114">Haga clic en la directiva (por ejemplo, "B2C_1_SiUp") tooopen.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-114">Click your policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="9bdd4-115">Haga clic en **editar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-115">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="9bdd4-116">Haga clic en **Page UI Customization** (Personalización de la IU de la página).</span><span class="sxs-lookup"><span data-stu-id="9bdd4-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="9bdd4-117">Haga clic en **Página de suscripción de cuenta local**.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="9bdd4-118">Haga clic en **dirección de correo electrónico** en hello **nombre** columna bajo hello **atributos suscripción** sección.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-118">Click **Email Address** in hello **Name** column under hello **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="9bdd4-119">Hola de alternancia **Requerir comprobación** opción demasiado**No**.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-119">Toggle hello **Require verification** option too**No**.</span></span>
8. <span data-ttu-id="9bdd4-120">Haga clic en **Aceptar** en parte inferior de hello hasta llegar a hello **Editar directiva** hoja.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-120">Click **OK** at hello bottom until you reach hello **Edit policy** blade.</span></span>
9. <span data-ttu-id="9bdd4-121">Haga clic en **guardar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-121">Click **Save** at hello top of hello blade.</span></span> <span data-ttu-id="9bdd4-122">¡Y ya está!</span><span class="sxs-lookup"><span data-stu-id="9bdd4-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="9bdd4-123">Deshabilitar la comprobación de correo electrónico en el proceso de registro de hello puede provocar toospam.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-123">Disabling email verification in hello sign-up process may lead toospam.</span></span> <span data-ttu-id="9bdd4-124">Si deshabilita Hola seleccionado de modo predeterminado, se recomienda agregar su propio sistema de comprobación.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-124">If you disable hello default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="9bdd4-125">Estamos siempre toofeedback abierta y sugerencias.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-125">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="9bdd4-126">Si tiene dificultades con este tema, o tiene las recomendaciones para mejorar el contenido, le agradeceríamos sus comentarios en la parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bdd4-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="9bdd4-127">Para las solicitudes de características, agregarlos demasiado[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="9bdd4-127">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
