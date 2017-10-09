---
title: aaaSetting de Azure AD Join para los usuarios | Documentos de Microsoft
description: "Explica cómo pueden configurar los administradores Azure AD Join para el directorio local y el registro de dispositivos."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="0c68c-103">Configuración de Azure AD Join en su organización</span><span class="sxs-lookup"><span data-stu-id="0c68c-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="0c68c-104">Antes de configurar Azure Active Directory Join (Azure AD Join), necesita realizar la sincronización de tooeither su directorio local de la nube de los usuarios toohello una copia de seguridad o crear manualmente las cuentas administradas en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c68c-104">Before you set up Azure Active Directory Join (Azure AD Join), you need tooeither sync up your on-premises directory of users toohello cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="0c68c-105">Instrucciones detalladas para sincronizar su tooAzure de usuarios local AD se trata en [integrar las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="0c68c-105">Detailed instructions for syncing your on-premises users tooAzure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="0c68c-106">toomanually crear y administrar los usuarios en Azure AD, consulte demasiado[administración de usuarios en Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c68c-106">toomanually create and manage users in Azure AD, refer too[User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="0c68c-107">Configuración del registro de dispositivos</span><span class="sxs-lookup"><span data-stu-id="0c68c-107">Set up device registration</span></span>
1. <span data-ttu-id="0c68c-108">Inicie sesión en toohello portal de Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="0c68c-108">Log on toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="0c68c-109">En el panel izquierdo de hello, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0c68c-109">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="0c68c-110">En hello **Directory** ficha, seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="0c68c-110">On hello **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="0c68c-111">Seleccione hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="0c68c-111">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="0c68c-112">Vaya toohello **dispositivos** sección.</span><span class="sxs-lookup"><span data-stu-id="0c68c-112">Go toohello **Devices** section.</span></span>
6. <span data-ttu-id="0c68c-113">En hello **dispositivos** pestaña, configure Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="0c68c-113">On hello **devices** tab, set hello following:</span></span>  
   * <span data-ttu-id="0c68c-114">**MÁXIMO número de dispositivos por usuario**: seleccione Hola número máximo de dispositivos que puede tener un usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c68c-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select hello maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="0c68c-115">Si un usuario alcanza esta cuota, no estarán tooadd capaz de más dispositivos hasta que se quiten uno o varios de los dispositivos existentes.</span><span class="sxs-lookup"><span data-stu-id="0c68c-115">If a user reaches this quota, they will not be able tooadd additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="0c68c-116">**REQUERIR la autenticación MULTIFACTOR tooJOIN dispositivos**: establecer si los usuarios están tooprovide necesaria una segunda autenticación factor toojoin su tooAzure dispositivo AD.</span><span class="sxs-lookup"><span data-stu-id="0c68c-116">**REQUIRE MULTI-FACTOR AUTH tooJOIN DEVICES**: Set whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="0c68c-117">Para obtener más información acerca de la autenticación multifactor de Azure, consulte [Introducción a la autenticación multifactor Azure en la nube de hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="0c68c-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="0c68c-118">**Los usuarios pueden dispositivos de combinación de AZURE AD**: seleccione Hola usuarios y grupos que se permiten toojoin dispositivos tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="0c68c-118">**USERS MAY AZURE AD JOIN DEVICES**: Select hello users and groups that are allowed toojoin devices tooAzure AD.</span></span>
   * <span data-ttu-id="0c68c-119">**DISPOSITIVOS Unidos a otros administradores ON AZURE AD**: con Azure AD Premium u Hola Enterprise Mobility Suite (EMS), puede escoger qué usuarios tienen derechos de administrador local toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0c68c-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or hello Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights toohello device.</span></span> <span data-ttu-id="0c68c-120">De forma predeterminada, a los administradores globales y a los propietarios de dispositivos se les conceden derechos de administrador local.</span><span class="sxs-lookup"><span data-stu-id="0c68c-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="0c68c-121"><center>![Configuración del registro de dispositivos](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png)</center></span><span class="sxs-lookup"><span data-stu-id="0c68c-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="0c68c-122">Después de configurar Azure AD Join para los usuarios, puede conectar tooAzure AD a través de su empresa o dispositivos personales.</span><span class="sxs-lookup"><span data-stu-id="0c68c-122">After you set up Azure AD Join for your users, they can connect tooAzure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="0c68c-123">Continuación se muestran tres escenarios de hello puede usar tooenable su tooset a los usuarios de Azure AD Join:</span><span class="sxs-lookup"><span data-stu-id="0c68c-123">Following are hello three scenarios you can use tooenable your users tooset up Azure AD Join:</span></span>

* <span data-ttu-id="0c68c-124">Los usuarios unir un dispositivo propiedad de la empresa directamente tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="0c68c-124">Users join a company-owned device directly tooAzure AD.</span></span>
* <span data-ttu-id="0c68c-125">Toohello de dispositivo de una empresa de unión al dominio de los usuarios de Active Directory local y, después, ampliarla Hola dispositivo tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="0c68c-125">Users domain-join a company-owned device toohello on-premises Active Directory and then extend hello device tooAzure AD.</span></span>
* <span data-ttu-id="0c68c-126">Los usuarios agregar trabajo o escuela cuentas tooWindows en un dispositivo personal</span><span class="sxs-lookup"><span data-stu-id="0c68c-126">Users add work or school accounts tooWindows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="0c68c-127">Información adicional</span><span class="sxs-lookup"><span data-stu-id="0c68c-127">Additional information</span></span>
* [<span data-ttu-id="0c68c-128">Windows 10 para empresa hello: dispositivos de toouse de formas de trabajo</span><span class="sxs-lookup"><span data-stu-id="0c68c-128">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="0c68c-129">Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="0c68c-129">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="0c68c-130">Conozca los escenarios de uso de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="0c68c-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="0c68c-131">Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10</span><span class="sxs-lookup"><span data-stu-id="0c68c-131">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="0c68c-132">Configuración de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="0c68c-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

