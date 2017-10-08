---
title: "Azure Active Directory B2C: configuración de Facebook | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Facebook en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a>Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Facebook
## <a name="create-a-facebook-application"></a>Creación de una aplicación de Facebook
toouse Facebook como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita toocreate una aplicación de Facebook y proporcionarle los parámetros correctos de Hola. Se necesita un toodo de cuenta de Facebook. Si no tiene una, puede obtenerla en [https://www.facebook.com/](https://www.facebook.com/).

1. Vaya toohello [Facebook para los desarrolladores](https://developers.facebook.com/) credenciales de cuenta de sitio Web e inicie sesión con su Facebook.
2. Si no lo ha hecho ya, deberá tooregister como un programador de Facebook. toodo, haga clic en **registrar** (en la esquina de superior derecha de Hola de página hello), acepte las directivas de Facebook y completar los pasos de registro de hello.
3. Haga clic en **Mis aplicaciones** y luego en **Agregar una nueva aplicación**. 
4. En el formulario de hello, proporcionar un **nombre para mostrar** y válido **correo electrónico de contacto**.
5. Haga clic en **Create App ID** (Crear id. de aplicación). Esto puede requieren directivas de plataforma Facebook tooaccept y completar una comprobación de seguridad en línea.
6. En la columna izquierda de hello, haga clic en **configuración** y, a continuación, seleccione **básica** si no ha seleccionado ya.
7. Seleccione un valor de **Categoría**. 
8. Haga clic en **+Add Platform** (+Agregar plataforma) y seleccione **Sitio web**.
   
    ![Facebook - Configuración](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - Configuración - Sitio web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. Escriba `https://login.microsoftonline.com/` en hello **dirección URL del sitio** campo y, a continuación, haga clic en **guardar cambios** final Hola de página Hola.
   
    ![Facebook - Dirección URL del sitio](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. Copiar valor de Hola de **identificador de la aplicación**. Haga clic en **mostrar** y copie el valor de Hola de **secreto de la aplicación**. Necesitará ambos tooconfigure Facebook como proveedor de identidades en su inquilino. El **secreto de la aplicación** es una credencial de seguridad importante.
   
    ![Facebook - Id. de aplicación y el secreto de la aplicación](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. Haga clic en **+ agregar producto** Hola de navegación izquierdo y, a continuación, Hola **Set Up** botón **inicio de sesión de Facebook**.
   
    ![Facebook - Inicio de sesión de Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. Haga clic en **configuración** en hello nav derecha bajo **inicio de sesión de Facebook**

    ![Facebook - Configuración de inicio de sesión de Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. Escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **URI de redireccionamiento válido OAuth** campo hello **configuración de cliente OAuth** sección. Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com). Haga clic en **guardar cambios** final Hola de página Hola.
    
    ![Facebook - URI de redireccionamiento de OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. toomake su aplicación de Facebook utilizable por Azure AD B2C, necesita toomake estén disponibles públicamente. Para ello, haga clic en **revisión de aplicación** en la barra de navegación izquierda de Hola y Hola activar cambiar al principio de Hola de página de hello demasiado**Sí** y haga clic en **confirmar**.
    
    ![Facebook - Público de la aplicación](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a>Configuración de Facebook como proveedor de identidades del inquilino
1. Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.
2. En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.
3. Haga clic en **+ agregar** princip Hola de hoja de Hola.
4. Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola. Por ejemplo, escriba "Facebook".
5. Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **Facebook** y haga clic en **OK** (Aceptar).
6. Haga clic en **configurar este proveedor de identidades** y escriba Hola Id. y aplicación secreto de la aplicación (de Hola aplicación de Facebook que creó anteriormente) en hello **Id. de cliente** y **secreto del cliente**campos respectivamente.
7. Haga clic en **Aceptar**y, a continuación, haga clic en **crear** toosave la configuración de Facebook.

> [!NOTE]
> Agregar un **proveedor de identidades** tooyour inquilino no modifica las directivas existentes. Recuerde tooupdate las directivas mediante la inclusión de proveedor de identidades de Hola que acaba de crear.
>