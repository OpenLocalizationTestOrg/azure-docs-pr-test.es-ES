---
title: "esquema de suscripción de cuadrícula de eventos de aaaAzure"
description: "Describe las propiedades de Hola para suscribir el evento tooan con cuadrícula de eventos de Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="ced50-103">Esquema de suscripción de Event Grid</span><span class="sxs-lookup"><span data-stu-id="ced50-103">Event Grid subscription schema</span></span>

<span data-ttu-id="ced50-104">toocreate una suscripción de la cuadrícula de eventos, debe enviar una operación de suscripción de Create Event toohello de solicitud.</span><span class="sxs-lookup"><span data-stu-id="ced50-104">toocreate an Event Grid subscription, you send a request toohello Create Event subscription operation.</span></span> <span data-ttu-id="ced50-105">Usar hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="ced50-105">Use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="ced50-106">Por ejemplo, toocreate una suscripción de eventos para una cuenta de almacenamiento denominada `examplestorage` en un grupo de recursos denominado `examplegroup`, formato uso Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ced50-106">For example, toocreate an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="ced50-107">Hola artículo describen propiedades Hola y el esquema de cuerpo de saludo de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="ced50-107">hello article describes hello properties and schema for hello body of hello request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="ced50-108">Propiedades de la suscripción de eventos</span><span class="sxs-lookup"><span data-stu-id="ced50-108">Event subscription properties</span></span>

| <span data-ttu-id="ced50-109">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ced50-109">Property</span></span> | <span data-ttu-id="ced50-110">Escriba</span><span class="sxs-lookup"><span data-stu-id="ced50-110">Type</span></span> | <span data-ttu-id="ced50-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="ced50-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="ced50-112">de destino</span><span class="sxs-lookup"><span data-stu-id="ced50-112">destination</span></span> | <span data-ttu-id="ced50-113">objeto</span><span class="sxs-lookup"><span data-stu-id="ced50-113">object</span></span> | <span data-ttu-id="ced50-114">objeto de Hola que define el punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ced50-114">hello object that defines hello endpoint.</span></span> |
| <span data-ttu-id="ced50-115">filter</span><span class="sxs-lookup"><span data-stu-id="ced50-115">filter</span></span> | <span data-ttu-id="ced50-116">objeto</span><span class="sxs-lookup"><span data-stu-id="ced50-116">object</span></span> | <span data-ttu-id="ced50-117">Un campo opcional para filtrar los tipos de Hola de eventos.</span><span class="sxs-lookup"><span data-stu-id="ced50-117">An optional field for filtering hello types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="ced50-118">Objeto de destino</span><span class="sxs-lookup"><span data-stu-id="ced50-118">destination object</span></span>

| <span data-ttu-id="ced50-119">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ced50-119">Property</span></span> | <span data-ttu-id="ced50-120">Escriba</span><span class="sxs-lookup"><span data-stu-id="ced50-120">Type</span></span> | <span data-ttu-id="ced50-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="ced50-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="ced50-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="ced50-122">endpointType</span></span> | <span data-ttu-id="ced50-123">cadena</span><span class="sxs-lookup"><span data-stu-id="ced50-123">string</span></span> | <span data-ttu-id="ced50-124">tipo de Hola de punto de conexión para la suscripción de hello (webhook/HTTP, centro de eventos o cola).</span><span class="sxs-lookup"><span data-stu-id="ced50-124">hello type of endpoint for hello subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="ced50-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="ced50-125">endpointUrl</span></span> | <span data-ttu-id="ced50-126">cadena</span><span class="sxs-lookup"><span data-stu-id="ced50-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="ced50-127">Objeto de filtro</span><span class="sxs-lookup"><span data-stu-id="ced50-127">filter object</span></span>

| <span data-ttu-id="ced50-128">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ced50-128">Property</span></span> | <span data-ttu-id="ced50-129">Escriba</span><span class="sxs-lookup"><span data-stu-id="ced50-129">Type</span></span> | <span data-ttu-id="ced50-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="ced50-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="ced50-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="ced50-131">includedEventTypes</span></span> | <span data-ttu-id="ced50-132">array</span><span class="sxs-lookup"><span data-stu-id="ced50-132">array</span></span> | <span data-ttu-id="ced50-133">Coincide con cuando el tipo de evento de hello en mensajes de bienvenida del evento es un tooone coincidencias exactas de estos nombres de tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="ced50-133">Match when hello event type in hello event message is an exact match tooone of these event type names.</span></span> <span data-ttu-id="ced50-134">Genera un error cuando el nombre del evento no coincide con los nombres de tipo de evento de hello registrado para el origen del evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="ced50-134">Raises an error when event name does not match hello registered event type names for hello event source.</span></span> <span data-ttu-id="ced50-135">El valor predeterminado coincide con todos los tipos de evento.</span><span class="sxs-lookup"><span data-stu-id="ced50-135">Default matches all event types.</span></span> |
| <span data-ttu-id="ced50-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="ced50-136">subjectBeginsWith</span></span> | <span data-ttu-id="ced50-137">cadena</span><span class="sxs-lookup"><span data-stu-id="ced50-137">string</span></span> | <span data-ttu-id="ced50-138">Un campo coincidencia de prefijo filtro toohello asunto en mensajes de bienvenida del evento.</span><span class="sxs-lookup"><span data-stu-id="ced50-138">A prefix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="ced50-139">valor predeterminado de Hola o la cadena vacía se ajusta a todas.</span><span class="sxs-lookup"><span data-stu-id="ced50-139">hello default or empty string matches all.</span></span> | 
| <span data-ttu-id="ced50-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="ced50-140">subjectEndsWith</span></span> | <span data-ttu-id="ced50-141">cadena</span><span class="sxs-lookup"><span data-stu-id="ced50-141">string</span></span> | <span data-ttu-id="ced50-142">Un sufijo-match filtro toohello campo de asunto en mensajes de bienvenida del evento.</span><span class="sxs-lookup"><span data-stu-id="ced50-142">A suffix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="ced50-143">valor predeterminado de Hola o la cadena vacía se ajusta a todas.</span><span class="sxs-lookup"><span data-stu-id="ced50-143">hello default or empty string matches all.</span></span> |
| <span data-ttu-id="ced50-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="ced50-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="ced50-145">cadena</span><span class="sxs-lookup"><span data-stu-id="ced50-145">string</span></span> | <span data-ttu-id="ced50-146">Controla la coincidencia que distingue mayúsculas de minúsculas en los filtros.</span><span class="sxs-lookup"><span data-stu-id="ced50-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="ced50-147">Esquema de suscripción de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ced50-147">Example subscription schema</span></span>

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="ced50-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ced50-148">Next steps</span></span>

* <span data-ttu-id="ced50-149">Para una cuadrícula de introducción tooEvent, consulte [¿qué es la cuadrícula de eventos?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="ced50-149">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
