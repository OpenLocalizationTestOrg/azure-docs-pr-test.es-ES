---
title: aaaBridge iOS WebView con iOS nativa de Mobile Engagement SDK
description: "Describe cómo toocreate un puente entre WebView ejecutando hello y Javascript nativo Mobile Engagement SDK de iOS"
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
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="30849-103">Puente de WebView en iOS con el SDK de iOS para Mobile Engagement nativo</span><span class="sxs-lookup"><span data-stu-id="30849-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30849-104">Puente de Android</span><span class="sxs-lookup"><span data-stu-id="30849-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="30849-105">Puente de iOS</span><span class="sxs-lookup"><span data-stu-id="30849-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="30849-106">Algunas aplicaciones móviles están diseñados como una aplicación híbrida donde la propia aplicación Hola se ha desarrollado usando la implementación de iOS nativo Objective-C pero algunos o incluso todas las pantallas de Hola se representan dentro de una vista Web de iOS.</span><span class="sxs-lookup"><span data-stu-id="30849-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native iOS Objective-C development but some or even all of hello screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="30849-107">Podrá seguir consumiendo SDK de Mobile Engagement iOS dentro de esas aplicaciones y este tutorial se describe cómo toogo acerca de cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="30849-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how toogo about doing this.</span></span> 

<span data-ttu-id="30849-108">Hay dos tooachieve enfoques esto aunque ambos son no documentados:</span><span class="sxs-lookup"><span data-stu-id="30849-108">There are two approaches tooachieve this though both are undocumented:</span></span>

* <span data-ttu-id="30849-109">El primero se describe en este [vínculo](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip), para el que es necesario registrar un `UIWebViewDelegate` en el WebView y, después, realizar un cambio de ubicación y su posterior cancelación inmediata en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="30849-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="30849-110">En segundo lugar, uno se basa en el objeto [WWDC 2013 sesión](https://developer.apple.com/videos/play/wwdc2013/615), un enfoque que es más limpio que Hola por primera vez y que se sigue en esta guía.</span><span class="sxs-lookup"><span data-stu-id="30849-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than hello first and which we will follow for this guide.</span></span> <span data-ttu-id="30849-111">Tenga en cuenta que este método solo funciona en iOS7 o una versión superior.</span><span class="sxs-lookup"><span data-stu-id="30849-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="30849-112">Siga los pasos de hello siguientes para iOS Hola cubrir ejemplo:</span><span class="sxs-lookup"><span data-stu-id="30849-112">Follow hello steps below for hello iOS bridge sample:</span></span>

1. <span data-ttu-id="30849-113">En primer lugar, debe tooensure que hayan pasado por nuestro [tutorial de introducción](mobile-engagement-ios-get-started.md) toointegrate Hola SDK de Mobile Engagement iOS en su aplicación híbrida.</span><span class="sxs-lookup"><span data-stu-id="30849-113">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) toointegrate hello Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="30849-114">Si lo desea, también puede habilitar pruebas se registre como sigue para que puedan ver métodos SDK de hello tal y como se activan de hello webview.</span><span class="sxs-lookup"><span data-stu-id="30849-114">Optionally, you can also enable test logging as follows so that you can see hello SDK methods as we trigger them from hello webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="30849-115">Ahora, asegúrese de que la aplicación híbrida tiene una pantalla con el componente WebView.</span><span class="sxs-lookup"><span data-stu-id="30849-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="30849-116">Puede agregar toohello `Main.storyboard` de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="30849-116">You can add it toohello `Main.storyboard` of hello app.</span></span> 
3. <span data-ttu-id="30849-117">Asociar este webview con su **ViewController** haciendo clic y arrastrando Hola webview de hello vista controlador escena toohello `ViewController.h` editar pantalla, colocarlo justo debajo de hello `@interface` línea.</span><span class="sxs-lookup"><span data-stu-id="30849-117">Associate this webview with your **ViewController** by clicking and dragging hello webview from hello View Controller Scene toohello `ViewController.h` edit screen, placing it just below hello `@interface` line.</span></span> 
4. <span data-ttu-id="30849-118">Cuando lo haya hecho, aparecerá un cuadro de diálogo solicitando un nombre.</span><span class="sxs-lookup"><span data-stu-id="30849-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="30849-119">Proporcione nombre hello como **webView**.</span><span class="sxs-lookup"><span data-stu-id="30849-119">Provide hello name as **webView**.</span></span> <span data-ttu-id="30849-120">Su `ViewController.h` archivo debe ser similar al siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="30849-120">Your `ViewController.h` file should look like hello following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="30849-121">Actualizaremos hello `ViewController.m` archivo más adelante, pero en primer lugar se creará el archivo de puente de hello que crea un contenedor a través de algunas iOS Mobile Engagement utilizadas métodos SDK.</span><span class="sxs-lookup"><span data-stu-id="30849-121">We will update hello `ViewController.m` file later but first we will create hello bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="30849-122">Crear un nuevo archivo de encabezado denominado **EngagementJsExports.h** que utiliza hello `JSExport` mecanismo descrito en hello mencionado anteriormente [sesión](https://developer.apple.com/videos/play/wwdc2013/615) métodos de tooexpose Hola nativas para iOS.</span><span class="sxs-lookup"><span data-stu-id="30849-122">Create a new header file called **EngagementJsExports.h** which uses hello `JSExport` mechanism described in hello aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello native iOS methods.</span></span> 
   
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
6. <span data-ttu-id="30849-123">A continuación se creará la segunda parte del archivo de puente de hello de Hola.</span><span class="sxs-lookup"><span data-stu-id="30849-123">Next we will create hello second part of hello bridge file.</span></span> <span data-ttu-id="30849-124">Cree un archivo denominado **EngagementJsExports.m** que contendrá la implementación de hello creación de hello contenedores reales mediante una llamada a iOS de Mobile Engagement Hola métodos SDK.</span><span class="sxs-lookup"><span data-stu-id="30849-124">Create a file called **EngagementJsExports.m** which will contain hello implementation creating hello actual wrappers by calling hello Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="30849-125">Tenga en cuenta también que nos estamos analizando hello `extras` que se pasan desde javascript de webview de Hola y colocarlo en un `NSMutableDictionary` toobe del objeto pasado con hello método Engagement SDK llamadas.</span><span class="sxs-lookup"><span data-stu-id="30849-125">Also note that we are parsing hello `extras` being passed from hello webview javascript and putting that into an `NSMutableDictionary` object toobe passed with hello Engagement SDK method calls.</span></span>  
   
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
7. <span data-ttu-id="30849-126">Ahora se vuelven a estar toohello **ViewController.m** y actualizarla con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="30849-126">Now we come back toohello **ViewController.m** and update it with hello following code:</span></span> 
   
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
8. <span data-ttu-id="30849-127">Puntos siguientes de Hola de nota sobre hello **ViewController.m** archivo:</span><span class="sxs-lookup"><span data-stu-id="30849-127">Note hello following points about hello **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="30849-128">Hola `loadWebView` método, vamos a cargar un archivo HTML local denominado **LocalPage.html** cuyo código se tratarán a continuación.</span><span class="sxs-lookup"><span data-stu-id="30849-128">In hello `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="30849-129">Hola `webViewDidFinishLoad` método, nos estamos arrastrar hello `JsContext` y asociar a la clase contenedora.</span><span class="sxs-lookup"><span data-stu-id="30849-129">In hello `webViewDidFinishLoad` method, we are grabbing hello `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="30849-130">Esto le permitirá llamar a nuestro contenedor métodos SDK mediante identificador hello **EngagementJs** de hello webView.</span><span class="sxs-lookup"><span data-stu-id="30849-130">This will allow calling our wrapper SDK methods using hello handle **EngagementJs** from hello webView.</span></span> 
9. <span data-ttu-id="30849-131">Cree un archivo denominado **LocalPage.html** con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="30849-131">Create a file called **LocalPage.html** with hello following code:</span></span>
   
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
                       // Example of how extras info can be passed with hello Engagement logs
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
10. <span data-ttu-id="30849-132">Puntos siguientes de Hola de nota sobre el archivo HTML de hello anterior:</span><span class="sxs-lookup"><span data-stu-id="30849-132">Note hello following points about hello HTML file above:</span></span>
    
    * <span data-ttu-id="30849-133">Contiene un conjunto de cuadros de entrada donde se puede especificar toobe de datos que se usan como nombres para el evento, trabajo, Error, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="30849-133">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="30849-134">Al hacer clic en tooit de hello botón siguiente, se realiza una llamada toohello Javascript que finalmente llama métodos Hola de hello puente archivo toopass esta toohello llamada SDK de Mobile Engagement iOS.</span><span class="sxs-lookup"><span data-stu-id="30849-134">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="30849-135">En algunos eventos de toohello estático información adicional, los trabajos e incluso errores toodemonstrate nos estamos etiquetado cómo esto puede realizarse.</span><span class="sxs-lookup"><span data-stu-id="30849-135">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="30849-136">Esta información adicional se envía como cadena de JSON que, si mira en hello `EngagementJsExports.m` de archivos, que se analiza y se pasa junto con eventos, trabajos, errores de envío.</span><span class="sxs-lookup"><span data-stu-id="30849-136">This extra info is sent as a JSON string which, if you look in hello `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="30849-137">Un trabajo de interacción móvil comienza con el nombre de Hola se especifica en el cuadro de entrada de hello, ejecutar durante 10 segundos y apagar.</span><span class="sxs-lookup"><span data-stu-id="30849-137">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="30849-138">Una etiqueta o Mobile Engagement appinfo se pasa con 'customer_name' como clave estática de Hola y el valor de Hola que ha especificado en la entrada de hello como valor de Hola para etiqueta Hola.</span><span class="sxs-lookup"><span data-stu-id="30849-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
11. <span data-ttu-id="30849-139">Aplicación hello ejecución y verá la siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="30849-139">Run hello app and you will see hello following.</span></span> <span data-ttu-id="30849-140">Proporcione un nombre para un evento de prueba como Hola después ahora y haga clic en **enviar** tooit siguiente.</span><span class="sxs-lookup"><span data-stu-id="30849-140">Now provide some name for a test event like hello following and click **Send** next tooit.</span></span> 
    
     ![][1]
12. <span data-ttu-id="30849-141">Ahora, si vaya toohello **Monitor** pestaña de la aplicación y busque **eventos -> detalles**, verá que este evento mostrarán junto con hello estático app-info que te enviamos.</span><span class="sxs-lookup"><span data-stu-id="30849-141">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
