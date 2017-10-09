---
title: "aaaAzure la autenticación multifactor: cómo funciona"
description: "La autenticación multifactor Azure le ayuda a proteger acceso toodata y aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Proporciona seguridad adicional al requerir una segunda forma de autenticación y ofrece autenticación segura a través de una gama de opciones de comprobación sencillas."
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
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="f6646-104">Cómo funciona Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f6646-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="f6646-105">seguridad de Hola de verificación en dos pasos se encuentra en su enfoque por capas.</span><span class="sxs-lookup"><span data-stu-id="f6646-105">hello security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="f6646-106">El uso de varias fases de autenticación supone un reto importante para los atacantes.</span><span class="sxs-lookup"><span data-stu-id="f6646-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="f6646-107">Aunque un atacante administra la contraseña del usuario de toolearn hello, es inútil sin tiene en su posesión del dispositivo de confianza de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6646-107">Even if an attacker manages toolearn hello user's password, it is useless without also having possession of hello trusted device.</span></span> 

![Página de proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="f6646-109">La autenticación multifactor Azure le ayuda a proteger acceso toodata y aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple.</span><span class="sxs-lookup"><span data-stu-id="f6646-109">Azure Multi-Factor Authentication helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="f6646-110">Proporciona seguridad adicional al requerir una segunda forma de autenticación y ofrece autenticación segura a través de una gama de opciones de comprobación sencillas.</span><span class="sxs-lookup"><span data-stu-id="f6646-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="f6646-111">Métodos disponibles para la verificación en dos pasos</span><span class="sxs-lookup"><span data-stu-id="f6646-111">Methods available for two-step verification</span></span>
<span data-ttu-id="f6646-112">Cuando un usuario inicia sesión, una comprobación adicional se envía toohello usuario.</span><span class="sxs-lookup"><span data-stu-id="f6646-112">When a user signs in, an additional verification is sent toohello user.</span></span>  <span data-ttu-id="f6646-113">siguiente Hola es una lista de métodos que puede utilizarse para esta comprobación de segundo.</span><span class="sxs-lookup"><span data-stu-id="f6646-113">hello following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="f6646-114">Método de comprobación</span><span class="sxs-lookup"><span data-stu-id="f6646-114">Verification Method</span></span> | <span data-ttu-id="f6646-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="f6646-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6646-116">llamada de teléfono</span><span class="sxs-lookup"><span data-stu-id="f6646-116">Phone call</span></span> |<span data-ttu-id="f6646-117">Se realiza una llamada telefónica registrada del usuario tooa.</span><span class="sxs-lookup"><span data-stu-id="f6646-117">A call is placed tooa user’s registered phone.</span></span> <span data-ttu-id="f6646-118">usuario de Hello escribe un PIN si es necesario, a continuación, presiona la tecla # de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6646-118">hello user enters a PIN if necessary then presses hello # key.</span></span> |
| <span data-ttu-id="f6646-119">mensaje de texto</span><span class="sxs-lookup"><span data-stu-id="f6646-119">Text message</span></span> |<span data-ttu-id="f6646-120">Se envía un mensaje de texto móvil del usuario tooa con un código de seis dígitos.</span><span class="sxs-lookup"><span data-stu-id="f6646-120">A text message is sent tooa user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="f6646-121">usuario de Hello escribe este código en la página de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6646-121">hello user enters this code on hello sign-in page.</span></span> |
| <span data-ttu-id="f6646-122">Notificación en aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="f6646-122">Mobile app notification</span></span> |<span data-ttu-id="f6646-123">Teléfono inteligente del usuario tooa, se envía una solicitud de comprobación.</span><span class="sxs-lookup"><span data-stu-id="f6646-123">A verification request is sent tooa user’s smart phone.</span></span> <span data-ttu-id="f6646-124">Hello usuario escriba un PIN si es necesario, a continuación, selecciona **compruebe** en aplicaciones móviles de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6646-124">hello user enters a PIN if necessary then selects **Verify** on hello mobile app.</span></span> |
| <span data-ttu-id="f6646-125">Código de verificación de la aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="f6646-125">Mobile app verification code</span></span> |<span data-ttu-id="f6646-126">aplicación móvil de Hello, que se ejecuta en el teléfono inteligente de un usuario, muestra un código de comprobación que cambia cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="f6646-126">hello mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="f6646-127">usuario de Hello encuentra código más reciente de Hola y entra en la página de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6646-127">hello user finds hello most recent code and enters it on hello sign-in page.</span></span> |
| <span data-ttu-id="f6646-128">Tokens OATH de terceros</span><span class="sxs-lookup"><span data-stu-id="f6646-128">Third-party OATH tokens</span></span> | <span data-ttu-id="f6646-129">Servidor de Azure Multi-factor Authentication pueden ser métodos de comprobación de terceros de tooaccept configurado.</span><span class="sxs-lookup"><span data-stu-id="f6646-129">Azure Multi-Factor Authentication Server can be configured tooaccept third-party verification methods.</span></span> |

<span data-ttu-id="f6646-130">Azure Multi-Factor Authentication proporciona métodos de comprobación seleccionables tanto para la nube y como para servidor.</span><span class="sxs-lookup"><span data-stu-id="f6646-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="f6646-131">Puede elegir qué métodos estarán disponibles para los usuarios: llamada telefónica, mensajes de texto, notificación en aplicación o códigos de aplicación.</span><span class="sxs-lookup"><span data-stu-id="f6646-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="f6646-132">Para más información, vea [Métodos de comprobación seleccionables](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="f6646-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6646-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6646-133">Next steps</span></span>

- <span data-ttu-id="f6646-134">Hola diferentes que conozca [versiones y los métodos de consumo para la autenticación multifactor de Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="f6646-134">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="f6646-135">Elija si toodeploy Azure MFA [en la nube de Hola o de forma local](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="f6646-135">Choose whether toodeploy Azure MFA [in hello cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="f6646-136">Obtenga respuestas para las [Preguntas más frecuentes](multi-factor-authentication-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f6646-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>