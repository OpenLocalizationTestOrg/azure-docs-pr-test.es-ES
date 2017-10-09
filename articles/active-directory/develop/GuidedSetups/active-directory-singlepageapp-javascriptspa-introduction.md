---
title: "aaaAzure AD v2 JS SPA guiada por el programa de instalación: Introducción | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones SPA de JavaScript a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Hola llamada API de Graph de Microsoft desde una aplicación de página única (SPA) de JavaScript

Esta guía muestra cómo una aplicación de página única (SPA) de JavaScript puede iniciar sesión en el trabajo personal y las cuentas de la escuela, obtener un token de acceso y llamar a Hola API Graph de Microsoft u Hola a otras API que requieren tokens de acceso de punto de conexión de Azure Active Directory v2.

### <a name="how-this-guide-works"></a>Funcionamiento de esta guía

![Cómo funciona la aplicación de ejemplo de Hola generado por esta guía](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Más información

aplicación de ejemplo de Hola creada por esta guía permite un Hola de tooquery SPA JavaScript API Graph de Microsoft o una API Web que acepta los tokens de punto de conexión de Azure Active Directory v2. En este escenario, después de que un usuario inicia sesión, un token de acceso es que las solicitudes de tooHTTP solicitado y agregadas mediante el encabezado de autorización de Hola. Renovación y adquisición de tokens se controlan mediante Hola biblioteca de autenticación de Microsoft (MSAL).

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Bibliotecas

Esta guía usa Hola después de la biblioteca:

|Biblioteca|Descripción|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Biblioteca de autenticación de Microsoft para la vista preliminar de JavaScript|

> [!NOTE]
> *MSAL.js* Hola destinos *punto de conexión de Azure Active Directory v2* -que permite toosign cuentas personales, educativa y profesionales en y adquirir tokens. Hola *punto de conexión de Azure Active Directory v2* tiene [algunas limitaciones](..\active-directory-v2-limitations.md). Si está interesado en cuentas profesionales y educativas, use *adal.js* hello y *V1 extremo*. toounderstand diferencias entre los extremos de v1 y v2 Hola leen hello [v1 y v2 comparación](..\active-directory-v2-compare.md).

<!--end-collapse-->
