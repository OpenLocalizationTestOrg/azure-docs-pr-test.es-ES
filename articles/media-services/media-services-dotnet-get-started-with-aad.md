---
title: "aaaUse tooaccess de autenticación de Azure AD API de servicios multimedia de Azure con .NET | Documentos de Microsoft"
description: "Este tema muestra cómo toouse tooaccess de autenticación de Azure Active Directory (Azure AD) servicios multimedia de Azure (AMS) API con. NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a>Utilizar autenticación de Azure AD tooaccess API de servicios multimedia de Azure con .NET

A partir de windowsazure.mediaservices 4.0.0.4, Azure Media Services admite la autenticación basada en Azure Active Directory (Azure AD). Este tema muestra cómo toouse tooaccess de autenticación de Azure AD API de servicios multimedia de Azure con Microsoft. NET.

## <a name="prerequisites"></a>Requisitos previos

- Una cuenta de Azure. Para más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Una cuenta de Media Services. Para obtener más información, consulte [crear una cuenta de servicios multimedia de Azure mediante el portal de Azure de hello](media-services-portal-create-account.md).
- Hola más reciente [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) paquete.
- Está familiarizado con el tema de hello [obtiene acceso a la API de los servicios de multimedia de Azure con información general de autenticación de AAD](media-services-use-aad-auth-to-access-ams-api.md). 

Si usa la autenticación de Azure AD con Azure Media Services, puede autenticarse de alguna de estas dos formas:

- **Autenticación de usuario** autentica una persona que usa Hola aplicación toointeract con recursos de servicios multimedia de Azure. aplicación interactiva de Hello en primer lugar debe solicitarle las credenciales de usuario Hola. Un ejemplo es una aplicación de consola de administración que se utiliza por toomonitor de usuarios autorizados trabajos de codificación o streaming en vivo. 
- **Autenticación de entidad de servicio** autentica un servicio. Las aplicaciones que normalmente utilizan este método de autenticación son aplicaciones que ejecutan servicios de demonio, servicios de nivel intermedio o trabajos programados, como Web Apps, Function Apps, Logic Apps, API o microservicios.

>[!IMPORTANT]
>Azure Media Services actualmente admite un modelo de autenticación de Azure Access Control Service. Sin embargo, la autorización de Control de acceso va toobe en desuso en 1 de junio de 2018. Se recomienda que migre modelo de autenticación de Azure Active Directory tooan tan pronto como sea posible.

## <a name="get-an-azure-ad-access-token"></a>Obtención de un token de acceso de Azure AD

tooconnect toohello API de servicios multimedia de Azure con autenticación de Azure AD, la aplicación de cliente de hello debe toorequest un token de acceso de Azure AD. Cuando usas SDK, muchos de los detalles de hello acerca de cómo se ajusta y simplificado para usted en hello tooacquire un token de acceso de Azure AD del cliente de .NET de los servicios multimedia de hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) y [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) clases. 

Por ejemplo, no es necesario tooprovide autoridad de hello Azure AD, URI de recurso de servicios multimedia o nativo detalles de la aplicación de Azure AD. Se trata de valores conocidos que ya están configurados de hello clase de proveedor de tokens de acceso de Azure AD. 

Si no utiliza el SDK de .NET de servicios multimedia de Azure, recomendamos que use hello [biblioteca de autenticación de Azure AD](../active-directory/develop/active-directory-authentication-libraries.md). tooget valores para parámetros de Hola que necesita toouse con la biblioteca de autenticación de Azure AD, consulte [usar la configuración de autenticación de Azure tooaccess portal Azure AD hello](media-services-portal-get-started-with-aad.md).

También tiene Hola opción de sustitución de la implementación predeterminada de Hola de hello **AzureAdTokenProvider** con su propia implementación.

## <a name="install-and-configure-azure-media-services-net-sdk"></a>Instalación y configuración del SDK de Azure Media Services para .NET

>[!NOTE] 
>autenticación de toouse Azure AD con hello Media Services .NET SDK, deberá toohave hello más reciente [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) paquete. Además, agregue una referencia toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** ensamblado. Si utilizas una aplicación existente, incluir hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** ensamblado. 

1. Cree una aplicación de consola en C# mediante Visual Studio.
2. Hola de uso [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall de paquete de NuGet **Azure Media Services .NET SDK**. 

    tooadd referencias usando NuGet, tomar Hola pasos: en **el Explorador de soluciones**, haga clic en el nombre del proyecto de hello y, a continuación, seleccione **administrar paquetes NuGet**. Después, busque **windowsazure.mediaservices** y seleccione **Instalar**.
    
    O bien

    Ejecución hello después del comando en **Package Manager Console** en Visual Studio.

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. Agregar **con** tooyour código de origen.

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a>Uso de la autenticación de usuario

tooconnect toohello API de servicios multimedia de Azure con la opción de autenticación de usuario de hello, aplicación de cliente de hello necesita toorequest Hola de un token de Azure AD mediante el uso de parámetros siguientes:  

- Punto de conexión de inquilino de Azure AD. puede recuperar la información de inquilino de Hola de hello portal de Azure. Mantenga el mouse sobre Hola usuario con sesión iniciada en la esquina superior derecha de Hola.
- URI del recurso de Media Services.
- Id. de cliente de aplicación de Media Services (nativo) 
- URI de redireccionamiento de aplicación de Media Services (nativo). 

valores de Hello para estos parámetros se pueden encontrar en **AzureEnvironments.AzureCloudEnvironment**. Hola **AzureEnvironments.AzureCloudEnvironment** constante es una aplicación auxiliar de hello .NET SDK tooget valores de variable de entorno derecho de Hola para un centro de datos de Azure pública. 

Contiene valores de configuración de entorno predefinidos para tener acceso a servicios multimedia en centros de datos públicos de hello solo. Para regiones con entornos de nube de administración pública o soberana, puede usar **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** o **AzureGermanCloudEnvironment**, respectivamente.

Hola, ejemplo de código siguiente crea un token:
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
toostart programar con servicios multimedia, necesita toocreate una **CloudMediaContext** instancia que representa el contexto de servidor hello. Hola **CloudMediaContext** incluye referencias tooimportant colecciones incluidos trabajos, activos, archivos, las directivas de acceso y localizadores. 

También necesita hello toopass **recurso URI para los servicios de REST de multimedia** toohello **CloudMediaContext** constructor. URI del recurso de hello tooget para servicios multimedia de REST, inicio de sesión toohello portal de Azure, seleccione la cuenta de servicios multimedia de Azure, seleccione **el acceso de API**y, a continuación, seleccione **conectar servicios de multimedia de tooAzure con usuario autenticación**. 

Hello ejemplo de código siguiente se crea un **CloudMediaContext** instancia:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

Hola de ejemplo siguiente muestra cómo toocreate Hola contexto hello y símbolo (token) de Azure AD:

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
>Si se produce una excepción que indicara "servidor remoto hello devolvió un error: (401) no autorizado," vea hello [el control de acceso](media-services-use-aad-auth-to-access-ams-api.md#access-control) sección de obtener acceso a la API de los servicios de multimedia de Azure con información general de autenticación de Azure AD.

## <a name="use-service-principal-authentication"></a>Uso de la autenticación de entidad de servicio
    
tooconnect toohello API de servicios multimedia de Azure con la opción de entidad de seguridad de servicio de hello, necesita la aplicación de nivel intermedio (API de web o aplicación web) toorequests un token de Azure AD con hello parámetros siguientes:  

- Punto de conexión de inquilino de Azure AD. puede recuperar la información de inquilino de Hola de hello portal de Azure. Mantenga el mouse sobre Hola usuario con sesión iniciada en la esquina superior derecha de Hola.
- URI del recurso de Media Services.
- Los valores de aplicación de Azure AD: Hola **Id. de cliente** y **secreto de cliente**.

Hola valores de hello **Id. de cliente** y **secreto de cliente** parámetros pueden encontrarse en hello portal de Azure. Para obtener más información, consulte [Introducción a Azure AD mediante autenticación Hola portal de Azure](media-services-portal-get-started-with-aad.md).

Hello ejemplo de código siguiente crea un token mediante hello **AzureAdTokenCredentials** constructor que toma **AzureAdClientSymmetricKey** como parámetro: 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

También puede especificar hello **AzureAdTokenCredentials** constructor que toma **AzureAdClientCertificate** como un parámetro. 

Para obtener instrucciones acerca de cómo toocreate y configurar un certificado en un formulario que puede usarse con Azure AD, consulte [tooAzure AD en aplicaciones de demonio con certificados: pasos de configuración manual de autenticación](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

toostart programar con servicios multimedia, necesita toocreate una **CloudMediaContext** instancia que representa el contexto de servidor hello. También necesita hello toopass **recurso URI para los servicios de REST de multimedia** toohello **CloudMediaContext** constructor. Puede obtener hello **recurso URI para los servicios de REST de multimedia** valor de hello portal de Azure.

Hello ejemplo de código siguiente se crea un **CloudMediaContext** instancia:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
Hola de ejemplo siguiente muestra cómo toocreate Hola contexto hello y símbolo (token) de Azure AD:

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a>Pasos siguientes

Empezar a trabajar con [cargar archivos tooyour cuenta](media-services-dotnet-upload-files.md).
