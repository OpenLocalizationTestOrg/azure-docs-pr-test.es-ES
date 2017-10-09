---
title: "aaaAzure AD v2 ASP.NET Web Server Introducción - introducción | Documentos de Microsoft"
description: "Implementación de inicio de sesión de Microsoft en una solución ASP.NET con una aplicación basada en un explorador web tradicional mediante el estándar OpenID Connect"
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a>Agregar inicie sesión con la aplicación web ASP.NET Microsoft tooan

Esta guía demuestra cómo tooimplement inicie sesión con Microsoft mediante una solución de MVC de ASP.NET con una aplicación basada en Explorador de web tradicional con OpenID Connect. 

Al final de Hola de esta guía, la aplicación de ser capaz de tooaccept de inicio de sesión inicios de personal cuentas (incluidos outlook.com, live.com u otros datos) así como de trabajo y cuentas de cualquier empresa u organización que se integra con Azure Active Directory educativas. 

> Esta guía requiere Visual Studio 2015 Update 3 o Visual Studio 2017.  ¿No lo tiene?  [Descargue Visual Studio 2017 de manera gratuita](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>Funcionamiento de esta guía

![Funcionamiento de esta guía](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

Esta guía se basa en el escenario de Hola donde un explorador tiene acceso a un sitio web ASP.NET, que solicita un tooauthenticate de usuario a través de un botón de inicio de sesión. En este escenario, la mayor parte de la página web de hello trabajo toorender Hola se produce en el lado del servidor de Hola.

## <a name="libraries"></a>Bibliotecas

Esta guía usa Hola después de bibliotecas:

|Biblioteca|Descripción|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|Software intermedio que permite que una aplicación toouse OpenIdConnect para la autenticación|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|Middleware que permite una sesión de usuario de aplicación toomaintain uso de cookies|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|Permite que las aplicaciones basadas en OWIN toorun en IIS mediante la canalización de solicitudes ASP.NET de Hola|

