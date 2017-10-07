---
title: aaaHow tooSet equipo para el desarrollo de servicios multimedia con .NET
description: "Obtenga información sobre los requisitos previos de Hola para servicios multimedia con hello SDK de servicios multimedia para. NET. También aprenderá cómo toocreate una aplicación de Visual Studio."
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
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a>Desarrollo de Servicios multimedia con .NET
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Este tema describe cómo de servicios multimedia de desarrollo de toostart aplicaciones con. NET.

Hola **Azure Media Services .NET SDK** biblioteca le permite tooprogram en servicios multimedia con. NET. toomake incluso más fácil toodevelop con. NET, hello **Azure Media Services .NET SDK Extensions** se proporciona la biblioteca. Esta biblioteca contiene un conjunto de métodos de extensión y funciones auxiliares que simplifican el código de .NET. Las dos bibliotecas están disponibles a través de **NuGet** y **GitHub**.

## <a name="prerequisites"></a>Requisitos previos
* Una cuenta de Servicios multimedia en una suscripción de Azure nueva o existente. Vea el tema de hello [cómo tooCreate una cuenta de servicios multimedia](media-services-portal-create-account.md).
* Sistemas operativos: Windows 10, Windows 7, Windows 2008 R2 o Windows 8.
* .NET Framework 4.5.
* Visual Studio.

## <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio
Esta sección muestra cómo toocreate un proyecto en Visual Studio y configurarla para el desarrollo de servicios multimedia.  En este caso, proyecto de hello es una aplicación de consola de Windows en C#, pero hello mismos pasos de configuración se muestra aquí aplican tooother tipos de proyectos que puede crear para las aplicaciones de servicios multimedia (por ejemplo, una aplicación de formularios Windows Forms o una aplicación Web ASP.NET).

Esta sección se muestra cómo toouse **NuGet** tooadd Media Services .NET SDK extensions y otras bibliotecas dependientes.

Como alternativa, puede obtener los bits más recientes de SDK de .NET de servicios multimedia de Hola desde GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) o [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), compilar soluciones de Hola y Agregar proyecto de cliente de hello referencias toohello. Todas las dependencias necesarias de hello obtengan descargadas y extraídas automáticamente.

1. Cree una aplicación de consola en C# mediante Visual Studio. Escriba hello **nombre**, **ubicación**, y **nombre de la solución**y, a continuación, haga clic en Aceptar.
2. Compile la solución de Hola.
3. Use **NuGet** tooinstall y agregue **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**). Al instalar este paquete, también se instala el **SDK de Servicios multimedia para .NET** y agrega todas las demás dependencias necesarias.
   
    Asegúrese de que tiene la versión más reciente de Hola de NuGet instalada. Para más información e instrucciones de instalación, consulte [NuGet](http://nuget.codeplex.com/).
4. En el Explorador de soluciones, haga clic en nombre de hello del proyecto de Hola y elija Administrar paquetes NuGet.
   
    aparece el cuadro de diálogo Administrar paquetes de NuGet Hola.
5. En la galería en línea de hello, busque las extensiones de MediaServices de Azure, elija Azure Media Services .NET SDK Extensions y, a continuación, haga clic en botón de instalar Hola.
   
    proyecto de Hola se modifica y hace referencia a toohello Media Services .NET SDK Extensions, Media Services .NET SDK, y se agregan otros ensamblados dependientes.
6. toopromote un entorno de desarrollo más limpio, considere la posibilidad de habilitar la restauración de paquetes de NuGet. Para obtener más información, consulte [Restauración de paquetes de NuGet](http://docs.nuget.org/consume/package-restore).
7. Agregue una referencia demasiado**System.Configuration** ensamblado. Este ensamblado contiene Hola System.Configuration. **ConfigurationManager** clase que es tooaccess usa archivos de configuración (por ejemplo, App.config).
   
    referencias de tooadd mediante el cuadro de diálogo de administrar referencias de hello, haga clic en el nombre del proyecto hello en el Explorador de soluciones de Hola. A continuación, seleccione Agregar y Referencias.
   
    aparece el cuadro de diálogo de administrar referencias de Hola.
8. En los ensamblados de .NET framework, buscar y seleccionar ensamblado System.Configuration de Hola y haga clic en Aceptar.
9. Abra el archivo App.config de hello y agregue un *appSettings* archivo toohello de sección.     
   
    Establecer valores de hello que son necesarios tooconnect toohello API de servicios multimedia. Para obtener más información, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

    Si utilizas [autenticación de usuario](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) el archivo de configuración tendrá probablemente valores para el dominio del inquilino de Azure AD y Hola extremo de la API de REST de AMS.
    
    >[!Important]
    >La mayoría de ejemplos de código de hello documentación de servicios multimedia de Azure establecido, utilice un tipo de autenticación tooconnect toohello AMS API (interactiva) de usuario. Este método de autenticación funcionará bien para administrar o supervisar aplicaciones nativas: aplicaciones móviles, aplicaciones Windows y aplicaciones de consola. Este método de autenticación no es adecuado para los tipos de aplicaciones de servidor, servicios web ni tipo de API.  Para obtener más información, consulte [Hola AMS API de acceso con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Sobrescribir Hola existente **con** al principio de hello las instrucciones del archivo Program.cs de hello con hello siguiente código.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

En este punto, está listo toostart desarrollar una aplicación de servicios multimedia.    

## <a name="example"></a>Ejemplo

Este es un pequeño ejemplo que se conecta toohello AMS API y enumera todos los procesadores de medios disponibles.
    
    class Program
    {
        // Read values from hello App.config file.
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

Ahora [puede conectarse toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) e iniciar [desarrollar](media-services-dotnet-get-started.md).


## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

