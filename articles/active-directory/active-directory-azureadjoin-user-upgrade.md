---
title: "Configuración de un dispositivo de Windows 10 con Azure AD desde Configuración | Microsoft Docs"
description: "Explica cómo pueden los usuarios unirse a Azure AD a través del menú Configuración."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 5a3963f16b471ad1ca8681b22a1a027935400465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="4156f-103">Configuración de un dispositivo de Windows 10 con Azure AD desde Configuración</span><span class="sxs-lookup"><span data-stu-id="4156f-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="4156f-104">Si ya usa Windows 7 o Windows 8 y el equipo o dispositivo se ha actualizado a Windows 10, puede unirse a Azure Active Directory (Azure AD) a través del menú Configuración.</span><span class="sxs-lookup"><span data-stu-id="4156f-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.</span></span>

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a><span data-ttu-id="4156f-105">Para unirse a Azure AD desde el menú Configuración</span><span class="sxs-lookup"><span data-stu-id="4156f-105">To join to Azure AD from the Settings menu</span></span>
1. <span data-ttu-id="4156f-106">En el menú **Inicio**, haga clic en el acceso a **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="4156f-106">From the **Start** menu, click the **Settings** charm.</span></span>
2. <span data-ttu-id="4156f-107">En **Configuración**, seleccione **Sistema**->**Acerca de**->**Unirse a Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="4156f-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="4156f-108"><center>
   ![Unirse a Azure AD desde el menú Configuración](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span><span class="sxs-lookup"><span data-stu-id="4156f-108"><center>
![Join Azure AD from the Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="4156f-109">Haga clic en **Continuar** en la ventana de mensaje de Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="4156f-109">Click **Continue** in the Azure AD Join message window.</span></span>
   
   <span data-ttu-id="4156f-110"><center>
   ![Ventana de mensaje de Unirse a Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="4156f-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="4156f-111">Proporcione sus credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="4156f-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="4156f-112">Esta experiencia de inicio de sesión incluirá todos los pasos necesarios para completar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="4156f-112">This sign-in experience will include all the steps that are required to complete authentication.</span></span> <span data-ttu-id="4156f-113">Si forma parte de un inquilino federado, el administrador le brindará la experiencia de federación que hospeda su organización.</span><span class="sxs-lookup"><span data-stu-id="4156f-113">If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="4156f-114"><center>
   ![Proporcionar credenciales de inicio de sesión](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span><span class="sxs-lookup"><span data-stu-id="4156f-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="4156f-115">Si la organización ha configurado Azure Multi-Factor Authentication para unirse a Azure AD, proporcione el segundo factor para poder continuar.</span><span class="sxs-lookup"><span data-stu-id="4156f-115">If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.</span></span>
6. <span data-ttu-id="4156f-116">Haga clic en **Aceptar** en la pantalla **Permitir la administración de este dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="4156f-116">Click **Accept** on the **Allow this device to be managed** screen.</span></span>
7. <span data-ttu-id="4156f-117">Verá el mensaje "Su dispositivo se ha unido ahora a su organización en Azure AD".</span><span class="sxs-lookup"><span data-stu-id="4156f-117">You should see the message "Your device is now joined to your organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="4156f-118">Información adicional</span><span class="sxs-lookup"><span data-stu-id="4156f-118">Additional information</span></span>
* [<span data-ttu-id="4156f-119">Conozca los escenarios de uso de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="4156f-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="4156f-120">Experiencias de conexión de dispositivos unidos a un dominio a Azure AD para Windows 10</span><span class="sxs-lookup"><span data-stu-id="4156f-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="4156f-121">Configuración de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="4156f-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="4156f-122">Autenticación de identidades sin contraseñas a través de Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="4156f-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

