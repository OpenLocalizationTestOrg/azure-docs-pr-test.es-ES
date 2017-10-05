---
title: "Azure Multi-Factor Authentication - Cómo funciona"
description: "Azure Multi-Factor Authentication ayuda a proteger el acceso a los datos y las aplicaciones, además de satisfacer la demanda de los usuarios de un proceso de inicio de sesión simple. Proporciona seguridad adicional al requerir una segunda forma de autenticación y ofrece autenticación segura a través de una gama de opciones de comprobación sencillas."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 6fee02885cc76b3a4fdad11e8702f623d6fe6597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="e32a6-104">Cómo funciona Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e32a6-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="e32a6-105">La seguridad de la comprobación en pos pasos se basa en el enfoque por niveles.</span><span class="sxs-lookup"><span data-stu-id="e32a6-105">The security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="e32a6-106">El uso de varias fases de autenticación supone un reto importante para los atacantes.</span><span class="sxs-lookup"><span data-stu-id="e32a6-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="e32a6-107">Incluso si un atacante consigue descifrar la contraseña de usuario, no sirve de nada si no dispone también del dispositivo de confianza.</span><span class="sxs-lookup"><span data-stu-id="e32a6-107">Even if an attacker manages to learn the user's password, it is useless without also having possession of the trusted device.</span></span> 

![Página de proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="e32a6-109">Azure Multi-Factor Authentication ayuda a proteger el acceso a los datos y las aplicaciones, además de satisfacer la demanda de los usuarios de un proceso de inicio de sesión simple.</span><span class="sxs-lookup"><span data-stu-id="e32a6-109">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="e32a6-110">Proporciona seguridad adicional al requerir una segunda forma de autenticación y ofrece autenticación segura a través de una gama de opciones de comprobación sencillas.</span><span class="sxs-lookup"><span data-stu-id="e32a6-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="e32a6-111">Métodos disponibles para la verificación en dos pasos</span><span class="sxs-lookup"><span data-stu-id="e32a6-111">Methods available for two-step verification</span></span>
<span data-ttu-id="e32a6-112">Cuando un usuario inicia sesión, se envía una comprobación adicional al usuario.</span><span class="sxs-lookup"><span data-stu-id="e32a6-112">When a user signs in, an additional verification is sent to the user.</span></span>  <span data-ttu-id="e32a6-113">Lo siguiente es una lista de métodos que pueden usarse para esta segunda comprobación.</span><span class="sxs-lookup"><span data-stu-id="e32a6-113">The following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="e32a6-114">Método de comprobación</span><span class="sxs-lookup"><span data-stu-id="e32a6-114">Verification Method</span></span> | <span data-ttu-id="e32a6-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="e32a6-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e32a6-116">llamada de teléfono</span><span class="sxs-lookup"><span data-stu-id="e32a6-116">Phone call</span></span> |<span data-ttu-id="e32a6-117">Se realiza una llamada al teléfono registrado de un usuario.</span><span class="sxs-lookup"><span data-stu-id="e32a6-117">A call is placed to a user’s registered phone.</span></span> <span data-ttu-id="e32a6-118">El usuario escribe un PIN, si es necesario, y, a continuación, presiona la tecla #.</span><span class="sxs-lookup"><span data-stu-id="e32a6-118">The user enters a PIN if necessary then presses the # key.</span></span> |
| <span data-ttu-id="e32a6-119">mensaje de texto</span><span class="sxs-lookup"><span data-stu-id="e32a6-119">Text message</span></span> |<span data-ttu-id="e32a6-120">Se envía un mensaje de texto al teléfono móvil del usuario con un código de seis dígitos.</span><span class="sxs-lookup"><span data-stu-id="e32a6-120">A text message is sent to a user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="e32a6-121">El usuario escribe este código en la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e32a6-121">The user enters this code on the sign-in page.</span></span> |
| <span data-ttu-id="e32a6-122">Notificación en aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="e32a6-122">Mobile app notification</span></span> |<span data-ttu-id="e32a6-123">Se envía una solicitud de comprobación al smartphone de un usuario.</span><span class="sxs-lookup"><span data-stu-id="e32a6-123">A verification request is sent to a user’s smart phone.</span></span> <span data-ttu-id="e32a6-124">El usuario escribe un PIN, si es necesario, y, a continuación, selecciona **Comprobar** en la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="e32a6-124">The user enters a PIN if necessary then selects **Verify** on the mobile app.</span></span> |
| <span data-ttu-id="e32a6-125">Código de verificación de la aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="e32a6-125">Mobile app verification code</span></span> |<span data-ttu-id="e32a6-126">La aplicación móvil, que se ejecuta en el smartphone de un usuario, muestra un código de verificación que cambia cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="e32a6-126">The mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="e32a6-127">El usuario busca el código más reciente y lo escribe en la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e32a6-127">The user finds the most recent code and enters it on the sign-in page.</span></span> |
| <span data-ttu-id="e32a6-128">Tokens OATH de terceros</span><span class="sxs-lookup"><span data-stu-id="e32a6-128">Third-party OATH tokens</span></span> | <span data-ttu-id="e32a6-129">El Servidor Azure Multi-Factor Authentication puede configurarse para aceptar métodos de verificación de terceros.</span><span class="sxs-lookup"><span data-stu-id="e32a6-129">Azure Multi-Factor Authentication Server can be configured to accept third-party verification methods.</span></span> |

<span data-ttu-id="e32a6-130">Azure Multi-Factor Authentication proporciona métodos de comprobación seleccionables tanto para la nube y como para servidor.</span><span class="sxs-lookup"><span data-stu-id="e32a6-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="e32a6-131">Puede elegir qué métodos estarán disponibles para los usuarios: llamada telefónica, mensajes de texto, notificación en aplicación o códigos de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e32a6-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="e32a6-132">Para más información, vea [Métodos de comprobación seleccionables](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="e32a6-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e32a6-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e32a6-133">Next steps</span></span>

- <span data-ttu-id="e32a6-134">Obtenga información sobre las diferentes [versiones y métodos de utilización de Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md).</span><span class="sxs-lookup"><span data-stu-id="e32a6-134">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="e32a6-135">Elija si va a implementar Azure MFA [en la nube o de forma local](multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e32a6-135">Choose whether to deploy Azure MFA [in the cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="e32a6-136">Obtenga respuestas para las [Preguntas más frecuentes](multi-factor-authentication-faq.md).</span><span class="sxs-lookup"><span data-stu-id="e32a6-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>