---
title: "Azure Active Directory B2C: configuración de Amazon | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Amazon en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a>Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Amazon
## <a name="create-an-amazon-application"></a>Creación de una aplicación de Amazon
toouse Amazon como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita toocreate una aplicación de Amazon y proporcionarle los parámetros correctos de Hola. Se necesita un toodo de cuenta de Amazon. Si no tiene una, puede obtenerla en [http://www.amazon.com/](http://www.amazon.com/).

1. Vaya toohello [Centro para desarrolladores de Amazon](https://login.amazon.com/) e inicie sesión con sus credenciales de cuenta de Amazon.
2. Si no lo ha hecho ya, haga clic en **Sign Up**, siga los pasos de registro del desarrollador de Hola y acepte la política de Hola.
3. Haga clic en **Register new application**(Registrar nueva aplicación).
   
    ![Registrar una nueva aplicación en el sitio Web de Amazon Hola](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. Especifique la información de la aplicación [**Name** (Nombre), **Description** (Descripción) y **Privacy Notice URL** (Dirección URL de aviso de privacidad)] y haga clic en **Save** (Guardar).
   
    ![Proporcionar información de la aplicación para registrar una nueva aplicación en Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. Hola **configuración Web** sección, copia los valores de hello de **Id. de cliente** y **secreto de cliente**. (Debe hello tooclick **mostrar secreto** botón toosee esto.) Necesita ambos tooconfigure Amazon como proveedor de identidades en su inquilino. Haga clic en **editar** final Hola de sección Hola. **secreto de cliente** es una credencial de seguridad importante.
   
    ![Proporcionar el identificador de cliente y el secreto de cliente para la nueva aplicación en Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. Escriba `https://login.microsoftonline.com` en hello **orígenes de JavaScript permite** campo y `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **permite direcciones URL de retorno** campo. Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contoso.onmicrosoft.com). Haga clic en **Guardar**. Hola **{tenant}** valor distingue mayúsculas de minúsculas.
   
    ![Proporcionar orígenes de JavaScript y direcciones URL de retorno para la nueva aplicación en Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a>Configuración de Amazon como proveedor de identidades del inquilino
1. Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.
2. En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.
3. Haga clic en **+ agregar** princip Hola de hoja de Hola.
4. Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola. Por ejemplo, "Amzn".
5. Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **Amazon** y haga clic en **OK** (Aceptar).
6. Haga clic en **configurar este proveedor de identidades** y escriba el secreto de cliente y el Id. de cliente de Hola de hello aplicaciones de Amazon que creó anteriormente.
7. Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de Amazon.

