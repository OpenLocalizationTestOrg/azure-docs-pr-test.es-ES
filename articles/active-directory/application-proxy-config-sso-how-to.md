---
title: "aaaHow tooconfigure único inicio de sesión tooan aplicación de Proxy de aplicación | Documentos de Microsoft"
description: "Cómo se pueden configurar rápidamente aplicaciones de proxy de aplicación de tooyour de inicio de sesión único"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e1289203177c77b3a8bcc9058c5c0b8ae50f243e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-single-sign-on-tooan-application-proxy-application"></a>Cómo tooconfigure single sign-on tooan aplicación de Proxy de aplicación

Inicio de sesión único (SSO) permite que su tooaccess a los usuarios una aplicación sin autenticar varias veces. Permite hello toooccur de autenticación único en la nube de hello, en Azure Active Directory y el servicio de Hola o conector tooimpersonate Hola usuario toocomplete los desafíos de autenticación adicional de la aplicación hello.

## <a name="how-tooconfigure-single-sign-on"></a>¿Cómo tooconfigure inicio de sesión único
tooconfigure SSO, primero asegúrese de que la aplicación está configurada para la autenticación previa a través de Azure Active Directory. toodo, vaya demasiado**Azure Active Directory**  - &gt; **aplicaciones empresariales**  - &gt; **todas las aplicaciones**  - &gt; La aplicación  **- &gt; Proxy de aplicación**. En esta página, consulte "Autenticación previa" hello campo y asegúrese de que se establece demasiado "Azure Active Directory. 

Para obtener más información sobre los métodos de autenticación previa de hello, vea el paso cuatro de hello [documento de publicación de aplicación](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

   ![Método de autenticación previa en Azure Portal](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a>Configuración de modos de inicio de sesión únicos para aplicaciones de proxy de aplicación
A continuación se configure el tipo específico de Hola de inicio de sesión único. métodos de inicio de sesión de Hola se clasifican en función de qué tipo de aplicación de autenticación hello back-end utiliza. Las aplicaciones de proxy de aplicación admiten tres tipos de inicio de sesión:

-   **Basado en contraseña Sign-On**: basado en contraseña de inicio de sesión puede utilizarse para cualquier aplicación que utilice los campos de nombre de usuario y contraseña en toosign. Los pasos de configuración se encuentran en nuestra [documentación sobre la configuración de SSO con contraseña](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications).

-   **Autenticación de Windows integrada**: para las aplicaciones que utilizan la autenticación de Windows integrada (IWA), el inicio de sesión único se habilita a través de la delegación limitada de Kerberos (KCD). Esto concede permiso de conectores Proxy de aplicación en los usuarios de Active Directory tooimpersonate y toosend y recibir tokens en su nombre. Encontrará detalles sobre cómo configurar KCD en hello [Single Sign-On con documentación KCD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).

-   **Inicio de sesión basado en el encabezado**: el inicio de sesión basado en el encabezado se habilita a través de una asociación y requiere configuración adicional. Para obtener más información de asociación de Hola y de instrucciones paso a paso para configurar la aplicación tooan de inicio de sesión único que usa encabezados para la autenticación, vea hello [PingAccess para obtener documentación de Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).

Cada una de estas opciones se puede encontrar yendo aplicación tooyour en hello de apertura y de "Aplicaciones empresariales" **Single Sign-On** página en el menú de la izquierda Hola. Tenga en cuenta que si la aplicación se creó en el portal antiguo de hello, no puede ver todas estas opciones.

En esta página, también verá una opción adicional para el inicio de sesión: Inicio de sesión vinculado. El proxy de aplicación también la admite. Sin embargo, tenga en cuenta que esta opción no agrega la aplicación toohello de inicio de sesión único. Una vez dicho esto aplicación hello ya habrá implementado con otro servicio, como los servicios de federación de Active Directory el inicio de sesión único. 

Esta opción permite a un administrador toocreate una aplicación de tooan de vínculo que los usuarios llegará al obtener acceso a la aplicación hello. Por ejemplo, si hay una aplicación que está configurado tooauthenticate a los usuarios con servicios de federación de Active Directory 2.0, un administrador puede usar Hola "vinculado Sign-On" opción toocreate un tooit de vínculo en el panel de acceso de Hola.

## <a name="next-steps"></a>Pasos siguientes
[Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md)
