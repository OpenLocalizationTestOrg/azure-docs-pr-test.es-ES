---
title: aaaConnecting tooMedia Services cuenta con .NET
description: "Este tema se muestra cómo usar servicios de tooMedia tooconnect. NET."
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a23bd285f7cae17ae5831e1e50e73947afbb9a3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a>Conexión tooMedia cuenta de servicios mediante el SDK de servicios multimedia para .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

Este tema describe cómo tooobtain una tooMicrosoft de conexión mediante programación los servicios de multimedia de Azure cuando se programa con Hola SDK de servicios multimedia para. NET.

## <a name="connecting-toomedia-services"></a>Conectar servicios tooMedia
tooconnect tooMedia servicios mediante programación, debe haber configurado previamente una cuenta de Azure, configura los servicios multimedia en dicha cuenta y, a continuación, establecer un proyecto de Visual Studio para el desarrollo con hello SDK de servicios multimedia para .NET. Para obtener más información, consulte el programa de instalación para el desarrollo con hello SDK de servicios multimedia para. NET.

Al final de hello del proceso de instalación de cuenta de servicios multimedia de hello, obtuvo siguiente Hola necesarios los valores de conexión. Use estas conexiones mediante programación toomake tooMedia servicios.

* Nombre de la cuenta de Servicios multimedia.
* Clave de la cuenta de Servicios multimedia.

toofind estos valores, vaya toohello Portal de administración de Azure, seleccione la cuenta de servicios multimedia y haga clic en hello "**administrar claves**" icono en parte inferior de Hola de ventana del portal Hola. Al hacer clic en hello icono siguiente tooeach texto cuadro copias Hola valor toohello Portapapeles del sistema.

## <a name="creating-a-cloudmediacontext-instance"></a>Creación de una instancia de CloudMediaContext
programar basándose en los medios de servicios que usted necesita toocreate de toostart un **CloudMediaContext** instancia que representa el contexto de servidor hello. Hola **CloudMediaContext** incluye referencias tooimportant colecciones incluidos trabajos, activos, archivos, las directivas de acceso y localizadores.

> [!NOTE]
> Hola **CloudMediaContext** clase no es segura para subprocesos. Debe crear un nuevo elemento CloudMediaContext por subproceso o por conjunto de operaciones.
> 
> 

CloudMediaContext tiene cinco sobrecargas de constructor. Es toouse recomendada constructores que toman **MediaServicesCredentials** como un parámetro. Para obtener más información, vea hello **reutilizar Tokens de servicio de Control de acceso** que sigue. 

Hello en el ejemplo siguiente se usa Hola pública CloudMediaContext(MediaServicesCredentials credentials) constructor:

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>Reutilización de los tokens del Servicio de control de acceso
Esta sección muestra cómo los tokens tooreuse Access Control Service mediante el uso de CloudMediaContext constructores que toman MediaServicesCredentials como un parámetro.

[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (también conocido como Access Control Service o ACS) es un servicio basado en la nube que proporciona una manera sencilla de autenticación y autorización a usuarios toogain de acceso tootheir las aplicaciones web. Servicios de multimedia de Microsoft Azure controla el acceso tooits servicios aunque protocolo OAuth que requiere un token de ACS. Servicios multimedia recibe los tokens de ACS de Hola de un servidor de autorización.

Al desarrollar con hello SDK de servicios multimedia, puede elegir solucionan toonot tokens Hola porque Hola administradores de código SDK usarlas para usted. Sin embargo, lo que permitirá Hola SDK administrar totalmente Hola ACS tokens clientes potenciales toounnecessary las solicitudes de token. Solicitar tokens lleva tiempo y consume recursos de servidor y cliente de Hola. Además, servidor de ACS de hello limita las solicitudes de hello si Hola velocidad es demasiado alta. límite de Hello es de 30 solicitudes por segundo, consulte [limitaciones del servicio ACS](https://msdn.microsoft.com/library/gg185909.aspx) para obtener más detalles.

A partir de hello SDK de servicios multimedia versión 3.0.0.0, puede volver a usar tokens de ACS de Hola. Hola **CloudMediaContext** constructores que toman **MediaServicesCredentials** como un parámetro de habilitar uso compartido tokens Hola ACS entre varios contextos. Hola MediaServicesCredentials clase encapsula las credenciales de servicios multimedia de Hola. Si un token de ACS está disponible y se conoce la fecha de expiración, puede crear una nueva instancia de MediaServicesCredentials con token de Hola y páselo constructor toohello de CloudMediaContext. Tenga en cuenta que Hola SDK de servicios multimedia actualiza automáticamente los tokens cada vez que expiran. Hay dos maneras de tokens de ACS tooreuse, tal y como se muestra en los ejemplos de hello siguientes.

* Puede almacenar en caché hello **MediaServicesCredentials** objeto en memoria (por ejemplo, en una variable de clase estática). A continuación, pase el constructor de hello en caché objetos toohello CloudMediaContext. objeto de Hello MediaServicesCredentials contiene un token de ACS que se puede reutilizar si sigue siendo válido. Si el token de hello no es válido, se actualizarán por hello SDK de servicios multimedia con credenciales de hello tiene toohello MediaServicesCredentials constructor.
  
    Tenga en cuenta que hello **MediaServicesCredentials** objeto obtiene un token válido después de hello RefreshToken se llama. Hola **CloudMediaContext** Hola llamadas **RefreshToken** método hello constructor. Si tiene previsto almacenamiento externo de toosave Hola valores de token tooan, tome toocheck seguro si hello TokenExpiration valor es válido antes de guardar los datos de token de Hola. Si no es válido, llame a RefreshToken antes del almacenamiento en caché.
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* También puede almacenar en caché hello AccessToken valores de cadena y hello TokenExpiration. valores de Hello más tarde podrían ser usada toocreate un MediaServicesCredentials nuevo objeto con datos de token de hello en caché.  Esto es especialmente útil para escenarios donde el token de hello puede compartirse de forma segura entre varios procesos o equipos.
  
    Hello siguientes fragmentos de código llaman Hola métodos SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage y UpdateTokenDataInExternalStorageIfNeeded que no estén definidos en este ejemplo. Puede definir estos métodos toostore y recuperar datos de token de actualización en un almacenamiento externo. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    Usar hello guarda los valores de token toocreate MediaServicesCredentials.

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    Actualizar copia del token de hello en caso de que el token de hello actualizó Hola SDK de servicios multimedia. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Si tiene varias cuentas de servicios multimedia (por ejemplo, para uso compartido con fines o la distribución geográfica de cargas) puede almacenar en caché objetos MediaServicesCredentials utilizando hello System.Collections.Concurrent.ConcurrentDictionary colección (Hola Colección de ConcurrentDictionary representa una colección segura para subprocesos de pares clave/valor que pueden acceder varios subprocesos simultáneamente). A continuación, puede usar Hola GetOrAdd método tooget hello en caché credenciales. 
  
        // Declare a static class variable of hello ConcurrentDictionary type in which hello Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials toocreate a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a>Conexión de cuenta de servicios multimedia de tooa ubicado en la región del Norte de China Hola
Si su cuenta se encuentra en la región del Norte de China hello, utilice Hola después de constructor:

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

Por ejemplo:

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>Almacenar valores de conexión en la configuración
Es un valores de conexión de toostore altamente recomendado, especialmente los valores confidenciales como el nombre de cuenta y contraseña, en la configuración. Además, es una práctica recomendada tooencrypt confidenciales de la configuración de datos. Puede cifrar archivo de configuración completo de hello mediante el uso de sistema de archivos de cifrado (EFS) de hello Windows. Seleccione tooenable EFS en un archivo, contextual hello, **propiedades**y habilitar el cifrado en hello **avanzadas** pestaña Configuración. O bien, puede crear una solución personalizada para cifrar las partes seleccionadas de un archivo de configuración mediante la configuración protegida. Consulte [Cifrar información de configuración mediante una configuración protegida](https://msdn.microsoft.com/library/53tyfkaw.aspx).

Hola siguiente archivo App.config contiene valores de conexión de hello necesario. Hola valores de hello <appSettings> elemento son valores de hello necesario que obtuvo en el proceso de configuración de cuenta de servicios multimedia de Hola.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


tooretrieve los valores de conexión de configuración, puede usar hello **ConfigurationManager** clase y, a continuación, asignar toofields de valores de hello en el código:

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

