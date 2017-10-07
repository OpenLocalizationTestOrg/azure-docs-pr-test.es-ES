---
title: "aaaAzure inicio rápido de servicio de contenedor - implementar clústeres de DC/OS | Documentos de Microsoft"
description: "Guía de inicio rápido de Azure Container Service - Implementación del clúster de DC/OS"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a>Implementación de un clúster de DC/OS

DC/OS proporciona una plataforma distribuida para ejecutar aplicaciones modernas y en contenedores. Con Azure Container Service, el aprovisionamiento de un clúster de DC/OS listo para producción se realiza de forma rápida y sencilla. Este pasos básicos de inicio rápido detalles Hola necesitan toodeploy un clúster de DC/OS y ejecución de cargas de trabajo básico.

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure 

Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.

```azurecli
az login
```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a>Creación del clúster de DC/OS

Crear un clúster de DC/OS con hello [az acs crear](/cli/azure/acs#create) comando.

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

se puede probar túnel SSH de Hello examinando demasiado`http://localhost`. Si un puerto de otro que se ha utilizado 80, ajustar Hola ubicación toomatch. 

Si el túnel de hello SSH se creó correctamente, se devuelve portal de Hola DC/OS.

![Interfaz de usuario de DCOS](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a>Instalación de la CLI de DC/OS

interfaz de línea de comandos de Hola DC/OS es toomanage usa un clúster de DC/OS desde Hola de línea de comandos. Instale Hola DC/OS cli con hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando. Si utilizas Azure CloudShell, Hola DC/OS CLI ya está instalado. 

Si está ejecutando Hola CLI de Azure en Mac OS o Linux, tendrá que comando de hello toorun con sudo.

```azurecli
az acs dcos install-cli
```

Antes de hello que CLI puede utilizarse con clúster de hello, debe ser túnel SSH de toouse configurado Hola. toodo por lo tanto, ejecute hello siguiente comando, ajustar el puerto de hello si es necesario.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Ejecución de una aplicación

valor predeterminado de Hello mecanismo para un clúster de ACS DC/OS de programación es maratón. Maratón es una aplicación de uso toostart y administrar el estado de Hola de aplicación hello en clúster de Hola DC/OS. tooschedule una aplicación a través de maratón, cree un archivo denominado *app.json maratón*, y Hola copia siguiendo contenido en él. 

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
dcos marathon app add marathon-app.json
```

estado de implementación de hello toosee para la aplicación hello, ejecute el siguiente comando de Hola.

```azurecli
dcos marathon app list
```

Cuando Hola **espera** pasa el valor de la columna de *True* demasiado*False*, implementación de aplicación se haya completado.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

Obtener dirección IP pública de Hola de Hola DC/clúster agentes del sistema operativo.

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Examinar dirección toothis devuelve sitio NGINX de hello predeterminado.

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a>Eliminación del clúster de DC/OS

Cuando ya no necesite, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, clúster de DC/OS y todos ellos relacionados con recursos.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha implementado un clúster de DC/OS y ha ejecutado un simple contenedor de Docker en clúster de Hola. toolearn más información sobre el servicio de contenedor de Azure, seguir tutoriales de toohello ACS.

> [!div class="nextstepaction"]
> [Administración de un clúster de ACS DC/OS](container-service-dcos-manage-tutorial.md)