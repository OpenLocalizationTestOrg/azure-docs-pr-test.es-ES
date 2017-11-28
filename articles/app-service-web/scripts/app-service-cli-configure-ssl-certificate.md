---
title: "Ejemplo de script de la CLI de Azure: enlace de un certificado SSL personalizado a una aplicación web | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: enlace de un certificado SSL personalizado a una aplicación web"
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
ms.openlocfilehash: d4fab3fb2c297bf5f498b63bee46692febb9180b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="28141-103">Enlace de un certificado SSL personalizado a una aplicación web</span><span class="sxs-lookup"><span data-stu-id="28141-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="28141-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, luego, enlaza el certificado SSL de un nombre de dominio personalizado a ella.</span><span class="sxs-lookup"><span data-stu-id="28141-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="28141-105">Para este ejemplo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="28141-105">For this sample, you will need:</span></span>

* <span data-ttu-id="28141-106">Acceso a la página de configuración DNS de su registrador de dominios.</span><span class="sxs-lookup"><span data-stu-id="28141-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="28141-107">Un archivo PFX válido y su contraseña para el certificado SSL que desea cargar y enlazar.</span><span class="sxs-lookup"><span data-stu-id="28141-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="28141-108">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="28141-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="28141-109">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="28141-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="28141-110">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="28141-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="28141-111">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="28141-111">Sample script</span></span>

<span data-ttu-id="28141-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Enlace de un certificado SSL personalizado a una aplicación web")]</span><span class="sxs-lookup"><span data-stu-id="28141-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="28141-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="28141-113">Script explanation</span></span>

<span data-ttu-id="28141-114">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="28141-114">This script uses the following commands.</span></span> <span data-ttu-id="28141-115">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="28141-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="28141-116">Comando</span><span class="sxs-lookup"><span data-stu-id="28141-116">Command</span></span> | <span data-ttu-id="28141-117">Notas</span><span class="sxs-lookup"><span data-stu-id="28141-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="28141-118">az group create</span><span class="sxs-lookup"><span data-stu-id="28141-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="28141-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="28141-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="28141-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="28141-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="28141-121">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="28141-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="28141-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="28141-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="28141-123">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="28141-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="28141-124">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="28141-124">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="28141-125">Asigna un dominio personalizado a una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="28141-125">Maps a custom domain to a web app.</span></span> |
| [<span data-ttu-id="28141-126">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="28141-126">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="28141-127">Carga un certificado SSL a una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="28141-127">Uploads an SSL certificate to a web app.</span></span> |
| [<span data-ttu-id="28141-128">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="28141-128">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="28141-129">Enlaza un certificado SSL cargado a una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="28141-129">Binds an uploaded SSL certificate to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="28141-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="28141-130">Next steps</span></span>

<span data-ttu-id="28141-131">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="28141-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="28141-132">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="28141-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
