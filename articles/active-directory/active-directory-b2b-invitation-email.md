---
title: "Los elementos del correo electrónico de invitación de colaboración B2B de Azure Active Directory | Microsoft Docs"
description: "Plantilla de correo electrónico de invitación de colaboración B2B de Azure Active Directory"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 458a2cab13b7e83f120e0926a95d454070181dfb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a><span data-ttu-id="af0c6-103">Los elementos del correo electrónico de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="af0c6-103">The elements of the B2B collaboration invitation email</span></span>

<span data-ttu-id="af0c6-104">Los correos electrónicos de invitación son un componente fundamental para incorporar a los asociados como usuarios de colaboración B2B en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af0c6-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="af0c6-105">Puede usarlos para aumentar la confianza del destinatario.</span><span class="sxs-lookup"><span data-stu-id="af0c6-105">You can use them to increase the recipient's trust.</span></span> <span data-ttu-id="af0c6-106">Puede agregar legitimidad y prueba social al correo electrónico para asegurarse de que el destinatario se sienta cómodo al seleccionar el botón **Empezar** para aceptar la invitación.</span><span class="sxs-lookup"><span data-stu-id="af0c6-106">you can add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span></span> <span data-ttu-id="af0c6-107">Esta confianza es clave para reducir la fricción en el uso compartido.</span><span class="sxs-lookup"><span data-stu-id="af0c6-107">This trust is a key means to reduce sharing friction.</span></span> <span data-ttu-id="af0c6-108">Y puede que también quiera que el correo electrónico tenga un buen aspecto.</span><span class="sxs-lookup"><span data-stu-id="af0c6-108">And you also want to make the email look great!</span></span>

![Correo electrónico de invitación de B2B de Azure AD](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a><span data-ttu-id="af0c6-110">Explicación del correo electrónico</span><span class="sxs-lookup"><span data-stu-id="af0c6-110">Explaining the email</span></span>
<span data-ttu-id="af0c6-111">Se van a tratar algunos elementos del correo electrónico para saber cómo hacer el mejor uso de estas funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="af0c6-111">Let's look at a few elements of the email so you know how best to use their capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="af0c6-112">Asunto</span><span class="sxs-lookup"><span data-stu-id="af0c6-112">Subject</span></span>
<span data-ttu-id="af0c6-113">El asunto del correo electrónico sigue este patrón: Está invitado a la organización de &lt;nombreinquilino&gt;.</span><span class="sxs-lookup"><span data-stu-id="af0c6-113">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="af0c6-114">Dirección De</span><span class="sxs-lookup"><span data-stu-id="af0c6-114">From address</span></span>
<span data-ttu-id="af0c6-115">Se usa un patrón similar a LinkedIn para la dirección De.</span><span class="sxs-lookup"><span data-stu-id="af0c6-115">We use a LinkedIn-like pattern for the From address.</span></span>  <span data-ttu-id="af0c6-116">Es necesario tener claro quién es el invitador y a qué empresa pertenece y también aclarar que el correo electrónico procede de una dirección de correo electrónico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="af0c6-116">You should be clear who the inviter is and from which company, and also clarify that the email is coming from a Microsoft email address.</span></span> <span data-ttu-id="af0c6-117">El formato es: &lt;Nombre para mostrar del invitador&gt; de &lt;nombreinquilino&gt; (a través de Microsoft) invites@microsoft.com&gt;.</span><span class="sxs-lookup"><span data-stu-id="af0c6-117">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="af0c6-118">Responder a</span><span class="sxs-lookup"><span data-stu-id="af0c6-118">Reply To</span></span>
<span data-ttu-id="af0c6-119">En la respuesta al correo electrónico se indica el correo electrónico del invitador si está disponible, para que al responder al correo electrónico se vuelva a enviar un correo al invitador.</span><span class="sxs-lookup"><span data-stu-id="af0c6-119">The reply-to email is set to the inviter's email when available, so that replying to the email sends an email back to the inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="af0c6-120">Personalización de marca</span><span class="sxs-lookup"><span data-stu-id="af0c6-120">Branding</span></span>
<span data-ttu-id="af0c6-121">Los correos electrónicos de invitación del inquilino usan la personalización de marca de la empresa que puede haberse configurado para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="af0c6-121">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="af0c6-122">Si desea beneficiarse de esta funcionalidad, [aquí](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) se proporcionan los detalles sobre cómo configurarla.</span><span class="sxs-lookup"><span data-stu-id="af0c6-122">If you want to take advantage of this capability, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span></span> <span data-ttu-id="af0c6-123">El logotipo del banner aparece en el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="af0c6-123">The banner logo appears in the email.</span></span> <span data-ttu-id="af0c6-124">Siga el tamaño de la imagen y las instrucciones de calidad indicadas [aquí](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) para obtener los mejores resultados.</span><span class="sxs-lookup"><span data-stu-id="af0c6-124">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="af0c6-125">Además, el nombre de la empresa también se presenta en la llamada a la acción.</span><span class="sxs-lookup"><span data-stu-id="af0c6-125">In addition, the company name also shows up in the call to action.</span></span>

### <a name="call-to-action"></a><span data-ttu-id="af0c6-126">Llamada a la acción</span><span class="sxs-lookup"><span data-stu-id="af0c6-126">Call to action</span></span>
<span data-ttu-id="af0c6-127">La llamada a la acción consta de dos partes: explicar por qué el destinatario ha recibido el correo electrónico y qué se pide al destinatario que haga al respecto.</span><span class="sxs-lookup"><span data-stu-id="af0c6-127">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span></span>
- <span data-ttu-id="af0c6-128">La sección “por qué” puede seguir este patrón: Se le ha invitado a acceder a aplicaciones en la organización de &lt;nombreinquilino&gt;.</span><span class="sxs-lookup"><span data-stu-id="af0c6-128">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="af0c6-129">Y la sección “qué se le pide que haga” está indicada por la presencia del botón **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="af0c6-129">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span></span> <span data-ttu-id="af0c6-130">Cuando el destinatario se agrega sin necesidad de invitaciones, este botón no se muestra.</span><span class="sxs-lookup"><span data-stu-id="af0c6-130">When the recipient has been added without the need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="af0c6-131">Información sobre el invitador</span><span class="sxs-lookup"><span data-stu-id="af0c6-131">Inviter's information</span></span>
<span data-ttu-id="af0c6-132">El nombre para mostrar del invitador se incluye en el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="af0c6-132">The inviter's display name is included in the email.</span></span> <span data-ttu-id="af0c6-133">Y, además, si ha configurado una imagen de perfil para la cuenta de Azure AD, el correo electrónico de invitación incluye también esa imagen.</span><span class="sxs-lookup"><span data-stu-id="af0c6-133">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span></span> <span data-ttu-id="af0c6-134">Ambas opciones están diseñadas para aumentar la confianza del destinatario en el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="af0c6-134">Both are intended to increase your recipient's confidence in the email.</span></span>

<span data-ttu-id="af0c6-135">Si aún no ha configurado la imagen del perfil, se muestra un icono con las iniciales del invitador en lugar de la imagen:</span><span class="sxs-lookup"><span data-stu-id="af0c6-135">If you haven't yet set up your profile picture, an icon with the inviter's initials in place of the picture is shown:</span></span>

  ![mostrar las iniciales del invitador](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="af0c6-137">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="af0c6-137">Body</span></span>
<span data-ttu-id="af0c6-138">Contiene el mensaje que el invitador escribe o se transmite a través de la API de invitación.</span><span class="sxs-lookup"><span data-stu-id="af0c6-138">The body contains the message that the inviter composes or is passed through the invitation API.</span></span> <span data-ttu-id="af0c6-139">Al ser un área de texto, por motivos de seguridad no se procesan las etiquetas HTML.</span><span class="sxs-lookup"><span data-stu-id="af0c6-139">It is a text area, so it does not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="af0c6-140">Sección de pie de página</span><span class="sxs-lookup"><span data-stu-id="af0c6-140">Footer section</span></span>
<span data-ttu-id="af0c6-141">El pie de página contiene la marca de empresa de Microsoft y permite que el destinatario sepa si el correo electrónico se envía desde un alias no supervisado.</span><span class="sxs-lookup"><span data-stu-id="af0c6-141">The footer contains the Microsoft company brand and lets the recipient know if the email was sent from an unmonitored alias.</span></span> <span data-ttu-id="af0c6-142">Casos especiales:</span><span class="sxs-lookup"><span data-stu-id="af0c6-142">Special cases:</span></span>

- <span data-ttu-id="af0c6-143">El invitador no tiene una dirección de correo electrónico en el espacio empresarial invitador.</span><span class="sxs-lookup"><span data-stu-id="af0c6-143">The inviter doesn't have an email address in the inviting tenancy</span></span>

  ![La imagen no tiene una dirección de correo electrónico en el espacio empresarial invitador.](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="af0c6-145">El destinatario no necesita canjear la invitación.</span><span class="sxs-lookup"><span data-stu-id="af0c6-145">The recipient doesn't need to redeem the invitation</span></span>

  ![Si el destinatario no necesita canjear la invitación.](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="af0c6-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af0c6-147">Next steps</span></span>

<span data-ttu-id="af0c6-148">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="af0c6-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="af0c6-149">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="af0c6-149">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="af0c6-150">¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="af0c6-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="af0c6-151">¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="af0c6-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="af0c6-152">Canje de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="af0c6-152">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="af0c6-153">Concesión de licencias de colaboración B2B de Azure AD</span><span class="sxs-lookup"><span data-stu-id="af0c6-153">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="af0c6-154">Solución de problemas de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af0c6-154">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="af0c6-155">Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)</span><span class="sxs-lookup"><span data-stu-id="af0c6-155">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="af0c6-156">Personalización y API de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af0c6-156">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="af0c6-157">Autenticación multifactor para usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="af0c6-157">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="af0c6-158">Incorporación de usuarios de colaboración B2B sin invitación</span><span class="sxs-lookup"><span data-stu-id="af0c6-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="af0c6-159">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af0c6-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
