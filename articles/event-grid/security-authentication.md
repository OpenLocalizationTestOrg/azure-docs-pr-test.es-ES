---
title: "autenticación y seguridad de la cuadrícula de eventos de aaaAzure"
description: Describe Azure Event Grid y sus conceptos.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a>Seguridad y autenticación de Event Grid 

Azure Event Grid tiene tres tipos de autenticación:

* Suscripciones a eventos
* Publicación de eventos
* Entrega de eventos de WebHook

## <a name="webhook-event-delivery"></a>Entrega de eventos de WebHook

Webhooks son uno de los eventos de muchas maneras tooreceive en tiempo real desde la cuadrícula de eventos de Azure.

Cada vez que hay un nuevo toobe listo de eventos entregado, cuadrícula de eventos envía una solicitud HTTP con tooyour WebHook con eventos de hello en el cuerpo de Hola.

Al registrar su propio punto de conexión de WebHook con cuadrícula de eventos, envía una solicitud POST con un código de validación simple en la propiedad de punto de conexión de tooprove de orden. La aplicación debe toorespond si reitera el código de validación de hello atrás. Cuadrícula de eventos no ofrecerá eventos tooWebHook extremos que no se han pasado la validación de Hola.
 
### <a name="validation-details"></a>Detalles de la validación:

* En tiempo de Hola de creación/actualización de la suscripción de eventos, cuadrícula de eventos expone un extremo de destino "SubscriptionValidationEvent" toohello de eventos.
* evento de Hello contiene un valor de encabezado "Validación de tipo de evento:".
* cuerpo de evento de Hello tiene Hola mismo esquema que otros eventos de la cuadrícula de eventos.
* datos del evento Hola incluyen una propiedad "ValidationCode" con una cadena generada de forma aleatoria p. ej. “ValidationCode: acb13…”.

En la propiedad de punto de conexión de tooprove de orden, por ejemplo, el código de validación de hello back-de eco "ValidationResponse: acb13...".

Por último, es importante toonote que cuadrícula de eventos de Azure solo es compatible con los puntos de conexión de webhook HTTPS.
## <a name="event-subscription"></a>Suscripción a eventos

evento de tooan toosubscribe, debe tener hello **Microsoft.EventGrid/EventSubscriptions/Write** recursos requiere el permiso en Hola. Necesita este permiso porque se está escribiendo una nueva suscripción en el ámbito de hello del recurso de Hola. Hola requiere recursos difiere en función de si se va a suscribir tooa tema de sistema o un tema personalizado. Ambos tipos se describen en esta sección.

### <a name="system-topics-azure-service-publishers"></a>Temas del sistema (editores del servicio de Azure)

Para consultar temas de sistema, necesita permiso toowrite una nueva suscripción de evento en el ámbito de Hola de evento de Hola Hola recursos publicación. formato de Hola de recursos de hello es:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

Por ejemplo, toosubscribe tooan evento en una cuenta de almacenamiento denominada **myacct**, necesita permiso de hello Microsoft.EventGrid/EventSubscriptions/Write en:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>Temas personalizados

Para temas personalizados, necesita permiso toowrite una nueva suscripción de evento en el ámbito de Hola de tema de la cuadrícula de eventos de Hola. formato de Hola de recursos de hello es:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

Por ejemplo, toosubscribe tooa tema personalizado denominado **mytopic**, necesita permiso de hello Microsoft.EventGrid/EventSubscriptions/Write en:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>Publicación de temas

Los temas utilizan la Firma de acceso compartido (SAS) o la autenticación de clave. Se recomienda el uso de SAS, pero la autenticación de clave proporciona programación simple y es compatible con muchos editores de webhook existentes. 

Incluir valor de autenticación de hello en el encabezado HTTP de Hola. SAS, use **aeg token de sas** para el valor del encabezado de Hola. Para la autenticación de clave, utilice **aeg de la clave sas** para el valor del encabezado de Hola.

### <a name="key-authentication"></a>Autenticación de clave

Autenticación de clave es la forma más sencilla de Hola de autenticación. Usar el formato de hello:`aeg-sas-key: <your key>`

Por ejemplo, pasa una clave con: 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>Tokens de SAS

Tokens SAS para la cuadrícula de eventos incluyen recursos de hello, un tiempo de expiración y una firma. Hello formato de token de SAS de hello es: `r={resource}&e={expiration}&s={signature}`.

recurso Hello es la ruta de acceso de Hola para hello tema toowhich va a enviar eventos. Por ejemplo, una ruta de acceso de recurso válida es: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

Generar la firma de Hola de una clave.

Por ejemplo, un valor **aeg-sas-token** válido es:

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

Hola de ejemplo siguiente crea un token SAS para su uso con la cuadrícula de eventos:

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a>Control de acceso de administración

Cuadrícula de eventos de Azure permite toocontrol Hola nivel de acceso dado toodifferent usuarios toodo varias operaciones de administración como las suscripciones de eventos de lista, crear nuevos y generar claves. Event Grid utiliza la comprobación de acceso basada en rol (RBAC) para esto.

### <a name="operation-types"></a>Tipos de operación

Cuadrícula de eventos de Azure admite Hola siguientes acciones:

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

Hola tres últimas operaciones devuelto potencialmente información secreta que obtiene filtrarse para quitarlos de las operaciones de lectura normales. Es una práctica recomendada para que las operaciones de toorestrict acceso toothese. Roles personalizados pueden crearse con [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [interfaz de línea de comandos (CLI) de Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md), hello y [API de REST](../active-directory/role-based-access-control-manage-access-rest.md).

### <a name="enforcing-role-based-access-check-rbac"></a>Exigencia de la comprobación de acceso basada en roles (RBAC)

Usar hello siguiendo los pasos tooenforce RBAC para los distintos usuarios:

#### <a name="create-a-custom-role-definition-file-json"></a>Creación de un archivo de definición de rol personalizado (.json)

siguiente Hola es definiciones de roles de cuadrícula de eventos de ejemplo que permiten a los usuarios tooperform distintos conjuntos de acciones.

**EventGridReadOnlyRole.json**: Permitir únicamente operaciones de solo lectura.
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

**EventGridNoDeleteListKeysRole.json**: Permitir acciones de publicación restringidas pero denegar acciones de eliminación.
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
**EventGridContributorRole.json**: Permite todas las acciones de Event Grid.  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a>Instalación e inicio de sesión tooAzure CLI

* CLI de Azure versión 0.8.8 o posterior. versión más reciente de tooinstall hello y asócielo con su suscripción de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md).
* Azure Resource Manager en la CLI de Azure Vaya demasiado[Using Hola CLI de Azure con el Administrador de recursos de hello](../xplat-cli-azure-resource-manager.md) para obtener más detalles.

#### <a name="create-a-custom-role"></a>Crear un rol personalizado

toocreate un rol personalizado, use:

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a>Asignar Hola rol tooa usuario


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>Pasos siguientes

* Para una cuadrícula de introducción tooEvent, consulte [acerca de la cuadrícula de eventos](overview.md)
