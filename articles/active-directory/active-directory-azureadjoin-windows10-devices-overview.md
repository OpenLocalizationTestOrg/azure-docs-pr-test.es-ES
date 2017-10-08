---
title: 'Windows 10 para empresa hello: dispositivos de toouse maneras para trabajo | Documentos de Microsoft'
description: "Información general de la implementación de dispositivos de Windows 10 para las empresas y cómo toointegrate con Azure Active Directory para hello Windows en la nube. Compara maneras diferentes de hello un dispositivo se pueden aprovisionar y usar en una empresa a través de hello portal de Azure."
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
ms.openlocfilehash: 95b452bc5ba3937e16de769275a59c77cb821e23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-10-for-hello-enterprise-ways-toouse-devices-for-work"></a><span data-ttu-id="31beb-105">Windows 10 para empresa hello: dispositivos de toouse de formas de trabajo</span><span class="sxs-lookup"><span data-stu-id="31beb-105">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>
<span data-ttu-id="31beb-106">Windows 10 proporciona Hola capacidad tooleverage Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31beb-106">Windows 10 gives you hello ability tooleverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="31beb-107">Puede conectar dispositivos de Windows 10 tooAzure AD para que los usuarios pueden iniciar sesión en tooWindows mediante cuentas de Azure AD o mediante la adición de sus identificadores de Azure toogain acceso toobusiness aplicaciones y recursos.</span><span class="sxs-lookup"><span data-stu-id="31beb-107">You can connect Windows 10 devices tooAzure AD so that users can sign in tooWindows by using Azure AD accounts or by adding their Azure IDs toogain access toobusiness apps and resources.</span></span>

![Azure Active Directory con servicios en la nube de Windows](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="31beb-109">Integración de dispositivos de Windows 10 con Azure Active Directory: mapa de contenidos</span><span class="sxs-lookup"><span data-stu-id="31beb-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="31beb-110">Hola temas siguientes proporciona una visión distintas capacidades de dispositivos de Windows 10 de su organización.</span><span class="sxs-lookup"><span data-stu-id="31beb-110">hello following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="31beb-111">Temas</span><span class="sxs-lookup"><span data-stu-id="31beb-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="31beb-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="31beb-112">Getting started</span></span> |[<span data-ttu-id="31beb-113">Uso de dispositivos de Windows 10 en el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="31beb-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="31beb-114">Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="31beb-114">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="31beb-115">Autenticación de identidades sin contraseñas a través de Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="31beb-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="31beb-116">Implementación</span><span class="sxs-lookup"><span data-stu-id="31beb-116">Deployment</span></span> |[<span data-ttu-id="31beb-117">Escenarios de uso y consideraciones de implementación de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="31beb-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="31beb-118">Experiencias de conectar dispositivos Unidos a dominio tooAzure AD, para Windows 10</span><span class="sxs-lookup"><span data-stu-id="31beb-118">Connecting domain-joined devices tooAzure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="31beb-119">Habilitar Microsoft Passport para el trabajo en la organización de Hola</span><span class="sxs-lookup"><span data-stu-id="31beb-119">Enabling Microsoft Passport for work in hello organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="31beb-120">Habilitación de Enterprise State Roaming para Windows 10</span><span class="sxs-lookup"><span data-stu-id="31beb-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="31beb-121">Tareas de usuario</span><span class="sxs-lookup"><span data-stu-id="31beb-121">User tasks</span></span> |[<span data-ttu-id="31beb-122">Configuración de un nuevo dispositivo de Windows 10 con Azure AD durante la instalación</span><span class="sxs-lookup"><span data-stu-id="31beb-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="31beb-123">Cómo configurar un dispositivo Windows 10 con Azure AD desde el menú de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="31beb-123">Setting up a Windows 10 device with Azure AD from hello settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="31beb-124">Unirse a una organización de tooyour de dispositivo de Windows 10 personal</span><span class="sxs-lookup"><span data-stu-id="31beb-124">Joining a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md) |

