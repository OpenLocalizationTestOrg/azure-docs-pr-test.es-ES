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
# <a name="create-and-route-custom-events-with-azure-event-grid"></a>Creación y enrutamiento de eventos personalizados con Azure Event Grid

Cuadrícula de eventos de Azure es un servicio de nube de Hola. En este artículo, use hello Azure CLI toocreate un tema personalizado, suscribirse toohello tema y desencadenar resultado hello tooview Hola. Por lo general, debe enviar extremo de tooan de eventos que responde el evento toohello, por ejemplo, un webhook o una función de Azure. Sin embargo, toosimplify en este artículo, enviar eventos de hello tooa dirección URL que simplemente recopila mensajes de saludo. Esta dirección URL se crea mediante una herramienta de código abierto de terceros llamada [RequestBin](https://requestb.in/).

>[!NOTE]
>**RequestBin** es una herramienta de código abierto que no está pensada para una utilización de alto rendimiento. uso de Hola de herramienta Hola aquí es meramente ilustrativos. Si se insertan más de un evento a la vez, puede que no vea todos los eventos en la herramienta de Hola.

Cuando haya terminado, verá que se ha enviado datos de eventos de hello tooan extremo.

![Datos de evento](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este artículo requiere que se ejecuta la versión más reciente de Hola de CLI de Azure (2.0.14 o posterior). versión de hello toofind, ejecute `az --version`. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Los temas de Event Grid son recursos de Azure y se deben colocar en un grupo de recursos de Azure. grupo de recursos de Hello es una colección lógica en que Azure se implementan y administran los recursos.

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *gridResourceGroup* en hello *westus2* ubicación.

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a>Creación de un tema personalizado

Un tema proporciona un punto de conexión definido por el usuario en el que se registran los eventos. Hello en el ejemplo siguiente se crea el tema de hello en el grupo de recursos. Reemplace `<topic_name>` por un nombre único para el tema. el nombre del tema Hola debe ser único porque se representa mediante una entrada DNS. Para la versión de vista previa de hello, admite la cuadrícula de eventos **westus2** y **westcentralus** ubicaciones.

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a>Creación de un punto de conexión de mensaje

Antes de suscribir toohello tema, vamos a crear punto de conexión de Hola para mensajes de bienvenida del evento. En lugar de escribir eventos de código toorespond toohello, vamos a crear un extremo que recopila mensajes de Hola para que pueda verlas. RequestBin es un código abierto, herramienta de terceros que permite toocreate un punto de conexión y ver solicitudes que se envían tooit. Vaya demasiado[RequestBin](https://requestb.in/)y haga clic en **crear un RequestBin**.  Copiar dirección URL de ubicación de hello, porque lo necesitará al suscribirse toohello tema.

## <a name="subscribe-tooa-topic"></a>Suscribirse tooa tema

Suscribirse tooa tema tootell cuadrícula de eventos los eventos que desea tootrack. Hello en el ejemplo siguiente se suscribe toohello tema que creó y, después, pasa la dirección URL de Hola de RequestBin como extremo de Hola para notificación de eventos. Reemplace `<event_subscription_name>` con un nombre único para la suscripción, y `<URL_from_RequestBin>` con valor de Hola de hello sección anterior. Al especificar un punto de conexión cuando se suscriba, cuadrícula de eventos controla Hola enrutamiento de punto de conexión de eventos toothat. Para `<topic_name>`, use valor Hola que creó anteriormente. 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a>Enviar un tema de tooyour de eventos

Ahora, vamos a desencadenar un evento toosee cómo distribuye el punto de conexión de tooyour de mensajes de Hola cuadrícula de eventos. En primer lugar, vamos a obtener la dirección URL de Hola y la clave de tema de Hola. De nuevo, use el nombre de su tema en `<topic_name>`.

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

toosimplify este artículo, hemos configurado hasta el tema de toohello del toosend de datos de evento de ejemplo. Normalmente, una aplicación o servicio de Azure enviaba datos de evento de saludo. Hola siguiente ejemplo obtiene datos de eventos de hello:

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

Si se `echo "$body"` puede ver eventos de hello completa. Hola `data` elemento de hello JSON es carga Hola del evento. En este campo, puede usar cualquier archivo JSON bien formado. También puede usar el campo de asunto Hola para enrutamiento y filtrado avanzados.

CURL es una utilidad que ejecuta solicitudes HTTP. En este artículo, usamos el tema tooour eventos CURL toosend Hola. 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

Desencadenó el evento de Hola y cuadrícula de eventos envía el extremo del mensaje de Hola toohello configurado al suscribirse. Examinar toohello RequestBin URL que creó anteriormente. O bien, haga clic en Actualizar en el explorador de RequestBin abierto. Ver eventos de hello que acabamos de enviar. 

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

## <a name="clean-up-resources"></a>Limpieza de recursos
Si tiene previsto trabajar con este evento de toocontinue, hacer no limpiar recursos de hello creados en este artículo. Si no tiene previsto toocontinue, use Hola comando toodelete Hola recursos que creó en este artículo siguientes.

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

Ahora que sabe cómo toocreate temas y suscripciones a eventos, obtener más información acerca de la cuadrícula de eventos puede ayudarle a hacerlo:

- [About Event Grid](overview.md) (Acerca de Event Grid)
- [Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md) (Supervisión de los cambios en máquinas virtuales con Azure Event Grid y Logic Apps)
