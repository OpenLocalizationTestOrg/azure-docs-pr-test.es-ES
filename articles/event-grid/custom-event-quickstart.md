---
title: Eventos personalizados para Azure Event Grid | Microsoft Docs
description: Use Azure Event Grid para publicar un tema y suscribirse a ese evento.
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 0290836bebadb20085a3ce84dddc088c3af385da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="f2e34-103">Creación y enrutamiento de eventos personalizados con Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="f2e34-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="f2e34-104">Azure Event Grid es un servicio de eventos para la nube.</span><span class="sxs-lookup"><span data-stu-id="f2e34-104">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="f2e34-105">En este artículo, se usa la CLI de Azure para crear un tema personalizado, suscribirse al tema y desencadenar el evento para ver el resultado.</span><span class="sxs-lookup"><span data-stu-id="f2e34-105">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="f2e34-106">Por lo general, los eventos se envían a un punto de conexión que responde al evento, como un webhook o Azure Function.</span><span class="sxs-lookup"><span data-stu-id="f2e34-106">Typically, you send events to an endpoint that responds to the event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="f2e34-107">Sin embargo, para simplificar las cosas, en este artículo los eventos se envían a una dirección URL que simplemente recopila los mensajes.</span><span class="sxs-lookup"><span data-stu-id="f2e34-107">However, to simplify this article, you send the events to a URL that merely collects the messages.</span></span> <span data-ttu-id="f2e34-108">Esta dirección URL se crea mediante una herramienta de código abierto de terceros llamada [RequestBin](https://requestb.in/).</span><span class="sxs-lookup"><span data-stu-id="f2e34-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="f2e34-109">**RequestBin** es una herramienta de código abierto que no está pensada para una utilización de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="f2e34-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="f2e34-110">El uso de la herramienta aquí es meramente ilustrativo.</span><span class="sxs-lookup"><span data-stu-id="f2e34-110">The use of the tool here is purely demonstrative.</span></span> <span data-ttu-id="f2e34-111">Si inserta más de un evento a la vez, puede que no vea todos los eventos en la herramienta.</span><span class="sxs-lookup"><span data-stu-id="f2e34-111">If you push more than one event at a time, you might not see all of your events in the tool.</span></span>

<span data-ttu-id="f2e34-112">Cuando haya terminado, verá que los datos del evento se han enviado a un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="f2e34-112">When you are finished, you see that the event data has been sent to an endpoint.</span></span>

![Datos de evento](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f2e34-114">Si decide instalar y usar la CLI de Azure localmente, para los fines de este artículo es preciso que ejecute la versión más reciente (2.0.14 o posterior).</span><span class="sxs-lookup"><span data-stu-id="f2e34-114">If you choose to install and use the CLI locally, this article requires that you are running the latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="f2e34-115">Para encontrar la versión, ejecute `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f2e34-115">To find the version, run `az --version`.</span></span> <span data-ttu-id="f2e34-116">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f2e34-116">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="f2e34-117">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f2e34-117">Create a resource group</span></span>

<span data-ttu-id="f2e34-118">Los temas de Event Grid son recursos de Azure y se deben colocar en un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2e34-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="f2e34-119">El grupo de recursos de Azure es una colección lógica en la que se implementan y administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2e34-119">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="f2e34-120">Cree un grupo de recursos con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f2e34-120">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="f2e34-121">En el ejemplo siguiente, se crea un grupo de recursos denominado *gridResourceGroup* en la ubicación *westus2*.</span><span class="sxs-lookup"><span data-stu-id="f2e34-121">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="f2e34-122">Creación de un tema personalizado</span><span class="sxs-lookup"><span data-stu-id="f2e34-122">Create a custom topic</span></span>

<span data-ttu-id="f2e34-123">Un tema proporciona un punto de conexión definido por el usuario en el que se registran los eventos.</span><span class="sxs-lookup"><span data-stu-id="f2e34-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="f2e34-124">En el ejemplo siguiente se crea el tema en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f2e34-124">The following example creates the topic in your resource group.</span></span> <span data-ttu-id="f2e34-125">Reemplace `<topic_name>` por un nombre único para el tema.</span><span class="sxs-lookup"><span data-stu-id="f2e34-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="f2e34-126">El nombre del tema debe ser único porque se representa mediante una entrada DNS.</span><span class="sxs-lookup"><span data-stu-id="f2e34-126">The topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="f2e34-127">En la versión preliminar, Event Grid admite las ubicaciones **westus2** y **westcentralus**.</span><span class="sxs-lookup"><span data-stu-id="f2e34-127">For the preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="f2e34-128">Creación de un punto de conexión de mensaje</span><span class="sxs-lookup"><span data-stu-id="f2e34-128">Create a message endpoint</span></span>

<span data-ttu-id="f2e34-129">Antes de suscribirse al tema, vamos a crear el punto de conexión para el mensaje de evento.</span><span class="sxs-lookup"><span data-stu-id="f2e34-129">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="f2e34-130">En lugar de escribir código para responder al evento, vamos a crear un punto de conexión que recopile los mensajes para que pueda verlos.</span><span class="sxs-lookup"><span data-stu-id="f2e34-130">Rather than write code to respond to the event, let's create an endpoint that collects the messages so you can view them.</span></span> <span data-ttu-id="f2e34-131">RequestBin es una herramienta de código abierto de terceros que le permite crear un punto de conexión y ver las solicitudes que se envían a él.</span><span class="sxs-lookup"><span data-stu-id="f2e34-131">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="f2e34-132">Vaya a [RequestBin](https://requestb.in/) y haga clic en **Create a RequestBin** (Crear RequestBin).</span><span class="sxs-lookup"><span data-stu-id="f2e34-132">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="f2e34-133">Copie la dirección URL de la ubicación, la necesitará para suscribirse al tema.</span><span class="sxs-lookup"><span data-stu-id="f2e34-133">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="f2e34-134">Suscripción a un tema</span><span class="sxs-lookup"><span data-stu-id="f2e34-134">Subscribe to a topic</span></span>

<span data-ttu-id="f2e34-135">Suscríbase a un tema para indicar a Event Grid los eventos cuyo seguimiento desea realizar. En el ejemplo siguiente se suscribirá al tema que ha creado y pasará la dirección URL de RequestBin como punto de conexión en la notificación de eventos.</span><span class="sxs-lookup"><span data-stu-id="f2e34-135">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the URL from RequestBin as the endpoint for event notification.</span></span> <span data-ttu-id="f2e34-136">Reemplace `<event_subscription_name>` por un nombre único para la suscripción y `<URL_from_RequestBin>` por el valor de la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="f2e34-136">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with the value from the preceding section.</span></span> <span data-ttu-id="f2e34-137">Al especificar un punto de conexión cuando se suscribe, Event Grid controla el enrutamiento de los eventos a ese punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="f2e34-137">By specifying an endpoint when subscribing, Event Grid handles the routing of events to that endpoint.</span></span> <span data-ttu-id="f2e34-138">En `<topic_name>`, use el valor que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f2e34-138">For `<topic_name>`, use the value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="f2e34-139">Envío de un evento al tema</span><span class="sxs-lookup"><span data-stu-id="f2e34-139">Send an event to your topic</span></span>

<span data-ttu-id="f2e34-140">Ahora, vamos a desencadenar un evento para ver cómo Event Grid distribuye el mensaje al punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="f2e34-140">Now, let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="f2e34-141">En primer lugar, vamos a obtener la dirección URL y la clave del tema.</span><span class="sxs-lookup"><span data-stu-id="f2e34-141">First, let's get the URL and key for the topic.</span></span> <span data-ttu-id="f2e34-142">De nuevo, use el nombre de su tema en `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="f2e34-142">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="f2e34-143">Para simplificar las cosas, en este artículo hemos configurado datos de evento de ejemplo para enviar al tema.</span><span class="sxs-lookup"><span data-stu-id="f2e34-143">To simplify this article, we have set up sample event data to send to the topic.</span></span> <span data-ttu-id="f2e34-144">Normalmente, una aplicación o servicio de Azure enviaría los datos del evento.</span><span class="sxs-lookup"><span data-stu-id="f2e34-144">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="f2e34-145">En el ejemplo siguiente se obtienen los datos del evento:</span><span class="sxs-lookup"><span data-stu-id="f2e34-145">The following example gets the event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="f2e34-146">Si ejecuta `echo "$body"` puede ver el evento completo.</span><span class="sxs-lookup"><span data-stu-id="f2e34-146">If you `echo "$body"` you can see the full event.</span></span> <span data-ttu-id="f2e34-147">El elemento `data` del archivo JSON es la carga del evento.</span><span class="sxs-lookup"><span data-stu-id="f2e34-147">The `data` element of the JSON is the payload of your event.</span></span> <span data-ttu-id="f2e34-148">En este campo, puede usar cualquier archivo JSON bien formado.</span><span class="sxs-lookup"><span data-stu-id="f2e34-148">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="f2e34-149">También puede usar el campo de asunto para realizar enrutamiento y filtrado avanzados.</span><span class="sxs-lookup"><span data-stu-id="f2e34-149">You can also use the subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="f2e34-150">CURL es una utilidad que ejecuta solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="f2e34-150">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="f2e34-151">En este artículo, usamos CURL para enviar el evento a nuestro tema.</span><span class="sxs-lookup"><span data-stu-id="f2e34-151">In this article, we use CURL to send the event to our topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="f2e34-152">Ha desencadenado el evento y Event Grid envió el mensaje al punto de conexión configurado durante la suscripción.</span><span class="sxs-lookup"><span data-stu-id="f2e34-152">You have triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span></span> <span data-ttu-id="f2e34-153">Vaya a la dirección URL de RequestBin que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f2e34-153">Browse to the RequestBin URL that you created earlier.</span></span> <span data-ttu-id="f2e34-154">O bien, haga clic en Actualizar en el explorador de RequestBin abierto.</span><span class="sxs-lookup"><span data-stu-id="f2e34-154">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="f2e34-155">Verá el evento que se acaba de enviar.</span><span class="sxs-lookup"><span data-stu-id="f2e34-155">You see the event you just sent.</span></span> 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a><span data-ttu-id="f2e34-156">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="f2e34-156">Clean up resources</span></span>
<span data-ttu-id="f2e34-157">Si piensa seguir trabajando con este evento, no limpie los recursos creados en este artículo.</span><span class="sxs-lookup"><span data-stu-id="f2e34-157">If you plan to continue working with this event, do not clean up the resources created in this article.</span></span> <span data-ttu-id="f2e34-158">Si no va a continuar, use el siguiente comando para eliminar los recursos creados en este artículo.</span><span class="sxs-lookup"><span data-stu-id="f2e34-158">If you do not plan to continue, use the following command to delete the resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f2e34-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f2e34-159">Next steps</span></span>

<span data-ttu-id="f2e34-160">Ahora que sabe cómo crear suscripciones a temas y eventos, aprenda más sobre cómo Event Grid puede ayudarle:</span><span class="sxs-lookup"><span data-stu-id="f2e34-160">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- <span data-ttu-id="f2e34-161">[About Event Grid](overview.md) (Acerca de Event Grid)</span><span class="sxs-lookup"><span data-stu-id="f2e34-161">[About Event Grid](overview.md)</span></span>
- <span data-ttu-id="f2e34-162">[Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md) (Supervisión de los cambios en máquinas virtuales con Azure Event Grid y Logic Apps)</span><span class="sxs-lookup"><span data-stu-id="f2e34-162">[Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md)</span></span>
