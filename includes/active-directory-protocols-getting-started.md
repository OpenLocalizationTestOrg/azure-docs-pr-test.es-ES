---
title: "aaaAzure AD Introducción al protocolo .NET | Documentos de Microsoft"
description: "Cómo tener acceso a toouse HTTP mensajes tooauthorize tooweb aplicaciones y las API web de su inquilino mediante Azure AD."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 5bd54af028c445afd3f35d67d47d7c84b476c757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## Registro de la aplicación con el inquilino de AD
En primer lugar, deberá tooregister la aplicación con su inquilino de Azure Active Directory (Azure AD). Esto se ofrecen un identificador de aplicación para la aplicación, así como habilitar tooreceive símbolos (tokens).

* Inicie sesión en toohello [Portal de Azure](https://portal.azure.com).
* Elija al inquilino de Azure AD, haga clic en su cuenta en hello superior derecho de la página de Hola.
* En el panel de navegación del lado izquierdo de hello, haga clic en **Azure Active Directory**.
* Haga clic en **Registros de aplicaciones** y en **Agregar**.
* Siga las indicaciones de Hola y cree una nueva aplicación. Para este tutorial, no importa si se trata de una aplicación web o nativa, pero si desea ver ejemplos específicos de aplicaciones web o nativas, consulte nuestras [guías de inicio rápido](../articles/active-directory/develop/active-directory-developers-guide.md).
  * Para aplicaciones Web, proporcione hello **dirección URL de inicio de sesión** que es Hola dirección URL base de la aplicación, donde los usuarios pueden iniciar sesión en, por ejemplo, `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Para aplicaciones nativas, proporcionar un **URI de redireccionamiento**, que Azure AD utilizará las respuestas de símbolo (token) de tooreturn. Escriba una aplicación de tooyour específico de valor,. por ejemplo`http://MyFirstAADApp`
* Una vez completado el registro, Azure AD se asigna un identificador de cliente único de la aplicación, Hola identificador de aplicación. Necesitará este valor en las secciones siguientes de hello, por lo tanto cópiela desde la página de aplicación Hola.
