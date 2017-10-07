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
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="2b2c1-104">Implementación de un clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="2b2c1-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="2b2c1-105">DC/OS proporciona una plataforma distribuida para ejecutar aplicaciones modernas y en contenedores.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="2b2c1-106">Con Azure Container Service, el aprovisionamiento de un clúster de DC/OS listo para producción se realiza de forma rápida y sencilla.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="2b2c1-107">Este pasos básicos de inicio rápido detalles Hola necesitan toodeploy un clúster de DC/OS y ejecución de cargas de trabajo básico.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-107">This quick start details hello basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="2b2c1-108">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="2b2c1-109">Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-109">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2b2c1-110">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2b2c1-111">Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2b2c1-111">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="2b2c1-112">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="2b2c1-112">Log in tooAzure</span></span> 

<span data-ttu-id="2b2c1-113">Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-113">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="2b2c1-114">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2b2c1-114">Create a resource group</span></span>

<span data-ttu-id="2b2c1-115">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="2b2c1-116">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="2b2c1-117">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-117">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="2b2c1-118">Creación del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="2b2c1-118">Create DC/OS cluster</span></span>

<span data-ttu-id="2b2c1-119">Crear un clúster de DC/OS con hello [az acs crear](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-119">Create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="2b2c1-120">Hello en el ejemplo siguiente se crea un clúster de DC/OS denominado *myDCOSCluster* y crea las claves de SSH si aún no existen.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-120">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="2b2c1-121">toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-121">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="2b2c1-122">Después de varios minutos, comando hello completa y devuelve información acerca de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-122">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="2b2c1-123">Conecta el clúster de tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="2b2c1-123">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="2b2c1-124">Una vez creado un clúster de DC/OS, es accesible a través de un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="2b2c1-125">Ejecute hello después comando tooreturn Hola dirección IP pública del maestro de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-125">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="2b2c1-126">Esta dirección IP se almacena en una variable y usada en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-126">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="2b2c1-127">toocreate Hola túnel SSH, ejecute el siguiente comando de Hola y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-127">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="2b2c1-128">Si el puerto 80 ya está en uso, se produce un error en el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-128">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="2b2c1-129">Hola actualización túnel tooone de puerto no está en uso, como `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-129">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="2b2c1-130">se puede probar túnel SSH de Hello examinando demasiado`http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-130">hello SSH tunnel can be tested by browsing too`http://localhost`.</span></span> <span data-ttu-id="2b2c1-131">Si un puerto de otro que se ha utilizado 80, ajustar Hola ubicación toomatch.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-131">If a port other that 80 has been used, adjust hello location toomatch.</span></span> 

<span data-ttu-id="2b2c1-132">Si el túnel de hello SSH se creó correctamente, se devuelve portal de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-132">If hello SSH tunnel was successfully created, hello DC/OS portal is returned.</span></span>

![Interfaz de usuario de DCOS](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="2b2c1-134">Instalación de la CLI de DC/OS</span><span class="sxs-lookup"><span data-stu-id="2b2c1-134">Install DC/OS CLI</span></span>

<span data-ttu-id="2b2c1-135">interfaz de línea de comandos de Hola DC/OS es toomanage usa un clúster de DC/OS desde Hola de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-135">hello DC/OS command line interface is used toomanage a DC/OS cluster from hello command-line.</span></span> <span data-ttu-id="2b2c1-136">Instale Hola DC/OS cli con hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-136">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="2b2c1-137">Si utilizas Azure CloudShell, Hola DC/OS CLI ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-137">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="2b2c1-138">Si está ejecutando Hola CLI de Azure en Mac OS o Linux, tendrá que comando de hello toorun con sudo.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-138">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="2b2c1-139">Antes de hello que CLI puede utilizarse con clúster de hello, debe ser túnel SSH de toouse configurado Hola.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-139">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="2b2c1-140">toodo por lo tanto, ejecute hello siguiente comando, ajustar el puerto de hello si es necesario.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-140">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="2b2c1-141">Ejecución de una aplicación</span><span class="sxs-lookup"><span data-stu-id="2b2c1-141">Run an application</span></span>

<span data-ttu-id="2b2c1-142">valor predeterminado de Hello mecanismo para un clúster de ACS DC/OS de programación es maratón.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-142">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="2b2c1-143">Maratón es una aplicación de uso toostart y administrar el estado de Hola de aplicación hello en clúster de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-143">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="2b2c1-144">tooschedule una aplicación a través de maratón, cree un archivo denominado *app.json maratón*, y Hola copia siguiendo contenido en él.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-144">tooschedule an application through Marathon, create a file named *marathon-app.json*, and copy hello following contents into it.</span></span> 

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

<span data-ttu-id="2b2c1-145">Ejecute hello siguiente comando tooschedule Hola aplicación toorun de clúster de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-145">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="2b2c1-146">estado de implementación de hello toosee para la aplicación hello, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-146">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="2b2c1-147">Cuando Hola **espera** pasa el valor de la columna de *True* demasiado*False*, implementación de aplicación se haya completado.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-147">When hello **WAITING** column value switches from *True* too*False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="2b2c1-148">Obtener dirección IP pública de Hola de Hola DC/clúster agentes del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-148">Get hello public IP address of hello DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="2b2c1-149">Examinar dirección toothis devuelve sitio NGINX de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-149">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="2b2c1-151">Eliminación del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="2b2c1-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="2b2c1-152">Cuando ya no necesite, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, clúster de DC/OS y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-152">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="2b2c1-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2b2c1-153">Next steps</span></span>

<span data-ttu-id="2b2c1-154">En este tutorial, ha implementado un clúster de DC/OS y ha ejecutado un simple contenedor de Docker en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on hello cluster.</span></span> <span data-ttu-id="2b2c1-155">toolearn más información sobre el servicio de contenedor de Azure, seguir tutoriales de toohello ACS.</span><span class="sxs-lookup"><span data-stu-id="2b2c1-155">toolearn more about Azure Container Service, continue toohello ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b2c1-156">Administración de un clúster de ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="2b2c1-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)