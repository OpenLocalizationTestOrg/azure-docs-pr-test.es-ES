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
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>Uso de webhooks de Azure Container Registry: Azure Portal

Un registro de contenedor de Azure almacena y administra imágenes de contenedor de Docker privadas, manera toohello similar Docker Hub almacena imágenes públicas de Docker. Use webhooks tootrigger eventos cuando determinadas acciones tienen lugar en uno de los repositorios de registro. Webhooks puede responder tooevents en nivel de registro de Hola o se pueden alcanzar hacia abajo de la etiqueta del repositorio específico de tooa. 

Para obtener más general y conceptos, vea hello [Introducción](./container-registry-intro.md).

## <a name="prerequisites"></a>Requisitos previos 

- Registro administrado por contenedores de Azure: cree un registro de contenedor administrado en la suscripción de Azure. Por ejemplo, usar hello portal de Azure u Hola 2.0 de CLI de Azure. 
- Docker CLI - tooset el equipo local como un host y el acceso Hola CLI de Docker comandos de Docker, instalar el motor de Docker. 

## <a name="create-webhook-azure-portal"></a>Creación del webhook con Azure Portal

1. Inicie sesión en toohello portal de Azure y navegue registro toohello en el que desea toocreate webhook. 

2. En la hoja de contenedor de hello, seleccione la pestaña de "Webhooks" de Hola. 

3. Seleccione "Agregar" de la barra de herramientas de hello webhook hoja. 

4. Hola completa *Webhook crear* formulario con hello siguiente información:

| Valor | Descripción |
|---|---|
| Nombre | nombre de Hola que desea toogive toohello webhook. Solo puede contener letras minúsculas y números, y tener entre 5 y 50 caracteres. |
| URI de servicio | Hola URI donde hello webhook debe enviar notificaciones de entrada. |
| Encabezados personalizados | Encabezados que desee toopass junto con la solicitud POST Hola. Deben tener el formato "clave: valor". |
| Acciones de desencadenador | Acciones que desencadenan hello webhook. Actualmente webhooks puede activarse mediante inserción o eliminar acciones tooan imagen. |
| Estado | estado de Hola Hola webhook después de crearlo. Esto está habilitada de manera predeterminada. |
| Scope | ámbito de Hello en qué funciona de webhook Hola. De forma predeterminada el ámbito de hello es para todos los eventos en el registro de hello. Se puede especificar para un repositorio o una etiqueta con formato de Hola "repositorio: etiqueta". |

Formulario de webhook de ejemplo:

![Interfaz de usuario de DCOS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>Crear el webhook con la CLI de Azure

toocreate un webhook utilizando Hola CLI de Azure, use hello [crear az acr webhook](/cli/azure/acr/webhook#create) comando.

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>Webhook de prueba

### <a name="azure-portal"></a>Azure Portal

Webhook de hello toousing anterior en el contenedor de inserción de la imagen y eliminar acciones, puede probar con hello **Ping** botón. Cuando se utiliza, Hola Ping envía que una toohello de solicitud de post genérico especifica registros y extremo Hola respuesta. Esto resulta útil tooverify que Hola webhook se ha configurado correctamente.

1. Seleccione webhook Hola desea tootest. 
2. En la barra de herramientas superior hello, seleccione acción de hello "hace Ping". 
3. Solicitud de comprobación de Hola y respuesta.

### <a name="azure-cli"></a>CLI de Azure

tootest un webhook de ACR con hello CLI de Azure, use hello [ping de webhook de acr az](/cli/azure/acr/webhook#ping) comando.

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

resultados de hello toosee, usar hello [az acr webhook eventos de lista](/cli/azure/acr/webhook#list-events) comando. 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>Eliminación del webhook

### <a name="azure-portal"></a>Azure Portal

Cada webhook puede eliminarse mediante la selección de webhook de hello y, a continuación, el botón de eliminación de hello en hello portal de Azure.

### <a name="azure-cli"></a>CLI de Azure

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```