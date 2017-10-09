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
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a><span data-ttu-id="416ed-104">Crear y montar un clúster de DC/OS de tooa de recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="416ed-104">Create and mount a file share tooa DC/OS cluster</span></span>
<span data-ttu-id="416ed-105">Este tutorial describe cómo toocreate un archivo de recurso compartido en Azure y montar en cada agente y el maestro de Hola clúster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="416ed-105">This tutorial details how toocreate a file share in Azure and mount it on each agent and master of hello DC/OS cluster.</span></span> <span data-ttu-id="416ed-106">Configurar un recurso compartido de archivos resulta más fácil de archivos tooshare en el clúster, como la configuración, el acceso, los registros y mucho más.</span><span class="sxs-lookup"><span data-stu-id="416ed-106">Setting up a file share makes it easier tooshare files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="416ed-107">Hola siguiente las tareas se completa en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="416ed-107">hello following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="416ed-108">Creación de una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="416ed-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="416ed-109">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="416ed-109">Create a file share</span></span>
> * <span data-ttu-id="416ed-110">Montar el recurso compartido de hello en clúster de Hola DC/OS</span><span class="sxs-lookup"><span data-stu-id="416ed-110">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="416ed-111">Necesita un controlador de dominio ACS/OS hello toocomplete de clúster de los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="416ed-111">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="416ed-112">Si es necesario, este [script de ejemplo](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) puede crear uno.</span><span class="sxs-lookup"><span data-stu-id="416ed-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="416ed-113">Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="416ed-113">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="416ed-114">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="416ed-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="416ed-115">Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="416ed-115">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="416ed-116">Creación de un recurso compartido de archivos en Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="416ed-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="416ed-117">Antes de usar un recurso compartido de archivos de Azure con un clúster de ACS DC/OS, debe crearse Hola almacenamiento cuenta y archivo de recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="416ed-117">Before using an Azure file share with an ACS DC/OS cluster, hello storage account and file share must be created.</span></span> <span data-ttu-id="416ed-118">Ejecute hello después script toocreate Hola almacenamiento y archivo de recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="416ed-118">Run hello following script toocreate hello storage and file share.</span></span> <span data-ttu-id="416ed-119">Actualizar los parámetros de hello con thoes de su entorno.</span><span class="sxs-lookup"><span data-stu-id="416ed-119">Update hello parameters with thoes from your environment.</span></span>

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

## <a name="mount-hello-share-in-your-cluster"></a><span data-ttu-id="416ed-120">Montar el recurso compartido de hello en el clúster</span><span class="sxs-lookup"><span data-stu-id="416ed-120">Mount hello share in your cluster</span></span>

<span data-ttu-id="416ed-121">A continuación, Hola recurso compartido de archivos necesita toobe montado en cada máquina virtual en el clúster.</span><span class="sxs-lookup"><span data-stu-id="416ed-121">Next, hello file share needs toobe mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="416ed-122">Esta tarea se completa con la herramienta/protocolo de hello cifs.</span><span class="sxs-lookup"><span data-stu-id="416ed-122">This task is completed using hello cifs tool/protocol.</span></span> <span data-ttu-id="416ed-123">operación de montaje de Hello puede realizarse manualmente en cada nodo de clúster de hello, o ejecutando un script en cada nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="416ed-123">hello mount operation can be completed manually on each node of hello cluster, or by running a script against each node in hello cluster.</span></span>

<span data-ttu-id="416ed-124">En este ejemplo, dos secuencias de comandos se ejecutan, uno toomount hello Azure archivos de recurso compartido y un segundo toorun esta secuencia de comandos en cada nodo del clúster de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="416ed-124">In this example, two scripts are run, one toomount hello Azure file share, and a second toorun this script on each node of hello DC/OS cluster.</span></span>

<span data-ttu-id="416ed-125">En primer lugar, se necesitan el nombre de cuenta de almacenamiento de Azure de Hola y clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="416ed-125">First, hello Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="416ed-126">Siguiente ejecución Hola comandos tooget esta información.</span><span class="sxs-lookup"><span data-stu-id="416ed-126">Run hello following commands tooget this information.</span></span> <span data-ttu-id="416ed-127">Tome nota de los valores, se usan en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="416ed-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="416ed-128">Nombre de la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="416ed-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="416ed-129">Clave de acceso de la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="416ed-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="416ed-130">A continuación, obtener Hola FQDN de Hola DC/OS maestro y almacenarlo en una variable.</span><span class="sxs-lookup"><span data-stu-id="416ed-130">Next, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="416ed-131">Copie el nodo principal de toohello clave privada.</span><span class="sxs-lookup"><span data-stu-id="416ed-131">Copy your private key toohello master node.</span></span> <span data-ttu-id="416ed-132">Esta clave es necesaria toocreate un ssh conexiones con todos los nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="416ed-132">This key is needed toocreate an ssh connection with all nodes in hello cluster.</span></span> <span data-ttu-id="416ed-133">Actualizar nombre de usuario de hello si se utilizó un valor no predeterminado al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="416ed-133">Update hello user name if a non-default value was used when creating hello cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="416ed-134">Crear una conexión SSH con hello (Hola primera maestra o) del clúster basadas en DC/OS.</span><span class="sxs-lookup"><span data-stu-id="416ed-134">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="416ed-135">Actualizar nombre de usuario de hello si se utilizó un valor no predeterminado al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="416ed-135">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="416ed-136">Cree un archivo denominado **cifsMount.sh**, y Hola copia siguiendo contenido en él.</span><span class="sxs-lookup"><span data-stu-id="416ed-136">Create a file named **cifsMount.sh**, and copy hello following contents into it.</span></span> 

<span data-ttu-id="416ed-137">Este script es el recurso compartido de archivos de Azure de hello toomount usado.</span><span class="sxs-lookup"><span data-stu-id="416ed-137">This script is used toomount hello Azure file share.</span></span> <span data-ttu-id="416ed-138">Hola de actualización `STORAGE_ACCT_NAME` y `ACCESS_KEY` variables con hello información recopilan anteriormente.</span><span class="sxs-lookup"><span data-stu-id="416ed-138">Update hello `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with hello information collected earlier.</span></span>

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
<span data-ttu-id="416ed-139">Cree un segundo archivo denominado **getNodesRunScript.sh** y Hola copia siguiendo el contenido en el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="416ed-139">Create a second file named **getNodesRunScript.sh** and copy hello following contents into hello file.</span></span> 

<span data-ttu-id="416ed-140">Este script detecta todos los nodos de clúster y, a continuación, se ejecuta hello **cifsMount.sh** script toomount Hola recurso compartido en cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="416ed-140">This script discovers all cluster nodes, and then runs hello **cifsMount.sh** script toomount hello file share on each.</span></span>

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

<span data-ttu-id="416ed-141">Hola ejecución script toomount hello Azure recurso compartido de archivos en todos los nodos del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="416ed-141">Run hello script toomount hello Azure file share on all nodes of hello cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="416ed-142">Hello recurso compartido de archivos es accesible en `/mnt/share/dcosshare` en cada nodo del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="416ed-142">hello file share is now accessible at `/mnt/share/dcosshare` on each node of hello cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="416ed-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="416ed-143">Next steps</span></span>

<span data-ttu-id="416ed-144">En este tutorial un Azure recurso compartido de archivos era clúster de DC/OS realizadas tooa disponibles mediante los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="416ed-144">In this tutorial an Azure file share was made available tooa DC/OS cluster using hello steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="416ed-145">Creación de una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="416ed-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="416ed-146">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="416ed-146">Create a file share</span></span>
> * <span data-ttu-id="416ed-147">Montar el recurso compartido de hello en clúster de Hola DC/OS</span><span class="sxs-lookup"><span data-stu-id="416ed-147">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="416ed-148">Avanzar toohello toolearn de tutorial siguiente sobre la integración de un registro de contenedor de Azure con controlador de dominio/OS en Azure.</span><span class="sxs-lookup"><span data-stu-id="416ed-148">Advance toohello next tutorial toolearn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="416ed-149">Aplicaciones de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="416ed-149">Load balance applications</span></span>](container-service-dcos-acr.md)