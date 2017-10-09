---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure enlazar una aplicación de web de tooa de certificado SSL personalizada | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos CLI Azure - enlace una aplicación de web de tooa de certificado SSL personalizada"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2fec2db84a2007fa6b005776c84d4f8cba392b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="b5af0-103">Enlazar una aplicación de web de tooa de certificado SSL personalizada</span><span class="sxs-lookup"><span data-stu-id="b5af0-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="b5af0-104">Este script de ejemplo crea una aplicación web en el servicio de aplicaciones con sus recursos relacionados, a continuación, enlaza el certificado SSL de Hola de un tooit de nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="b5af0-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="b5af0-105">Para este ejemplo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b5af0-105">For this sample, you will need:</span></span>

* <span data-ttu-id="b5af0-106">Obtener acceso a la página de configuración de DNS del registrador de dominios tooyour.</span><span class="sxs-lookup"><span data-stu-id="b5af0-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="b5af0-107">Válido. Archivo PFX y su contraseña para hello SSL certificado que desee tooupload y enlazar.</span><span class="sxs-lookup"><span data-stu-id="b5af0-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b5af0-108">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="b5af0-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b5af0-109">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5af0-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b5af0-110">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b5af0-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="b5af0-111">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b5af0-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b5af0-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="b5af0-112">Script explanation</span></span>

<span data-ttu-id="b5af0-113">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="b5af0-113">This script uses hello following commands.</span></span> <span data-ttu-id="b5af0-114">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="b5af0-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b5af0-115">Comando</span><span class="sxs-lookup"><span data-stu-id="b5af0-115">Command</span></span> | <span data-ttu-id="b5af0-116">Notas</span><span class="sxs-lookup"><span data-stu-id="b5af0-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b5af0-117">az group create</span><span class="sxs-lookup"><span data-stu-id="b5af0-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b5af0-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="b5af0-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b5af0-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="b5af0-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="b5af0-120">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="b5af0-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="b5af0-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="b5af0-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="b5af0-122">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5af0-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="b5af0-123">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="b5af0-123">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="b5af0-124">Asigna una aplicación web de tooa de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="b5af0-124">Maps a custom domain tooa web app.</span></span> |
| [<span data-ttu-id="b5af0-125">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="b5af0-125">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="b5af0-126">Carga una aplicación web SSL certificado tooa.</span><span class="sxs-lookup"><span data-stu-id="b5af0-126">Uploads an SSL certificate tooa web app.</span></span> |
| [<span data-ttu-id="b5af0-127">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="b5af0-127">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="b5af0-128">Enlaza una aplicación de web de tooa de certificado SSL cargada.</span><span class="sxs-lookup"><span data-stu-id="b5af0-128">Binds an uploaded SSL certificate tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b5af0-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5af0-129">Next steps</span></span>

<span data-ttu-id="b5af0-130">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b5af0-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b5af0-131">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b5af0-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
