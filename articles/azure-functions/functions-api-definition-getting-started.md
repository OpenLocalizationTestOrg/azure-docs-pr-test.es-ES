---
title: aaaGetting Started with OpenAPI Metadata en las funciones de Azure | Documentos de Microsoft
description: "Introducción a la compatibilidad con OpenAPI en Azure Functions"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="bfa05-103">Creación de OpenAPI 2.0 (Swagger) Metadata para una Function App (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="bfa05-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="bfa05-104">Este documento le guía a través del proceso paso a paso de Hola de creación de una definición de OpenAPI para una API sencilla que se hospedan en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfa05-104">This document guides you through hello step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="bfa05-105">¿Qué es OpenAPI (Swagger)?</span><span class="sxs-lookup"><span data-stu-id="bfa05-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="bfa05-106">[Metadatos de swagger](http://swagger.io/) es un archivo que define la funcionalidad de Hola y modos de la API de funcionamiento y permite hospedar un toobe de API de REST utilizado por una gran variedad de otro software a una función.</span><span class="sxs-lookup"><span data-stu-id="bfa05-106">[Swagger Metadata](http://swagger.io/) is a file that defines hello functionality and operating modes of your API, and allows a function hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="bfa05-107">Ofertas de Microsoft, como PowerApps y [aplicaciones de API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), así como herramientas como 3rd para el desarrollador entidad [Postman](https://www.getpostman.com/docs/importing_swagger) y [muchos más paquetes](http://swagger.io/tools/) todos permiten su toobe API consumida con una Definición de swagger.</span><span class="sxs-lookup"><span data-stu-id="bfa05-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API toobe consumed with a Swagger definition.</span></span>

## <span data-ttu-id="bfa05-108"><a name="prepare-function"></a>Creación de una instancia de Function con una API sencilla</span><span class="sxs-lookup"><span data-stu-id="bfa05-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="bfa05-109">una definición de OpenAPI toocreate, primero necesitamos toocreate una función con una API sencilla.</span><span class="sxs-lookup"><span data-stu-id="bfa05-109">toocreate an OpenAPI definition, we first need toocreate a Function with a simple API.</span></span> <span data-ttu-id="bfa05-110">Si ya tiene una API que se hospeda en una aplicación de la función, puede omitir toohello recta próxima sección</span><span class="sxs-lookup"><span data-stu-id="bfa05-110">If you already have an API hosted on a Function App, you can skip straight toohello next section</span></span>
1. <span data-ttu-id="bfa05-111">Cree una nueva instancia de Function App.</span><span class="sxs-lookup"><span data-stu-id="bfa05-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="bfa05-112">[Azure Portal](https://portal.azure.com) > `+ New` &gt; Busque "Function App"</span><span class="sxs-lookup"><span data-stu-id="bfa05-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="bfa05-113">Cree una nueva función de desencadenador HTTP dentro de la nueva instancia de Function App.</span><span class="sxs-lookup"><span data-stu-id="bfa05-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="bfa05-114">La función se rellena previamente con el código que define una API de REST muy sencilla.</span><span class="sxs-lookup"><span data-stu-id="bfa05-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="bfa05-115">Cualquier cadena que se pasa toohello función como un parámetro de consulta o en el cuerpo de Hola se devuelve como "Hello {entrada}"</span><span class="sxs-lookup"><span data-stu-id="bfa05-115">Any string passed toohello Function as a query parameter or in hello body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="bfa05-116">Vaya toohello `Integrate` ficha de la nueva función de desencadenador de HTTP</span><span class="sxs-lookup"><span data-stu-id="bfa05-116">Go toohello `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="bfa05-117">Alternar `Allowed HTTP methods` demasiado`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="bfa05-117">Toggle `Allowed HTTP methods` too`Selected methods`</span></span>
    1. <span data-ttu-id="bfa05-118">En `Selected HTTP methods` desactive todos los verbos excepto POST.</span><span class="sxs-lookup"><span data-stu-id="bfa05-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="bfa05-119">![Métodos HTTP seleccionados](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="bfa05-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="bfa05-120">Este paso simplificará la definición de la API más adelante.</span><span class="sxs-lookup"><span data-stu-id="bfa05-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="bfa05-121"><a name="enable"></a>Habilitación de compatibilidad de definición de la API</span><span class="sxs-lookup"><span data-stu-id="bfa05-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="bfa05-122">Navegue demasiado`your function name` > `Platform Features` > `API Definition`
![ficha Definición](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="bfa05-122">Navigate too`your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="bfa05-123">Establecer `API Definition Source` demasiado`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="bfa05-123">Set `API Definition Source` too`Function (preview)`</span></span>
    1. <span data-ttu-id="bfa05-124">Este paso permite que un conjunto de opciones de OpenAPI para la aplicación de función, incluido un toohost de punto de conexión un archivo OpenAPI de dominio de la aplicación de la función, una copia en línea del programa Hola a [OpenAPI Editor](http://editor.swagger.io)y un generador de definición de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="bfa05-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint toohost an OpenAPI file from your Function App's domain, an inline copy of hello [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="bfa05-125">![Definición habilitada](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="bfa05-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="bfa05-126"><a name="create-definition"></a>Creación de la definición de la API desde una plantilla</span><span class="sxs-lookup"><span data-stu-id="bfa05-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="bfa05-127">Haga clic en `Generate API Definition template`</span><span class="sxs-lookup"><span data-stu-id="bfa05-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="bfa05-128">Este paso examina la aplicación de función para las funciones de desencadenador de HTTP y usa información de hello en functions.json toogenerate un documento de OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="bfa05-128">This step scans your Function App for HTTP Trigger functions and uses hello info in functions.json toogenerate an OpenAPI document.</span></span>
1. <span data-ttu-id="bfa05-129">Agregar un objeto de la operación demasiado`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="bfa05-129">Add an operation object too`paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="bfa05-130">documento de OpenAPI de inicio rápido de Hello es un esquema de un documento de OpenAPI completo. Se necesita más metadatos toobe una definición completa de OpenAPI, como objetos de operación y las plantillas de respuesta.</span><span class="sxs-lookup"><span data-stu-id="bfa05-130">hello quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata toobe a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="bfa05-131">objeto de operación de ejemplo de Hola a continuación tiene una forma rellena sección genera o consume, un objeto de parámetro y un objeto de respuesta.</span><span class="sxs-lookup"><span data-stu-id="bfa05-131">hello sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  <span data-ttu-id="bfa05-132">x-ms-resumen proporciona un nombre para mostrar en Logic Apps, Flow y PowerApps.</span><span class="sxs-lookup"><span data-stu-id="bfa05-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="bfa05-133">Extraer del repositorio [personalizar la definición de Swagger para PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn más.</span><span class="sxs-lookup"><span data-stu-id="bfa05-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn more.</span></span>

1. <span data-ttu-id="bfa05-134">Haga clic en `save` toosave los cambios ![agregar la definición de plantilla](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="bfa05-134">Click `save` toosave your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="bfa05-135"><a name="use-definition"></a>Uso de su definición de API</span><span class="sxs-lookup"><span data-stu-id="bfa05-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="bfa05-136">Copia la `API definition URL` y péguelo en un nuevo tooview pestaña de explorador del documento OpenAPI sin formato.</span><span class="sxs-lookup"><span data-stu-id="bfa05-136">Copy your `API definition URL` and paste it into a new browser tab tooview your raw OpenAPI document.</span></span>
1. <span data-ttu-id="bfa05-137">Puede importar el número de tooany de documento OpenAPI de herramientas para pruebas e integración con esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="bfa05-137">You can import your OpenAPI document tooany number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="bfa05-138">Muchos recursos de Azure son importación pueda tooautomatically del documento OpenAPI mediante Hola dirección URL de la definición de API que se guarda en la configuración de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="bfa05-138">Many Azure resources are able tooautomatically import your OpenAPI doc using hello API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="bfa05-139">Como parte de hello `Function` origen de la definición de API, actualizamos esa dirección url para usted.</span><span class="sxs-lookup"><span data-stu-id="bfa05-139">As a part of hello `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="bfa05-140"><a name="test-definition"></a>Con la definición de API de hello tootest de interfaz de usuario de Swagger</span><span class="sxs-lookup"><span data-stu-id="bfa05-140"><a name="test-definition"></a>Using hello Swagger UI tootest your API definition</span></span>
<span data-ttu-id="bfa05-141">Prueban herramientas integradas en la vista de la interfaz de usuario de toohello del editor de definición de API de hello incrustada.</span><span class="sxs-lookup"><span data-stu-id="bfa05-141">There are testing tools built in toohello UI view of hello imbedded API definition editor.</span></span> <span data-ttu-id="bfa05-142">Agregar la clave de API y, a continuación, usar hello `Try this operation` botón en cada método.</span><span class="sxs-lookup"><span data-stu-id="bfa05-142">Add your API key, and then use hello `Try this operation` button under each method.</span></span> <span data-ttu-id="bfa05-143">herramienta de Hello usará las solicitudes de definición de la API tooformat hello y respuestas correctas se indicarán que la definición es correcta.</span><span class="sxs-lookup"><span data-stu-id="bfa05-143">hello tool will use your API Definition tooformat hello requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="bfa05-144">Pasos:</span><span class="sxs-lookup"><span data-stu-id="bfa05-144">Steps:</span></span>

1. <span data-ttu-id="bfa05-145">Copie la clave de API de la función.</span><span class="sxs-lookup"><span data-stu-id="bfa05-145">Copy your function API key</span></span>
    1. <span data-ttu-id="bfa05-146">clave de API de Hello puede encontrarse en la función de activación HTTP en `function name` > `Keys` > `Function Keys` 
   ![tecla de función](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="bfa05-146">hello API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="bfa05-147">Navegue toohello `API Definition` página.</span><span class="sxs-lookup"><span data-stu-id="bfa05-147">Navigate toohello `API Definition` page.</span></span>
    1. <span data-ttu-id="bfa05-148">Haga clic en `Authenticate` y agregue el objeto de seguridad de toohello clave de API de función en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfa05-148">Click `Authenticate` and add your Function API key toohello security object at hello top.</span></span>
  <span data-ttu-id="bfa05-149">![Clave de OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="bfa05-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="bfa05-150">Seleccione `/api/yourfunctionroute` > `POST`.</span><span class="sxs-lookup"><span data-stu-id="bfa05-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="bfa05-151">Haga clic en `Try it out` y escriba un nombre tootest</span><span class="sxs-lookup"><span data-stu-id="bfa05-151">Click `Try it out` and enter a name tootest</span></span>
1. <span data-ttu-id="bfa05-152">Debería ver un resultado SUCCESS en `Pretty` 
 ![prueba de definición de la API](./media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="bfa05-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfa05-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfa05-153">Next steps</span></span>
* [<span data-ttu-id="bfa05-154">Definición de OpenAPI en información general de Functions</span><span class="sxs-lookup"><span data-stu-id="bfa05-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="bfa05-155">Lea la documentación completa de Hola para obtener más información sobre la compatibilidad con OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="bfa05-155">Read hello full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="bfa05-156">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="bfa05-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="bfa05-157">contiene las referencias del programador para codificar funciones y definir desencadenadores y enlaces.</span><span class="sxs-lookup"><span data-stu-id="bfa05-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="bfa05-158">Repositorio de GitHub de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="bfa05-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="bfa05-159">¡Extraer del repositorio Hola funciones GitHub toogive nos comentarios en vista previa de compatibilidad de definición de API de Hola!</span><span class="sxs-lookup"><span data-stu-id="bfa05-159">Check out hello Functions GitHub toogive us feedback on hello API definition support preview!</span></span> <span data-ttu-id="bfa05-160">Asegúrese de un problema de GitHub para cualquier elemento que le gustaría toosee actualizado.</span><span class="sxs-lookup"><span data-stu-id="bfa05-160">Make a GitHub issue for anything you'd like toosee updated.</span></span>
