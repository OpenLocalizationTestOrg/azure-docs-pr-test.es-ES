---
title: aaaCreate una API sin servidor mediante las funciones de Azure | Documentos de Microsoft
description: "¿Cómo toocreate una API sin servidor mediante las funciones de Azure"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Creación de una API sin servidor mediante Azure Functions

En este tutorial, aprenderá cómo las funciones de Azure permite toobuild API altamente escalable. Las funciones de Azure incluye una colección de integrados desencadenadores HTTP y los enlaces que sea fácil tooauthor un punto de conexión en una variedad de lenguajes, como Node.JS, C# y mucho más. En este tutorial, va a personalizar una acción específica de HTTP desencadenador toohandle en el diseño de la API. También va a prepararse para ampliar su API integrándola con Servidores proxy de Azure Functions y configurando API simuladas. Todo esto se logra encima de entorno Hola funciones sin servidor proceso, por lo que no tiene tooworry acerca de cómo escalar recursos, puede centrarse simplemente en la lógica de la API.

## <a name="prerequisites"></a>Requisitos previos 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

función resultante Hola se usará para el resto de Hola de este tutorial.

### <a name="sign-in-tooazure"></a>Inicie sesión en tooAzure

Hola abrir portal de Azure. toodo esto, inicie sesión en demasiado[https://portal.azure.com](https://portal.azure.com) con su cuenta de Azure.

## <a name="customize-your-http-function"></a>Personalización de la función HTTP

De forma predeterminada, la función desencadena HTTP está configurado tooaccept cualquier método HTTP. También hay una dirección URL predeterminada del formulario de hello `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`. Si ha seguido inicio rápido de hello, a continuación, `<funcname>` probablemente es algo parecido a "HttpTriggerJS1". En esta sección, modificará las solicitudes de toorespond tooGET solo función de Hola a `/api/hello` enrutar en su lugar. 

Navegar por función tooyour Hola portal de Azure. Seleccione **integrar** Hola barra de navegación izquierda.

![Personalización de una función HTTP](./media/functions-create-serverless-api/customizing-http.png)

Use la configuración de desencadenador HTTP como se especifica en la tabla de Hola.

| Campo | Valor de ejemplo | Descripción |
|---|---|---|
| Métodos HTTP permitidos | Métodos seleccionados | Determina los métodos HTTP que pueden ser tooinvoke usa esta función |
| Métodos HTTP seleccionados | GET | Permite solo toobe de métodos HTTP seleccionado utiliza tooinvoke esta función |
| Plantilla de ruta | /hello | Determina qué ruta es tooinvoke usa esta función |

Tenga en cuenta que no incluía hello `/api` base prefijo de ruta de acceso en la plantilla de ruta de hello, tal y como esto se controla mediante una configuración global.

Haga clic en **Guardar**.

Puede aprender más sobre cómo personalizar funciones HTTP en [Enlaces HTTP y webhook en Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).

### <a name="test-your-api"></a>Prueba de la API

A continuación, pruebe su toosee de función que funcione con la nueva superficie de la API de Hola.

Explorar la página de desarrollo de toohello atrás haciendo clic en el nombre de la función de Hola Hola barra de navegación izquierda.

Haga clic en **obtener dirección URL de la función** y copie la dirección URL de Hola. Debería ver que usa hello `/api/hello` enrutar ahora.

Copiar dirección URL de hello en una nueva pestaña del explorador o el cliente REST preferido. Los exploradores utilizarán GET de forma predeterminada.

Ejecute la función hello y confirme que se está trabajando. Puede que tenga parámetros de "nombre" hello tooprovide como un código de inicio rápido de consulta cadena toosatisfy Hola.

También puede intentar llamar a un extremo de hello con otro tooconfirm de método HTTP que no se ejecuta la función de Hola. Para ello, deberá toouse un cliente REST, como cURL, Postman o Fiddler.

## <a name="proxies-overview"></a>Introducción a Servidores proxy

En la siguiente sección hello, mostrará la API a través de un servidor proxy. Servidores proxy de funciones de Azure es una característica de vista previa que le permite tooforward solicitudes tooother recursos. Definir un extremo HTTP igual que con el desencadenador HTTP, pero en lugar de escribir código tooexecute cuando se llama a ese punto de conexión, se proporciona una implementación remota de tooa de dirección URL. Esto le permite toocompose API varios orígenes en una superficie de API única que es fácil que los clientes tooconsume. Esto es especialmente útil si desea toobuild su API como microservicios.

Un servidor proxy puede apuntar recurso tooany HTTP, como:
- Funciones de Azure 
- Aplicaciones de API en [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- Contenedores de Docker en [App Service en Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)
- Cualquier otra API hospedada

toolearn más información acerca de los servidores proxy, consulte [trabajar con servidores proxy de las funciones de Azure (vista previa)].

## <a name="create-your-first-proxy"></a>Creación de su primer proxy

En esta sección, creará un nuevo proxy que actúa como un servidor front-end tooyour API general. 

### <a name="setting-up-hello-frontend-environment"></a>Configuración de entorno de front-end de Hola

Repita los pasos de hello demasiado[crear una aplicación de la función](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate una nueva aplicación de función en la que va a crear el proxy. Esta nueva aplicación servirá como front-end de Hola para nuestra API y aplicación de función hello que estaba editando previamente actuará como un back-end.

Navegue tooyour nueva aplicación de función de front-end en el portal de Hola.

Seleccione **Configuración**. A continuación, activar o desactivar **Habilitar proxy de funciones de Azure (vista previa)** demasiado "On".

Seleccione **Configuración de plataforma** y elija **Configuración de la aplicación**.

Desplácese hacia abajo demasiado**configuración de la aplicación** y crear una nueva configuración con la clave "HELLO_HOST". Establezca su valor toohello de host de la aplicación de función de back-end, como `<YourApp>.azurewebsites.net`. Esto forma parte de la dirección URL de Hola que copió anteriormente al probar la función HTTP. Podrá hacer referencia a esta configuración en la configuración de hello más tarde.

> [!NOTE] 
> Configuración de la aplicación se recomienda para tooprevent de configuración de host de hello una dependencia codificada de forma rígida entorno para el proxy de Hola. Con la configuración de aplicación significa que puede mover la configuración de proxy de hello entre entornos, y se aplicará la configuración de la aplicación específica del entorno de Hola.

Haga clic en **Guardar**.

### <a name="creating-a-proxy-on-hello-frontend"></a>Crear a un proxy en hello front-end

Navegue tooyour atrás front-end función aplicación de portal de Hola.

En el panel de navegación izquierdo hello, haga clic en hello signo '+' siguiente demasiado "Servidores proxy (vista previa)".

![Creación de un proxy](./media/functions-create-serverless-api/creating-proxy.png)

Usar configuración de proxy como se especifica en la tabla de Hola.

| Campo | Valor de ejemplo | Descripción |
|---|---|---|
| Nombre | HelloProxy | Un nombre descriptivo que se usa solo para la administración |
| Plantilla de ruta | /api/hello | Determina qué ruta es tooinvoke usado este proxy |
| Dirección URL de back-end | https://%HELLO_HOST%/api/hello | Especifica la solicitud de hello extremo toowhich Hola debe ser procesadas por el proxy |

Tenga en cuenta que los servidores proxy no proporciona hello `/api` prefijo de ruta de acceso base y debe incluirse en la plantilla de ruta de Hola.

Hola `%HELLO_HOST%` sintaxis hará referencia a configuración de la aplicación hello que creó anteriormente. Hola resuelve la que dirección URL señala tooyour de función original.

Haga clic en **Crear**.

Puede probar el nuevo proxy copiando Hola dirección URL del Proxy y probarlo en el Explorador de Hola o con el cliente HTTP favorito.

## <a name="create-a-mock-api"></a>Creación de una API simulada

A continuación, usará un toocreate una API ficticia de proxy para la solución. Esto permite el desarrollo de cliente tooprogress, sin necesidad de back-end de hello totalmente implementada. Más adelante en el desarrollo, puede crear una nueva aplicación de función que admite esta lógica y redirigir el tooit de proxy.

toocreate este ejemplo de API, se creará un nuevo proxy, esta vez utilizando hello [Editor de aplicación de servicio](https://github.com/projectkudu/kudu/wiki/App-Service-Editor). tooget iniciado, navegue tooyour función aplicación de portal de Hola. Seleccione **Características de la plataforma** y busque **Editor de App Service**. Al hacer clic en este se abrirá Hola Editor de aplicación de servicio en una nueva pestaña.

Seleccione `proxies.json` Hola barra de navegación izquierda. Se trata de un archivo hello que almacena la configuración de Hola de todos los servidores proxy. Si utiliza uno de hello [las funciones de métodos de implementación](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), se trata de archivo hello mantendrá en control de código fuente. toolearn más información acerca de este archivo, consulte [configuración avanzada de servidores proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).

Si ha seguido estos pasos hasta ahora, su proxies.json debería ser similar Hola siguiente:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

A continuación, va a agregar su API simulada. Reemplace el archivo proxies.json con hello siguiente:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

Esto agrega a un nuevo proxy, "GetUserByName", sin una propiedad backendUri Hola. En lugar de llamar a otro recurso, modifica la respuesta predeterminada de Hola de servidores proxy mediante una invalidación de la respuesta. Las invalidaciones de solicitud y respuesta también pueden utilizarse junto con una dirección URL de back-end. Esto es especialmente útil cuando un proxy tooa heredado system, que podrían necesitar toomodify encabezados, parámetros de consulta, etc. toolearn más acerca de las invalidaciones de solicitud y respuesta, vea [modificar las solicitudes y respuestas en los Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).

Probar la API ficticia llamada Hola `/api/users/{username}` punto de conexión mediante un explorador o el cliente REST favoritos. Ser seguro tooreplace _{username}_ con un valor de cadena que representa un nombre de usuario.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se habrá aprendido cómo toobuild y personalizar una API en las funciones de Azure. También ha aprendido cómo toobring varias API, incluidos mocks, juntos como una superficie de API unificada. Puede usar estos toobuild técnicas a las API de cualquier complejidad, todos los mientras se ejecutan en hello sin servidor de proceso modelo que proporcionan funciones de Azure.

Hello las referencias siguientes pueden serle de ayuda a medida que desarrolla su API adicional:

- [Enlaces HTTP y webhook en Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [trabajar con servidores proxy de las funciones de Azure (vista previa)]
- [Documentación de una API de Azure Functions (versión preliminar)](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[trabajar con servidores proxy de las funciones de Azure (vista previa)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
