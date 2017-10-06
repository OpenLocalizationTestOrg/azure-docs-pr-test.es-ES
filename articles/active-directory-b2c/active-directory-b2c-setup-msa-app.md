---
title: "Azure Active Directory B2C: configuración de la cuenta Microsoft | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Microsoft en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a>Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Microsoft
## <a name="create-a-microsoft-account-application"></a>Creación de una aplicación de cuenta Microsoft
toouse cuenta de Microsoft como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita toocreate una aplicación de la cuenta de Microsoft y suministrarle los parámetros correctos de Hola. Se necesita un toodo de cuenta de Microsoft. Si no tiene una, puede obtenerla en [https://www.live.com/](https://www.live.com/).

1. Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e inicie sesión con sus credenciales de cuenta de Microsoft.
2. Haga clic en **Agregar una aplicación**.
   
    ![Cuenta Microsoft: adición de una aplicación nueva](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. Especifique un **nombre** para la aplicación y haga clic en **Crear aplicación**.
   
    ![Cuenta Microsoft: nombre de la aplicación](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. Copiar valor de Hola de **identificador de la aplicación**. Necesitará tooconfigure cuenta de Microsoft como proveedor de identidades en su inquilino.
   
    ![Cuenta Microsoft: Id. de la aplicación](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. Haga clic en **Agregar plataforma** y elija **Web**.
   
    ![Cuenta Microsoft: Agregar plataforma](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Cuenta Microsoft: Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. Escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **URI de redireccionamiento** campo. Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).
   
    ![Cuenta Microsoft: dirección URL de redireccionamiento](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. Haga clic en **generar nueva contraseña** en hello **aplicación secretos** sección. Copiar contraseña nueva hello muestra en pantalla. Necesitará tooconfigure cuenta de Microsoft como proveedor de identidades en su inquilino. Esta contraseña es una credencial de seguridad importante.
   
    ![Cuenta Microsoft: Generar nueva contraseña](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Cuenta Microsoft: Nueva contraseña](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. Casilla de Hola que dice **soporte técnico del SDK de Live** en hello **opciones avanzadas** sección. Haga clic en **Guardar**.
   
    ![Cuenta Microsoft: Soporte técnico de SDK de Live](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a>Configuración de una cuenta Microsoft como proveedor de identidades de su inquilino
1. Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.
2. En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.
3. Haga clic en **+ agregar** princip Hola de hoja de Hola.
4. Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola. Por ejemplo, escriba "MSA".
5. Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **Microsoft account** (Cuenta Microsoft) y haga clic en **OK** (Aceptar).
6. Haga clic en **configurar este proveedor de identidades** y escriba Hola Id. de aplicación y la contraseña de hello aplicación de cuentas de Microsoft que creó anteriormente.
7. Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave configuración de la cuenta de Microsoft.

