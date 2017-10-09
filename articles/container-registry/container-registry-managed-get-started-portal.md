---
title: registro Docker privada aaaCreate - portal de Azure | Documentos de Microsoft
description: Empezar a crear y administrar registros de contenedor de Docker privados con hello portal de Azure
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a>Crear un registro de contenedor administrado mediante Hola portal de Azure

Azure Container Registry es un servicio de registro de contenedores de Docker administrado usado para almacenar imágenes de contenedor de Docker privadas. Esta guía se detalla la creación de una instancia de registro de contenedor de Azure administrados mediante Hola portal de Azure.

Azure Container Registry está en versión preliminar y no está disponible en todas las regiones.

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Inicie sesión en toohello portal de Azure en http://portal.azure.com.

## <a name="create-a-container-registry"></a>Creación de un registro de contenedor

1. Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.

2. Busque en marketplace Hola para **registro de contenedor de Azure** y selecciónelo.

3. Haga clic en **crear** que abrirá la hoja de creación de hello ACR.

    ![Configuración de Container Registry](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. Hola **registro de contenedor de Azure** hoja, escriba Hola siguiente información. Cuando haya terminado, haga clic en **Crear**.

    a. **Nombre del registro**: un nombre de dominio de nivel superior único global para el registro específico. En este ejemplo, es el nombre del registro de hello *myAzureContainerRegistry1*, pero sustituir un nombre único de su elección. Hola nombre puede contener sólo letras y números.

    b. **Grupo de recursos**: seleccione una existente [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) o nombre de tipo hello para uno nuevo.

    c. **Ubicación**: seleccione la ubicación de centro de datos Azure donde es el servicio de hello [disponibles](https://azure.microsoft.com/regions/services/), como **Ee.uu. Central sur**.

    d. **El usuario administrador**: si lo desea, habilitar un registro de hello de tooaccess de usuario de administrador. Puede cambiar esta configuración después de crear el registro de hello.

    e. **Registro de uso administrado**: seleccione la opción Sí toohave ACR automáticamente administrar el almacenamiento de registro de hello, use webhooks y use autenticación de AAD.

    f. **Plan de tarifa**: seleccione un plan de tarifa, consulte precios de ACR para más información.

## <a name="log-in-tooacr-instance"></a>Inicie sesión en la instancia de tooACR

Antes de insertar y extraer imágenes de contenedor, primero debe iniciar sesión en la instancia ACR toohello. 

toodo por lo tanto, utilice Hola 2.0 de CLI de Azure. En primer lugar, si es necesario, inicie sesión en Azure con hello [inicio de sesión de az](/cli/azure/#login) comando. 

```azurecli
az login
```

A continuación, usar hello [inicio de sesión de acr az](/cli/azure/acr#login) comando toolog en toohello del registro de contenedor de Azure.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a>Uso de Azure Container Registry

### <a name="list-container-images"></a>Lista de imágenes de contenedor

Hola de uso `az acr` tooquery imágenes de Hola y etiquetas en un repositorio de los comandos de CLI.

> [!NOTE]
> Actualmente, el registro de contenedor no admite hello `docker search` tooquery de comando para imágenes y etiquetas.

### <a name="list-repositories"></a>Lista de repositorios

Hello en el ejemplo siguiente se enumera los repositorios de hello en un registro, en formato JSON (JavaScript Object Notation):

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Lista de etiquetas

Hello en el ejemplo siguiente se muestra etiquetas de hello en hello **ejemplos/nginx** repositorio, en formato JSON:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha creado una instancia administrada de registro de contenedor de Azure con hello portal de Azure.

> [!div class="nextstepaction"]
> [Insertar la primera imagen con hello CLI de Docker](container-registry-get-started-docker-cli.md)
