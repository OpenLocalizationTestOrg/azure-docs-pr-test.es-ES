---
title: "aaaYou no se puede llegar allí desde aquí en hello portal de Azure desde un dispositivo Windows | Documentos de Microsoft"
description: "Obtenga información donde no existe desde aquí proceden de get y lo que podría comprobar tooavoid ejecutando en este cuadro de diálogo."
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
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="d0019-104">No puede llegar ahí desde aquí en un dispositivo Windows</span><span class="sxs-lookup"><span data-stu-id="d0019-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="d0019-105">Durante un intento de, por ejemplo, acceder a la intranet de SharePoint Online de su organización puede llegar a una página que indique que *no se puede llegar a ese sitio desde este otro*.</span><span class="sxs-lookup"><span data-stu-id="d0019-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="d0019-106">Está viendo esta página, porque el administrador ha configurado una directiva de acceso condicional que impide que los recursos de la organización de acceso tooyour bajo ciertas condiciones.</span><span class="sxs-lookup"><span data-stu-id="d0019-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access tooyour organization's resources under certain conditions.</span></span> <span data-ttu-id="d0019-107">Aunque puede que sea necesario toocontact departamento de soporte técnico o el tooget de administrador que resuelve este problema, hay algunas cosas que puede probar usted mismo, en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="d0019-107">While it might be necessary toocontact helpdesk or your administrator tooget this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="d0019-108">Si usas un **Windows** dispositivo, debe comprobar Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="d0019-108">If you are using a **Windows** device, you should check hello following:</span></span>

- <span data-ttu-id="d0019-109">¿Usa un explorador compatible?</span><span class="sxs-lookup"><span data-stu-id="d0019-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="d0019-110">¿Ejecuta una versión compatible de Windows en el dispositivo?</span><span class="sxs-lookup"><span data-stu-id="d0019-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="d0019-111">¿Es compatible con el dispositivo?</span><span class="sxs-lookup"><span data-stu-id="d0019-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="d0019-112">Explorador compatible</span><span class="sxs-lookup"><span data-stu-id="d0019-112">Supported browser</span></span>

<span data-ttu-id="d0019-113">Si el administrador ha configurado una directiva de acceso condicional, solo puede acceder a los recursos de su organización mediante un explorador compatible.</span><span class="sxs-lookup"><span data-stu-id="d0019-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="d0019-114">En los dispositivos con Windows, solo se admiten **Internet Explorer** y **Edge**.</span><span class="sxs-lookup"><span data-stu-id="d0019-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="d0019-115">Puede identificar fácilmente si no se puede tener acceso a un recurso debido explorador incompatible tooan examinando Hola detalles de la sección de página de error de hello:</span><span class="sxs-lookup"><span data-stu-id="d0019-115">You can easily identify whether you can't access a resource due tooan unsupported browser by looking at hello details section of hello error page:</span></span>

<span data-ttu-id="d0019-116">![Mensaje "No se puede llegar allí desde aquí" para exploradores no admitidos](./media/active-directory-conditional-access-device-remediation/02.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="d0019-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="d0019-117">corrección de Hello solo es toouse un explorador que admite la aplicación hello para la plataforma de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d0019-117">hello only remediation is toouse a browser that hello application supports for your device platform.</span></span> <span data-ttu-id="d0019-118">Para obtener una lista completa de los exploradores compatibles, consulte la sección [Exploradores compatibles](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span><span class="sxs-lookup"><span data-stu-id="d0019-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="d0019-119">Versiones compatibles de Windows</span><span class="sxs-lookup"><span data-stu-id="d0019-119">Supported versions of Windows</span></span>

<span data-ttu-id="d0019-120">deben cumplirse los siguientes Hola sobre el sistema de operativo de Windows hello en el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="d0019-120">hello following must be true about hello Windows operating system on your device:</span></span> 

- <span data-ttu-id="d0019-121">Si se ejecuta un sistema operativo de escritorio Windows en el dispositivo, debe toobe Windows 7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="d0019-121">If you are running a Windows desktop operating system on your device, it needs toobe Windows 7 or later.</span></span>
- <span data-ttu-id="d0019-122">Si se ejecuta un sistema operativo de Windows server en el dispositivo, debe toobe Windows Server 2008 R2 o posterior.</span><span class="sxs-lookup"><span data-stu-id="d0019-122">If you are running a Windows server operating system on your device, it needs toobe Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="d0019-123">Dispositivos compatible</span><span class="sxs-lookup"><span data-stu-id="d0019-123">Compliant device</span></span>

<span data-ttu-id="d0019-124">El administrador podría haber configurado una directiva de acceso condicional que permite que los recursos de la organización de acceso tooyour solo desde dispositivos compatibles.</span><span class="sxs-lookup"><span data-stu-id="d0019-124">Your administrator might have configured a conditional access policy that allows access tooyour organization's resources only from compliant devices.</span></span> <span data-ttu-id="d0019-125">toobe compatible, que el dispositivo debe ser cualquier tooyour unido a Active Directory local o unido tooyour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0019-125">toobe compliant, your device must be either joined tooyour on-premises Active Directory or joined tooyour Azure Active Directory.</span></span>

<span data-ttu-id="d0019-126">Puede identificar fácilmente si no se puede tener acceso a un recurso debido tooa dispositivo que no es compatible con examinando Hola detalles de la sección de página de error de hello:</span><span class="sxs-lookup"><span data-stu-id="d0019-126">You can easily identify whether you can't access a resource due tooa device that is not compliant by looking at hello details section of hello error page:</span></span>
 
<span data-ttu-id="d0019-127">![Mensajes del tipo "No se puede llegar allí desde aquí" para dispositivos no registrados](./media/active-directory-conditional-access-device-remediation/01.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="d0019-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="d0019-128">¿Es su tooan dispositivo unido a Active Directory local?</span><span class="sxs-lookup"><span data-stu-id="d0019-128">Is your device joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="d0019-129">**Si el dispositivo se une tooan en Active Directory local en su organización:**</span><span class="sxs-lookup"><span data-stu-id="d0019-129">**If your device is joined tooan on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="d0019-130">Asegúrese de que inicie sesión en tooWindows mediante su cuenta profesional (su cuenta de Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d0019-130">Make sure that you sign in tooWindows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="d0019-131">Conectar tooyour la red corporativa a través de una red privada virtual (VPN) o DirectAccess.</span><span class="sxs-lookup"><span data-stu-id="d0019-131">Connect tooyour corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="d0019-132">Cuando se haya conectado, presione la tecla del logotipo de Windows hello + toolock clave Hola L su sesión de Windows.</span><span class="sxs-lookup"><span data-stu-id="d0019-132">After you are connected, press hello Windows logo key + hello L key toolock your Windows session.</span></span>
4. <span data-ttu-id="d0019-133">Desbloquee la sesión de Windows, para lo que debe especificar las credenciales de su cuenta profesional.</span><span class="sxs-lookup"><span data-stu-id="d0019-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="d0019-134">Espere un minuto y, a continuación, vuelva a intentarlo tooaccess Hola aplicación o servicio.</span><span class="sxs-lookup"><span data-stu-id="d0019-134">Wait for a minute, and then try again tooaccess hello application or service.</span></span>
6. <span data-ttu-id="d0019-135">Si ve Hola misma página, haga clic en hello **detalles más** vincular y, a continuación, póngase en contacto con el Administrador con los detalles de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0019-135">If you see hello same page, click hello **More details** link, and then contact your administrator with hello details.</span></span>


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="d0019-136">¿Es el tooan de dispositivos no unidos a un Active Directory local?</span><span class="sxs-lookup"><span data-stu-id="d0019-136">Is your device not joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="d0019-137">Si el dispositivo no está unido tooan Active Directory local y ejecute Windows 10, tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="d0019-137">If your device is not joined tooan on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="d0019-138">Ejecutar Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="d0019-138">Run Azure AD Join</span></span>
* <span data-ttu-id="d0019-139">Agregar el trabajo o escuela tooWindows de cuenta</span><span class="sxs-lookup"><span data-stu-id="d0019-139">Add your work or school account tooWindows</span></span>

<span data-ttu-id="d0019-140">Para obtener información acerca de las diferencias entre estas opciones, consulte [Uso de dispositivos de Windows 10 en el área de trabajo](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="d0019-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="d0019-141">Si el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="d0019-141">If your device:</span></span>

- <span data-ttu-id="d0019-142">Pertenece tooyour organización, debe ejecutar Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="d0019-142">Belongs tooyour organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="d0019-143">Es un dispositivo personal o un dispositivo Windows phone, debe agregar su trabajo o escuela tooWindows de cuenta</span><span class="sxs-lookup"><span data-stu-id="d0019-143">Is a personal device or a Windows phone, you should add your work or school account tooWindows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="d0019-144">Azure AD Join en Windows 10</span><span class="sxs-lookup"><span data-stu-id="d0019-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="d0019-145">Hello toojoin pasos son los tooAzure dispositivo AD enlazado versión Hola de Windows 10 que se ejecuta en él.</span><span class="sxs-lookup"><span data-stu-id="d0019-145">hello steps toojoin your device tooAzure AD are tied hello version of Windows 10 you are running on it.</span></span> <span data-ttu-id="d0019-146">versión de hello toodetermine del sistema operativo Windows 10, ejecute hello **winver** comando:</span><span class="sxs-lookup"><span data-stu-id="d0019-146">toodetermine hello version of your Windows 10 operating system, run hello **winver** command:</span></span> 

![Versión de Windows](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="d0019-148">**Actualización de aniversario de Windows 10 (versión 1607):**</span><span class="sxs-lookup"><span data-stu-id="d0019-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="d0019-149">Abra hello **configuración** aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0019-149">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="d0019-150">Haga clic en **Cuentas** > **Access work or school** (Acceder a la cuenta profesional o educativa).</span><span class="sxs-lookup"><span data-stu-id="d0019-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="d0019-151">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="d0019-151">Click **Connect**.</span></span>
4. <span data-ttu-id="d0019-152">Haga clic en **unir este tooAzure dispositivo AD**.</span><span class="sxs-lookup"><span data-stu-id="d0019-152">Click **Join this device tooAzure AD**.</span></span>
5. <span data-ttu-id="d0019-153">Autenticar tooyour organización, proporcione la autenticación multifactor si se le pida y, a continuación, siga los pasos de Hola que se muestran.</span><span class="sxs-lookup"><span data-stu-id="d0019-153">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
6. <span data-ttu-id="d0019-154">Cierre la sesión y vuelva a iniciarla con su cuenta profesional.</span><span class="sxs-lookup"><span data-stu-id="d0019-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="d0019-155">Vuelva a intentarlo aplicación hello de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d0019-155">Try again tooaccess hello application.</span></span>

<span data-ttu-id="d0019-156">**Actualización de Windows de 10 de noviembre de 2015 (versión 1511):**</span><span class="sxs-lookup"><span data-stu-id="d0019-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="d0019-157">Abra hello **configuración** aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0019-157">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="d0019-158">Haga clic en **Sistema** > **About** (Acerca de).</span><span class="sxs-lookup"><span data-stu-id="d0019-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="d0019-159">Haga clic en **Unirse a Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="d0019-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="d0019-160">Autenticar tooyour organización, proporcione la autenticación multifactor si se le pida y, a continuación, siga los pasos de Hola que se muestran.</span><span class="sxs-lookup"><span data-stu-id="d0019-160">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="d0019-161">Cierre la sesión y vuelva a iniciarla con su cuenta profesional (cuenta de Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0019-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="d0019-162">Vuelva a intentarlo aplicación hello de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d0019-162">Try again tooaccess hello application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="d0019-163">Workplace Join en Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="d0019-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="d0019-164">Si el dispositivo no está unido a un dominio y ejecuta Windows 8.1, toodo una unión e inscribe en Microsoft Intune, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d0019-164">If your device is not domain-joined and runs Windows 8.1, toodo a Workplace Join and enroll in Microsoft Intune, do hello following steps:</span></span>

1. <span data-ttu-id="d0019-165">Abra **Configuración de PC**.</span><span class="sxs-lookup"><span data-stu-id="d0019-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="d0019-166">Haga clic en **Red** > **Área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="d0019-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="d0019-167">Haga clic en **Unir**.</span><span class="sxs-lookup"><span data-stu-id="d0019-167">Click **Join**.</span></span>
4. <span data-ttu-id="d0019-168">Autenticar tooyour organización, proporcione la autenticación multifactor si se le pida y, a continuación, siga los pasos de Hola que se muestran.</span><span class="sxs-lookup"><span data-stu-id="d0019-168">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="d0019-169">Haga clic en **Activar**.</span><span class="sxs-lookup"><span data-stu-id="d0019-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="d0019-170">Vuelva a intentarlo aplicación hello de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d0019-170">Try again tooaccess hello application.</span></span>



#### <a name="add-your-work-or-school-account-toowindows"></a><span data-ttu-id="d0019-171">Agregar el trabajo o escuela tooWindows de cuenta</span><span class="sxs-lookup"><span data-stu-id="d0019-171">Add your work or school account tooWindows</span></span> 


<span data-ttu-id="d0019-172">**Actualización de aniversario de Windows 10 (versión 1607):**</span><span class="sxs-lookup"><span data-stu-id="d0019-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="d0019-173">Abra hello **configuración** aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0019-173">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="d0019-174">Haga clic en **Cuentas** > **Access work or school** (Acceder a la cuenta profesional o educativa).</span><span class="sxs-lookup"><span data-stu-id="d0019-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="d0019-175">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="d0019-175">Click **Connect**.</span></span>
4. <span data-ttu-id="d0019-176">Autenticar tooyour organización, proporcione la autenticación multifactor si se le pida y, a continuación, siga los pasos de Hola que se muestran.</span><span class="sxs-lookup"><span data-stu-id="d0019-176">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="d0019-177">Vuelva a intentarlo aplicación hello de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d0019-177">Try again tooaccess hello application.</span></span>


<span data-ttu-id="d0019-178">**Actualización de Windows de 10 de noviembre de 2015 (versión 1511):**</span><span class="sxs-lookup"><span data-stu-id="d0019-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="d0019-179">Abra hello **configuración** aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0019-179">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="d0019-180">Haga clic en **Cuentas** > **Your accounts** (Sus cuentas).</span><span class="sxs-lookup"><span data-stu-id="d0019-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="d0019-181">Haga clic en **Add work or school account**(Agregar cuenta profesional o educativa).</span><span class="sxs-lookup"><span data-stu-id="d0019-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="d0019-182">Autenticar tooyour organización, proporcione la autenticación multifactor si se le pida y, a continuación, siga los pasos de Hola que se muestran.</span><span class="sxs-lookup"><span data-stu-id="d0019-182">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="d0019-183">Vuelva a intentarlo aplicación hello de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d0019-183">Try again tooaccess hello application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="d0019-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d0019-184">Next steps</span></span>
[<span data-ttu-id="d0019-185">Acceso condicional de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0019-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

