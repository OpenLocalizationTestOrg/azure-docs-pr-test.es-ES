---
title: "aaaSet de un dispositivo Windows 10 con Azure AD desde configuración | Documentos de Microsoft"
description: "Explica cómo los usuarios pueden unirse tooAzure AD a través del menú de configuración de Hola."
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
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="68ae9-103">Configuración de un dispositivo de Windows 10 con Azure AD desde Configuración</span><span class="sxs-lookup"><span data-stu-id="68ae9-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="68ae9-104">Si ya está usando Windows 7 o Windows 8 y el equipo o dispositivo se ha actualizado tooWindows 10, puede combinar tooAzure Active Directory (Azure AD) a través del menú de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="68ae9-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded tooWindows 10, you can join tooAzure Active Directory (Azure AD) through hello Settings menu.</span></span>

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a><span data-ttu-id="68ae9-105">toojoin tooAzure AD desde el menú de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="68ae9-105">toojoin tooAzure AD from hello Settings menu</span></span>
1. <span data-ttu-id="68ae9-106">De hello **iniciar** menú, haga clic en hello **configuración** acceso.</span><span class="sxs-lookup"><span data-stu-id="68ae9-106">From hello **Start** menu, click hello **Settings** charm.</span></span>
2. <span data-ttu-id="68ae9-107">En **Configuración**, seleccione **Sistema**->**Acerca de**->**Unirse a Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="68ae9-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="68ae9-108"><center>
   ![Unirse a Azure AD desde el menú de configuración de hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="68ae9-108"><center>
![Join Azure AD from hello Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="68ae9-109">Haga clic en **continuar** en la ventana de mensaje de Hola Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="68ae9-109">Click **Continue** in hello Azure AD Join message window.</span></span>
   
   <span data-ttu-id="68ae9-110"><center>
   ![Ventana de mensaje de Unirse a Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center></span><span class="sxs-lookup"><span data-stu-id="68ae9-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="68ae9-111">Proporcione sus credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="68ae9-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="68ae9-112">Esta experiencia de inicio de sesión incluirá todos los pasos de hello toocomplete requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="68ae9-112">This sign-in experience will include all hello steps that are required toocomplete authentication.</span></span> <span data-ttu-id="68ae9-113">Si forma parte de un inquilino federado, el administrador le proporcionará experiencia de federación de Hola que está alojado en su organización.</span><span class="sxs-lookup"><span data-stu-id="68ae9-113">If you are part of a federated tenant, your administrator will provide you with hello federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="68ae9-114"><center>
   ![Proporcionar credenciales de inicio de sesión](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center></span><span class="sxs-lookup"><span data-stu-id="68ae9-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="68ae9-115">Si su organización ha configurado la autenticación multifactor Azure para combinar tooAzure AD, proporcione el segundo factor de hello antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="68ae9-115">If your organization has configured Azure Multi-Factor Authentication for joining tooAzure AD, provide hello second factor before proceeding.</span></span>
6. <span data-ttu-id="68ae9-116">Haga clic en **Accept** en hello **permitir este toobe dispositivo administrado** pantalla.</span><span class="sxs-lookup"><span data-stu-id="68ae9-116">Click **Accept** on hello **Allow this device toobe managed** screen.</span></span>
7. <span data-ttu-id="68ae9-117">Debería ver el mensaje de saludo "el dispositivo ya está combinadas tooyour organización en Azure AD".</span><span class="sxs-lookup"><span data-stu-id="68ae9-117">You should see hello message "Your device is now joined tooyour organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="68ae9-118">Información adicional</span><span class="sxs-lookup"><span data-stu-id="68ae9-118">Additional information</span></span>
* [<span data-ttu-id="68ae9-119">Conozca los escenarios de uso de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="68ae9-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="68ae9-120">Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10</span><span class="sxs-lookup"><span data-stu-id="68ae9-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="68ae9-121">Configuración de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="68ae9-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="68ae9-122">Autenticación de identidades sin contraseñas a través de Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="68ae9-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

