---
title: metadatos de aaaOpenAPI en las funciones de Azure | Documentos de Microsoft
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
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a>Compatibilidad con metadatos de OpenAPI 2.0 en Azure Functions (versión preliminar)
2.0 OpenAPI (anteriormente Swagger) compatibilidad de metadatos en las funciones de Azure es una característica de vista previa que puede usar definición de toowrite un 2.0 OpenAPI dentro de una aplicación de la función. A continuación, puede hospedar ese archivo mediante el uso de la aplicación de la función de hello.

[Metadatos de OpenAPI](http://swagger.io/) permite a una función que hospeda una API de REST toobe utilizado por una gran variedad de otro software. Este software incluye ofertas de Microsoft como hello y PowerApps [característica de aplicaciones de API de servicio de aplicaciones de Azure](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), herramientas de desarrollo de aplicaciones de terceros, como [Postman](https://www.getpostman.com/docs/importing_swagger), y [muchos más paquetes](http://swagger.io/tools/).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
>Se recomienda empezar por hello [tutorial de introducción](./functions-api-definition-getting-started.md) y, a continuación, devolver toothis documento toolearn más información sobre características específicas.

## <a name="enable"></a>Habilitar la compatibilidad con definiciones de OpenAPI
Puede configurar todas las configuraciones de OpenAPI en hello **definición de la API** página de la aplicación de la función **características de la plataforma**.

generación de hello tooenable de una definición de OpenAPI hospedada y una definición de inicio rápido, establezca **origen de la definición de API** demasiado**función (vista previa)**. **Dirección URL externa** permite a la función toouse una definición de OpenAPI que ha hospedado en otro lugar.

## <a name="generate-definition"></a>Generación de un esqueleto de Swagger a partir de los metadatos de la función.
Una plantilla puede ayudarle a empezar a escribir la primera definición de OpenAPI. característica de plantilla de definición de Hello crea una definición de OpenAPI dispersa mediante todos los metadatos de Hola Hola function.json archivo para cada una de las funciones de desencadenador HTTP. Necesitará toofill en obtener más información sobre la API de hello [OpenAPI especificación](http://swagger.io/specification/), como las plantillas de solicitud y respuesta.

Para obtener instrucciones detalladas, consulte hello [tutorial de introducción](./functions-api-definition-getting-started.md).

### <a name="templates"></a>Plantillas disponibles

|Nombre| Descripción |
|:-----|:-----|
|Definición generada|Una definición de OpenAPI con la cantidad máxima de Hola de información que puede deducirse de metadatos existentes de la función hello.|

### <a name="quickstart-details"></a>Genera los metadatos incluyen Hola definición

Hola después de la tabla representa Hola configuración del portal de Azure y los datos correspondientes en function.json porque está asignada toohello genera Swagger esqueleto.

|Swagger.json|IU del portal|Function.json|
|:----|:-----|:-----|
|[Host](http://swagger.io/specification/#fixed-fields-15)|**Configuración de Function App** > **Configuración de App Service** > **Información general** > **Dirección URL**|*No presente*
|[Paths](http://swagger.io/specification/#paths-object-29)|**Integrar** > **Métodos HTTP seleccionados**|Bindings: Route
|[Path Item](http://swagger.io/specification/#path-item-object-32)|**Integrar** > **Plantilla de ruta**|Bindings: Methods
|[Seguridad](http://swagger.io/specification/#security-scheme-object-112)|**Claves**|*No presente*|
|operationID*|**Ruta + verbos permitidos**|Ruta + verbos permitidos|

\*Id. de operación de Hello solo es necesario para integrar con PowerApps y el flujo.
> [!NOTE]
> extensión de x-ms-summary Hola proporciona un nombre para mostrar en las aplicaciones lógicas, PowerApps y el flujo.
>
> más información, consulte toolearn [personalizar la definición de Swagger para PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).

## <a name="CICD"></a>Usar definición de elemento de configuración/CD tooset una API

 Debe habilitar el API definición hospedaje en el portal de hello antes de habilitar toomodify de control de código fuente de la definición de la API de control de código fuente. Siga estas instrucciones:

1. Examinar demasiado**(vista previa) de la definición de API** en la configuración de aplicación de la función.
  1. Establecer **origen de la definición de API** demasiado**función**.
  1. Haga clic en **plantilla de definición de API generar** y, a continuación, **guardar** toocreate una definición de plantilla para modificar más adelante.
  1. Tome nota de la dirección URL de la definición de API y la clave.
1. [Configurar la integración continua e implementación continua (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).
2. Modifique swagger.json en control de código fuente en \site\wwwroot\.azurefunctions\swagger\swagger.json.

Ahora, los cambios tooswagger.json en el repositorio están hospedados por la aplicación de la función en la dirección URL de definición de hello API y la clave que anotó en el paso 1.

## <a name="next-steps"></a>Pasos siguientes
* [Tutorial de inicio](functions-api-definition-getting-started.md). Pruebe nuestro toosee tutorial una definición de OpenAPI en acción.
* [Repositorio de GitHub de Azure Functions](https://github.com/Azure/Azure-Functions/). Extraer del repositorio Hola funciones repositorio toogive nos comentarios en vista previa de compatibilidad de definición de hello API. Asegúrese de un problema de GitHub para el que desee toosee actualizado.
* [Referencia para desarrolladores de Azure Functions](functions-reference.md). Obtenga información sobre la codificación de funciones y la definición de desencadenadores y enlaces.
