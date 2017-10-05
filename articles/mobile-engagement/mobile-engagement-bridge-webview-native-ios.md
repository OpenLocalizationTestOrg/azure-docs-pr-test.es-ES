---
title: Puente de WebView en iOS con el SDK de iOS para Mobile Engagement nativo
description: "Describe cómo crear un puente entre un componente WebView que ejecuta Javascript y el SDK de iOS para Mobile Engagement nativo"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 35f7bdbeb480122513ae2a0b04a6d8cfd426802a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="1b574-103">Puente de WebView en iOS con el SDK de iOS para Mobile Engagement nativo</span><span class="sxs-lookup"><span data-stu-id="1b574-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b574-104">Puente de Android</span><span class="sxs-lookup"><span data-stu-id="1b574-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="1b574-105">Puente de iOS</span><span class="sxs-lookup"><span data-stu-id="1b574-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="1b574-106">Algunas aplicaciones móviles están diseñadas como una aplicación híbrida en la que la propia aplicación se desarrolla mediante tecnología Objective-C nativa de iOS, pero algunas o incluso todas las pantallas se representan en el componente WebView en iOS.</span><span class="sxs-lookup"><span data-stu-id="1b574-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native iOS Objective-C development but some or even all of the screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="1b574-107">Puede seguir utilizando el SDK de iOS para Mobile Engagement en estas aplicaciones: en este tutorial se describe cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="1b574-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how to go about doing this.</span></span> 

<span data-ttu-id="1b574-108">Para ello, puede seguir dos planteamientos, aunque no se documentan en este artículo:</span><span class="sxs-lookup"><span data-stu-id="1b574-108">There are two approaches to achieve this though both are undocumented:</span></span>

* <span data-ttu-id="1b574-109">El primero se describe en este [vínculo](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip), para el que es necesario registrar un `UIWebViewDelegate` en el WebView y, después, realizar un cambio de ubicación y su posterior cancelación inmediata en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1b574-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="1b574-110">El segundo se basa en esta [sesión WWDC 2013](https://developer.apple.com/videos/play/wwdc2013/615), un planteamiento que es más limpio que el primero y que seguiremos en esta guía.</span><span class="sxs-lookup"><span data-stu-id="1b574-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than the first and which we will follow for this guide.</span></span> <span data-ttu-id="1b574-111">Tenga en cuenta que este método solo funciona en iOS7 o una versión superior.</span><span class="sxs-lookup"><span data-stu-id="1b574-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="1b574-112">Siga los pasos siguientes para el ejemplo de puente de iOS.</span><span class="sxs-lookup"><span data-stu-id="1b574-112">Follow the steps below for the iOS bridge sample:</span></span>

1. <span data-ttu-id="1b574-113">En primer lugar, debe asegurarse de que ha completado nuestro [tutorial de introducción](mobile-engagement-ios-get-started.md) para integrar el SDK de iOS para Mobile Engagement en la aplicación híbrida.</span><span class="sxs-lookup"><span data-stu-id="1b574-113">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) to integrate the Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="1b574-114">Si lo desea, también puede habilitar el registro de pruebas del modo siguiente para ver los métodos SDK a medida que se desencadenen en WebView.</span><span class="sxs-lookup"><span data-stu-id="1b574-114">Optionally, you can also enable test logging as follows so that you can see the SDK methods as we trigger them from the webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="1b574-115">Ahora, asegúrese de que la aplicación híbrida tiene una pantalla con el componente WebView.</span><span class="sxs-lookup"><span data-stu-id="1b574-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="1b574-116">Puede agregarlo al `Main.storyboard` de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1b574-116">You can add it to the `Main.storyboard` of the app.</span></span> 
3. <span data-ttu-id="1b574-117">Para asociar el WebView a su **ViewController**, haga clic y arrastre el WebView desde View Controller Scene hasta la pantalla de edición de `ViewController.h` y, después, colóquelo justo debajo de la línea `@interface`.</span><span class="sxs-lookup"><span data-stu-id="1b574-117">Associate this webview with your **ViewController** by clicking and dragging the webview from the View Controller Scene to the `ViewController.h` edit screen, placing it just below the `@interface` line.</span></span> 
4. <span data-ttu-id="1b574-118">Cuando lo haya hecho, aparecerá un cuadro de diálogo solicitando un nombre.</span><span class="sxs-lookup"><span data-stu-id="1b574-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="1b574-119">Proporcione el nombre como **webView**.</span><span class="sxs-lookup"><span data-stu-id="1b574-119">Provide the name as **webView**.</span></span> <span data-ttu-id="1b574-120">El archivo `ViewController.h` debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="1b574-120">Your `ViewController.h` file should look like the following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="1b574-121">El archivo `ViewController.m` se actualizará más adelante, pero antes se creará el archivo puente que crea un contenedor sobre algunos de los métodos del SDK de iOS para Mobile Engagement más utilizados.</span><span class="sxs-lookup"><span data-stu-id="1b574-121">We will update the `ViewController.m` file later but first we will create the bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="1b574-122">Cree un archivo de encabezado denominado **EngagementJsExports.h** que use el mecanismo `JSExport` descrito en la [sesión](https://developer.apple.com/videos/play/wwdc2013/615) anterior para exponer los métodos de iOS nativos.</span><span class="sxs-lookup"><span data-stu-id="1b574-122">Create a new header file called **EngagementJsExports.h** which uses the `JSExport` mechanism described in the aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) to expose the native iOS methods.</span></span> 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. <span data-ttu-id="1b574-123">A continuación, crearemos la segunda parte del archivo puente.</span><span class="sxs-lookup"><span data-stu-id="1b574-123">Next we will create the second part of the bridge file.</span></span> <span data-ttu-id="1b574-124">Cree un archivo llamado **EngagementJsExports.m** que contenga la implementación (para hacerlo, cree los contenedores reales llamando a los métodos del SDK de iOS para Mobile Engagement).</span><span class="sxs-lookup"><span data-stu-id="1b574-124">Create a file called **EngagementJsExports.m** which will contain the implementation creating the actual wrappers by calling the Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="1b574-125">Observe también que se está analizando el `extras` que se pasa desde Javascript en Webview y que se pone en un objeto `NSMutableDictionary` que se pasará con las llamadas al método del SDK para Engagement.</span><span class="sxs-lookup"><span data-stu-id="1b574-125">Also note that we are parsing the `extras` being passed from the webview javascript and putting that into an `NSMutableDictionary` object to be passed with the Engagement SDK method calls.</span></span>  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. <span data-ttu-id="1b574-126">Ahora, se regresa a **ViewController.m** y se actualiza con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b574-126">Now we come back to the **ViewController.m** and update it with the following code:</span></span> 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. <span data-ttu-id="1b574-127">Tenga en cuenta los siguientes aspectos sobre el archivo **ViewController.m** :</span><span class="sxs-lookup"><span data-stu-id="1b574-127">Note the following points about the **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="1b574-128">En el método `loadWebView` , se está cargando un archivo HTML local denominado **LocalPage.html** cuyo código se examinará a continuación.</span><span class="sxs-lookup"><span data-stu-id="1b574-128">In the `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="1b574-129">En el método `webViewDidFinishLoad`, se está tomando `JsContext` y se está asociando nuestra clase de contenedor a este valor.</span><span class="sxs-lookup"><span data-stu-id="1b574-129">In the `webViewDidFinishLoad` method, we are grabbing the `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="1b574-130">Esto posibilitará la llamada a nuestros métodos de SDK de contenedor mediante el identificador **EngagementJs** desde WebView.</span><span class="sxs-lookup"><span data-stu-id="1b574-130">This will allow calling our wrapper SDK methods using the handle **EngagementJs** from the webView.</span></span> 
9. <span data-ttu-id="1b574-131">Cree un archivo llamado **LocalPage.html** con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b574-131">Create a file called **LocalPage.html** with the following code:</span></span>
   
        <!doctype html>
        <html>
           <head>
               <style type='text/css'>
                   html { font-family:Helvetica; color:#222; }
                   h1 { color:steelblue; font-size:22px; margin-top:16px; }
                   h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
               </style>
   
               <script type="text/javascript">
   
               window.onerror = function(err)
               {
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with the Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. <span data-ttu-id="1b574-132">Tenga en cuenta los siguientes aspectos sobre el archivo HTML anterior:</span><span class="sxs-lookup"><span data-stu-id="1b574-132">Note the following points about the HTML file above:</span></span>
    
    * <span data-ttu-id="1b574-133">Contiene un conjunto de cuadros de entrada donde puede proporcionar los datos que se utilizarán como nombres para los valores de Event, Job, Error, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="1b574-133">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="1b574-134">Al hacer clic en el botón situado junto a él, se realiza una llamada a Javascript, que finalmente llama a los métodos desde el archivo puente para pasar esta llamada al SDK de iOS para Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1b574-134">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="1b574-135">Estamos añadiendo algo de información adicional estática a los eventos, trabajos e incluso errores para demostrar cómo podría ser este proceso.</span><span class="sxs-lookup"><span data-stu-id="1b574-135">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="1b574-136">Esta información adicional se envía como una cadena JSON que, si observa el archivo `EngagementJsExports.m` , se analiza y se pasa junto con los eventos, las tareas y los errores que se envían.</span><span class="sxs-lookup"><span data-stu-id="1b574-136">This extra info is sent as a JSON string which, if you look in the `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="1b574-137">Un trabajo de Mobile Engagement comienza con el nombre que especifique en el cuadro de entrada, se ejecuta durante 10 segundos y luego se apaga.</span><span class="sxs-lookup"><span data-stu-id="1b574-137">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="1b574-138">Se pasa una información de aplicación o una etiqueta de Mobile Engagement con 'customer_name' como clave estática y el valor que especificó en la entrada como valor para la etiqueta.</span><span class="sxs-lookup"><span data-stu-id="1b574-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
11. <span data-ttu-id="1b574-139">Ejecute la aplicación y verá lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="1b574-139">Run the app and you will see the following.</span></span> <span data-ttu-id="1b574-140">Ahora, proporcione un nombre para un evento de prueba similar al siguiente y haga clic en el botón **Send** (Enviar) que está al lado.</span><span class="sxs-lookup"><span data-stu-id="1b574-140">Now provide some name for a test event like the following and click **Send** next to it.</span></span> 
    
     ![][1]
12. <span data-ttu-id="1b574-141">Ahora, si va a la pestaña **Monitor** (Supervisar) de la aplicación y busca **Events -> Details** (Eventos -> Detalles), verá que este evento se muestra con app-info estática que se envía.</span><span class="sxs-lookup"><span data-stu-id="1b574-141">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
