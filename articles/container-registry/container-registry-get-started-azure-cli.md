---
title: registro de contenedor de Docker privada de aaaCreate - CLI de Azure | Documentos de Microsoft
description: Empezar a crear y administrar registros de contenedor de Docker privados con hello 2.0 de CLI de Azure
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a>Crear un registro de contenedor de Docker privado mediante Hola 2.0 de CLI de Azure
Usar comandos en hello [CLI de Azure 2.0](https://github.com/Azure/azure-cli) toocreate un registro de contenedor y administrar su configuración desde un equipo Linux, Mac o Windows. También puede crear y administrar registros de contenedor con hello [portal de Azure](container-registry-get-started-portal.md) o mediante programación con registro de contenedor de hello [API de REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* En el fondo y conceptos, vea [Hola información general](container-registry-intro.md)
* Para obtener ayuda sobre los comandos de CLI de contenedor del registro (`az acr` comandos), pasar hello `-h` comando tooany de parámetro.


## <a name="prerequisites"></a>Requisitos previos
* **Azure 2.0 CLI**: tooinstall y empezar a trabajar con hello 2.0 de CLI, consulte hello [las instrucciones de instalación](/cli/azure/install-azure-cli). Inicie sesión en tooyour suscripción de Azure ejecutando `az login`. Para obtener más información, consulte [empezar a trabajar con hello CLI 2.0](/cli/azure/get-started-with-azure-cli).
* **Grupo de recursos**: cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) antes de crear un registro de contenedor o utilice un grupo de recursos ya existente. Asegúrese de que el grupo de recursos de hello está en una ubicación donde hello servicio de registro de contenedor es [disponibles](https://azure.microsoft.com/regions/services/). toocreate un grupo de recursos con Hola 2.0 de CLI, consulte [Hola referencia CLI 2.0](/cli/azure/group).
* **Cuenta de almacenamiento** (opcional): crear un estándar Azure [cuenta de almacenamiento](../storage/common/storage-introduction.md) tooback registro de contenedor de Hola Hola misma ubicación. Si no especifica una cuenta de almacenamiento al crear un registro con `az acr create`, comando hello crea uno automáticamente. toocreate cuenta de almacenamiento mediante Hola 2.0 de CLI, consulte [Hola referencia CLI 2.0](/cli/azure/storage/account). Premium Storage no se admite actualmente.
* **Entidad de servicio** (opcional): cuando se crea un registro con hello CLI, de forma predeterminada no está configurado para el acceso. Según sus necesidades, puede asignar un registro de tooa principal de servicio de Azure Active Directory existente (o crear y asignar una nueva), o habilitar la cuenta de usuario de administrador del registro de hello. Vea las secciones de hello más adelante en este artículo. Para obtener más información acerca del acceso del registro, consulte [autenticar con registro de contenedor de hello](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Creación de un registro de contenedor
Ejecute hello `az acr create` comando toocreate un registro de contenedor.

> [!TIP]
> Cuando cree un registro, especifique un nombre de dominio de nivel superior único global que contenga solo letras y números. nombre del registro de Hello en los ejemplos de hello `myRegistry1`, pero sustituir un nombre único de su elección.
>
>

Hola el siguiente comando utiliza Hola del registro de contenedor de parámetros mínimos toocreate `myRegistry1` en grupo de recursos de hello `myResourceGroup`y el uso de hello *básica* sku:

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* `--storage-account-name` es opcional. Si no se especifica, se crea una cuenta de almacenamiento con un nombre que consta del nombre del registro de hello y una marca de tiempo en hello especifica el grupo de recursos.

Cuando se crea el registro de hello, salida de hello es siguiente de toohello similar:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


Tenga en cuenta especialmente:

* `id`-Identificador de registro de hello en su suscripción, que es necesario si desea tooassign una entidad de servicio.
* `loginServer`-nombre completo de Hola que especifique demasiado[inicie sesión en el registro de toohello](container-registry-authentication.md). En este ejemplo, se denomina hello `myregistry1.exp.azurecr.io` (en minúsculas).

## <a name="assign-a-service-principal"></a>Asignación de una entidad de servicio
Usar comandos de CLI 2.0 tooassign un registro de tooa principal de servicio de Azure Active Directory. Hello entidad de servicio en estos ejemplos se asigna el rol de propietario de hello, pero puede asignar [otros roles](../active-directory/role-based-access-control-configure.md) si desea.

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a>Crear a una entidad de servicio y asignar del registro de acceso toohello
En el siguiente comando de hello, una nueva entidad de servicio se asigna identificador Propietario rol acceso toohello del registro se ha superado con hello `--scopes` parámetro. Especifique una contraseña segura con hello `--password` parámetro.

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>Asignación de una entidad de servicio existente
Si ya tiene una entidad de servicio y desea tooassign el registro de toohello de propietario rol acceso, que se ejecute un toohello similar de comando siguiente ejemplo. Pasar el identificador de la aplicación principal de servicio hello mediante hello `--assignee` parámetro:

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>Administración de las credenciales de administrador
Se crea automáticamente una cuenta de administrador para cada registro de contenedor, que estará deshabilitada de forma predeterminada. Hola siguientes ejemplos se muestra `az acr` toomanage credenciales de administrador de hello para el registro de contenedor de comandos de CLI.

### <a name="obtain-admin-user-credentials"></a>Obtención de las credenciales de administrador
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Habilitación del usuario de administrador para un registro existente
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Deshabilitación del usuario de administrador para un registro existente
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>Lista de las imágenes y etiquetas
Hola de uso `az acr` tooquery imágenes de Hola y etiquetas en un repositorio de los comandos de CLI.

> [!NOTE]
> Actualmente, el registro de contenedor no admite hello `docker search` tooquery de comando para imágenes y etiquetas.


### <a name="list-repositories"></a>Lista de repositorios
Hello en el ejemplo siguiente se enumera los repositorios de hello en un registro, en formato JSON (JavaScript Object Notation):

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>Lista de etiquetas
Hello en el ejemplo siguiente se muestra etiquetas de hello en hello **ejemplos/nginx** repositorio, en formato JSON:

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Pasos siguientes
* [Insertar la primera imagen con hello CLI de Docker](container-registry-get-started-docker-cli.md)
