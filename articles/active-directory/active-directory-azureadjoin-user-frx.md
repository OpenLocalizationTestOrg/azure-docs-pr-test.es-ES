---
title: "Configuración de un dispositivo nuevo con Azure AD durante la configuración | Microsoft Docs"
description: "Un tema que explica cómo los usuarios pueden configurar Azure AD Join durante su configuración rápida."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 4367f453ef7c794653dfa9f305b137a168e0d207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a><span data-ttu-id="cb563-103">Configuración de un dispositivo nuevo con Azure AD durante la configuración</span><span class="sxs-lookup"><span data-stu-id="cb563-103">Set up a new device with Azure AD during Setup</span></span>
<span data-ttu-id="cb563-104">En Windows 10, los usuarios pueden unir sus dispositivos a Azure Active Directory (Azure AD) en la Primera vista de Windows (FRX).</span><span class="sxs-lookup"><span data-stu-id="cb563-104">In Windows 10, users can join their devices to Azure Active Directory (Azure AD) in the first-run experience (FRX).</span></span> <span data-ttu-id="cb563-105">Esto permite que las organizaciones distribuyan dispositivos empaquetados a sus empleados o estudiantes, o bien permitirles elegir sus propios dispositivos (CYOD).</span><span class="sxs-lookup"><span data-stu-id="cb563-105">This allows organizations to distribute shrink-wrapped devices to their employees or students, or let them choose their own devices (CYOD).</span></span>
<span data-ttu-id="cb563-106">Si un dispositivo tiene instaladas las ediciones Windows 10 Professional o Windows 10 Enterprise, la experiencia predeterminada es el proceso de configuración de los dispositivos de empresa.</span><span class="sxs-lookup"><span data-stu-id="cb563-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, the experience defaults to the setup process for company-owned devices.</span></span>

## <a name="to-join-a-device-to-azure-ad"></a><span data-ttu-id="cb563-107">Para unir un dispositivo a Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb563-107">To join a device to Azure AD</span></span>
1. <span data-ttu-id="cb563-108">Al activar el nuevo dispositivo e iniciar el proceso de configuración, debería ver el mensaje **Preparación** .</span><span class="sxs-lookup"><span data-stu-id="cb563-108">When you turn on your new device and start the setup process, you should see the  **Getting Ready** message.</span></span> <span data-ttu-id="cb563-109">Siga las indicaciones para configurar el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cb563-109">Follow the prompts to set up your device.</span></span>
2. <span data-ttu-id="cb563-110">Para comenzar, personalice su región e idioma.</span><span class="sxs-lookup"><span data-stu-id="cb563-110">Start by customizing your region and language.</span></span> <span data-ttu-id="cb563-111">A continuación, acepte los términos de licencia del software de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cb563-111">Then accept the Microsoft Software License Terms.</span></span>
   <span data-ttu-id="cb563-112">![Personalizar para la región](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span><span class="sxs-lookup"><span data-stu-id="cb563-112">![Customize for your region](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span></span>
3. <span data-ttu-id="cb563-113">Seleccione la red que desea usar para conectarse a Internet.</span><span class="sxs-lookup"><span data-stu-id="cb563-113">Select the network you want to use for connecting to the Internet.</span></span>
4. <span data-ttu-id="cb563-114">Seleccione si usa un dispositivo personal o un dispositivo propiedad de la empresa.</span><span class="sxs-lookup"><span data-stu-id="cb563-114">Select whether you're using a personal device or a company-owned device.</span></span> <span data-ttu-id="cb563-115">Si es propiedad de la empresa, haga clic en **Este dispositivo pertenece a mi organización**.</span><span class="sxs-lookup"><span data-stu-id="cb563-115">If it's company-owned, click **This device belongs to my organization**.</span></span> <span data-ttu-id="cb563-116">Con esto comienza la experiencia de Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="cb563-116">This starts the Azure AD Join experience.</span></span> <span data-ttu-id="cb563-117">La siguiente pantalla aparece si usa Windows 10 Professional.</span><span class="sxs-lookup"><span data-stu-id="cb563-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span></span>
   <span data-ttu-id="cb563-118"><center>
   ![Pantalla ¿A quién pertenece el equipo?](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span><span class="sxs-lookup"><span data-stu-id="cb563-118"><center>
![Who owns this PC screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span></span>
5. <span data-ttu-id="cb563-119">Escriba las credenciales que le ha proporcionado la organización.</span><span class="sxs-lookup"><span data-stu-id="cb563-119">Enter the credentials that were provided to you by your organization.</span></span>
   <span data-ttu-id="cb563-120"><center>
   ![Pantalla de inicio de sesión](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span><span class="sxs-lookup"><span data-stu-id="cb563-120"><center>
![Sign-in screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span></span>
6. <span data-ttu-id="cb563-121">Después de que escriba su nombre de usuario, se coloca un inquilino coincidente en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb563-121">After you have entered your user name, a matching tenant is located in Azure AD.</span></span> <span data-ttu-id="cb563-122">Si se encuentra en un dominio federado, se le redirigirá al servidor del servicio de token seguro (STS) local; por ejemplo, Servicios de federación de Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="cb563-122">If you are in a federated domain, you will be redirected to your on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span></span>
7. <span data-ttu-id="cb563-123">Si es un usuario en un dominio no federado, deberá escribir las credenciales directamente en la página hospedada en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb563-123">If you are a user in a non-federated domain, enter your credentials directly on the Azure AD-hosted page.</span></span> <span data-ttu-id="cb563-124">Si se ha configurado la personalización de la marca, también verá el logotipo de la organización y texto complementario.</span><span class="sxs-lookup"><span data-stu-id="cb563-124">If company branding was configured, you will also see your organization’s logo and support text.</span></span>
8. <span data-ttu-id="cb563-125">A continuación, encontrará un desafío de Multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="cb563-125">You're prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="cb563-126">Este desafío puede configurarlo un administrador de TI.</span><span class="sxs-lookup"><span data-stu-id="cb563-126">This challenge is configurable by an IT administrator.</span></span>
9. <span data-ttu-id="cb563-127">Azure AD comprobará si este usuario/dispositivo requiere la inscripción en la administración de dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="cb563-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span></span>
10. <span data-ttu-id="cb563-128">Windows registra el dispositivo en el directorio de la organización en Azure AD y lo inscribe en la administración de dispositivos móviles, si procede.</span><span class="sxs-lookup"><span data-stu-id="cb563-128">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
11. <span data-ttu-id="cb563-129">Si es un usuario administrado, Windows le llevará al escritorio mediante el proceso de inicio de sesión automático.</span><span class="sxs-lookup"><span data-stu-id="cb563-129">If you are a managed user, Windows takes you to the desktop through the automatic sign-in process.</span></span>
12. <span data-ttu-id="cb563-130">Si es un usuario federado, verá la pantalla de inicio de sesión de Windows y deberá escribir sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="cb563-130">If you are a federated user, you are directed to the Windows sign-in screen to enter your credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="cb563-131">La configuración predeterminada de Windows no permite la unión a un dominio de Windows Server Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="cb563-131">Joining an on-premises Windows Server Active Directory domain in the Windows out-of-box experience is not supported.</span></span> <span data-ttu-id="cb563-132">Por lo tanto, si planea unir un equipo a un dominio, debe seleccionar en su lugar el vínculo **Configurar Windows con una cuenta local** .</span><span class="sxs-lookup"><span data-stu-id="cb563-132">Therefore, if you plan to join a computer to a domain, you should select the link **Set up Windows with a local account** instead.</span></span> <span data-ttu-id="cb563-133">Luego, puede unirse al dominio desde la configuración del equipo como ya lo hizo anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cb563-133">You can then join the domain from the settings on your computer as you’ve done before.</span></span>
> 
> 

## <a name="additional-information"></a><span data-ttu-id="cb563-134">Información adicional</span><span class="sxs-lookup"><span data-stu-id="cb563-134">Additional information</span></span>
* [<span data-ttu-id="cb563-135">Windows 10 para la empresa: formas de usar dispositivos para trabajar</span><span class="sxs-lookup"><span data-stu-id="cb563-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="cb563-136">Ampliación de las capacidades de nube a dispositivos de Windows 10 a través de Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="cb563-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="cb563-137">Autenticación de identidades sin contraseñas a través de Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="cb563-137">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="cb563-138">Conozca los escenarios de uso de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="cb563-138">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="cb563-139">Experiencias de conexión de dispositivos unidos a un dominio a Azure AD para Windows 10</span><span class="sxs-lookup"><span data-stu-id="cb563-139">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="cb563-140">Configuración de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="cb563-140">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

