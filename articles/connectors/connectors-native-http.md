---
title: "aaaCommunicate con cualquier punto de conexión a través de HTTP - Azure Logic Apps | Documentos de Microsoft"
description: "Creación de aplicaciones lógicas que se comuniquen con cualquier punto de conexión a través de HTTP"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a>Empezar a trabajar con hello acción HTTP

Con hello acción HTTP, puede ampliar los flujos de trabajo para su organización y punto de conexión de tooany se comunican a través de HTTP.

Puede:

* Cree flujos de trabajo de aplicaciones lógicas que se activen (desencadenador) cuando un sitio web que administre deje de funcionar.
* Comunicarse el punto de conexión de tooany en otros servicios a través de HTTP tooextend los flujos de trabajo.

tooget se hayan iniciado mediante la acción de hello HTTP en una aplicación de lógica, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-trigger"></a>Utilice el desencadenador de hello HTTP
Un desencadenador es un evento que puede ser el flujo de trabajo hello toostart utilizado que se define en una aplicación de lógica. [Más información sobre los desencadenadores](connectors-overview.md).

Aquí es una secuencia de ejemplo de cómo desencadenar tooset seguridad Hola HTTP Hola diseñador la lógica de aplicación.

1. Agregar desencadenador HTTP de hello en la aplicación lógica.
2. Completar parámetros de Hola de punto de conexión de hello HTTP que desea toopoll.
3. Modificar el intervalo de periodicidad de hello en la frecuencia con debería realizar el sondeo.

   aplicación de la lógica de Hello ahora se desencadena con cualquier contenido que se devuelve durante cada comprobación.

   ![Desencadenador HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a>Cómo funciona el desencadenador de hello HTTP

desencadenador de Hello HTTP envía un punto de conexión de llamada tooHTTP en un intervalo periódico. De forma predeterminada, cualquier código de respuesta HTTP que es inferior a 300 hace un toorun de aplicación lógica. toospecify si debería desencadenar la aplicación de la lógica de hello, puede editar aplicación de lógica de hello en la vista de código y agregar una condición que se evalúa como después de hello llamada HTTP. Este es un ejemplo de un desencadenador HTTP que se desencadena cuando Hola devolvió el código de estado es mayor o igual a demasiado`400`.

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

Encuentran los detalles completos acerca de los parámetros de desencadenador de hello HTTP en [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).

## <a name="use-hello-http-action"></a>Use la acción Hola HTTP

Una acción es una operación que se lleva a cabo por flujo de trabajo de Hola que se define en una aplicación de lógica. 
[Más información acerca de las acciones](connectors-overview.md).

1. Elija **Nuevo paso** > **Agregar una acción**.
3. En el cuadro de búsqueda de la acción de hello, escriba **http** acciones de hello HTTP toolist.
   
    ![Seleccione la acción de hello HTTP](./media/connectors-native-http/using-action-1.png)

4. Agregue los parámetros necesarios para la llamada de hello HTTP.
   
    ![Hola completa acción HTTP](./media/connectors-native-http/using-action-2.png)

5. En la barra de herramientas del diseñador hello, haga clic en **guardar**. La aplicación lógica se guardó y publicó (activada) en hello mismo tiempo.

## <a name="http-trigger"></a>Desencadenador HTTP
A continuación encontrará los detalles de Hola de desencadenador de hello admitido por este conector. conector HTTP de Hello tiene un desencadenador.

| Desencadenador | Description |
| --- | --- |
| HTTP |Realiza una llamada HTTP y devuelve el contenido de la respuesta de Hola. |

## <a name="http-action"></a>Acción HTTP
A continuación encontrará los detalles de hello para la acción de hello admitido por este conector. Conector de Hello HTTP tiene una acción posible.

| Acción | Description |
| --- | --- |
| HTTP |Realiza una llamada HTTP y devuelve el contenido de la respuesta de Hola. |

## <a name="http-details"></a>Detalles HTTP
Hello en las tablas siguientes se describen Hola necesarios y campos de entrada opcionales para acción de Hola y detalles salida correspondientes Hola que están asociados con el uso de la acción de Hola.

#### <a name="http-request"></a>Solicitud HTTP
los siguientes Hola son campos de entrada para la acción de hello, que realiza una solicitud de salida HTTP.
Un * significa que es un campo obligatorio.

| Nombre para mostrar | Nombre de propiedad | Description |
| --- | --- | --- |
| Método* |estático |Hola HTTP verbo toouse |
| URI* |uri |Hola URI de solicitud de hello HTTP |
| Encabezados |encabezados |Un objeto JSON de tooinclude de encabezados HTTP |
| Cuerpo |body |Hola cuerpo de solicitud HTTP |
| Autenticación |Autenticación |Detalles de hello [autenticación](#authentication) sección |

<br>

#### <a name="output-details"></a>Detalles de salida
siguiente Hola es detalles de salida de respuesta HTTP Hola.

| Nombre de propiedad | Tipo de datos | Description |
| --- | --- | --- |
| encabezados |objeto |Encabezados de respuesta |
| Cuerpo |objeto |Objeto de respuesta |
| Código de estado |int |Código de estado HTTP |

## <a name="authentication"></a>Autenticación
característica de las aplicaciones lógicas de Hello permite a toouse diferentes tipos de autenticación en los extremos HTTP. Puede usar este procedimiento de autenticación con hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, y  **[HTTP Webhook](connectors-native-webhook.md)**  conectores. Hola siguientes tipos de autenticación es configurable:

* [Autenticación básica](#basic-authentication)
* [Autenticación de certificados de clientes](#client-certificate-authentication)
* [Autenticación de OAuth de Azure Active Directory (Azure AD)](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a>Autenticación básica

Hola después el objeto de autenticación es necesario para la autenticación básica.
Un * significa que es un campo obligatorio.

| Nombre de propiedad | Tipo de datos | Description |
| --- | --- | --- |
| Type* |type |Tipo de autenticación (debe ser `Basic` para la autenticación básica) |
| Username* |nombre de usuario |Tooauthenticate de nombre de usuario |
| Password* |Contraseña |Contraseña tooauthenticate |

> [!TIP]
> Si desea toouse una contraseña que no se puede recuperar de la definición de hello, use un `securestring` hello y parámetro `@parameters()`  
>  [función de la definición de flujo de trabajo](http://aka.ms/logicappdocs).

Por ejemplo:

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a>Autenticación de certificados de clientes

Hello es necesario siguiente objeto de autenticación para la autenticación de certificado de cliente. Un * significa que es un campo obligatorio.

| Nombre de propiedad | Tipo de datos | Description |
| --- | --- | --- |
| Type* |type |tipo de autenticación de Hola (debe ser `ClientCertificate` para los certificados de cliente SSL) |
| PFX* |pfx |contenido de Hello con codificación Base64 del archivo de intercambio de información Personal (PFX) Hola |
| Password* |Contraseña |Hola contraseña tooaccess Hola archivo PFX |

> [!TIP]
> toouse un parámetro que no se puede leer en la definición de hello después de guardar la aplicación de la lógica de hello, puede usar un `securestring` hello y parámetro `@parameters()`  
>  [función de la definición de flujo de trabajo](http://aka.ms/logicappdocs).

Por ejemplo:

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a>Autenticación de OAuth de Azure AD
Hola después el objeto de autenticación es necesario para la autenticación de OAuth de Azure AD. Un * significa que es un campo obligatorio.

| Nombre de propiedad | Tipo de datos | Description |
| --- | --- | --- |
| Type* |type |tipo de autenticación de Hola (debe ser `ActiveDirectoryOAuth` para Azure AD OAuth) |
| Tenant* |tenant |identificador del inquilino Hello para el inquilino de hello Azure AD |
| Audience* |audience |recurso de Hola que está solicitando toouse de autorización. Por ejemplo: `https://management.core.windows.net/` |
| Client ID* |clientId |Hola identificador de cliente de la aplicación hello Azure AD |
| Secret* |secret |secreto de Hola Hola del cliente de que solicita el token de Hola |

> [!TIP]
> Puede usar un `securestring` hello y parámetro `@parameters()` [función de la definición de flujo de trabajo](http://aka.ms/logicappdocs) toouse un parámetro que no se puede leer en la definición de hello después de guardar.
> 
> 

Por ejemplo:

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a>Pasos siguientes
Ahora, pruebe plataforma hello y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md). Puede explorar Hola otros conectores disponibles en las aplicaciones lógicas examinando nuestro [lista de las API](apis-list.md).

