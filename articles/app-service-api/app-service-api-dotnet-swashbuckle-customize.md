---
title: definiciones de aaaCustomize genera Swashbuckle API
description: "Obtenga información acerca de cómo las definiciones de API de Swagger de toocustomize generadas por Swashbuckle para una aplicación de API de servicio de aplicaciones de Azure."
services: app-service\api
documentationcenter: .net
author: bradygaster
manager: erikre
editor: jimbe
ms.assetid: 6b8cbc38-d282-4a0f-b0c5-762631bae6f3
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: e31c665f8993533c5ec9a935e42cce34f86a5ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a>Personalización de definiciones de API generadas por Swashbuckle
## <a name="overview"></a>Información general
Este artículo se explica cómo toocustomize Swashbuckle toohandle comunes escenarios donde puede que desee tooalter Hola comportamiento predeterminado:

* Swashbuckle genera identificadores de operación duplicados para las sobrecargas de los métodos de controlador
* Swashbuckle se da por supuesto que Hola sólo hay una respuesta válida desde un método HTTP 200 (OK) 

## <a name="customize-operation-identifier-generation"></a>Personalización de la generación de identificadores de operación
Swashbuckle genera identificadores de operación de Swagger concatenando el nombre del controlador y el nombre del método. Este patrón ocasiona un problema cuando se tienen varias sobrecargas de un método: Swashbuckle genera identificadores de operación duplicados, lo cual supone un JSON de Swagger no válido.

Por ejemplo, hello después el código del controlador hace Swashbuckle toogenerate tres identificadores de operación Contact_Get.

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

Para resolver el problema de hello manualmente proporcionando métodos Hola nombres únicos, como siguiente hello en este ejemplo:

* Obtener
* GetById
* GetPage

alternativa de Hello es tooextend Swashbuckle toomake generar automáticamente el Id. único de la operación.

Hello pasos siguientes muestran cómo Hola toocustomize Swashbuckle utilizando *SwaggerConfig.cs* archivo que se incluye en el proyecto de Hola de plantilla de proyecto de Visual Studio Preview de aplicaciones de la API de Hola.  También puede personalizar Swashbuckle en un proyecto  de API web que configure para implementarlo como una aplicación de API.

1. Creación de una implementación de `IOperationFilter` personalizada 
   
    Hola `IOperationFilter` interfaz proporciona un punto de extensibilidad para los usuarios de Swashbuckle que desea toocustomize diversos aspectos del proceso de metadatos de Swagger Hola. Hello código siguiente muestra un método para cambiar el comportamiento de Id. de operación de generación de Hola. código de Hello anexa el nombre de Id. de operación de toohello de nombres de parámetro.  
   
        using Swashbuckle.Swagger;
        using System.Web.Http.Description;
   
        namespace ContactsList
        {
            public class MultipleOperationsWithSameVerbFilter : IOperationFilter
            {
                public void Apply(
                    Operation operation,
                    SchemaRegistry schemaRegistry,
                    ApiDescription apiDescription)
                {
                    if (operation.parameters != null)
                    {
                        operation.operationId += "By";
                        foreach (var parm in operation.parameters)
                        {
                            operation.operationId += string.Format("{0}",parm.name);
                        }
                    }
                }
            }
        }
2. En *App_Start\SwaggerConfig.cs* archivo, llamada hello `OperationFilter` método toocause Swashbuckle toouse ¡hello nueva `IOperationFilter` implementación.
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    Hola *SwaggerConfig.cs* archivo que se ha quitado por hello Swashbuckle NuGet paquete contiene muchos ejemplos de comentarios de los puntos de extensibilidad. comentarios adicionales de Hello no se muestran aquí. 
   
    Después de realizar este cambio, su `IOperationFilter` implementación se usa y hace que toobe de Id. de operación único generado.
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>Permitir códigos de respuesta distintos de 200
De forma predeterminada, Swashbuckle se da por supuesto que una respuesta HTTP 200 (OK) es hello *sólo* legítimos respuesta desde un método de API Web. En algunos casos, puede que desee tooreturn otros códigos de respuesta sin producir una excepción de hello cliente tooraise.  Por ejemplo, hello Web API código siguiente muestra un escenario en el que desearía Hola cliente tooaccept 200 o 404 como las respuestas válidas.

    [ResponseType(typeof(Contact))]
    public HttpResponseMessage Get(int id)
    {
        var contacts = GetContacts();

        var requestedContact = contacts.FirstOrDefault(x => x.Id == id);

        if (requestedContact == null)
        {
            return Request.CreateResponse(HttpStatusCode.NotFound);
        }
        else
        {
            return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
        }
    }

En este escenario, hello Swagger que Swashbuckle genera de forma predeterminada especifica solo un código de estado HTTP legítimo, 200 de HTTP.

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

Dado que Visual Studio utiliza hello toogenerate código de definición de Swagger API para los clientes de hello, crea el código de cliente que genera una excepción para todas las respuestas que no sea un HTTP 200. código de Hello siguiente es desde un cliente de C# generado para este método de API Web de ejemplo.

    if (statusCode != HttpStatusCode.OK)
    {
        HttpOperationException<object> ex = new HttpOperationException<object>();
        ex.Request = httpRequest;
        ex.Response = httpResponse;
        ex.Body = null;
        if (shouldTrace)
        {
            ServiceClientTracing.Error(invocationId, ex);
        }
        throw ex;
    } 

Swashbuckle proporciona dos maneras de personalizar la lista de Hola de códigos de respuesta HTTP esperados que genera, mediante los comentarios XML o hello `SwaggerResponse` atributo. atributo de Hello es más fácil, pero solo está disponible en Swashbuckle 5.1.5 o posterior. plantilla de proyecto nuevo de vista previa de aplicaciones de API en Visual Studio 2013 Hello incluye Swashbuckle versión 5.0.0, por lo que si usa la plantilla de hello y no desea tooupdate Swashbuckle, la única opción es toouse los comentarios XML. 

### <a name="customize-expected-response-codes-using-xml-comments"></a>Personalización de códigos de respuesta esperados mediante comentarios XML
Use los códigos de respuesta de toospecify de este método si la versión de Swashbuckle es anterior a 5.1.5.

1. En primer lugar, agregue comentarios de documentación XML frente a métodos de hello para que desea toospecify códigos de respuesta HTTP. Realizar la acción de API Web de ejemplo de Hola tooit de documentación de XML se muestra anteriormente y aplicar hello, se crearán en código como el siguiente ejemplo de Hola. 
   
        /// <summary>
        /// Returns hello specified contact.
        /// </summary>
        /// <param name="id">hello ID of hello contact.</param>
        /// <returns>A contact record with an HTTP 200, or null with an HTTP 404.</returns>
        /// <response code="200">OK</response>
        /// <response code="404">Not Found</response>
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
   
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
2. Agregar instrucciones de hello *SwaggerConfig.cs* toodirect Swashbuckle toomake uso del archivo de documentación XML Hola de archivos.
   
   * Abra *SwaggerConfig.cs* y cree un método en hello *SwaggerConfig* archivo XML de documentación toohello de clase toospecify Hola ruta de acceso. 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Desplácese hacia abajo en hello *SwaggerConfig.cs* archivo hasta que vea hello como comentario de línea de código similar al siguiente captura de pantalla de bienvenida. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * Quite el comentario de hello tooenable Hola XML comentarios de una línea de procesamiento durante la generación de Swagger. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. En el archivo de documentación de XML de pedido toogenerate hello, vaya a propiedades del proyecto de Hola y habilitar el archivo de documentación XML de hello tal y como se muestra en la siguiente captura de pantalla de Hola. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

Después de realizar estos pasos, hello Swagger texto JSON generado por Swashbuckle reflejará los códigos de respuesta HTTP de Hola que especificó en los comentarios XML Hola. Hola de captura de pantalla siguiente muestra esta nueva carga JSON. 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

Cuando se usa código de cliente de Visual Studio tooregenerate hello para la API de REST, Hola código C# acepta ambos códigos de estado OK de HTTP y no se encuentra de hello sin generar una excepción, lo que sus decisiones de toomake código usado en cómo devolver toohandle Hola de un valor null Póngase en contacto con el registro. 

        if (statusCode != HttpStatusCode.OK && statusCode != HttpStatusCode.NotFound)
        {
            HttpOperationException<object> ex = new HttpOperationException<object>();
            ex.Request = httpRequest;
            ex.Response = httpResponse;
            ex.Body = null;
            if (shouldTrace)
            {
                ServiceClientTracing.Error(invocationId, ex);
            }
                throw ex;
        }

código de Hello para esta demostración se puede encontrar en [este repositorio de GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse). Junto con la API Web de hello marcado con comentarios de documentación XML del proyecto es un proyecto de aplicación de consola que contenga a un cliente generado para esta API. 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a>Personalizar los códigos de respuesta esperado con hello SwaggerResponse atributo
Hola [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) atributo está disponible en Swashbuckle 5.1.5 y versiones posteriores. En caso de que tiene una versión anterior del proyecto, en esta sección se inicia mediante la explicación de cómo tooupdate hello Swashbuckle NuGet paquete para que puedan utilizar este atributo.

1. En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto de la API web y haga clic en **Administrar paquetes de NuGet**. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. Haga clic en hello *actualización* botón siguiente toohello *Swashbuckle* paquete NuGet. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. Agregar hello *SwaggerResponse* atributos toohello métodos de acción de API Web que se desea toospecify códigos de respuesta HTTP válidos. 
   
        [SwaggerResponse(HttpStatusCode.OK)]
        [SwaggerResponse(HttpStatusCode.NotFound)]
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
4. Agregar un `using` declaración de espacio de nombres del atributo de hello:
   
        using Swashbuckle.Swagger.Annotations;
5. Examinar toohello */swagger/docs/v1* dirección URL de su proyecto y Hola serán visibles en varios códigos de respuesta HTTP Hola Swagger JSON. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

código de Hello para esta demostración se puede encontrar en [este repositorio de GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes). Junto con hello proyecto de API Web decorada con hello *SwaggerResponse* atributo es un proyecto de aplicación de consola que contiene un cliente generado para esta API. 

## <a name="next-steps"></a>Pasos siguientes
Este artículo le haya mostrado cómo forma de hello toocustomize Swashbuckle genera identificadores de operación y códigos de respuesta válido. Para obtener más información, consulte [Swashbuckle en GitHub](https://github.com/domaindrivendev/Swashbuckle).

