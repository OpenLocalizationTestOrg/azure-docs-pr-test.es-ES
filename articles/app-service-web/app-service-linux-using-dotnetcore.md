---
title: "aaaUse .NET Core en la aplicación Web en Linux | Documentos de Microsoft"
description: Use .NET Core en Web App en Linux.
keywords: "azure app service, aplic. web, dotnet, núcleo, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>Uso de .NET Core en una instancia de Azure Web App en Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Aplicación Web](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) en Linux proporciona un servicio de hospedaje web muy escalables y aplicación de revisiones automáticamente con el sistema operativo de Linux de Hola. Este tutorial contiene instrucciones paso a paso que muestra cómo toocreate una [.NET Core](https://docs.microsoft.com/aspnet/core/) aplicación en la aplicación web de Azure en Linux. 

![Aplicación web en Linux][10]

Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux.

## <a name="prerequisites"></a>Requisitos previos ##

toocomplete este tutorial: 

* Instalar hello [.NET Core SDK](https://www.microsoft.com/net/download/core).
* Instale [Git](https://git-scm.com/downloads).

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>Creación de una aplicación .NET Core local ##

Inicie una nueva sesión de terminal. Cree un directorio denominado `hellodotnetcore`y cambiar hello tooit de directorio actual. A continuación, escriba lo siguiente hello: 

```
dotnet new web
``` 

  Este comando crea tres archivos (*hellodotnetcore.csproj*, *Program.cs*, y *Startup.cs*) y una carpeta vacía (*wwwroot /*) en el directorio actual de Hola. contenido de Hello `.csproj` archivo debe ser similar al siguiente hello: 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

Puesto que esta aplicación es una aplicación web, un tooan referencia paquete ASP.NET Core automáticamente fue agregado toohello *hellodotnetcore.csproj* archivo. número de versión de Hola de paquetes de saludo se establece según toohello elegido framework. Este ejemplo hace referencia a ASP.NET Core versión 1.1.2 porque se usa .NET Core 1.1.

## <a name="build-and-test-hello-application-locally"></a>Compilar y probar la aplicación hello localmente ##

Puede compilar y ejecutar la aplicación de .NET Core con hello `dotnet restore` comando seguido por hello `dotnet run` de comandos, como se muestra aquí:

```
dotnet restore
dotnet run
```


Cuando se inicia la aplicación hello, muestra un mensaje que indica la aplicación hello escucha las solicitudes de tooincoming en un puerto. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

Probar examinando demasiado`http://localhost:5000/` con el explorador. Si todo funciona correctamente, verá "Hello World!" (¡Hola mundo!) como texto de resultado de hello.

![Prueba con un explorador][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a>Crear una aplicación de .NET Core en hello Portal de Azure ##

En primer lugar debe toocreate una aplicación web vacía. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) y crear un nuevo [aplicación Web en Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).

![Creación de una aplicación web][1]

Cuando Hola **crear** se abre la página, proporcione detalles acerca de la aplicación web:

![Elección de una pila de tiempo de ejecución .NET Core][2]

Use Hola siguiente tabla se como un toofill guía out hello **crear** página, a continuación, seleccione **Aceptar** y **crear** toocreate Hola aplicación.

| Configuración      | Valor sugerido  | Descripción                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| Nombre de la aplicación | hellodotnetcore  | nombre de saludo de la aplicación. Este nombre debe ser único. |
| La suscripción | Elección de una suscripción actual | Hola suscripción de Azure. |
| Grupo de recursos | myResourceGroup |  Hola recursos de Azure grupo toocontain hello web app. |
| Plan de servicio de aplicación | Nombre del plan de App Service existente |  Hola plan de servicio de aplicaciones.  |
| Configuración del contenedor | .NET Core 1.1 | tipo de contenedor de esta aplicación web de Hola: registro integrado, Docker o Private. |
| Origen de la imagen  | Característica integrada  |  origen de Hola de imagen de Hola. |
| Pila de tiempo de ejecución  | .NET Core 1.1  | pila de tiempo de ejecución de Hola y versión.  |

## <a name="deploy-your-application-via-git"></a>Implementación de la aplicación a través de Git ##

Usar Git toodeploy Hola .NET Core aplicación tooAzure aplicación Web de servicio de aplicaciones en Linux.

aplicación web de Azure nuevo de Hello ya tiene configurado de implementación de Git. Encontrará dirección URL de implementación de Git Hola desplazándose toohello siguiendo la dirección URL después de insertar el nombre de la aplicación web:

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

Hola dirección URL de Git tiene Hola siguiente formulario basado en el nombre de la aplicación web:

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Ejecute hello después de la aplicación de comandos toodeploy hello aplicación local tooyour web de Azure: 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

No es necesario toopush los archivos en *bin /* o *obj /* directorios dado que la aplicación se basa en la nube de Hola Hola cuando la aplicación los archivos de origen se insertan tooAzure. Una vez completado el proceso de compilación de hello, archivos binarios se copian en el directorio de la aplicación hello en */principal/sitio/wwwroot/*.

Confirme que las operaciones de implementación remota de hello informan correcto. Las operaciones de inserción pueden tardar bastante tiempo desde la resolución de paquete y en la nube Hola de proceso de compilación. Verá varios mensajes de estado, y algunos indican que se han copiado los archivos. salida de Hello debería ser similar siguiente toohello:

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Cuando haya completado la implementación de hello, reinicie la aplicación web con efecto de hello implementación tootake. toodo, vaya toohello portal de Azure y navegue toohello **Introducción** página de la aplicación web. Seleccione hello **reiniciar** botón en la página de Hola. Cuando aparezca una ventana emergente, seleccione **Sí** tooconfirm. A continuación, puede examinar la aplicación web, como se muestra aquí:

![Exploración .NET Core implementado tooAzure servicio de aplicaciones en Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Pasos siguientes
* [Preguntas más frecuentes sobre Web App on Linux de Azure App Service](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
