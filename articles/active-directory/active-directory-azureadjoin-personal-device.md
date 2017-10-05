---
title: "Unión de un dispositivo personal a una organización | Microsoft Docs"
description: "Explica cómo los usuarios pueden registrar sus dispositivos personales con Windows 10 en su red corporativa, y se ofrecen pasos de implementación para un escenario BYOD."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a><span data-ttu-id="fc8c4-103">Unión de un dispositivo personal a su organización</span><span class="sxs-lookup"><span data-stu-id="fc8c4-103">Join a personal device to your organization</span></span>
## <a name="to-join-a-windows-10-device-to-your-organization"></a><span data-ttu-id="fc8c4-104">Para unir un dispositivo de Windows 10 a su organización</span><span class="sxs-lookup"><span data-stu-id="fc8c4-104">To join a Windows 10 device to your organization</span></span>
1. <span data-ttu-id="fc8c4-105">En el menú **Inicio**, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="fc8c4-105">From the **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="fc8c4-106">Seleccione **Cuentas** y luego haga clic en **Su cuenta**.</span><span class="sxs-lookup"><span data-stu-id="fc8c4-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="fc8c4-107">Haga clic en **Agregar cuenta profesional o educativa**y luego escriba su cuenta de organización.</span><span class="sxs-lookup"><span data-stu-id="fc8c4-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="fc8c4-108">En la página de inicio de sesión de su organización, escriba su nombre de usuario y contraseña y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fc8c4-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="fc8c4-109">A continuación, encontrará un desafío de autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="fc8c4-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="fc8c4-110">(Este desafío puede configurarlo un administrador de TI).</span><span class="sxs-lookup"><span data-stu-id="fc8c4-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="fc8c4-111">Azure Active Directory (Azure AD) comprueba si el dispositivo requiere la inscripción de administración de dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="fc8c4-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="fc8c4-112">Windows registra el dispositivo en el directorio de la organización en Azure AD y lo inscribe en la administración de dispositivos móviles, si procede.</span><span class="sxs-lookup"><span data-stu-id="fc8c4-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="fc8c4-113">Si es un usuario administrado, Windows le llevará al escritorio mediante el inicio de sesión automático.</span><span class="sxs-lookup"><span data-stu-id="fc8c4-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span></span>
9. <span data-ttu-id="fc8c4-114">Si es un usuario federado, verá la pantalla de inicio de sesión de Windows y deberá escribir sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="fc8c4-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="fc8c4-115">Información adicional</span><span class="sxs-lookup"><span data-stu-id="fc8c4-115">Additional information</span></span>
* [<span data-ttu-id="fc8c4-116">Windows 10 para la empresa: formas de usar dispositivos para trabajar</span><span class="sxs-lookup"><span data-stu-id="fc8c4-116">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="fc8c4-117">Ampliación de las capacidades de nube a dispositivos de Windows 10 a través de Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="fc8c4-117">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="fc8c4-118">Autenticación de identidades sin contraseñas a través de Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="fc8c4-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="fc8c4-119">Conozca los escenarios de uso de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="fc8c4-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="fc8c4-120">Experiencias de conexión de dispositivos unidos a un dominio a Azure AD para Windows 10</span><span class="sxs-lookup"><span data-stu-id="fc8c4-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="fc8c4-121">Configuración de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="fc8c4-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

