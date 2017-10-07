---
title: aaaCreate un centro de IoT mediante Azure CLI (az.py) | Documentos de Microsoft
description: "¿Cómo toocreate un centro de IoT de Azure utilizando Hola multiplataforma Azure CLI 2.0 (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a>Crear un centro de IoT con hello 2.0 de CLI de Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introducción

Puede usar toocreate de CLI de Azure 2.0 (az.py) y administrar los centros de IoT de Azure mediante programación. Este artículo muestra cómo toouse Hola toocreate de CLI de Azure 2.0 (az.py) a un centro de IoT.

Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

* [CLI de Azure (azure.js)](iot-hub-create-using-cli-nodejs.md) : Hola CLI para modelos de implementación de administración de recursos y clásico Hola.
* Azure CLI 2.0 (az.py) - Hola CLI de próxima generación para el modelo de implementación de administración de hello recursos tal como se describe en este artículo.

toocomplete este tutorial, necesita Hola siguientes:

* Una cuenta de Azure activa. Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.
* [CLI de Azure 2.0][lnk-CLI-install].

## <a name="sign-in-and-set-your-azure-account"></a>Inicio de sesión y configuración de la cuenta de Azure

Inicie sesión en tooyour cuenta de Azure y seleccione su suscripción.

1. En el símbolo de hello, ejecute hello [comando de inicio de sesión][lnk-login-command]:
    
    ```azurecli
    az login
    ```

    Siga Hola instrucciones tooauthenticate utilizando el código de hello e inicie sesión en tooyour cuenta de Azure a través de un explorador web.

2. Si tiene varias suscripciones de Azure, iniciar sesión en tooAzure concede acceso tooall Hola asociadas con sus credenciales de cuentas de Azure. Utilice Hola siguiente [toolist comando Hola cuentas de Azure] [ lnk-az-account-command] disponibles para toouse:
    
    ```azurecli
    az account list 
    ```

    Usar hello después de suscripción de tooselect de comando que desea toouse toorun Hola comandos toocreate su centro de IoT. Puede usar el nombre de la suscripción de Hola o Id. de salida de hello del comando anterior hello:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a>Creación de un IoT Hub

Use hello Azure CLI toocreate un grupo de recursos y, a continuación, agregue un centro de IoT.

1. Cuando crea una instancia de IoT Hub, debe crearla en un grupo de recursos. Utilice un grupo de recursos existente, o bien ejecute hello siguiente [comando toocreate un grupo de recursos][lnk-az-resource-command]:
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > ejemplo de Hola anterior crea grupo de recursos de hello en hello ubicación oeste de EE.. Puede ver una lista de ubicaciones disponibles mediante la ejecución de comando hello `az account list-locations -o table`.
    >
    >

2. Ejecute hello siguiente [comando toocreate un centro de IoT] [ lnk-az-iot-command] en el grupo de recursos, con un nombre único global para el centro de IoT:
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> comando anterior Hola crea un centro de IoT en hello S1 para el que se le cobra según el nivel de precios. Para más información, consulte el artículo sobre los [precios de Azure IoT Hub][lnk-iot-pricing].
>
>

## <a name="remove-an-iot-hub"></a>Eliminación de una instancia de IoT Hub

Puede usar hello Azure CLI demasiado[eliminar un recurso individual][lnk-az-resource-command], como un centro de IoT o eliminar un grupo de recursos y todos sus recursos, incluidos los centros de IoT.

toodelete un centro de IoT, ejecute el siguiente comando de hello:

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

toodelete de comandos de un grupo de recursos y todos sus recursos, ejecución Hola siguientes:

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a>Pasos siguientes
toolearn más sobre el desarrollo de centro de IoT, vea Hola siguientes artículos:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Uso de hello toomanage portal Azure centro de IoT][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
