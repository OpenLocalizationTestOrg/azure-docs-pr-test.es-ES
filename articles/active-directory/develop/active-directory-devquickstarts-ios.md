---
title: "aaaIntegrate Azure AD en una aplicación de iOS | Documentos de Microsoft"
description: "¿Cómo toobuild una aplicación de iOS que se integra con Azure AD para inicio de sesión y llamadas a Azure AD había protegido API mediante OAuth."
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="5a9b4-103">Integrar Azure AD en una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="5a9b4-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="5a9b4-104">Probar la versión preliminar de Hola de nuestra nueva [portal para desarrolladores de](https://identity.microsoft.com/Docs/iOS) que le ayuda a ponerse a trabajar con Azure Active Directory en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="5a9b4-105">portal para desarrolladores de Hello le guía a través del proceso de Hola de registrar una aplicación y la integración de Azure AD en el código.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-105">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="5a9b4-106">Cuando haya terminado, tendrá una aplicación sencilla que podrá autenticar a los usuarios del inquilino, así como un back-end con capacidad para aceptar tokens y realizar validaciones.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="5a9b4-107">Azure Active Directory (Azure AD) proporciona Hola biblioteca de autenticación de Active Directory o AAL, para los clientes de iOS que necesitan tooaccess los recursos protegidos.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-107">Azure Active Directory (Azure AD) provides hello Active Directory Authentication Library, or ADAL, for iOS clients that need tooaccess protected resources.</span></span> <span data-ttu-id="5a9b4-108">AAL simplifica el proceso de Hola que su aplicación usa los tokens de acceso tooobtain.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-108">ADAL simplifies hello process that your app uses tooobtain access tokens.</span></span> <span data-ttu-id="5a9b4-109">toodemonstrate lo fácil es, en este artículo se compila una aplicación de lista de tareas pendientes de C de objetivo que:</span><span class="sxs-lookup"><span data-stu-id="5a9b4-109">toodemonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="5a9b4-110">Obtiene acceso para llamar a API de Azure AD Graph hello mediante el uso de hello [protocolo de autenticación de OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a9b4-110">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="5a9b4-111">Buscar un directorio para los usuarios con un alias determinado</span><span class="sxs-lookup"><span data-stu-id="5a9b4-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="5a9b4-112">aplicación toobuild Hola completa trabajo, debe:</span><span class="sxs-lookup"><span data-stu-id="5a9b4-112">toobuild hello complete working application, you need to:</span></span>

1. <span data-ttu-id="5a9b4-113">Registrar la aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a9b4-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="5a9b4-114">Instalar y configurar ADAL.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="5a9b4-115">Usar AAL tooget tokens de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="5a9b4-116">tooget iniciado, [descargar esqueleto de aplicación Hola](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5a9b4-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="5a9b4-117">También necesita a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="5a9b4-118">Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="5a9b4-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="5a9b4-119">Probar la versión preliminar de Hola de nuestra nueva [portal para desarrolladores de](https://identity.microsoft.com/Docs/iOS) que le ayuda a ponerse en marcha con Azure AD en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-119">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="5a9b4-120">portal para desarrolladores de Hello le guía a través del proceso de Hola de registrar una aplicación y la integración de Azure AD en el código.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-120">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="5a9b4-121">Cuando haya terminado, tendrá una aplicación sencilla que podrá autenticar a los usuarios del inquilino, así como un back-end con capacidad para aceptar tokens y realizar validaciones.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="5a9b4-122">1. Determinación de cuál es el URI de redireccionamiento para iOS</span><span class="sxs-lookup"><span data-stu-id="5a9b4-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="5a9b4-123">toosecurely iniciar las aplicaciones en ciertos escenarios SSO, debe crear un *URI de redireccionamiento* en un formato determinado.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-123">toosecurely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="5a9b4-124">Una redirección URI es tooensure usado que Hola tokens toohello devuelto correcta aplicación que solicitó para ellos.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-124">A redirect URI is used tooensure that hello tokens return toohello correct application that asked for them.</span></span>


<span data-ttu-id="5a9b4-125">formato de iOS de Hello en una redirección URI es:</span><span class="sxs-lookup"><span data-stu-id="5a9b4-125">hello iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="5a9b4-126">**aap-scheme**: está registrado en el proyecto de XCode.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="5a9b4-127">Es el modo en que otras aplicaciones pueden llamarlo.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-127">It is how other applications can call you.</span></span> <span data-ttu-id="5a9b4-128">Puede encontrarlo en Info.plist -> Tipos de URL -> Identificador de URL.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="5a9b4-129">Debe crear uno si aún no tiene ninguno configurado.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="5a9b4-130">**identificador de paquete** -esto es hello bajo "identidad" se encuentra el identificador de paquete anula la configuración del proyecto en XCode.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-130">**bundle-id** - This is hello Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="5a9b4-131">Ejemplo de este código de inicio rápido: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-hello-directorysearcher-application"></a><span data-ttu-id="5a9b4-132">2. Registrar aplicación de DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="5a9b4-132">2. Register hello DirectorySearcher application</span></span>
<span data-ttu-id="5a9b4-133">tooset seguridad sus tokens de tooget de aplicación, primero debe tooregister en Azure AD de inquilinos y otórguele Hola de permiso tooaccess API de Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="5a9b4-133">tooset up your app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="5a9b4-134">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a9b4-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5a9b4-135">En la barra superior de hello, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-135">On hello top bar, click your account.</span></span> <span data-ttu-id="5a9b4-136">En hello **Directory** lista, seleccione la aplicación de inquilino de Active Directory de Hola donde desea tooregister.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-136">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="5a9b4-137">Haga clic en **más servicios** en Hola panel de navegación izquierda y, a continuación, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-137">Click **More Services** in hello leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="5a9b4-138">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="5a9b4-139">Siga Hola solicita toocreate un nuevo **aplicación cliente nativa**.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-139">Follow hello prompts toocreate a new **Native Client Application**.</span></span>
  * <span data-ttu-id="5a9b4-140">Hola **nombre** de hello aplicación describe los usuarios de tooend de aplicación.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-140">hello **Name** of hello application describes your application tooend users.</span></span>
  * <span data-ttu-id="5a9b4-141">Hola **Uri de redireccionamiento** es una combinación de esquema y la cadena que Azure AD usa tooreturn token respuestas.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-141">hello **Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span>  <span data-ttu-id="5a9b4-142">Escriba un valor que es específico tooyour aplicación y se basa en información del identificador URI de redireccionamiento anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-142">Enter a value that is specific tooyour application and is based on hello previous redirect URI information.</span></span>
6. <span data-ttu-id="5a9b4-143">Después de haber completado el registro de hello, Azure AD le asigna la aplicación un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-143">After you've completed hello registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="5a9b4-144">Necesitará este valor en las secciones siguientes de hello, por lo tanto cópiela desde la pestaña de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-144">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="5a9b4-145">De hello **configuración** página, seleccione **permisos necesarios** y, a continuación, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-145">From hello **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="5a9b4-146">Seleccione **Microsoft Graph** como Hola API y, a continuación, agregue hello **leer datos de directorio** permiso en **permisos delegados**.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-146">Select **Microsoft Graph** as hello API, and then add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="5a9b4-147">Esta acción configura la Hola de tooquery aplicación API de Azure AD Graph para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-147">This sets up your application tooquery hello Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="5a9b4-148">3. Instalación y configuración de ADAL</span><span class="sxs-lookup"><span data-stu-id="5a9b4-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="5a9b4-149">Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="5a9b4-150">Para obtener toocommunicate ADAL con Azure AD, deberá tooprovide con cierta información sobre el registro de aplicación.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-150">For ADAL toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

1. <span data-ttu-id="5a9b4-151">Comienza agregando toohello AAL DirectorySearcher proyecto mediante el uso de CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-151">Begin by adding ADAL toohello DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="5a9b4-152">Agregue Hola después toothis podfile:</span><span class="sxs-lookup"><span data-stu-id="5a9b4-152">Add hello following toothis podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="5a9b4-153">Ahora cargue hello podfile utilizando CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-153">Now load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="5a9b4-154">Mediante este paso se crea un área de trabajo de XCode que cargará.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="5a9b4-155">En proyecto de inicio rápido de hello, abra el archivo plist de hello `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-155">In hello QuickStart project, open hello plist file `settings.plist`.</span></span>  <span data-ttu-id="5a9b4-156">Reemplace los valores de hello de elementos de Hola de hello sección tooreflect Hola valores especificados en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-156">Replace hello values of hello elements in hello section tooreflect hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="5a9b4-157">El código hace referencia a estos valores cada vez que usa ADAL.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="5a9b4-158">Hola `tenant` es Hola dominio del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-158">hello `tenant` is hello domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="5a9b4-159">Hola `clientId` es Hola Id. de cliente de la aplicación que ha copiado desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-159">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="5a9b4-160">Hola `redirectUri` es la dirección URL de redireccionamiento de Hola que registró en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-160">hello `redirectUri` is hello redirect URL that you registered in hello portal.</span></span>

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="5a9b4-161">4.    Usar AAL tooget tokens de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a9b4-161">4.    Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="5a9b4-162">Hello principio básico detrás de AAL es que cada vez que la aplicación necesita un token de acceso, simplemente llama un completionBlock `+(void) getToken : `, y AAL Hola rest.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-162">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="5a9b4-163">Hola `QuickStart` proyecto abierto `GraphAPICaller.m` y busque hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comentario cerca de la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-163">In hello `QuickStart` project, open `GraphAPICaller.m` and locate hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near hello top.</span></span>  <span data-ttu-id="5a9b4-164">Aquí es donde pasan coordenadas Hola AAL a través de un CompletionBlock, toocommunicate con Azure AD y le diga cómo toocache símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="5a9b4-164">This is where you pass ADAL hello coordinates through a CompletionBlock, toocommunicate with Azure AD, and tell it how toocache tokens.</span></span>

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. <span data-ttu-id="5a9b4-165">Ahora necesitamos toouse este token toosearch para los usuarios en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-165">Now we need toouse this token toosearch for users in hello graph.</span></span> <span data-ttu-id="5a9b4-166">Buscar hello `// TODO: implement SearchUsersList` comentario.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-166">Find hello `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="5a9b4-167">Este método realiza una tooquery de toohello Azure AD Graph API de solicitud GET para los usuarios cuyo UPN comienza con hello dado el término de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-167">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="5a9b4-168">tooquery hello Azure AD Graph API, deberá tooinclude un access_token Hola `Authorization` encabezado de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-168">tooquery hello Azure AD Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request.</span></span> <span data-ttu-id="5a9b4-169">Aquí es donde entra en juego AAL.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-169">This is where ADAL comes in.</span></span>

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

                             [Users addObject:s];
                         }

                         completionBlock(Users, nil);
                     }
                     else
                     {
                         completionBlock(nil, error);
                     }

                }];
             }
         }];

    }

    ```


3. <span data-ttu-id="5a9b4-170">Cuando la aplicación solicita un token mediante una llamada a `getToken(...)`, AAL intenta tooreturn un token sin pedir las credenciales de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-170">When your app requests a token by calling `getToken(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="5a9b4-171">Si AAL determina que el usuario hello toosign en tooget un token es necesario, mostrar un cuadro de diálogo de inicio de sesión, recopilar las credenciales de usuario de hello y, a continuación, devuelve un token después de una autenticación correcta.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-171">If ADAL determines that hello user needs toosign in tooget a token, it will display a dialog box for sign-in, collect hello user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="5a9b4-172">Si AAL no es capaz de tooreturn un token por cualquier motivo, produce un `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-172">If ADAL is not able tooreturn a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="5a9b4-173">Hola `AuthenticationResult` objeto contiene un `tokenCacheStoreItem` objeto que puede ser usado toocollect Hola información que necesite la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-173">hello `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used toocollect hello information that your app may need.</span></span> <span data-ttu-id="5a9b4-174">Hola de inicio rápido, `tokenCacheStoreItem` es toodetermine usado si ya se realiza la autenticación.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-174">In hello QuickStart, `tokenCacheStoreItem` is used toodetermine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-hello-application"></a><span data-ttu-id="5a9b4-175">5. Compilar y ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="5a9b4-175">5. Build and run hello application</span></span>
<span data-ttu-id="5a9b4-176">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="5a9b4-176">Congratulations!</span></span> <span data-ttu-id="5a9b4-177">Ahora tiene una aplicación de iOS de trabajo que puede autenticar a los usuarios, seguro llamar a las API Web mediante OAuth 2.0 y obtener información básica acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="5a9b4-178">Si no lo ha hecho ya, ahora es Hola tiempo toopopulate el inquilino con algunos usuarios.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-178">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="5a9b4-179">Inicie la aplicación QuickStart e inicie sesión con uno de esos usuarios.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="5a9b4-180">Busque otros usuarios según su UPN.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="5a9b4-181">Cierre la aplicación hello y, a continuación, vuelva a abrirlo.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-181">Close hello app, and then start it again.</span></span>  <span data-ttu-id="5a9b4-182">Tenga en cuenta que la sesión del usuario de hello permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-182">Notice that hello user's session remains intact.</span></span>

<span data-ttu-id="5a9b4-183">AAL resulta fácil tooincorporate todas estas características de identidad comunes en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-183">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="5a9b4-184">Se encarga de todo el trabajo dirty Hola para usted, como la administración de memoria caché, compatibilidad con protocolos de OAuth, presentaciones usuario Hola con un toosign de interfaz de usuario en y actualizar tokens caducados.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-184">It takes care of all hello dirty work for you, like cache management, OAuth protocol support, presenting hello user with a UI toosign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="5a9b4-185">Todo lo que realmente necesita tooknow es una sola llamada API, `getToken`.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-185">All you really need tooknow is a single API call, `getToken`.</span></span>

<span data-ttu-id="5a9b4-186">Como referencia, ejemplo de Hola finalizado (sin los valores de configuración) se proporciona en [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5a9b4-186">For reference, hello completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="5a9b4-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5a9b4-187">Next steps</span></span>
<span data-ttu-id="5a9b4-188">Ahora puede mover en escenarios de tooadditional.</span><span class="sxs-lookup"><span data-stu-id="5a9b4-188">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="5a9b4-189">Puede que desee tootry:</span><span class="sxs-lookup"><span data-stu-id="5a9b4-189">You may want tootry:</span></span>

* [<span data-ttu-id="5a9b4-190">Proteger una API web de Node.js con Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a9b4-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="5a9b4-191">Obtenga información acerca de [cómo tooenable SSO de aplicación cruzado en iOS mediante AAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="5a9b4-191">Learn [how tooenable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

