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
# <a name="security-frame-exception-management--mitigations"></a>Marco de seguridad: Administración de excepciones | Mitigaciones 
| Producto o servicio | Artículo |
| --------------- | ------- |
| **WCF** | <ul><li>[WCF: no incluya el nodo serviceDebug en el archivo de configuración](#servicedebug)</li><li>[WCF: no incluya el nodo serviceMetadata en el archivo de configuración](#servicemetadata)</li></ul> |
| **API web** | <ul><li>[Asegúrese de que se realiza un control adecuado de las excepciones en ASP.NET Web API](#exception)</li></ul> |
| **Aplicación web** | <ul><li>[No exponga detalles de seguridad en los mensajes de error](#messages)</li><li>[Implemente una página de control de errores predeterminado](#default)</li><li>[Establecer el método de implementación tooRetail en IIS](#deployment)</li><li>[Las excepciones deben generar un error con seguridad](#fail)</li></ul> |

## <a id="servicedebug"></a>WCF: no incluya el nodo serviceDebug en el archivo de configuración

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | Servicios de Windows Communication Framework (WCF) pueden ser configurado tooexpose información de depuración. La información de depuración no debe usarse en entornos de producción. Hola `<serviceDebug>` etiqueta define si está habilitada la característica de información de depuración de Hola para un servicio WCF. Si Hola atributo includeExceptionDetailInFaults se establece tootrue, se devolverá información de excepción de aplicación hello tooclients. Los atacantes pueden aprovechar la información adicional de hello obtienen de la depuración de salida toomount los ataques dirigidos en framework hello, base de datos u otros recursos usados por la aplicación hello. |

### <a name="example"></a>Ejemplo
archivo de configuración siguiente Hello incluye hello `<serviceDebug>` etiqueta: 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
Deshabilitar la información de depuración en el servicio de Hola. Esto puede realizarse mediante la eliminación de hello `<serviceDebug>` etiqueta desde el archivo de configuración de la aplicación. 

## <a id="servicemetadata"></a>WCF: no incluya el nodo serviceMetadata en el archivo de configuración

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Genérico, .NET Framework 3 |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | Exponer públicamente información acerca de un servicio puede proporcionar a los atacantes valiosa información sobre cómo pueden sacar provecho de servicio de Hola. Hola `<serviceMetadata>` etiqueta habilita la característica de publicación de metadatos de Hola. Los metadatos del servicio pueden contener información confidencial que no debe estar accesible públicamente. Como mínimo, permitir solo los usuarios de confianza tooaccess Hola metadatos y asegúrese de que no se expone información innecesaria. Mejor aún, deshabilitar completamente Hola capacidad toopublish metadatos. Una configuración segura de WCF no contendrá hello `<serviceMetadata>` etiqueta. |

## <a id="exception"></a>Asegúrese de que se realiza un tratamiento adecuado de las excepciones en ASP.NET Web API

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC 5, MVC 6 |
| **Atributos**              | N/D  |
| **Referencias**              | [Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling) (Control de excepciones en ASP.NET Web API), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) (Validación de modelos en ASP.NET Web API) |
| **Pasos** | De forma predeterminada, la mayoría de las excepciones no detectadas en ASP.NET Web API se traducen en una respuesta HTTP con código de estado `500, Internal Server Error`|

### <a name="example"></a>Ejemplo
código de estado de hello toocontrol devuelve Hola API, `HttpResponseException` puede utilizarse tal y como se muestra a continuación: 
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

### <a name="example"></a>Ejemplo
Para un control adicional en la respuesta de la excepción de hello, Hola `HttpResponseMessage` clase puede utilizarse tal y como se muestra a continuación: 
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
toocatch excepciones no controladas que no sean del tipo hello `HttpResponseException`, puede usar filtros de excepción. Filtros de excepción implementan hello `System.Web.Http.Filters.IExceptionFilter` interfaz. toowrite de manera más sencilla de Hello un filtro de excepción es tooderive de hello `System.Web.Http.Filters.ExceptionFilterAttribute` clase e invalidar el método OnException de Hola. 

### <a name="example"></a>Ejemplo
A continuación puede ver un filtro que convierte excepciones `NotImplementedException` en código de estado HTTP `501, Not Implemented`: 
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

Hay varias maneras tooregister un filtro de excepción Web API:
- Por acción
- Por controlador
- Globalmente

### <a name="example"></a>Ejemplo
Hola tooapply tooa específico acción de filtrado, agregar filtro de hello como una acción de toohello de atributo: 
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
### <a name="example"></a>Ejemplo
tooapply Hola filtro tooall de acciones de hello en un `controller`, agregar filtro de Hola como un atributo toohello `controller` clase: 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a>Ejemplo
Hola tooapply globalmente filtrar tooall controladores de API Web, debe agregar una instancia de hello filtro toohello `GlobalConfiguration.Configuration.Filters` colección. Filtros de excepciones en esta colección aplican tooany la acción de controlador de API Web. 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a>Ejemplo
Para la validación del modelo, se puede pasar a estado del modelo hello tooCreateErrorResponse método tal como se muestra a continuación: 
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

Comprobar los enlaces de hello en la sección de referencias de Hola para obtener más información acerca del control de excepciones y la validación del modelo en ASP.Net Web API 

## <a id="messages"></a>No exponga detalles de seguridad en los mensajes de error

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Mensajes de error genéricos se proporcionan directamente toohello usuario sin necesidad de incluir datos confidenciales de la aplicación. Ejemplos de datos confidenciales incluyen:</p><ul><li>Nombres de servidor</li><li>Cadenas de conexión</li><li>Nombres de usuario</li><li>Contraseñas</li><li>Procedimientos SQL</li><li>Detalles de errores SQL dinámicos</li><li>Seguimiento de la pila y líneas de código</li><li>Variables almacenadas en memoria</li><li>Ubicaciones de unidad y carpeta</li><li>Puntos de instalación de aplicación</li><li>Valores de la configuración de host</li><li>Otros detalles de la aplicación interna</li></ul><p>La captura de todos los errores dentro de una aplicación y el envío de mensajes de error genéricos, así como la habilitación de errores personalizados dentro de IIS, le ayudará a evitar la divulgación de información. Base de datos de SQL Server y .NET control de excepciones, entre otros arquitecturas de control de errores son la aplicación de generación de perfiles de usuario malintencionado tooa especialmente detallados y muy útil. Hacer no directamente Hola de mostrar contenido de una clase deriva de la clase de excepción de .NET de hello y asegúrese de que tiene el control de excepciones adecuado para que una excepción inesperada no accidentalmente directamente genera toohello usuario.</p><ul><li>Proporcionar mensajes de error genérico directamente usuario toohello que condensan y alejadas detalles específicos que se encuentra directamente en el mensaje de error de excepción/hello</li><li>No mostrar hello contenido de una excepción .NET clase directamente toohello usuario</li><li>Capturar todos los mensajes de error y si es necesario informar al usuario de Hola a través de un cliente de aplicación de toohello enviado de mensaje de error genérico</li><li>No exponga contenido Hola de clase de excepción de hello directamente usuario toohello, especialmente Hola devuelve el valor de `.ToString()`, o valores de hello de propiedades de mensaje o el seguimiento de la pila de Hola. Esta información de registro y mostrar un mensaje toohello usuario más inofensivo de forma segura</li></ul>|

## <a id="default"></a>Implemente una página de control de errores predeterminado

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Modificar configuración de páginas de errores ASP.NET (Cuadro de diálogo)](https://technet.microsoft.com/library/dd569096(WS.10).aspx) |
| **Pasos** | <p>Cuando se produce un error en una aplicación ASP.NET que provoca un error 1.x 500 o HTTP 500 Error interno del servidor, o la configuración de una característica (por ejemplo, el filtrado de solicitudes) impide que se muestre una página, se generará un mensaje de error. Los administradores pueden elegir si o no la aplicación hello debe mostrar un mensaje descriptivo toohello cliente, cliente de toohello de mensaje de error detallado o solo toolocalhost de mensaje de error detallado. Hola <customErrors> etiqueta en el archivo web.config de hello tiene tres modos:</p><ul><li>**On:** especifica que los errores personalizados están habilitados. Si no se especifica ningún atributo defaultRedirect, los usuarios verán un error genérico. los errores personalizados de Hola se muestran los clientes remotos de toohello y toohello host local</li><li>**Off:** especifica que los errores personalizados están deshabilitados. Hello errores detallados de ASP.NET se muestran los clientes remotos de toohello y toohello host local</li><li>**RemoteOnly:** especifica que los errores personalizados se muestran solo los clientes remotos toohello y que los errores ASP.NET se muestran toohello host local. Se trata de valor predeterminado de Hola</li></ul><p>Abra hello `web.config` de archivos para el sitio de la aplicación hello y asegúrese de que la etiqueta de hello tiene cualquiera `<customErrors mode="RemoteOnly" />` o `<customErrors mode="On" />` definido.</p>|

## <a id="deployment"></a>Establecer el método de implementación tooRetail en IIS

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [deployment (Elemento, Esquema de configuración de ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx) |
| **Pasos** | <p>Hola `<deployment retail>` conmutador está diseñado para su uso por servidores IIS de producción. Este modificador es toohelp usa las aplicaciones se ejecutan con la mejor rendimiento posible de Hola y de error detallados de información de seguridad mínimos escapes deshabilitando Hola resultados de seguimiento de toogenerate de capacidad de la aplicación en una página, deshabilitar toodisplay de capacidad de Hola mensajes que los usuarios tooend y Hola deshabilitar el modificador de depuración.</p><p>A menudo, los conmutadores y opciones que están enfocadas hacia en el desarrollador, como los errores de solicitud de seguimiento y depuración, se habilitan durante el desarrollo activo. Se recomienda que el método de implementación de hello en cualquier servidor de producción se establecer tooretail. Abra el archivo machine.config de hello y asegúrese de que `<deployment retail="true" />` mantiene establecido tootrue.</p>|

## <a id="fail"></a>Las excepciones deben generar un error con seguridad

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Fail securely](https://www.owasp.org/index.php/Fail_securely) (Control seguro de los errores) |
| **Pasos** | La aplicación debe generar un error con seguridad. Cualquier método que devuelve un valor booleano en el que se va a basar la toma de una decisión específica, debe tener el bloque de excepción creado con cuidado. Hay muchos errores lógicos debido toowhich sobrante de problemas de seguridad en, cuando se escribe el bloque de excepción de Hola.|

### <a name="example"></a>Ejemplo
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
Hola sobre el método siempre devolverá True, si se produce alguna excepción. Si el usuario final de hello proporciona una dirección URL con formato incorrecto, que Hola aspectos de explorador, pero Hola `Uri()` constructor no, se producirá una excepción y víctima de Hola se tomará de dirección URL válido pero tiene un formato incorrecto de toohello. 
