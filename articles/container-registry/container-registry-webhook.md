---
title: Webhook de Azure Container Registry | Microsoft Docs
description: Webhook de Azure Container Registry
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: Docker, Contenedores, ACR
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: d0190f5725671c320d92b897f0dcef7a526a86e3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="40ef8-104">Uso de webhooks de Azure Container Registry: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="40ef8-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="40ef8-105">Un registro de contenedor de Azure almacena y administra imágenes privadas de contenedor de Docker, de una forma similar a la que Docker Hub almacena imágenes públicas.</span><span class="sxs-lookup"><span data-stu-id="40ef8-105">An Azure container registry stores and manages private Docker container images, similar to the way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="40ef8-106">Use webhooks para desencadenar eventos cuando determinadas acciones tienen lugar en uno de los repositorios de registro.</span><span class="sxs-lookup"><span data-stu-id="40ef8-106">You use webhooks to trigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="40ef8-107">Los webhooks pueden responder a eventos en el nivel de registro o pueden limitarse a una etiqueta de repositorio específica.</span><span class="sxs-lookup"><span data-stu-id="40ef8-107">Webhooks can respond to events at the registry level or they can be scoped down to a specific repository tag.</span></span> 

<span data-ttu-id="40ef8-108">Para más información sobre el entorno y los conceptos, consulte la [introducción](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="40ef8-108">For more background and concepts, see the [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40ef8-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="40ef8-109">Prerequisites</span></span> 

- <span data-ttu-id="40ef8-110">Registro administrado por contenedores de Azure: cree un registro de contenedor administrado en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="40ef8-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="40ef8-111">Por ejemplo, use Azure Portal o la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="40ef8-111">For example, use the Azure portal or the Azure CLI 2.0.</span></span> 
- <span data-ttu-id="40ef8-112">CLI de docker: para configurar el equipo local como un host de Docker y tener acceso a los comandos de la CLI de Docker, instale Docker Engine.</span><span class="sxs-lookup"><span data-stu-id="40ef8-112">Docker CLI - To set up your local computer as a Docker host and access the Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="40ef8-113">Creación del webhook con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="40ef8-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="40ef8-114">Inicie sesión en Azure Portal y navegue hasta el registro en el que desea crear el webhook.</span><span class="sxs-lookup"><span data-stu-id="40ef8-114">Log in to the Azure portal and navigate to the registry in which you want to create webhooks.</span></span> 

2. <span data-ttu-id="40ef8-115">En la hoja de contenedor, seleccione la pestaña "Webhook".</span><span class="sxs-lookup"><span data-stu-id="40ef8-115">In the container blade, select the "Webhooks" tab.</span></span> 

3. <span data-ttu-id="40ef8-116">Seleccione "Agregar" en la barra de herramientas de la hoja Webhook.</span><span class="sxs-lookup"><span data-stu-id="40ef8-116">Select "Add" from the webhook blade toolbar.</span></span> 

4. <span data-ttu-id="40ef8-117">Complete el formulario *Crear webhook* con la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="40ef8-117">Complete the *Create Webhook* form with the following information:</span></span>

| <span data-ttu-id="40ef8-118">Valor</span><span class="sxs-lookup"><span data-stu-id="40ef8-118">Value</span></span> | <span data-ttu-id="40ef8-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="40ef8-119">Description</span></span> |
|---|---|
| <span data-ttu-id="40ef8-120">Nombre</span><span class="sxs-lookup"><span data-stu-id="40ef8-120">Name</span></span> | <span data-ttu-id="40ef8-121">El nombre que desea dar al webhook.</span><span class="sxs-lookup"><span data-stu-id="40ef8-121">The name you want to give to the webhook.</span></span> <span data-ttu-id="40ef8-122">Solo puede contener letras minúsculas y números, y tener entre 5 y 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="40ef8-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="40ef8-123">URI de servicio</span><span class="sxs-lookup"><span data-stu-id="40ef8-123">Service URI</span></span> | <span data-ttu-id="40ef8-124">El identificador URI donde el webhook debe enviar notificaciones POST.</span><span class="sxs-lookup"><span data-stu-id="40ef8-124">The URI where the webhook should send POST notifications.</span></span> |
| <span data-ttu-id="40ef8-125">Encabezados personalizados</span><span class="sxs-lookup"><span data-stu-id="40ef8-125">Custom headers</span></span> | <span data-ttu-id="40ef8-126">Los encabezados que van a pasar junto con la solicitud POST.</span><span class="sxs-lookup"><span data-stu-id="40ef8-126">Headers you want to pass along with the POST request.</span></span> <span data-ttu-id="40ef8-127">Deben tener el formato "clave: valor".</span><span class="sxs-lookup"><span data-stu-id="40ef8-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="40ef8-128">Acciones de desencadenador</span><span class="sxs-lookup"><span data-stu-id="40ef8-128">Trigger actions</span></span> | <span data-ttu-id="40ef8-129">Acciones que desencadenan el webhook.</span><span class="sxs-lookup"><span data-stu-id="40ef8-129">Actions that trigger the webhook.</span></span> <span data-ttu-id="40ef8-130">Actualmente los webhooks pueden activarse mediante acciones de inserción o eliminación en una imagen.</span><span class="sxs-lookup"><span data-stu-id="40ef8-130">Currently webhooks can be triggered by push and/or delete actions to an image.</span></span> |
| <span data-ttu-id="40ef8-131">Estado</span><span class="sxs-lookup"><span data-stu-id="40ef8-131">Status</span></span> | <span data-ttu-id="40ef8-132">El estado del webhook después de su creación.</span><span class="sxs-lookup"><span data-stu-id="40ef8-132">The status for the webhook after it's created.</span></span> <span data-ttu-id="40ef8-133">Esto está habilitada de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="40ef8-133">It's enabled by default.</span></span> |
| <span data-ttu-id="40ef8-134">Scope</span><span class="sxs-lookup"><span data-stu-id="40ef8-134">Scope</span></span> | <span data-ttu-id="40ef8-135">El ámbito en el que trabaja el webhook.</span><span class="sxs-lookup"><span data-stu-id="40ef8-135">The scope at which the webhook works.</span></span> <span data-ttu-id="40ef8-136">De forma predeterminada el ámbito sirve para todos los eventos del registro.</span><span class="sxs-lookup"><span data-stu-id="40ef8-136">By default the scope is for all events in the registry.</span></span> <span data-ttu-id="40ef8-137">Se puede especificar para un repositorio o etiqueta con el formato "repositorio: etiqueta".</span><span class="sxs-lookup"><span data-stu-id="40ef8-137">It can be specified for a repository or a tag by using the format "repository: tag".</span></span> |

<span data-ttu-id="40ef8-138">Formulario de webhook de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="40ef8-138">Example webhook form:</span></span>

![Interfaz de usuario de DCOS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="40ef8-140">Crear el webhook con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="40ef8-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="40ef8-141">Para crear un webhook mediante la CLI de Azure, use el comando [az acr webhook create](/cli/azure/acr/webhook#create).</span><span class="sxs-lookup"><span data-stu-id="40ef8-141">To create a webhook using the Azure CLI, use the [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="40ef8-142">Webhook de prueba</span><span class="sxs-lookup"><span data-stu-id="40ef8-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="40ef8-143">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="40ef8-143">Azure portal</span></span>

<span data-ttu-id="40ef8-144">Antes de usar el webhook en acciones de inserción y eliminación de imágenes de contenedor, se puede probar mediante el botón **Ping**.</span><span class="sxs-lookup"><span data-stu-id="40ef8-144">Prior to using the webhook on container image push and delete actions, it can be tested using the **Ping** button.</span></span> <span data-ttu-id="40ef8-145">Cuando se utiliza, el comando Ping envía una solicitud post genérica al punto de conexión especificado y registra la respuesta.</span><span class="sxs-lookup"><span data-stu-id="40ef8-145">When used, the Ping sends a generic post request to the specified endpoint and logs the response.</span></span> <span data-ttu-id="40ef8-146">Esto resulta útil para comprobar que el webhook se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="40ef8-146">This is helpful to verify that the webhook has been set up correctly.</span></span>

1. <span data-ttu-id="40ef8-147">Seleccione el webhook que desea probar.</span><span class="sxs-lookup"><span data-stu-id="40ef8-147">Select the webhook you want to test.</span></span> 
2. <span data-ttu-id="40ef8-148">En la barra de herramientas superior, seleccione la acción "Ping".</span><span class="sxs-lookup"><span data-stu-id="40ef8-148">In the top toolbar, select the "Ping" action.</span></span> 
3. <span data-ttu-id="40ef8-149">Compruebe la solicitud y respuesta.</span><span class="sxs-lookup"><span data-stu-id="40ef8-149">Check the request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="40ef8-150">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="40ef8-150">Azure CLI</span></span>

<span data-ttu-id="40ef8-151">Para probar un webhook de ACR con la CLI de Azure, use el comando [az acr webhook ping](/cli/azure/acr/webhook#ping).</span><span class="sxs-lookup"><span data-stu-id="40ef8-151">To test an ACR webhook with the Azure CLI, use the [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="40ef8-152">Para ver los resultados, use el comando [az acr webhook list-events](/cli/azure/acr/webhook#list-events).</span><span class="sxs-lookup"><span data-stu-id="40ef8-152">To see the results, use the [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="40ef8-153">Eliminación del webhook</span><span class="sxs-lookup"><span data-stu-id="40ef8-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="40ef8-154">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="40ef8-154">Azure portal</span></span>

<span data-ttu-id="40ef8-155">Se pueden eliminar los webhooks seleccionando un webhook y, después, el botón Eliminar en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="40ef8-155">Each webhook can be deleted by selecting the webhook and then the delete button on the Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="40ef8-156">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="40ef8-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```