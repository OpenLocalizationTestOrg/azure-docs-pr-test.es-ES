---
title: "Azure Active Directory B2C: configuración de Twitter | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Twitter en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a>Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Twitter

> [!NOTE]
> Esta característica se encuentra en su versión preliminar.
> 

## <a name="create-a-twitter-application"></a>Crear una aplicación de Twitter
toouse Twitter como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita una aplicación de Twitter toocreate y proporcionarle los parámetros correctos de Hola. Se necesita un toodo de cuenta de desarrollador de Twitter. Si no tiene una, puede obtenerla en [https://dev.twitter.com/](https://dev.twitter.com/).

1. Vaya toohello [sitio Web del desarrollador de Twitter](https://dev.twitter.com/) e inicie sesión con sus credenciales.
2. Haga clic en **Mis aplicaciones** en **Herramientas y soporte técnico** y, después, haga clic en **Crear una aplicación nueva**. 
3. En el formulario de hello, proporcione un valor para hello **nombre**, **descripción**, y **sitio Web**.
4. Para hello **dirección URL de devolución de llamada**, escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`. Asegúrese de que tooreplace **{tenant}** con el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).
5. Comprobar Hola cuadro tooagree toohello **acuerdo para desarrolladores de** y haga clic en **crear su aplicación de Twitter**.
6. Una vez creada la aplicación hello, haga clic en **claves y Tokens de acceso**.
7. Copiar valor de Hola de **clave de consumidor** y **secreto de consumidor**. Necesitará ambos tooconfigure Twitter como proveedor de identidades en su inquilino.

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a>Configuración de Twitter como proveedor de identidades del inquilino
1. Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.
2. En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.
3. Haga clic en **+ agregar** princip Hola de hoja de Hola.
4. Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola. Por ejemplo, escriba "Twitter".
5. Haga clic en **Tipo de proveedor de identidades**, seleccione **Twitter** y haga clic en **Aceptar**.
6. Haga clic en **configurar este proveedor de identidades** y escriba Hola Twitter **clave de consumidor** para hello **Id. de cliente** y Hola Twitter **secreto del consumidor**para hello **secreto de cliente**.
7. Haga clic en **Aceptar**y, a continuación, haga clic en **crear** toosave la configuración de Twitter.

