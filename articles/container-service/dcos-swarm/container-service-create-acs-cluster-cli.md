---
title: "aaaDeploy un clúster de contenedor de Docker - CLI de Azure | Documentos de Microsoft"
description: "Implementación de una solución Kubernetes, DC/OS o Docker Swarm en Azure Container Service mediante la CLI de Azure 2.0"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a>Implementar un contenedor de Docker con hello Azure CLI 2.0 de solución de hospedaje

Hola de uso `az acs` comandos de CLI de Azure 2.0 hello toocreate y administrar los clústeres en el servicio de contenedor de Azure. También puede implementar un clúster de servicio de contenedor de Azure mediante el uso de hello [portal de Azure](container-service-deployment.md) u Hola API de servicio de contenedor de Azure.

Para obtener ayuda sobre `az acs` comandos, pasar hello `-h` comando tooany de parámetro. Por ejemplo: `az acs create -h`.



## <a name="prerequisites"></a>Requisitos previos
toocreate un clúster de servicio de contenedor de Azure con Hola 2.0 de CLI de Azure, debe:
* tener una cuenta de Azure ([obtenga aquí una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/))
* tener instalado y configurado hello [2.0 de CLI de Azure](/cli/azure/install-az-cli2)

## <a name="get-started"></a>Primeros pasos 
### <a name="log-in-tooyour-account"></a>Inicie sesión en la cuenta de tooyour
```azurecli
az login 
```

Siga toolog de mensajes de Hola en forma interactiva. Para otro toolog métodos en, consulte [empezar a trabajar con Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).

### <a name="set-your-azure-subscription"></a>Establecimiento de una suscripción a Azure

Si tiene más de una suscripción de Azure, establezca suscripción predeterminada de Hola. Por ejemplo:

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a>Crear un grupo de recursos
Se recomienda crear un grupo de recursos para cada clúster. Especifique una región de Azure en la que Azure Container Service esté [disponible](https://azure.microsoft.com/en-us/regions/services/). Por ejemplo:

```azurecli
az group create -n acsrg1 -l "westus"
```
Salida es la siguiente de toohello similar:

![Crear un grupo de recursos](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a>Creación de un clúster de Azure Container Service

toocreate un clúster, use `az acs create`.
Un nombre para el clúster de Hola y específicos de Hola Hola del grupo de recursos creado en el paso anterior de hello son parámetros obligatorios. 

Otras entradas son valores del conjunto toodefault (vea Hola después de la pantalla), a menos que se sobrescribe con sus respectivos conmutadores. Por ejemplo, orchestrator hello es establecer predeterminado tooDC/OS. Y si no se especifica uno, un prefijo de nombre DNS se crea basándose en nombre del clúster Hola.

![Uso de az acs create](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a>Uso rápido de `acs create` con los valores predeterminados
Si tiene un archivo de clave público SSH RSA `id_rsa.pub` en la ubicación predeterminada de hello (o crear uno para [OS X y Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) o [Windows](../../virtual-machines/linux/ssh-from-windows.md)), utilice un comando similar al siguiente hello:

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
Si no tiene una clave pública SSH, use este segundo comando. Este comando con hello `--generate-ssh-keys` conmutador crea uno automáticamente.

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

Después de escribir el comando de hello, espere unos 10 minutos para hello clúster toobe creado. resultado del comando Hello incluye nombres de dominio completo (FQDN) del patrón de Hola y nodos de agente y un tooconnect toohello SSH comando primer patrón. Este es un resultado abreviado:

![Imagen del comando create de ACS](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> Hola [Kubernetes tutorial](../kubernetes/container-service-kubernetes-walkthrough.md) muestra cómo toouse `az acs create` con toocreate de valores de forma predeterminada un Kubernetes de clúster.
>

## <a name="manage-acs-clusters"></a>Administración de clústeres de ACS

Uso adicional `az acs` comandos toomanage el clúster. Estos son algunos ejemplos.

### <a name="list-clusters-under-a-subscription"></a>Lista de clústeres de una suscripción

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a>Lista de clústeres de un grupo de recursos

```azurecli
az acs list -g acsrg1 --output table
```

![acs list](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a>Visualización de los detalles de un clúster del servicio de contenedor

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![acs show](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a>Clúster de Hola de escala
Se permite la reducción y el escalado horizontales de nodos de agente. Hola parámetro `new-agent-count` es Hola nuevo número de agentes en el clúster de hello ACS.

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![acs scale](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a>Eliminación de un clúster del servicio de contenedor
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
Este comando no elimina todos los recursos (red y almacenamiento) creados durante la creación de servicio de contenedor de Hola. toodelete todos los recursos fácilmente, se recomienda implementar cada clúster en un grupo de recursos distinto. A continuación, eliminar grupo de recursos de hello cuando ya no se necesita el clúster de Hola.

## <a name="next-steps"></a>Pasos siguientes
Ahora que tiene un clúster funcionando, consulte los siguientes documentos para obtener información detallada sobre conexión y administración:

* [Conectar el clúster del servicio de contenedor de Azure tooan](../container-service-connect.md)
* [Administración de contenedores con la API de REST](container-service-mesos-marathon-rest.md)
* [Administración de contenedores con Docker Swarm](container-service-docker-swarm.md)
* [Trabajo con Azure Container Service y Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md)