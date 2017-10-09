---
title: "aaaAzure AD v2 iOS Introducción - introducción | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones de iOS (Swift) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a>Hola llamada API de Microsoft Graph desde una aplicación de iOS

Esta guía muestra cómo una aplicación de iOS nativo (Swift) puede obtener un acceso token y llamar a Hola API Graph de Microsoft u otras API que requiere tokens de acceso de punto de conexión de Azure Active Directory v2.

Al final de Hola de esta guía, la aplicación se ser capaz de toocall API protegida mediante cuentas personales (incluidos outlook.com, live.com etc.) así como trabajar y cuentas de escuela de cualquier empresa u organización con Azure Active Directory.

> ### <a name="pre-requisites"></a>Requisitos previos
> - Para esta guía se requiere XCode 8.x. Puede descargar XCode [aquí](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "Dirección URL de descarga de XCode").
> - [Carthage](https://github.com/Carthage/Carthage) para administración de paquetes

### <a name="how-this-guide-works"></a>Funcionamiento de esta guía

![Funcionamiento de esta guía](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

aplicación de ejemplo de Hola creada por esta guía permite un hello tooquery de aplicación de iOS API Graph de Microsoft o una API Web que acepta los tokens de punto de conexión de Azure Active Directory v2. En este escenario, un símbolo (token) se agrega tooHTTP solicitudes a través del encabezado de autorización de Hola. Hola biblioteca de autenticación de Microsoft (MSAL) se administra la renovación y adquisición de tokens.


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Tratamiento de la adquisición de tokens para tener acceso a API web protegidas

Cuando se autentica el usuario hello, aplicación de ejemplo de Hola recibe un token que puede ser utilizados tooquery Hola API Graph de Microsoft o una API Web protegida por Microsoft Azure Active Directory v2.

Las API, como Microsoft Graph requieren un tooallow de token de acceso obtener acceso a recursos específicos, por ejemplo, tooread un perfil de usuario, obtener acceso a calendario del usuario o envían un correo electrónico. La aplicación puede solicitar un token de acceso mediante MSAL mediante la especificación de ámbitos de API. Este token de acceso es agregado toohello encabezado de autorización HTTP para todas las llamadas efectuadas contra Hola al recurso protegido.

MSAL administra el almacenamiento en caché y la actualización de los tokens de acceso automáticamente, así que no tiene que preocuparse por ello.


### <a name="nuget-packages"></a>Paquetes NuGet

Esta guía usa Hola siguientes paquetes de NuGet:

|Biblioteca|Descripción|
|---|---|
|[MSAL.framework](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|Versión preliminar de Biblioteca de autenticación de Microsoft para iOS|

