---
title: aaaDeploy tooAzure instancias de contenedor de hello del registro de contenedor de Azure | Documentos de Azure
description: Implementar instancias de contenedor tooAzure de hello del registro de contenedor de Azure
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a>Implementar instancias de contenedor tooAzure de hello del registro de contenedor de Azure

Hola del registro de contenedor de Azure es un registro basado en Azure, privado, para las imágenes de contenedor de Docker. Este artículo trata cómo imágenes del contenedor toodeploy almacenan Hola del registro de contenedor de Azure tooAzure instancias de contenedor.

## <a name="using-hello-azure-cli"></a>Uso de hello CLI de Azure

Hola CLI de Azure incluye comandos para crear y administrar contenedores en instancias de contenedor de Azure. Si especifica una imagen privada en hello `create` comando, también puede especificar Hola imagen del registro requiere una contraseña tooauthenticate con registro de contenedor de Hola.

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

Hola `create` el comando también admite la especificación de hello `registry-login-server` y `registry-username`. Sin embargo, servidor de inicio de sesión de Hola para saludo del registro de contenedor de Azure es siempre *registryname*. nombre de usuario predeterminado hello y azurecr.io es *registryname*, por lo que estos valores se deducen del nombre de la imagen de hello si no se proporcionan explícitamente.

## <a name="using-an-azure-resource-manager-template"></a>Uso de una plantilla de Azure Resource Manager

Puede especificar propiedades de Hola de seguridad del registro de contenedor de Azure en una plantilla de Azure Resource Manager mediante la inclusión de hello `imageRegistryCredentials` propiedad de definición de grupo del contenedor de hello:

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

tooavoid almacenar la contraseña del registro de contenedor directamente en la plantilla de hello, se recomienda que se almacenan como un secreto en [el almacén de claves de Azure](../key-vault/key-vault-manage-with-cli2.md) y hacer referencia a él en plantilla de hello mediante hello [integración nativa entre Hola, Administrador de recursos de Azure y el almacén de claves](../azure-resource-manager/resource-manager-keyvault-parameter.md).

## <a name="using-hello-azure-portal"></a>Uso de hello portal de Azure

Si mantener imágenes de contenedor en hello del registro de contenedor de Azure, puede crear fácilmente un contenedor en instancias de contenedor de Azure mediante Hola portal de Azure.

1. Hola portal de Azure, navegue tooyour registro de contenedor.

2. Elija Repositorios.

    ![menú de registro de contenedor de Azure Hola Hola portal de Azure][acr-menu]

3. Elija el repositorio de Hola que desee toodeploy desde.

4. Haga clic en la etiqueta de hello para la imagen de contenedor de hello desea toodeploy.

    ![Menú contextual para iniciar el contenedor con Azure Container Instances][acr-runinstance-contextmenu]

5. Escriba un nombre para el contenedor de Hola y un nombre para el grupo de recursos de Hola. También puede cambiar los valores predeterminados de hello si lo desea.

    ![Menú Crear para Azure Container Instances][acr-create-deeplink]

6. Una vez que se haya completado la implementación de hello, puede navegar por grupo de contenedor toohello de hello notificaciones panel toofind su dirección IP y otras propiedades.

    ![Vista de detalles del grupo de contenedores de Azure Container Instances][aci-detailsview]

## <a name="next-steps"></a>Pasos siguientes

Saber cómo insertarlas del registro de contenedor privado tooa toobuild contenedores e implementarlos en instancias de contenedor de tooAzure por [completar el tutorial de hello](container-instances-tutorial-prepare-app.md).

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
