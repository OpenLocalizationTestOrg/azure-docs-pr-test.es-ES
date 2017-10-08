---
title: tooa aaaChanges realizados MVC proyecto cuando se conecta tooAzure AD | Documentos de Microsoft
description: Describe lo que sucede tooyour proyecto MVC cuando se conecta tooAzure AD mediante el uso de servicios de Visual Studio conectado
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a>¿Qué proyecto MVC toomy problema (servicio de Visual Studio Azure Active Directory conectado)?
> [!div class="op_single_selector"]
> * [Introducción](vs-active-directory-dotnet-getting-started.md)
> * [¿Qué ha ocurrido?](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Se han agregado referencias
### <a name="nuget-package-references"></a>Referencias de paquetes de NuGet
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel.Tokens.Jwt**

### <a name="net-references"></a>Referencias de .NET
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel**
* **System.IdentityModel.Tokens.Jwt**
* **System.Runtime.Serialization**

## <a name="code-has-been-added"></a>Se ha agregado el código
### <a name="code-files-were-added-tooyour-project"></a>Archivos de código se agregaron tooyour proyecto
Una clase de inicio de autenticación, **App_Start/Startup.Auth.cs** agregó proyecto tooyour que contiene la lógica de inicio para la autenticación de Azure AD. Además, se ha agregado una clase de controlador (Controllers/AccountController.cs) que contiene los métodos **SignIn()** y **SignOut()**. Por último, se ha agregado una vista parcial **Views/Shared/_LoginPartial.cshtml** que contiene un vínculo de acción para SignIn/SignOut.

### <a name="startup-code-was-added-tooyour-project"></a>El código de inicio se agregó tooyour proyecto
Si ya tenía una clase de inicio en el proyecto, Hola **configuración** método era tooinclude actualizado una llamada demasiado**ConfigureAuth(app)**. En caso contrario, se agrega una clase de inicio tooyour proyecto.

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a>Su archivo app.config o web.config tiene nuevos valores de configuración
se han agregado Hola siguiendo las entradas de configuración.

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a>Se ha creado una aplicación de Azure Active Directory (AD)
Una aplicación de Azure AD se creó en el directorio de Hola que seleccionó en el Asistente de Hola.

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>¿Si activa *deshabilitar la autenticación de cuentas de usuario individuales*, los cambios adicionales se aplicaron toomy proyecto?
Se han quitado las referencias al paquete NuGet y se han quitado los archivos y se ha realizado una copia de seguridad de los mismos. Según el estado de saludo del proyecto, puede tener toomanually quitar referencias adicionales o archivos, o modificar el código según corresponda.

### <a name="nuget-package-references-removed-for-those-present"></a>Referencias al paquete NuGet quitadas (si existen)
* **Microsoft.AspNet.Identity.Core**
* **Microsoft.AspNet.Identity.EntityFramework**
* **Microsoft.AspNet.Identity.Owin**

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Se ha realizado una copia de seguridad de los archivos y se han eliminado (si existen)
Cada uno de los siguientes archivos se copia de seguridad y quitará Hola proyecto. Archivos de copia de seguridad se encuentran en una carpeta "Backup" hello raíz del directorio del proyecto de Hola.

* **App_Start\IdentityConfig.cs**
* **Controllers\ManageController.cs**
* **Models\IdentityModels.cs**
* **Models\ManageViewModels.cs**

### <a name="code-files-backed-up-for-those-present"></a>Copia de seguridad de los archivos de código (si existen)
Se realizó una copia de seguridad de cada uno de los siguientes archivos antes de ser reemplazados. Archivos de copia de seguridad se encuentran en una carpeta "Backup" hello raíz del directorio del proyecto de Hola.

* **Startup.cs**
* **App_Start\Startup.Auth.cs**
* **Controllers\AccountController.cs**
* **Views\Shared\_LoginPartial.cshtml**

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>¿Si activa *leer datos de directorio*, los cambios adicionales se aplicaron toomy proyecto?
Se han agregado referencias adicionales.

### <a name="additional-nuget-package-references"></a>Referencias de paquetes de NuGet adicionales
* **EntityFramework**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **System.Spatial**

### <a name="additional-net-references"></a>Referencias de .NET adicionales
* **EntityFramework**
* **EntityFramework.SqlServer**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**
* **System.Spatial**

### <a name="additional-code-files-were-added-tooyour-project"></a>Archivos de código adicionales se agregaron tooyour proyecto
Se agregan dos archivos toosupport símbolo (token) de almacenamiento en caché: **Models\ADALTokenCache.cs** y **Models\ApplicationDbContext.cs**.  Un controlador adicional y la vista se agregaron tooillustrate acceso a la información de perfil de usuario mediante las API de Azure graph.  Estos archivos son **Controllers\UserProfileController.cs** y **Views\UserProfile\Index.cshtml**.

### <a name="additional-startup-code-was-added-tooyour-project"></a>El código de inicio adicional se agregó tooyour proyecto
Hola **startup.auth.cs** de archivos, un nuevo **OpenIdConnectAuthenticationNotifications** se agregó el objeto toohello **notificaciones** miembro de hello  **OpenIdConnectAuthenticationOptions**.  Se trata de tooenable recibir hello OAuth código e intercambian para un token de acceso.

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Se realizaron cambios adicionales tooyour app.config o web.config
Hello entradas de configuración adicionales siguientes se han agregado.

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

Hello secciones de configuración siguientes y cadena de conexión se ha agregado.

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a>Se ha actualizado la aplicación Azure Active Directory
La aplicación de Azure Active Directory estaba actualizada tooinclude hello *leer datos de directorio* permiso y una clave adicional que se creó, a continuación, que se usó como hello *ida: ClientSecret* en hello  **Web.config** archivo.

## <a name="next-steps"></a>Pasos siguientes
- [Más información acerca de Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

