---
title: Tutorial de Azure Container Service - Administrar DC/OS | Microsoft Docs
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
ms.openlocfilehash: e93f782c26c32f97749e817ec59ee3c2ecb7e119
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="ac2ff-104">Tutorial de Azure Container Service - Administrar DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="ac2ff-105">DC/OS proporciona una plataforma distribuida para ejecutar aplicaciones modernas y en contenedores.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="ac2ff-106">Con Azure Container Service, el aprovisionamiento de un clúster de DC/OS listo para producción se realiza de forma rápida y sencilla.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="ac2ff-107">En esta guía de inicio rápido se describen los pasos básicos necesarios para implementar un clúster de DC/OS y ejecutar una carga de trabajo básica.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-107">This quick start details basic steps needed to deploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ac2ff-108">Creación de un clúster de ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="ac2ff-109">Conexión al clúster</span><span class="sxs-lookup"><span data-stu-id="ac2ff-109">Connect to the cluster</span></span>
> * <span data-ttu-id="ac2ff-110">Instalación de la CLI de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-110">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="ac2ff-111">Implementación de una aplicación en el clúster</span><span class="sxs-lookup"><span data-stu-id="ac2ff-111">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="ac2ff-112">Escalado de una aplicación en el clúster</span><span class="sxs-lookup"><span data-stu-id="ac2ff-112">Scale an application on the cluster</span></span>
> * <span data-ttu-id="ac2ff-113">Escalado de los nodos del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-113">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="ac2ff-114">Administración básica de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="ac2ff-115">Eliminación del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-115">Delete the DC/OS cluster</span></span>

<span data-ttu-id="ac2ff-116">Para realizar este tutorial es necesaria la versión 2.0.4 o superior de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-116">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ac2ff-117">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-117">Run `az --version` to find the version.</span></span> <span data-ttu-id="ac2ff-118">Si necesita actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ac2ff-118">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="ac2ff-119">Creación del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-119">Create DC/OS cluster</span></span>

<span data-ttu-id="ac2ff-120">En primer lugar, cree un grupo de recursos con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ac2ff-120">First, create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ac2ff-121">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="ac2ff-122">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-122">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="ac2ff-123">A continuación, cree un clúster de DC/OS con el comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="ac2ff-123">Next, create a DC/OS cluster with the [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="ac2ff-124">En el ejemplo siguiente se crea un clúster de DC/OS denominado *myDCOSCluster* y las claves SSH si aún no existen.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-124">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="ac2ff-125">Para utilizar un conjunto específico de claves, utilice la opción `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-125">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="ac2ff-126">Después de varios minutos, el comando se completa y muestra la información sobre la implementación.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-126">After several minutes, the command completes, and returns information about the deployment.</span></span>

## <a name="connect-to-dcos-cluster"></a><span data-ttu-id="ac2ff-127">Conexión al clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-127">Connect to DC/OS cluster</span></span>

<span data-ttu-id="ac2ff-128">Una vez creado un clúster de DC/OS, es accesible a través de un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="ac2ff-129">Ejecute el comando siguiente para devolver la dirección IP pública del patrón de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-129">Run the following command to return the public IP address of the DC/OS master.</span></span> <span data-ttu-id="ac2ff-130">Esta dirección IP se almacena en una variable y se utiliza en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-130">This IP address is stored in a variable and used in the next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="ac2ff-131">Para crear el túnel SSH, ejecute el siguiente comando y siga las instrucciones en pantalla.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-131">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span></span> <span data-ttu-id="ac2ff-132">Si el puerto 80 ya está en uso, se produce un error en el comando.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-132">If port 80 is already in use, the command fails.</span></span> <span data-ttu-id="ac2ff-133">Actualice el puerto de túnel a uno que no esté en uso, como `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-133">Update the tunneled port to one not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="ac2ff-134">Instalación de la CLI de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-134">Install DC/OS CLI</span></span>

<span data-ttu-id="ac2ff-135">Instale la CLI de DC/OS con el comando [az acs dcos install-cli](/azure/acs/dcos#install-cli).</span><span class="sxs-lookup"><span data-stu-id="ac2ff-135">Install the DC/OS cli using the [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="ac2ff-136">Si usa Azure CloudShell, la CLI de DC/OS ya estará instalada.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-136">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span></span> <span data-ttu-id="ac2ff-137">Si está ejecutando la CLI de Azure en macOS o Linux, es posible que tenga que ejecutar el comando con sudo.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-137">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="ac2ff-138">Antes de usar la CLI con el clúster, debe configurarse para usar el túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-138">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span></span> <span data-ttu-id="ac2ff-139">Para ello, ejecute el comando siguiente, ajustando el puerto si es necesario.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-139">To do so, run the following command, adjusting the port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="ac2ff-140">Ejecución de una aplicación</span><span class="sxs-lookup"><span data-stu-id="ac2ff-140">Run an application</span></span>

<span data-ttu-id="ac2ff-141">El mecanismo de programación predeterminado para un clúster de ACS DC/OS es Marathon.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-141">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="ac2ff-142">Marathon se usa para iniciar una aplicación y administrar el estado de la aplicación en el clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-142">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span></span> <span data-ttu-id="ac2ff-143">Para programar una aplicación mediante Marathon, cree un archivo denominado **marathon-app.json** y copie el siguiente contenido en él.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-143">To schedule an application through Marathon, create a file named **marathon-app.json**, and copy the following contents into it.</span></span> 

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

<span data-ttu-id="ac2ff-144">Ejecute el comando siguiente para programar la aplicación que ejecutar en el clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-144">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="ac2ff-145">Para ver el estado de implementación de la aplicación, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-145">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="ac2ff-146">Cuando el valor de la columna **TASKS** cambie de *0/1* a *1/1*, se habrá completado la implementación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-146">When the **TASKS** column value switches from *0/1* to *1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="ac2ff-147">Escalado de la aplicación de Marathon</span><span class="sxs-lookup"><span data-stu-id="ac2ff-147">Scale Marathon application</span></span>

<span data-ttu-id="ac2ff-148">En el ejemplo anterior, se creó una aplicación de instancia única.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-148">In the previous example, a single instance application was created.</span></span> <span data-ttu-id="ac2ff-149">Para actualizar esta implementación para que haya disponibles tres instancias de la aplicación, abra el archivo **marathon-app.json** y actualice la propiedad de instancias a 3.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-149">To update this deployment so that three instances of the application are available, open up the **marathon-app.json** file, and update the instance property to 3.</span></span>

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

<span data-ttu-id="ac2ff-150">Actualice la aplicación mediante el comando `dcos marathon app update`.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-150">Update the application using the `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="ac2ff-151">Para ver el estado de implementación de la aplicación, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-151">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="ac2ff-152">Cuando el valor de la columna **TASKS** cambie de *1/3* a *3/1*, se habrá completado la implementación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-152">When the **TASKS** column value switches from *1/3* to *3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="ac2ff-153">Ejecución de una aplicación accesible a través de Internet</span><span class="sxs-lookup"><span data-stu-id="ac2ff-153">Run internet accessible app</span></span>

<span data-ttu-id="ac2ff-154">El clúster de ACS DC/OS consta de dos conjuntos de nodos: uno público, que es accesible en Internet, y otro privado, que no es accesible en Internet.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-154">The ACS DC/OS cluster consists of two node sets, one public which is accessible on the internet, and one private which is not accessible on the internet.</span></span> <span data-ttu-id="ac2ff-155">El conjunto predeterminado es el de nodos privados, que se utilizó en el último ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-155">The default set is the private nodes, which was used in the last example.</span></span>

<span data-ttu-id="ac2ff-156">Para que una aplicación sea accesible en Internet, impleméntela en el conjunto de nodos públicos.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-156">To make an application accessible on the internet, deploy them to the public node set.</span></span> <span data-ttu-id="ac2ff-157">Para ello, asigne al objeto `acceptedResourceRoles` un valor de `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-157">To do so, give the `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="ac2ff-158">Cree un archivo denominado **nginx-public.json** y copie en él el contenido siguiente.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-158">Create a file named **nginx-public.json** and copy the following contents into it.</span></span>

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

<span data-ttu-id="ac2ff-159">Ejecute el comando siguiente para programar la aplicación que ejecutar en el clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-159">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="ac2ff-160">Obtenga la dirección IP pública de los agentes de clúster públicos de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-160">Get the public IP address of the DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="ac2ff-161">Esta dirección dirige al sitio de NGINX predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-161">Browsing to this address returns the default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="ac2ff-163">Escalado del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="ac2ff-164">En los ejemplos anteriores, una aplicación se ha escalado a varias instancias.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-164">In the previous examples, an application was scaled to multiple instance.</span></span> <span data-ttu-id="ac2ff-165">También se puede escalar la infraestructura de DC/OS para proporcionar más o menos capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-165">The DC/OS infrastructure can also be scaled to provide more or less compute capacity.</span></span> <span data-ttu-id="ac2ff-166">Esto se realiza con el comando [az acs scale]().</span><span class="sxs-lookup"><span data-stu-id="ac2ff-166">This is done with the [az acs scale]() command.</span></span> 

<span data-ttu-id="ac2ff-167">Para ver el recuento actual de agentes de DC/OS, use el comando [az acs show](/cli/azure/acs#show).</span><span class="sxs-lookup"><span data-stu-id="ac2ff-167">To see the current count of DC/OS agents, use the [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="ac2ff-168">Para aumentar el total a 5, utilice el comando [az acs scale](/cli/azure/acs#scale).</span><span class="sxs-lookup"><span data-stu-id="ac2ff-168">To increase the count to 5, use the [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="ac2ff-169">Eliminación del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="ac2ff-170">Cuando ya no se necesiten, puede usar el comando [az group delete](/cli/azure/group#delete) para quitar el grupo de recursos, el clúster de DC/OS y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-170">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="ac2ff-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac2ff-171">Next steps</span></span>

<span data-ttu-id="ac2ff-172">En este tutorial, ha aprendido sobre tareas básicas de administración de DC/OS, incluidas las siguientes.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-172">In this tutorial, you have learned about basic DC/OS management task including the following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ac2ff-173">Creación de un clúster de ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="ac2ff-174">Conexión al clúster</span><span class="sxs-lookup"><span data-stu-id="ac2ff-174">Connect to the cluster</span></span>
> * <span data-ttu-id="ac2ff-175">Instalación de la CLI de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-175">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="ac2ff-176">Implementación de una aplicación en el clúster</span><span class="sxs-lookup"><span data-stu-id="ac2ff-176">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="ac2ff-177">Escalado de una aplicación en el clúster</span><span class="sxs-lookup"><span data-stu-id="ac2ff-177">Scale an application on the cluster</span></span>
> * <span data-ttu-id="ac2ff-178">Escalado de los nodos del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-178">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="ac2ff-179">Eliminación del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac2ff-179">Delete the DC/OS cluster</span></span>

<span data-ttu-id="ac2ff-180">Vaya al siguiente tutorial para obtener información acerca de la aplicación de equilibrio de carga de DC/OS en Azure.</span><span class="sxs-lookup"><span data-stu-id="ac2ff-180">Advance to the next tutorial to learn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac2ff-181">Aplicaciones de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="ac2ff-181">Load balance applications</span></span>](container-service-load-balancing.md)