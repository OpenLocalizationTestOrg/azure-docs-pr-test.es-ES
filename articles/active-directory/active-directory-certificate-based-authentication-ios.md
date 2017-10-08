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
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a>Autenticación basada en certificados de Azure Active Directory en iOS

Autenticación basada en certificados (CBA) le permite toobe autenticado por Azure Active Directory con un certificado de cliente en un dispositivo de Windows, Android o iOS cuando se conecte a su cuenta de Exchange online para: 

* aplicaciones móviles de Office como Microsoft Outlook y Microsoft Word,   
* clientes de Exchange ActiveSync (EAS). 

La configuración de esta característica elimina Hola necesidad tooenter un nombre de usuario y la combinación de contraseña en determinados correo electrónico y aplicaciones de Microsoft Office en su dispositivo móvil. 

En este tema se proporciona con los requisitos de Hola y escenarios de hello admitida para configurar CBA en un dispositivo iOS(Android) para los usuarios de inquilinos de Office 365 Enterprise, Business, educación, gobierno de Estados Unidos, China y planes de Alemania.

Esta característica se encuentra disponible como versión preliminar en los planes Office 365 US Government Defense y US Government Federal.




## <a name="office-mobile-applications-support"></a>Compatibilidad con aplicaciones móviles de Office

| Aplicaciones | Soporte técnico |
| --- | --- |
| Aplicación Azure Information Protection |![Comprobar][1] |
| Equipos de Microsoft |![Comprobar][1] |
| OneNote |![Comprobar][1] |
| OneDrive |![Comprobar][1] |
| Outlook |![Comprobar][1] |
| Aplicaciones móviles de Power BI |![Comprobar][1] |
| Skype Empresarial |![Comprobar][1] |
| Word, Excel y PowerPoint |![Comprobar][1] |
| Yammer |![Comprobar][1] |


## <a name="requirements"></a>Requisitos 

Hello versión de sistema operativo del dispositivo debe ser iOS 9 y versiones posteriores 

Se debe configurar un servidor de federación.  

Se requiere Microsoft Authenticator para las aplicaciones de Office en iOS.  

Para toorevoke un certificado de cliente de Azure Active Directory, token ADFS Hola debe tener Hola siguientes notificaciones:  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  (número de serie de Hola Hola del certificado de cliente) 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  (cadena de Hola de emisor de Hola Hola del certificado de cliente) 

Azure Active Directory agrega estos token de actualización de toohello notificaciones si están disponibles en el símbolo (token) de AD FS de hello (o cualquier otro token SAML). Cuando el token de actualización de hello necesita toobe validado, esta información es toocheck usado Hola revocación. 

Como práctica recomendada, debe actualizar las páginas de error de hello ADFS con siguiente hello:

* requisito de Hello para la instalación de Microsoft Authenticator hello en iOS
* Instrucciones sobre cómo tooget un certificado de usuario. 

Para obtener más información, consulte [Customizing Hola AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).

Algunas aplicaciones de Office (con la autenticación moderna habilitada) enviar '*= inicio de sesión de símbolo del sistema*' tooAzure AD en su solicitud. De forma predeterminada, Azure AD la traduce en hello solicitud tooADFS demasiado '*wauth = usernamepassworduri*' (solicita la autenticación ADFS toodo U/P) y '*wfresh = 0*' (solicita el estado SSO de tooignore ADFS y realice una nueva autenticación) . Si desea que la autenticación basada en certificados tooenable para estas aplicaciones, que necesite un comportamiento de Azure AD de toomodify Hola de forma predeterminada. Solo un conjunto hello '*PromptLoginBehavior*' en la configuración del dominio federado demasiado '*deshabilitado*'. Puede usar hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform cmdlet esta tarea:

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a>Compatibilidad con clientes de Exchange ActiveSync
En iOS 9 o posterior, se admite el cliente de correo electrónico de iOS nativo Hola. Para todas las demás aplicaciones de Exchange ActiveSync, toodetermine si se admite esta característica, póngase en contacto con el desarrollador de aplicaciones.  


## <a name="next-steps"></a>Pasos siguientes

Si desea que la autenticación basada en certificados tooconfigure en su entorno, consulte [empezar a trabajar con autenticación basada en certificados en Android](active-directory-certificate-based-authentication-get-started.md) para obtener instrucciones.


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
