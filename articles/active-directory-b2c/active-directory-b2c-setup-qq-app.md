---
title: "Azure Active Directory B2C: configuración de QQ | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de TT en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a>Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de TT

> [!NOTE]
> Esta característica se encuentra en su versión preliminar.
> 

## <a name="create-a-qq-application"></a>Creación de una aplicación de QQ

toouse TT como proveedor de identidades en Azure Active Directory (Azure AD) B2C, que necesita una aplicación TT toocreate y proporcionarla con los parámetros correctos de Hola. Se necesita un toodo de cuenta TT. Si no tiene una, puede obtenerla en [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).

### <a name="register-for-hello-qq-developer-program"></a>Registrarse para el programa de desarrolladores de hello TT

1. Vaya toohello [portal para desarrolladores de TT](http://open.qq.com) e inicie sesión con sus credenciales de cuenta TT.
2. Después de iniciar sesión, vaya demasiado[http://open.qq.com/reg](http://open.qq.com/reg) tooregister usted como desarrollador.
3. En el menú de hello, seleccione**个人**(para desarrolladores individuales).
4. Introducir información de hello necesario en el formulario de Hola y haga clic en**下一步**(paso siguiente).
5. Complete el proceso de comprobación de correo electrónico de Hola.

> [!NOTE]
> Necesitará toowait unos toobe días aprobado después de registrar como desarrollador. 

### <a name="register-a-qq-application"></a>Registro de una aplicación QQ

1. Vaya demasiado[https://connect.qq.com/index.html](https://connect.qq.com/index.html).
2. Haga clic en **应用管理** (administración de la aplicación).
3. Haga clic en **创建应用** (crear la aplicación).
4. Escriba la información de aplicación necesarios Hola.
5. Haga clic en **创建应用** (crear la aplicación).
6. Escriba la información de hello necesario.
7. Para hello**授权回调域**(dirección URL de devolución de llamada), escriba `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Por ejemplo, si su `tenant_name` es contoso.onmicrosoft.com, conjunto Hola URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
8. Haga clic en **创建应用** (crear la aplicación).
9. En la página de confirmación de hello, haga clic en**应用管理**página de administración de aplicaciones de toohello de tooreturn de (administración de aplicaciones).
10. Haga clic en**查看**aplicación toohello siguiente (vista) que se acaba de crear.
11. Haga clic en **修改** (editar).
12. Desde la parte superior de la página de Hola Hola copiar hello **Id. de aplicación** y **clave de aplicación**.

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a>Configuración de QQ como proveedor de identidades del inquilino
1. Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.
2. En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.
3. Haga clic en **+ agregar** princip Hola de hoja de Hola.
4. Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola. Por ejemplo, escriba "QQ".
5. Haga clic en **Tipo de proveedor de identidades**, seleccione **QQ** y haga clic en **Aceptar**.
6. Haga clic en **Configurar este proveedor de identidades**.
7. Escriba hello **clave de aplicación** que copió anteriormente como hello **Id. de cliente**.
8. Escriba hello **secreto de la aplicación** que copió anteriormente como hello **secreto de cliente**.
9. Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de TT.

