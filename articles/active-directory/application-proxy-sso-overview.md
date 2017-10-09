---
title: "aaaManage SSO para el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Obtenga información acerca de conceptos básicos de Hola de inicio de sesión único con el Proxy de aplicación"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a>¿Cómo permite el proxy de aplicación de Azure AD el inicio de sesión único?

El inicio de sesión único es un elemento clave del proxy de aplicación de Azure AD.  Proporciona mejor experiencia de usuario Hola ya que los usuarios sólo tienen toosign en Active Directory en la nube de hello tooAzure. Una vez que se autentican tooAzure Active Directory, el conector del Proxy de aplicación de hello controla Hola autenticación toohello local de aplicación. aplicación de back-end de Hello no puede indicar la diferencia de hello entre un usuario remoto iniciar sesión a través de Proxy de aplicación y un uso normal en un dispositivo unido al dominio. 

toouse Azure Active Directory para las aplicaciones de tooyour de inicio de sesión único, deberá tooselect **Azure Active Directory** como método de autenticación previa de Hola. Si selecciona **Passthrough** , a continuación, los usuarios no autenticar tooAzure Active Directory en absoluto, pero son toohello recta dirigida de la aplicación. Puede configurar esta opción cuando primero publicar una aplicación, o vaya tooyour aplicación Hola portal de Azure y editar la configuración de Proxy de aplicación Hola. 

toosee sus únicas opciones de inicio de sesión, siga estos pasos:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Navegue demasiado**Azure Active Directory** > **aplicaciones empresariales** > **todas las aplicaciones**.
3. Aplicación de hello seleccione cuyo inicio de sesión único en las opciones desee toomanage.
4. Seleccione **Inicio de sesión único**.

   ![Menú desplegable SSO](./media/application-proxy-sso-overview/single-sign-on-mode.png)

menú desplegable de Hello muestra cinco opciones para la aplicación de tooyour de inicio de sesión único:

* Inicio de sesión único de Azure AD deshabilitado
* Inicio de sesión único con contraseña
* Inicio de sesión vinculado
* Autenticación integrada de Windows
* Inicio de sesión basado en el encabezado

## <a name="azure-ad-single-sign-on-disabled"></a>Inicio de sesión único de Azure AD deshabilitado

Si no desea que la integración de Azure Active Directory toouse para aplicaciones de tooyour de inicio de sesión único, elija **Azure AD inicio de sesión único deshabilitado**. Con esta opción seleccionada, los usuarios pueden autenticarse dos veces. En primer lugar, se autentican tooAzure Active Directory y, a continuación, inicie sesión en la propia aplicación toohello. 

Esta opción es una buena opción si la aplicación local no requiere tooauthenticate a los usuarios, pero desea tooadd Azure Active Directory como un nivel de seguridad para el acceso remoto. 

## <a name="password-based-sign-on"></a>Inicio de sesión único con contraseña

Elija si desea toouse Azure Active Directory como un almacén de contraseñas para las aplicaciones locales, **sesión basado en contraseña**. Esta opción es adecuada si la aplicación se autentica con una combinación de nombre de usuario y contraseña en lugar de con tokens de acceso o encabezados. Con basado en contraseña de sesión, los usuarios necesitan toosign Hola de aplicación toohello primera vez que accedan a él. Después de eso, Azure Active Directory proporciona Hola username y password en nombre de usuario de Hola. 

Para obtener información acerca de cómo configurar el inicio de sesión con contraseña, consulte [Almacén de contraseñas para el inicio de sesión único con el proxy de aplicación](application-proxy-sso-azure-portal.md).

## <a name="linked-sign-on"></a>Inicio de sesión vinculado

Si ya tiene una solución de inicio de sesión único configurada para las identidades locales, elija **Inicio de sesión vinculado**. Esta opción permite a las soluciones SSO tooleverage existentes Azure Active Directory, pero todavía ofrece a los usuarios de aplicación de toohello de acceso remoto. 

Para más información sobre el inicio de sesión vinculado (conocido anteriormente como inicio de sesión único), consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="integrated-windows-authentication"></a>Autenticación integrada de Windows

Si las aplicaciones locales utilizan Authentication(IWA) integrada de Windows o si desea toouse delegación limitada de Kerberos (KCD) para el inicio de sesión único, elija **autenticación integrada de Windows**. Con esta opción, los usuarios solo necesitan tooauthenticate tooAzure Active Directory y, a continuación, el conector del Proxy de aplicación de hello suplanta Hola usuario tooget un token de Kerberos e inicie sesión en la aplicación toohello. 

Para más información acerca de cómo configurar la autenticación integrada de Windows, consulte [Delegación limitada de Kerberos para el inicio de sesión único con el proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md).

## <a name="header-based-sign-on"></a>Inicio de sesión basado en el encabezado 

Si las aplicaciones utilizan encabezados para la autenticación, elija **Inicio de sesión basado en el encabezado**. Con esta opción, los usuarios solo necesitan tooauthentication hello Azure Active Directory. Los socios de Microsoft con un servicio de autenticación de otro fabricante denominan PingAccess, que traduce el token de acceso de Azure Active Directory de hello en un formato de encabezado para la aplicación hello. 

Para más información acerca de cómo configurar la autenticación basada en el encabezado, consulte [Autenticación basada en el encabezado para el inicio de sesión único con el proxy de aplicación](application-proxy-ping-access.md).

## <a name="next-steps"></a>Pasos siguientes

- [Almacén de contraseñas para el inicio de sesión único con el proxy de aplicación](application-proxy-sso-azure-portal.md)
- [Delegación limitada de Kerberos para el inicio de sesión único con el proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md)
- [Autenticación basada en el encabezado para el inicio de sesión único con el proxy de aplicación](application-proxy-ping-access.md) 
