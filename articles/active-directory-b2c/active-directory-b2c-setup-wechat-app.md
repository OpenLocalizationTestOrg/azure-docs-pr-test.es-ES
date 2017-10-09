---
title: "Azure Active Directory B2C: configuración de WeChat | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de WeChat en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a>Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de WeChat

> [!NOTE]
> Esta característica se encuentra en su versión preliminar.
> 

## <a name="create-a-wechat-application"></a>Creación de una aplicación de WeChat

toouse WeChat como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita una aplicación de WeChat toocreate y proporcionarla con los parámetros correctos de Hola. Se necesita un toodo de cuenta WeChat. Si no tiene una, puede obtenerla registrándose a través de una de sus aplicaciones móviles o mediante su número de QQ. A continuación, configurar su cuenta registrado con el programa para desarrolladores de WeChat Hola. Puede encontrar más información [aquí](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html):

### <a name="register-a-wechat-application"></a>Registro de una aplicación de WeChat

1. Vaya demasiado[https://open.weixin.qq.com/](https://open.weixin.qq.com/) e inicie sesión.
2. Haga clic en **管理中心** (centro de administración).
3. Siga los pasos necesarios de hello tooregister una nueva aplicación.
4. Para **授权回调域** (dirección URL de devolución de llamada), escriba `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Por ejemplo, si su `tenant_name` es contoso.onmicrosoft.com, conjunto Hola URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
5. Buscar y copia Hola **Id. de aplicación** y **clave de aplicación**. Los necesitará más adelante.

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a>Configuración de WeChat como proveedor de identidades del inquilino
1. Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.
2. En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.
3. Haga clic en **+ agregar** princip Hola de hoja de Hola.
4. Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola. Por ejemplo, escriba "WeChat".
5. Haga clic en **Tipo de proveedor de identidades**, seleccione **WeChat** y haga clic en **Aceptar**.
6. Haga clic en **Configurar este proveedor de identidades**.
7. Escriba hello **clave de aplicación** que copió anteriormente como hello **Id. de cliente**.
8. Escriba hello **secreto de la aplicación** que copió anteriormente como hello **secreto de cliente**.
9. Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de WeChat.

