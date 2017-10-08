---
title: "autenticación basada en certificados en Active Directory aaaAzure en iOS | Documentos de Microsoft"
description: "Obtenga información acerca de los escenarios de hello admitido y los requisitos de Hola para configurar la autenticación basada en certificados en soluciones con dispositivos iOS"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="f9b0f-103">Autenticación basada en certificados de Azure Active Directory en iOS</span><span class="sxs-lookup"><span data-stu-id="f9b0f-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="f9b0f-104">Autenticación basada en certificados (CBA) le permite toobe autenticado por Azure Active Directory con un certificado de cliente en un dispositivo de Windows, Android o iOS cuando se conecte a su cuenta de Exchange online para:</span><span class="sxs-lookup"><span data-stu-id="f9b0f-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="f9b0f-105">aplicaciones móviles de Office como Microsoft Outlook y Microsoft Word,</span><span class="sxs-lookup"><span data-stu-id="f9b0f-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="f9b0f-106">clientes de Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="f9b0f-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="f9b0f-107">La configuración de esta característica elimina Hola necesidad tooenter un nombre de usuario y la combinación de contraseña en determinados correo electrónico y aplicaciones de Microsoft Office en su dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="f9b0f-108">En este tema se proporciona con los requisitos de Hola y escenarios de hello admitida para configurar CBA en un dispositivo iOS(Android) para los usuarios de inquilinos de Office 365 Enterprise, Business, educación, gobierno de Estados Unidos, China y planes de Alemania.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="f9b0f-109">Esta característica se encuentra disponible como versión preliminar en los planes Office 365 US Government Defense y US Government Federal.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="f9b0f-110">Compatibilidad con aplicaciones móviles de Office</span><span class="sxs-lookup"><span data-stu-id="f9b0f-110">Office mobile applications support</span></span>

| <span data-ttu-id="f9b0f-111">Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f9b0f-111">Apps</span></span> | <span data-ttu-id="f9b0f-112">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="f9b0f-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="f9b0f-113">Aplicación Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="f9b0f-113">Azure Information Protection app</span></span> |![Comprobar][1] |
| <span data-ttu-id="f9b0f-115">Equipos de Microsoft</span><span class="sxs-lookup"><span data-stu-id="f9b0f-115">Microsoft Teams</span></span> |![Comprobar][1] |
| <span data-ttu-id="f9b0f-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="f9b0f-117">OneNote</span></span> |![Comprobar][1] |
| <span data-ttu-id="f9b0f-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="f9b0f-119">OneDrive</span></span> |![Comprobar][1] |
| <span data-ttu-id="f9b0f-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="f9b0f-121">Outlook</span></span> |![Comprobar][1] |
| <span data-ttu-id="f9b0f-123">Aplicaciones móviles de Power BI</span><span class="sxs-lookup"><span data-stu-id="f9b0f-123">Power BI mobile apps</span></span> |![Comprobar][1] |
| <span data-ttu-id="f9b0f-125">Skype Empresarial</span><span class="sxs-lookup"><span data-stu-id="f9b0f-125">Skype for Business</span></span> |![Comprobar][1] |
| <span data-ttu-id="f9b0f-127">Word, Excel y PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f9b0f-127">Word / Excel / PowerPoint</span></span> |![Comprobar][1] |
| <span data-ttu-id="f9b0f-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="f9b0f-129">Yammer</span></span> |![Comprobar][1] |


## <a name="requirements"></a><span data-ttu-id="f9b0f-131">Requisitos</span><span class="sxs-lookup"><span data-stu-id="f9b0f-131">Requirements</span></span> 

<span data-ttu-id="f9b0f-132">Hello versión de sistema operativo del dispositivo debe ser iOS 9 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="f9b0f-132">hello device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="f9b0f-133">Se debe configurar un servidor de federación.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-133">A federation server must be configured.</span></span>  

<span data-ttu-id="f9b0f-134">Se requiere Microsoft Authenticator para las aplicaciones de Office en iOS.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="f9b0f-135">Para toorevoke un certificado de cliente de Azure Active Directory, token ADFS Hola debe tener Hola siguientes notificaciones:</span><span class="sxs-lookup"><span data-stu-id="f9b0f-135">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="f9b0f-136">(número de serie de Hola Hola del certificado de cliente)</span><span class="sxs-lookup"><span data-stu-id="f9b0f-136">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="f9b0f-137">(cadena de Hola de emisor de Hola Hola del certificado de cliente)</span><span class="sxs-lookup"><span data-stu-id="f9b0f-137">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="f9b0f-138">Azure Active Directory agrega estos token de actualización de toohello notificaciones si están disponibles en el símbolo (token) de AD FS de hello (o cualquier otro token SAML).</span><span class="sxs-lookup"><span data-stu-id="f9b0f-138">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="f9b0f-139">Cuando el token de actualización de hello necesita toobe validado, esta información es toocheck usado Hola revocación.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-139">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="f9b0f-140">Como práctica recomendada, debe actualizar las páginas de error de hello ADFS con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="f9b0f-140">As a best practice, you should update hello ADFS error pages with hello following:</span></span>

* <span data-ttu-id="f9b0f-141">requisito de Hello para la instalación de Microsoft Authenticator hello en iOS</span><span class="sxs-lookup"><span data-stu-id="f9b0f-141">hello requirement for installing hello Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="f9b0f-142">Instrucciones sobre cómo tooget un certificado de usuario.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-142">Instructions on how tooget a user certificate.</span></span> 

<span data-ttu-id="f9b0f-143">Para obtener más información, consulte [Customizing Hola AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9b0f-143">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="f9b0f-144">Algunas aplicaciones de Office (con la autenticación moderna habilitada) enviar '*= inicio de sesión de símbolo del sistema*' tooAzure AD en su solicitud.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="f9b0f-145">De forma predeterminada, Azure AD la traduce en hello solicitud tooADFS demasiado '*wauth = usernamepassworduri*' (solicita la autenticación ADFS toodo U/P) y '*wfresh = 0*' (solicita el estado SSO de tooignore ADFS y realice una nueva autenticación) .</span><span class="sxs-lookup"><span data-stu-id="f9b0f-145">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="f9b0f-146">Si desea que la autenticación basada en certificados tooenable para estas aplicaciones, que necesite un comportamiento de Azure AD de toomodify Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-146">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="f9b0f-147">Solo un conjunto hello '*PromptLoginBehavior*' en la configuración del dominio federado demasiado '*deshabilitado*'.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-147">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="f9b0f-148">Puede usar hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform cmdlet esta tarea:</span><span class="sxs-lookup"><span data-stu-id="f9b0f-148">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="f9b0f-149">Compatibilidad con clientes de Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="f9b0f-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="f9b0f-150">En iOS 9 o posterior, se admite el cliente de correo electrónico de iOS nativo Hola.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-150">On iOS 9 or later, hello native iOS mail client is supported.</span></span> <span data-ttu-id="f9b0f-151">Para todas las demás aplicaciones de Exchange ActiveSync, toodetermine si se admite esta característica, póngase en contacto con el desarrollador de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-151">For all other Exchange ActiveSync applications, toodetermine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="f9b0f-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9b0f-152">Next steps</span></span>

<span data-ttu-id="f9b0f-153">Si desea que la autenticación basada en certificados tooconfigure en su entorno, consulte [empezar a trabajar con autenticación basada en certificados en Android](active-directory-certificate-based-authentication-get-started.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="f9b0f-153">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
