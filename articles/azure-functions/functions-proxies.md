---
title: aaaWork con servidores proxy en las funciones de Azure | Documentos de Microsoft
description: "Información general sobre cómo toouse servidores proxy de las funciones de Azure"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a>Uso de Azure Functions Proxies (versión preliminar)

> [!NOTE] 
> Azure Functions Proxies actualmente se encuentra disponible en versión preliminar. Es gratuito, mientras que en la vista previa, pero las funciones estándar facturación aplica tooproxy ejecuciones. Para más información, consulte los [precios de Azure Functions](https://azure.microsoft.com/pricing/details/functions/).

Este artículo se explica cómo tooconfigure y trabajar con servidores proxy de las funciones de Azure. Con esta característica, puede especificar puntos de conexión en su aplicación de función que se implementan con otro recurso. Puede utilizar estos servidores proxy toobreak una API grande en varias aplicaciones de función (como en una arquitectura de microservicio), mientras que presenta una superficie de API única para los clientes.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <a name="enable"></a>Habilitación de Azure Functions Proxies

Los servidores proxy no están habilitados de forma predeterminada. Puede crear a servidores proxy mientras Hola característica está deshabilitada, pero no ejecutará. servidores proxy tooenable, Hola siguientes:

1. Abra hello [portal de Azure], y, a continuación, vaya tooyour función aplicación.
2. Seleccione **Configuración de Function App**.
3. Conmutador **Habilitar proxy de funciones de Azure (vista previa)** demasiado**en**.

También puede devolver aquí en tiempo de ejecución de tooupdate Hola proxy nuevas características estén disponibles.


## <a name="create"></a>Creación de un proxy

Esta sección muestra cómo toocreate un proxy en Hola portal de funciones.

1. Abra hello [portal de Azure], y, a continuación, vaya tooyour función aplicación.
2. En el panel izquierdo de hello, seleccione **nuevo proxy**.
3. Proporcione un nombre para el proxy.
4. Configurar el punto de conexión de Hola que se expone en esta aplicación de función mediante la especificación de hello **plantilla de ruta** y **métodos HTTP**. Estos parámetros comportan correspondiente reglas toohello para [HTTP desencadenadores].
5. Conjunto hello **dirección URL de back-end** tooanother punto de conexión. El punto de conexión podría tratarse de una función en otra aplicación de función o podría ser cualquier otra API. Hello valor no necesita toobe estático, y puede hacer referencia a [configuración de la aplicación] y [parámetros de solicitud de cliente original hello].
6. Haga clic en **Crear**.

El proxy ahora existe como un nuevo punto de conexión en la Function App. Desde una perspectiva de cliente, es equivalente tooan HttpTrigger en las funciones de Azure. Puede probar el nuevo proxy copiando Hola dirección URL del Proxy y probarlo con el cliente HTTP favorito.

## <a name="modify-requests-responses"></a>Modificación de solicitudes y respuestas

Con servidores proxy de las funciones de Azure, puede modificar las respuestas de tooand de las solicitudes de back-end de Hola. Estas transformaciones pueden usar variables, como se define en [Uso de variables].

### <a name="modify-backend-request"></a>Modificar la solicitud de back-end de Hola

De forma predeterminada, solicitud de back-end de Hola se inicializa como una copia de la solicitud original Hola. Además toosetting Hola back-end URL, puede hacer cambios toohello HTTP método, encabezados y parámetros de cadena de consulta. Hello los valores modificados pueden hacer referencia a [configuración de la aplicación] y [parámetros de solicitud de cliente original hello].

Actualmente, no existe ninguna experiencia de portal para modificar las solicitudes de back-end. toolearn tooapply esta capacidad a proxies.json, vea [definir un objeto requestOverrides].

### <a name="modify-response"></a>Modificar respuesta Hola

De forma predeterminada, se inicializa respuesta del cliente hello como una copia de la respuesta de back-end de Hola. Puede realizar el código de estado de la respuesta de toohello de cambios, motivo, encabezados y cuerpo. Hello los valores modificados pueden hacer referencia a [configuración de la aplicación], [parámetros de solicitud de cliente original hello], y [parámetros de respuesta de back-end de hello].

Actualmente, no existe ninguna experiencia de portal para modificar respuestas. toolearn tooapply esta capacidad a proxies.json, vea [definir un objeto responseOverrides].

## <a name="using-variables"></a>Uso de variables

configuración de Hola para un servidor proxy no es necesario toobe estático. Puede condición toouse variables de solicitud original hello, respuesta de back-end de Hola o configuración de la aplicación.

### <a name="request-parameters"></a>Referencia a los parámetros de solicitud

Puede usar los parámetros de solicitud, las entradas de la propiedad de dirección URL de back-end de toohello o como parte de la modificación de las solicitudes y respuestas. Pueden enlazar algunos parámetros de plantilla de ruta de Hola que se especifica en la configuración de proxy base hello y otros usuarios pueden proceder de propiedades de solicitud entrante de Hola.

#### <a name="route-template-parameters"></a>Parámetros de plantilla de ruta
Parámetros que se usan en la plantilla de ruta de hello son toobe disponible al que hace referencia por su nombre. los nombres de parámetro Hello están entre llaves ({}).

Por ejemplo, si un proxy tiene una plantilla de ruta, como `/pets/{petId}`, dirección URL de back-end de hello puede incluir el valor de Hola de `{petId}`, como en `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`. Si plantilla de ruta de hello finaliza en un carácter comodín, como `/api/{*restOfPath}`, Hola valor `{restOfPath}` es una representación de cadena de hello restantes segmentos de ruta de acceso de solicitud entrante de Hola.

#### <a name="additional-request-parameters"></a>Parámetros de solicitud adicionales
Además toohello enrutar parámetros de plantilla, Hola después de valores se puede utilizar en valores de configuración:

* **{request.method}** : Hola método HTTP que se usa en la solicitud original Hola.
* **{request.headers. \<HeaderName\>}**: un encabezado que se puede leer desde la solicitud original Hola. Reemplace  *\<HeaderName\>*  con nombre hello del encabezado de Hola que desea tooread. Si no se incluye el encabezado de hello en solicitud de hello, el valor de hello será una cadena vacía Hola.
* **{request.querystring. \<ParameterName\>}**: un parámetro de cadena de consulta que se puede leer desde la solicitud original Hola. Reemplace  *\<ParameterName\>*  con nombre de Hola de parámetro de Hola que desea tooread. Si no se incluye el parámetro hello en solicitud de hello, el valor de hello será una cadena vacía Hola.

### <a name="response-parameters"></a>Referencia a parámetros de respuesta de back-end

Parámetros de respuesta pueden utilizarse como parte de la modificación de cliente de toohello de respuesta de Hola. Hola después valores puede utilizarse en los valores de configuración:

* **{backend.response.statusCode}** : Hola código de estado HTTP que se devuelve en la respuesta de back-end de Hola.
* **{backend.response.statusReason}** : oración de motivo Hola HTTP que se devuelve en la respuesta de back-end de Hola.
* **{backend.response.headers. \<HeaderName\>}**: un encabezado que puede leerse de respuesta de back-end de Hola. Reemplace  *\<HeaderName\>*  con el nombre de hello del encabezado de hello desea tooread. Si no se incluye el encabezado de hello en solicitud de hello, el valor de hello será una cadena vacía Hola.

### <a name="use-appsettings"></a>Referencia a la configuración de la aplicación

También puede hacer referencia a [configuración de la aplicación definida para la aplicación de la función de hello](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) rodeando el nombre de la configuración de hello con signos de porcentaje (%).

Por ejemplo, una URL de back-end de *https://%ORDER_PROCESSING_HOST%/api/orders* tendría "% ORDER_PROCESSING_HOST %" Reemplazar con valor de Hola de configuración de ORDER_PROCESSING_HOST de Hola.

> [!TIP] 
> Use la configuración de la aplicación para hosts back-end si tiene varias implementaciones o entornos de prueba. De este modo, puede asegurarse de que siempre están hablando toohello vuelta end para ese entorno.

## <a name="advanced-configuration"></a>Configuración avanzada

servidores proxy de Hola que configure se almacena en un archivo proxies.json, que se encuentra en la raíz de Hola de un directorio de aplicación de la función. Puede editar este archivo manualmente e implementar como parte de la aplicación cuando se utiliza cualquiera de hello [métodos de implementación](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) compatible con las funciones. característica de Hello debe ser [habilitado](#enable) para hello archivo toobe procesado. 

> [!TIP] 
> Si no configuró uno de los métodos de implementación de hello, también puede trabajar con archivos de proxies.json hello en el portal de Hola. Aplicación de función vaya tooyour, seleccione **características de la plataforma**y, a continuación, seleccione **Editor de aplicación de servicio**. Al hacerlo, puede ver Hola estructura de archivo completo de la aplicación de la función y, a continuación, realizar cambios.

El archivo proxies.json lo define un objeto de servidores proxy, compuesto de servidores proxy con nombre y de sus definiciones. De forma opcional, si el editor lo admite, puede hacer referencia a un [esquema JSON](http://json.schemastore.org/proxies) para completar el código. Un archivo de ejemplo podría ser similar Hola siguiente:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

Cada proxy tiene un nombre descriptivo, como *proxy1* en el anterior ejemplo de Hola. objeto de definición de proxy correspondiente de Hola se define mediante Hola propiedades siguientes:

* **matchCondition**: obligatorio: un objeto que define las solicitudes de Hola que desencadenan la ejecución de Hola de este proxy. Contiene dos propiedades compartidas con los [HTTP desencadenadores]:
    * _métodos_: una matriz de los métodos de hello HTTP que Hola proxy responde a. Si no se especifica, el proxy de Hola responde tooall métodos HTTP en la ruta de Hola.
    * _ruta_: obligatorio: define la plantilla de ruta de hello, controlar que las direcciones URL de solicitud es el proxy responde a. A diferencia de los desencadenadores HTTP, no hay ningún valor predeterminado.
* **backendUri**: dirección URL de Hola Hola back-end toowhich Hola de solicitud de recursos debe ser procesadas por el proxy. Este valor puede hacer referencia a configuración de la aplicación y los parámetros de solicitud de cliente original Hola. Si no se incluye esta propiedad, Azure Functions responde con el mensaje HTTP 200 - Correcto.
* **requestOverrides**: un objeto que define la solicitud de transformaciones toohello back-end. Consulte [definir un objeto requestOverrides].
* **responseOverrides**: un objeto que define la respuesta del cliente de toohello de transformaciones. Consulte [definir un objeto responseOverrides].

> [!NOTE] 
> propiedad de ruta de Hello servidores proxy de las funciones de Azure no respeta la propiedad de hello routePrefix de configuración de host de las funciones de Hola. Si desea tooinclude un prefijo, como/API, se deben incluirse en la propiedad de ruta de Hola.

### <a name="requestOverrides"></a>Definición de un objeto requestOverrides

objeto de Hello requestOverrides define cambios que realizó la solicitud de toohello cuando se llama a recursos de back-end de Hola. objeto de Hola se define por hello propiedades siguientes:

* **backend.Request.Method**: Hola método HTTP que se ha utilizado toocall Hola back-end.
* **backend.Request.QueryString. \<ParameterName\>**: un parámetro de cadena de consulta que se pueden establecer para hello llamada toohello back-end. Reemplace  *\<ParameterName\>*  con nombre de Hola de parámetro de Hola que desea tooset. Si se proporciona una cadena vacía hello, parámetro hello no se incluye en la solicitud de back-end de Hola.
* **backend.Request.Headers. \<HeaderName\>**: un encabezado que se pueden establecer para hello llamada toohello back-end. Reemplace  *\<HeaderName\>*  con nombre hello del encabezado de Hola que desea tooset. Si proporciona una cadena vacía hello, encabezado de hello no se incluye en la solicitud de back-end de Hola.

Valores pueden hacer referencia a configuración de la aplicación y los parámetros de solicitud de cliente original Hola.

Una configuración de ejemplo podría ser similar Hola siguiente:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <a name="responseOverrides"></a>Definición de un objeto responseOverrides

objeto requestOverrides de Hello define cambios que se realizan respuesta toohello que transcurrió a cliente toohello atrás. objeto de Hola se define por hello propiedades siguientes:

* **response.statusCode**: toobe de código de estado HTTP de hello devuelve toohello cliente.
* **response.statusReason**: Hola HTTP motivo frase toobe devuelve toohello cliente.
* **Response.Body**: representación de cadena de Hola de hello cuerpo toobe devuelve toohello cliente.
* **Response.Headers. \<HeaderName\>**: un encabezado que puede establecer para hello respuesta toohello. Reemplace  *\<HeaderName\>*  con nombre hello del encabezado de Hola que desea tooset. Si proporciona una cadena vacía hello, encabezado de hello no se incluye en la respuesta de Hola.

Valores pueden hacer referencia a configuración de la aplicación, los parámetros de solicitud de cliente original de Hola y los parámetros de respuesta de back-end de Hola.

Una configuración de ejemplo podría ser similar Hola siguiente:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> En este ejemplo, el cuerpo de hello es que se va a establecer directamente, por lo que no `backendUri` propiedad es necesaria. ejemplo de Hola muestra cómo puede usar a servidores proxy de las funciones de Azure para las API de simulación.

[portal de Azure]: https://portal.azure.com
[HTTP desencadenadores]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[definir un objeto requestOverrides]: #requestOverrides
[definir un objeto responseOverrides]: #responseOverrides
[configuración de la aplicación]: #use-appsettings
[Uso de variables]: #using-variables
[parámetros de solicitud de cliente original hello]: #request-parameters
[parámetros de respuesta de back-end de hello]: #response-parameters
