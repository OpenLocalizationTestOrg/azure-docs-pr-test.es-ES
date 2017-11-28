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
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="9dc12-104">Tutorial de Azure Container Service - Administrar DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="9dc12-105">DC/OS proporciona una plataforma distribuida para ejecutar aplicaciones modernas y en contenedores.</span><span class="sxs-lookup"><span data-stu-id="9dc12-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="9dc12-106">Con Azure Container Service, el aprovisionamiento de un clúster de DC/OS listo para producción se realiza de forma rápida y sencilla.</span><span class="sxs-lookup"><span data-stu-id="9dc12-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="9dc12-107">Este inicio rápido se detallan los pasos básicos necesitan toodeploy un clúster de DC/OS y ejecución de cargas de trabajo básico.</span><span class="sxs-lookup"><span data-stu-id="9dc12-107">This quick start details basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9dc12-108">Creación de un clúster de ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="9dc12-109">Conectar el clúster toohello</span><span class="sxs-lookup"><span data-stu-id="9dc12-109">Connect toohello cluster</span></span>
> * <span data-ttu-id="9dc12-110">Instalar Hola DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="9dc12-110">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="9dc12-111">Implementar un clúster de toohello de aplicación</span><span class="sxs-lookup"><span data-stu-id="9dc12-111">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="9dc12-112">Escalar una aplicación en clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="9dc12-112">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="9dc12-113">Escalar los nodos del clúster Hola DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-113">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="9dc12-114">Administración básica de DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="9dc12-115">Eliminar el clúster de Hola DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-115">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="9dc12-116">Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="9dc12-116">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9dc12-117">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dc12-117">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9dc12-118">Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9dc12-118">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="9dc12-119">Creación del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-119">Create DC/OS cluster</span></span>

<span data-ttu-id="9dc12-120">En primer lugar, cree un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="9dc12-120">First, create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="9dc12-121">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc12-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="9dc12-122">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *westeurope* ubicación.</span><span class="sxs-lookup"><span data-stu-id="9dc12-122">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="9dc12-123">A continuación, crear un clúster de DC/OS con hello [az acs crear](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="9dc12-123">Next, create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="9dc12-124">Hello en el ejemplo siguiente se crea un clúster de DC/OS denominado *myDCOSCluster* y crea las claves de SSH si aún no existen.</span><span class="sxs-lookup"><span data-stu-id="9dc12-124">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="9dc12-125">toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.</span><span class="sxs-lookup"><span data-stu-id="9dc12-125">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="9dc12-126">Después de varios minutos, comando hello completa y devuelve información acerca de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dc12-126">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="9dc12-127">Conecta el clúster de tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-127">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="9dc12-128">Una vez creado un clúster de DC/OS, es accesible a través de un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="9dc12-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="9dc12-129">Ejecute hello después comando tooreturn Hola dirección IP pública del maestro de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="9dc12-129">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="9dc12-130">Esta dirección IP se almacena en una variable y usada en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="9dc12-130">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="9dc12-131">toocreate Hola túnel SSH, ejecute el siguiente comando de Hola y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="9dc12-131">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="9dc12-132">Si el puerto 80 ya está en uso, se produce un error en el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dc12-132">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="9dc12-133">Hola actualización túnel tooone de puerto no está en uso, como `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="9dc12-133">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="9dc12-134">Instalación de la CLI de DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-134">Install DC/OS CLI</span></span>

<span data-ttu-id="9dc12-135">Instale Hola DC/OS cli con hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="9dc12-135">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="9dc12-136">Si utilizas Azure CloudShell, Hola DC/OS CLI ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="9dc12-136">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> <span data-ttu-id="9dc12-137">Si está ejecutando Hola CLI de Azure en Mac OS o Linux, tendrá que comando de hello toorun con sudo.</span><span class="sxs-lookup"><span data-stu-id="9dc12-137">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="9dc12-138">Antes de hello que CLI puede utilizarse con clúster de hello, debe ser túnel SSH de toouse configurado Hola.</span><span class="sxs-lookup"><span data-stu-id="9dc12-138">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="9dc12-139">toodo por lo tanto, ejecute hello siguiente comando, ajustar el puerto de hello si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9dc12-139">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="9dc12-140">Ejecución de una aplicación</span><span class="sxs-lookup"><span data-stu-id="9dc12-140">Run an application</span></span>

<span data-ttu-id="9dc12-141">valor predeterminado de Hello mecanismo para un clúster de ACS DC/OS de programación es maratón.</span><span class="sxs-lookup"><span data-stu-id="9dc12-141">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="9dc12-142">Maratón es una aplicación de uso toostart y administrar el estado de Hola de aplicación hello en clúster de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="9dc12-142">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="9dc12-143">tooschedule una aplicación a través de maratón, cree un archivo denominado **app.json maratón**, y Hola copia siguiendo contenido en él.</span><span class="sxs-lookup"><span data-stu-id="9dc12-143">tooschedule an application through Marathon, create a file named **marathon-app.json**, and copy hello following contents into it.</span></span> 

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

<span data-ttu-id="9dc12-144">Ejecute hello siguiente comando tooschedule Hola aplicación toorun de clúster de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="9dc12-144">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="9dc12-145">estado de implementación de hello toosee para la aplicación hello, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dc12-145">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="9dc12-146">Cuando Hola **tareas** pasa el valor de la columna de *0/1* demasiado*1/1*, implementación de aplicación se haya completado.</span><span class="sxs-lookup"><span data-stu-id="9dc12-146">When hello **TASKS** column value switches from *0/1* too*1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="9dc12-147">Escalado de la aplicación de Marathon</span><span class="sxs-lookup"><span data-stu-id="9dc12-147">Scale Marathon application</span></span>

<span data-ttu-id="9dc12-148">En el ejemplo anterior de hello, se creará una aplicación de instancia única.</span><span class="sxs-lookup"><span data-stu-id="9dc12-148">In hello previous example, a single instance application was created.</span></span> <span data-ttu-id="9dc12-149">tooupdate esta implementación para que estén disponibles, tres instancias de la aplicación hello abrirán hello **app.json maratón** de archivos y actualizar too3 de propiedad de instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dc12-149">tooupdate this deployment so that three instances of hello application are available, open up hello **marathon-app.json** file, and update hello instance property too3.</span></span>

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

<span data-ttu-id="9dc12-150">Actualizar la aplicación hello mediante hello `dcos marathon app update` comando.</span><span class="sxs-lookup"><span data-stu-id="9dc12-150">Update hello application using hello `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="9dc12-151">estado de implementación de hello toosee para la aplicación hello, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dc12-151">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="9dc12-152">Cuando Hola **tareas** pasa el valor de la columna de *1/3* demasiado*3/1*, implementación de aplicación se haya completado.</span><span class="sxs-lookup"><span data-stu-id="9dc12-152">When hello **TASKS** column value switches from *1/3* too*3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="9dc12-153">Ejecución de una aplicación accesible a través de Internet</span><span class="sxs-lookup"><span data-stu-id="9dc12-153">Run internet accessible app</span></span>

<span data-ttu-id="9dc12-154">Hello ACS DC/OS clúster está formado por dos conjuntos de nodos, una pública que se pueda acceder en Hola internet y otra privada que no es accesible en Hola internet.</span><span class="sxs-lookup"><span data-stu-id="9dc12-154">hello ACS DC/OS cluster consists of two node sets, one public which is accessible on hello internet, and one private which is not accessible on hello internet.</span></span> <span data-ttu-id="9dc12-155">conjunto predeterminado de Hello es nodos privada de hello, que se utilizó en el último ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dc12-155">hello default set is hello private nodes, which was used in hello last example.</span></span>

<span data-ttu-id="9dc12-156">toomake una aplicación accesible en internet de Hola, implementarlas conjunto de nodos pública de toohello.</span><span class="sxs-lookup"><span data-stu-id="9dc12-156">toomake an application accessible on hello internet, deploy them toohello public node set.</span></span> <span data-ttu-id="9dc12-157">toodo por lo tanto, proporcionar hello `acceptedResourceRoles` un valor de objeto `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="9dc12-157">toodo so, give hello `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="9dc12-158">Cree un archivo denominado **nginx public.json** y Hola copia siguiendo contenido en él.</span><span class="sxs-lookup"><span data-stu-id="9dc12-158">Create a file named **nginx-public.json** and copy hello following contents into it.</span></span>

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

<span data-ttu-id="9dc12-159">Ejecute hello siguiente comando tooschedule Hola aplicación toorun de clúster de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="9dc12-159">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="9dc12-160">Obtener dirección IP pública de Hola de Hola DC/clúster pública agentes del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="9dc12-160">Get hello public IP address of hello DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="9dc12-161">Examinar dirección toothis devuelve sitio NGINX de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9dc12-161">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="9dc12-163">Escalado del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="9dc12-164">En los ejemplos anteriores de hello, una aplicación era la instancia de toomultiple escalado.</span><span class="sxs-lookup"><span data-stu-id="9dc12-164">In hello previous examples, an application was scaled toomultiple instance.</span></span> <span data-ttu-id="9dc12-165">infraestructura de DC/OS Hello también puede ser tooprovide escalado más o menos capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="9dc12-165">hello DC/OS infrastructure can also be scaled tooprovide more or less compute capacity.</span></span> <span data-ttu-id="9dc12-166">Esto se hace con hello [az acs escalar]() comando.</span><span class="sxs-lookup"><span data-stu-id="9dc12-166">This is done with hello [az acs scale]() command.</span></span> 

<span data-ttu-id="9dc12-167">número actual de hello toosee de agentes de DC/OS, usar hello [az acs mostrar](/cli/azure/acs#show) comando.</span><span class="sxs-lookup"><span data-stu-id="9dc12-167">toosee hello current count of DC/OS agents, use hello [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="9dc12-168">tooincrease Hola too5 de recuento, use hello [az acs escalar](/cli/azure/acs#scale) comando.</span><span class="sxs-lookup"><span data-stu-id="9dc12-168">tooincrease hello count too5, use hello [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="9dc12-169">Eliminación del clúster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="9dc12-170">Cuando ya no necesite, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, clúster de DC/OS y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="9dc12-170">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="9dc12-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9dc12-171">Next steps</span></span>

<span data-ttu-id="9dc12-172">En este tutorial, ha aprendido sobre tareas básicas de administración de DC/OS incluidos Hola siguientes.</span><span class="sxs-lookup"><span data-stu-id="9dc12-172">In this tutorial, you have learned about basic DC/OS management task including hello following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="9dc12-173">Creación de un clúster de ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="9dc12-174">Conectar el clúster toohello</span><span class="sxs-lookup"><span data-stu-id="9dc12-174">Connect toohello cluster</span></span>
> * <span data-ttu-id="9dc12-175">Instalar Hola DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="9dc12-175">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="9dc12-176">Implementar un clúster de toohello de aplicación</span><span class="sxs-lookup"><span data-stu-id="9dc12-176">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="9dc12-177">Escalar una aplicación en clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="9dc12-177">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="9dc12-178">Escalar los nodos del clúster Hola DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-178">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="9dc12-179">Eliminar el clúster de Hola DC/OS</span><span class="sxs-lookup"><span data-stu-id="9dc12-179">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="9dc12-180">Toohello por adelantado siguiente toolearn tutorial acerca de cómo cargar la aplicación equilibrio en DC/OS en Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc12-180">Advance toohello next tutorial toolearn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="9dc12-181">Aplicaciones de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="9dc12-181">Load balance applications</span></span>](container-service-load-balancing.md)