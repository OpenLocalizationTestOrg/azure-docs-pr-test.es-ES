---
title: "Azure Active Directory B2C: configuración de Weibo | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Weibo en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a>Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Weibo

> [!NOTE]
> Esta característica se encuentra en su versión preliminar. No utilice este proveedor de identidades en su entorno de producción.
> 

## <a name="create-a-weibo-application"></a>Creación de una aplicación de Weibo

toouse Weibo como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita una aplicación de Weibo toocreate y proporcionarla con los parámetros correctos de Hola. Se necesita un toodo de cuenta Weibo. Si no tiene una, puede obtenerla en [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).

### <a name="register-for-hello-weibo-developer-program"></a>Registrarse para el programa de desarrolladores de hello Weibo

1. Vaya toohello [portal para desarrolladores de Weibo](http://open.weibo.com/) e inicie sesión con sus credenciales de cuenta Weibo.
2. Después de iniciar sesión, haga clic en el nombre para mostrar en la esquina superior derecha de Hola.
3. En la lista desplegable de hello, seleccione**编辑开发者信息**(editar la información para desarrolladores).
4. Introducir información de hello necesario en el formulario de Hola y haga clic en**提交**(enviar).
5. Complete el proceso de comprobación de correo electrónico de Hola.
6. Vaya toohello [página de comprobación de identidad](http://open.weibo.com/developers/identity/edit).
7. Introducir información de hello necesario en el formulario de Hola y haga clic en**提交**(enviar).

### <a name="register-a-weibo-application"></a>Registro de una aplicación de Weibo

1. Vaya toohello [nueva página de registro de aplicación de Weibo](http://open.weibo.com/apps/new).
2. Escriba la información de aplicación necesaria Hola.
3. Haga clic en **创建** (crear).
4. Copiar valores de hello de **clave de aplicación** y **secreto de la aplicación**. Lo necesitará más adelante.
5. Cargar fotografías Hola necesario y escriba la información necesaria de Hola.
6. Haga clic en **保存以上信息** (guardar).
7. Haga clic en **高级信息** (información avanzada).
8. Haga clic en**编辑**(Editar) siguiente campo toohello para OAuth2.0**授权设置**(dirección URL de redireccionamiento).
9. Escriba `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` para OAuth2.0 **授权设置** (dirección URL de redireccionamiento). Por ejemplo, si su `tenant_name` es contoso.onmicrosoft.com, conjunto Hola URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
10. Haga clic en **提交** (enviar).  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a>Configuración de Weibo como proveedor de identidades del inquilino
1. Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.
2. En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.
3. Haga clic en **+ agregar** princip Hola de hoja de Hola.
4. Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola. Por ejemplo, escriba "Weibo".
5. Haga clic en **Tipo de proveedor de identidades**, seleccione **Weibo** y haga clic en **Aceptar**.
6. Haga clic en **Configurar este proveedor de identidades**.
7. Escriba hello **clave de aplicación** que copió anteriormente como hello **Id. de cliente**.
8. Escriba hello **secreto de la aplicación** que copió anteriormente como hello **secreto de cliente**.
9. Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de Weibo.

