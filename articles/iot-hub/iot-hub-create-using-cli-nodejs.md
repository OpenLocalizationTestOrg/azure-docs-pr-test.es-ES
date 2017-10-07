---
title: aaaCreate un centro de IoT mediante Azure CLI (azure.js) | Documentos de Microsoft
description: "¿Cómo toocreate un centro de IoT de Azure utilizando Hola multiplataforma Azure CLI (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a>Crear un centro de IoT con hello CLI de Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introducción

Puede usar toocreate de CLI de Azure (azure.js) y administrar los centros de IoT de Azure mediante programación. Este artículo muestra cómo toouse Hola toocreate de CLI de Azure (azure.js) a un centro de IoT.

Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

* CLI de Azure (azure.js): Hola CLI hello clásico y modelos de implementación de administración de recursos como se describe en este artículo.
* [Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -Hola CLI de próxima generación para el modelo de implementación de administración de recursos de Hola.

toocomplete este tutorial, necesita Hola siguientes:

* Una cuenta de Azure activa. En caso de no tener ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.
* [CLI de Azure 0.10.4][lnk-CLI-install] o una versión posterior. Si ya tienes Hola CLI de Azure instalado, puede validar versión actual de hello en el símbolo del sistema Hola con hello siguiente comando:

```azurecli
azure --version
```

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y clásico](../azure-resource-manager/resource-manager-deployment-model.md). Hola CLI de Azure debe estar en modo Azure Resource Manager:
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a>Definición de su cuenta y suscripción de Azure

1. En el símbolo de hello, inicio de sesión, escriba Hola siguiente comando:

   ```azurecli
    azure login
   ```

   Hola uso sugerido explorador web y tooauthenticate de código.
1. Si tiene varias suscripciones de Azure, conectar tooAzure concede acceso tooall hello Azure suscripciones asociadas con sus credenciales. Puede ver Hola suscripciones de Azure e identifique cuál es la predeterminada de hello, mediante el comando hello:

   ```azurecli
    azure account list
   ```

   uso de comandos de contexto de suscripción de hello tooset bajo el cual desea rest de hello toorun de hello:

   ```azurecli
    azure account set <subscription name>
   ```

1. Si no tiene un grupo de recursos, puede crear uno denominado **exampleResourceGroup**:

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> artículo de Hello [usar hello Azure CLI toomanage Azure y grupos de recursos] [ lnk-CLI-arm] proporciona más información acerca de cómo toouse hello Azure CLI toomanage Azure recursos.

## <a name="create-an-iot-hub"></a>Creación de un IoT Hub

Parámetros obligatorios:

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* **resource-group**. nombre del grupo de recursos de Hola. formato de Hello es entre mayúsculas y minúsculas alfanuméricos, caracteres de subrayado y guiones, longitud de 1-64.
* **nombre**. nombre de Hola de hello IoT hub toobe creado. formato de Hello es entre mayúsculas y minúsculas alfanuméricos, caracteres de subrayado y guiones, longitud de 3-50.
* **location**. Centro de IoT Hola de Hello ubicación (región/centro de datos azure) tooprovision.
* **sku-name**. nombre de Hola de sku de hello, uno de: [F1, S1, S2, S3]. Para la lista completa de hello más reciente, consulte toohello página de precios para el centro de IoT.
* **units**. número de Hola de unidades de aprovisionamiento. Intervalo: F1 [1-1] : S1, S2 [1-200] : S3 [1-10]. Unidades de centro de IoT se basan en el número total de mensajes, hello y recuento de dispositivos que desee tooconnect.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

toosee Hola a todos los parámetros disponibles para la creación, puede usar comandos de la Ayuda de hello en el símbolo del sistema:

```azurecli
azure iothub create -h
```

Ejemplo rápido: toocreate llama a un centro de IoT **exampleIoTHubName** en grupo de recursos de hello **exampleResourceGroup**, ejecute hello comando siguiente:

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> Este comando de la CLI de Azure crea un IoT Hub Estándar S1 por el que se le cobrará. Puede eliminar el centro de IoT de hello **exampleIoTHubName** con el comando siguiente:
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a>Pasos siguientes

toolearn más sobre el desarrollo de centro de IoT, vea Hola artículo siguiente:

* [SDK de IoT][lnk-sdks]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Uso de hello toomanage portal Azure centro de IoT][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
