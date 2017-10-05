---
title: "Ejemplo de script de la CLI de Azure: adición de una aplicación a Batch | Microsoft Docs"
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
ms.openlocfilehash: 5d057eaf32867aedc95d58c5185e2be1f9385ec0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a><span data-ttu-id="d07a5-103">Adición de aplicaciones a Azure Batch con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d07a5-103">Adding applications to Azure Batch with Azure CLI</span></span>

<span data-ttu-id="d07a5-104">Este script demuestra cómo configurar una aplicación para usarla con un grupo o tarea de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d07a5-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="d07a5-105">Para configurar una aplicación, cree un archivo .zip que incluya el ejecutable y cualquier dependencia.</span><span class="sxs-lookup"><span data-stu-id="d07a5-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="d07a5-106">En este ejemplo, el archivo zip con el ejecutable se llama "my-application-exe.zip".</span><span class="sxs-lookup"><span data-stu-id="d07a5-106">In this example the executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d07a5-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d07a5-107">Prerequisites</span></span>

- <span data-ttu-id="d07a5-108">Instale la CLI de Azure con las instrucciones que se encuentran en la [guía de instalación de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli) si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="d07a5-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="d07a5-109">Cree una cuenta de Batch si aún no tiene una.</span><span class="sxs-lookup"><span data-stu-id="d07a5-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="d07a5-110">Consulte [Creación de una cuenta de Batch con la CLI de Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para ver un script de ejemplo que crea una cuenta.</span><span class="sxs-lookup"><span data-stu-id="d07a5-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d07a5-111">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d07a5-111">Sample script</span></span>

<span data-ttu-id="d07a5-112">[!code-azurecli[principal](../../../cli_scripts/batch/add-application/add-application.sh "Agregar aplicación")]</span><span class="sxs-lookup"><span data-stu-id="d07a5-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]</span></span>

## <a name="clean-up-application"></a><span data-ttu-id="d07a5-113">Aplicación de limpieza</span><span class="sxs-lookup"><span data-stu-id="d07a5-113">Clean up application</span></span>

<span data-ttu-id="d07a5-114">Después de ejecutar el script de muestra anterior, ejecute los comandos siguientes para eliminar la aplicación y todos los paquetes de aplicación cargados.</span><span class="sxs-lookup"><span data-stu-id="d07a5-114">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d07a5-115">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="d07a5-115">Script explanation</span></span>

<span data-ttu-id="d07a5-116">Este script usa los comandos siguientes para crear una aplicación y cargar el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d07a5-116">This script uses the following commands to create an application and upload an application package.</span></span>
<span data-ttu-id="d07a5-117">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="d07a5-117">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d07a5-118">Comando</span><span class="sxs-lookup"><span data-stu-id="d07a5-118">Command</span></span> | <span data-ttu-id="d07a5-119">Notas</span><span class="sxs-lookup"><span data-stu-id="d07a5-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d07a5-120">az batch application create</span><span class="sxs-lookup"><span data-stu-id="d07a5-120">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="d07a5-121">Crea una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d07a5-121">Creates an application.</span></span>  |
| [<span data-ttu-id="d07a5-122">az batch application set</span><span class="sxs-lookup"><span data-stu-id="d07a5-122">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="d07a5-123">Actualiza las propiedades de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d07a5-123">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="d07a5-124">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="d07a5-124">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="d07a5-125">Agrega un paquete de aplicación a la aplicación especificada.</span><span class="sxs-lookup"><span data-stu-id="d07a5-125">Adds an application package to the specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="d07a5-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d07a5-126">Next steps</span></span>

<span data-ttu-id="d07a5-127">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d07a5-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d07a5-128">Puede encontrar ejemplos de script adicionales de la CLI de Batch en la [documentación de la CLI de Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d07a5-128">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
