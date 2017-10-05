---
title: "Inicio de sesión único de conexión directa de Azure AD Connect: Quía de inicio rápido | Microsoft Docs"
description: "En este artículo se describe cómo empezar a trabajar con el inicio de sesión único de conexión directa de Azure Active Directory."
services: active-directory
keywords: "qué es Azure AD Connect, instalar Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 977108687734a5eb7f7a30419de2a6bdef184d0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="21ac5-104">Inicio de sesión único de conexión directa de Azure Active Directory: Guía de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="21ac5-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-to-deploy-seamless-sso"></a><span data-ttu-id="21ac5-105">Implementación de SSO de conexión directa</span><span class="sxs-lookup"><span data-stu-id="21ac5-105">How to deploy Seamless SSO</span></span>

<span data-ttu-id="21ac5-106">El inicio de sesión único de conexión directa de Azure Active Directory (SSO de conexión directa de Azure AD) permite iniciar sesión automáticamente a los usuarios en equipos de escritorio corporativos conectados a la red de la empresa.</span><span class="sxs-lookup"><span data-stu-id="21ac5-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected to your corporate network.</span></span> <span data-ttu-id="21ac5-107">Esta característica proporciona a los usuarios un acceso sencillo a las aplicaciones en la nube sin necesidad de otros componentes locales.</span><span class="sxs-lookup"><span data-stu-id="21ac5-107">It provides your users easy access to your cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="21ac5-108">La característica de SSO de conexión directa está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="21ac5-108">The Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="21ac5-109">Para implementar SSO de conexión directa, debe seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="21ac5-109">To deploy Seamless SSO, you need to follow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="21ac5-110">Paso 1: Comprobación de los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="21ac5-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="21ac5-111">Asegúrese de que se cumplen los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="21ac5-111">Ensure that the following prerequisites are in place:</span></span>

1. <span data-ttu-id="21ac5-112">El servidor de Azure AD Connect está configurado: si usa la [autenticación de paso a través](active-directory-aadconnect-pass-through-authentication.md) como método de inicio de sesión, no es necesaria realizar ninguna otra acción.</span><span class="sxs-lookup"><span data-stu-id="21ac5-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="21ac5-113">Si va a usar la [sincronización de hash de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) como método de inicio de sesión y hay un firewall entre Azure AD Connect y Azure AD, asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="21ac5-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="21ac5-114">Está usando la versión 1.1.484.0 de Azure AD Connect o una posterior.</span><span class="sxs-lookup"><span data-stu-id="21ac5-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="21ac5-115">Azure AD Connect puede comunicarse con las direcciones URL de `*.msappproxy.net` y a través del puerto 443.</span><span class="sxs-lookup"><span data-stu-id="21ac5-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="21ac5-116">Este requisito solo es aplicable cuando se habilita la característica, no para los inicios de sesión de usuarios reales.</span><span class="sxs-lookup"><span data-stu-id="21ac5-116">This prerequisite is applicable only when you enable the feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="21ac5-117">Azure AD Connect también puede crear conexiones IP directas con los [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="21ac5-117">Azure AD Connect can make direct IP connections to the [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="21ac5-118">De nuevo, este requisito solo es aplicable cuando se habilita la característica.</span><span class="sxs-lookup"><span data-stu-id="21ac5-118">Again, this prerequisite is applicable only when you enable the feature.</span></span>
2. <span data-ttu-id="21ac5-119">Tendrá que especificar las credenciales de administrador de dominio para cada bosque de AD que sincronice con Azure AD (a través de Azure AD Connect) y para cuyos usuarios desee habilitar SSO de conexión directa.</span><span class="sxs-lookup"><span data-stu-id="21ac5-119">You need Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span>

## <a name="step-2-enable-the-feature"></a><span data-ttu-id="21ac5-120">Paso 2: Habilitación de la característica</span><span class="sxs-lookup"><span data-stu-id="21ac5-120">Step 2: Enable the feature</span></span>

<span data-ttu-id="21ac5-121">SSO de conexión directa se puede habilitar a través de [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="21ac5-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="21ac5-122">Si va a realizar una instalación nueva de Azure AD Connect, elija la [ruta de acceso de instalación personalizada](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="21ac5-122">If you are doing a fresh installation of Azure AD Connect, choose the [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="21ac5-123">En la página "Inicio de sesión de usuario", active la opción "Habilitar el inicio de sesión único".</span><span class="sxs-lookup"><span data-stu-id="21ac5-123">At the "User sign-in" page, check the "Enable single sign on" option.</span></span>

![Azure AD Connect: Inicio de sesión de usuario](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="21ac5-125">Si ya tiene una instalación de Azure AD Connect, elija "Change user sign-in page" (Cambiar página de inicio de sesión del usuario) en Azure AD Connect y haga clic en "Siguiente".</span><span class="sxs-lookup"><span data-stu-id="21ac5-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="21ac5-126">A continuación, active la opción "Habilitar el inicio de sesión único".</span><span class="sxs-lookup"><span data-stu-id="21ac5-126">Then check the "Enable single sign on" option.</span></span>

![Azure AD Connect: Change user sign-in page (Cambiar página de inicio de sesión del usuario)](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="21ac5-128">Continúe con el asistente hasta llegar a la página "Habilitar el inicio de sesión único".</span><span class="sxs-lookup"><span data-stu-id="21ac5-128">Continue through the wizard until you get to the "Enable single sign on" page.</span></span> <span data-ttu-id="21ac5-129">Especifique las credenciales de administrador de dominio para cada bosque de AD que sincronice con Azure AD (a través de Azure AD Connect) y para cuyos usuarios desee habilitar SSO de conexión directa.</span><span class="sxs-lookup"><span data-stu-id="21ac5-129">Provide Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span> 

<span data-ttu-id="21ac5-130">Cuando haya finalizado con el asistente, el SSO de conexión directa estará habilitado en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="21ac5-130">After completion of the wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="21ac5-131">Las credenciales de administrador de dominio no se almacenan en Azure AD Connect ni en Azure AD, sino que solo se usan para habilitar la característica.</span><span class="sxs-lookup"><span data-stu-id="21ac5-131">The Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used to enable the feature.</span></span>

<span data-ttu-id="21ac5-132">Siga estas instrucciones para verificar que ha habilitado SSO de conexión directa correctamente:</span><span class="sxs-lookup"><span data-stu-id="21ac5-132">Follow these instructions to verify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="21ac5-133">Inicie sesión en el [Centro de administración de Azure Active Directory](https://aad.portal.azure.com) con las credenciales de administrador global del inquilino.</span><span class="sxs-lookup"><span data-stu-id="21ac5-133">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with the Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="21ac5-134">Seleccione **Azure Active Directory** en la barra de navegación de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="21ac5-134">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="21ac5-135">Seleccione **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="21ac5-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="21ac5-136">Verifique que la característica de **Inicio de sesión único de conexión directa** aparece como **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="21ac5-136">Verify that the **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Azure Portal: hoja Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-the-feature"></a><span data-ttu-id="21ac5-138">Paso 3: Implementación de la característica</span><span class="sxs-lookup"><span data-stu-id="21ac5-138">Step 3: Roll out the feature</span></span>

<span data-ttu-id="21ac5-139">Para implementar la característica para los usuarios, debe agregar dos direcciones URL de Azure AD (https://autologon.microsoftazuread-sso.com y https://aadg.windows.net.nsatc.net) en la configuración de zona de intranet de los usuarios a través de una directiva de grupo en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="21ac5-139">To roll out the feature to your users, you need to add two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) to users' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="21ac5-140">Las siguientes instrucciones solo funcionan en Internet Explorer y Google Chrome en Windows (si comparte el mismo conjunto de direcciones URL de sitios de confianza que Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="21ac5-140">The following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="21ac5-141">Lea la sección siguiente para obtener instrucciones para configurar Mozilla Firefox y Google Chrome en Mac.</span><span class="sxs-lookup"><span data-stu-id="21ac5-141">Read the next section for instructions to set up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-to-modify-users-intranet-zone-settings"></a><span data-ttu-id="21ac5-142">¿Por qué es necesario modificar la configuración de zona de Intranet de los usuarios?</span><span class="sxs-lookup"><span data-stu-id="21ac5-142">Why do you need to modify users' Intranet zone settings?</span></span>

<span data-ttu-id="21ac5-143">De forma predeterminada, el explorador calcula automáticamente la zona correcta (Internet o intranet) de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="21ac5-143">By default, the browser automatically calculates the right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="21ac5-144">Por ejemplo, http://contoso/ se asignará a la zona de intranet, mientras que http://intranet.contoso.com/ se asignará a la zona de Internet (porque la dirección URL contiene un punto).</span><span class="sxs-lookup"><span data-stu-id="21ac5-144">For example, http://contoso/ is mapped to the Intranet zone, whereas http://intranet.contoso.com/ is mapped to the Internet zone (because the URL contains a period).</span></span> <span data-ttu-id="21ac5-145">Los exploradores no envían vales Kerberos a un punto de conexión en la nube, como las dos direcciones URL de Azure, a menos que su dirección URL se agregue explícitamente a la zona de intranet del explorador.</span><span class="sxs-lookup"><span data-stu-id="21ac5-145">Browsers don't send Kerberos tickets to a cloud endpoint - like the two Azure AD URLs - unless its URL is explicitly added to the browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="21ac5-146">Pasos detallados</span><span class="sxs-lookup"><span data-stu-id="21ac5-146">Detailed steps</span></span>

1. <span data-ttu-id="21ac5-147">Abra las herramientas de administración de directivas de grupo.</span><span class="sxs-lookup"><span data-stu-id="21ac5-147">Open the Group Policy Management tool.</span></span>
2. <span data-ttu-id="21ac5-148">Edite la directiva de grupo que se aplica a algunos o todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="21ac5-148">Edit the Group Policy that is applied to some or all your users.</span></span> <span data-ttu-id="21ac5-149">En este ejemplo, se usa la **directiva de dominio predeterminada**.</span><span class="sxs-lookup"><span data-stu-id="21ac5-149">In this example, we use the **Default Domain Policy**.</span></span>
3. <span data-ttu-id="21ac5-150">Vaya a **User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** y seleccione **Site to Zone Assignment List** (Lista de asignación de sitio a zona).</span><span class="sxs-lookup"><span data-stu-id="21ac5-150">Navigate to **User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site to Zone Assignment List**.</span></span>
<span data-ttu-id="21ac5-151">![Inicio de sesión único](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="21ac5-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="21ac5-152">Habilite la directiva y escriba los siguientes valores (direcciones URL de Azure AD desde donde se reenvían los vales de Kerberos) y los datos (*1* indica la zona de Intranet) en el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="21ac5-152">Enable the policy, and enter the following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in the dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="21ac5-153">Si no desea permitir que algunos usuarios usen SSO de conexión directa (por ejemplo, si estos usuarios inician sesión en quioscos compartidos) establezca los valores anteriores en *4*.</span><span class="sxs-lookup"><span data-stu-id="21ac5-153">If you want to disallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set the preceding values to *4*.</span></span> <span data-ttu-id="21ac5-154">De este modo, agrega las direcciones URL de AD Azure a la zona Sitios restringidos y el SSO de conexión directa no puede conectar a esos usuarios.</span><span class="sxs-lookup"><span data-stu-id="21ac5-154">This action adds the Azure AD URLs to the Restricted Zone, and fails Seamless SSO all the time.</span></span>

5. <span data-ttu-id="21ac5-155">Haga clic en **Aceptar** y en **Aceptar** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="21ac5-155">Click **OK** and **OK** again.</span></span>

![Inicio de sesión único](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="21ac5-157">Consideraciones sobre el explorador</span><span class="sxs-lookup"><span data-stu-id="21ac5-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="21ac5-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="21ac5-158">Mozilla Firefox</span></span>

<span data-ttu-id="21ac5-159">Mozilla Firefox no realiza automáticamente la autenticación Kerberos.</span><span class="sxs-lookup"><span data-stu-id="21ac5-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="21ac5-160">Cada usuario tiene que agregar manualmente las direcciones URL de Azure AD a su configuración de Firefox siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="21ac5-160">Each user has to manually add the Azure AD URLs to their Firefox settings using the following steps:</span></span>
1. <span data-ttu-id="21ac5-161">Ejecute Firefox y escriba `about:config` en la barra de direcciones.</span><span class="sxs-lookup"><span data-stu-id="21ac5-161">Run Firefox and enter `about:config` in the address bar.</span></span> <span data-ttu-id="21ac5-162">Descarte las notificaciones que vea.</span><span class="sxs-lookup"><span data-stu-id="21ac5-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="21ac5-163">Busque la preferencia **network.negotiate-auth.trusted-URI**.</span><span class="sxs-lookup"><span data-stu-id="21ac5-163">Search for the **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="21ac5-164">Esta preferencia enumera los sitios de confianza de Firefox para la autenticación Kerberos.</span><span class="sxs-lookup"><span data-stu-id="21ac5-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="21ac5-165">Haga clic con el botón derecho y seleccione "Modificar".</span><span class="sxs-lookup"><span data-stu-id="21ac5-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="21ac5-166">Escriba "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" en el campo.</span><span class="sxs-lookup"><span data-stu-id="21ac5-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in the field.</span></span>
5. <span data-ttu-id="21ac5-167">Haga clic en "Aceptar" y vuelva a abrir el explorador.</span><span class="sxs-lookup"><span data-stu-id="21ac5-167">Click "OK" and reopen the browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="21ac5-168">Safari en Mac OS</span><span class="sxs-lookup"><span data-stu-id="21ac5-168">Safari on Mac OS</span></span>

<span data-ttu-id="21ac5-169">Asegúrese de que la máquina que ejecuta Mac OS se ha unido a AD.</span><span class="sxs-lookup"><span data-stu-id="21ac5-169">Ensure that the machine running Mac OS is joined to AD.</span></span> <span data-ttu-id="21ac5-170">Consulte instrucciones sobre cómo hacerlo [aquí](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="21ac5-170">See instructions on how to do that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="21ac5-171">Google Chrome en Mac OS</span><span class="sxs-lookup"><span data-stu-id="21ac5-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="21ac5-172">En el caso de Google Chrome para Mac OS y otras plataformas distintas de Windows, consulte [este artículo](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) para obtener información sobre cómo incluir en la lista blanca las direcciones URL de Azure AD para la autenticación integrada.</span><span class="sxs-lookup"><span data-stu-id="21ac5-172">For Google Chrome on Mac OS and other non-Windows platforms, refer to [this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how to whitelist the Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="21ac5-173">El uso de las extensiones de directiva de grupo de Active Directory de terceros para implementar las direcciones URL de AD Azure de Firefox y Google Chrome para los usuarios de Mac está fuera del ámbito de este artículo.</span><span class="sxs-lookup"><span data-stu-id="21ac5-173">Using third-party Active Directory Group Policy extensions to roll out the Azure AD URLs to Firefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="21ac5-174">Limitaciones conocidas</span><span class="sxs-lookup"><span data-stu-id="21ac5-174">Known limitations</span></span>

<span data-ttu-id="21ac5-175">SSO de conexión directa no funciona en modo de exploración privada en los navegadores Firefox y Edge.</span><span class="sxs-lookup"><span data-stu-id="21ac5-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="21ac5-176">Tampoco funciona en Internet Explorer si el navegador se ejecuta en modo de protección mejorada.</span><span class="sxs-lookup"><span data-stu-id="21ac5-176">It also doesn't work on Internet Explorer if the browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="21ac5-177">Recientemente se ha revertido la compatibilidad para Edge, a fin de investigar los problemas notificados por los clientes.</span><span class="sxs-lookup"><span data-stu-id="21ac5-177">We recently rolled back support for Edge to investigate customer-reported issues.</span></span>

## <a name="step-4-test-the-feature"></a><span data-ttu-id="21ac5-178">Paso 4: Prueba de la característica</span><span class="sxs-lookup"><span data-stu-id="21ac5-178">Step 4: Test the feature</span></span>

<span data-ttu-id="21ac5-179">Para probar la característica con un usuario específico, asegúrese de que se cumplen _todas los_ las condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="21ac5-179">To test the feature for a specific user, ensure that _all_ the following conditions are in place:</span></span>
  - <span data-ttu-id="21ac5-180">El usuario inicia sesión en un escritorio corporativo.</span><span class="sxs-lookup"><span data-stu-id="21ac5-180">The user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="21ac5-181">El dispositivo se ha unido previamente a su dominio de Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="21ac5-181">The device has been previously joined to your Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="21ac5-182">El dispositivo tiene una conexión directa a su controlador de dominio (DC), en la red con cable o inalámbrica de la empresa, o a través de una conexión de acceso remoto, como una conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="21ac5-182">The device has a direct connection to your Domain Controller (DC), either on the corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="21ac5-183">Ha [implantado la característica](##step-3-roll-out-the-feature) para este usuario mediante la directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="21ac5-183">You have [rolled out the feature](##step-3-roll-out-the-feature) to this user using Group Policy.</span></span>

<span data-ttu-id="21ac5-184">Para probar el escenario en el que el usuario escribe solo su nombre de usuario, pero no la contraseña:</span><span class="sxs-lookup"><span data-stu-id="21ac5-184">To test the scenario where the user enters only the username, but not the password:</span></span>
- <span data-ttu-id="21ac5-185">Inicie sesión en *https://myapps.microsoft.com/* en una nueva sesión privada del explorador.</span><span class="sxs-lookup"><span data-stu-id="21ac5-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="21ac5-186">Para probar el escenario en el que el usuario no tiene que escribir ni su nombre de usuario ni su contraseña:</span><span class="sxs-lookup"><span data-stu-id="21ac5-186">To test the scenario where the user doesn't have to enter the username or the password:</span></span> 
- <span data-ttu-id="21ac5-187">Inicie sesión en *https://myapps.microsoft.com/contoso.onmicrosoft.com* en una nueva sesión privada del explorador.</span><span class="sxs-lookup"><span data-stu-id="21ac5-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="21ac5-188">Reemplace "*contoso*" con el nombre de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="21ac5-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="21ac5-189">O bien, inicie sesión en *https://myapps.microsoft.com/contoso.com* en una nueva sesión privada del explorador.</span><span class="sxs-lookup"><span data-stu-id="21ac5-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="21ac5-190">Reemplace "*contoso.com*" con un dominio comprobado (no un dominio federado) en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="21ac5-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="21ac5-191">Paso 5: Sustitución de claves</span><span class="sxs-lookup"><span data-stu-id="21ac5-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="21ac5-192">En el paso 2, Azure AD Connect crea cuentas de equipo (que representan a Azure AD) en todos los bosques de AD en que se ha habilitado SSO de conexión directa.</span><span class="sxs-lookup"><span data-stu-id="21ac5-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all the AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="21ac5-193">Obtenga información más detallada [aquí](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="21ac5-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="21ac5-194">Para mejorar la seguridad, se recomienda sustituir con frecuencia las claves de descifrado de Kerberos de estas cuentas de equipo.</span><span class="sxs-lookup"><span data-stu-id="21ac5-194">For improved security, it is recommended that  you frequently roll over the Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="21ac5-195">No es necesario realizar este paso _inmediatamente_ después de haber habilitado la característica.</span><span class="sxs-lookup"><span data-stu-id="21ac5-195">You don't need to do this step _immediately_ after you have enabled the feature.</span></span> <span data-ttu-id="21ac5-196">Sustituya las claves de descifrado de Kerberos al menos cada 30 días.</span><span class="sxs-lookup"><span data-stu-id="21ac5-196">Roll over the Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21ac5-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="21ac5-197">Next steps</span></span>

- <span data-ttu-id="21ac5-198">[**Profundización técnica** ](active-directory-aadconnect-sso-how-it-works.md): descripción del funcionamiento de esta característica.</span><span class="sxs-lookup"><span data-stu-id="21ac5-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="21ac5-199">[**Preguntas más frecuentes**](active-directory-aadconnect-sso-faq.md): obtenga respuestas a las preguntas más frecuentes.</span><span class="sxs-lookup"><span data-stu-id="21ac5-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="21ac5-200">[**Solución de problemas**](active-directory-aadconnect-troubleshoot-sso.md): aprenda a resolver problemas comunes de esta característica.</span><span class="sxs-lookup"><span data-stu-id="21ac5-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="21ac5-201">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para la tramitación de solicitudes de nuevas características.</span><span class="sxs-lookup"><span data-stu-id="21ac5-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
