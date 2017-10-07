---
title: aaaAzure contenedor del registro webhooks | Documentos de Microsoft
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
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="9ac4f-104">Uso de webhooks de Azure Container Registry: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9ac4f-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="9ac4f-105">Un registro de contenedor de Azure almacena y administra imágenes de contenedor de Docker privadas, manera toohello similar Docker Hub almacena imágenes públicas de Docker.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-105">An Azure container registry stores and manages private Docker container images, similar toohello way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="9ac4f-106">Use webhooks tootrigger eventos cuando determinadas acciones tienen lugar en uno de los repositorios de registro.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-106">You use webhooks tootrigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="9ac4f-107">Webhooks puede responder tooevents en nivel de registro de Hola o se pueden alcanzar hacia abajo de la etiqueta del repositorio específico de tooa.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-107">Webhooks can respond tooevents at hello registry level or they can be scoped down tooa specific repository tag.</span></span> 

<span data-ttu-id="9ac4f-108">Para obtener más general y conceptos, vea hello [Introducción](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="9ac4f-108">For more background and concepts, see hello [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ac4f-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9ac4f-109">Prerequisites</span></span> 

- <span data-ttu-id="9ac4f-110">Registro administrado por contenedores de Azure: cree un registro de contenedor administrado en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="9ac4f-111">Por ejemplo, usar hello portal de Azure u Hola 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-111">For example, use hello Azure portal or hello Azure CLI 2.0.</span></span> 
- <span data-ttu-id="9ac4f-112">Docker CLI - tooset el equipo local como un host y el acceso Hola CLI de Docker comandos de Docker, instalar el motor de Docker.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-112">Docker CLI - tooset up your local computer as a Docker host and access hello Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="9ac4f-113">Creación del webhook con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9ac4f-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="9ac4f-114">Inicie sesión en toohello portal de Azure y navegue registro toohello en el que desea toocreate webhook.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-114">Log in toohello Azure portal and navigate toohello registry in which you want toocreate webhooks.</span></span> 

2. <span data-ttu-id="9ac4f-115">En la hoja de contenedor de hello, seleccione la pestaña de "Webhooks" de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-115">In hello container blade, select hello "Webhooks" tab.</span></span> 

3. <span data-ttu-id="9ac4f-116">Seleccione "Agregar" de la barra de herramientas de hello webhook hoja.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-116">Select "Add" from hello webhook blade toolbar.</span></span> 

4. <span data-ttu-id="9ac4f-117">Hola completa *Webhook crear* formulario con hello siguiente información:</span><span class="sxs-lookup"><span data-stu-id="9ac4f-117">Complete hello *Create Webhook* form with hello following information:</span></span>

| <span data-ttu-id="9ac4f-118">Valor</span><span class="sxs-lookup"><span data-stu-id="9ac4f-118">Value</span></span> | <span data-ttu-id="9ac4f-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="9ac4f-119">Description</span></span> |
|---|---|
| <span data-ttu-id="9ac4f-120">Nombre</span><span class="sxs-lookup"><span data-stu-id="9ac4f-120">Name</span></span> | <span data-ttu-id="9ac4f-121">nombre de Hola que desea toogive toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-121">hello name you want toogive toohello webhook.</span></span> <span data-ttu-id="9ac4f-122">Solo puede contener letras minúsculas y números, y tener entre 5 y 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="9ac4f-123">URI de servicio</span><span class="sxs-lookup"><span data-stu-id="9ac4f-123">Service URI</span></span> | <span data-ttu-id="9ac4f-124">Hola URI donde hello webhook debe enviar notificaciones de entrada.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-124">hello URI where hello webhook should send POST notifications.</span></span> |
| <span data-ttu-id="9ac4f-125">Encabezados personalizados</span><span class="sxs-lookup"><span data-stu-id="9ac4f-125">Custom headers</span></span> | <span data-ttu-id="9ac4f-126">Encabezados que desee toopass junto con la solicitud POST Hola.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-126">Headers you want toopass along with hello POST request.</span></span> <span data-ttu-id="9ac4f-127">Deben tener el formato "clave: valor".</span><span class="sxs-lookup"><span data-stu-id="9ac4f-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="9ac4f-128">Acciones de desencadenador</span><span class="sxs-lookup"><span data-stu-id="9ac4f-128">Trigger actions</span></span> | <span data-ttu-id="9ac4f-129">Acciones que desencadenan hello webhook.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-129">Actions that trigger hello webhook.</span></span> <span data-ttu-id="9ac4f-130">Actualmente webhooks puede activarse mediante inserción o eliminar acciones tooan imagen.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-130">Currently webhooks can be triggered by push and/or delete actions tooan image.</span></span> |
| <span data-ttu-id="9ac4f-131">Estado</span><span class="sxs-lookup"><span data-stu-id="9ac4f-131">Status</span></span> | <span data-ttu-id="9ac4f-132">estado de Hola Hola webhook después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-132">hello status for hello webhook after it's created.</span></span> <span data-ttu-id="9ac4f-133">Esto está habilitada de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-133">It's enabled by default.</span></span> |
| <span data-ttu-id="9ac4f-134">Scope</span><span class="sxs-lookup"><span data-stu-id="9ac4f-134">Scope</span></span> | <span data-ttu-id="9ac4f-135">ámbito de Hello en qué funciona de webhook Hola.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-135">hello scope at which hello webhook works.</span></span> <span data-ttu-id="9ac4f-136">De forma predeterminada el ámbito de hello es para todos los eventos en el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-136">By default hello scope is for all events in hello registry.</span></span> <span data-ttu-id="9ac4f-137">Se puede especificar para un repositorio o una etiqueta con formato de Hola "repositorio: etiqueta".</span><span class="sxs-lookup"><span data-stu-id="9ac4f-137">It can be specified for a repository or a tag by using hello format "repository: tag".</span></span> |

<span data-ttu-id="9ac4f-138">Formulario de webhook de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9ac4f-138">Example webhook form:</span></span>

![Interfaz de usuario de DCOS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="9ac4f-140">Crear el webhook con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9ac4f-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="9ac4f-141">toocreate un webhook utilizando Hola CLI de Azure, use hello [crear az acr webhook](/cli/azure/acr/webhook#create) comando.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-141">toocreate a webhook using hello Azure CLI, use hello [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="9ac4f-142">Webhook de prueba</span><span class="sxs-lookup"><span data-stu-id="9ac4f-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="9ac4f-143">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9ac4f-143">Azure portal</span></span>

<span data-ttu-id="9ac4f-144">Webhook de hello toousing anterior en el contenedor de inserción de la imagen y eliminar acciones, puede probar con hello **Ping** botón.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-144">Prior toousing hello webhook on container image push and delete actions, it can be tested using hello **Ping** button.</span></span> <span data-ttu-id="9ac4f-145">Cuando se utiliza, Hola Ping envía que una toohello de solicitud de post genérico especifica registros y extremo Hola respuesta.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-145">When used, hello Ping sends a generic post request toohello specified endpoint and logs hello response.</span></span> <span data-ttu-id="9ac4f-146">Esto resulta útil tooverify que Hola webhook se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-146">This is helpful tooverify that hello webhook has been set up correctly.</span></span>

1. <span data-ttu-id="9ac4f-147">Seleccione webhook Hola desea tootest.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-147">Select hello webhook you want tootest.</span></span> 
2. <span data-ttu-id="9ac4f-148">En la barra de herramientas superior hello, seleccione acción de hello "hace Ping".</span><span class="sxs-lookup"><span data-stu-id="9ac4f-148">In hello top toolbar, select hello "Ping" action.</span></span> 
3. <span data-ttu-id="9ac4f-149">Solicitud de comprobación de Hola y respuesta.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-149">Check hello request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="9ac4f-150">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9ac4f-150">Azure CLI</span></span>

<span data-ttu-id="9ac4f-151">tootest un webhook de ACR con hello CLI de Azure, use hello [ping de webhook de acr az](/cli/azure/acr/webhook#ping) comando.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-151">tootest an ACR webhook with hello Azure CLI, use hello [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="9ac4f-152">resultados de hello toosee, usar hello [az acr webhook eventos de lista](/cli/azure/acr/webhook#list-events) comando.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-152">toosee hello results, use hello [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="9ac4f-153">Eliminación del webhook</span><span class="sxs-lookup"><span data-stu-id="9ac4f-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="9ac4f-154">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9ac4f-154">Azure portal</span></span>

<span data-ttu-id="9ac4f-155">Cada webhook puede eliminarse mediante la selección de webhook de hello y, a continuación, el botón de eliminación de hello en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-155">Each webhook can be deleted by selecting hello webhook and then hello delete button on hello Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="9ac4f-156">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9ac4f-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```