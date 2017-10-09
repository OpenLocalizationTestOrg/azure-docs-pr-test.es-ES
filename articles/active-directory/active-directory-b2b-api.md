---
title: "aaaAzure B2B de Active Directory personalización y colaboración API | Documentos de Microsoft"
description: "Colaboración B2B de Active Directory de Azure es compatible con las relaciones entre empresas habilitando tooselectively los socios comerciales acceso aplicaciones corporativas"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="68319-103">Personalización y API de colaboración B2B de Active Directory Azure</span><span class="sxs-lookup"><span data-stu-id="68319-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="68319-104">Hemos tenido muchos clientes nos indican que desean que el proceso de invitación de hello toocustomize de forma que se adapte mejor a sus organizaciones.</span><span class="sxs-lookup"><span data-stu-id="68319-104">We've had many customers tell us that they want toocustomize hello invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="68319-105">Con nuestra API, pueden hacer justamente eso.</span><span class="sxs-lookup"><span data-stu-id="68319-105">With our API, you can do just that.</span></span> [<span data-ttu-id="68319-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="68319-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a><span data-ttu-id="68319-107">Capacidades de invitación de hello API</span><span class="sxs-lookup"><span data-stu-id="68319-107">Capabilities of hello invitation API</span></span>
<span data-ttu-id="68319-108">Hola API ofrece Hola siguientes capacidades:</span><span class="sxs-lookup"><span data-stu-id="68319-108">hello API offers hello following capabilities:</span></span>

1. <span data-ttu-id="68319-109">Invite a un usuario externo con *cualquier* dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="68319-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="68319-110">Personalizar donde desea que su tooland a los usuarios después de que acepten la invitación.</span><span class="sxs-lookup"><span data-stu-id="68319-110">Customize where you want your users tooland after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="68319-111">Elija correo electrónico de invitación estándar de toosend Hola por medio de nosotros</span><span class="sxs-lookup"><span data-stu-id="68319-111">Choose toosend hello standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="68319-112">con un destinatario del mensaje toohello que se puede personalizar</span><span class="sxs-lookup"><span data-stu-id="68319-112">with a message toohello recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="68319-113">Y elija toocc: personas que desea tookeep Hola bucle sobre su invitar a este colaborador.</span><span class="sxs-lookup"><span data-stu-id="68319-113">And choose toocc: people you want tookeep in hello loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="68319-114">O bien personalizar completamente su invitación y el flujo de trabajo de incorporación eligiendo no toosend notificaciones a través de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68319-114">Or completely customize your invitation and onboarding workflow by choosing not toosend notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="68319-115">En este caso, se recibe una URL de pago de hello API que se puede incrustar en una plantilla de correo electrónico, mensajería instantánea u otro método de distribución de su elección.</span><span class="sxs-lookup"><span data-stu-id="68319-115">In this case, you get back a redemption URL from hello API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="68319-116">Por último, si es administrador, puede elegir usuario de hello tooinvite como miembro.</span><span class="sxs-lookup"><span data-stu-id="68319-116">Finally, if you are an admin, you can choose tooinvite hello user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="68319-117">Modelo de autorización</span><span class="sxs-lookup"><span data-stu-id="68319-117">Authorization model</span></span>
<span data-ttu-id="68319-118">Hola API se puede ejecutar en los siguientes modos de autorización de hello:</span><span class="sxs-lookup"><span data-stu-id="68319-118">hello API can be run in hello following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="68319-119">Aplicación y modo de usuario</span><span class="sxs-lookup"><span data-stu-id="68319-119">App + User mode</span></span>
<span data-ttu-id="68319-120">En este modo, gana el jugador que está usando Hola API necesidades toohave Hola permisos toobe crear invitaciones de B2B.</span><span class="sxs-lookup"><span data-stu-id="68319-120">In this mode, whoever is using hello API needs toohave hello permissions toobe create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="68319-121">Modo de solo aplicación</span><span class="sxs-lookup"><span data-stu-id="68319-121">App only mode</span></span>
<span data-ttu-id="68319-122">En el contexto solo de aplicación, aplicación hello debe hello User.ReadWrite.All o Directory.ReadWrite.All ámbitos para hello invitación toosucceed.</span><span class="sxs-lookup"><span data-stu-id="68319-122">In app only context, hello app needs hello User.ReadWrite.All or Directory.ReadWrite.All scopes for hello invitation toosucceed.</span></span>

<span data-ttu-id="68319-123">Para obtener más información, consulte: https://graph.microsoft.io/docs/authorization/permission_scopes.</span><span class="sxs-lookup"><span data-stu-id="68319-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="68319-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68319-124">PowerShell</span></span>
<span data-ttu-id="68319-125">Es ahora toouse posibles PowerShell tooadd e invitar a usuarios externos tooan organización fácilmente.</span><span class="sxs-lookup"><span data-stu-id="68319-125">It is now possible toouse PowerShell tooadd and invite external users tooan organization easily.</span></span> <span data-ttu-id="68319-126">Crear una invitación con hello cmdlet:</span><span class="sxs-lookup"><span data-stu-id="68319-126">Create an invitation using hello cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="68319-127">Puede usar Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="68319-127">You can use hello following options:</span></span>

* <span data-ttu-id="68319-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="68319-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="68319-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="68319-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="68319-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="68319-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="68319-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="68319-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="68319-132">También es posible desproteger referencia de API de invitación de hello en [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="68319-132">You can also check out hello invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="68319-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="68319-133">Next steps</span></span>

<span data-ttu-id="68319-134">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="68319-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="68319-135">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="68319-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="68319-136">¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="68319-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="68319-137">¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="68319-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="68319-138">elementos de saludo de correo electrónico de invitación de colaboración B2B de hello</span><span class="sxs-lookup"><span data-stu-id="68319-138">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="68319-139">Canje de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="68319-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="68319-140">Concesión de licencias de colaboración B2B de Azure AD</span><span class="sxs-lookup"><span data-stu-id="68319-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="68319-141">Solución de problemas de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68319-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="68319-142">Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)</span><span class="sxs-lookup"><span data-stu-id="68319-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="68319-143">Autenticación multifactor para usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="68319-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="68319-144">Incorporación de usuarios de colaboración B2B sin invitación</span><span class="sxs-lookup"><span data-stu-id="68319-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="68319-145">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68319-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
