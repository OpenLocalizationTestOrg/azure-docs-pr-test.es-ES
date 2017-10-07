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
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a>Puente de WebView en iOS con el SDK de iOS para Mobile Engagement nativo
> [!div class="op_single_selector"]
> * [Puente de Android](mobile-engagement-bridge-webview-native-android.md)
> * [Puente de iOS](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Algunas aplicaciones móviles están diseñados como una aplicación híbrida donde la propia aplicación Hola se ha desarrollado usando la implementación de iOS nativo Objective-C pero algunos o incluso todas las pantallas de Hola se representan dentro de una vista Web de iOS. Podrá seguir consumiendo SDK de Mobile Engagement iOS dentro de esas aplicaciones y este tutorial se describe cómo toogo acerca de cómo hacerlo. 

Hay dos tooachieve enfoques esto aunque ambos son no documentados:

* El primero se describe en este [vínculo](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip), para el que es necesario registrar un `UIWebViewDelegate` en el WebView y, después, realizar un cambio de ubicación y su posterior cancelación inmediata en JavaScript. 
* En segundo lugar, uno se basa en el objeto [WWDC 2013 sesión](https://developer.apple.com/videos/play/wwdc2013/615), un enfoque que es más limpio que Hola por primera vez y que se sigue en esta guía. Tenga en cuenta que este método solo funciona en iOS7 o una versión superior. 

Siga los pasos de hello siguientes para iOS Hola cubrir ejemplo:

1. En primer lugar, debe tooensure que hayan pasado por nuestro [tutorial de introducción](mobile-engagement-ios-get-started.md) toointegrate Hola SDK de Mobile Engagement iOS en su aplicación híbrida. Si lo desea, también puede habilitar pruebas se registre como sigue para que puedan ver métodos SDK de hello tal y como se activan de hello webview. 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. Ahora, asegúrese de que la aplicación híbrida tiene una pantalla con el componente WebView. Puede agregar toohello `Main.storyboard` de aplicación hello. 
3. Asociar este webview con su **ViewController** haciendo clic y arrastrando Hola webview de hello vista controlador escena toohello `ViewController.h` editar pantalla, colocarlo justo debajo de hello `@interface` línea. 
4. Cuando lo haya hecho, aparecerá un cuadro de diálogo solicitando un nombre. Proporcione nombre hello como **webView**. Su `ViewController.h` archivo debe ser similar al siguiente hello:
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. Actualizaremos hello `ViewController.m` archivo más adelante, pero en primer lugar se creará el archivo de puente de hello que crea un contenedor a través de algunas iOS Mobile Engagement utilizadas métodos SDK. Crear un nuevo archivo de encabezado denominado **EngagementJsExports.h** que utiliza hello `JSExport` mecanismo descrito en hello mencionado anteriormente [sesión](https://developer.apple.com/videos/play/wwdc2013/615) métodos de tooexpose Hola nativas para iOS. 
   
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
6. A continuación se creará la segunda parte del archivo de puente de hello de Hola. Cree un archivo denominado **EngagementJsExports.m** que contendrá la implementación de hello creación de hello contenedores reales mediante una llamada a iOS de Mobile Engagement Hola métodos SDK. Tenga en cuenta también que nos estamos analizando hello `extras` que se pasan desde javascript de webview de Hola y colocarlo en un `NSMutableDictionary` toobe del objeto pasado con hello método Engagement SDK llamadas.  
   
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
7. Ahora se vuelven a estar toohello **ViewController.m** y actualizarla con hello siguiente código: 
   
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
8. Puntos siguientes de Hola de nota sobre hello **ViewController.m** archivo:
   
   * Hola `loadWebView` método, vamos a cargar un archivo HTML local denominado **LocalPage.html** cuyo código se tratarán a continuación. 
   * Hola `webViewDidFinishLoad` método, nos estamos arrastrar hello `JsContext` y asociar a la clase contenedora. Esto le permitirá llamar a nuestro contenedor métodos SDK mediante identificador hello **EngagementJs** de hello webView. 
9. Cree un archivo denominado **LocalPage.html** con hello siguiente código:
   
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
10. Puntos siguientes de Hola de nota sobre el archivo HTML de hello anterior:
    
    * Contiene un conjunto de cuadros de entrada donde se puede especificar toobe de datos que se usan como nombres para el evento, trabajo, Error, AppInfo. Al hacer clic en tooit de hello botón siguiente, se realiza una llamada toohello Javascript que finalmente llama métodos Hola de hello puente archivo toopass esta toohello llamada SDK de Mobile Engagement iOS. 
    * En algunos eventos de toohello estático información adicional, los trabajos e incluso errores toodemonstrate nos estamos etiquetado cómo esto puede realizarse. Esta información adicional se envía como cadena de JSON que, si mira en hello `EngagementJsExports.m` de archivos, que se analiza y se pasa junto con eventos, trabajos, errores de envío. 
    * Un trabajo de interacción móvil comienza con el nombre de Hola se especifica en el cuadro de entrada de hello, ejecutar durante 10 segundos y apagar. 
    * Una etiqueta o Mobile Engagement appinfo se pasa con 'customer_name' como clave estática de Hola y el valor de Hola que ha especificado en la entrada de hello como valor de Hola para etiqueta Hola. 
11. Aplicación hello ejecución y verá la siguiente Hola. Proporcione un nombre para un evento de prueba como Hola después ahora y haga clic en **enviar** tooit siguiente. 
    
     ![][1]
12. Ahora, si vaya toohello **Monitor** pestaña de la aplicación y busque **eventos -> detalles**, verá que este evento mostrarán junto con hello estático app-info que te enviamos. 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
