---
title: "Integrar Azure AD en una aplicación iOS | Microsoft Docs"
description: "Cómo compilar una aplicación iOS que se integra con Azure AD para el inicio de sesión y llama a las API protegidas de Azure AD mediante OAuth."
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
ms.openlocfilehash: 57f465df99ac234466459b8031f61805d8334b59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="3e91b-103">Integrar Azure AD en una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="3e91b-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="3e91b-104">Pruebe la versión preliminar de nuestro nuevo [portal para desarrolladores](https://identity.microsoft.com/Docs/iOS), que le ayudará a empezar a trabajar con Azure Active Directory en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="3e91b-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="3e91b-105">El portal para desarrolladores lo guiará a través del proceso de registro de una aplicación y de integración de Azure AD en el código.</span><span class="sxs-lookup"><span data-stu-id="3e91b-105">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="3e91b-106">Cuando haya terminado, tendrá una aplicación sencilla que podrá autenticar a los usuarios del inquilino, así como un back-end con capacidad para aceptar tokens y realizar validaciones.</span><span class="sxs-lookup"><span data-stu-id="3e91b-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="3e91b-107">Azure Active Directory (Azure AD) proporciona la biblioteca de autenticación de Active Directory (ADAL) para los clientes de iOS que necesitan tener acceso a recursos protegidos.</span><span class="sxs-lookup"><span data-stu-id="3e91b-107">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span> <span data-ttu-id="3e91b-108">ADAL simplifica el proceso que la aplicación usa para obtener tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="3e91b-108">ADAL simplifies the process that your app uses to obtain access tokens.</span></span> <span data-ttu-id="3e91b-109">Para demostrar lo fácil que es, en este artículo compilaremos una aplicación Objective-C de lista de tareas pendientes que permita realizar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3e91b-109">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="3e91b-110">Obtiene tokens de acceso para llamar a la API Graph de Azure AD mediante el [protocolo de autenticación OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e91b-110">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="3e91b-111">Buscar un directorio para los usuarios con un alias determinado</span><span class="sxs-lookup"><span data-stu-id="3e91b-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="3e91b-112">Para compilar la aplicación de trabajo completa, debe realizar estas acciones:</span><span class="sxs-lookup"><span data-stu-id="3e91b-112">To build the complete working application, you need to:</span></span>

1. <span data-ttu-id="3e91b-113">Registrar la aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e91b-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="3e91b-114">Instalar y configurar ADAL.</span><span class="sxs-lookup"><span data-stu-id="3e91b-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="3e91b-115">Usar ADAL para obtener tokens de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e91b-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="3e91b-116">Para empezar, [descargue el esquema de la aplicación](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) o [descargue el ejemplo finalizado](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="3e91b-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="3e91b-117">También necesita a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e91b-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="3e91b-118">Si aún no tiene un inquilino, [descubra cómo conseguir uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="3e91b-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="3e91b-119">Pruebe la versión preliminar de nuestro nuevo [portal para desarrolladores](https://identity.microsoft.com/Docs/iOS), que le ayudará a empezar a trabajar con Azure AD en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="3e91b-119">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="3e91b-120">El portal para desarrolladores lo guiará a través del proceso de registro de una aplicación y de integración de Azure AD en el código.</span><span class="sxs-lookup"><span data-stu-id="3e91b-120">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="3e91b-121">Cuando haya terminado, tendrá una aplicación sencilla que podrá autenticar a los usuarios del inquilino, así como un back-end con capacidad para aceptar tokens y realizar validaciones.</span><span class="sxs-lookup"><span data-stu-id="3e91b-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="3e91b-122">1. Determinación de cuál es el URI de redireccionamiento para iOS</span><span class="sxs-lookup"><span data-stu-id="3e91b-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="3e91b-123">Para iniciar de forma segura sus aplicaciones en ciertos escenarios SSO, es necesaria la creación de un *URI de redireccionamiento* en un formato determinado.</span><span class="sxs-lookup"><span data-stu-id="3e91b-123">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="3e91b-124">Se usa un URI de redireccionamiento para garantizar que los tokens se devuelven a la aplicación correcta que los solicitó.</span><span class="sxs-lookup"><span data-stu-id="3e91b-124">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>


<span data-ttu-id="3e91b-125">El formato de iOS para un URI de redireccionamiento es:</span><span class="sxs-lookup"><span data-stu-id="3e91b-125">The iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="3e91b-126">**aap-scheme**: está registrado en el proyecto de XCode.</span><span class="sxs-lookup"><span data-stu-id="3e91b-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="3e91b-127">Es el modo en que otras aplicaciones pueden llamarlo.</span><span class="sxs-lookup"><span data-stu-id="3e91b-127">It is how other applications can call you.</span></span> <span data-ttu-id="3e91b-128">Puede encontrarlo en Info.plist -> Tipos de URL -> Identificador de URL.</span><span class="sxs-lookup"><span data-stu-id="3e91b-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="3e91b-129">Debe crear uno si aún no tiene ninguno configurado.</span><span class="sxs-lookup"><span data-stu-id="3e91b-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="3e91b-130">**bundle-id** : es el identificador de paquete que se encuentra en la "identity" de la configuración del proyecto en XCode.</span><span class="sxs-lookup"><span data-stu-id="3e91b-130">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="3e91b-131">Ejemplo de este código de inicio rápido: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***.</span><span class="sxs-lookup"><span data-stu-id="3e91b-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="3e91b-132">2. Registro de la aplicación DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="3e91b-132">2. Register the DirectorySearcher application</span></span>
<span data-ttu-id="3e91b-133">Para configurar la aplicación para que obtenga tokens, primero debe registrarla en su inquilino de Azure AD y concederle permiso de acceso a la API de Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="3e91b-133">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="3e91b-134">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3e91b-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3e91b-135">En la barra superior, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="3e91b-135">On the top bar, click your account.</span></span> <span data-ttu-id="3e91b-136">En la lista **Directorio** lista, elija el inquilino de Active Directory donde desea registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e91b-136">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>
3. <span data-ttu-id="3e91b-137">Haga clic en **Más servicios** en el panel de navegación izquierdo y seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-137">Click **More Services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="3e91b-138">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="3e91b-139">Siga las indicaciones para crear una nueva **aplicación cliente nativa**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-139">Follow the prompts to create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="3e91b-140">El **nombre** de la aplicación describe la aplicación a los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="3e91b-140">The **Name** of the application describes your application to end users.</span></span>
  * <span data-ttu-id="3e91b-141">El **URI de redireccionamiento** es una combinación de esquema y cadena que Azure AD usa para devolver respuestas de tokens.</span><span class="sxs-lookup"><span data-stu-id="3e91b-141">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span></span>  <span data-ttu-id="3e91b-142">Escriba un valor que sea específico de la aplicación y que se base en la información del anterior URI de redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="3e91b-142">Enter a value that is specific to your application and is based on the previous redirect URI information.</span></span>
6. <span data-ttu-id="3e91b-143">Después de haber completado el registro, Azure AD le asigna a la aplicación un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="3e91b-143">After you've completed the registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="3e91b-144">Necesitará este valor en las secciones siguientes, así que cópielo de la pestaña de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e91b-144">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="3e91b-145">En la página **Configuración**, seleccione **Permisos necesarios** y **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-145">From the **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="3e91b-146">Seleccione **Microsoft Graph** como API y agregue el permiso **Leer datos de directorio** en **Permisos delegados**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-146">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="3e91b-147">Esto configura la aplicación de modo que consulte la API Graph de Azure AD para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="3e91b-147">This sets up your application to query the Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="3e91b-148">3. Instalación y configuración de ADAL</span><span class="sxs-lookup"><span data-stu-id="3e91b-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="3e91b-149">Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="3e91b-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="3e91b-150">Para que ADAL se comunique con Azure AD, hay que proporcionarle información sobre el registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e91b-150">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

1. <span data-ttu-id="3e91b-151">Comience agregando ADAL al proyecto de DirectorySearcher mediante CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="3e91b-151">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="3e91b-152">Agregue lo siguiente a este podfile:</span><span class="sxs-lookup"><span data-stu-id="3e91b-152">Add the following to this podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="3e91b-153">Cargue el archivo podfile mediante CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="3e91b-153">Now load the podfile by using CocoaPods.</span></span> <span data-ttu-id="3e91b-154">Mediante este paso se crea un área de trabajo de XCode que cargará.</span><span class="sxs-lookup"><span data-stu-id="3e91b-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="3e91b-155">En el proyecto QuickStart, abra el archivo plist `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="3e91b-155">In the QuickStart project, open the plist file `settings.plist`.</span></span>  <span data-ttu-id="3e91b-156">Reemplace los valores de los elementos de la sección de modo que reflejen los especificados en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3e91b-156">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span></span> <span data-ttu-id="3e91b-157">El código hace referencia a estos valores cada vez que usa ADAL.</span><span class="sxs-lookup"><span data-stu-id="3e91b-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="3e91b-158">`tenant` es el dominio del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="3e91b-158">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="3e91b-159">`clientId` es el identificador de cliente de la aplicación que copió del portal.</span><span class="sxs-lookup"><span data-stu-id="3e91b-159">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="3e91b-160">`redirectUri` es la URL de redireccionamiento que ha registrado en el portal.</span><span class="sxs-lookup"><span data-stu-id="3e91b-160">The `redirectUri` is the redirect URL that you registered in the portal.</span></span>

## <a name="4----use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="3e91b-161">4.    Uso de ADAL para obtener tokens de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e91b-161">4.    Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="3e91b-162">El principio básico inherente a ADAL es que cada vez que la aplicación necesita un token de acceso, simplemente llama a un completionBlock `+(void) getToken : ` y ADAL se encarga del resto.</span><span class="sxs-lookup"><span data-stu-id="3e91b-162">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="3e91b-163">En el proyecto `QuickStart`, abra `GraphAPICaller.m` y busque el comentario `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="3e91b-163">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span>  <span data-ttu-id="3e91b-164">Este es el lugar en el que se pasan a ADAL mediante CompletionBlock las coordenadas necesarias para comunicarse con Azure AD e indicarle cómo almacenar en caché los tokens.</span><span class="sxs-lookup"><span data-stu-id="3e91b-164">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span></span>

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
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy to display the correct mobile UX. You most likely won't need it in your code.
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

2. <span data-ttu-id="3e91b-165">Ahora tenemos que utilizar este token para buscar usuarios en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="3e91b-165">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="3e91b-166">Busque el comentario `// TODO: implement SearchUsersList`.</span><span class="sxs-lookup"><span data-stu-id="3e91b-166">Find the `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="3e91b-167">Este método realiza una solicitud GET a la API Graph de Azure AD para realizar una consulta sobre los usuarios cuyo UPN comienza con el término de búsqueda especificado.</span><span class="sxs-lookup"><span data-stu-id="3e91b-167">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="3e91b-168">Para realizar una consulta a la API Graph de Azure AD, tiene que incluir un access_token en el encabezado `Authorization` de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="3e91b-168">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span></span> <span data-ttu-id="3e91b-169">Aquí es donde entra en juego AAL.</span><span class="sxs-lookup"><span data-stu-id="3e91b-169">This is where ADAL comes in.</span></span>

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

                         // We can grab the JSON node at the top to get our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by the key name being "value". It really is the name of the
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


3. <span data-ttu-id="3e91b-170">Cuando la aplicación llama a `getToken(...)` para solicitar un token, ADAL intenta devolver uno sin pedir credenciales al usuario.</span><span class="sxs-lookup"><span data-stu-id="3e91b-170">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="3e91b-171">Si ADAL determina que el usuario debe iniciar sesión para obtener un token, mostrará un cuadro de diálogo de inicio de sesión, recopilará las credenciales del usuario y devolverá un token tras una autenticación correcta.</span><span class="sxs-lookup"><span data-stu-id="3e91b-171">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="3e91b-172">Si ADAL no puede devolver un token por alguna razón, mostrará una `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="3e91b-172">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="3e91b-173">El objeto `AuthenticationResult` contiene un objeto `tokenCacheStoreItem` que puede usarse para recopilar información que puede necesitar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e91b-173">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span></span> <span data-ttu-id="3e91b-174">En QuickStart, `tokenCacheStoreItem` se usa para determinar si ya se ha producido la autenticación.</span><span class="sxs-lookup"><span data-stu-id="3e91b-174">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="3e91b-175">5. Compilación y ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3e91b-175">5. Build and run the application</span></span>
<span data-ttu-id="3e91b-176">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="3e91b-176">Congratulations!</span></span> <span data-ttu-id="3e91b-177">Ahora tiene una aplicación de iOS operativa que puede autenticar usuarios, realizar llamadas seguras a las API web mediante OAuth 2.0 y obtener información básica sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="3e91b-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="3e91b-178">Si todavía no lo ha hecho, ahora es el momento de completar el inquilino con algunos usuarios.</span><span class="sxs-lookup"><span data-stu-id="3e91b-178">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="3e91b-179">Inicie la aplicación QuickStart e inicie sesión con uno de esos usuarios.</span><span class="sxs-lookup"><span data-stu-id="3e91b-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="3e91b-180">Busque otros usuarios según su UPN.</span><span class="sxs-lookup"><span data-stu-id="3e91b-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="3e91b-181">Cierre la aplicación y vuelva a abrirla.</span><span class="sxs-lookup"><span data-stu-id="3e91b-181">Close the app, and then start it again.</span></span>  <span data-ttu-id="3e91b-182">Observe que la sesión del usuario permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="3e91b-182">Notice that the user's session remains intact.</span></span>

<span data-ttu-id="3e91b-183">ADAL facilita la incorporación de todas estas características comunes de identidad en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e91b-183">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="3e91b-184">Hace el trabajo sucio por usted: administración en caché, compatibilidad con el protocolo OAuth, presentación al usuario de una interfaz de usuario de inicio de sesión y actualización de tokens expirados.</span><span class="sxs-lookup"><span data-stu-id="3e91b-184">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="3e91b-185">Todo lo que necesita saber es una única llamada de API, `getToken`.</span><span class="sxs-lookup"><span data-stu-id="3e91b-185">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="3e91b-186">Como referencia, en [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip) puede ver el ejemplo finalizado (sin sus valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="3e91b-186">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3e91b-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3e91b-187">Next steps</span></span>
<span data-ttu-id="3e91b-188">Ahora puede pasar a otros escenarios.</span><span class="sxs-lookup"><span data-stu-id="3e91b-188">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="3e91b-189">También puede probar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3e91b-189">You may want to try:</span></span>

* [<span data-ttu-id="3e91b-190">Proteger una API web de Node.js con Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e91b-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="3e91b-191">Obtener información sobre [cómo habilitar el inicio de sesión único entre aplicaciones en iOS mediante ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="3e91b-191">Learn [how to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

