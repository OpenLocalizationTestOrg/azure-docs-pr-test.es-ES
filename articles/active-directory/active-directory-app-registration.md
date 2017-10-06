---
title: "el registro de aplicación de Active Directory aaaAzure | Documentos de Microsoft"
description: "Este artículo describe cómo toouse Hola tooregister portal Azure una aplicación con Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a>Registro de una aplicación en un inquilino de Azure Active Directory

Puede usar la aplicación de hello tooregister de portal de Azure con su inquilino de Azure Active Directory (Azure AD). Esto crea un identificador de aplicación para la aplicación hello y permite tooreceive símbolos (tokens).

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Elija al inquilino de Azure AD seleccionando su cuenta en hello superior derecho de la página de Hola.
3. En el panel de navegación izquierdo de hello, elija **más servicios**, haga clic en **registros de aplicaciones**y haga clic en **agregar**.
4. Siga las indicaciones de Hola y cree una nueva aplicación. Si desea ejemplos específicos de aplicaciones web o aplicaciones nativa, visite nuestras [guías de inicio rápido](active-directory-developers-guide.md).
  * Para aplicaciones Web, proporcione hello **dirección URL de inicio de sesión**, que es Hola dirección URL base de la aplicación, donde los usuarios pueden iniciar sesión en, por ejemplo, `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Para aplicaciones nativas, proporcionar un **URI de redireccionamiento**, que Azure AD usa tooreturn token respuestas. Escriba una aplicación de tooyour específico de valor,. por ejemplo`http://MyFirstAADApp`
5. Una vez completado el registro, Azure AD le asigna la aplicación un identificador de cliente único, hello identificador de aplicación.

## <a name="update-application-settings-from-hello-azure-portal"></a>Actualizar configuración de la aplicación de portal de Azure Hola

Puede modificar fácilmente la configuración de la aplicación existente mediante Hola portal de Azure. Por ejemplo, puede que desee tooconfigure una dirección URL de respuesta, que es donde Azure AD emite tokens respuestas. Puede que también desee tooconfigure permisos tooother aplicaciones, para la instancia tooallow sus tooaccess aplicación Hola API Graph de Microsoft. Puede hacer todo esto a través de la página de configuración de aplicación Hola.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Elija al inquilino de Azure AD seleccionando su cuenta en hello superior derecho de la página de Hola.
3. En el panel de navegación izquierdo de hello, elija **más servicios**, haga clic en **registros de aplicación**y elija la aplicación de lista de Hola.
4. Haga clic en **configuración** tooopen la página de configuración de hello para la aplicación hello.
  * Hola **propiedades** página le permite modificar la información general de Hola de aplicación hello. Esto incluye el nombre de la aplicación hello, dirección URL de inicio de sesión de Hola y dirección URL de cierre de sesión de Hola.
  * Hola **direcciones URL de respuesta** página permite tooadd una dirección URL de respuesta, que es donde Azure AD envía las respuestas de símbolo (token).
  * Hola **propietarios** página permite tooadd propietarios de las aplicaciones.
  * Hola **permisos** página permite tooconfigure permisos para la aplicación hello. Por ejemplo, hello tooaccess API Graph de Microsoft, haga clic en **agregar** y seleccione **Microsoft Graph** en el selector de hello API, a continuación, elija requerido, por ejemplo el permiso de hello **leer datos de directorio** .
  * Hola **claves** página permite tooadd secretos de aplicación. Hello secreto sólo se mostrará una vez inmediatamente después de crear, por lo que debe toocopy seguro para su uso posterior.

## <a name="use-hello-inline-manifest-editor"></a>Utilice el editor de manifiestos de hello en línea

Puede usar Hola alineado editor de manifiestos toomodify determinadas propiedades de la aplicación que no se exponen directamente en Hola portal de Azure. Por ejemplo, puede usar App ID URI la aplicación de toomodify Hola o tooenable Hola flujo implícitos de OAuth2.0 en lugar de autorización predeterminado de hello conceder flujo de código.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Elija al inquilino de Azure AD seleccionando su cuenta en hello superior derecho de la página de Hola.
3. En el panel de navegación izquierdo de hello, elija **más servicios**, haga clic en **registros de aplicación**y elija la aplicación de lista de Hola.
4. Haga clic en **manifiesto** de hello aplicación página tooopen Hola alineado editor de manifiestos.
5. Puede hacer cambios toohello directamente manifiesto y guárdelo cuando esté listo. Como alternativa, puede descargar tooopen manifiesto hello en su favoritos Hola de editor y la carga actualiza el manifiesto.

## <a name="next-steps"></a>Pasos siguientes

1. Extraer del repositorio hello [tutoriales](active-directory-developers-guide.md) para ver tutoriales detallados de las aplicaciones que se realiza la autenticación con Azure AD.
2. Consulte la lista completa de ejemplos de código en [GitHub](https://github.com/azure-samples).
