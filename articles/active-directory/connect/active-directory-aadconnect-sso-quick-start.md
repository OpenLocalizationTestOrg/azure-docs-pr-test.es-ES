---
title: "Inicio de sesión único de conexión directa de Azure AD Connect: Quía de inicio rápido | Microsoft Docs"
description: "Este artículo describe cómo se inicia tooget con Azure Active Directory sin problemas Single Sign-On."
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
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="d30de-104">Inicio de sesión único de conexión directa de Azure Active Directory: Guía de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="d30de-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-toodeploy-seamless-sso"></a><span data-ttu-id="d30de-105">¿Cómo toodeploy SSO sin problemas</span><span class="sxs-lookup"><span data-stu-id="d30de-105">How toodeploy Seamless SSO</span></span>

<span data-ttu-id="d30de-106">Azure Active Directory sin problemas Single Sign-On (SSO sin problemas de Azure AD), inicia automáticamente los usuarios cuando se encuentran en su red corporativa de los escritorios corporativos tooyour conectado.</span><span class="sxs-lookup"><span data-stu-id="d30de-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected tooyour corporate network.</span></span> <span data-ttu-id="d30de-107">Proporciona a los usuarios un acceso fácil tooyour basada en la nube aplicaciones sin necesidad de todos los componentes locales adicionales.</span><span class="sxs-lookup"><span data-stu-id="d30de-107">It provides your users easy access tooyour cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d30de-108">característica de SSO sin problemas de Hello está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="d30de-108">hello Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="d30de-109">toodeploy SSO sin problemas, necesita toofollow estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d30de-109">toodeploy Seamless SSO, you need toofollow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="d30de-110">Paso 1: Comprobación de los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d30de-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="d30de-111">Asegúrese de que Hola siguiendo los requisitos previos están en su lugar:</span><span class="sxs-lookup"><span data-stu-id="d30de-111">Ensure that hello following prerequisites are in place:</span></span>

1. <span data-ttu-id="d30de-112">El servidor de Azure AD Connect está configurado: si usa la [autenticación de paso a través](active-directory-aadconnect-pass-through-authentication.md) como método de inicio de sesión, no es necesaria realizar ninguna otra acción.</span><span class="sxs-lookup"><span data-stu-id="d30de-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="d30de-113">Si va a usar la [sincronización de hash de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) como método de inicio de sesión y hay un firewall entre Azure AD Connect y Azure AD, asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="d30de-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="d30de-114">Está usando la versión 1.1.484.0 de Azure AD Connect o una posterior.</span><span class="sxs-lookup"><span data-stu-id="d30de-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="d30de-115">Azure AD Connect puede comunicarse con las direcciones URL de `*.msappproxy.net` y a través del puerto 443.</span><span class="sxs-lookup"><span data-stu-id="d30de-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="d30de-116">Este requisito previo solo es aplicable cuando se habilita la característica de hello, no para los inicios de sesión de usuario real.</span><span class="sxs-lookup"><span data-stu-id="d30de-116">This prerequisite is applicable only when you enable hello feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="d30de-117">Azure AD Connect hacer direct IP conexiones toohello [intervalos IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="d30de-117">Azure AD Connect can make direct IP connections toohello [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="d30de-118">Una vez más, este requisito previo solo es aplicable cuando se habilita la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-118">Again, this prerequisite is applicable only when you enable hello feature.</span></span>
2. <span data-ttu-id="d30de-119">Necesita credenciales de administrador de dominio para cada bosque de AD que sincronizar tooAzure AD (mediante Azure AD Connect) y para cuyos usuarios desea tooenable SSO sin problemas.</span><span class="sxs-lookup"><span data-stu-id="d30de-119">You need Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span>

## <a name="step-2-enable-hello-feature"></a><span data-ttu-id="d30de-120">Paso 2: Habilitar la característica de Hola</span><span class="sxs-lookup"><span data-stu-id="d30de-120">Step 2: Enable hello feature</span></span>

<span data-ttu-id="d30de-121">SSO de conexión directa se puede habilitar a través de [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d30de-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="d30de-122">Si está realizando una instalación nueva de Azure AD Connect, elija hello [ruta de acceso de instalación personalizada](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d30de-122">If you are doing a fresh installation of Azure AD Connect, choose hello [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="d30de-123">En la página de Hola "Inicio de sesión de usuario", active la opción de "Habilitar inicio de sesión único" de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-123">At hello "User sign-in" page, check hello "Enable single sign on" option.</span></span>

![Azure AD Connect: Inicio de sesión de usuario](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="d30de-125">Si ya tiene una instalación de Azure AD Connect, elija "Change user sign-in page" (Cambiar página de inicio de sesión del usuario) en Azure AD Connect y haga clic en "Siguiente".</span><span class="sxs-lookup"><span data-stu-id="d30de-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="d30de-126">A continuación, compruebe la opción "Habilitar inicio de sesión único" de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-126">Then check hello "Enable single sign on" option.</span></span>

![Azure AD Connect: Change user sign-in page (Cambiar página de inicio de sesión del usuario)](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="d30de-128">Continúe con el Asistente de hello hasta obtener la página de "Habilitar inicio de sesión único" de toohello.</span><span class="sxs-lookup"><span data-stu-id="d30de-128">Continue through hello wizard until you get toohello "Enable single sign on" page.</span></span> <span data-ttu-id="d30de-129">Proporcione las credenciales de administrador de dominio para cada bosque de AD que sincronizar tooAzure AD (mediante Azure AD Connect) y para cuyos usuarios desea tooenable SSO sin problemas.</span><span class="sxs-lookup"><span data-stu-id="d30de-129">Provide Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span> 

<span data-ttu-id="d30de-130">Tras la finalización del Asistente para hello, SSO sin problemas está habilitado en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="d30de-130">After completion of hello wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="d30de-131">las credenciales de administrador de dominio de Hello no se almacenan en Azure AD Connect o en Azure AD, pero son solo la característica de hello tooenable usado.</span><span class="sxs-lookup"><span data-stu-id="d30de-131">hello Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used tooenable hello feature.</span></span>

<span data-ttu-id="d30de-132">Siga estos tooverify de instrucciones que se ha habilitado correctamente SSO sin problemas:</span><span class="sxs-lookup"><span data-stu-id="d30de-132">Follow these instructions tooverify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="d30de-133">Inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con credenciales de administrador Global de hello para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="d30de-133">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with hello Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="d30de-134">Seleccione **Azure Active Directory** en el panel de navegación izquierdo Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-134">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="d30de-135">Seleccione **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="d30de-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="d30de-136">Compruebe que hello **perfecta Single Sign-On** característica se muestra como **habilitado**.</span><span class="sxs-lookup"><span data-stu-id="d30de-136">Verify that hello **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Azure Portal: hoja Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a><span data-ttu-id="d30de-138">Paso 3: Implementar características de Hola</span><span class="sxs-lookup"><span data-stu-id="d30de-138">Step 3: Roll out hello feature</span></span>

<span data-ttu-id="d30de-139">tooroll los usuarios de hello característica tooyour, necesita configuración de zona de Intranet de toousers del Azure direcciones URL de AD (https://autologon.microsoftazuread-sso.com y https://aadg.windows.net.nsatc.net) de dos tooadd a través de la directiva de grupo en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d30de-139">tooroll out hello feature tooyour users, you need tooadd two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) toousers' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="d30de-140">Hola siguiendo las instrucciones sólo funcionan para Internet Explorer y Google Chrome en Windows (si el conjunto de direcciones URL de sitios de confianza comparte con Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="d30de-140">hello following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="d30de-141">Lea las secciones siguiente Hola para instrucciones tooset Mozilla Firefox y Google Chrome en Mac.</span><span class="sxs-lookup"><span data-stu-id="d30de-141">Read hello next section for instructions tooset up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a><span data-ttu-id="d30de-142">¿Por qué necesita la configuración de zona de Intranet de los usuarios de toomodify?</span><span class="sxs-lookup"><span data-stu-id="d30de-142">Why do you need toomodify users' Intranet zone settings?</span></span>

<span data-ttu-id="d30de-143">De forma predeterminada, el Explorador de hello calcula automáticamente zona derecha de hello (Internet o Intranet) desde una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="d30de-143">By default, hello browser automatically calculates hello right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="d30de-144">Por ejemplo, http://contoso/ es toohello asignada la zona de Intranet, mientras que http://intranet.contoso.com/ es zona de Internet asignada toohello (porque la dirección URL de hello contiene un punto).</span><span class="sxs-lookup"><span data-stu-id="d30de-144">For example, http://contoso/ is mapped toohello Intranet zone, whereas http://intranet.contoso.com/ is mapped toohello Internet zone (because hello URL contains a period).</span></span> <span data-ttu-id="d30de-145">Exploradores no envían el extremo de nube de tooa de vales de Kerberos - como Hola dos Azure AD direcciones URL - a menos que su dirección URL se agrega explícitamente a la zona de Intranet del explorador de toohello.</span><span class="sxs-lookup"><span data-stu-id="d30de-145">Browsers don't send Kerberos tickets tooa cloud endpoint - like hello two Azure AD URLs - unless its URL is explicitly added toohello browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="d30de-146">Pasos detallados</span><span class="sxs-lookup"><span data-stu-id="d30de-146">Detailed steps</span></span>

1. <span data-ttu-id="d30de-147">Abra la herramienta de administración de directivas de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-147">Open hello Group Policy Management tool.</span></span>
2. <span data-ttu-id="d30de-148">Editar directiva de grupo aplicado toosome o todos los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-148">Edit hello Group Policy that is applied toosome or all your users.</span></span> <span data-ttu-id="d30de-149">En este ejemplo, utilizamos hello **Default Domain Policy**.</span><span class="sxs-lookup"><span data-stu-id="d30de-149">In this example, we use hello **Default Domain Policy**.</span></span>
3. <span data-ttu-id="d30de-150">Navegue demasiado**usuario Configuración del equipo\Plantillas administrativas\Componentes de Windows\Internet Internet Control Internet\página** y seleccione **tooZone lista de asignación de sitio**.</span><span class="sxs-lookup"><span data-stu-id="d30de-150">Navigate too**User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site tooZone Assignment List**.</span></span>
<span data-ttu-id="d30de-151">![Inicio de sesión único](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="d30de-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="d30de-152">Habilitar directiva de Hola y escriba Hola después de valores (Azure AD direcciones URL donde se reenvían los vales de Kerberos) y los datos (*1* indica la zona de Intranet) en el cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-152">Enable hello policy, and enter hello following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in hello dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="d30de-153">Si desea toodisallow algunos usuarios utilizasen SSO sin problemas: por ejemplo, si estos usuarios inician sesión en quioscos compartidos - establezca Hola valores iniciales demasiado*4*.</span><span class="sxs-lookup"><span data-stu-id="d30de-153">If you want toodisallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set hello preceding values too*4*.</span></span> <span data-ttu-id="d30de-154">Esta acción agrega hello las direcciones URL de Azure AD toohello zona Sitios restringidos y se produce un error SSO sin problemas todo el tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-154">This action adds hello Azure AD URLs toohello Restricted Zone, and fails Seamless SSO all hello time.</span></span>

5. <span data-ttu-id="d30de-155">Haga clic en **Aceptar** y en **Aceptar** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="d30de-155">Click **OK** and **OK** again.</span></span>

![Inicio de sesión único](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="d30de-157">Consideraciones sobre el explorador</span><span class="sxs-lookup"><span data-stu-id="d30de-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="d30de-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="d30de-158">Mozilla Firefox</span></span>

<span data-ttu-id="d30de-159">Mozilla Firefox no realiza automáticamente la autenticación Kerberos.</span><span class="sxs-lookup"><span data-stu-id="d30de-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="d30de-160">Cada usuario tiene toomanually agregar configuraciones de Firefox hello Azure AD direcciones URL tootheir con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="d30de-160">Each user has toomanually add hello Azure AD URLs tootheir Firefox settings using hello following steps:</span></span>
1. <span data-ttu-id="d30de-161">Ejecute Firefox y escriba `about:config` en la barra de direcciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-161">Run Firefox and enter `about:config` in hello address bar.</span></span> <span data-ttu-id="d30de-162">Descarte las notificaciones que vea.</span><span class="sxs-lookup"><span data-stu-id="d30de-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="d30de-163">Busque hello **network.negotiate-auth.trusted-URI** preferencias.</span><span class="sxs-lookup"><span data-stu-id="d30de-163">Search for hello **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="d30de-164">Esta preferencia enumera los sitios de confianza de Firefox para la autenticación Kerberos.</span><span class="sxs-lookup"><span data-stu-id="d30de-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="d30de-165">Haga clic con el botón derecho y seleccione "Modificar".</span><span class="sxs-lookup"><span data-stu-id="d30de-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="d30de-166">Escriba "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" en el campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in hello field.</span></span>
5. <span data-ttu-id="d30de-167">Haga clic en "Aceptar" y vuelva a abrir el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-167">Click "OK" and reopen hello browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="d30de-168">Safari en Mac OS</span><span class="sxs-lookup"><span data-stu-id="d30de-168">Safari on Mac OS</span></span>

<span data-ttu-id="d30de-169">Asegúrese de que Hola equipo ejecuta Mac OS tooAD combinada.</span><span class="sxs-lookup"><span data-stu-id="d30de-169">Ensure that hello machine running Mac OS is joined tooAD.</span></span> <span data-ttu-id="d30de-170">Consulte las instrucciones sobre cómo toodo que [aquí](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="d30de-170">See instructions on how toodo that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="d30de-171">Google Chrome en Mac OS</span><span class="sxs-lookup"><span data-stu-id="d30de-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="d30de-172">Para Google Chrome en Mac OS y otras plataformas distintas de Windows, consulte demasiado[este artículo](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) para obtener información sobre cómo toowhitelist Hola direcciones URL de Azure AD para la autenticación integrada.</span><span class="sxs-lookup"><span data-stu-id="d30de-172">For Google Chrome on Mac OS and other non-Windows platforms, refer too[this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how toowhitelist hello Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="d30de-173">Mediante la directiva de grupo de aplicaciones de terceros Active Directory extensiones tooroll tooFirefox de hello las direcciones URL de Azure AD y Google Chrome en los usuarios de Mac está fuera del ámbito de este artículo.</span><span class="sxs-lookup"><span data-stu-id="d30de-173">Using third-party Active Directory Group Policy extensions tooroll out hello Azure AD URLs tooFirefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="d30de-174">Limitaciones conocidas</span><span class="sxs-lookup"><span data-stu-id="d30de-174">Known limitations</span></span>

<span data-ttu-id="d30de-175">SSO de conexión directa no funciona en modo de exploración privada en los navegadores Firefox y Edge.</span><span class="sxs-lookup"><span data-stu-id="d30de-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="d30de-176">También no funciona en Internet Explorer si Hola explorador se ejecuta en modo de protección mejorado.</span><span class="sxs-lookup"><span data-stu-id="d30de-176">It also doesn't work on Internet Explorer if hello browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d30de-177">Se recientemente revierten compatibilidad con borde tooinvestigate problemas detectados por el cliente.</span><span class="sxs-lookup"><span data-stu-id="d30de-177">We recently rolled back support for Edge tooinvestigate customer-reported issues.</span></span>

## <a name="step-4-test-hello-feature"></a><span data-ttu-id="d30de-178">Paso 4: Probar la característica de Hola</span><span class="sxs-lookup"><span data-stu-id="d30de-178">Step 4: Test hello feature</span></span>

<span data-ttu-id="d30de-179">característica de hello tootest para un usuario específico, asegúrese de que _todos los_ Hola condiciones siguientes está en su lugar:</span><span class="sxs-lookup"><span data-stu-id="d30de-179">tootest hello feature for a specific user, ensure that _all_ hello following conditions are in place:</span></span>
  - <span data-ttu-id="d30de-180">usuario de Hello es iniciar sesión en un dispositivo de la empresa.</span><span class="sxs-lookup"><span data-stu-id="d30de-180">hello user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="d30de-181">dispositivo de Hello ha sido tooyour previamente Unidos a un dominio de Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="d30de-181">hello device has been previously joined tooyour Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="d30de-182">dispositivo de Hello tiene un controlador de dominio (DC), ya sea en la red corporativa con cable o inalámbrica de Hola o mediante una conexión de acceso remoto, como una conexión VPN tooyour de conexión directa.</span><span class="sxs-lookup"><span data-stu-id="d30de-182">hello device has a direct connection tooyour Domain Controller (DC), either on hello corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="d30de-183">Tiene [implantado característica hello](##step-3-roll-out-the-feature) usuario toothis mediante Directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="d30de-183">You have [rolled out hello feature](##step-3-roll-out-the-feature) toothis user using Group Policy.</span></span>

<span data-ttu-id="d30de-184">escenario de hello tootest donde entra en usuario Hola solo nombre de usuario de hello, pero una contraseña no sea hello:</span><span class="sxs-lookup"><span data-stu-id="d30de-184">tootest hello scenario where hello user enters only hello username, but not hello password:</span></span>
- <span data-ttu-id="d30de-185">Inicie sesión en *https://myapps.microsoft.com/* en una nueva sesión privada del explorador.</span><span class="sxs-lookup"><span data-stu-id="d30de-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="d30de-186">escenario de hello tootest donde el usuario de hello no tiene la contraseña de nombre de usuario u Hola Hola tooenter:</span><span class="sxs-lookup"><span data-stu-id="d30de-186">tootest hello scenario where hello user doesn't have tooenter hello username or hello password:</span></span> 
- <span data-ttu-id="d30de-187">Inicie sesión en *https://myapps.microsoft.com/contoso.onmicrosoft.com* en una nueva sesión privada del explorador.</span><span class="sxs-lookup"><span data-stu-id="d30de-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="d30de-188">Reemplace "*contoso*" con el nombre de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="d30de-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="d30de-189">O bien, inicie sesión en *https://myapps.microsoft.com/contoso.com* en una nueva sesión privada del explorador.</span><span class="sxs-lookup"><span data-stu-id="d30de-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="d30de-190">Reemplace "*contoso.com*" con un dominio comprobado (no un dominio federado) en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="d30de-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="d30de-191">Paso 5: Sustitución de claves</span><span class="sxs-lookup"><span data-stu-id="d30de-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="d30de-192">En el paso 2, Azure AD Connect crea cuentas de equipo (que representa a Azure AD) en todos los bosques de AD de hello en el que ha habilitado SSO sin problemas.</span><span class="sxs-lookup"><span data-stu-id="d30de-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all hello AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="d30de-193">Obtenga información más detallada [aquí](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="d30de-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="d30de-194">Para mejorar la seguridad, se recomienda que con frecuencia se sustituyen las claves de descifrado de hello Kerberos de estas cuentas de equipo.</span><span class="sxs-lookup"><span data-stu-id="d30de-194">For improved security, it is recommended that  you frequently roll over hello Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d30de-195">No es necesario toodo este paso _inmediatamente_ después de haber habilitado la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-195">You don't need toodo this step _immediately_ after you have enabled hello feature.</span></span> <span data-ttu-id="d30de-196">Se sustituyen las claves de descifrado de Kerberos de hello al menos cada 30 días.</span><span class="sxs-lookup"><span data-stu-id="d30de-196">Roll over hello Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d30de-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d30de-197">Next steps</span></span>

- <span data-ttu-id="d30de-198">[**Profundización técnica**](active-directory-aadconnect-sso-how-it-works.md): descripción del funcionamiento de esta característica.</span><span class="sxs-lookup"><span data-stu-id="d30de-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="d30de-199">[**Preguntas más frecuentes** ](active-directory-aadconnect-sso-faq.md) -responde toofrequently preguntas más frecuentes.</span><span class="sxs-lookup"><span data-stu-id="d30de-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="d30de-200">[**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="d30de-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="d30de-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para la tramitación de solicitudes de nuevas características.</span><span class="sxs-lookup"><span data-stu-id="d30de-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
