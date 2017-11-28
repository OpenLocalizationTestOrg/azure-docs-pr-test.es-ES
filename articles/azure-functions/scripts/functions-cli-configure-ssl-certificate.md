---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure enlazar una aplicación de la función de tooa de certificado SSL personalizada | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos CLI Azure - enlace una aplicación de función personalizada de tooa certificados SSL en Azure"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a><span data-ttu-id="8aee1-103">Enlazar una aplicación de la función de tooa de certificado SSL personalizada</span><span class="sxs-lookup"><span data-stu-id="8aee1-103">Bind a custom SSL certificate tooa function app</span></span>

<span data-ttu-id="8aee1-104">Este script de ejemplo crea una aplicación de la función de servicio de aplicaciones con sus recursos relacionados, a continuación, enlaza el certificado SSL de Hola de un tooit de nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="8aee1-104">This sample script creates a function app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="8aee1-105">Para este ejemplo, se necesita:</span><span class="sxs-lookup"><span data-stu-id="8aee1-105">For this sample, you need:</span></span>

* <span data-ttu-id="8aee1-106">Obtener acceso a la página de configuración de DNS del registrador de dominios tooyour.</span><span class="sxs-lookup"><span data-stu-id="8aee1-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="8aee1-107">Válido. Archivo PFX y su contraseña para hello SSL certificado que desee tooupload y enlazar.</span><span class="sxs-lookup"><span data-stu-id="8aee1-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

<span data-ttu-id="8aee1-108">toobind un certificado SSL, la aplicación de la función debe crearse en un plan de servicio de aplicaciones y no en un plan de consumo.</span><span class="sxs-lookup"><span data-stu-id="8aee1-108">toobind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8aee1-109">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="8aee1-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8aee1-110">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8aee1-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8aee1-111">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8aee1-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8aee1-112">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8aee1-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8aee1-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="8aee1-113">Script explanation</span></span>

<span data-ttu-id="8aee1-114">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="8aee1-114">This script uses hello following commands.</span></span> <span data-ttu-id="8aee1-115">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="8aee1-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8aee1-116">Comando</span><span class="sxs-lookup"><span data-stu-id="8aee1-116">Command</span></span> | <span data-ttu-id="8aee1-117">Notas</span><span class="sxs-lookup"><span data-stu-id="8aee1-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8aee1-118">az group create</span><span class="sxs-lookup"><span data-stu-id="8aee1-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8aee1-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="8aee1-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8aee1-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="8aee1-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8aee1-121">Crea un toobind requerido un plan de servicio de aplicaciones certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="8aee1-121">Creates an App Service plan required toobind SSL certificates.</span></span> |
| [<span data-ttu-id="8aee1-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="8aee1-122">az functionapp create</span></span>]() | <span data-ttu-id="8aee1-123">Crea una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="8aee1-123">Creates a function app.</span></span> |
| [<span data-ttu-id="8aee1-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="8aee1-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="8aee1-125">Asigna una aplicación de función de toohello de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="8aee1-125">Maps a custom domain toohello function app.</span></span> |
| [<span data-ttu-id="8aee1-126">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="8aee1-126">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="8aee1-127">Carga una aplicación de función de tooa de certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="8aee1-127">Uploads an SSL certificate tooa function app.</span></span> |
| [<span data-ttu-id="8aee1-128">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="8aee1-128">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="8aee1-129">Enlaza una aplicación de la función de tooa de certificado SSL cargada.</span><span class="sxs-lookup"><span data-stu-id="8aee1-129">Binds an uploaded SSL certificate tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8aee1-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8aee1-130">Next steps</span></span>

<span data-ttu-id="8aee1-131">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8aee1-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8aee1-132">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure]().</span><span class="sxs-lookup"><span data-stu-id="8aee1-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation]().</span></span>
