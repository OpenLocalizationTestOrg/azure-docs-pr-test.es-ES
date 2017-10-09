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
# <a name="create-your-first-function-using-hello-azure-cli"></a><span data-ttu-id="e483b-103">Crear la primera función mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e483b-103">Create your first function using hello Azure CLI</span></span>

<span data-ttu-id="e483b-104">Este tutorial de inicio rápido le guía por el proceso de toouse funciones de Azure toocreate la primera función.</span><span class="sxs-lookup"><span data-stu-id="e483b-104">This quickstart tutorial walks through how toouse Azure Functions toocreate your first function.</span></span> <span data-ttu-id="e483b-105">Utilice hello Azure CLI toocreate una aplicación de función, que es Hola infraestructura sin servidor que hospeda la función.</span><span class="sxs-lookup"><span data-stu-id="e483b-105">You use hello Azure CLI toocreate a function app, which is hello serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="e483b-106">código de la función de Hello propio se implementa desde un repositorio de ejemplo de GitHub.</span><span class="sxs-lookup"><span data-stu-id="e483b-106">hello function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="e483b-107">Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="e483b-107">You can follow hello steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e483b-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e483b-108">Prerequisites</span></span> 

<span data-ttu-id="e483b-109">Antes de ejecutar este ejemplo, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="e483b-109">Before running this sample, you must have hello following:</span></span>

+ <span data-ttu-id="e483b-110">Una cuenta de [GitHub](https://github.com) activa.</span><span class="sxs-lookup"><span data-stu-id="e483b-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="e483b-111">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="e483b-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e483b-112">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e483b-112">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e483b-113">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e483b-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e483b-114">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e483b-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="e483b-115">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e483b-115">Create a resource group</span></span>

<span data-ttu-id="e483b-116">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e483b-116">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e483b-117">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran recursos de Azure como instancias de Function App, bases de datos y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e483b-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="e483b-118">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e483b-118">hello following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="e483b-119">Si no usa Cloud Shell, primero debe iniciar sesión con `az login`.</span><span class="sxs-lookup"><span data-stu-id="e483b-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="e483b-120">Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e483b-120">Create an Azure Storage account</span></span>

<span data-ttu-id="e483b-121">Funciones usa un estado de toomaintain de cuenta de almacenamiento de Azure y otra información sobre las funciones.</span><span class="sxs-lookup"><span data-stu-id="e483b-121">Functions uses an Azure Storage account toomaintain state and other information about your functions.</span></span> <span data-ttu-id="e483b-122">Crear una cuenta de almacenamiento en grupo de recursos de hello creada mediante hello [crear cuenta de almacenamiento az](/cli/azure/storage/account#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e483b-122">Create a storage account in hello resource group you created by using hello [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="e483b-123">Hola siguiente comando, sustituya su propio nombre de cuenta de almacenamiento único global donde verá hello `<storage_name>` marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="e483b-123">In hello following command, substitute your own globally unique storage account name where you see hello `<storage_name>` placeholder.</span></span> <span data-ttu-id="e483b-124">Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y solo pueden contener números y letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e483b-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="e483b-125">Una vez creada la cuenta de almacenamiento de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e483b-125">After hello storage account has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="create-a-function-app"></a><span data-ttu-id="e483b-126">Creación de una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="e483b-126">Create a function app</span></span>

<span data-ttu-id="e483b-127">Debe tener una ejecución de la función aplicación toohost Hola de las funciones.</span><span class="sxs-lookup"><span data-stu-id="e483b-127">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="e483b-128">aplicación de la función de Hello proporciona un entorno de ejecución sin servidor de su código de la función.</span><span class="sxs-lookup"><span data-stu-id="e483b-128">hello function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="e483b-129">Le permite agrupar funciones como una unidad lógica para facilitar la administración, la implementación y el uso compartido de recursos.</span><span class="sxs-lookup"><span data-stu-id="e483b-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="e483b-130">Crear una aplicación de la función mediante hello [crear az functionapp](/cli/azure/functionapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e483b-130">Create a function app by using hello [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="e483b-131">Hola siguiente comando, sustituya su propio nombre de la aplicación de función única donde verá hello `<app_name>` hello y marcador de posición de nombre de cuenta de almacenamiento para `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="e483b-131">In hello following command, substitute your own unique function app name where you see hello `<app_name>` placeholder and hello storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="e483b-132">Hola `<app_name>` se usa como dominio DNS de hello predeterminado de aplicación de función de Hola y ese nombre hello necesita toobe único en todas las aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="e483b-132">hello `<app_name>` is used as hello default DNS domain for hello function app, and so hello name needs toobe unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="e483b-133">De forma predeterminada, se crea una aplicación de la función con el plan de hospedaje de consumo de hello, lo que significa que los recursos se agregan dinámicamente según sea necesario por las funciones y solo se paga cuando se están ejecutando las funciones.</span><span class="sxs-lookup"><span data-stu-id="e483b-133">By default, a function app is created with hello Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="e483b-134">Para obtener más información, consulte [plan de hospedaje correcta elegir hello](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="e483b-134">For more information, see [Choose hello correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="e483b-135">Una vez creada la aplicación de la función de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e483b-135">After hello function app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="e483b-136">Ahora que tiene una aplicación de función, puede implementar código de la función real de Hola desde el repositorio de ejemplo de Hola GitHub.</span><span class="sxs-lookup"><span data-stu-id="e483b-136">Now that you have a function app, you can deploy hello actual function code from hello GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="e483b-137">Implementar el código de función</span><span class="sxs-lookup"><span data-stu-id="e483b-137">Deploy your function code</span></span>  

<span data-ttu-id="e483b-138">Hay toocreate de varias maneras el código de función en la nueva aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="e483b-138">There are several ways toocreate your function code in your new function app.</span></span> <span data-ttu-id="e483b-139">En este tema se conecta tooa repositorio de ejemplo en GitHub.</span><span class="sxs-lookup"><span data-stu-id="e483b-139">This topic connects tooa sample repository in GitHub.</span></span> <span data-ttu-id="e483b-140">Como antes, en hello sigue código reemplace hello `<app_name>` marcador de posición con nombre Hola de aplicación de función hello que creó.</span><span class="sxs-lookup"><span data-stu-id="e483b-140">As before, in hello following code replace hello `<app_name>` placeholder with hello name of hello function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="e483b-141">Después de la implementación de hello origen estableció, Hola CLI de Azure muestra información toohello similar siguiente ejemplo (valores null quitados para mayor legibilidad):</span><span class="sxs-lookup"><span data-stu-id="e483b-141">After hello deployment source been set, hello Azure CLI shows information similar toohello following example (null values removed for readability):</span></span>

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

## <a name="test-hello-function"></a><span data-ttu-id="e483b-142">Probar función hello</span><span class="sxs-lookup"><span data-stu-id="e483b-142">Test hello function</span></span>

<span data-ttu-id="e483b-143">Usar funciones de hello implementado de cURL tootest en un equipo Mac o Linux o mediante intensiva de errores en Windows.</span><span class="sxs-lookup"><span data-stu-id="e483b-143">Use cURL tootest hello deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="e483b-144">Ejecutar Hola siguiente cURL comando, reemplazando hello `<app_name>` marcador de posición con nombre hello de la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="e483b-144">Execute hello following cURL command, replacing hello `<app_name>` placeholder with hello name of your function app.</span></span> <span data-ttu-id="e483b-145">Anexar la cadena de consulta de hello `&name=<yourname>` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="e483b-145">Append hello query string `&name=<yourname>` toohello URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![La respuesta de función que se muestra en un explorador.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="e483b-147">Si no tienes cURL disponible en la línea de comandos, escriba Hola la misma dirección URL en la dirección de hello del explorador web.</span><span class="sxs-lookup"><span data-stu-id="e483b-147">If you don't have cURL available in your command line, enter hello same URL in hello address of your web browser.</span></span> <span data-ttu-id="e483b-148">Hola de nuevo, reemplazar `<app_name>` marcador de posición con nombre hello de la aplicación de la función y anexar la cadena de consulta de hello `&name=<yourname>` toohello URL y ejecutar la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="e483b-148">Again, replace hello `<app_name>` placeholder with hello name of your function app, and append hello query string `&name=<yourname>` toohello URL and execute hello request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![La respuesta de función que se muestra en un explorador.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="e483b-150">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="e483b-150">Clean up resources</span></span>

<span data-ttu-id="e483b-151">Otras guías de inicio rápido de esta colección se basan en los valores de esta.</span><span class="sxs-lookup"><span data-stu-id="e483b-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="e483b-152">Si tiene previsto toocontinue toowork con tutoriales posteriores, o con los tutoriales de hello, realice no limpiar los recursos de hello creados en este tutorial rápido.</span><span class="sxs-lookup"><span data-stu-id="e483b-152">If you plan toocontinue on toowork with subsequent quickstarts or with hello tutorials, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="e483b-153">Si no tiene previsto toocontinue, usar hello después comando toodelete todos los recursos creados por este tutorial rápido:</span><span class="sxs-lookup"><span data-stu-id="e483b-153">If you do not plan toocontinue, use hello following command toodelete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="e483b-154">Cuando se le solicite, escriba `y`.</span><span class="sxs-lookup"><span data-stu-id="e483b-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e483b-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e483b-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
