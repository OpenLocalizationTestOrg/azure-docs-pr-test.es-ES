---
title: "aaaAzure AD v2 Android Introducción - introducción | Documentos de Microsoft"
description: "Cómo puede una aplicación de Android obtener un token de acceso y llamar a las API Graph que requieren tokens de acceso desde el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a>Hola llamada API de Microsoft Graph desde una aplicación de Android

En esta guía se muestra cómo una aplicación nativa de Android puede obtener un token de acceso y llamar a la API Graph de Microsoft u otras API que requieran tokens de acceso desde un punto de conexión de Azure Active Directory v2.

Al final de Hola de esta guía, la aplicación se ser capaz de toocall API protegida mediante cuentas personales (incluidos outlook.com, live.com etc.) así como trabajar y cuentas de escuela de cualquier empresa u organización con Azure Active Directory.  

### <a name="how-this-sample-works"></a>Funcionamiento de este ejemplo
![Funcionamiento de este ejemplo](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

ejemplo de Hola creado en esta guía se basa en un escenario donde una aplicación Android es tooquery usa una API Web que acepta los tokens de Azure Active Directory v2 endpoint – en este caso, Microsoft Graph API. En este escenario, un símbolo (token) se agrega tooHTTP solicitudes a través del encabezado de autorización de Hola. Hola biblioteca de autenticación de Microsoft (MSAL) se administra la renovación y adquisición de tokens.

### <a name="pre-requisites"></a>Requisitos previos
* Esta guía paso a paso se centra en Android Studio, pero cualquier otro entorno de desarrollo de aplicaciones de Android también es aceptable. 
* Se requiere Android SDK 21 o posterior (se recomienda SDK 25).
* Se requiere Google Chrome o un explorador web que use pestañas personalizadas para esta versión de la biblioteca de autenticación de Microsoft (MSAL) para Android.

> Nota: Google Chrome no se incluye en el Emulador de Visual Studio para Android. Le recomendamos que tootest este código en un emulador con API de 25 o una imagen con API 21 o posterior que tenga con Google Chrome instalado.


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a>¿Cómo toohandle token adquisición tooaccess API Web protegida

Cuando se autentica el usuario hello, aplicación de ejemplo de Hola recibe un token que puede ser utilizado tooquery API Graph de Microsoft o una API Web protegida por Microsoft Azure Active Directory v2.

Las API, como Microsoft Graph requieren un tooallow de token de acceso obtener acceso a recursos específicos, por ejemplo, tooread un perfil de usuario, obtener acceso a calendario del usuario o envían un correo electrónico. La aplicación puede solicitar un token de acceso mediante MSAL tooaccess estos recursos mediante la especificación de ámbitos de API. Este token de acceso es agregado toohello encabezado de autorización HTTP para todas las llamadas efectuadas contra Hola al recurso protegido. 

MSAL administra el almacenamiento en caché y la actualización de los tokens de acceso automáticamente, así que no tiene que preocuparse por ello.

### <a name="libraries"></a>Bibliotecas

Esta guía usa Hola después de bibliotecas:

|Biblioteca|Descripción|
|---|---|
|[com.microsoft.identity.client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|Biblioteca de autenticación de Microsoft (MSAL)|
