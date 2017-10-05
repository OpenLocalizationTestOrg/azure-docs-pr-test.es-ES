---
title: Puente de WebView en Android con el SDK de Android para Mobile Engagement nativo
description: "Describe cómo crear un puente entre un WebView que ejecuta Javascript y el SDK de Android para Mobile Engagement nativo."
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
ms.openlocfilehash: f4fc7b3c81747ec80974a99084eeb1acc311f11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="231cf-103">Puente de WebView en Android con el SDK de Android para Mobile Engagement nativo</span><span class="sxs-lookup"><span data-stu-id="231cf-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="231cf-104">Puente de Android</span><span class="sxs-lookup"><span data-stu-id="231cf-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="231cf-105">Puente de iOS</span><span class="sxs-lookup"><span data-stu-id="231cf-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="231cf-106">Algunas aplicaciones móviles están diseñadas como una aplicación híbrida en la que la propia aplicación se desarrolla mediante tecnología nativa de Android, pero algunas o incluso todas las pantallas se representan en el componente WebView en Android.</span><span class="sxs-lookup"><span data-stu-id="231cf-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native Android development but some or even all of the screens are rendered within an Android WebView.</span></span> <span data-ttu-id="231cf-107">Puede seguir utilizando el SDK de Android para Mobile Engagement en estas aplicaciones: en este tutorial se describe cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="231cf-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how to go about doing this.</span></span> <span data-ttu-id="231cf-108">El código de ejemplo siguiente se basa en la documentación de Android que puede encontrar [aquí](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="231cf-108">The sample code below is based on the Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="231cf-109">Se describe cómo podría usarse este enfoque documentado a fin de implementar lo mismo para los métodos más utilizados para el SDK de Android para Mobile Engagement, como que Webview pueda también iniciar solicitudes de seguimiento de eventos, trabajos, errores e información de la aplicación desde una aplicación híbrida al tiempo que se canalizan a través de nuestro SDK de Android.</span><span class="sxs-lookup"><span data-stu-id="231cf-109">It describes how this documented approach could be used to implement the same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests to track events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="231cf-110">En primer lugar, debe asegurarse de que ha completado nuestro [tutorial de introducción](mobile-engagement-android-get-started.md) para integrar el SDK de Android para Mobile Engagement en la aplicación híbrida.</span><span class="sxs-lookup"><span data-stu-id="231cf-110">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) to integrate the Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="231cf-111">Una vez hecho esto, su método `OnCreate` tendrá un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="231cf-111">Once you do that, your `OnCreate` method will look like the following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="231cf-112">Ahora, asegúrese de que la aplicación híbrida tiene una pantalla con el componente WebView.</span><span class="sxs-lookup"><span data-stu-id="231cf-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="231cf-113">El código para ello será similar a la siguiente, donde vamos a cargar un archivo HTML local **Sample.html** en Webview en el método `onCreate` de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="231cf-113">The code for it will be similar to the following where we are loading a local HTML file **Sample.html** in the Webview in the `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="231cf-114">Ahora cree un archivo puente denominado **WebAppInterface**, que crea un contenedor sobre algunos métodos de SDK de Android para Mobile Engagement utilizados frecuentemente mediante el enfoque `@JavascriptInterface` descrito en la [documentación de Android](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="231cf-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using the `@JavascriptInterface` approach described in the [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate the interface and set the context */
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
4. <span data-ttu-id="231cf-115">Una vez creado el archivo puente anterior, es necesario asegurarse de que está asociado a nuestro componente Webview.</span><span class="sxs-lookup"><span data-stu-id="231cf-115">Once we have created the above bridge file, we need to ensure that it is associated with our Webview.</span></span> <span data-ttu-id="231cf-116">Para ello, deberá modificar su método `SetWebview` para que quede como sigue:</span><span class="sxs-lookup"><span data-stu-id="231cf-116">For this to happen, you need to edit your `SetWebview` method so that it looks like the following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="231cf-117">En el fragmento de código anterior, se llamó a `addJavascriptInterface` para asociar nuestra clase de puente con nuestro componente Webview, y también se creó un identificador denominado **EngagementJs** para llamar a los métodos desde el archivo puente.</span><span class="sxs-lookup"><span data-stu-id="231cf-117">In the above snippet, we called `addJavascriptInterface` to associate our bridge class with our Webview and also created a handle called **EngagementJs** to call the methods from the bridge file.</span></span> 
6. <span data-ttu-id="231cf-118">Ahora, cree el siguiente archivo denominado **Sample.html** en el proyecto en una carpeta denominada **assets** que se carga en Webview y donde se llamará a los métodos desde el archivo puente.</span><span class="sxs-lookup"><span data-stu-id="231cf-118">Now create the following file called **Sample.html** in your project in a folder called **assets** which is loaded into the Webview and where we will call the methods from the bridge file.</span></span>
   
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
                            // Example of how extras info can be passed with the Engagement logs
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
7. <span data-ttu-id="231cf-119">Tenga en cuenta los siguientes aspectos sobre el archivo HTML anterior:</span><span class="sxs-lookup"><span data-stu-id="231cf-119">Note the following points about the HTML file above:</span></span>
   
   * <span data-ttu-id="231cf-120">Contiene un conjunto de cuadros de entrada donde puede proporcionar los datos que se utilizarán como nombres para los valores de Event, Job, Error, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="231cf-120">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="231cf-121">Al hacer clic en el botón situado junto a él, se realiza una llamada a Javascript, que finalmente llama a los métodos desde el archivo puente para pasar esta llamada al SDK de Android para Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="231cf-121">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="231cf-122">Estamos añadiendo algo de información adicional estática a los eventos, trabajos e incluso errores para demostrar cómo podría ser este proceso.</span><span class="sxs-lookup"><span data-stu-id="231cf-122">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="231cf-123">Esta información adicional se envía como una cadena JSON que, si observa el archivo `WebAppInterface`, se analiza y se coloca en un dispositivo Android `Bundle` y se pasa junto con los eventos, los trabajos y los errores que se envían.</span><span class="sxs-lookup"><span data-stu-id="231cf-123">This extra info is sent as a JSON string which, if you look in the `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="231cf-124">Un trabajo de Mobile Engagement comienza con el nombre que especifique en el cuadro de entrada, se ejecuta durante 10 segundos y luego se apaga.</span><span class="sxs-lookup"><span data-stu-id="231cf-124">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="231cf-125">Se pasa una información de aplicación o una etiqueta de Mobile Engagement con 'customer_name' como clave estática y el valor que especificó en la entrada como valor para la etiqueta.</span><span class="sxs-lookup"><span data-stu-id="231cf-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
8. <span data-ttu-id="231cf-126">Ejecute la aplicación y verá lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="231cf-126">Run the app and you will see the following.</span></span> <span data-ttu-id="231cf-127">Ahora, proporcione un nombre para un evento de prueba similar al siguiente y haga clic en el botón **Send** (Enviar) que se encuentra debajo.</span><span class="sxs-lookup"><span data-stu-id="231cf-127">Now provide some name for a test event like the following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="231cf-128">Ahora, si va a la pestaña **Monitor** (Supervisar) de la aplicación y busca **Events -> Details** (Eventos -> Detalles), verá que este evento se muestra con app-info estática que se envía.</span><span class="sxs-lookup"><span data-stu-id="231cf-128">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
