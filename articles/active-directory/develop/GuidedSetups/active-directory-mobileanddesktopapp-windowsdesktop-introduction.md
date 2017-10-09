---
title: "aaaAzure AD v2 Windows Desktop Introducción - introducción | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones .NET de escritorio de Windows (XAML) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
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
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a>Hola llamada API de Microsoft Graph desde una aplicación de escritorio de Windows

Esta guía muestra cómo una aplicación nativa de .NET de escritorio de Windows (XAML) puede obtener un token de acceso y llamar a la API Graph de Microsoft u otras API que requieran tokens de acceso desde un punto de conexión de Azure Active Directory v2.

Al final de Hola de esta guía, la aplicación se ser capaz de toocall API protegida mediante cuentas personales (incluidos outlook.com, live.com etc.) así como trabajar y cuentas de escuela de cualquier empresa u organización con Azure Active Directory.  

> Esta guía requiere Visual Studio 2015 Update 3 o Visual Studio 2017.  ¿No lo tiene? [Descargue Visual Studio 2017 de manera gratuita](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a>Funcionamiento de esta guía

![Funcionamiento de esta guía](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

aplicación de ejemplo de Hola creada en esta guía habilita una API de Microsoft Graph tooquery de aplicación de escritorio de Windows o una API Web que acepta los tokens de punto de conexión de Azure Active Directory v2. En este escenario, un símbolo (token) se agrega tooHTTP solicitudes a través del encabezado de autorización de Hola. Hola biblioteca de autenticación de Microsoft (MSAL) se administra la renovación y adquisición de tokens.


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Tratamiento de la adquisición de tokens para tener acceso a API web protegidas

Cuando se autentica el usuario hello, aplicación de ejemplo de Hola recibe un token que puede ser utilizado tooquery API Graph de Microsoft o una API Web protegida por Microsoft Azure Active Directory v2.

Las API, como Microsoft Graph requieren un tooallow de token de acceso obtener acceso a recursos específicos, por ejemplo, tooread un perfil de usuario, obtener acceso a calendario del usuario o envían un correo electrónico. La aplicación puede solicitar un token de acceso mediante MSAL tooaccess estos recursos mediante la especificación de ámbitos de API. Este token de acceso es agregado toohello encabezado de autorización HTTP para todas las llamadas efectuadas contra Hola al recurso protegido. 

MSAL administra el almacenamiento en caché y la actualización de los tokens de acceso automáticamente, así que no tiene que preocuparse por ello.


### <a name="nuget-packages"></a>Paquetes de NuGet

Esta guía usa Hola siguientes paquetes de NuGet:

|Biblioteca|Descripción|
|---|---|
|[Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client)|Biblioteca de autenticación de Microsoft (MSAL)|

