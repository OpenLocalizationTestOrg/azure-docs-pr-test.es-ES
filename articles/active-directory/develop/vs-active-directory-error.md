---
title: "errores de toodiagnose aaaHow con hello Asistente de conexión de Azure Active Directory"
description: "Asistente para la conexión de active directory de Hello detectó un tipo de autenticación incompatible"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a>Diagnóstico de errores con hello Asistente de conexión de Azure Active Directory
Al detectar el anterior código de autenticación, el Asistente de hello detectó un tipo de autenticación incompatible.   

## <a name="what-is-being-checked"></a>¿Qué se está comprobando?
**Nota:** toocorrectly detecta el anterior código de autenticación en un proyecto, se debe compilar el proyecto de Hola.  Si se produjo este error y no tiene un código de autenticación anterior en el proyecto, vuelva a compilarlo e inténtelo de nuevo.

### <a name="project-types"></a>Tipos de proyecto
Asistente de Hello comprueba el tipo de Hola de proyecto que se va a desarrollar por lo que puede insertar lógica de autenticación adecuado de hello en el proyecto de Hola.  Si no hay ningún controlador que se deriva de `ApiController` en el proyecto de hello, proyecto de Hola se considera un proyecto de WebAPI.  Si hay solo los controladores que se derivan de `MVC.Controller` en el proyecto de hello, proyecto de Hola se considera un proyecto de MVC.  Todo lo demás no es compatible con asistente Hola.

### <a name="compatible-authentication-code"></a>Código de autenticación compatible
Asistente Hello también comprueba si la configuración de autenticación que se haya configurado anteriormente con el Asistente de Hola o es compatibles con el Asistente de Hola.  Si todos los valores están presentes, se considera un caso reentrante y abrirá el Asistente Hola Mostrar configuración Hola.  Si solo algunos de los valores de hello están presentes, se considera un caso de error.

En un proyecto MVC, Hola asistente comprueba cualquiera de hello después de la configuración, que genera frente al uso anterior del Asistente para hello:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

Además, Hola asistente comprueba cualquiera de hello después de la configuración en un proyecto de API Web, que genera frente al uso anterior del Asistente para hello:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>Código de autenticación incompatible
Por último, el Asistente de Hola intenta toodetect versiones de código de autenticación que se han configurado con versiones anteriores de Visual Studio. Si recibió este error, significa el proyecto contiene un tipo de autenticación incompatible. Asistente de Hello detecta Hola siguientes tipos de autenticación de las versiones anteriores de Visual Studio:

* Autenticación de Windows 
* Cuentas de usuario individuales 
* Cuentas organizativas 

toodetect autenticación de Windows en un proyecto MVC, el Asistente de hello busca hello `authentication` elemento desde el **web.config** archivo.

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

toodetect autenticación de Windows en un proyecto de API Web, el Asistente de hello busca hello `IISExpressWindowsAuthentication` elemento desde el proyecto **.csproj** archivo:

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

autenticación de cuentas de usuario individuales toodetect, Hola examina para elemento de paquete de Hola desde su **Packages.config** archivo.

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

toodetect un formato antiguo de autenticación de cuenta profesional, Asistente Hola busca Hola siguiente elemento de **web.config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

tipo de autenticación de toochange hello, quitar el tipo de autenticación incompatible de Hola y vuelva a ejecutar el Asistente de Hola.

Para obtener más información, consulte [Escenarios de autenticación en Azure AD](active-directory-authentication-scenarios.md).

#<a name="next-steps"></a>Pasos siguientes
- [Escenarios de autenticación para Azure AD](active-directory-authentication-scenarios.md)