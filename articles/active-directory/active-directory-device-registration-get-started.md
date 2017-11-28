---
title: "aaaHow tooconfigure el registro automático de dispositivos Unidos a un dominio de Windows con Azure Active Directory | Documentos de Microsoft"
description: "Configurar los dispositivos de Windows Unidos a un dominio, tooregister automática y silenciosa con Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="fc44c-103">Introducción al Registro de dispositivos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc44c-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="fc44c-104">Registro de dispositivos de Azure Active Directory es la base de Hola para escenarios de acceso condicional basado en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fc44c-104">Azure Active Directory device registration is hello foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="fc44c-105">Cuando se registra un dispositivo, el registro de dispositivos de Azure Active Directory proporciona dispositivo Hola con una identidad que es el dispositivo de hello tooauthenticate usado cuando Hola usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="fc44c-105">When a device is registered, Azure Active Directory device registration provides hello device with an identity which is used tooauthenticate hello device when hello user signs in.</span></span> <span data-ttu-id="fc44c-106">dispositivo de Hello autenticado y los atributos de hello de dispositivo de hello, se pueden tooenforce usa directivas de acceso condicional para las aplicaciones que se hospedan en la nube de Hola y local.</span><span class="sxs-lookup"><span data-stu-id="fc44c-106">hello authenticated device, and hello attributes of hello device, can then be used tooenforce conditional access policies for applications that are hosted in hello cloud and on-premises.</span></span>

<span data-ttu-id="fc44c-107">Cuando se combina con una solución de management(MDM) de dispositivos móviles como Microsoft Intune, los atributos de dispositivo de hello en Azure Active Directory se actualizan con información adicional sobre el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc44c-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure Active Directory are updated with additional information about hello device.</span></span> <span data-ttu-id="fc44c-108">Esto permite que las reglas de acceso condicional de toocreate que exijan el acceso desde dispositivos toomeet los estándares de seguridad y cumplimiento de normas.</span><span class="sxs-lookup"><span data-stu-id="fc44c-108">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="fc44c-109">Para obtener más información sobre la inscripción de dispositivos de Microsoft Intune, consulte el artículo sobre cómo inscribir dispositivos para su administración en Intune.</span><span class="sxs-lookup"><span data-stu-id="fc44c-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="fc44c-110">Entre los escenarios que posibilita el Registro de dispositivos de Azure Active Directory se encuentra la compatibilidad con dispositivos Windows, iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="fc44c-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="fc44c-111">escenarios de individuales de Hola que utilizan el registro de dispositivos de Azure AD pueden tener compatibilidad con la plataforma y requisitos más específicos.</span><span class="sxs-lookup"><span data-stu-id="fc44c-111">hello individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="fc44c-112">Estos escenarios son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="fc44c-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="fc44c-113">**Acceso condicional para aplicaciones de Office 365 con Microsoft Intune:** administradores de TI pueden aprovisionar acceso condicional dispositivo directivas toosecure los recursos corporativos, mientras que en hello mismo tiempo permitir que los trabajadores de información en dispositivos compatibles Servicios de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="fc44c-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies toosecure corporate resources, while at hello same time allowing information workers on compliant devices tooaccess hello services.</span></span> <span data-ttu-id="fc44c-114">Para más información, consulte las directivas de dispositivo de acceso condicional para los servicios de Office 365.</span><span class="sxs-lookup"><span data-stu-id="fc44c-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="fc44c-115">**Tooapplications de acceso condicional que están hospedados en local:** puede utilizar dispositivos registrados con directivas de acceso para las aplicaciones que están configuradas toouse AD FS con Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="fc44c-115">**Conditional access tooapplications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured toouse AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="fc44c-116">Para obtener más información sobre cómo configurar el acceso condicional localmente, consulte [Configuración del acceso condicional local mediante el registro de dispositivos de Azure Active Directory](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="fc44c-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="fc44c-117">Configuración del Registro de dispositivos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc44c-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="fc44c-118">registro de dispositivos de toosetup, tiene varias opciones:</span><span class="sxs-lookup"><span data-stu-id="fc44c-118">toosetup device registration, you have multiple options:</span></span>

- <span data-ttu-id="fc44c-119">Pueden registrar dispositivos cuando AD de tooAzure Unidos a un dominio.</span><span class="sxs-lookup"><span data-stu-id="fc44c-119">Devices can register when joined tooAzure AD domain.</span></span> <span data-ttu-id="fc44c-120">Para obtener más información acerca de este tema, se puede obtener más información sobre la configuración de Azure AD Join y Hola necesaria para los usuarios de dominio toojoin Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc44c-120">For more on this topic, you can Learn more about Azure AD Join and hello settings required for users toojoin Azure AD domain.</span></span>

- <span data-ttu-id="fc44c-121">Cuando los usuarios agregar trabajo o escuela cuentas tooWindows en un dispositivo personal o cuando los dispositivos móviles conectan tooa los recursos de trabajo que requieren el registro, se pueden registrar dispositivos.</span><span class="sxs-lookup"><span data-stu-id="fc44c-121">Devices can be registered when users add work or school accounts tooWindows on a personal device or when mobile devices connect tooa work resources requiring registration.</span></span> <span data-ttu-id="fc44c-122">tooensure esto, debe habilitar el registro de dispositivos de Azure AD en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc44c-122">tooensure this, you must enable Azure AD Device Registration in hello Azure Portal.</span></span> 

- <span data-ttu-id="fc44c-123">Los dispositivos se pueden registrar con el registro automático de dispositivos en máquinas tradicionales unidas un dominio.</span><span class="sxs-lookup"><span data-stu-id="fc44c-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="fc44c-124">tooensure esto, debe primero el programa de instalación de Azure AD Connect antes de continuar con el registro automático de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="fc44c-124">tooensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="fc44c-125">Para obtener instrucciones más recientes, consulte [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="fc44c-125">For latest instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="fc44c-126">También puede revisar y habilitar o deshabilitar dispositivos registrados con hello Portal del administrador en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc44c-126">You can also review and enable or disable registered devices using hello Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-hello-azure-active-directory-device-registration-service"></a><span data-ttu-id="fc44c-127">Habilitar el servicio de registro de dispositivos de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="fc44c-127">Enable hello Azure Active Directory device registration service</span></span>

<span data-ttu-id="fc44c-128">**Hola tooenable servicio de registro de dispositivo de Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="fc44c-128">**tooenable hello Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="fc44c-129">Inicie sesión en toohello portal de Microsoft Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="fc44c-129">Sign in toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="fc44c-130">En el panel izquierdo de hello, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fc44c-130">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="fc44c-131">En la ficha directorio de hello, seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="fc44c-131">On hello Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="fc44c-132">Haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="fc44c-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="fc44c-133">Desplácese demasiado**dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="fc44c-133">Scroll too**Devices**.</span></span>

6.  <span data-ttu-id="fc44c-134">Seleccione TODO en LOS USUARIOS PUEDEN REGISTRAR SUS DISPOSITIVOS CON AZURE AD.</span><span class="sxs-lookup"><span data-stu-id="fc44c-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="fc44c-135">Seleccione el número máximo de Hola de dispositivos que desee tooauthorize por usuario.</span><span class="sxs-lookup"><span data-stu-id="fc44c-135">Select hello maximum number of devices you want tooauthorize per user.</span></span>

<span data-ttu-id="fc44c-136">inscripción de Hello con Microsoft Intune o administración de dispositivos móviles para Office 365 requiere el registro del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fc44c-136">hello enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="fc44c-137">Si configuró alguno de estos servicios, se seleccionará **TODOS** y se deshabilitará el botón **NINGUNO**.</span><span class="sxs-lookup"><span data-stu-id="fc44c-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="fc44c-138">Asegúrese de que estén configurados correctamente y que tiene licencias adecuadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc44c-138">Please ensure that they are configured correctly and have hello appropriate licensing.</span></span>

<span data-ttu-id="fc44c-139">De forma predeterminada, la autenticación en dos fases no está habilitada para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc44c-139">By default, two-factor authentication is not enabled for hello service.</span></span> <span data-ttu-id="fc44c-140">Aunque se recomienda usar la autenticación en dos fases al registrar un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fc44c-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="fc44c-141">Antes de requerir la autenticación en dos fases para este servicio, debe configurar un proveedor de autenticación en dos fases en Azure Active Directory y configurar las cuentas de usuario para la autenticación multifactor, consulte Agregar la autenticación multifactor tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc44c-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication tooAzure Active Directory</span></span>

- <span data-ttu-id="fc44c-142">Si utiliza AD FS con Windows Server 2012 R2, debe configurar un módulo de autenticación en dos fases en AD FS. Para ello consulte Utilización de Multi-Factor Authentication con Servicios de federación de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc44c-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="fc44c-143">Visualización y administración de objetos de dispositivo en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc44c-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="fc44c-144">Desde el portal de administración de Azure de hello, puede ver, bloquear y desbloquear dispositivos.</span><span class="sxs-lookup"><span data-stu-id="fc44c-144">From hello Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="fc44c-145">Un dispositivo bloqueado dejará de tener acceso tooapplications que están configurados tooallow solo los dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="fc44c-145">A device that is blocked will no longer have access tooapplications that are configured tooallow only registered devices.</span></span>

<span data-ttu-id="fc44c-146">**tooview y administrar objetos de dispositivo en Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="fc44c-146">**tooview and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="fc44c-147">Inicie sesión en toohello portal de Microsoft Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="fc44c-147">Log on toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="fc44c-148">En el panel izquierdo de hello, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fc44c-148">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="fc44c-149">Seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="fc44c-149">Select your directory.</span></span>

4.  <span data-ttu-id="fc44c-150">Seleccione **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fc44c-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="fc44c-151">Haga clic en usuario de hello para el que desea que los dispositivos de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="fc44c-151">Click hello user for which you want toosee hello devices.</span></span>

6.  <span data-ttu-id="fc44c-152">Seleccione **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="fc44c-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="fc44c-153">Seleccione **Dispositivos registrados**.</span><span class="sxs-lookup"><span data-stu-id="fc44c-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="fc44c-154">Ahora, puede revisar, bloquear o desbloquear dispositivos registrados del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc44c-154">Now, you can review, block, or unblock hello user's registered devices.</span></span>
<span data-ttu-id="fc44c-155">Dispositivos de Windows 10 que están unidos a un dominio y se registren automáticamente en las instalaciones no aparecen en la ficha de usuarios de Hola. Use toofind de comandos de PowerShell Get-MsolDevice Hola todos los dispositivos de su empresa.</span><span class="sxs-lookup"><span data-stu-id="fc44c-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under hello Users tab. Please use hello Get-MsolDevice PowerShell command toofind all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="fc44c-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc44c-156">Next steps</span></span>

<span data-ttu-id="fc44c-157">toosetup automatizada registro de dispositivos, consulte [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="fc44c-157">toosetup automated device registration, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


