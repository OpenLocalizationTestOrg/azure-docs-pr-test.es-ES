---
title: "Configuración del equipo para el desarrollo de Servicios multimedia con .NET"
description: "Conozca los requisitos previos de Servicios multimedia usando el SDK de Servicios multimedia para .NET. Aprenda también a crear una aplicación de Visual Studio."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: 15828bc74937a036871b26493498232ec7cf6f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-development-with-net"></a>Desarrollo de Servicios multimedia con .NET
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

En este tema se explica cómo empezar a desarrollar aplicaciones de Servicios multimedia con .NET.

La **biblioteca del SDK de Azure Media Services para .NET** le permite programar en los Media Services mediante. NET. Para que el desarrollo con .NET sea aún más fácil, se proporciona la biblioteca **Extensiones del SDK de Azure Media Services para .NET**. Esta biblioteca contiene un conjunto de métodos de extensión y funciones auxiliares que simplifican el código de .NET. Las dos bibliotecas están disponibles a través de **NuGet** y **GitHub**.

## <a name="prerequisites"></a>Requisitos previos
* Una cuenta de Servicios multimedia en una suscripción de Azure nueva o existente. Vea el tema [Cómo crear una cuenta de Media Services](media-services-portal-create-account.md).
* Sistemas operativos: Windows 10, Windows 7, Windows 2008 R2 o Windows 8.
* .NET Framework 4.5.
* Visual Studio.

## <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio
En esta sección se muestra cómo crear un proyecto en Visual Studio y configurarlo para el desarrollo de Servicios multimedia.  En este caso, el proyecto es una aplicación de consola Windows de C#, pero los pasos de configuración que se muestran aquí se aplican a otros tipos de proyectos que puede crear para las aplicaciones de Media Services (por ejemplo, una aplicación de Windows Forms o una aplicación web ASP.NET).

En esta sección se muestra cómo usar **NuGet** para agregar las extensiones del SDK de .NET para Media Services y otras bibliotecas dependientes.

También puede obtener los bits más recientes del SDK de Media Services para .NET en GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) o [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), compilar la solución y agregar las referencias al proyecto de cliente. Todas las dependencias necesarias se descargan y extraen automáticamente.

1. Cree una aplicación de consola en C# mediante Visual Studio. Escriba el **Nombre**, la **Ubicación** y el **Nombre de la solución** y, a continuación, haga clic en Aceptar.
2. Compile la solución.
3. Use **NuGet** para instalar y agregar **Extensiones del SDK de .NET para Azure Media Services** (**windowsazure.mediaservices.extensions**). Al instalar este paquete, también se instala el **SDK de Servicios multimedia para .NET** y agrega todas las demás dependencias necesarias.
   
    Asegúrese de que tiene instalada la versión más reciente de NuGet. Para más información e instrucciones de instalación, consulte [NuGet](http://nuget.codeplex.com/).
4. En el Explorador de soluciones, haga clic con el botón derecho en el nombre del proyecto y elija Administrar paquetes NuGet.
   
    Aparecerá el cuadro de diálogo Administrar paquetes de NuGet.
5. En la galería en línea, busque Extensiones de Servicios multimedia de Azure, elija Extensiones del SDK de Servicios multimedia de Azure para .NET y luego haga clic en el botón Instalar.
   
    El proyecto se modifica y se agregan referencias a Extensiones del SDK de Media Services para .NET, al SDK de .NET de Media Services y a otros ensamblados dependientes.
6. Para promover un entorno de desarrollo más limpio, considere la posibilidad de habilitar la restauración de paquetes de NuGet. Para obtener más información, consulte [Restauración de paquetes de NuGet](http://docs.nuget.org/consume/package-restore).
7. Agregue una referencia al ensamblado **System.Configuration** . Este ensamblado contiene la clase de Configuración del sistema.**Administrador de configuración** que se usa para tener acceso a los archivos de configuración (por ejemplo, App.config).
   
    Para agregar referencias usando el cuadro de diálogo de administración de referencias, haga clic con el botón derecho en el nombre del proyecto en el Explorador de soluciones. A continuación, seleccione Agregar y Referencias.
   
    Aparecerá el cuadro de diálogo Administrar referencias.
8. En los ensamblados de .NET Framework, busque, seleccione el ensamblado System.Configuration y haga clic en Aceptar.
9. Abra el archivo App.config y agregue una sección *appSettings* al archivo.     
   
    Establezca los valores que se necesitan para conectarse a la API de Media Services. Para más información, consulte [Acceso a Azure Media Services API con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

    Si usa la [autenticación de usuario](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication), el archivo de configuración probablemente tendrá valores para el dominio del inquilino de Azure AD y el punto de conexión de la API de REST de AMS.
    
    >[!Important]
    >La mayoría de los ejemplos de código que aparecen en el conjunto de documentación de Azure Media Services usan un tipo de autenticación de usuario (interactivo) para conectarse a la API de AMS. Este método de autenticación funcionará bien para administrar o supervisar aplicaciones nativas: aplicaciones móviles, aplicaciones Windows y aplicaciones de consola. Este método de autenticación no es adecuado para los tipos de aplicaciones de servidor, servicios web ni tipo de API.  Para más información, consulte [Acceso a Azure Media Services API con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Sobrescriba las instrucciones **using** existentes siguiendo las instrucciones al comienzo del archivo Program.cs con el siguiente código.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

En este punto, está listo para iniciar el desarrollo de una aplicación de Servicios multimedia.    

## <a name="example"></a>Ejemplo

Este es un pequeño ejemplo en que se establece una conexión a la API de AMS y muestra todos los procesadores de multimedia disponibles.
    
    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a>Pasos siguientes

Ahora [puede conectarse a la API de AMS](media-services-use-aad-auth-to-access-ams-api.md) y empezar a [desarrollar](media-services-dotnet-get-started.md).


## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

