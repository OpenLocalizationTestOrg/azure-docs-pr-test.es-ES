---
title: "Azure Active Directory B2C: configuración de LinkedIn | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de LinkedIn en las aplicaciones que están protegidas por Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a>Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de LinkedIn
## <a name="create-a-linkedin-application"></a>Creación de una aplicación de LinkedIn
toouse LinkedIn como proveedor de identidades en Azure Active Directory (Azure AD) B2C, se necesita una aplicación de LinkedIn toocreate y suministrarlo con los parámetros correctos de Hola. Se necesita un toodo de cuenta de LinkedIn. Si no tiene una, puede obtenerla en [https://www.linkedin.com/](https://www.linkedin.com/).

1. Vaya toohello [sitio Web de desarrolladores de LinkedIn](https://www.developer.linkedin.com/) e inicie sesión con sus credenciales de cuenta de LinkedIn.
2. Haga clic en **mis aplicaciones** en Hola barra de menús superior y, a continuación, haga clic en **crear aplicación**.
   
    ![LinkedIn - nueva aplicación](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. Hola **crear una nueva aplicación** forman, rellene la información pertinente de hello (**nombre de la compañía**, **nombre**, **descripción**, **Dirección URL del logotipo de la aplicación**, **uso de las aplicaciones**, **URL del sitio Web**, **correo electrónico empresarial** y **teléfono del trabajo**).
4. Acepta toohello **LinkedIn términos de uso de la API** y haga clic en **enviar**.
   
    ![LinkedIn - registrar aplicación](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. Copiar valores de hello de **Id. de cliente** y **secreto de cliente**. [Los encontrará en **Authentication Keys** (Claves de autenticación)]. Necesitará ambos tooconfigure LinkedIn como proveedor de identidades en su inquilino.
   
   > [!NOTE]
   > **secreto de cliente** es una credencial de seguridad importante.
   > 
   > 
6. Escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **autorizado redirigir las direcciones URL** campo (en **OAuth 2.0**). Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contoso.onmicrosoft.com). Haga clic en **Add** (Agregar) y después en **Update** (Actualizar). Hola **{tenant}** valor distingue mayúsculas de minúsculas.
   
    ![LinkedIn - configurar aplicación](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a>Configuración de LinkedIn como proveedor de identidades del inquilino
1. Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.
2. En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.
3. Haga clic en **+ agregar** princip Hola de hoja de Hola.
4. Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola. Por ejemplo "LI".
5. Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **LinkedIn** y haga clic en **Aceptar**.
6. Haga clic en **configurar este proveedor de identidades** y escriba el secreto de cliente y el Id. de cliente de Hola de hello aplicación LinkedIn que creó anteriormente.
7. Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de LinkedIn.

