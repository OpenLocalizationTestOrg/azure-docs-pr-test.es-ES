---
title: "recurso compartido aaaFile para clúster SO/controlador de dominio de Azure | Documentos de Microsoft"
description: "Crear y montar un clúster de DC/OS de tooa de recurso compartido de archivos en el servicio de contenedor de Azure"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Mesos, Azure, recurso compartido de archivos, cifs
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a>Crear y montar un clúster de DC/OS de tooa de recurso compartido de archivos
Este tutorial describe cómo toocreate un archivo de recurso compartido en Azure y montar en cada agente y el maestro de Hola clúster DC/OS. Configurar un recurso compartido de archivos resulta más fácil de archivos tooshare en el clúster, como la configuración, el acceso, los registros y mucho más. Hola siguiente las tareas se completa en este tutorial:

> [!div class="checklist"]
> * Creación de una cuenta de Azure Storage
> * Creación de un recurso compartido de archivos
> * Montar el recurso compartido de hello en clúster de Hola DC/OS

Necesita un controlador de dominio ACS/OS hello toocomplete de clúster de los pasos de este tutorial. Si es necesario, este [script de ejemplo](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) puede crear uno.

Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a>Creación de un recurso compartido de archivos en Microsoft Azure

Antes de usar un recurso compartido de archivos de Azure con un clúster de ACS DC/OS, debe crearse Hola almacenamiento cuenta y archivo de recurso compartido. Ejecute hello después script toocreate Hola almacenamiento y archivo de recurso compartido. Actualizar los parámetros de hello con thoes de su entorno.

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a>Montar el recurso compartido de hello en el clúster

A continuación, Hola recurso compartido de archivos necesita toobe montado en cada máquina virtual en el clúster. Esta tarea se completa con la herramienta/protocolo de hello cifs. operación de montaje de Hello puede realizarse manualmente en cada nodo de clúster de hello, o ejecutando un script en cada nodo de clúster de Hola.

En este ejemplo, dos secuencias de comandos se ejecutan, uno toomount hello Azure archivos de recurso compartido y un segundo toorun esta secuencia de comandos en cada nodo del clúster de Hola DC/OS.

En primer lugar, se necesitan el nombre de cuenta de almacenamiento de Azure de Hola y clave de acceso. Siguiente ejecución Hola comandos tooget esta información. Tome nota de los valores, se usan en un paso posterior.

Nombre de la cuenta de almacenamiento:

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

Clave de acceso de la cuenta de almacenamiento:

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

A continuación, obtener Hola FQDN de Hola DC/OS maestro y almacenarlo en una variable.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Copie el nodo principal de toohello clave privada. Esta clave es necesaria toocreate un ssh conexiones con todos los nodos de clúster de Hola. Actualizar nombre de usuario de hello si se utilizó un valor no predeterminado al crear el clúster de Hola. 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

Crear una conexión SSH con hello (Hola primera maestra o) del clúster basadas en DC/OS. Actualizar nombre de usuario de hello si se utilizó un valor no predeterminado al crear el clúster de Hola.

```azurecli-interactive
ssh azureuser@$FQDN
```

Cree un archivo denominado **cifsMount.sh**, y Hola copia siguiendo contenido en él. 

Este script es el recurso compartido de archivos de Azure de hello toomount usado. Hola de actualización `STORAGE_ACCT_NAME` y `ACCESS_KEY` variables con hello información recopilan anteriormente.

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
Cree un segundo archivo denominado **getNodesRunScript.sh** y Hola copia siguiendo el contenido en el archivo hello. 

Este script detecta todos los nodos de clúster y, a continuación, se ejecuta hello **cifsMount.sh** script toomount Hola recurso compartido en cada uno de ellos.

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

Hola ejecución script toomount hello Azure recurso compartido de archivos en todos los nodos del clúster de Hola.

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

Hello recurso compartido de archivos es accesible en `/mnt/share/dcosshare` en cada nodo del clúster de Hola.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial un Azure recurso compartido de archivos era clúster de DC/OS realizadas tooa disponibles mediante los pasos de hello:

> [!div class="checklist"]
> * Creación de una cuenta de Azure Storage
> * Creación de un recurso compartido de archivos
> * Montar el recurso compartido de hello en clúster de Hola DC/OS

Avanzar toohello toolearn de tutorial siguiente sobre la integración de un registro de contenedor de Azure con controlador de dominio/OS en Azure.  

> [!div class="nextstepaction"]
> [Aplicaciones de equilibrio de carga](container-service-dcos-acr.md)