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
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="dd70f-103">Seguridad y autenticación de Event Grid</span><span class="sxs-lookup"><span data-stu-id="dd70f-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="dd70f-104">Azure Event Grid tiene tres tipos de autenticación:</span><span class="sxs-lookup"><span data-stu-id="dd70f-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="dd70f-105">Suscripciones a eventos</span><span class="sxs-lookup"><span data-stu-id="dd70f-105">Event subscriptions</span></span>
* <span data-ttu-id="dd70f-106">Publicación de eventos</span><span class="sxs-lookup"><span data-stu-id="dd70f-106">Event publishing</span></span>
* <span data-ttu-id="dd70f-107">Entrega de eventos de WebHook</span><span class="sxs-lookup"><span data-stu-id="dd70f-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="dd70f-108">Entrega de eventos de WebHook</span><span class="sxs-lookup"><span data-stu-id="dd70f-108">WebHook Event delivery</span></span>

<span data-ttu-id="dd70f-109">Webhooks son uno de los eventos de muchas maneras tooreceive en tiempo real desde la cuadrícula de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd70f-109">Webhooks are one of many ways tooreceive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="dd70f-110">Cada vez que hay un nuevo toobe listo de eventos entregado, cuadrícula de eventos envía una solicitud HTTP con tooyour WebHook con eventos de hello en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd70f-110">Every time there is a new event ready toobe delivered, Event Grid sends an HTTP request with tooyour WebHook with hello event in hello body.</span></span>

<span data-ttu-id="dd70f-111">Al registrar su propio punto de conexión de WebHook con cuadrícula de eventos, envía una solicitud POST con un código de validación simple en la propiedad de punto de conexión de tooprove de orden.</span><span class="sxs-lookup"><span data-stu-id="dd70f-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order tooprove endpoint ownership.</span></span> <span data-ttu-id="dd70f-112">La aplicación debe toorespond si reitera el código de validación de hello atrás.</span><span class="sxs-lookup"><span data-stu-id="dd70f-112">Your app needs toorespond by echoing back hello validation code.</span></span> <span data-ttu-id="dd70f-113">Cuadrícula de eventos no ofrecerá eventos tooWebHook extremos que no se han pasado la validación de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd70f-113">Event Grid will not deliver events tooWebHook endpoints that have not passed hello validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="dd70f-114">Detalles de la validación:</span><span class="sxs-lookup"><span data-stu-id="dd70f-114">Validation details:</span></span>

* <span data-ttu-id="dd70f-115">En tiempo de Hola de creación/actualización de la suscripción de eventos, cuadrícula de eventos expone un extremo de destino "SubscriptionValidationEvent" toohello de eventos.</span><span class="sxs-lookup"><span data-stu-id="dd70f-115">At hello time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event toohello target endpoint.</span></span>
* <span data-ttu-id="dd70f-116">evento de Hello contiene un valor de encabezado "Validación de tipo de evento:".</span><span class="sxs-lookup"><span data-stu-id="dd70f-116">hello event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="dd70f-117">cuerpo de evento de Hello tiene Hola mismo esquema que otros eventos de la cuadrícula de eventos.</span><span class="sxs-lookup"><span data-stu-id="dd70f-117">hello event body has hello same schema as other Event Grid events.</span></span>
* <span data-ttu-id="dd70f-118">datos del evento Hola incluyen una propiedad "ValidationCode" con una cadena generada de forma aleatoria p. ej. “ValidationCode: acb13…”.</span><span class="sxs-lookup"><span data-stu-id="dd70f-118">hello event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="dd70f-119">En la propiedad de punto de conexión de tooprove de orden, por ejemplo, el código de validación de hello back-de eco "ValidationResponse: acb13...".</span><span class="sxs-lookup"><span data-stu-id="dd70f-119">In order tooprove endpoint ownership, echo back hello validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="dd70f-120">Por último, es importante toonote que cuadrícula de eventos de Azure solo es compatible con los puntos de conexión de webhook HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dd70f-120">Finally, it is important toonote that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="dd70f-121">Suscripción a eventos</span><span class="sxs-lookup"><span data-stu-id="dd70f-121">Event subscription</span></span>

<span data-ttu-id="dd70f-122">evento de tooan toosubscribe, debe tener hello **Microsoft.EventGrid/EventSubscriptions/Write** recursos requiere el permiso en Hola.</span><span class="sxs-lookup"><span data-stu-id="dd70f-122">toosubscribe tooan event, you must have hello **Microsoft.EventGrid/EventSubscriptions/Write** permission on hello required resource.</span></span> <span data-ttu-id="dd70f-123">Necesita este permiso porque se está escribiendo una nueva suscripción en el ámbito de hello del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd70f-123">You need this permission because you are writing a new subscription at hello scope of hello resource.</span></span> <span data-ttu-id="dd70f-124">Hola requiere recursos difiere en función de si se va a suscribir tooa tema de sistema o un tema personalizado.</span><span class="sxs-lookup"><span data-stu-id="dd70f-124">hello required resource differs based on whether you are subscribing tooa system topic or custom topic.</span></span> <span data-ttu-id="dd70f-125">Ambos tipos se describen en esta sección.</span><span class="sxs-lookup"><span data-stu-id="dd70f-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="dd70f-126">Temas del sistema (editores del servicio de Azure)</span><span class="sxs-lookup"><span data-stu-id="dd70f-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="dd70f-127">Para consultar temas de sistema, necesita permiso toowrite una nueva suscripción de evento en el ámbito de Hola de evento de Hola Hola recursos publicación.</span><span class="sxs-lookup"><span data-stu-id="dd70f-127">For system topics, you need permission toowrite a new event subscription at hello scope of hello resource publishing hello event.</span></span> <span data-ttu-id="dd70f-128">formato de Hola de recursos de hello es:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="dd70f-128">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="dd70f-129">Por ejemplo, toosubscribe tooan evento en una cuenta de almacenamiento denominada **myacct**, necesita permiso de hello Microsoft.EventGrid/EventSubscriptions/Write en:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="dd70f-129">For example, toosubscribe tooan event on a storage account named **myacct**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="dd70f-130">Temas personalizados</span><span class="sxs-lookup"><span data-stu-id="dd70f-130">Custom topics</span></span>

<span data-ttu-id="dd70f-131">Para temas personalizados, necesita permiso toowrite una nueva suscripción de evento en el ámbito de Hola de tema de la cuadrícula de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd70f-131">For custom topics, you need permission toowrite a new event subscription at hello scope of hello Event Grid topic.</span></span> <span data-ttu-id="dd70f-132">formato de Hola de recursos de hello es:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="dd70f-132">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="dd70f-133">Por ejemplo, toosubscribe tooa tema personalizado denominado **mytopic**, necesita permiso de hello Microsoft.EventGrid/EventSubscriptions/Write en:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="dd70f-133">For example, toosubscribe tooa custom topic named **mytopic**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="dd70f-134">Publicación de temas</span><span class="sxs-lookup"><span data-stu-id="dd70f-134">Topic publishing</span></span>

<span data-ttu-id="dd70f-135">Los temas utilizan la Firma de acceso compartido (SAS) o la autenticación de clave.</span><span class="sxs-lookup"><span data-stu-id="dd70f-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="dd70f-136">Se recomienda el uso de SAS, pero la autenticación de clave proporciona programación simple y es compatible con muchos editores de webhook existentes.</span><span class="sxs-lookup"><span data-stu-id="dd70f-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="dd70f-137">Incluir valor de autenticación de hello en el encabezado HTTP de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd70f-137">You include hello authentication value in hello HTTP header.</span></span> <span data-ttu-id="dd70f-138">SAS, use **aeg token de sas** para el valor del encabezado de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd70f-138">For SAS, use **aeg-sas-token** for hello header value.</span></span> <span data-ttu-id="dd70f-139">Para la autenticación de clave, utilice **aeg de la clave sas** para el valor del encabezado de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd70f-139">For key authentication, use **aeg-sas-key** for hello header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="dd70f-140">Autenticación de clave</span><span class="sxs-lookup"><span data-stu-id="dd70f-140">Key authentication</span></span>

<span data-ttu-id="dd70f-141">Autenticación de clave es la forma más sencilla de Hola de autenticación.</span><span class="sxs-lookup"><span data-stu-id="dd70f-141">Key authentication is hello simplest form of authentication.</span></span> <span data-ttu-id="dd70f-142">Usar el formato de hello:`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="dd70f-142">Use hello format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="dd70f-143">Por ejemplo, pasa una clave con:</span><span class="sxs-lookup"><span data-stu-id="dd70f-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="dd70f-144">Tokens de SAS</span><span class="sxs-lookup"><span data-stu-id="dd70f-144">SAS tokens</span></span>

<span data-ttu-id="dd70f-145">Tokens SAS para la cuadrícula de eventos incluyen recursos de hello, un tiempo de expiración y una firma.</span><span class="sxs-lookup"><span data-stu-id="dd70f-145">SAS tokens for Event Grid include hello resource, an expiration time, and a signature.</span></span> <span data-ttu-id="dd70f-146">Hello formato de token de SAS de hello es: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="dd70f-146">hello format of hello SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="dd70f-147">recurso Hello es la ruta de acceso de Hola para hello tema toowhich va a enviar eventos.</span><span class="sxs-lookup"><span data-stu-id="dd70f-147">hello resource is hello path for hello topic toowhich you are sending events.</span></span> <span data-ttu-id="dd70f-148">Por ejemplo, una ruta de acceso de recurso válida es: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="dd70f-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="dd70f-149">Generar la firma de Hola de una clave.</span><span class="sxs-lookup"><span data-stu-id="dd70f-149">You generate hello signature from a key.</span></span>

<span data-ttu-id="dd70f-150">Por ejemplo, un valor **aeg-sas-token** válido es:</span><span class="sxs-lookup"><span data-stu-id="dd70f-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="dd70f-151">Hola de ejemplo siguiente crea un token SAS para su uso con la cuadrícula de eventos:</span><span class="sxs-lookup"><span data-stu-id="dd70f-151">hello following example creates a SAS token for use with Event Grid:</span></span>

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

## <a name="management-access-control"></a><span data-ttu-id="dd70f-152">Control de acceso de administración</span><span class="sxs-lookup"><span data-stu-id="dd70f-152">Management Access Control</span></span>

<span data-ttu-id="dd70f-153">Cuadrícula de eventos de Azure permite toocontrol Hola nivel de acceso dado toodifferent usuarios toodo varias operaciones de administración como las suscripciones de eventos de lista, crear nuevos y generar claves.</span><span class="sxs-lookup"><span data-stu-id="dd70f-153">Azure Event Grid allows you toocontrol hello level of access given toodifferent users toodo various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="dd70f-154">Event Grid utiliza la comprobación de acceso basada en rol (RBAC) para esto.</span><span class="sxs-lookup"><span data-stu-id="dd70f-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="dd70f-155">Tipos de operación</span><span class="sxs-lookup"><span data-stu-id="dd70f-155">Operation types</span></span>

<span data-ttu-id="dd70f-156">Cuadrícula de eventos de Azure admite Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="dd70f-156">Azure event grid supports hello following actions:</span></span>

* <span data-ttu-id="dd70f-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="dd70f-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="dd70f-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="dd70f-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="dd70f-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="dd70f-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="dd70f-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="dd70f-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="dd70f-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="dd70f-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="dd70f-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="dd70f-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="dd70f-163">Hola tres últimas operaciones devuelto potencialmente información secreta que obtiene filtrarse para quitarlos de las operaciones de lectura normales.</span><span class="sxs-lookup"><span data-stu-id="dd70f-163">hello last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="dd70f-164">Es una práctica recomendada para que las operaciones de toorestrict acceso toothese.</span><span class="sxs-lookup"><span data-stu-id="dd70f-164">It is best practice for you toorestrict access toothese operations.</span></span> <span data-ttu-id="dd70f-165">Roles personalizados pueden crearse con [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [interfaz de línea de comandos (CLI) de Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md), hello y [API de REST](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="dd70f-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="dd70f-166">Exigencia de la comprobación de acceso basada en roles (RBAC)</span><span class="sxs-lookup"><span data-stu-id="dd70f-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="dd70f-167">Usar hello siguiendo los pasos tooenforce RBAC para los distintos usuarios:</span><span class="sxs-lookup"><span data-stu-id="dd70f-167">Use hello following steps tooenforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="dd70f-168">Creación de un archivo de definición de rol personalizado (.json)</span><span class="sxs-lookup"><span data-stu-id="dd70f-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="dd70f-169">siguiente Hola es definiciones de roles de cuadrícula de eventos de ejemplo que permiten a los usuarios tooperform distintos conjuntos de acciones.</span><span class="sxs-lookup"><span data-stu-id="dd70f-169">hello following are sample Event Grid role definitions which allow users tooperform different sets of actions.</span></span>

<span data-ttu-id="dd70f-170">**EventGridReadOnlyRole.json**: Permitir únicamente operaciones de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="dd70f-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
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

<span data-ttu-id="dd70f-171">**EventGridNoDeleteListKeysRole.json**: Permitir acciones de publicación restringidas pero denegar acciones de eliminación.</span><span class="sxs-lookup"><span data-stu-id="dd70f-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
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
 
<span data-ttu-id="dd70f-172">**EventGridContributorRole.json**: Permite todas las acciones de Event Grid.</span><span class="sxs-lookup"><span data-stu-id="dd70f-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
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

#### <a name="install-and-login-tooazure-cli"></a><span data-ttu-id="dd70f-173">Instalación e inicio de sesión tooAzure CLI</span><span class="sxs-lookup"><span data-stu-id="dd70f-173">Install and login tooAzure CLI</span></span>

* <span data-ttu-id="dd70f-174">CLI de Azure versión 0.8.8 o posterior.</span><span class="sxs-lookup"><span data-stu-id="dd70f-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="dd70f-175">versión más reciente de tooinstall hello y asócielo con su suscripción de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="dd70f-175">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="dd70f-176">Azure Resource Manager en la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="dd70f-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="dd70f-177">Vaya demasiado[Using Hola CLI de Azure con el Administrador de recursos de hello](../xplat-cli-azure-resource-manager.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="dd70f-177">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="dd70f-178">Crear un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="dd70f-178">Create a custom role</span></span>

<span data-ttu-id="dd70f-179">toocreate un rol personalizado, use:</span><span class="sxs-lookup"><span data-stu-id="dd70f-179">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a><span data-ttu-id="dd70f-180">Asignar Hola rol tooa usuario</span><span class="sxs-lookup"><span data-stu-id="dd70f-180">Assign hello role tooa user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="dd70f-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd70f-181">Next steps</span></span>

* <span data-ttu-id="dd70f-182">Para una cuadrícula de introducción tooEvent, consulte [acerca de la cuadrícula de eventos](overview.md)</span><span class="sxs-lookup"><span data-stu-id="dd70f-182">For an introduction tooEvent Grid, see [About Event Grid](overview.md)</span></span>
