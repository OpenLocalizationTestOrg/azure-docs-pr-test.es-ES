---
title: 'Windows 10 para empresa: formas de usar dispositivos para trabajar | Microsoft Docs'
description: "Información general de la implementación de dispositivos de Windows 10 para empresas y cómo integrarlos con Azure Active Directory para la nube de Windows. Compara las distintas formas de aprovisionar y usar un dispositivo en una empresa mediante el Portal de Azure."
keywords: nube de Windows, Windows en Azure Active Directory, dispositivos Windows 10 en Azure, dispositivos Windows en Azure
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2cb9ab6a-55b6-4658-b7f2-6e05ae015e1b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 804156048a7596f9937098e6fe762f424526473c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="windows-10-for-the-enterprise-ways-to-use-devices-for-work"></a><span data-ttu-id="683e0-105">Windows 10 para empresa: formas de usar dispositivos para trabajar</span><span class="sxs-lookup"><span data-stu-id="683e0-105">Windows 10 for the enterprise: Ways to use devices for work</span></span>
<span data-ttu-id="683e0-106">Windows 10 permite aprovechar Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="683e0-106">Windows 10 gives you the ability to leverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="683e0-107">Puede conectar dispositivos de Windows 10 a Azure AD y los usuarios pueden iniciar sesión en Windows con cuentas de Azure AD o agregando sus identificadores de Azure para acceder a los recursos y las aplicaciones empresariales.</span><span class="sxs-lookup"><span data-stu-id="683e0-107">You can connect Windows 10 devices to Azure AD so that users can sign in to Windows by using Azure AD accounts or by adding their Azure IDs to gain access to business apps and resources.</span></span>

![Azure Active Directory con servicios en la nube de Windows](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="683e0-109">Integración de dispositivos de Windows 10 con Azure Active Directory: mapa de contenidos</span><span class="sxs-lookup"><span data-stu-id="683e0-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="683e0-110">En los temas siguientes, se proporciona información de utilidad acerca de distintas funcionalidades de los dispositivos Windows 10 de su organización.</span><span class="sxs-lookup"><span data-stu-id="683e0-110">The following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="683e0-111">Temas</span><span class="sxs-lookup"><span data-stu-id="683e0-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="683e0-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="683e0-112">Getting started</span></span> |[<span data-ttu-id="683e0-113">Uso de dispositivos de Windows 10 en el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="683e0-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="683e0-114">Ampliación de las funcionalidades de nube a dispositivos de Windows 10 a través de Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="683e0-114">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="683e0-115">Autenticación de identidades sin contraseñas a través de Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="683e0-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="683e0-116">Implementación</span><span class="sxs-lookup"><span data-stu-id="683e0-116">Deployment</span></span> |[<span data-ttu-id="683e0-117">Escenarios de uso y consideraciones de implementación de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="683e0-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="683e0-118">Experiencias de conexión de dispositivos unidos a un dominio a Azure AD para Windows 10</span><span class="sxs-lookup"><span data-stu-id="683e0-118">Connecting domain-joined devices to Azure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="683e0-119">Habilitación de Microsoft Passport for Work en su organización</span><span class="sxs-lookup"><span data-stu-id="683e0-119">Enabling Microsoft Passport for work in the organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="683e0-120">Habilitación de Enterprise State Roaming para Windows 10</span><span class="sxs-lookup"><span data-stu-id="683e0-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="683e0-121">Tareas de usuario</span><span class="sxs-lookup"><span data-stu-id="683e0-121">User tasks</span></span> |[<span data-ttu-id="683e0-122">Configuración de un nuevo dispositivo de Windows 10 con Azure AD durante la instalación</span><span class="sxs-lookup"><span data-stu-id="683e0-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="683e0-123">Configuración de un dispositivo de Windows 10 con Azure AD desde el menú de configuración</span><span class="sxs-lookup"><span data-stu-id="683e0-123">Setting up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="683e0-124">Unión de un dispositivo de Windows 10 personal a su organización</span><span class="sxs-lookup"><span data-stu-id="683e0-124">Joining a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md) |

