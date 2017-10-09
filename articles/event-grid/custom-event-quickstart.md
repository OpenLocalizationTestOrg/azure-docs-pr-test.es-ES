---
title: "eventos de aaaCustom de cuadrícula de eventos de Azure | Documentos de Microsoft"
description: "Utilice la cuadrícula de eventos de Azure toopublish un tema y suscribir el evento toothat."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="37c34-103">Creación y enrutamiento de eventos personalizados con Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="37c34-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="37c34-104">Cuadrícula de eventos de Azure es un servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c34-104">Azure Event Grid is an eventing service for hello cloud.</span></span> <span data-ttu-id="37c34-105">En este artículo, use hello Azure CLI toocreate un tema personalizado, suscribirse toohello tema y desencadenar resultado hello tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="37c34-105">In this article, you use hello Azure CLI toocreate a custom topic, subscribe toohello topic, and trigger hello event tooview hello result.</span></span> <span data-ttu-id="37c34-106">Por lo general, debe enviar extremo de tooan de eventos que responde el evento toohello, por ejemplo, un webhook o una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="37c34-106">Typically, you send events tooan endpoint that responds toohello event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="37c34-107">Sin embargo, toosimplify en este artículo, enviar eventos de hello tooa dirección URL que simplemente recopila mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="37c34-107">However, toosimplify this article, you send hello events tooa URL that merely collects hello messages.</span></span> <span data-ttu-id="37c34-108">Esta dirección URL se crea mediante una herramienta de código abierto de terceros llamada [RequestBin](https://requestb.in/).</span><span class="sxs-lookup"><span data-stu-id="37c34-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="37c34-109">**RequestBin** es una herramienta de código abierto que no está pensada para una utilización de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="37c34-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="37c34-110">uso de Hola de herramienta Hola aquí es meramente ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="37c34-110">hello use of hello tool here is purely demonstrative.</span></span> <span data-ttu-id="37c34-111">Si se insertan más de un evento a la vez, puede que no vea todos los eventos en la herramienta de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c34-111">If you push more than one event at a time, you might not see all of your events in hello tool.</span></span>

<span data-ttu-id="37c34-112">Cuando haya terminado, verá que se ha enviado datos de eventos de hello tooan extremo.</span><span class="sxs-lookup"><span data-stu-id="37c34-112">When you are finished, you see that hello event data has been sent tooan endpoint.</span></span>

![Datos de evento](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="37c34-114">Si elige tooinstall y usar hello CLI localmente, en este artículo requiere que se ejecuta la versión más reciente de Hola de CLI de Azure (2.0.14 o posterior).</span><span class="sxs-lookup"><span data-stu-id="37c34-114">If you choose tooinstall and use hello CLI locally, this article requires that you are running hello latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="37c34-115">versión de hello toofind, ejecute `az --version`.</span><span class="sxs-lookup"><span data-stu-id="37c34-115">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="37c34-116">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="37c34-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="37c34-117">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="37c34-117">Create a resource group</span></span>

<span data-ttu-id="37c34-118">Los temas de Event Grid son recursos de Azure y se deben colocar en un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="37c34-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="37c34-119">grupo de recursos de Hello es una colección lógica en que Azure se implementan y administran los recursos.</span><span class="sxs-lookup"><span data-stu-id="37c34-119">hello resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="37c34-120">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="37c34-120">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="37c34-121">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *gridResourceGroup* en hello *westus2* ubicación.</span><span class="sxs-lookup"><span data-stu-id="37c34-121">hello following example creates a resource group named *gridResourceGroup* in hello *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="37c34-122">Creación de un tema personalizado</span><span class="sxs-lookup"><span data-stu-id="37c34-122">Create a custom topic</span></span>

<span data-ttu-id="37c34-123">Un tema proporciona un punto de conexión definido por el usuario en el que se registran los eventos.</span><span class="sxs-lookup"><span data-stu-id="37c34-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="37c34-124">Hello en el ejemplo siguiente se crea el tema de hello en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="37c34-124">hello following example creates hello topic in your resource group.</span></span> <span data-ttu-id="37c34-125">Reemplace `<topic_name>` por un nombre único para el tema.</span><span class="sxs-lookup"><span data-stu-id="37c34-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="37c34-126">el nombre del tema Hola debe ser único porque se representa mediante una entrada DNS.</span><span class="sxs-lookup"><span data-stu-id="37c34-126">hello topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="37c34-127">Para la versión de vista previa de hello, admite la cuadrícula de eventos **westus2** y **westcentralus** ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="37c34-127">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="37c34-128">Creación de un punto de conexión de mensaje</span><span class="sxs-lookup"><span data-stu-id="37c34-128">Create a message endpoint</span></span>

<span data-ttu-id="37c34-129">Antes de suscribir toohello tema, vamos a crear punto de conexión de Hola para mensajes de bienvenida del evento.</span><span class="sxs-lookup"><span data-stu-id="37c34-129">Before subscribing toohello topic, let's create hello endpoint for hello event message.</span></span> <span data-ttu-id="37c34-130">En lugar de escribir eventos de código toorespond toohello, vamos a crear un extremo que recopila mensajes de Hola para que pueda verlas.</span><span class="sxs-lookup"><span data-stu-id="37c34-130">Rather than write code toorespond toohello event, let's create an endpoint that collects hello messages so you can view them.</span></span> <span data-ttu-id="37c34-131">RequestBin es un código abierto, herramienta de terceros que permite toocreate un punto de conexión y ver solicitudes que se envían tooit.</span><span class="sxs-lookup"><span data-stu-id="37c34-131">RequestBin is an open source, third-party tool that enables you toocreate an endpoint, and view requests that are sent tooit.</span></span> <span data-ttu-id="37c34-132">Vaya demasiado[RequestBin](https://requestb.in/)y haga clic en **crear un RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="37c34-132">Go too[RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="37c34-133">Copiar dirección URL de ubicación de hello, porque lo necesitará al suscribirse toohello tema.</span><span class="sxs-lookup"><span data-stu-id="37c34-133">Copy hello bin URL, because you need it when subscribing toohello topic.</span></span>

## <a name="subscribe-tooa-topic"></a><span data-ttu-id="37c34-134">Suscribirse tooa tema</span><span class="sxs-lookup"><span data-stu-id="37c34-134">Subscribe tooa topic</span></span>

<span data-ttu-id="37c34-135">Suscribirse tooa tema tootell cuadrícula de eventos los eventos que desea tootrack.</span><span class="sxs-lookup"><span data-stu-id="37c34-135">You subscribe tooa topic tootell Event Grid which events you want tootrack.</span></span> <span data-ttu-id="37c34-136">Hello en el ejemplo siguiente se suscribe toohello tema que creó y, después, pasa la dirección URL de Hola de RequestBin como extremo de Hola para notificación de eventos.</span><span class="sxs-lookup"><span data-stu-id="37c34-136">hello following example subscribes toohello topic you created, and passes hello URL from RequestBin as hello endpoint for event notification.</span></span> <span data-ttu-id="37c34-137">Reemplace `<event_subscription_name>` con un nombre único para la suscripción, y `<URL_from_RequestBin>` con valor de Hola de hello sección anterior.</span><span class="sxs-lookup"><span data-stu-id="37c34-137">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with hello value from hello preceding section.</span></span> <span data-ttu-id="37c34-138">Al especificar un punto de conexión cuando se suscriba, cuadrícula de eventos controla Hola enrutamiento de punto de conexión de eventos toothat.</span><span class="sxs-lookup"><span data-stu-id="37c34-138">By specifying an endpoint when subscribing, Event Grid handles hello routing of events toothat endpoint.</span></span> <span data-ttu-id="37c34-139">Para `<topic_name>`, use valor Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="37c34-139">For `<topic_name>`, use hello value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a><span data-ttu-id="37c34-140">Enviar un tema de tooyour de eventos</span><span class="sxs-lookup"><span data-stu-id="37c34-140">Send an event tooyour topic</span></span>

<span data-ttu-id="37c34-141">Ahora, vamos a desencadenar un evento toosee cómo distribuye el punto de conexión de tooyour de mensajes de Hola cuadrícula de eventos.</span><span class="sxs-lookup"><span data-stu-id="37c34-141">Now, let's trigger an event toosee how Event Grid distributes hello message tooyour endpoint.</span></span> <span data-ttu-id="37c34-142">En primer lugar, vamos a obtener la dirección URL de Hola y la clave de tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c34-142">First, let's get hello URL and key for hello topic.</span></span> <span data-ttu-id="37c34-143">De nuevo, use el nombre de su tema en `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="37c34-143">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="37c34-144">toosimplify este artículo, hemos configurado hasta el tema de toohello del toosend de datos de evento de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="37c34-144">toosimplify this article, we have set up sample event data toosend toohello topic.</span></span> <span data-ttu-id="37c34-145">Normalmente, una aplicación o servicio de Azure enviaba datos de evento de saludo.</span><span class="sxs-lookup"><span data-stu-id="37c34-145">Typically, an application or Azure service would send hello event data.</span></span> <span data-ttu-id="37c34-146">Hola siguiente ejemplo obtiene datos de eventos de hello:</span><span class="sxs-lookup"><span data-stu-id="37c34-146">hello following example gets hello event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="37c34-147">Si se `echo "$body"` puede ver eventos de hello completa.</span><span class="sxs-lookup"><span data-stu-id="37c34-147">If you `echo "$body"` you can see hello full event.</span></span> <span data-ttu-id="37c34-148">Hola `data` elemento de hello JSON es carga Hola del evento.</span><span class="sxs-lookup"><span data-stu-id="37c34-148">hello `data` element of hello JSON is hello payload of your event.</span></span> <span data-ttu-id="37c34-149">En este campo, puede usar cualquier archivo JSON bien formado.</span><span class="sxs-lookup"><span data-stu-id="37c34-149">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="37c34-150">También puede usar el campo de asunto Hola para enrutamiento y filtrado avanzados.</span><span class="sxs-lookup"><span data-stu-id="37c34-150">You can also use hello subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="37c34-151">CURL es una utilidad que ejecuta solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="37c34-151">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="37c34-152">En este artículo, usamos el tema tooour eventos CURL toosend Hola.</span><span class="sxs-lookup"><span data-stu-id="37c34-152">In this article, we use CURL toosend hello event tooour topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="37c34-153">Desencadenó el evento de Hola y cuadrícula de eventos envía el extremo del mensaje de Hola toohello configurado al suscribirse.</span><span class="sxs-lookup"><span data-stu-id="37c34-153">You have triggered hello event, and Event Grid sent hello message toohello endpoint you configured when subscribing.</span></span> <span data-ttu-id="37c34-154">Examinar toohello RequestBin URL que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="37c34-154">Browse toohello RequestBin URL that you created earlier.</span></span> <span data-ttu-id="37c34-155">O bien, haga clic en Actualizar en el explorador de RequestBin abierto.</span><span class="sxs-lookup"><span data-stu-id="37c34-155">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="37c34-156">Ver eventos de hello que acabamos de enviar.</span><span class="sxs-lookup"><span data-stu-id="37c34-156">You see hello event you just sent.</span></span> 

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

## <a name="clean-up-resources"></a><span data-ttu-id="37c34-157">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="37c34-157">Clean up resources</span></span>
<span data-ttu-id="37c34-158">Si tiene previsto trabajar con este evento de toocontinue, hacer no limpiar recursos de hello creados en este artículo.</span><span class="sxs-lookup"><span data-stu-id="37c34-158">If you plan toocontinue working with this event, do not clean up hello resources created in this article.</span></span> <span data-ttu-id="37c34-159">Si no tiene previsto toocontinue, use Hola comando toodelete Hola recursos que creó en este artículo siguientes.</span><span class="sxs-lookup"><span data-stu-id="37c34-159">If you do not plan toocontinue, use hello following command toodelete hello resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="37c34-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37c34-160">Next steps</span></span>

<span data-ttu-id="37c34-161">Ahora que sabe cómo toocreate temas y suscripciones a eventos, obtener más información acerca de la cuadrícula de eventos puede ayudarle a hacerlo:</span><span class="sxs-lookup"><span data-stu-id="37c34-161">Now that you know how toocreate topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- <span data-ttu-id="37c34-162">[About Event Grid](overview.md) (Acerca de Event Grid)</span><span class="sxs-lookup"><span data-stu-id="37c34-162">[About Event Grid](overview.md)</span></span>
- <span data-ttu-id="37c34-163">[Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md) (Supervisión de los cambios en máquinas virtuales con Azure Event Grid y Logic Apps)</span><span class="sxs-lookup"><span data-stu-id="37c34-163">[Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md)</span></span>
