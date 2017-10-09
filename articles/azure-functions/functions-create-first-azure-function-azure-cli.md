---
title: "aaaCreate la primera función de hello CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate su primera Azure funcionar para la ejecución sin servidor con Hola CLI de Azure."
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a>Crear la primera función mediante Hola CLI de Azure

Este tutorial de inicio rápido le guía por el proceso de toouse funciones de Azure toocreate la primera función. Utilice hello Azure CLI toocreate una aplicación de función, que es Hola infraestructura sin servidor que hospeda la función. código de la función de Hello propio se implementa desde un repositorio de ejemplo de GitHub.    

Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux. 

## <a name="prerequisites"></a>Requisitos previos 

Antes de ejecutar este ejemplo, debe tener el siguiente hello:

+ Una cuenta de [GitHub](https://github.com) activa. 
+ Una suscripción de Azure activa.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create). Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran recursos de Azure como instancias de Function App, bases de datos y cuentas de almacenamiento.

Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup`.  
Si no usa Cloud Shell, primero debe iniciar sesión con `az login`.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a>Creación de una cuenta de almacenamiento de Azure

Funciones usa un estado de toomaintain de cuenta de almacenamiento de Azure y otra información sobre las funciones. Crear una cuenta de almacenamiento en grupo de recursos de hello creada mediante hello [crear cuenta de almacenamiento az](/cli/azure/storage/account#create) comando.

Hola siguiente comando, sustituya su propio nombre de cuenta de almacenamiento único global donde verá hello `<storage_name>` marcador de posición. Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y solo pueden contener números y letras minúsculas.

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

Una vez creada la cuenta de almacenamiento de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a>Creación de una aplicación de función

Debe tener una ejecución de la función aplicación toohost Hola de las funciones. aplicación de la función de Hello proporciona un entorno de ejecución sin servidor de su código de la función. Le permite agrupar funciones como una unidad lógica para facilitar la administración, la implementación y el uso compartido de recursos. Crear una aplicación de la función mediante hello [crear az functionapp](/cli/azure/functionapp#create) comando. 

Hola siguiente comando, sustituya su propio nombre de la aplicación de función única donde verá hello `<app_name>` hello y marcador de posición de nombre de cuenta de almacenamiento para `<storage_name>`. Hola `<app_name>` se usa como dominio DNS de hello predeterminado de aplicación de función de Hola y ese nombre hello necesita toobe único en todas las aplicaciones de Azure. 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
De forma predeterminada, se crea una aplicación de la función con el plan de hospedaje de consumo de hello, lo que significa que los recursos se agregan dinámicamente según sea necesario por las funciones y solo se paga cuando se están ejecutando las funciones. Para obtener más información, consulte [plan de hospedaje correcta elegir hello](functions-scale.md). 

Una vez creada la aplicación de la función de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

Ahora que tiene una aplicación de función, puede implementar código de la función real de Hola desde el repositorio de ejemplo de Hola GitHub.

## <a name="deploy-your-function-code"></a>Implementar el código de función  

Hay toocreate de varias maneras el código de función en la nueva aplicación de función. En este tema se conecta tooa repositorio de ejemplo en GitHub. Como antes, en hello sigue código reemplace hello `<app_name>` marcador de posición con nombre Hola de aplicación de función hello que creó. 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
Después de la implementación de hello origen estableció, Hola CLI de Azure muestra información toohello similar siguiente ejemplo (valores null quitados para mayor legibilidad):

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-hello-function"></a>Probar función hello

Usar funciones de hello implementado de cURL tootest en un equipo Mac o Linux o mediante intensiva de errores en Windows. Ejecutar Hola siguiente cURL comando, reemplazando hello `<app_name>` marcador de posición con nombre hello de la aplicación de la función. Anexar la cadena de consulta de hello `&name=<yourname>` toohello URL.

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![La respuesta de función que se muestra en un explorador.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

Si no tienes cURL disponible en la línea de comandos, escriba Hola la misma dirección URL en la dirección de hello del explorador web. Hola de nuevo, reemplazar `<app_name>` marcador de posición con nombre hello de la aplicación de la función y anexar la cadena de consulta de hello `&name=<yourname>` toohello URL y ejecutar la solicitud de saludo. 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![La respuesta de función que se muestra en un explorador.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a>Limpieza de recursos

Otras guías de inicio rápido de esta colección se basan en los valores de esta. Si tiene previsto toocontinue toowork con tutoriales posteriores, o con los tutoriales de hello, realice no limpiar los recursos de hello creados en este tutorial rápido. Si no tiene previsto toocontinue, usar hello después comando toodelete todos los recursos creados por este tutorial rápido:

```azurecli-interactive
az group delete --name myResourceGroup
```
Cuando se le solicite, escriba `y`.

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
