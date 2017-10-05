---
title: "Configuración del registro automático de dispositivos unidos a un dominio de Windows con Azure Active Directory | Microsoft Docs"
description: "Configure sus dispositivos Windows unidos a un dominio para registrarse de forma automática y silenciosa en Azure Active Directory."
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
ms.openlocfilehash: 38750050e8525272079e1f3a5509da1e8f0a557b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="12492-103">Introducción al Registro de dispositivos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12492-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="12492-104">El Registro de dispositivos de Azure Active Directory es la base de los escenarios de acceso condicional basado en dispositivos.</span><span class="sxs-lookup"><span data-stu-id="12492-104">Azure Active Directory device registration is the foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="12492-105">Cuando se registra un dispositivo, el Registro de dispositivos de Azure Active Directory le proporciona una identidad que se utiliza para autenticar el dispositivo cuando el usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="12492-105">When a device is registered, Azure Active Directory device registration provides the device with an identity which is used to authenticate the device when the user signs in.</span></span> <span data-ttu-id="12492-106">El dispositivo autenticado y los atributos del dispositivo pueden utilizarse para aplicar directivas de acceso condicional para las aplicaciones que se hospedan en la nube y locales.</span><span class="sxs-lookup"><span data-stu-id="12492-106">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span></span>

<span data-ttu-id="12492-107">Cuando se combina con una solución de administración de dispositivos móviles (MDM) como Microsoft Intune, los atributos del dispositivo en Azure Active Directory se actualizan con información adicional sobre este.</span><span class="sxs-lookup"><span data-stu-id="12492-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span></span> <span data-ttu-id="12492-108">Esto le permite crear reglas de acceso condicional que obligan a que el acceso desde dispositivos cumpla con las normas de seguridad y cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="12492-108">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="12492-109">Para obtener más información sobre la inscripción de dispositivos de Microsoft Intune, consulte el artículo sobre cómo inscribir dispositivos para su administración en Intune.</span><span class="sxs-lookup"><span data-stu-id="12492-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="12492-110">Entre los escenarios que posibilita el Registro de dispositivos de Azure Active Directory se encuentra la compatibilidad con dispositivos Windows, iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="12492-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="12492-111">Los distintos escenarios que usan el Registro de dispositivos de Azure AD pueden tener requisitos y compatibilidad con la plataforma más específicos.</span><span class="sxs-lookup"><span data-stu-id="12492-111">The individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="12492-112">Estos escenarios son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="12492-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="12492-113">**Acceso condicional para aplicaciones de Office 365 con Microsoft Intune**: los administradores de TI pueden aprovisionar directivas de dispositivos de acceso condicional para proteger los recursos corporativos, al tiempo que permiten que los trabajadores de la información con dispositivos compatibles tengan acceso a los servicios.</span><span class="sxs-lookup"><span data-stu-id="12492-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies to secure corporate resources, while at the same time allowing information workers on compliant devices to access the services.</span></span> <span data-ttu-id="12492-114">Para más información, consulte las directivas de dispositivo de acceso condicional para los servicios de Office 365.</span><span class="sxs-lookup"><span data-stu-id="12492-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="12492-115">**Acceso condicional a las aplicaciones hospedadas localmente**: puede usar dispositivos registrados con directivas de acceso en las aplicaciones configuradas para usar AD FS con Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="12492-115">**Conditional access to applications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured to use AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="12492-116">Para obtener más información sobre cómo configurar el acceso condicional localmente, consulte [Configuración del acceso condicional local mediante el registro de dispositivos de Azure Active Directory](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="12492-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="12492-117">Configuración del Registro de dispositivos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12492-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="12492-118">Para configurar el Registro de dispositivos, tiene varias opciones:</span><span class="sxs-lookup"><span data-stu-id="12492-118">To setup device registration, you have multiple options:</span></span>

- <span data-ttu-id="12492-119">Los dispositivos se pueden registrar cuando se unen al dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12492-119">Devices can register when joined to Azure AD domain.</span></span> <span data-ttu-id="12492-120">Para obtener más información sobre este tema, puede leer sobre la unión a Azure AD y la configuración necesaria para que los usuarios se unan a un dominio de este tipo.</span><span class="sxs-lookup"><span data-stu-id="12492-120">For more on this topic, you can Learn more about Azure AD Join and the settings required for users to join Azure AD domain.</span></span>

- <span data-ttu-id="12492-121">Los dispositivos pueden registrarse cuando los usuarios agregan cuentas profesionales o educativas a Windows en un dispositivo personal, o bien cuando los dispositivos móviles se conectan a unos recursos de trabajo que precisan registrarse.</span><span class="sxs-lookup"><span data-stu-id="12492-121">Devices can be registered when users add work or school accounts to Windows on a personal device or when mobile devices connect to a work resources requiring registration.</span></span> <span data-ttu-id="12492-122">Para asegurarse de esto, debe habilitar el Registro de dispositivos de Azure AD en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="12492-122">To ensure this, you must enable Azure AD Device Registration in the Azure Portal.</span></span> 

- <span data-ttu-id="12492-123">Los dispositivos se pueden registrar con el registro automático de dispositivos en máquinas tradicionales unidas un dominio.</span><span class="sxs-lookup"><span data-stu-id="12492-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="12492-124">Para asegurarse de esto, debe primero configurar Azure AD Connect antes de continuar con el registro automático de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="12492-124">To ensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="12492-125">Para ver las instrucciones más recientes, consulte [Configuración del registro automático de dispositivos unidos a un dominio de Windows con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="12492-125">For latest instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="12492-126">También puede ver y habilitar o deshabilitar dispositivos registrados mediante el Portal de administrador de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12492-126">You can also review and enable or disable registered devices using the Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-the-azure-active-directory-device-registration-service"></a><span data-ttu-id="12492-127">Habilitación del servicio Registro de dispositivos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12492-127">Enable the Azure Active Directory device registration service</span></span>

<span data-ttu-id="12492-128">**Para habilitar el servicio Registro de dispositivos de Azure Active Directory, siga estos pasos**:</span><span class="sxs-lookup"><span data-stu-id="12492-128">**To enable the Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="12492-129">Inicie sesión como administrador en Microsoft Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="12492-129">Sign in to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="12492-130">En el panel izquierdo, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="12492-130">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="12492-131">En la pestaña Directorio, seleccione su directorio.</span><span class="sxs-lookup"><span data-stu-id="12492-131">On the Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="12492-132">Haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="12492-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="12492-133">Desplácese a **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="12492-133">Scroll to **Devices**.</span></span>

6.  <span data-ttu-id="12492-134">Seleccione TODO en LOS USUARIOS PUEDEN REGISTRAR SUS DISPOSITIVOS CON AZURE AD.</span><span class="sxs-lookup"><span data-stu-id="12492-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="12492-135">Seleccione el número máximo de dispositivos que quiere autorizar por usuario.</span><span class="sxs-lookup"><span data-stu-id="12492-135">Select the maximum number of devices you want to authorize per user.</span></span>

<span data-ttu-id="12492-136">La inscripción en Microsoft Intune o Administración de dispositivos móviles para Office 365 requiere la unión al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="12492-136">The enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="12492-137">Si configuró alguno de estos servicios, se seleccionará **TODOS** y se deshabilitará el botón **NINGUNO**.</span><span class="sxs-lookup"><span data-stu-id="12492-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="12492-138">Asegúrese de que se están configurados correctamente y tiene la licencia adecuada.</span><span class="sxs-lookup"><span data-stu-id="12492-138">Please ensure that they are configured correctly and have the appropriate licensing.</span></span>

<span data-ttu-id="12492-139">De forma predeterminada, la autenticación en dos fases no está habilitada para el servicio.</span><span class="sxs-lookup"><span data-stu-id="12492-139">By default, two-factor authentication is not enabled for the service.</span></span> <span data-ttu-id="12492-140">Aunque se recomienda usar la autenticación en dos fases al registrar un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12492-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="12492-141">Antes de requerir la autenticación en dos fases para este servicio, debe configurar un proveedor de autenticación en dos fases en Azure Active Directory y configurar las cuentas de usuario para Multi-Factor Authentication. Vea Adición de Multi-Factor Authentication a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12492-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication to Azure Active Directory</span></span>

- <span data-ttu-id="12492-142">Si utiliza AD FS con Windows Server 2012 R2, debe configurar un módulo de autenticación en dos fases en AD FS. Para ello consulte Utilización de Multi-Factor Authentication con Servicios de federación de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12492-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="12492-143">Visualización y administración de objetos de dispositivo en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12492-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="12492-144">En el Portal de administrador de Azure, puede ver, bloquear y desbloquear dispositivos.</span><span class="sxs-lookup"><span data-stu-id="12492-144">From the Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="12492-145">Un dispositivo bloqueado dejará de tener acceso a las aplicaciones configuradas para permitir solo dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="12492-145">A device that is blocked will no longer have access to applications that are configured to allow only registered devices.</span></span>

<span data-ttu-id="12492-146">**Para ver y administrar objetos de dispositivo en Azure Active Directory, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="12492-146">**To view and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="12492-147">Inicie sesión en Microsoft Azure Portal como administrador.</span><span class="sxs-lookup"><span data-stu-id="12492-147">Log on to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="12492-148">En el panel izquierdo, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="12492-148">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="12492-149">Seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="12492-149">Select your directory.</span></span>

4.  <span data-ttu-id="12492-150">Seleccione **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="12492-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="12492-151">Haga clic en el usuario para el que desea ver los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="12492-151">Click the user for which you want to see the devices.</span></span>

6.  <span data-ttu-id="12492-152">Seleccione **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="12492-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="12492-153">Seleccione **Dispositivos registrados**.</span><span class="sxs-lookup"><span data-stu-id="12492-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="12492-154">Ahora, puede ver, bloquear o desbloquear dispositivos registrados de usuarios.</span><span class="sxs-lookup"><span data-stu-id="12492-154">Now, you can review, block, or unblock the user's registered devices.</span></span>
<span data-ttu-id="12492-155">Los dispositivos Windows 10 que están unidos a un dominio local y se registran automáticamente no aparecen en la pestaña Usuarios.</span><span class="sxs-lookup"><span data-stu-id="12492-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under the Users tab.</span></span> <span data-ttu-id="12492-156">Use el comando Get-MsolDevice de PowerShell para buscar todos los dispositivos empresariales.</span><span class="sxs-lookup"><span data-stu-id="12492-156">Please use the Get-MsolDevice PowerShell command to find all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="12492-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12492-157">Next steps</span></span>

<span data-ttu-id="12492-158">Para configurar el registro de dispositivos automatizado, siga los pasos de [Configuración del registro automático de dispositivos unidos a un dominio de Windows con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="12492-158">To setup automated device registration, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


