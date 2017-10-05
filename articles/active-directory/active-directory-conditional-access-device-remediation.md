---
title: No puede llegar a un lugar desde otro lugar en Azure Portal desde un dispositivo Windows | Microsoft Docs
description: "Aprenda por qué no puede llegar a un lugar desde otro lugar y qué debe comprobar para evitar encontrarse con este cuadro de diálogo."
services: active-directory
keywords: acceso condicional basado en dispositivo, registro de dispositivo, habilitar registro de dispositivo, registro de dispositivo y MDM
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 16543c7bb7b6b236dcc24093c9963bc218ca1fa6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="2b171-104">No puede llegar ahí desde aquí en un dispositivo Windows</span><span class="sxs-lookup"><span data-stu-id="2b171-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="2b171-105">Durante un intento de, por ejemplo, acceder a la intranet de SharePoint Online de su organización puede llegar a una página que indique que *no se puede llegar a ese sitio desde este otro*.</span><span class="sxs-lookup"><span data-stu-id="2b171-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="2b171-106">Ve esta página porque el administrador ha configurado una directiva de acceso condicional que impide el acceso a los recursos de su organización en determinadas condiciones.</span><span class="sxs-lookup"><span data-stu-id="2b171-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access to your organization's resources under certain conditions.</span></span> <span data-ttu-id="2b171-107">Aunque puede que sea necesario que se ponga en contacto con el departamento de soporte técnico o con el administrador para solucionar el problema, antes de hacerlo puede probar varias cosas.</span><span class="sxs-lookup"><span data-stu-id="2b171-107">While it might be necessary to contact helpdesk or your administrator to get this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="2b171-108">Si usa un dispositivo con **Windows**, debe comprobar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2b171-108">If you are using a **Windows** device, you should check the following:</span></span>

- <span data-ttu-id="2b171-109">¿Usa un explorador compatible?</span><span class="sxs-lookup"><span data-stu-id="2b171-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="2b171-110">¿Ejecuta una versión compatible de Windows en el dispositivo?</span><span class="sxs-lookup"><span data-stu-id="2b171-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="2b171-111">¿Es compatible con el dispositivo?</span><span class="sxs-lookup"><span data-stu-id="2b171-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="2b171-112">Explorador compatible</span><span class="sxs-lookup"><span data-stu-id="2b171-112">Supported browser</span></span>

<span data-ttu-id="2b171-113">Si el administrador ha configurado una directiva de acceso condicional, solo puede acceder a los recursos de su organización mediante un explorador compatible.</span><span class="sxs-lookup"><span data-stu-id="2b171-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="2b171-114">En los dispositivos con Windows, solo se admiten **Internet Explorer** y **Edge**.</span><span class="sxs-lookup"><span data-stu-id="2b171-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="2b171-115">Es fácil identificar si no se puede acceder a un recurso debido a que el explorador no es compatible, solo hay que examinar la sección de detalles de la página de error:</span><span class="sxs-lookup"><span data-stu-id="2b171-115">You can easily identify whether you can't access a resource due to an unsupported browser by looking at the details section of the error page:</span></span>

<span data-ttu-id="2b171-116">![Mensaje "No se puede llegar allí desde aquí" para exploradores no admitidos](./media/active-directory-conditional-access-device-remediation/02.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="2b171-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="2b171-117">La única solución es utilizar un explorador compatible con la aplicación de la plataforma del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2b171-117">The only remediation is to use a browser that the application supports for your device platform.</span></span> <span data-ttu-id="2b171-118">Para obtener una lista completa de los exploradores compatibles, consulte la sección [Exploradores compatibles](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span><span class="sxs-lookup"><span data-stu-id="2b171-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="2b171-119">Versiones compatibles de Windows</span><span class="sxs-lookup"><span data-stu-id="2b171-119">Supported versions of Windows</span></span>

<span data-ttu-id="2b171-120">Las siguientes condiciones deben cumplirse en el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="2b171-120">The following must be true about the Windows operating system on your device:</span></span> 

- <span data-ttu-id="2b171-121">Si ejecuta un sistema operativo de equipo de escritorio Windows en el dispositivo, debe ser Windows 7, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="2b171-121">If you are running a Windows desktop operating system on your device, it needs to be Windows 7 or later.</span></span>
- <span data-ttu-id="2b171-122">Si ejecuta un sistema operativo Windows Server en el dispositivo, debe ser Windows Server 2008 R2, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="2b171-122">If you are running a Windows server operating system on your device, it needs to be Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="2b171-123">Dispositivos compatible</span><span class="sxs-lookup"><span data-stu-id="2b171-123">Compliant device</span></span>

<span data-ttu-id="2b171-124">El administrador puede haber configurado una directiva de acceso condicional que permite el acceso a los recursos de la organización solo desde dispositivos compatibles.</span><span class="sxs-lookup"><span data-stu-id="2b171-124">Your administrator might have configured a conditional access policy that allows access to your organization's resources only from compliant devices.</span></span> <span data-ttu-id="2b171-125">Para ser compatible, un dispositivo debe haberse unido a una versión local de Active Directory o a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b171-125">To be compliant, your device must be either joined to your on-premises Active Directory or joined to your Azure Active Directory.</span></span>

<span data-ttu-id="2b171-126">Es fácil identificar si no se puede acceder a un recurso debido a que el dispositivo no es compatible, solo hay que examinar la sección de detalles de la página de error:</span><span class="sxs-lookup"><span data-stu-id="2b171-126">You can easily identify whether you can't access a resource due to a device that is not compliant by looking at the details section of the error page:</span></span>
 
<span data-ttu-id="2b171-127">![Mensajes del tipo "No se puede llegar allí desde aquí" para dispositivos no registrados](./media/active-directory-conditional-access-device-remediation/01.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="2b171-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="2b171-128">¿Se ha unido el dispositivo a una versión local de Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b171-128">Is your device joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="2b171-129">**Si el dispositivo se ha unido a una versión local de Active Directory de la organización:**</span><span class="sxs-lookup"><span data-stu-id="2b171-129">**If your device is joined to an on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="2b171-130">Asegúrese de que ha iniciado sesión en Windows con su cuenta de trabajo (su cuenta de Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2b171-130">Make sure that you sign in to Windows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="2b171-131">Conéctese a su red corporativa a través de una red privada virtual (VPN) o DirectAccess.</span><span class="sxs-lookup"><span data-stu-id="2b171-131">Connect to your corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="2b171-132">Una vez conectado, bloquee la sesión de Windows presionando a la vez la tecla Windows y la tecla L.</span><span class="sxs-lookup"><span data-stu-id="2b171-132">After you are connected, press the Windows logo key + the L key to lock your Windows session.</span></span>
4. <span data-ttu-id="2b171-133">Desbloquee la sesión de Windows, para lo que debe especificar las credenciales de su cuenta profesional.</span><span class="sxs-lookup"><span data-stu-id="2b171-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="2b171-134">Espere un minuto e intente de nuevo acceder a la aplicación o servicio.</span><span class="sxs-lookup"><span data-stu-id="2b171-134">Wait for a minute, and then try again to access the application or service.</span></span>
6. <span data-ttu-id="2b171-135">Si aparece la misma página, haga clic en **Más detalles** y póngase en contacto con el administrador para informarle de los detalles.</span><span class="sxs-lookup"><span data-stu-id="2b171-135">If you see the same page, click the **More details** link, and then contact your administrator with the details.</span></span>


### <a name="is-your-device-not-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="2b171-136">¿No se ha unido el dispositivo a una versión local de Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b171-136">Is your device not joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="2b171-137">Si el dispositivo no se ha unido a una versión local Active Directory y ejecuta Windows 10, tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="2b171-137">If your device is not joined to an on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="2b171-138">Ejecutar Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="2b171-138">Run Azure AD Join</span></span>
* <span data-ttu-id="2b171-139">Agregar su cuenta profesional o educativa a Windows</span><span class="sxs-lookup"><span data-stu-id="2b171-139">Add your work or school account to Windows</span></span>

<span data-ttu-id="2b171-140">Para obtener información acerca de las diferencias entre estas opciones, consulte [Uso de dispositivos de Windows 10 en el área de trabajo](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="2b171-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="2b171-141">Si el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="2b171-141">If your device:</span></span>

- <span data-ttu-id="2b171-142">Pertenece a su organización, debe ejecutar Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="2b171-142">Belongs to your organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="2b171-143">Es un dispositivo personal o un teléfono Windows, debe agregar su cuenta profesional o educativa a Windows</span><span class="sxs-lookup"><span data-stu-id="2b171-143">Is a personal device or a Windows phone, you should add your work or school account to Windows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="2b171-144">Azure AD Join en Windows 10</span><span class="sxs-lookup"><span data-stu-id="2b171-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="2b171-145">Los pasos para unir un dispositivo a Azure AD están vinculados a la versión de Windows 10 en que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="2b171-145">The steps to join your device to Azure AD are tied the version of Windows 10 you are running on it.</span></span> <span data-ttu-id="2b171-146">Para determinar la versión del sistema operativo Windows 10, ejecute el comando **winver**:</span><span class="sxs-lookup"><span data-stu-id="2b171-146">To determine the version of your Windows 10 operating system, run the **winver** command:</span></span> 

![Versión de Windows](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="2b171-148">**Actualización de aniversario de Windows 10 (versión 1607):**</span><span class="sxs-lookup"><span data-stu-id="2b171-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="2b171-149">Abra la aplicación de **configuración** .</span><span class="sxs-lookup"><span data-stu-id="2b171-149">Open the **Settings** app.</span></span>
2. <span data-ttu-id="2b171-150">Haga clic en **Cuentas** > **Access work or school** (Acceder a la cuenta profesional o educativa).</span><span class="sxs-lookup"><span data-stu-id="2b171-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="2b171-151">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="2b171-151">Click **Connect**.</span></span>
4. <span data-ttu-id="2b171-152">Haga clic en **Join this device to Azure AD** (Conectar este dispositivo a Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b171-152">Click **Join this device to Azure AD**.</span></span>
5. <span data-ttu-id="2b171-153">Autentique su organización, proporcione Multi-Factor Authentication, si fuera necesario, y siga los pasos que se muestran.</span><span class="sxs-lookup"><span data-stu-id="2b171-153">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
6. <span data-ttu-id="2b171-154">Cierre la sesión y vuelva a iniciarla con su cuenta profesional.</span><span class="sxs-lookup"><span data-stu-id="2b171-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="2b171-155">Intente volver a acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b171-155">Try again to access the application.</span></span>

<span data-ttu-id="2b171-156">**Actualización de Windows de 10 de noviembre de 2015 (versión 1511):**</span><span class="sxs-lookup"><span data-stu-id="2b171-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="2b171-157">Abra la aplicación de **configuración** .</span><span class="sxs-lookup"><span data-stu-id="2b171-157">Open the **Settings** app.</span></span>
2. <span data-ttu-id="2b171-158">Haga clic en **Sistema** > **About** (Acerca de).</span><span class="sxs-lookup"><span data-stu-id="2b171-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="2b171-159">Haga clic en **Unirse a Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="2b171-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="2b171-160">Autentique su organización, proporcione Multi-Factor Authentication, si fuera necesario, y siga los pasos que se muestran.</span><span class="sxs-lookup"><span data-stu-id="2b171-160">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="2b171-161">Cierre la sesión y vuelva a iniciarla con su cuenta profesional (cuenta de Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b171-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="2b171-162">Intente volver a acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b171-162">Try again to access the application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="2b171-163">Workplace Join en Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="2b171-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="2b171-164">Si el dispositivo no está unido a un dominio y ejecuta Windows 8.1, para unirse al lugar de trabajo e inscribirse en Microsoft Intune, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2b171-164">If your device is not domain-joined and runs Windows 8.1, to do a Workplace Join and enroll in Microsoft Intune, do the following steps:</span></span>

1. <span data-ttu-id="2b171-165">Abra **Configuración de PC**.</span><span class="sxs-lookup"><span data-stu-id="2b171-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="2b171-166">Haga clic en **Red** > **Área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="2b171-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="2b171-167">Haga clic en **Unir**.</span><span class="sxs-lookup"><span data-stu-id="2b171-167">Click **Join**.</span></span>
4. <span data-ttu-id="2b171-168">Autentique su organización, proporcione Multi-Factor Authentication, si fuera necesario, y siga los pasos que se muestran.</span><span class="sxs-lookup"><span data-stu-id="2b171-168">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="2b171-169">Haga clic en **Activar**.</span><span class="sxs-lookup"><span data-stu-id="2b171-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="2b171-170">Intente volver a acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b171-170">Try again to access the application.</span></span>



#### <a name="add-your-work-or-school-account-to-windows"></a><span data-ttu-id="2b171-171">Agregar su cuenta profesional o educativa a Windows</span><span class="sxs-lookup"><span data-stu-id="2b171-171">Add your work or school account to Windows</span></span> 


<span data-ttu-id="2b171-172">**Actualización de aniversario de Windows 10 (versión 1607):**</span><span class="sxs-lookup"><span data-stu-id="2b171-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="2b171-173">Abra la aplicación de **configuración** .</span><span class="sxs-lookup"><span data-stu-id="2b171-173">Open the **Settings** app.</span></span>
2. <span data-ttu-id="2b171-174">Haga clic en **Cuentas** > **Access work or school** (Acceder a la cuenta profesional o educativa).</span><span class="sxs-lookup"><span data-stu-id="2b171-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="2b171-175">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="2b171-175">Click **Connect**.</span></span>
4. <span data-ttu-id="2b171-176">Autentique su organización, proporcione Multi-Factor Authentication, si fuera necesario, y siga los pasos que se muestran.</span><span class="sxs-lookup"><span data-stu-id="2b171-176">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="2b171-177">Intente volver a acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b171-177">Try again to access the application.</span></span>


<span data-ttu-id="2b171-178">**Actualización de Windows de 10 de noviembre de 2015 (versión 1511):**</span><span class="sxs-lookup"><span data-stu-id="2b171-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="2b171-179">Abra la aplicación de **configuración** .</span><span class="sxs-lookup"><span data-stu-id="2b171-179">Open the **Settings** app.</span></span>
2. <span data-ttu-id="2b171-180">Haga clic en **Cuentas** > **Your accounts** (Sus cuentas).</span><span class="sxs-lookup"><span data-stu-id="2b171-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="2b171-181">Haga clic en **Add work or school account**(Agregar cuenta profesional o educativa).</span><span class="sxs-lookup"><span data-stu-id="2b171-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="2b171-182">Autentique su organización, proporcione Multi-Factor Authentication, si fuera necesario, y siga los pasos que se muestran.</span><span class="sxs-lookup"><span data-stu-id="2b171-182">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="2b171-183">Intente volver a acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b171-183">Try again to access the application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="2b171-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2b171-184">Next steps</span></span>
[<span data-ttu-id="2b171-185">Acceso condicional de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b171-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

