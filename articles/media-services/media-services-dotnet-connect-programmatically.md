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
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="49079-103">Conexión tooMedia cuenta de servicios mediante el SDK de servicios multimedia para .NET</span><span class="sxs-lookup"><span data-stu-id="49079-103">Connecting tooMedia Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49079-104">REST</span><span class="sxs-lookup"><span data-stu-id="49079-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="49079-105">.NET</span><span class="sxs-lookup"><span data-stu-id="49079-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="49079-106">Este tema describe cómo tooobtain una tooMicrosoft de conexión mediante programación los servicios de multimedia de Azure cuando se programa con Hola SDK de servicios multimedia para. NET.</span><span class="sxs-lookup"><span data-stu-id="49079-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services SDK for .NET.</span></span>

## <a name="connecting-toomedia-services"></a><span data-ttu-id="49079-107">Conectar servicios tooMedia</span><span class="sxs-lookup"><span data-stu-id="49079-107">Connecting tooMedia Services</span></span>
<span data-ttu-id="49079-108">tooconnect tooMedia servicios mediante programación, debe haber configurado previamente una cuenta de Azure, configura los servicios multimedia en dicha cuenta y, a continuación, establecer un proyecto de Visual Studio para el desarrollo con hello SDK de servicios multimedia para .NET.</span><span class="sxs-lookup"><span data-stu-id="49079-108">tooconnect tooMedia Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with hello Media Services SDK for .NET.</span></span> <span data-ttu-id="49079-109">Para obtener más información, consulte el programa de instalación para el desarrollo con hello SDK de servicios multimedia para. NET.</span><span class="sxs-lookup"><span data-stu-id="49079-109">For more information, see Setup for Development with hello Media Services SDK for .NET.</span></span>

<span data-ttu-id="49079-110">Al final de hello del proceso de instalación de cuenta de servicios multimedia de hello, obtuvo siguiente Hola necesarios los valores de conexión.</span><span class="sxs-lookup"><span data-stu-id="49079-110">At hello end of hello Media Services account setup process, you obtained hello following required connection values.</span></span> <span data-ttu-id="49079-111">Use estas conexiones mediante programación toomake tooMedia servicios.</span><span class="sxs-lookup"><span data-stu-id="49079-111">Use these toomake programmatic connections tooMedia Services.</span></span>

* <span data-ttu-id="49079-112">Nombre de la cuenta de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="49079-112">Your Media Services account name.</span></span>
* <span data-ttu-id="49079-113">Clave de la cuenta de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="49079-113">Your Media Services account key.</span></span>

<span data-ttu-id="49079-114">toofind estos valores, vaya toohello Portal de administración de Azure, seleccione la cuenta de servicios multimedia y haga clic en hello "**administrar claves**" icono en parte inferior de Hola de ventana del portal Hola.</span><span class="sxs-lookup"><span data-stu-id="49079-114">toofind these values, go toohello Azure Managment Portal, select your Media Service account, and click on hello “**MANAGE KEYS**” icon on hello bottom of hello portal window.</span></span> <span data-ttu-id="49079-115">Al hacer clic en hello icono siguiente tooeach texto cuadro copias Hola valor toohello Portapapeles del sistema.</span><span class="sxs-lookup"><span data-stu-id="49079-115">Clicking on hello icon next tooeach text box copies hello value toohello system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="49079-116">Creación de una instancia de CloudMediaContext</span><span class="sxs-lookup"><span data-stu-id="49079-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="49079-117">programar basándose en los medios de servicios que usted necesita toocreate de toostart un **CloudMediaContext** instancia que representa el contexto de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="49079-117">toostart programming against Media Services you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="49079-118">Hola **CloudMediaContext** incluye referencias tooimportant colecciones incluidos trabajos, activos, archivos, las directivas de acceso y localizadores.</span><span class="sxs-lookup"><span data-stu-id="49079-118">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="49079-119">Hola **CloudMediaContext** clase no es segura para subprocesos.</span><span class="sxs-lookup"><span data-stu-id="49079-119">hello **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="49079-120">Debe crear un nuevo elemento CloudMediaContext por subproceso o por conjunto de operaciones.</span><span class="sxs-lookup"><span data-stu-id="49079-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="49079-121">CloudMediaContext tiene cinco sobrecargas de constructor.</span><span class="sxs-lookup"><span data-stu-id="49079-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="49079-122">Es toouse recomendada constructores que toman **MediaServicesCredentials** como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="49079-122">It is recommended toouse constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="49079-123">Para obtener más información, vea hello **reutilizar Tokens de servicio de Control de acceso** que sigue.</span><span class="sxs-lookup"><span data-stu-id="49079-123">For more information, see hello **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="49079-124">Hello en el ejemplo siguiente se usa Hola pública CloudMediaContext(MediaServicesCredentials credentials) constructor:</span><span class="sxs-lookup"><span data-stu-id="49079-124">hello following example uses hello public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="49079-125">Reutilización de los tokens del Servicio de control de acceso</span><span class="sxs-lookup"><span data-stu-id="49079-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="49079-126">Esta sección muestra cómo los tokens tooreuse Access Control Service mediante el uso de CloudMediaContext constructores que toman MediaServicesCredentials como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="49079-126">This section shows how tooreuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="49079-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (también conocido como Access Control Service o ACS) es un servicio basado en la nube que proporciona una manera sencilla de autenticación y autorización a usuarios toogain de acceso tootheir las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="49079-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users toogain access tootheir web applications.</span></span> <span data-ttu-id="49079-128">Servicios de multimedia de Microsoft Azure controla el acceso tooits servicios aunque protocolo OAuth que requiere un token de ACS.</span><span class="sxs-lookup"><span data-stu-id="49079-128">Microsoft Azure Media Services controls access tooits services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="49079-129">Servicios multimedia recibe los tokens de ACS de Hola de un servidor de autorización.</span><span class="sxs-lookup"><span data-stu-id="49079-129">Media Services receives hello ACS tokens from an authorization server.</span></span>

<span data-ttu-id="49079-130">Al desarrollar con hello SDK de servicios multimedia, puede elegir solucionan toonot tokens Hola porque Hola administradores de código SDK usarlas para usted.</span><span class="sxs-lookup"><span data-stu-id="49079-130">When developing with hello Media Services SDK, you can choose toonot deal with hello tokens because hello SDK code managers them for you.</span></span> <span data-ttu-id="49079-131">Sin embargo, lo que permitirá Hola SDK administrar totalmente Hola ACS tokens clientes potenciales toounnecessary las solicitudes de token.</span><span class="sxs-lookup"><span data-stu-id="49079-131">However, letting hello SDK fully manage hello ACS tokens leads toounnecessary token requests.</span></span> <span data-ttu-id="49079-132">Solicitar tokens lleva tiempo y consume recursos de servidor y cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="49079-132">Requesting tokens takes time and consumes hello client and server resources.</span></span> <span data-ttu-id="49079-133">Además, servidor de ACS de hello limita las solicitudes de hello si Hola velocidad es demasiado alta.</span><span class="sxs-lookup"><span data-stu-id="49079-133">Also, hello ACS server throttles hello requests if hello rate is too high.</span></span> <span data-ttu-id="49079-134">límite de Hello es de 30 solicitudes por segundo, consulte [limitaciones del servicio ACS](https://msdn.microsoft.com/library/gg185909.aspx) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="49079-134">hello limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="49079-135">A partir de hello SDK de servicios multimedia versión 3.0.0.0, puede volver a usar tokens de ACS de Hola.</span><span class="sxs-lookup"><span data-stu-id="49079-135">Starting with hello Media Services SDK version 3.0.0.0, you can reuse hello ACS tokens.</span></span> <span data-ttu-id="49079-136">Hola **CloudMediaContext** constructores que toman **MediaServicesCredentials** como un parámetro de habilitar uso compartido tokens Hola ACS entre varios contextos.</span><span class="sxs-lookup"><span data-stu-id="49079-136">hello **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing hello ACS tokens between multiple contexts.</span></span> <span data-ttu-id="49079-137">Hola MediaServicesCredentials clase encapsula las credenciales de servicios multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="49079-137">hello MediaServicesCredentials class encapsulates hello Media Services credentials.</span></span> <span data-ttu-id="49079-138">Si un token de ACS está disponible y se conoce la fecha de expiración, puede crear una nueva instancia de MediaServicesCredentials con token de Hola y páselo constructor toohello de CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="49079-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with hello token and pass it toohello constructor of CloudMediaContext.</span></span> <span data-ttu-id="49079-139">Tenga en cuenta que Hola SDK de servicios multimedia actualiza automáticamente los tokens cada vez que expiran.</span><span class="sxs-lookup"><span data-stu-id="49079-139">Note that hello Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="49079-140">Hay dos maneras de tokens de ACS tooreuse, tal y como se muestra en los ejemplos de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="49079-140">There are two ways tooreuse ACS tokens, as shown in hello examples below.</span></span>

* <span data-ttu-id="49079-141">Puede almacenar en caché hello **MediaServicesCredentials** objeto en memoria (por ejemplo, en una variable de clase estática).</span><span class="sxs-lookup"><span data-stu-id="49079-141">You can cache hello **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="49079-142">A continuación, pase el constructor de hello en caché objetos toohello CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="49079-142">Then, pass hello cached object toohello CloudMediaContext constructor.</span></span> <span data-ttu-id="49079-143">objeto de Hello MediaServicesCredentials contiene un token de ACS que se puede reutilizar si sigue siendo válido.</span><span class="sxs-lookup"><span data-stu-id="49079-143">hello MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="49079-144">Si el token de hello no es válido, se actualizarán por hello SDK de servicios multimedia con credenciales de hello tiene toohello MediaServicesCredentials constructor.</span><span class="sxs-lookup"><span data-stu-id="49079-144">If hello token is not valid, it will be refreshed by hello Media Services SDK using hello credentials given toohello MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="49079-145">Tenga en cuenta que hello **MediaServicesCredentials** objeto obtiene un token válido después de hello RefreshToken se llama.</span><span class="sxs-lookup"><span data-stu-id="49079-145">Note that hello **MediaServicesCredentials** object gets a valid token after hello RefreshToken is called.</span></span> <span data-ttu-id="49079-146">Hola **CloudMediaContext** Hola llamadas **RefreshToken** método hello constructor.</span><span class="sxs-lookup"><span data-stu-id="49079-146">hello **CloudMediaContext** calls hello **RefreshToken** method in hello constructor.</span></span> <span data-ttu-id="49079-147">Si tiene previsto almacenamiento externo de toosave Hola valores de token tooan, tome toocheck seguro si hello TokenExpiration valor es válido antes de guardar los datos de token de Hola.</span><span class="sxs-lookup"><span data-stu-id="49079-147">If you are planning toosave hello token values tooan external storage, make sure toocheck whether hello TokenExpiration value is valid before saving hello token data.</span></span> <span data-ttu-id="49079-148">Si no es válido, llame a RefreshToken antes del almacenamiento en caché.</span><span class="sxs-lookup"><span data-stu-id="49079-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="49079-149">También puede almacenar en caché hello AccessToken valores de cadena y hello TokenExpiration.</span><span class="sxs-lookup"><span data-stu-id="49079-149">You can also cache hello AccessToken string and hello TokenExpiration values.</span></span> <span data-ttu-id="49079-150">valores de Hello más tarde podrían ser usada toocreate un MediaServicesCredentials nuevo objeto con datos de token de hello en caché.</span><span class="sxs-lookup"><span data-stu-id="49079-150">hello values could later be used toocreate a new MediaServicesCredentials object with hello cached token data.</span></span>  <span data-ttu-id="49079-151">Esto es especialmente útil para escenarios donde el token de hello puede compartirse de forma segura entre varios procesos o equipos.</span><span class="sxs-lookup"><span data-stu-id="49079-151">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="49079-152">Hello siguientes fragmentos de código llaman Hola métodos SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage y UpdateTokenDataInExternalStorageIfNeeded que no estén definidos en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="49079-152">hello following code snippets call hello SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="49079-153">Puede definir estos métodos toostore y recuperar datos de token de actualización en un almacenamiento externo.</span><span class="sxs-lookup"><span data-stu-id="49079-153">You could define these methods toostore, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="49079-154">Usar hello guarda los valores de token toocreate MediaServicesCredentials.</span><span class="sxs-lookup"><span data-stu-id="49079-154">Use hello saved token values toocreate MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="49079-155">Actualizar copia del token de hello en caso de que el token de hello actualizó Hola SDK de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="49079-155">Update hello token copy in case hello token was updated by hello Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="49079-156">Si tiene varias cuentas de servicios multimedia (por ejemplo, para uso compartido con fines o la distribución geográfica de cargas) puede almacenar en caché objetos MediaServicesCredentials utilizando hello System.Collections.Concurrent.ConcurrentDictionary colección (Hola Colección de ConcurrentDictionary representa una colección segura para subprocesos de pares clave/valor que pueden acceder varios subprocesos simultáneamente).</span><span class="sxs-lookup"><span data-stu-id="49079-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using hello System.Collections.Concurrent.ConcurrentDictionary collection (hello ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="49079-157">A continuación, puede usar Hola GetOrAdd método tooget hello en caché credenciales.</span><span class="sxs-lookup"><span data-stu-id="49079-157">You can then use hello GetOrAdd method tooget hello cached credentials.</span></span> 
  
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

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a><span data-ttu-id="49079-158">Conexión de cuenta de servicios multimedia de tooa ubicado en la región del Norte de China Hola</span><span class="sxs-lookup"><span data-stu-id="49079-158">Connecting tooa Media Services account located in hello North China region</span></span>
<span data-ttu-id="49079-159">Si su cuenta se encuentra en la región del Norte de China hello, utilice Hola después de constructor:</span><span class="sxs-lookup"><span data-stu-id="49079-159">If your account is located in hello North China region, use hello following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="49079-160">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="49079-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="49079-161">Almacenar valores de conexión en la configuración</span><span class="sxs-lookup"><span data-stu-id="49079-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="49079-162">Es un valores de conexión de toostore altamente recomendado, especialmente los valores confidenciales como el nombre de cuenta y contraseña, en la configuración.</span><span class="sxs-lookup"><span data-stu-id="49079-162">It is a highly recommended practice toostore connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="49079-163">Además, es una práctica recomendada tooencrypt confidenciales de la configuración de datos.</span><span class="sxs-lookup"><span data-stu-id="49079-163">Also, it is a recommended practice tooencrypt sensitive configuration data.</span></span> <span data-ttu-id="49079-164">Puede cifrar archivo de configuración completo de hello mediante el uso de sistema de archivos de cifrado (EFS) de hello Windows.</span><span class="sxs-lookup"><span data-stu-id="49079-164">You can encrypt hello entire configuration file by using hello Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="49079-165">Seleccione tooenable EFS en un archivo, contextual hello, **propiedades**y habilitar el cifrado en hello **avanzadas** pestaña Configuración. O bien, puede crear una solución personalizada para cifrar las partes seleccionadas de un archivo de configuración mediante la configuración protegida.</span><span class="sxs-lookup"><span data-stu-id="49079-165">tooenable EFS on a file, right-click hello file, select **Properties**, and enable encryption in hello **Advanced** settings tab. Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="49079-166">Consulte [Cifrar información de configuración mediante una configuración protegida](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="49079-166">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="49079-167">Hola siguiente archivo App.config contiene valores de conexión de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="49079-167">hello following App.config file contains hello required connection values.</span></span> <span data-ttu-id="49079-168">Hola valores de hello <appSettings> elemento son valores de hello necesario que obtuvo en el proceso de configuración de cuenta de servicios multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="49079-168">hello values in hello <appSettings> element are hello required values that you got from hello Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="49079-169">tooretrieve los valores de conexión de configuración, puede usar hello **ConfigurationManager** clase y, a continuación, asignar toofields de valores de hello en el código:</span><span class="sxs-lookup"><span data-stu-id="49079-169">tooretrieve connection values from configuration, you can use hello **ConfigurationManager** class and then assign hello values toofields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="49079-170">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="49079-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="49079-171">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="49079-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

