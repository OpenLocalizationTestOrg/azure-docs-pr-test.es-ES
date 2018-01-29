---
title: "Diagnóstico de errores y excepciones en aplicaciones web con Azure Application Insights | Microsoft Docs"
description: "Capture las excepciones de las aplicaciones ASP.NET junto con la telemetría de solicitudes."
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 09/19/2017
ms.author: mbullwin
ms.openlocfilehash: d6a0b945bad36842142d16a4840c9c3d69e1564e
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2018
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a>Diagnóstico de excepciones en aplicaciones web con Application Insights
Las excepciones en la aplicación web en directo se notifican mediante [Application Insights](app-insights-overview.md). Puede correlacionar las solicitudes con error con excepciones y otros eventos en el cliente y en el servidor, de modo que pueda diagnosticar rápidamente las causas.

## <a name="set-up-exception-reporting"></a>Configuración de informes de excepciones
* Para que se notifiquen excepciones desde su aplicación de servidor:
  * Instale el [SDK de Application Insights](app-insights-asp-net.md) en su código de aplicación.
  * Servidores web de IIS: ejecute el [agente de Application Insights](app-insights-monitor-performance-live-website-now.md).
  * Aplicaciones web de Azure: agregue la [extensión de Application Insights](app-insights-azure-web-apps.md).
  * Aplicaciones web de Java: instale el [agente de Java](app-insights-java-agent.md).
* Instale el [fragmento de código de JavaScript](app-insights-javascript.md) en las páginas web para capturar las excepciones del explorador.
* En algunos marcos de aplicaciones o con algunas opciones de configuración, debe realizar algunos pasos adicionales para capturar más excepciones:
  * [Formularios web](#web-forms)
  * [MVC](#mvc)
  * [API web 1.*](#web-api-1x)
  * [API web 2.*](#web-api-2x)
  * [WCF](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a>Diagnóstico de excepciones mediante Visual Studio
Abra la solución de aplicación en Visual Studio para ayudar con la depuración.

Ejecute la aplicación, bien en el servidor o en el equipo de desarrollo mediante F5.

Abra la ventana Búsqueda de Application Insights en Visual Studio y configúrela para mostrar los eventos de la aplicación. Durante la depuración, puede hacer esto haciendo clic simplemente en el botón de Application Insights.

![Haga clic con el botón derecho en el proyecto y seleccione Application Insights, Abrir.](./media/app-insights-asp-net-exceptions/34.png)

Observe que puede filtrar el informe para mostrar solo excepciones.

*¿No se muestra ninguna excepción? Consulte [Captura de excepciones](#exceptions).*

Haga clic en un informe de excepciones para mostrar su seguimiento de la pila.
Haga clic en una referencia de línea en el seguimiento de la pila para abrir el archivo de código pertinente.  

En el código, tenga en cuenta que CodeLens muestra datos de las excepciones:

![Notificación de CodeLens de excepciones.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-the-azure-portal"></a>Diagnóstico de errores mediante el Portal de Azure
Application Insights incluye una experiencia APM seleccionada para ayudar a diagnosticar errores en las aplicaciones supervisadas. Para empezar, haga clic en la opción Errores del menú de recursos de Application Insights situado en la sección de investigación. Debería ver una vista de pantalla completa que muestra las tendencias de índice de errores de sus solicitudes: cuántas de ellas generan errores y cuántos usuarios se ven afectados. A la derecha, verá algunas de las distribuciones más útiles específicas de la operación con error seleccionada, incluidos los 3 códigos de respuesta principales, los 3 tipos principales de excepción y los 3 tipos principales de dependencia con error. 

![Vista de evaluación de prioridades de errores (pestaña Operaciones)](./media/app-insights-asp-net-exceptions/FailuresTriageView.png)

En un solo clic, a continuación, puede revisar ejemplos representativos de cada uno de estos subconjuntos de operaciones. En concreto, para diagnosticar excepciones, puede hacer clic en el recuento de una excepción determinada para que se muestre una hoja de detalles de excepciones como esta:

![Hoja de detalles de excepciones](./media/app-insights-asp-net-exceptions/ExceptionDetailsBlade.png)

**Como alternativa,** en lugar de observar las excepciones de una operación específica con errores, puede empezar desde la vista general de excepciones y cambiar a la pestaña Excepciones:

![Vista de evaluación de prioridades de errores (pestaña Excepciones)](./media/app-insights-asp-net-exceptions/FailuresTriageView_Exceptions.png)

Aquí puede ver todas las excepciones que se recopilan para la aplicación supervisada.

*¿No se muestra ninguna excepción? Consulte [Captura de excepciones](#exceptions).*


## <a name="custom-tracing-and-log-data"></a>Personalización del seguimiento y del registro de datos
Para obtener datos de diagnóstico específicos de su aplicación, puede insertar código para enviar sus propios datos de telemetría. Esto aparece en la búsqueda de diagnóstico junto con la solicitud, vista de página y otros datos que se recopilan automáticamente.

Tiene varias opciones:

* [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) normalmente se usa para supervisar patrones de uso, pero los datos que envía también aparecen en Eventos personalizados en la búsqueda de diagnósticos. Los eventos tienen nombre y pueden llevar propiedades de cadena y métricas numéricas en las que puede [filtrar las búsquedas de diagnósticos](app-insights-diagnostic-search.md).
* [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) le permite enviar datos más grandes, como la información de POST.
* [TrackException()](#exceptions) envía seguimientos de la pila. [Más información sobre excepciones](#exceptions).
* Si ya usa un marco de registro como Log4Net o NLog, puede [capturar aquellos registros](app-insights-asp-net-trace-logs.md) y verlos en la búsqueda de diagnósticos junto con datos de solicitud y excepción.

Para ver estos eventos, abra [Buscar](app-insights-diagnostic-search.md), abra Filtrar y luego elija Evento personalizado, Seguimiento o Excepción.

![Obtener detalles](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> Si la aplicación genera mucha telemetría, el módulo de muestreo adaptable reducirá automáticamente el volumen que se envía al portal mediante el envío de únicamente una fracción representativa de eventos. Los eventos que forman parte de la misma operación se seleccionarán o se anulará su selección como grupo, por lo que puede navegar entre los eventos relacionados. [Más información sobre el muestreo.](app-insights-sampling.md)
>
>

### <a name="how-to-see-request-post-data"></a>Visualización de los datos de solicitud POST
Los detalles de la solicitud no incluyen los datos enviados a la aplicación en una llamada a POST. Para que se notifiquen estos datos:

* [Instale el SDK](app-insights-asp-net.md) en su proyecto de aplicación.
* Inserte código en la aplicación para llamar a [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace). Envíe los datos de POST en el parámetro de mensaje. Hay un límite en cuanto al tamaño permitido, así que debe intentar enviar únicamente los datos fundamentales.
* Cuando investigue una solicitud con error, busque los seguimientos asociados.  

![Obtener detalles](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a> Captura de excepciones y datos de diagnóstico relacionados
En primer lugar, no verá en el portal todas las excepciones que provocan errores en su aplicación. Verá las excepciones del explorador (si usa el [SDK de JavaScript](app-insights-javascript.md) en sus páginas web). Pero la mayoría de las excepciones de servidor las detecta IIS y debe escribir algo de código para verlas.

Puede:

* **Registrar excepciones explícitamente** insertando código en los controladores de excepciones para notificar las excepciones.
* **Capturar excepciones automáticamente** configurando su marco de ASP.NET. Las adiciones necesarias son diferentes para los distintos tipos de marco.

## <a name="reporting-exceptions-explicitly"></a>Notificación de excepciones explícitamente
La manera más sencilla consiste en insertar una llamada a TrackException() en un controlador de excepciones.

JavaScript

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

C#

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send the exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

VB

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send the exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

Los parámetros de las propiedades y las medidas son opcionales, pero son útiles para [filtrar y agregar información](app-insights-diagnostic-search.md) adicional. Por ejemplo, si tiene una aplicación que se puede ejecutar varios juegos, podría buscar todos los informes de excepción relacionados con un juego en particular. Puede agregar tantos elementos como desee para cada diccionario.

## <a name="browser-exceptions"></a>Excepciones de explorador
Se notifican la mayoría de las excepciones de explorador.

Si la página web incluye archivos de script de redes de entrega de contenido o de otros dominios, asegúrese de que la etiqueta de script tenga el atributo ```crossorigin="anonymous"```, y que el servidor envíe [encabezados CORS](http://enable-cors.org/). Esto le permitirá obtener un seguimiento de pila y los detalles de las excepciones no controladas de JavaScript de estos recursos.

## <a name="web-forms"></a>Formularios web
Para los formularios web, el módulo HTTP podrá recopilar las excepciones cuando no haya ningún redireccionamiento configurado con CustomErrors.

Pero si tiene redireccionamientos activos, agregue las siguientes líneas a la función Application_Error en Global.asax.cs. (Agregue un archivo Global.asax si aún no tiene uno.)

*C#*

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a>MVC
Si la configuración de [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) es `Off`, entonces habrá excepciones disponibles para que las recopile el [módulo HTTP](https://msdn.microsoft.com/library/ms178468.aspx). Sin embargo, si es `RemoteOnly` (valor predeterminado), o `On`, la excepción se desactivará y no estará disponible para que Application Insights la recopile automáticamente. Para corregir este problema, invalide la [clase System.Web.Mvc.HandleErrorAttribute](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx) y aplique la clase invalidada como se muestra a continuación para las diferentes versiones de MVC ([origen de github](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report the exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a>MVC 2
Sustituya el atributo HandleError por el nuevo atributo en los controladores.

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[Ejemplo](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a>MVC 3
Registrar `AiHandleErrorAttribute` como filtro global de Global.asax.cs:

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[Ejemplo](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a>MVC 4, MVC5
Registrar AiHandleErrorAttribute como filtro global en FilterConfig.cs:

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with the override to track unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[Ejemplo](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a>Web API 1.x
Invalidar System.Web.Http.Filters.ExceptionFilterAttribute:

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

Podría agregar este atributo invalidado a controladores específicos o agregarlo a la configuración de filtros globales en la clase WebApiConfig:

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[Ejemplo](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

Hay un número de casos que los filtros de excepciones no pueden procesar. Por ejemplo: 

* Excepciones iniciadas por constructores del controlador.
* Excepciones iniciadas por controladores de mensajes.
* Excepciones iniciadas durante el enrutamiento.
* Excepciones iniciadas durante la serialización del contenido de respuesta.

## <a name="web-api-2x"></a>Web API 2.x
Agregue una implementación de IExceptionLogger:

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

Agregue lo siguiente a los servicios en WebApiConfig:

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  }

[Ejemplo](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

Como alternativa, puede:

1. Sustituir el único ExceptionHandler por una implementación personalizada de IExceptionHandler. Solo se llama a este controlador de excepciones cuando el marco es aún capaz de seleccionar el mensaje de respuesta que se enviará (no cuando se anula la conexión, por ejemplo)
2. Los filtros de excepciones (como se describe en la sección sobre controladores de Web API 1.x anteriores) no se llaman en todos los casos.

## <a name="wcf"></a>WCF
Agregue una clase que extienda el atributo y que implemente IErrorHandler y IServiceBehavior.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

Agregue el atributo a las implementaciones de servicio:

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[Ejemplo](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a>Contadores de rendimiento de excepciones
Si tiene [instalado el agente de Application Insights](app-insights-monitor-performance-live-website-now.md) en el servidor, puede obtener un gráfico de la tasa de excepciones, medida por .NET. Esto incluye las excepciones de .NET, tanto controladas como no controladas.

Abra una hoja del Explorador de métricas, agregue un nuevo gráfico y seleccione **Tasa de excepciones**, que aparece debajo de Contadores de rendimiento.

.NET framework calcula la tasa contando el número de excepciones producidas en un intervalo y dividiéndolo por la duración del intervalo de tiempo.

Esto es diferente del recuento de "Excepciones" calculado por el portal de Application Insights contando los informes de TrackException. Los intervalos de muestreo son diferentes y el SDK no envía informes de TrackException para todas las excepciones, controladas y no controladas.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a>pasos siguientes
* [Supervisar REST, SQL y otras llamadas a las dependencias](app-insights-asp-net-dependencies.md)
* [Supervisar los tiempos de carga de página, las excepciones del explorador y las llamadas AJAX](app-insights-javascript.md)
* [Supervisar los contadores de rendimiento](app-insights-performance-counters.md)
