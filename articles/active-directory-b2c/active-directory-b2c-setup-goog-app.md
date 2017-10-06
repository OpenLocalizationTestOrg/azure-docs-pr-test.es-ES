---
title: "Azure Active Directory B2C: configuración de Google+ | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Google + en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a>Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Google +
## <a name="create-a-google-application"></a>Creación de una aplicación de Google+
toouse Google + como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita una aplicación de Google + toocreate y proporcionarla con los parámetros correctos de Hola. Se necesita una cuenta de Google + toodo. Si no tiene una, puede obtenerla en [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).

1. Vaya toohello [Google Developers Console](https://console.developers.google.com/) e inicie sesión con sus credenciales de cuenta de Google +.
2. Haga clic en **Create project** (Crear proyecto), escriba un nombre de proyecto en **Project name** y haga clic en **Create** (Crear).
   
    ![Google+: introducción](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+: nuevo proyecto](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. Haga clic en **API Manager** y, a continuación, haga clic en **credenciales** Hola barra de navegación izquierda.
4. Haga clic en hello **pantalla de consentimiento de OAuth** ficha situada en la parte superior de Hola.
   
    ![Google+: credenciales](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. Seleccione o especifique una dirección de correo electrónico válida en **Email address**, especifique un nombre de producto en **Product name** y haga clic en **Save** (Guardar).
   
    ![Google+: pantalla de consentimiento de OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. Haga clic en **New credentials** (Nuevas credenciales) y, luego, elija **OAuth client ID** (Id. de cliente de OAuth).
   
    ![Google+: pantalla de consentimiento de OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. En **Application type** (Tipo de aplicación), seleccione **Web application** (Aplicación web).
   
    ![Google+: pantalla de consentimiento de OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. Proporcionar un **nombre** para la aplicación, escriba `https://login.microsoftonline.com` en hello **orígenes de JavaScript autorizados** campo, y `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **autorizadas redirigir URI**campo. Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com). Hola **{tenant}** valor distingue mayúsculas de minúsculas. Haga clic en **Crear**.
   
    ![Google+: creación del identificador de cliente](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. Copiar valores de hello de **Id. de cliente** y **secreto de cliente**. Necesitará ambos tooconfigure Google + como proveedor de identidades en su inquilino. **Secreto del cliente** es una credencial de seguridad importante.
   
    ![Google+: secreto de cliente](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a>Configuración de Google+ como proveedor de identidades del inquilino
1. Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.
2. En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.
3. Haga clic en **+ agregar** princip Hola de hoja de Hola.
4. Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola. Por ejemplo, "G+".
5. Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **Google** y haga clic en **OK** (Aceptar).
6. Haga clic en **configurar este proveedor de identidades** y escriba el secreto de cliente y el Id. de cliente de Hola de hello aplicación de Google + que creó anteriormente.
7. Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de Google +.

