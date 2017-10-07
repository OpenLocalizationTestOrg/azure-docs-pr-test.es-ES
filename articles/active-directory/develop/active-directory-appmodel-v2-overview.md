---
title: extremo de v2.0 de Active Directory aaaAzure | Documentos de Microsoft
description: "Una introducción toobuilding las aplicaciones con Microsoft Account y Azure Active Directory inicio de sesión."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a>Inicio de sesión de usuarios de cuentas de Microsoft y de Azure AD en una sola aplicación
Hola más allá, un desarrollador de aplicaciones que deseaban toosupport ambas cuentas de Microsoft personales y cuentas para el trabajo de Azure Active Directory era necesario toointegrate con dos sistemas independientes.  Hola **punto de conexión de Azure AD v2.0** presenta una nueva versión de API de autenticación que permite toosign en ambos tipos de cuentas mediante una integración sencilla.  Aplicaciones que usan el punto de conexión de hello v2.0 también pueden usar las API de REST de hello [Microsoft Graph](https://graph.microsoft.io) con cualquier tipo de cuenta.

## <a name="getting-started"></a>Introducción
Elija la plataforma favoritos de hello sigue lista toobuild una aplicación con nuestras bibliotecas de código abierto y marcos de trabajo.  Como alternativa, puede usar nuestro toosend de documentación del protocolo OAuth 2.0 y OpenID Connect y recibir mensajes de protocolo directamente sin utilizar una biblioteca de autenticación.

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a>Novedades
información de Hello aquí será útil para entender qué es & lo que no es posible con el punto de conexión de hello v2.0.

* Obtenga información acerca de hello [tipos de aplicaciones puede crear con el punto de conexión de hello v2.0](active-directory-v2-flows.md).
* Comprender hello [limitaciones y restricciones, las restricciones](active-directory-v2-limitations.md) con el punto de conexión de hello v2.0.
* Este vídeo para el punto de conexión de hello v2.0 de información general, consulte:

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a>Referencia
Estos vínculos le servirán para explorar la plataforma de hello en profundidad:

* [Referencia de protocolos de v2.0](active-directory-v2-protocols.md)
* [Referencia de los tokens de v2.0](active-directory-v2-tokens.md)
* [Referencia de la biblioteca de la versión 2.0](active-directory-v2-libraries.md)
* [Ámbitos y consentimiento en el punto de conexión de hello v2.0](active-directory-v2-scopes.md)
* [Hola Microsoft Graph](https://graph.microsoft.io)

## <a name="help--support"></a>Ayuda y soporte técnico
Se trata de hello mejores lugares tooget ayuda con el desarrollo en Azure Active Directory.

* [`azure-active-directory` de Stack Overflow y etiquetas `adal`](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [Comentarios sobre Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> Si solo necesita toosign en cuentas profesionales o educativas de Azure Active Directory, debe comenzar con nuestras [Guía del desarrollador de Azure AD](active-directory-developers-guide.md).  el punto de conexión de Hello v2.0 está diseñado para su uso por los desarrolladores que necesiten explícitamente toosign en cuentas personales de Microsoft.

