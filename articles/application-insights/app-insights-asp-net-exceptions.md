---
title: aaaDiagnose errores y excepciones en aplicaciones con Azure Application Insights de web | Documentos de Microsoft
description: "Capture las excepciones de las aplicaciones ASP.NET junto con la telemetría de solicitudes."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a>Diagnóstico de excepciones en aplicaciones web con Application Insights
Las excepciones en la aplicación web en directo se notifican mediante [Application Insights](app-insights-overview.md). Puede correlacionar las solicitudes erróneas con excepciones y otros eventos en el cliente de Hola y el servidor, por lo que puede diagnosticar rápidamente Hola causas.

## <a name="set-up-exception-reporting"></a>Configuración de informes de excepciones
* excepciones de toohave desde la aplicación de servidor:
  * Instale el [SDK de Application Insights](app-insights-asp-net.md) en su código de aplicación.
  * Servidores web de IIS: ejecute el [agente de Application Insights](app-insights-monitor-performance-live-website-now.md).
  * Aplicaciones web de Azure: agregar hello [extensión de visión de la aplicación](app-insights-azure-web-apps.md)
  * Aplicaciones web de Java: Hola Install [agente Java](app-insights-java-agent.md)
* Instalar hello [fragmento de código de JavaScript](app-insights-javascript.md) en sus excepciones de explorador toocatch de páginas web.
* En algunos marcos de aplicaciones o con algunas opciones de configuración, deberá tootake algunos pasos adicionales toocatch más excepciones:
  * [Formularios web](#web-forms)
  * [MVC](#mvc)
  * [API web 1.*](#web-api-1)
  * [API web 2.*](#web-api-2)
  * [WCF](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a>Diagnóstico de excepciones mediante Visual Studio
Abra la solución de aplicación de hello en toohelp de Visual Studio con la depuración.

Ejecute la aplicación hello, ya sea en el servidor o en el equipo de desarrollo utilizando F5.

Abra la ventana de búsqueda de visión de la aplicación hello en Visual Studio y establézcalo toodisplay eventos de la aplicación. Durante la depuración, puede hacerlo haciendo clic en el botón de Application Insights Hola.

![Haga clic en proyecto de Hola y elija Application Insights, abrir.](./media/app-insights-asp-net-exceptions/34.png)

Tenga en cuenta que se pueden filtrar solo las excepciones Hola informe tooshow.

*¿No se muestra ninguna excepción? Consulte [Captura de excepciones](#exceptions).*

Haga clic en un tooshow de informes de excepción su seguimiento de la pila.
Haga clic en una referencia de la línea de seguimiento de la pila de hello, archivo de código relevante de hello tooopen.  

En el código de hello, tenga en cuenta que CodeLens muestra datos sobre las excepciones de hello:

![Notificación de CodeLens de excepciones.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a>Diagnosticar errores mediante Hola portal de Azure
De información general de Application Insights hello de la aplicación, iconos de errores de hello muestran los gráficos de excepciones y errores de solicitud HTTP, junto con una lista de hello solicitar direcciones URL que dar lugar a errores más frecuentes de Hola.

![Selección de Configuración, Errores](./media/app-insights-asp-net-exceptions/012-start.png)

Haga clic en a través de uno de hello no se pudo tipos de excepciones en las repeticiones de hello lista tooget tooindividual de excepción de hello, donde puede ver los detalles de Hola y seguimiento de pila:

![Seleccione una instancia de una solicitud con error y en detalles de la excepción, obtener tooinstances de excepción de Hola.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

**O bien,** puede iniciar desde la lista de Hola de solicitudes y buscar excepciones relacionadas tooit.

*¿No se muestra ninguna excepción? Consulte [Captura de excepciones](#exceptions).*


## <a name="custom-tracing-and-log-data"></a>Personalización del seguimiento y del registro de datos
aplicación de tooyour específico de datos de diagnóstico de tooget, puede insertar código toosend sus propios datos de telemetría. Esto se muestra en la búsqueda de diagnóstico junto con la solicitud de hello, vista de página y otros datos recopilados automáticamente.

Tiene varias opciones:

* [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) normalmente se usa para supervisar patrones de uso, pero Hola datos envía también aparecen en eventos personalizados en la búsqueda de diagnóstico. Los eventos tienen nombre y pueden llevar propiedades de cadena y métricas numéricas en las que puede [filtrar las búsquedas de diagnósticos](app-insights-diagnostic-search.md).
* [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) le permite enviar datos más grandes, como la información de POST.
* [TrackException()](#exceptions) envía seguimientos de la pila. [Más información sobre excepciones](#exceptions).
* Si ya usa un marco de registro como Log4Net o NLog, puede [capturar aquellos registros](app-insights-asp-net-trace-logs.md) y verlos en la búsqueda de diagnósticos junto con datos de solicitud y excepción.

estos eventos, abra a toosee [búsqueda](app-insights-diagnostic-search.md), Abrir filtro y, a continuación, elija Custom Event, seguimiento o excepción.

![Obtener detalles](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> Si la aplicación genera una gran cantidad de telemetría, módulo de muestreo adaptativo de Hola reducirá automáticamente volumen Hola que se envía toohello portal enviando sólo una fracción representativa de eventos. Eventos que forman parte de hello misma operación se selecciona o anula la selección como un grupo, por lo que puede desplazarse entre los eventos relacionados. [Más información sobre el muestreo.](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a>¿Cómo toosee solicitar datos POST
Detalles de la solicitud no incluyen datos de hello enviados tooyour aplicación en una llamada a POST. toohave notifican estos datos:

* [Instalar SDK de hello](app-insights-asp-net.md) en el proyecto de aplicación.
* Inserte código en su aplicación toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace). Enviar datos POST de hello en el parámetro de mensaje de Hola. Hay un toohello permitida limitar el tamaño, por lo que debe intentar datos esenciales de toosend simplemente Hola.
* Cuando se investiga un solicitudes con error, encuentre ningún rastro de hello asociado.  

![Obtener detalles](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a> Captura de excepciones y datos de diagnóstico relacionados
En primer lugar, no se mostrará en el portal de hello todas las excepciones de Hola que dar lugar a errores en la aplicación. Podrá ver las excepciones de explorador (si usa hello [SDK de JavaScript](app-insights-javascript.md) en las páginas web). Pero la mayoría de las excepciones de servidor capturada por IIS y tiene un poco de código toosee toowrite ellos.

Puede:

* **Registrar excepciones explícitamente** mediante la inserción de código en las excepciones Hola de tooreport de controladores de excepción.
* **Capturar excepciones automáticamente** configurando su marco de ASP.NET. adiciones necesarias Hola son diferentes para distintos tipos de framework.

## <a name="reporting-exceptions-explicitly"></a>Notificación de excepciones explícitamente
Hello forma más sencilla es tooinsert un tooTrackException() de llamada en un controlador de excepciones.

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

       // Send hello exception telemetry:
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

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

Hello las medidas y las propiedades de parámetros son opcionales, pero son útiles para [filtrar y agregar](app-insights-diagnostic-search.md) información adicional. Por ejemplo, si tiene una aplicación que se puede ejecutar varios juegos, encontró todos los Hola excepción informes relacionados tooa juego determinado. Puede agregar tantos elementos como como diccionario tooeach.

## <a name="browser-exceptions"></a>Excepciones de explorador
Se notifican la mayoría de las excepciones de explorador.

Si la página web incluye archivos de script de otros dominios o redes de entrega de contenido, asegúrese de que la etiqueta de script tiene el atributo de hello ```crossorigin="anonymous"```, y envía ese servidor hello [encabezados CORS](http://enable-cors.org/). Esto le permitirá tooget un seguimiento de pila y los detalles de las excepciones no controladas de JavaScript de estos recursos.

## <a name="web-forms"></a>Formularios web
Para formularios web forms, Hola módulo HTTP será toocollect capaz de excepciones de hello cuando no hay ningún redirecciones configuradas con CustomErrors.

Pero si tiene activas redirecciones, agregar Hola siguen líneas toohello Application_Error función en Global.asax.cs. (Agregue un archivo Global.asax si aún no tiene uno.)

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
Si hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuración es `Off`, a continuación, las excepciones estarán disponibles para hello [módulo HTTP](https://msdn.microsoft.com/library/ms178468.aspx) toocollect. Sin embargo, si es `RemoteOnly` (valor predeterminado), o `On`, a continuación, se borrará la excepción de hello y no está disponible para Application Insights tooautomatically recopilar. Puede solucionar esto mediante la invalidación hello [System.Web.Mvc.HandleErrorAttribute clase](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)y aplicar clase hello se reemplaza, tal como se muestra de Hola diferentes MVC las versiones siguientes ([github origen](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):

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
                //If customError is Off, then AI HTTPModule will report hello exception
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
Reemplace el atributo de HandleError de hello con el nuevo atributo en los controladores.

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
        // Default replaced with hello override tootrack unhandled exceptions
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

Puede agregar este atributo reemplazado los controladores de toospecific o agregar configuración de filtros globales toohello en la clase WebApiConfig de hello:

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

Hay una serie de casos que no pueden controlar los filtros de excepción Hola. Por ejemplo:

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

Agregue este servicios toohello en WebApiConfig:

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

1. Reemplace Hola solo ExceptionHandler con una implementación personalizada de IExceptionHandler. Esto solo se llama cuando el marco de trabajo de hello es todavía puede toochoose qué respuesta mensaje toosend (no cuando Hola conexión anulada por ejemplo)
2. Filtros de excepción (como se describe en la sección de hello en los controladores de API Web 1.x anteriores) - no se llama en todos los casos.

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

Agregue las implementaciones del servicio Hola atributo toohello:

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[Ejemplo](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a>Contadores de rendimiento de excepciones
Si tiene [instalado el agente de visión de la aplicación hello](app-insights-monitor-performance-live-website-now.md) en el servidor, puede obtener un gráfico de velocidad de excepciones de hello, medido por. NET. Esto incluye las excepciones de .NET, tanto controladas como no controladas.

Abra una hoja del Explorador de métricas, agregue un nuevo gráfico y seleccione **Tasa de excepciones**, que aparece debajo de Contadores de rendimiento.

.NET framework de Hello calcula la tasa de Hola Hola recuento de excepciones en un intervalo y dividiendo por longitud Hola de intervalo de saludo.

Tenga en cuenta que debe ser diferente del número de excepciones' hello' calculado por el portal de Application Insights Hola contando TrackException informes. intervalos de muestreo de Hello son diferentes y Hola SDK no enviar informes de TrackException para todas las excepciones controladas y sin controlar.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a>Pasos siguientes
* [Supervisar REST, SQL y otros toodependencies de llamadas](app-insights-asp-net-dependencies.md)
* [Supervisar los tiempos de carga de página, las excepciones del explorador y las llamadas AJAX](app-insights-javascript.md)
* [Supervisar los contadores de rendimiento](app-insights-performance-counters.md)
