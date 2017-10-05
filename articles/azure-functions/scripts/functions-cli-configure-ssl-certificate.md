---
title: "Ejemplo de script de la CLI de Azure: enlace de un certificado SSL personalizado a una aplicación de función | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: enlace de un certificado SSL personalizado a una aplicación de función en Azure"
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
ms.openlocfilehash: ddabb701d7d5615232d1f6163aa6fb166efe5cb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a><span data-ttu-id="f3c38-103">Enlace de un certificado SSL personalizado a una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="f3c38-103">Bind a custom SSL certificate to a function app</span></span>

<span data-ttu-id="f3c38-104">Este script de ejemplo crea una aplicación de función en App Service con sus recursos relacionados y, luego, enlaza el certificado SSL de un nombre de dominio personalizado a ella.</span><span class="sxs-lookup"><span data-stu-id="f3c38-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="f3c38-105">Para este ejemplo, se necesita:</span><span class="sxs-lookup"><span data-stu-id="f3c38-105">For this sample, you need:</span></span>

* <span data-ttu-id="f3c38-106">Acceso a la página de configuración DNS de su registrador de dominios.</span><span class="sxs-lookup"><span data-stu-id="f3c38-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="f3c38-107">Un archivo PFX válido y su contraseña para el certificado SSL que desea cargar y enlazar.</span><span class="sxs-lookup"><span data-stu-id="f3c38-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

<span data-ttu-id="f3c38-108">Para enlazar un certificado SSL, la aplicación de función se debe crear en un plan de App Service y no en un plan de consumo.</span><span class="sxs-lookup"><span data-stu-id="f3c38-108">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f3c38-109">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f3c38-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f3c38-110">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="f3c38-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="f3c38-111">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f3c38-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f3c38-112">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f3c38-112">Sample script</span></span>

<span data-ttu-id="f3c38-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Enlace de un certificado SSL personalizado a una aplicación web")]</span><span class="sxs-lookup"><span data-stu-id="f3c38-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f3c38-114">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f3c38-114">Script explanation</span></span>

<span data-ttu-id="f3c38-115">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="f3c38-115">This script uses the following commands.</span></span> <span data-ttu-id="f3c38-116">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="f3c38-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f3c38-117">Comando</span><span class="sxs-lookup"><span data-stu-id="f3c38-117">Command</span></span> | <span data-ttu-id="f3c38-118">Notas</span><span class="sxs-lookup"><span data-stu-id="f3c38-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f3c38-119">az group create</span><span class="sxs-lookup"><span data-stu-id="f3c38-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f3c38-120">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="f3c38-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f3c38-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="f3c38-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f3c38-122">Crea un plan de App Service necesario para enlazar certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="f3c38-122">Creates an App Service plan required to bind SSL certificates.</span></span> |
| [<span data-ttu-id="f3c38-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="f3c38-123">az functionapp create</span></span>]() | <span data-ttu-id="f3c38-124">Crea una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="f3c38-124">Creates a function app.</span></span> |
| [<span data-ttu-id="f3c38-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="f3c38-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="f3c38-126">Asigna un dominio personalizado a la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="f3c38-126">Maps a custom domain to the function app.</span></span> |
| [<span data-ttu-id="f3c38-127">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="f3c38-127">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="f3c38-128">Carga un certificado SSL a una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="f3c38-128">Uploads an SSL certificate to a function app.</span></span> |
| [<span data-ttu-id="f3c38-129">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="f3c38-129">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="f3c38-130">Enlaza un certificado SSL cargado a una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="f3c38-130">Binds an uploaded SSL certificate to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f3c38-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3c38-131">Next steps</span></span>

<span data-ttu-id="f3c38-132">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f3c38-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f3c38-133">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service]().</span><span class="sxs-lookup"><span data-stu-id="f3c38-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation]().</span></span>
