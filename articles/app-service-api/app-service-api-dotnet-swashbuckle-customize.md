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
# <a name="customize-swashbuckle-generated-api-definitions"></a><span data-ttu-id="19f12-103">Personalización de definiciones de API generadas por Swashbuckle</span><span class="sxs-lookup"><span data-stu-id="19f12-103">Customize Swashbuckle-generated API definitions</span></span>
## <a name="overview"></a><span data-ttu-id="19f12-104">Información general</span><span class="sxs-lookup"><span data-stu-id="19f12-104">Overview</span></span>
<span data-ttu-id="19f12-105">Este artículo se explica cómo toocustomize Swashbuckle toohandle comunes escenarios donde puede que desee tooalter Hola comportamiento predeterminado:</span><span class="sxs-lookup"><span data-stu-id="19f12-105">This article explains how toocustomize Swashbuckle toohandle common scenarios where you may want tooalter hello default behavior:</span></span>

* <span data-ttu-id="19f12-106">Swashbuckle genera identificadores de operación duplicados para las sobrecargas de los métodos de controlador</span><span class="sxs-lookup"><span data-stu-id="19f12-106">Swashbuckle generates duplicate operation identifiers for overloads of controller methods</span></span>
* <span data-ttu-id="19f12-107">Swashbuckle se da por supuesto que Hola sólo hay una respuesta válida desde un método HTTP 200 (OK)</span><span class="sxs-lookup"><span data-stu-id="19f12-107">Swashbuckle assumes that hello only valid response from a method is HTTP 200 (OK)</span></span> 

## <a name="customize-operation-identifier-generation"></a><span data-ttu-id="19f12-108">Personalización de la generación de identificadores de operación</span><span class="sxs-lookup"><span data-stu-id="19f12-108">Customize operation identifier generation</span></span>
<span data-ttu-id="19f12-109">Swashbuckle genera identificadores de operación de Swagger concatenando el nombre del controlador y el nombre del método.</span><span class="sxs-lookup"><span data-stu-id="19f12-109">Swashbuckle generates Swagger operation identifiers by concatenating controller name and method name.</span></span> <span data-ttu-id="19f12-110">Este patrón ocasiona un problema cuando se tienen varias sobrecargas de un método: Swashbuckle genera identificadores de operación duplicados, lo cual supone un JSON de Swagger no válido.</span><span class="sxs-lookup"><span data-stu-id="19f12-110">This pattern creates a problem when you have multiple overloads of a method: Swashbuckle generates duplicate operation ids, which is invalid Swagger JSON.</span></span>

<span data-ttu-id="19f12-111">Por ejemplo, hello después el código del controlador hace Swashbuckle toogenerate tres identificadores de operación Contact_Get.</span><span class="sxs-lookup"><span data-stu-id="19f12-111">For example, hello following controller code causes Swashbuckle toogenerate three Contact_Get operation ids.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

<span data-ttu-id="19f12-112">Para resolver el problema de hello manualmente proporcionando métodos Hola nombres únicos, como siguiente hello en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="19f12-112">You can solve hello problem manually by giving hello methods unique names, such as hello following for this example:</span></span>

* <span data-ttu-id="19f12-113">Obtener</span><span class="sxs-lookup"><span data-stu-id="19f12-113">Get</span></span>
* <span data-ttu-id="19f12-114">GetById</span><span class="sxs-lookup"><span data-stu-id="19f12-114">GetById</span></span>
* <span data-ttu-id="19f12-115">GetPage</span><span class="sxs-lookup"><span data-stu-id="19f12-115">GetPage</span></span>

<span data-ttu-id="19f12-116">alternativa de Hello es tooextend Swashbuckle toomake generar automáticamente el Id. único de la operación.</span><span class="sxs-lookup"><span data-stu-id="19f12-116">hello alternative is tooextend Swashbuckle toomake it automatically generate unique operation ids.</span></span>

<span data-ttu-id="19f12-117">Hello pasos siguientes muestran cómo Hola toocustomize Swashbuckle utilizando *SwaggerConfig.cs* archivo que se incluye en el proyecto de Hola de plantilla de proyecto de Visual Studio Preview de aplicaciones de la API de Hola.</span><span class="sxs-lookup"><span data-stu-id="19f12-117">hello following steps show how toocustomize Swashbuckle by using hello *SwaggerConfig.cs* file that is included in hello project by hello Visual Studio API Apps Preview project template.</span></span>  <span data-ttu-id="19f12-118">También puede personalizar Swashbuckle en un proyecto  de API web que configure para implementarlo como una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="19f12-118">You can also customize Swashbuckle in a Web API project that you configure for deployment as an API app.</span></span>

1. <span data-ttu-id="19f12-119">Creación de una implementación de `IOperationFilter` personalizada</span><span class="sxs-lookup"><span data-stu-id="19f12-119">Create a custom `IOperationFilter` implementation</span></span> 
   
    <span data-ttu-id="19f12-120">Hola `IOperationFilter` interfaz proporciona un punto de extensibilidad para los usuarios de Swashbuckle que desea toocustomize diversos aspectos del proceso de metadatos de Swagger Hola.</span><span class="sxs-lookup"><span data-stu-id="19f12-120">hello `IOperationFilter` interface provides an extensibility point for Swashbuckle users who want toocustomize various aspects of hello Swagger metadata process.</span></span> <span data-ttu-id="19f12-121">Hello código siguiente muestra un método para cambiar el comportamiento de Id. de operación de generación de Hola.</span><span class="sxs-lookup"><span data-stu-id="19f12-121">hello following code demonstrates one method of changing hello operation-id-generation behavior.</span></span> <span data-ttu-id="19f12-122">código de Hello anexa el nombre de Id. de operación de toohello de nombres de parámetro.</span><span class="sxs-lookup"><span data-stu-id="19f12-122">hello code appends parameter names toohello operation id name.</span></span>  
   
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
2. <span data-ttu-id="19f12-123">En *App_Start\SwaggerConfig.cs* archivo, llamada hello `OperationFilter` método toocause Swashbuckle toouse ¡hello nueva `IOperationFilter` implementación.</span><span class="sxs-lookup"><span data-stu-id="19f12-123">In *App_Start\SwaggerConfig.cs* file, call hello `OperationFilter` method toocause Swashbuckle toouse hello new `IOperationFilter` implementation.</span></span>
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    <span data-ttu-id="19f12-124">Hola *SwaggerConfig.cs* archivo que se ha quitado por hello Swashbuckle NuGet paquete contiene muchos ejemplos de comentarios de los puntos de extensibilidad.</span><span class="sxs-lookup"><span data-stu-id="19f12-124">hello *SwaggerConfig.cs* file that is dropped in by hello Swashbuckle NuGet package contains many commented-out examples of extensibility points.</span></span> <span data-ttu-id="19f12-125">comentarios adicionales de Hello no se muestran aquí.</span><span class="sxs-lookup"><span data-stu-id="19f12-125">hello additional comments are not shown here.</span></span> 
   
    <span data-ttu-id="19f12-126">Después de realizar este cambio, su `IOperationFilter` implementación se usa y hace que toobe de Id. de operación único generado.</span><span class="sxs-lookup"><span data-stu-id="19f12-126">After you make this change, your `IOperationFilter` implementation is used and causes unique operation ids toobe generated.</span></span>
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a><span data-ttu-id="19f12-127">Permitir códigos de respuesta distintos de 200</span><span class="sxs-lookup"><span data-stu-id="19f12-127">Allow response codes other than 200</span></span>
<span data-ttu-id="19f12-128">De forma predeterminada, Swashbuckle se da por supuesto que una respuesta HTTP 200 (OK) es hello *sólo* legítimos respuesta desde un método de API Web.</span><span class="sxs-lookup"><span data-stu-id="19f12-128">By default, Swashbuckle assumes that an HTTP 200 (OK) response is hello *only* legitimate response from a Web API method.</span></span> <span data-ttu-id="19f12-129">En algunos casos, puede que desee tooreturn otros códigos de respuesta sin producir una excepción de hello cliente tooraise.</span><span class="sxs-lookup"><span data-stu-id="19f12-129">In some cases, you may want tooreturn other response codes without causing hello client tooraise an exception.</span></span>  <span data-ttu-id="19f12-130">Por ejemplo, hello Web API código siguiente muestra un escenario en el que desearía Hola cliente tooaccept 200 o 404 como las respuestas válidas.</span><span class="sxs-lookup"><span data-stu-id="19f12-130">For example, hello following Web API code demonstrates a scenario in which you would want hello client tooaccept either a 200 or a 404 as valid responses.</span></span>

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

<span data-ttu-id="19f12-131">En este escenario, hello Swagger que Swashbuckle genera de forma predeterminada especifica solo un código de estado HTTP legítimo, 200 de HTTP.</span><span class="sxs-lookup"><span data-stu-id="19f12-131">In this scenario, hello Swagger that Swashbuckle generates by default specifies only one legitimate HTTP status code, HTTP 200.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

<span data-ttu-id="19f12-132">Dado que Visual Studio utiliza hello toogenerate código de definición de Swagger API para los clientes de hello, crea el código de cliente que genera una excepción para todas las respuestas que no sea un HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="19f12-132">Since Visual Studio uses hello Swagger API definition toogenerate code for hello client, it creates client code that raises an exception for any response other than an HTTP 200.</span></span> <span data-ttu-id="19f12-133">código de Hello siguiente es desde un cliente de C# generado para este método de API Web de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="19f12-133">hello code below is from a C# client generated for this sample Web API method.</span></span>

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

<span data-ttu-id="19f12-134">Swashbuckle proporciona dos maneras de personalizar la lista de Hola de códigos de respuesta HTTP esperados que genera, mediante los comentarios XML o hello `SwaggerResponse` atributo.</span><span class="sxs-lookup"><span data-stu-id="19f12-134">Swashbuckle provides two ways of customizing hello list of expected HTTP response codes that it generates, using XML comments or hello `SwaggerResponse` attribute.</span></span> <span data-ttu-id="19f12-135">atributo de Hello es más fácil, pero solo está disponible en Swashbuckle 5.1.5 o posterior.</span><span class="sxs-lookup"><span data-stu-id="19f12-135">hello attribute is easier, but it is only available in Swashbuckle 5.1.5 or later.</span></span> <span data-ttu-id="19f12-136">plantilla de proyecto nuevo de vista previa de aplicaciones de API en Visual Studio 2013 Hello incluye Swashbuckle versión 5.0.0, por lo que si usa la plantilla de hello y no desea tooupdate Swashbuckle, la única opción es toouse los comentarios XML.</span><span class="sxs-lookup"><span data-stu-id="19f12-136">hello API Apps preview new-project template in Visual Studio 2013 includes Swashbuckle version 5.0.0, so if you used hello template and don't want tooupdate Swashbuckle, your only option is toouse XML comments.</span></span> 

### <a name="customize-expected-response-codes-using-xml-comments"></a><span data-ttu-id="19f12-137">Personalización de códigos de respuesta esperados mediante comentarios XML</span><span class="sxs-lookup"><span data-stu-id="19f12-137">Customize expected response codes using XML comments</span></span>
<span data-ttu-id="19f12-138">Use los códigos de respuesta de toospecify de este método si la versión de Swashbuckle es anterior a 5.1.5.</span><span class="sxs-lookup"><span data-stu-id="19f12-138">Use this method toospecify response codes if your Swashbuckle version is earlier than 5.1.5.</span></span>

1. <span data-ttu-id="19f12-139">En primer lugar, agregue comentarios de documentación XML frente a métodos de hello para que desea toospecify códigos de respuesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="19f12-139">First, add XML documentation comments over hello methods you wish toospecify HTTP response codes for.</span></span> <span data-ttu-id="19f12-140">Realizar la acción de API Web de ejemplo de Hola tooit de documentación de XML se muestra anteriormente y aplicar hello, se crearán en código como el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19f12-140">Taking hello sample Web API action shown above and applying hello XML documentation tooit would result in code like hello following example.</span></span> 
   
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
2. <span data-ttu-id="19f12-141">Agregar instrucciones de hello *SwaggerConfig.cs* toodirect Swashbuckle toomake uso del archivo de documentación XML Hola de archivos.</span><span class="sxs-lookup"><span data-stu-id="19f12-141">Add instructions in hello *SwaggerConfig.cs* file toodirect Swashbuckle toomake use of hello XML documentation file.</span></span>
   
   * <span data-ttu-id="19f12-142">Abra *SwaggerConfig.cs* y cree un método en hello *SwaggerConfig* archivo XML de documentación toohello de clase toospecify Hola ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="19f12-142">Open *SwaggerConfig.cs* and create a method on hello *SwaggerConfig* class toospecify hello path toohello documentation XML file.</span></span> 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * <span data-ttu-id="19f12-143">Desplácese hacia abajo en hello *SwaggerConfig.cs* archivo hasta que vea hello como comentario de línea de código similar al siguiente captura de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="19f12-143">Scroll down in hello *SwaggerConfig.cs* file until you see hello commented-out line of code resembling hello screen shot below.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * <span data-ttu-id="19f12-144">Quite el comentario de hello tooenable Hola XML comentarios de una línea de procesamiento durante la generación de Swagger.</span><span class="sxs-lookup"><span data-stu-id="19f12-144">Uncomment hello line tooenable hello XML comments processing during Swagger generation.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. <span data-ttu-id="19f12-145">En el archivo de documentación de XML de pedido toogenerate hello, vaya a propiedades del proyecto de Hola y habilitar el archivo de documentación XML de hello tal y como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="19f12-145">In order toogenerate hello XML documentation file, go into hello project's properties and enable hello XML documentation file as shown in hello screenshot below.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

<span data-ttu-id="19f12-146">Después de realizar estos pasos, hello Swagger texto JSON generado por Swashbuckle reflejará los códigos de respuesta HTTP de Hola que especificó en los comentarios XML Hola.</span><span class="sxs-lookup"><span data-stu-id="19f12-146">Once you perform these steps, hello Swagger JSON generated by Swashbuckle will reflect hello HTTP response codes that you specified in hello XML comments.</span></span> <span data-ttu-id="19f12-147">Hola de captura de pantalla siguiente muestra esta nueva carga JSON.</span><span class="sxs-lookup"><span data-stu-id="19f12-147">hello screenshot below demonstrates this new JSON payload.</span></span> 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

<span data-ttu-id="19f12-148">Cuando se usa código de cliente de Visual Studio tooregenerate hello para la API de REST, Hola código C# acepta ambos códigos de estado OK de HTTP y no se encuentra de hello sin generar una excepción, lo que sus decisiones de toomake código usado en cómo devolver toohandle Hola de un valor null Póngase en contacto con el registro.</span><span class="sxs-lookup"><span data-stu-id="19f12-148">When you use Visual Studio tooregenerate hello client code for your REST API, hello C# code accepts both hello HTTP OK and Not Found status codes without raising an exception, allowing your consuming code toomake decisions on how toohandle hello return of a null Contact record.</span></span> 

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

<span data-ttu-id="19f12-149">código de Hello para esta demostración se puede encontrar en [este repositorio de GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span><span class="sxs-lookup"><span data-stu-id="19f12-149">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span></span> <span data-ttu-id="19f12-150">Junto con la API Web de hello marcado con comentarios de documentación XML del proyecto es un proyecto de aplicación de consola que contenga a un cliente generado para esta API.</span><span class="sxs-lookup"><span data-stu-id="19f12-150">Along with hello Web API project marked up with XML documentation comments is a Console Application project that contains a generated client for this API.</span></span> 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a><span data-ttu-id="19f12-151">Personalizar los códigos de respuesta esperado con hello SwaggerResponse atributo</span><span class="sxs-lookup"><span data-stu-id="19f12-151">Customize expected response codes using hello SwaggerResponse attribute</span></span>
<span data-ttu-id="19f12-152">Hola [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) atributo está disponible en Swashbuckle 5.1.5 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="19f12-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribute is available in Swashbuckle 5.1.5 and later.</span></span> <span data-ttu-id="19f12-153">En caso de que tiene una versión anterior del proyecto, en esta sección se inicia mediante la explicación de cómo tooupdate hello Swashbuckle NuGet paquete para que puedan utilizar este atributo.</span><span class="sxs-lookup"><span data-stu-id="19f12-153">In case you have an earlier version in your project, this section starts by explaining how tooupdate hello Swashbuckle NuGet package so that you can use this attribute.</span></span>

1. <span data-ttu-id="19f12-154">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto de la API web y haga clic en **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="19f12-154">In **Solution Explorer**, right-click your Web API project and click **Manage NuGet Packages**.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. <span data-ttu-id="19f12-155">Haga clic en hello *actualización* botón siguiente toohello *Swashbuckle* paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="19f12-155">Click hello *Update* button next toohello *Swashbuckle* NuGet package.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. <span data-ttu-id="19f12-156">Agregar hello *SwaggerResponse* atributos toohello métodos de acción de API Web que se desea toospecify códigos de respuesta HTTP válidos.</span><span class="sxs-lookup"><span data-stu-id="19f12-156">Add hello *SwaggerResponse* attributes toohello Web API action methods for which you want toospecify valid HTTP response codes.</span></span> 
   
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
4. <span data-ttu-id="19f12-157">Agregar un `using` declaración de espacio de nombres del atributo de hello:</span><span class="sxs-lookup"><span data-stu-id="19f12-157">Add a `using` statement for hello attribute's namespace:</span></span>
   
        using Swashbuckle.Swagger.Annotations;
5. <span data-ttu-id="19f12-158">Examinar toohello */swagger/docs/v1* dirección URL de su proyecto y Hola serán visibles en varios códigos de respuesta HTTP Hola Swagger JSON.</span><span class="sxs-lookup"><span data-stu-id="19f12-158">Browse toohello */swagger/docs/v1* URL of your project and hello various HTTP response codes will be visible in hello Swagger JSON.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

<span data-ttu-id="19f12-159">código de Hello para esta demostración se puede encontrar en [este repositorio de GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span><span class="sxs-lookup"><span data-stu-id="19f12-159">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span></span> <span data-ttu-id="19f12-160">Junto con hello proyecto de API Web decorada con hello *SwaggerResponse* atributo es un proyecto de aplicación de consola que contiene un cliente generado para esta API.</span><span class="sxs-lookup"><span data-stu-id="19f12-160">Along with hello Web API project decorated with hello *SwaggerResponse* attribute is a Console Application project that contains a generated client for this API.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="19f12-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19f12-161">Next steps</span></span>
<span data-ttu-id="19f12-162">Este artículo le haya mostrado cómo forma de hello toocustomize Swashbuckle genera identificadores de operación y códigos de respuesta válido.</span><span class="sxs-lookup"><span data-stu-id="19f12-162">This article has shown how toocustomize hello way Swashbuckle generates operation ids and valid response codes.</span></span> <span data-ttu-id="19f12-163">Para obtener más información, consulte [Swashbuckle en GitHub](https://github.com/domaindrivendev/Swashbuckle).</span><span class="sxs-lookup"><span data-stu-id="19f12-163">For more information, see [Swashbuckle on GitHub](https://github.com/domaindrivendev/Swashbuckle).</span></span>

