---
title: aaaChanges realizado tooa WebApi proyecto cuando se conecta tooAzure AD | Documentos de Microsoft
description: Describe lo que sucede tooyour WebApi proyecto cuando se conecta tooAzure AD mediante Visual Studio
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a>¿Qué proyecto de WebApi toomy problema (servicio de Visual Studio Azure Active Directory conectado)
> [!div class="op_single_selector"]
> * [Introducción](vs-active-directory-webapi-getting-started.md)
> * [¿Qué ha ocurrido?](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Se han agregado referencias
### <a name="nuget-package-references"></a>Referencias de paquetes de NuGet
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>Referencias de .NET
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>Cambios de código
### <a name="code-files-were-added-tooyour-project"></a>Archivos de código se agregaron tooyour proyecto
Una clase de inicio de autenticación, **App_Start/Startup.Auth.cs** agregó proyecto tooyour que contiene la lógica de inicio para la autenticación de Azure AD.

### <a name="startup-code-was-added-tooyour-project"></a>El código de inicio se agregó tooyour proyecto
Si ya tenía una clase de inicio en el proyecto, Hola **configuración** método era tooinclude actualizado una llamada demasiado`ConfigureAuth(app)`. En caso contrario, se agrega una clase de inicio tooyour proyecto.

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>Su archivo app.config o web.config tiene nuevos valores de configuración.
se han agregado Hola siguiendo las entradas de configuración.

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>Se ha creado una aplicación de Azure AD.
Una aplicación de Azure AD se creó en el directorio de Hola que seleccionó en el Asistente de Hola.

[Más información acerca de Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>¿Si activa *deshabilitar la autenticación de cuentas de usuario individuales*, los cambios adicionales se aplicaron toomy proyecto?
Se han quitado las referencias al paquete NuGet y se han quitado los archivos y se ha realizado una copia de seguridad de los mismos. Según el estado de saludo del proyecto, puede tener toomanually quitar referencias adicionales o archivos, o modificar el código según corresponda.

### <a name="nuget-package-references-removed-for-those-present"></a>Referencias al paquete NuGet quitadas (si existen)
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Se ha realizado una copia de seguridad de los archivos y se han eliminado (si existen)
Cada uno de los siguientes archivos se copia de seguridad y quitará Hola proyecto. Archivos de copia de seguridad se encuentran en una carpeta "Backup" hello raíz del directorio del proyecto de Hola.

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>Copia de seguridad de los archivos de código (si existen)
Se realizó una copia de seguridad de cada uno de los siguientes archivos antes de ser reemplazados. Archivos de copia de seguridad se encuentran en una carpeta "Backup" hello raíz del directorio del proyecto de Hola.

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>¿Si activa *leer datos de directorio*, los cambios adicionales se aplicaron toomy proyecto?
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Se realizaron cambios adicionales tooyour app.config o web.config
Hello entradas de configuración adicionales siguientes se han agregado.

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>Se ha actualizado la aplicación Azure Active Directory
La aplicación de Azure Active Directory estaba actualizada tooinclude hello *leer datos de directorio* permiso y una clave adicional que se creó, a continuación, que se usó como hello *ida: contraseña* en hello `web.config` archivo.

## <a name="next-steps"></a>Pasos siguientes
- [Más información acerca de Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

