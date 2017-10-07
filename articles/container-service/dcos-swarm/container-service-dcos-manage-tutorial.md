---
title: tutorial de servicio de contenedor de aaaAzure - DC/OS administrar | Documentos de Microsoft
description: Tutorial de Azure Container Service - Administrar DC/OS
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a>Tutorial de Azure Container Service - Administrar DC/OS

DC/OS proporciona una plataforma distribuida para ejecutar aplicaciones modernas y en contenedores. Con Azure Container Service, el aprovisionamiento de un clúster de DC/OS listo para producción se realiza de forma rápida y sencilla. Este inicio rápido se detallan los pasos básicos necesitan toodeploy un clúster de DC/OS y ejecución de cargas de trabajo básico.

> [!div class="checklist"]
> * Creación de un clúster de ACS DC/OS
> * Conectar el clúster toohello
> * Instalar Hola DC/OS CLI
> * Implementar un clúster de toohello de aplicación
> * Escalar una aplicación en clúster de Hola
> * Escalar los nodos del clúster Hola DC/OS
> * Administración básica de DC/OS
> * Eliminar el clúster de Hola DC/OS

Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-dcos-cluster"></a>Creación del clúster de DC/OS

En primer lugar, cree un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *westeurope* ubicación.

```azurecli
az group create --name myResourceGroup --location westeurope
```

A continuación, crear un clúster de DC/OS con hello [az acs crear](/cli/azure/acs#create) comando.

Hello en el ejemplo siguiente se crea un clúster de DC/OS denominado *myDCOSCluster* y crea las claves de SSH si aún no existen. toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

Después de varios minutos, comando hello completa y devuelve información acerca de la implementación de Hola.

## <a name="connect-toodcos-cluster"></a>Conecta el clúster de tooDC/OS

Una vez creado un clúster de DC/OS, es accesible a través de un túnel SSH. Ejecute hello después comando tooreturn Hola dirección IP pública del maestro de Hola DC/OS. Esta dirección IP se almacena en una variable y usada en el paso siguiente de saludo.

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

toocreate Hola túnel SSH, ejecute el siguiente comando de Hola y siga hello en pantalla instrucciones. Si el puerto 80 ya está en uso, se produce un error en el comando de Hola. Hola actualización túnel tooone de puerto no está en uso, como `85:localhost:80`. 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a>Instalación de la CLI de DC/OS

Instale Hola DC/OS cli con hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando. Si utilizas Azure CloudShell, Hola DC/OS CLI ya está instalado. Si está ejecutando Hola CLI de Azure en Mac OS o Linux, tendrá que comando de hello toorun con sudo.

```azurecli
az acs dcos install-cli
```

Antes de hello que CLI puede utilizarse con clúster de hello, debe ser túnel SSH de toouse configurado Hola. toodo por lo tanto, ejecute hello siguiente comando, ajustar el puerto de hello si es necesario.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Ejecución de una aplicación

valor predeterminado de Hello mecanismo para un clúster de ACS DC/OS de programación es maratón. Maratón es una aplicación de uso toostart y administrar el estado de Hola de aplicación hello en clúster de Hola DC/OS. tooschedule una aplicación a través de maratón, cree un archivo denominado **app.json maratón**, y Hola copia siguiendo contenido en él. 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Ejecute hello siguiente comando tooschedule Hola aplicación toorun de clúster de Hola DC/OS.

```azurecli
dcos marathon app add marathon-app.json
```

estado de implementación de hello toosee para la aplicación hello, ejecute el siguiente comando de Hola.

```azurecli
dcos marathon app list
```

Cuando Hola **tareas** pasa el valor de la columna de *0/1* demasiado*1/1*, implementación de aplicación se haya completado.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a>Escalado de la aplicación de Marathon

En el ejemplo anterior de hello, se creará una aplicación de instancia única. tooupdate esta implementación para que estén disponibles, tres instancias de la aplicación hello abrirán hello **app.json maratón** de archivos y actualizar too3 de propiedad de instancia de Hola.

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Actualizar la aplicación hello mediante hello `dcos marathon app update` comando.

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

estado de implementación de hello toosee para la aplicación hello, ejecute el siguiente comando de Hola.

```azurecli
dcos marathon app list
```

Cuando Hola **tareas** pasa el valor de la columna de *1/3* demasiado*3/1*, implementación de aplicación se haya completado.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a>Ejecución de una aplicación accesible a través de Internet

Hello ACS DC/OS clúster está formado por dos conjuntos de nodos, una pública que se pueda acceder en Hola internet y otra privada que no es accesible en Hola internet. conjunto predeterminado de Hello es nodos privada de hello, que se utilizó en el último ejemplo de Hola.

toomake una aplicación accesible en internet de Hola, implementarlas conjunto de nodos pública de toohello. toodo por lo tanto, proporcionar hello `acceptedResourceRoles` un valor de objeto `slave_public`.

Cree un archivo denominado **nginx public.json** y Hola copia siguiendo contenido en él.

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

Ejecute hello siguiente comando tooschedule Hola aplicación toorun de clúster de Hola DC/OS.

```azurecli 
dcos marathon app add nginx-public.json
```

Obtener dirección IP pública de Hola de Hola DC/clúster pública agentes del sistema operativo.

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Examinar dirección toothis devuelve sitio NGINX de hello predeterminado.

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a>Escalado del clúster de DC/OS

En los ejemplos anteriores de hello, una aplicación era la instancia de toomultiple escalado. infraestructura de DC/OS Hello también puede ser tooprovide escalado más o menos capacidad de proceso. Esto se hace con hello [az acs escalar]() comando. 

número actual de hello toosee de agentes de DC/OS, usar hello [az acs mostrar](/cli/azure/acs#show) comando.

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

tooincrease Hola too5 de recuento, use hello [az acs escalar](/cli/azure/acs#scale) comando. 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a>Eliminación del clúster de DC/OS

Cuando ya no necesite, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, clúster de DC/OS y todos ellos relacionados con recursos.

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido sobre tareas básicas de administración de DC/OS incluidos Hola siguientes. 

> [!div class="checklist"]
> * Creación de un clúster de ACS DC/OS
> * Conectar el clúster toohello
> * Instalar Hola DC/OS CLI
> * Implementar un clúster de toohello de aplicación
> * Escalar una aplicación en clúster de Hola
> * Escalar los nodos del clúster Hola DC/OS
> * Eliminar el clúster de Hola DC/OS

Toohello por adelantado siguiente toolearn tutorial acerca de cómo cargar la aplicación equilibrio en DC/OS en Azure. 

> [!div class="nextstepaction"]
> [Aplicaciones de equilibrio de carga](container-service-load-balancing.md)