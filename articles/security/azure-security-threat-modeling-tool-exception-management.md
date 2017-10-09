---
title: "aaaException de administración - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft"
description: mitigaciones en busca de amenazas que se exponen en hello herramienta de modelado de amenazas
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="6b10d-103">Marco de seguridad: Administración de excepciones | Mitigaciones</span><span class="sxs-lookup"><span data-stu-id="6b10d-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="6b10d-104">Producto o servicio</span><span class="sxs-lookup"><span data-stu-id="6b10d-104">Product/Service</span></span> | <span data-ttu-id="6b10d-105">Artículo</span><span class="sxs-lookup"><span data-stu-id="6b10d-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="6b10d-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="6b10d-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="6b10d-107">WCF: no incluya el nodo serviceDebug en el archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="6b10d-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="6b10d-108">WCF: no incluya el nodo serviceMetadata en el archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="6b10d-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="6b10d-109">**API web**</span><span class="sxs-lookup"><span data-stu-id="6b10d-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="6b10d-110">Asegúrese de que se realiza un control adecuado de las excepciones en ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="6b10d-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="6b10d-111">**Aplicación web**</span><span class="sxs-lookup"><span data-stu-id="6b10d-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="6b10d-112">No exponga detalles de seguridad en los mensajes de error</span><span class="sxs-lookup"><span data-stu-id="6b10d-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="6b10d-113">Implemente una página de control de errores predeterminado</span><span class="sxs-lookup"><span data-stu-id="6b10d-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="6b10d-114">Establecer el método de implementación tooRetail en IIS</span><span class="sxs-lookup"><span data-stu-id="6b10d-114">Set Deployment Method tooRetail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="6b10d-115">Las excepciones deben generar un error con seguridad</span><span class="sxs-lookup"><span data-stu-id="6b10d-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="6b10d-116"><a id="servicedebug"></a>WCF: no incluya el nodo serviceDebug en el archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="6b10d-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="6b10d-117">Título</span><span class="sxs-lookup"><span data-stu-id="6b10d-117">Title</span></span>                   | <span data-ttu-id="6b10d-118">Detalles</span><span class="sxs-lookup"><span data-stu-id="6b10d-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="6b10d-119">**Componente**</span><span class="sxs-lookup"><span data-stu-id="6b10d-119">**Component**</span></span>               | <span data-ttu-id="6b10d-120">WCF</span><span class="sxs-lookup"><span data-stu-id="6b10d-120">WCF</span></span> | 
| <span data-ttu-id="6b10d-121">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="6b10d-121">**SDL Phase**</span></span>               | <span data-ttu-id="6b10d-122">Compilación</span><span class="sxs-lookup"><span data-stu-id="6b10d-122">Build</span></span> |  
| <span data-ttu-id="6b10d-123">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="6b10d-123">**Applicable Technologies**</span></span> | <span data-ttu-id="6b10d-124">Genérico, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="6b10d-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="6b10d-125">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-125">**Attributes**</span></span>              | <span data-ttu-id="6b10d-126">N/D</span><span class="sxs-lookup"><span data-stu-id="6b10d-126">N/A</span></span>  |
| <span data-ttu-id="6b10d-127">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="6b10d-127">**References**</span></span>              | <span data-ttu-id="6b10d-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="6b10d-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="6b10d-129">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-129">**Steps**</span></span> | <span data-ttu-id="6b10d-130">Servicios de Windows Communication Framework (WCF) pueden ser configurado tooexpose información de depuración.</span><span class="sxs-lookup"><span data-stu-id="6b10d-130">Windows Communication Framework (WCF) services can be configured tooexpose debugging information.</span></span> <span data-ttu-id="6b10d-131">La información de depuración no debe usarse en entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="6b10d-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="6b10d-132">Hola `<serviceDebug>` etiqueta define si está habilitada la característica de información de depuración de Hola para un servicio WCF.</span><span class="sxs-lookup"><span data-stu-id="6b10d-132">hello `<serviceDebug>` tag defines whether hello debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="6b10d-133">Si Hola atributo includeExceptionDetailInFaults se establece tootrue, se devolverá información de excepción de aplicación hello tooclients.</span><span class="sxs-lookup"><span data-stu-id="6b10d-133">If hello attribute includeExceptionDetailInFaults is set tootrue, exception information from hello application will be returned tooclients.</span></span> <span data-ttu-id="6b10d-134">Los atacantes pueden aprovechar la información adicional de hello obtienen de la depuración de salida toomount los ataques dirigidos en framework hello, base de datos u otros recursos usados por la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6b10d-134">Attackers can leverage hello additional information they gain from debugging output toomount attacks targeted on hello framework, database, or other resources used by hello application.</span></span> |

### <a name="example"></a><span data-ttu-id="6b10d-135">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6b10d-135">Example</span></span>
<span data-ttu-id="6b10d-136">archivo de configuración siguiente Hello incluye hello `<serviceDebug>` etiqueta:</span><span class="sxs-lookup"><span data-stu-id="6b10d-136">hello following configuration file includes hello `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="6b10d-137">Deshabilitar la información de depuración en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b10d-137">Disable debugging information in hello service.</span></span> <span data-ttu-id="6b10d-138">Esto puede realizarse mediante la eliminación de hello `<serviceDebug>` etiqueta desde el archivo de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b10d-138">This can be accomplished by removing hello `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="6b10d-139"><a id="servicemetadata"></a>WCF: no incluya el nodo serviceMetadata en el archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="6b10d-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="6b10d-140">Título</span><span class="sxs-lookup"><span data-stu-id="6b10d-140">Title</span></span>                   | <span data-ttu-id="6b10d-141">Detalles</span><span class="sxs-lookup"><span data-stu-id="6b10d-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="6b10d-142">**Componente**</span><span class="sxs-lookup"><span data-stu-id="6b10d-142">**Component**</span></span>               | <span data-ttu-id="6b10d-143">WCF</span><span class="sxs-lookup"><span data-stu-id="6b10d-143">WCF</span></span> | 
| <span data-ttu-id="6b10d-144">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="6b10d-144">**SDL Phase**</span></span>               | <span data-ttu-id="6b10d-145">Compilación</span><span class="sxs-lookup"><span data-stu-id="6b10d-145">Build</span></span> |  
| <span data-ttu-id="6b10d-146">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="6b10d-146">**Applicable Technologies**</span></span> | <span data-ttu-id="6b10d-147">Genérico</span><span class="sxs-lookup"><span data-stu-id="6b10d-147">Generic</span></span> |
| <span data-ttu-id="6b10d-148">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-148">**Attributes**</span></span>              | <span data-ttu-id="6b10d-149">Genérico, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="6b10d-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="6b10d-150">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="6b10d-150">**References**</span></span>              | <span data-ttu-id="6b10d-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="6b10d-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="6b10d-152">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-152">**Steps**</span></span> | <span data-ttu-id="6b10d-153">Exponer públicamente información acerca de un servicio puede proporcionar a los atacantes valiosa información sobre cómo pueden sacar provecho de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b10d-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit hello service.</span></span> <span data-ttu-id="6b10d-154">Hola `<serviceMetadata>` etiqueta habilita la característica de publicación de metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b10d-154">hello `<serviceMetadata>` tag enables hello metadata publishing feature.</span></span> <span data-ttu-id="6b10d-155">Los metadatos del servicio pueden contener información confidencial que no debe estar accesible públicamente.</span><span class="sxs-lookup"><span data-stu-id="6b10d-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="6b10d-156">Como mínimo, permitir solo los usuarios de confianza tooaccess Hola metadatos y asegúrese de que no se expone información innecesaria.</span><span class="sxs-lookup"><span data-stu-id="6b10d-156">At a minimum, only allow trusted users tooaccess hello metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="6b10d-157">Mejor aún, deshabilitar completamente Hola capacidad toopublish metadatos.</span><span class="sxs-lookup"><span data-stu-id="6b10d-157">Better yet, entirely disable hello ability toopublish metadata.</span></span> <span data-ttu-id="6b10d-158">Una configuración segura de WCF no contendrá hello `<serviceMetadata>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="6b10d-158">A safe WCF configuration will not contain hello `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="6b10d-159"><a id="exception"></a>Asegúrese de que se realiza un tratamiento adecuado de las excepciones en ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="6b10d-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="6b10d-160">Título</span><span class="sxs-lookup"><span data-stu-id="6b10d-160">Title</span></span>                   | <span data-ttu-id="6b10d-161">Detalles</span><span class="sxs-lookup"><span data-stu-id="6b10d-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="6b10d-162">**Componente**</span><span class="sxs-lookup"><span data-stu-id="6b10d-162">**Component**</span></span>               | <span data-ttu-id="6b10d-163">API Web</span><span class="sxs-lookup"><span data-stu-id="6b10d-163">Web API</span></span> | 
| <span data-ttu-id="6b10d-164">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="6b10d-164">**SDL Phase**</span></span>               | <span data-ttu-id="6b10d-165">Compilación</span><span class="sxs-lookup"><span data-stu-id="6b10d-165">Build</span></span> |  
| <span data-ttu-id="6b10d-166">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="6b10d-166">**Applicable Technologies**</span></span> | <span data-ttu-id="6b10d-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="6b10d-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="6b10d-168">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-168">**Attributes**</span></span>              | <span data-ttu-id="6b10d-169">N/D</span><span class="sxs-lookup"><span data-stu-id="6b10d-169">N/A</span></span>  |
| <span data-ttu-id="6b10d-170">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="6b10d-170">**References**</span></span>              | <span data-ttu-id="6b10d-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling) (Control de excepciones en ASP.NET Web API), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) (Validación de modelos en ASP.NET Web API)</span><span class="sxs-lookup"><span data-stu-id="6b10d-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="6b10d-172">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-172">**Steps**</span></span> | <span data-ttu-id="6b10d-173">De forma predeterminada, la mayoría de las excepciones no detectadas en ASP.NET Web API se traducen en una respuesta HTTP con código de estado `500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="6b10d-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="6b10d-174">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6b10d-174">Example</span></span>
<span data-ttu-id="6b10d-175">código de estado de hello toocontrol devuelve Hola API, `HttpResponseException` puede utilizarse tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="6b10d-175">toocontrol hello status code returned by hello API, `HttpResponseException` can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a><span data-ttu-id="6b10d-176">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6b10d-176">Example</span></span>
<span data-ttu-id="6b10d-177">Para un control adicional en la respuesta de la excepción de hello, Hola `HttpResponseMessage` clase puede utilizarse tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="6b10d-177">For further control on hello exception response, hello `HttpResponseMessage` class can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
<span data-ttu-id="6b10d-178">toocatch excepciones no controladas que no sean del tipo hello `HttpResponseException`, puede usar filtros de excepción.</span><span class="sxs-lookup"><span data-stu-id="6b10d-178">toocatch unhandled exceptions that are not of hello type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="6b10d-179">Filtros de excepción implementan hello `System.Web.Http.Filters.IExceptionFilter` interfaz.</span><span class="sxs-lookup"><span data-stu-id="6b10d-179">Exception filters implement hello `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="6b10d-180">toowrite de manera más sencilla de Hello un filtro de excepción es tooderive de hello `System.Web.Http.Filters.ExceptionFilterAttribute` clase e invalidar el método OnException de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b10d-180">hello simplest way toowrite an exception filter is tooderive from hello `System.Web.Http.Filters.ExceptionFilterAttribute` class and override hello OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="6b10d-181">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6b10d-181">Example</span></span>
<span data-ttu-id="6b10d-182">A continuación puede ver un filtro que convierte excepciones `NotImplementedException` en código de estado HTTP `501, Not Implemented`:</span><span class="sxs-lookup"><span data-stu-id="6b10d-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

<span data-ttu-id="6b10d-183">Hay varias maneras tooregister un filtro de excepción Web API:</span><span class="sxs-lookup"><span data-stu-id="6b10d-183">There are several ways tooregister a Web API exception filter:</span></span>
- <span data-ttu-id="6b10d-184">Por acción</span><span class="sxs-lookup"><span data-stu-id="6b10d-184">By action</span></span>
- <span data-ttu-id="6b10d-185">Por controlador</span><span class="sxs-lookup"><span data-stu-id="6b10d-185">By controller</span></span>
- <span data-ttu-id="6b10d-186">Globalmente</span><span class="sxs-lookup"><span data-stu-id="6b10d-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="6b10d-187">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6b10d-187">Example</span></span>
<span data-ttu-id="6b10d-188">Hola tooapply tooa específico acción de filtrado, agregar filtro de hello como una acción de toohello de atributo:</span><span class="sxs-lookup"><span data-stu-id="6b10d-188">tooapply hello filter tooa specific action, add hello filter as an attribute toohello action:</span></span> 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a><span data-ttu-id="6b10d-189">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6b10d-189">Example</span></span>
<span data-ttu-id="6b10d-190">tooapply Hola filtro tooall de acciones de hello en un `controller`, agregar filtro de Hola como un atributo toohello `controller` clase:</span><span class="sxs-lookup"><span data-stu-id="6b10d-190">tooapply hello filter tooall of hello actions on a `controller`, add hello filter as an attribute toohello `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="6b10d-191">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6b10d-191">Example</span></span>
<span data-ttu-id="6b10d-192">Hola tooapply globalmente filtrar tooall controladores de API Web, debe agregar una instancia de hello filtro toohello `GlobalConfiguration.Configuration.Filters` colección.</span><span class="sxs-lookup"><span data-stu-id="6b10d-192">tooapply hello filter globally tooall Web API controllers, add an instance of hello filter toohello `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="6b10d-193">Filtros de excepciones en esta colección aplican tooany la acción de controlador de API Web.</span><span class="sxs-lookup"><span data-stu-id="6b10d-193">Exception filters in this collection apply tooany Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="6b10d-194">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6b10d-194">Example</span></span>
<span data-ttu-id="6b10d-195">Para la validación del modelo, se puede pasar a estado del modelo hello tooCreateErrorResponse método tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="6b10d-195">For model validation, hello model state can be passed tooCreateErrorResponse method as shown below:</span></span> 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

<span data-ttu-id="6b10d-196">Comprobar los enlaces de hello en la sección de referencias de Hola para obtener más información acerca del control de excepciones y la validación del modelo en ASP.Net Web API</span><span class="sxs-lookup"><span data-stu-id="6b10d-196">Check hello links in hello references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="6b10d-197"><a id="messages"></a>No exponga detalles de seguridad en los mensajes de error</span><span class="sxs-lookup"><span data-stu-id="6b10d-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="6b10d-198">Título</span><span class="sxs-lookup"><span data-stu-id="6b10d-198">Title</span></span>                   | <span data-ttu-id="6b10d-199">Detalles</span><span class="sxs-lookup"><span data-stu-id="6b10d-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="6b10d-200">**Componente**</span><span class="sxs-lookup"><span data-stu-id="6b10d-200">**Component**</span></span>               | <span data-ttu-id="6b10d-201">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="6b10d-201">Web Application</span></span> | 
| <span data-ttu-id="6b10d-202">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="6b10d-202">**SDL Phase**</span></span>               | <span data-ttu-id="6b10d-203">Compilación</span><span class="sxs-lookup"><span data-stu-id="6b10d-203">Build</span></span> |  
| <span data-ttu-id="6b10d-204">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="6b10d-204">**Applicable Technologies**</span></span> | <span data-ttu-id="6b10d-205">Genérico</span><span class="sxs-lookup"><span data-stu-id="6b10d-205">Generic</span></span> |
| <span data-ttu-id="6b10d-206">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-206">**Attributes**</span></span>              | <span data-ttu-id="6b10d-207">N/D</span><span class="sxs-lookup"><span data-stu-id="6b10d-207">N/A</span></span>  |
| <span data-ttu-id="6b10d-208">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="6b10d-208">**References**</span></span>              | <span data-ttu-id="6b10d-209">N/D</span><span class="sxs-lookup"><span data-stu-id="6b10d-209">N/A</span></span>  |
| <span data-ttu-id="6b10d-210">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-210">**Steps**</span></span> | <p><span data-ttu-id="6b10d-211">Mensajes de error genéricos se proporcionan directamente toohello usuario sin necesidad de incluir datos confidenciales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b10d-211">Generic error messages are provided directly toohello user without including sensitive application data.</span></span> <span data-ttu-id="6b10d-212">Ejemplos de datos confidenciales incluyen:</span><span class="sxs-lookup"><span data-stu-id="6b10d-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="6b10d-213">Nombres de servidor</span><span class="sxs-lookup"><span data-stu-id="6b10d-213">Server names</span></span></li><li><span data-ttu-id="6b10d-214">Cadenas de conexión</span><span class="sxs-lookup"><span data-stu-id="6b10d-214">Connection strings</span></span></li><li><span data-ttu-id="6b10d-215">Nombres de usuario</span><span class="sxs-lookup"><span data-stu-id="6b10d-215">Usernames</span></span></li><li><span data-ttu-id="6b10d-216">Contraseñas</span><span class="sxs-lookup"><span data-stu-id="6b10d-216">Passwords</span></span></li><li><span data-ttu-id="6b10d-217">Procedimientos SQL</span><span class="sxs-lookup"><span data-stu-id="6b10d-217">SQL procedures</span></span></li><li><span data-ttu-id="6b10d-218">Detalles de errores SQL dinámicos</span><span class="sxs-lookup"><span data-stu-id="6b10d-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="6b10d-219">Seguimiento de la pila y líneas de código</span><span class="sxs-lookup"><span data-stu-id="6b10d-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="6b10d-220">Variables almacenadas en memoria</span><span class="sxs-lookup"><span data-stu-id="6b10d-220">Variables stored in memory</span></span></li><li><span data-ttu-id="6b10d-221">Ubicaciones de unidad y carpeta</span><span class="sxs-lookup"><span data-stu-id="6b10d-221">Drive and folder locations</span></span></li><li><span data-ttu-id="6b10d-222">Puntos de instalación de aplicación</span><span class="sxs-lookup"><span data-stu-id="6b10d-222">Application install points</span></span></li><li><span data-ttu-id="6b10d-223">Valores de la configuración de host</span><span class="sxs-lookup"><span data-stu-id="6b10d-223">Host configuration settings</span></span></li><li><span data-ttu-id="6b10d-224">Otros detalles de la aplicación interna</span><span class="sxs-lookup"><span data-stu-id="6b10d-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="6b10d-225">La captura de todos los errores dentro de una aplicación y el envío de mensajes de error genéricos, así como la habilitación de errores personalizados dentro de IIS, le ayudará a evitar la divulgación de información.</span><span class="sxs-lookup"><span data-stu-id="6b10d-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="6b10d-226">Base de datos de SQL Server y .NET control de excepciones, entre otros arquitecturas de control de errores son la aplicación de generación de perfiles de usuario malintencionado tooa especialmente detallados y muy útil.</span><span class="sxs-lookup"><span data-stu-id="6b10d-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful tooa malicious user profiling your application.</span></span> <span data-ttu-id="6b10d-227">Hacer no directamente Hola de mostrar contenido de una clase deriva de la clase de excepción de .NET de hello y asegúrese de que tiene el control de excepciones adecuado para que una excepción inesperada no accidentalmente directamente genera toohello usuario.</span><span class="sxs-lookup"><span data-stu-id="6b10d-227">Do not directly display hello contents of a class derived from hello .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly toohello user.</span></span></p><ul><li><span data-ttu-id="6b10d-228">Proporcionar mensajes de error genérico directamente usuario toohello que condensan y alejadas detalles específicos que se encuentra directamente en el mensaje de error de excepción/hello</span><span class="sxs-lookup"><span data-stu-id="6b10d-228">Provide generic error messages directly toohello user that abstract away specific details found directly in hello exception/error message</span></span></li><li><span data-ttu-id="6b10d-229">No mostrar hello contenido de una excepción .NET clase directamente toohello usuario</span><span class="sxs-lookup"><span data-stu-id="6b10d-229">Do not display hello contents of a .NET exception class directly toohello user</span></span></li><li><span data-ttu-id="6b10d-230">Capturar todos los mensajes de error y si es necesario informar al usuario de Hola a través de un cliente de aplicación de toohello enviado de mensaje de error genérico</span><span class="sxs-lookup"><span data-stu-id="6b10d-230">Trap all error messages and if appropriate inform hello user via a generic error message sent toohello application client</span></span></li><li><span data-ttu-id="6b10d-231">No exponga contenido Hola de clase de excepción de hello directamente usuario toohello, especialmente Hola devuelve el valor de `.ToString()`, o valores de hello de propiedades de mensaje o el seguimiento de la pila de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b10d-231">Do not expose hello contents of hello Exception class directly toohello user, especially hello return value from `.ToString()`, or hello values of hello Message or StackTrace properties.</span></span> <span data-ttu-id="6b10d-232">Esta información de registro y mostrar un mensaje toohello usuario más inofensivo de forma segura</span><span class="sxs-lookup"><span data-stu-id="6b10d-232">Securely log this information and display a more innocuous message toohello user</span></span></li></ul>|

## <span data-ttu-id="6b10d-233"><a id="default"></a>Implemente una página de control de errores predeterminado</span><span class="sxs-lookup"><span data-stu-id="6b10d-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="6b10d-234">Título</span><span class="sxs-lookup"><span data-stu-id="6b10d-234">Title</span></span>                   | <span data-ttu-id="6b10d-235">Detalles</span><span class="sxs-lookup"><span data-stu-id="6b10d-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="6b10d-236">**Componente**</span><span class="sxs-lookup"><span data-stu-id="6b10d-236">**Component**</span></span>               | <span data-ttu-id="6b10d-237">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="6b10d-237">Web Application</span></span> | 
| <span data-ttu-id="6b10d-238">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="6b10d-238">**SDL Phase**</span></span>               | <span data-ttu-id="6b10d-239">Compilación</span><span class="sxs-lookup"><span data-stu-id="6b10d-239">Build</span></span> |  
| <span data-ttu-id="6b10d-240">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="6b10d-240">**Applicable Technologies**</span></span> | <span data-ttu-id="6b10d-241">Genérico</span><span class="sxs-lookup"><span data-stu-id="6b10d-241">Generic</span></span> |
| <span data-ttu-id="6b10d-242">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-242">**Attributes**</span></span>              | <span data-ttu-id="6b10d-243">N/D</span><span class="sxs-lookup"><span data-stu-id="6b10d-243">N/A</span></span>  |
| <span data-ttu-id="6b10d-244">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="6b10d-244">**References**</span></span>              | <span data-ttu-id="6b10d-245">[Modificar configuración de páginas de errores ASP.NET (Cuadro de diálogo)](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="6b10d-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="6b10d-246">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-246">**Steps**</span></span> | <p><span data-ttu-id="6b10d-247">Cuando se produce un error en una aplicación ASP.NET que provoca un error 1.x 500 o HTTP 500 Error interno del servidor, o la configuración de una característica (por ejemplo, el filtrado de solicitudes) impide que se muestre una página, se generará un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="6b10d-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="6b10d-248">Los administradores pueden elegir si o no la aplicación hello debe mostrar un mensaje descriptivo toohello cliente, cliente de toohello de mensaje de error detallado o solo toolocalhost de mensaje de error detallado.</span><span class="sxs-lookup"><span data-stu-id="6b10d-248">Administrators can choose whether or not hello application should display a friendly message toohello client, detailed error message toohello client, or detailed error message toolocalhost only.</span></span> <span data-ttu-id="6b10d-249">Hola <customErrors> etiqueta en el archivo web.config de hello tiene tres modos:</span><span class="sxs-lookup"><span data-stu-id="6b10d-249">hello <customErrors> tag in hello web.config has three modes:</span></span></p><ul><li><span data-ttu-id="6b10d-250">**On:** especifica que los errores personalizados están habilitados.</span><span class="sxs-lookup"><span data-stu-id="6b10d-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="6b10d-251">Si no se especifica ningún atributo defaultRedirect, los usuarios verán un error genérico.</span><span class="sxs-lookup"><span data-stu-id="6b10d-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="6b10d-252">los errores personalizados de Hola se muestran los clientes remotos de toohello y toohello host local</span><span class="sxs-lookup"><span data-stu-id="6b10d-252">hello custom errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="6b10d-253">**Off:** especifica que los errores personalizados están deshabilitados.</span><span class="sxs-lookup"><span data-stu-id="6b10d-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="6b10d-254">Hello errores detallados de ASP.NET se muestran los clientes remotos de toohello y toohello host local</span><span class="sxs-lookup"><span data-stu-id="6b10d-254">hello detailed ASP.NET errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="6b10d-255">**RemoteOnly:** especifica que los errores personalizados se muestran solo los clientes remotos toohello y que los errores ASP.NET se muestran toohello host local.</span><span class="sxs-lookup"><span data-stu-id="6b10d-255">**RemoteOnly:** Specifies that custom errors are shown only toohello remote clients, and that ASP.NET errors are shown toohello local host.</span></span> <span data-ttu-id="6b10d-256">Se trata de valor predeterminado de Hola</span><span class="sxs-lookup"><span data-stu-id="6b10d-256">This is hello default value</span></span></li></ul><p><span data-ttu-id="6b10d-257">Abra hello `web.config` de archivos para el sitio de la aplicación hello y asegúrese de que la etiqueta de hello tiene cualquiera `<customErrors mode="RemoteOnly" />` o `<customErrors mode="On" />` definido.</span><span class="sxs-lookup"><span data-stu-id="6b10d-257">Open hello `web.config` file for hello application/site and ensure that hello tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="6b10d-258"><a id="deployment"></a>Establecer el método de implementación tooRetail en IIS</span><span class="sxs-lookup"><span data-stu-id="6b10d-258"><a id="deployment"></a>Set Deployment Method tooRetail in IIS</span></span>

| <span data-ttu-id="6b10d-259">Título</span><span class="sxs-lookup"><span data-stu-id="6b10d-259">Title</span></span>                   | <span data-ttu-id="6b10d-260">Detalles</span><span class="sxs-lookup"><span data-stu-id="6b10d-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="6b10d-261">**Componente**</span><span class="sxs-lookup"><span data-stu-id="6b10d-261">**Component**</span></span>               | <span data-ttu-id="6b10d-262">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="6b10d-262">Web Application</span></span> | 
| <span data-ttu-id="6b10d-263">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="6b10d-263">**SDL Phase**</span></span>               | <span data-ttu-id="6b10d-264">Implementación</span><span class="sxs-lookup"><span data-stu-id="6b10d-264">Deployment</span></span> |  
| <span data-ttu-id="6b10d-265">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="6b10d-265">**Applicable Technologies**</span></span> | <span data-ttu-id="6b10d-266">Genérico</span><span class="sxs-lookup"><span data-stu-id="6b10d-266">Generic</span></span> |
| <span data-ttu-id="6b10d-267">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-267">**Attributes**</span></span>              | <span data-ttu-id="6b10d-268">N/D</span><span class="sxs-lookup"><span data-stu-id="6b10d-268">N/A</span></span>  |
| <span data-ttu-id="6b10d-269">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="6b10d-269">**References**</span></span>              | <span data-ttu-id="6b10d-270">[deployment (Elemento, Esquema de configuración de ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="6b10d-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="6b10d-271">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-271">**Steps**</span></span> | <p><span data-ttu-id="6b10d-272">Hola `<deployment retail>` conmutador está diseñado para su uso por servidores IIS de producción.</span><span class="sxs-lookup"><span data-stu-id="6b10d-272">hello `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="6b10d-273">Este modificador es toohelp usa las aplicaciones se ejecutan con la mejor rendimiento posible de Hola y de error detallados de información de seguridad mínimos escapes deshabilitando Hola resultados de seguimiento de toogenerate de capacidad de la aplicación en una página, deshabilitar toodisplay de capacidad de Hola mensajes que los usuarios tooend y Hola deshabilitar el modificador de depuración.</span><span class="sxs-lookup"><span data-stu-id="6b10d-273">This switch is used toohelp applications run with hello best possible performance and least possible security information leakages by disabling hello application's ability toogenerate trace output on a page, disabling hello ability toodisplay detailed error messages tooend users, and disabling hello debug switch.</span></span></p><p><span data-ttu-id="6b10d-274">A menudo, los conmutadores y opciones que están enfocadas hacia en el desarrollador, como los errores de solicitud de seguimiento y depuración, se habilitan durante el desarrollo activo.</span><span class="sxs-lookup"><span data-stu-id="6b10d-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="6b10d-275">Se recomienda que el método de implementación de hello en cualquier servidor de producción se establecer tooretail.</span><span class="sxs-lookup"><span data-stu-id="6b10d-275">It is recommended that hello deployment method on any production server be set tooretail.</span></span> <span data-ttu-id="6b10d-276">Abra el archivo machine.config de hello y asegúrese de que `<deployment retail="true" />` mantiene establecido tootrue.</span><span class="sxs-lookup"><span data-stu-id="6b10d-276">open hello machine.config file and ensure that `<deployment retail="true" />` remains set tootrue.</span></span></p>|

## <span data-ttu-id="6b10d-277"><a id="fail"></a>Las excepciones deben generar un error con seguridad</span><span class="sxs-lookup"><span data-stu-id="6b10d-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="6b10d-278">Título</span><span class="sxs-lookup"><span data-stu-id="6b10d-278">Title</span></span>                   | <span data-ttu-id="6b10d-279">Detalles</span><span class="sxs-lookup"><span data-stu-id="6b10d-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="6b10d-280">**Componente**</span><span class="sxs-lookup"><span data-stu-id="6b10d-280">**Component**</span></span>               | <span data-ttu-id="6b10d-281">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="6b10d-281">Web Application</span></span> | 
| <span data-ttu-id="6b10d-282">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="6b10d-282">**SDL Phase**</span></span>               | <span data-ttu-id="6b10d-283">Compilación</span><span class="sxs-lookup"><span data-stu-id="6b10d-283">Build</span></span> |  
| <span data-ttu-id="6b10d-284">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="6b10d-284">**Applicable Technologies**</span></span> | <span data-ttu-id="6b10d-285">Genérico</span><span class="sxs-lookup"><span data-stu-id="6b10d-285">Generic</span></span> |
| <span data-ttu-id="6b10d-286">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-286">**Attributes**</span></span>              | <span data-ttu-id="6b10d-287">N/D</span><span class="sxs-lookup"><span data-stu-id="6b10d-287">N/A</span></span>  |
| <span data-ttu-id="6b10d-288">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="6b10d-288">**References**</span></span>              | <span data-ttu-id="6b10d-289">[Fail securely](https://www.owasp.org/index.php/Fail_securely) (Control seguro de los errores)</span><span class="sxs-lookup"><span data-stu-id="6b10d-289">[Fail securely](https://www.owasp.org/index.php/Fail_securely)</span></span> |
| <span data-ttu-id="6b10d-290">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="6b10d-290">**Steps**</span></span> | <span data-ttu-id="6b10d-291">La aplicación debe generar un error con seguridad.</span><span class="sxs-lookup"><span data-stu-id="6b10d-291">Application should fail safely.</span></span> <span data-ttu-id="6b10d-292">Cualquier método que devuelve un valor booleano en el que se va a basar la toma de una decisión específica, debe tener el bloque de excepción creado con cuidado.</span><span class="sxs-lookup"><span data-stu-id="6b10d-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="6b10d-293">Hay muchos errores lógicos debido toowhich sobrante de problemas de seguridad en, cuando se escribe el bloque de excepción de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b10d-293">There are lot of logical errors due toowhich security issues creep in, when hello exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="6b10d-294">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6b10d-294">Example</span></span>
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
<span data-ttu-id="6b10d-295">Hola sobre el método siempre devolverá True, si se produce alguna excepción.</span><span class="sxs-lookup"><span data-stu-id="6b10d-295">hello above method will always return True, if some exception happens.</span></span> <span data-ttu-id="6b10d-296">Si el usuario final de hello proporciona una dirección URL con formato incorrecto, que Hola aspectos de explorador, pero Hola `Uri()` constructor no, se producirá una excepción y víctima de Hola se tomará de dirección URL válido pero tiene un formato incorrecto de toohello.</span><span class="sxs-lookup"><span data-stu-id="6b10d-296">If hello end user provides a malformed URL, that hello browser respects, but hello `Uri()` constructor doesn't, this will throw an exception, and hello victim will be taken toohello valid but malformed URL.</span></span> 
