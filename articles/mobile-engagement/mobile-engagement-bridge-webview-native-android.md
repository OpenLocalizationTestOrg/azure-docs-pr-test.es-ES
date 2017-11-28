---
title: aaaBridge WebView Android nativo Mobile Engagement Android SDK
description: "Describe cómo un puente entre WebView toocreate ejecutar Javascript y Hola nativo SDK de Android de interacción móvil"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a7a09bcc156490fe69ad29a67809745dcfc22da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="71a4f-103">Puente de WebView en Android con el SDK de Android para Mobile Engagement nativo</span><span class="sxs-lookup"><span data-stu-id="71a4f-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71a4f-104">Puente de Android</span><span class="sxs-lookup"><span data-stu-id="71a4f-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="71a4f-105">Puente de iOS</span><span class="sxs-lookup"><span data-stu-id="71a4f-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="71a4f-106">Algunas aplicaciones móviles están diseñados como una aplicación híbrida donde propia aplicación Hola se ha desarrollado usando desarrollo nativo de Android, pero algunos o incluso todas las pantallas de Hola se representan dentro de un WebView Android.</span><span class="sxs-lookup"><span data-stu-id="71a4f-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native Android development but some or even all of hello screens are rendered within an Android WebView.</span></span> <span data-ttu-id="71a4f-107">Podrá seguir consumiendo Android SDK de Mobile Engagement dentro de esas aplicaciones y este tutorial se describe cómo toogo acerca de cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="71a4f-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how toogo about doing this.</span></span> <span data-ttu-id="71a4f-108">Hola ejemplo de código siguiente se basa en hello documentación Android [aquí](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="71a4f-108">hello sample code below is based on hello Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="71a4f-109">Describe cómo se podría utilizar este enfoque documentado tooimplement Hola igual para Mobile Engagement Android SDK de uso general métodos de forma que una vista Web desde una aplicación híbrida también puede iniciar solicitudes tootrack eventos, los trabajos, errores y app-info mientras canalizando ellos a través de el SDK de Android.</span><span class="sxs-lookup"><span data-stu-id="71a4f-109">It describes how this documented approach could be used tooimplement hello same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests tootrack events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="71a4f-110">En primer lugar, debe tooensure que hayan pasado por nuestro [tutorial de introducción](mobile-engagement-android-get-started.md) toointegrate Hola Android SDK de Mobile Engagement en la aplicación híbrida.</span><span class="sxs-lookup"><span data-stu-id="71a4f-110">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="71a4f-111">Una vez hecho esto, su `OnCreate` método tendrá un aspecto similar a Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="71a4f-111">Once you do that, your `OnCreate` method will look like hello following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="71a4f-112">Ahora, asegúrese de que la aplicación híbrida tiene una pantalla con el componente WebView.</span><span class="sxs-lookup"><span data-stu-id="71a4f-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="71a4f-113">Hello código para él será similar toohello siguiente que vamos a cargar un archivo HTML local **Sample.html** Hola Webview Hola `onCreate` método de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="71a4f-113">hello code for it will be similar toohello following where we are loading a local HTML file **Sample.html** in hello Webview in hello `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="71a4f-114">Ahora cree un archivo de puente denominado **WebAppInterface** que crea un contenedor a través de algunas normalmente utiliza métodos de Android SDK de Mobile Engagement mediante hello `@JavascriptInterface` enfoque descrito en hello [documentación de Android ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="71a4f-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using hello `@JavascriptInterface` approach described in hello [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate hello interface and set hello context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. <span data-ttu-id="71a4f-115">Una vez que hemos creado Hola por encima de archivo del puente, necesitamos tooensure que está asociado con nuestro Webview.</span><span class="sxs-lookup"><span data-stu-id="71a4f-115">Once we have created hello above bridge file, we need tooensure that it is associated with our Webview.</span></span> <span data-ttu-id="71a4f-116">Para este toohappen debe tooedit su `SetWebview` método de modo que TI aspecto Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="71a4f-116">For this toohappen, you need tooedit your `SetWebview` method so that it looks like hello following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="71a4f-117">Hola por encima del fragmento de código, se llama `addJavascriptInterface` tooassociate nuestro puente clase con nuestro Webview y también crea un identificador que se llama **EngagementJs** toocall métodos de Hola de archivo del puente Hola.</span><span class="sxs-lookup"><span data-stu-id="71a4f-117">In hello above snippet, we called `addJavascriptInterface` tooassociate our bridge class with our Webview and also created a handle called **EngagementJs** toocall hello methods from hello bridge file.</span></span> 
6. <span data-ttu-id="71a4f-118">Ahora crear Hola siguiente archivo denominado **Sample.html** en el proyecto en una carpeta denominada **activos** que se cargan en hello Webview y donde se llamará a métodos de Hola desde archivo de puente de hello.</span><span class="sxs-lookup"><span data-stu-id="71a4f-118">Now create hello following file called **Sample.html** in your project in a folder called **assets** which is loaded into hello Webview and where we will call hello methods from hello bridge file.</span></span>
   
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
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with hello Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. <span data-ttu-id="71a4f-119">Puntos siguientes de Hola de nota sobre el archivo HTML de hello anterior:</span><span class="sxs-lookup"><span data-stu-id="71a4f-119">Note hello following points about hello HTML file above:</span></span>
   
   * <span data-ttu-id="71a4f-120">Contiene un conjunto de cuadros de entrada donde se puede especificar toobe de datos que se usan como nombres para el evento, trabajo, Error, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="71a4f-120">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="71a4f-121">Al hacer clic en tooit de hello botón siguiente, se realiza una llamada toohello Javascript que finalmente llama métodos Hola de hello puente archivo toopass esta toohello llamada Android SDK de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="71a4f-121">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="71a4f-122">En algunos eventos de toohello estático información adicional, los trabajos e incluso errores toodemonstrate nos estamos etiquetado cómo esto puede realizarse.</span><span class="sxs-lookup"><span data-stu-id="71a4f-122">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="71a4f-123">Esta información adicional se envía como cadena de JSON que, si mira en hello `WebAppInterface` de archivos, que se analiza y se coloca en un Android `Bundle` y se pasa junto con eventos, trabajos, errores de envío.</span><span class="sxs-lookup"><span data-stu-id="71a4f-123">This extra info is sent as a JSON string which, if you look in hello `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="71a4f-124">Un trabajo de interacción móvil comienza con el nombre de Hola se especifica en el cuadro de entrada de hello, ejecutar durante 10 segundos y apagar.</span><span class="sxs-lookup"><span data-stu-id="71a4f-124">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="71a4f-125">Una etiqueta o Mobile Engagement appinfo se pasa con 'customer_name' como clave estática de Hola y el valor de Hola que ha especificado en la entrada de hello como valor de Hola para etiqueta Hola.</span><span class="sxs-lookup"><span data-stu-id="71a4f-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
8. <span data-ttu-id="71a4f-126">Aplicación hello ejecución y verá la siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="71a4f-126">Run hello app and you will see hello following.</span></span> <span data-ttu-id="71a4f-127">Proporcione un nombre para un evento de prueba como Hola después ahora y haga clic en **enviar** por debajo de él.</span><span class="sxs-lookup"><span data-stu-id="71a4f-127">Now provide some name for a test event like hello following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="71a4f-128">Ahora, si vaya toohello **Monitor** pestaña de la aplicación y busque **eventos -> detalles**, verá que este evento mostrarán junto con hello estático app-info que te enviamos.</span><span class="sxs-lookup"><span data-stu-id="71a4f-128">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
