---
title: "aaaSingle inicio de sesión tooapps con el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Activar inicio de sesión único para las aplicaciones locales publicadas con Proxy de aplicación de Azure AD en hello portal de Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a>Almacén de contraseñas para el inicio de sesión único con el proxy de aplicación

El proxy de aplicación de Azure Active Directory le ayuda a mejorar la productividad mediante la publicación de aplicaciones locales de manera que los empleados remotos puedan tener acceso seguro a estas. Hola portal de Azure, también puede configurar single sign-on (SSO) toothese aplicaciones. Los usuarios solo necesitan tooauthenticate con Azure AD y puede acceder a la aplicación empresarial sin necesidad de toosign nuevo.

El proxy de aplicación admite varios [modos de inicio de sesión único](application-proxy-sso-overview.md). El inicio de sesión basado en contraseña se ha creado para aplicaciones que usan una combinación de nombre de usuario/contraseña para la autenticación. Al configurar sesión basado en contraseña para la aplicación, los usuarios tendrán toosign en la aplicación una vez de toohello local. Después de eso, Azure Active Directory almacena la información de inicio de sesión de Hola y proporciona automáticamente lo toohello aplicación cuando los usuarios tener acceso remoto. 

Debe haber publicado y probado ya la aplicación con el proxy de aplicación. Si no es así, siga los pasos de hello en [publicar aplicaciones mediante el Proxy de aplicación de Azure AD](application-proxy-publish-azure-portal.md) , a continuación, vuelve aquí proceden. 

## <a name="set-up-password-vaulting-for-your-application"></a>Configuración del almacenamiento de contraseñas para la aplicación

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador.
2. Seleccione **Azure Active Directory** > **Aplicaciones empresariales** > **Todas las aplicaciones**.
3. En lista de hello, seleccione la aplicación hello que desea tooset seguridad con SSO.  
4. Seleccione **Inicio de sesión único**.

   ![Seleccionar inicio de sesión único](./media/application-proxy-sso-azure-portal/select-sso.png)

5. Para el modo SSO de hello, elija **sesión basado en contraseña**.
6. Hola inicio de sesión en la dirección URL, escriba la dirección URL de hello para la página de Hola donde los usuarios escribir su nombre de usuario y contraseña toosign en aplicación tooyour fuera de la red corporativa de Hola. Esto puede ser Hola dirección URL externa que creó cuando publicó la aplicación hello a través de Proxy de aplicación. 

   ![Elegir inicio de sesión basado en contraseña y escribir la URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. Seleccione **Guardar**.

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a>Prueba de la aplicación

Ir a dirección URL de tooexternal que ha configurado para la aplicación de tooyour de acceso remoto. Inicie sesión con sus credenciales para esa aplicación (o las credenciales de Hola para una cuenta de prueba que configura con acceso). Cuando inicie sesión correctamente, debe ser capaz de tooleave Hola aplicación y vuelven a estar sin escribir sus credenciales de nuevo. 

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información sobre otra maneras tooimplement [inicio de sesión único con el Proxy de aplicación](application-proxy-sso-overview.md)
- Más información sobre [Consideraciones de seguridad al obtener acceso a aplicaciones de forma remota con el Proxy de aplicación de Azure AD](application-proxy-security-considerations.md)