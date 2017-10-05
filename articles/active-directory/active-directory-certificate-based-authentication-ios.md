---
title: "Autenticación basada en certificados de Azure Active Directory en iOS | Microsoft Docs"
description: "Obtenga información acerca de los escenarios admitidos y los requisitos para configurar la autenticación basada en certificados en las soluciones con dispositivos iOS"
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
ms.openlocfilehash: c781f3f054fad5c5092fed5058c932fd4e97cf35
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="4d0e1-103">Autenticación basada en certificados de Azure Active Directory en iOS</span><span class="sxs-lookup"><span data-stu-id="4d0e1-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="4d0e1-104">La autenticación basada en certificados (CBA) le permite autenticarse mediante Azure Active Directory con un certificado de cliente en un dispositivo Windows, Android o iOS al conectar su cuenta de Exchange Online a:</span><span class="sxs-lookup"><span data-stu-id="4d0e1-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="4d0e1-105">aplicaciones móviles de Office como Microsoft Outlook y Microsoft Word,</span><span class="sxs-lookup"><span data-stu-id="4d0e1-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="4d0e1-106">clientes de Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="4d0e1-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="4d0e1-107">Al configurar esta función, no tendrá que escribir una combinación de nombre de usuario y contraseña en determinadas aplicaciones de correo electrónico y Microsoft Office de su dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="4d0e1-108">En este tema se proporcionan los requisitos y los escenarios admitidos para configurar CBA en un dispositivo iOS (Android) para usuarios de inquilinos de planes de Office 365 Enterprise, Empresa, Educación, US Government, China y Alemania.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="4d0e1-109">Esta característica se encuentra disponible como versión preliminar en los planes Office 365 US Government Defense y US Government Federal.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="4d0e1-110">Compatibilidad con aplicaciones móviles de Office</span><span class="sxs-lookup"><span data-stu-id="4d0e1-110">Office mobile applications support</span></span>

| <span data-ttu-id="4d0e1-111">Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4d0e1-111">Apps</span></span> | <span data-ttu-id="4d0e1-112">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="4d0e1-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="4d0e1-113">Aplicación Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="4d0e1-113">Azure Information Protection app</span></span> |![Comprobar][1] |
| <span data-ttu-id="4d0e1-115">Equipos de Microsoft</span><span class="sxs-lookup"><span data-stu-id="4d0e1-115">Microsoft Teams</span></span> |![Comprobar][1] |
| <span data-ttu-id="4d0e1-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="4d0e1-117">OneNote</span></span> |![Comprobar][1] |
| <span data-ttu-id="4d0e1-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="4d0e1-119">OneDrive</span></span> |![Comprobar][1] |
| <span data-ttu-id="4d0e1-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="4d0e1-121">Outlook</span></span> |![Comprobar][1] |
| <span data-ttu-id="4d0e1-123">Aplicaciones móviles de Power BI</span><span class="sxs-lookup"><span data-stu-id="4d0e1-123">Power BI mobile apps</span></span> |![Comprobar][1] |
| <span data-ttu-id="4d0e1-125">Skype Empresarial</span><span class="sxs-lookup"><span data-stu-id="4d0e1-125">Skype for Business</span></span> |![Comprobar][1] |
| <span data-ttu-id="4d0e1-127">Word, Excel y PowerPoint</span><span class="sxs-lookup"><span data-stu-id="4d0e1-127">Word / Excel / PowerPoint</span></span> |![Comprobar][1] |
| <span data-ttu-id="4d0e1-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="4d0e1-129">Yammer</span></span> |![Comprobar][1] |


## <a name="requirements"></a><span data-ttu-id="4d0e1-131">Requisitos</span><span class="sxs-lookup"><span data-stu-id="4d0e1-131">Requirements</span></span> 

<span data-ttu-id="4d0e1-132">La versión del sistema operativo del dispositivo debe ser iOS 9 y posterior.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-132">The device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="4d0e1-133">Se debe configurar un servidor de federación.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-133">A federation server must be configured.</span></span>  

<span data-ttu-id="4d0e1-134">Se requiere Microsoft Authenticator para las aplicaciones de Office en iOS.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="4d0e1-135">Para que Azure Active Directory revoque un certificado de cliente, el token de ADFS debe tener las siguientes notificaciones:</span><span class="sxs-lookup"><span data-stu-id="4d0e1-135">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="4d0e1-136">(el número de serie del certificado de cliente)</span><span class="sxs-lookup"><span data-stu-id="4d0e1-136">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="4d0e1-137">(la cadena del emisor del certificado de cliente)</span><span class="sxs-lookup"><span data-stu-id="4d0e1-137">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="4d0e1-138">Azure Active Directory agrega estas notificaciones para el token de actualización, en caso de que estén disponibles en el token de ADFS (o en cualquier otro token SAML).</span><span class="sxs-lookup"><span data-stu-id="4d0e1-138">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="4d0e1-139">Cuando hay que validar el token de actualización, esta información se utiliza para comprobar la revocación.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-139">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="4d0e1-140">Se recomienda actualizar las páginas de error de ADFS con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4d0e1-140">As a best practice, you should update the ADFS error pages with the following:</span></span>

* <span data-ttu-id="4d0e1-141">El requisito de instalar Microsoft Authenticator en iOS</span><span class="sxs-lookup"><span data-stu-id="4d0e1-141">The requirement for installing the Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="4d0e1-142">Instrucciones sobre cómo obtener un certificado de usuario</span><span class="sxs-lookup"><span data-stu-id="4d0e1-142">Instructions on how to get a user certificate.</span></span> 

<span data-ttu-id="4d0e1-143">Para más información, consulte [Personalizar las páginas de inicio de sesión de AD FS](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d0e1-143">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="4d0e1-144">Algunas aplicaciones de Office (con la autenticación moderna habilitada) envían ‘*prompt=login*’ a Azure AD en su solicitud.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="4d0e1-145">De manera predeterminada, Azure AD lo traduce en la solicitud para ADFS a '*wauth = usernamepassworduri*' (pide a ADFS que realice la autenticación de U y P) y '*wfresh = 0*' (pide a ADFS que ignore el estado de SSO y realice una autenticación nueva).</span><span class="sxs-lookup"><span data-stu-id="4d0e1-145">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="4d0e1-146">Si desea habilitar la autenticación basada en certificados para estas aplicaciones, es preciso que modifique el comportamiento predeterminado de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-146">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="4d0e1-147">Basta con establecer '*PromptLoginBehavior*' en la configuración del dominio federado como '*Disabled*'.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-147">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="4d0e1-148">Para realizar esta tarea, puede usar el cmdlet [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0):</span><span class="sxs-lookup"><span data-stu-id="4d0e1-148">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="4d0e1-149">Compatibilidad con clientes de Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="4d0e1-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="4d0e1-150">En iOS 9 o posterior, se admite el cliente de correo de iOS nativo.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-150">On iOS 9 or later, the native iOS mail client is supported.</span></span> <span data-ttu-id="4d0e1-151">Para todas las demás aplicaciones de Exchange ActiveSync, para determinar si se admite esta característica, póngase en contacto con el desarrollador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d0e1-151">For all other Exchange ActiveSync applications, to determine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="4d0e1-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4d0e1-152">Next steps</span></span>

<span data-ttu-id="4d0e1-153">Si quiere configurar la autenticación basada en certificados en su entorno, consulte las instrucciones de [Introducción a la autenticación basada en certificados en Android](active-directory-certificate-based-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4d0e1-153">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
