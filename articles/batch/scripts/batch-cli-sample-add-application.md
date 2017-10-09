---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure agregar una aplicación en el lote | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: adición de una aplicación a Batch"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a><span data-ttu-id="cebd5-103">Agregar aplicaciones tooAzure por lotes con CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cebd5-103">Adding applications tooAzure Batch with Azure CLI</span></span>

<span data-ttu-id="cebd5-104">Este script muestra cómo tooset una aplicación para su uso con un grupo de lote de Azure o la tarea.</span><span class="sxs-lookup"><span data-stu-id="cebd5-104">This script demonstrates how tooset up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="cebd5-105">tooset de una aplicación, empaquetar una aplicación ejecutable, junto con las dependencias, en un archivo .zip.</span><span class="sxs-lookup"><span data-stu-id="cebd5-105">tooset up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="cebd5-106">En este archivo zip ejecutable de ejemplo Hola archivo se denomina ' Mi-aplicaciones-exe.zip'.</span><span class="sxs-lookup"><span data-stu-id="cebd5-106">In this example hello executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cebd5-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cebd5-107">Prerequisites</span></span>

- <span data-ttu-id="cebd5-108">Instalación Hola CLI de Azure utilizando instrucciones de hello proporcionadas en hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="cebd5-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="cebd5-109">Cree una cuenta de Batch si aún no tiene una.</span><span class="sxs-lookup"><span data-stu-id="cebd5-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="cebd5-110">Vea [crear una cuenta de lote con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para una secuencia de comandos de ejemplo que crea una cuenta.</span><span class="sxs-lookup"><span data-stu-id="cebd5-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="cebd5-111">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="cebd5-111">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a><span data-ttu-id="cebd5-112">Aplicación de limpieza</span><span class="sxs-lookup"><span data-stu-id="cebd5-112">Clean up application</span></span>

<span data-ttu-id="cebd5-113">Después de ejecutar Hola por encima de la secuencia de comandos de ejemplo, ejecutar Hola después comandos tooremove la aplicación y todos sus paquetes de aplicación cargada.</span><span class="sxs-lookup"><span data-stu-id="cebd5-113">After you run hello above sample script, run hello following commands tooremove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="cebd5-114">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="cebd5-114">Script explanation</span></span>

<span data-ttu-id="cebd5-115">Este script utiliza Hola después comandos toocreate una aplicación y carga un paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cebd5-115">This script uses hello following commands toocreate an application and upload an application package.</span></span>
<span data-ttu-id="cebd5-116">Cada comando de la tabla de hello vincula documentación específica del toocommand.</span><span class="sxs-lookup"><span data-stu-id="cebd5-116">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="cebd5-117">Comando</span><span class="sxs-lookup"><span data-stu-id="cebd5-117">Command</span></span> | <span data-ttu-id="cebd5-118">Notas</span><span class="sxs-lookup"><span data-stu-id="cebd5-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cebd5-119">az batch application create</span><span class="sxs-lookup"><span data-stu-id="cebd5-119">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="cebd5-120">Crea una aplicación.</span><span class="sxs-lookup"><span data-stu-id="cebd5-120">Creates an application.</span></span>  |
| [<span data-ttu-id="cebd5-121">az batch application set</span><span class="sxs-lookup"><span data-stu-id="cebd5-121">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="cebd5-122">Actualiza las propiedades de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="cebd5-122">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="cebd5-123">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="cebd5-123">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="cebd5-124">Agrega un toohello de paquete de aplicación especificado aplicación.</span><span class="sxs-lookup"><span data-stu-id="cebd5-124">Adds an application package toohello specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="cebd5-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cebd5-125">Next steps</span></span>

<span data-ttu-id="cebd5-126">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cebd5-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cebd5-127">Encontrará más ejemplos de secuencias de comandos de CLI de lote en hello [documentación de CLI de lote de Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cebd5-127">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
