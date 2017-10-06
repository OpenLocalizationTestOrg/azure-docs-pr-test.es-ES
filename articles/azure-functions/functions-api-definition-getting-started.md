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
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>Creación de OpenAPI 2.0 (Swagger) Metadata para una Function App (versión preliminar)

Este documento le guía a través del proceso paso a paso de Hola de creación de una definición de OpenAPI para una API sencilla que se hospedan en las funciones de Azure.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>¿Qué es OpenAPI (Swagger)?
[Metadatos de swagger](http://swagger.io/) es un archivo que define la funcionalidad de Hola y modos de la API de funcionamiento y permite hospedar un toobe de API de REST utilizado por una gran variedad de otro software a una función. Ofertas de Microsoft, como PowerApps y [aplicaciones de API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), así como herramientas como 3rd para el desarrollador entidad [Postman](https://www.getpostman.com/docs/importing_swagger) y [muchos más paquetes](http://swagger.io/tools/) todos permiten su toobe API consumida con una Definición de swagger.

## <a name="prepare-function"></a>Creación de una instancia de Function con una API sencilla
  una definición de OpenAPI toocreate, primero necesitamos toocreate una función con una API sencilla. Si ya tiene una API que se hospeda en una aplicación de la función, puede omitir toohello recta próxima sección
1. Cree una nueva instancia de Function App.
    1. [Azure Portal](https://portal.azure.com) > `+ New` &gt; Busque "Function App"
1. Cree una nueva función de desencadenador HTTP dentro de la nueva instancia de Function App.
    1. La función se rellena previamente con el código que define una API de REST muy sencilla.
    1. Cualquier cadena que se pasa toohello función como un parámetro de consulta o en el cuerpo de Hola se devuelve como "Hello {entrada}"
1. Vaya toohello `Integrate` ficha de la nueva función de desencadenador de HTTP
    1. Alternar `Allowed HTTP methods` demasiado`Selected methods`
    1. En `Selected HTTP methods` desactive todos los verbos excepto POST.
    ![Métodos HTTP seleccionados](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. Este paso simplificará la definición de la API más adelante.

## <a name="enable"></a>Habilitación de compatibilidad de definición de la API
1. Navegue demasiado`your function name` > `Platform Features` > `API Definition`
![ficha Definición](./media/functions-api-definition-getting-started/definitiontab.png)
1. Establecer `API Definition Source` demasiado`Function (preview)`
    1. Este paso permite que un conjunto de opciones de OpenAPI para la aplicación de función, incluido un toohost de punto de conexión un archivo OpenAPI de dominio de la aplicación de la función, una copia en línea del programa Hola a [OpenAPI Editor](http://editor.swagger.io)y un generador de definición de inicio rápido.
![Definición habilitada](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>Creación de la definición de la API desde una plantilla
1. Haga clic en `Generate API Definition template`
    1. Este paso examina la aplicación de función para las funciones de desencadenador de HTTP y usa información de hello en functions.json toogenerate un documento de OpenAPI.
1. Agregar un objeto de la operación demasiado`paths: /api/yourfunctionroute post:`
    1. documento de OpenAPI de inicio rápido de Hello es un esquema de un documento de OpenAPI completo. Se necesita más metadatos toobe una definición completa de OpenAPI, como objetos de operación y las plantillas de respuesta.
    1. objeto de operación de ejemplo de Hola a continuación tiene una forma rellena sección genera o consume, un objeto de parámetro y un objeto de respuesta.
    
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
    >  x-ms-resumen proporciona un nombre para mostrar en Logic Apps, Flow y PowerApps.
    >
    > Extraer del repositorio [personalizar la definición de Swagger para PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn más.

1. Haga clic en `save` toosave los cambios ![agregar la definición de plantilla](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>Uso de su definición de API
1. Copia la `API definition URL` y péguelo en un nuevo tooview pestaña de explorador del documento OpenAPI sin formato.
1. Puede importar el número de tooany de documento OpenAPI de herramientas para pruebas e integración con esa dirección URL.
    1. Muchos recursos de Azure son importación pueda tooautomatically del documento OpenAPI mediante Hola dirección URL de la definición de API que se guarda en la configuración de la aplicación de función. Como parte de hello `Function` origen de la definición de API, actualizamos esa dirección url para usted.


## <a name="test-definition"></a>Con la definición de API de hello tootest de interfaz de usuario de Swagger
Prueban herramientas integradas en la vista de la interfaz de usuario de toohello del editor de definición de API de hello incrustada. Agregar la clave de API y, a continuación, usar hello `Try this operation` botón en cada método. herramienta de Hello usará las solicitudes de definición de la API tooformat hello y respuestas correctas se indicarán que la definición es correcta.

### <a name="steps"></a>Pasos:

1. Copie la clave de API de la función.
    1. clave de API de Hello puede encontrarse en la función de activación HTTP en `function name` > `Keys` > `Function Keys` 
   ![tecla de función](./media/functions-api-definition-getting-started/functionkey.png)
1. Navegue toohello `API Definition` página.
    1. Haga clic en `Authenticate` y agregue el objeto de seguridad de toohello clave de API de función en la parte superior de Hola.
  ![Clave de OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. Seleccione `/api/yourfunctionroute` > `POST`.
1. Haga clic en `Try it out` y escriba un nombre tootest
1. Debería ver un resultado SUCCESS en `Pretty` 
 ![prueba de definición de la API](./media/functions-api-definition-getting-started/definitionTest.png)

## <a name="next-steps"></a>Pasos siguientes
* [Definición de OpenAPI en información general de Functions](functions-api-definition.md)
  * Lea la documentación completa de Hola para obtener más información sobre la compatibilidad con OpenAPI.
* [Azure Functions developer reference](functions-reference.md)  
  * contiene las referencias del programador para codificar funciones y definir desencadenadores y enlaces.
* [Repositorio de GitHub de Azure Functions](https://github.com/Azure/Azure-Functions/)
  * ¡Extraer del repositorio Hola funciones GitHub toogive nos comentarios en vista previa de compatibilidad de definición de API de Hola! Asegúrese de un problema de GitHub para cualquier elemento que le gustaría toosee actualizado.
