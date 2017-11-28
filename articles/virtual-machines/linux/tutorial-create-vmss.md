---
title: "Creación de un conjunto de escalado de máquinas virtuales Linux en Azure | Microsoft Docs"
description: "Cree e implemente una aplicación de alta disponibilidad en máquinas virtuales Linux con un conjunto de escalado de máquinas virtuales."
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 2b8d519e11f70eda164bd8f6e131a3989f242ab0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="9e76a-103">Creación de un conjunto de escalado de máquinas virtuales e implementación de una aplicación de alta disponibilidad en Linux</span><span class="sxs-lookup"><span data-stu-id="9e76a-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="9e76a-104">El conjunto de escalado de máquinas virtuales le permite implementar y administrar un conjunto de máquinas virtuales de escalado automático idénticas.</span><span class="sxs-lookup"><span data-stu-id="9e76a-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="9e76a-105">Puede escalar el número de máquinas virtuales del conjunto de escalado manualmente, o definir reglas de escalado automático basado en el uso de la CPU, la demanda de memoria o el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="9e76a-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="9e76a-106">En este tutorial, implementará un conjunto de escalado de máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="9e76a-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="9e76a-107">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="9e76a-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9e76a-108">Usar cloud-init para crear una aplicación para escalar</span><span class="sxs-lookup"><span data-stu-id="9e76a-108">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="9e76a-109">Crear un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9e76a-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="9e76a-110">Aumentar o disminuir el número de instancias en un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="9e76a-110">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="9e76a-111">Ver la información de conexión de las instancias del conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="9e76a-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="9e76a-112">Usar discos de datos con conjuntos de escalado</span><span class="sxs-lookup"><span data-stu-id="9e76a-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9e76a-113">Si decide instalar y usar la CLI localmente, para este tutorial es preciso que ejecute la CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="9e76a-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9e76a-114">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="9e76a-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="9e76a-115">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9e76a-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="9e76a-116">Introducción al conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="9e76a-116">Scale Set overview</span></span>
<span data-ttu-id="9e76a-117">El conjunto de escalado de máquinas virtuales le permite implementar y administrar un conjunto de máquinas virtuales de escalado automático idénticas.</span><span class="sxs-lookup"><span data-stu-id="9e76a-117">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="9e76a-118">Los conjuntos de escalado usan los mismos componentes que ha aprendido en el tutorial anterior sobre [Creación de máquinas virtuales de alta disponibilidad](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="9e76a-118">Scale sets use the same components as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="9e76a-119">Las máquinas virtuales de un conjunto de escalado se crean en un conjunto de disponibilidad y se distribuyen entre los dominios de error lógico y de actualización.</span><span class="sxs-lookup"><span data-stu-id="9e76a-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="9e76a-120">Las máquinas virtuales se crean según sea necesario en un conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="9e76a-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="9e76a-121">Defina reglas de escalado automático para controlar cómo y cuándo se agregan o se quitan las máquinas virtuales del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="9e76a-121">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="9e76a-122">Estas reglas se pueden desencadenar en función de métricas como la carga de la CPU, el uso de la memoria o el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="9e76a-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="9e76a-123">Los conjuntos de escalado admiten hasta 1000 máquinas virtuales cuando se usa una imagen de la plataforma de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e76a-123">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="9e76a-124">Para las cargas de trabajo de producción, puede que desee la [creación de una imagen de máquina virtual personalizada](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="9e76a-124">For production workloads, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="9e76a-125">Puede crear hasta 100 máquinas virtuales en un conjunto de escalado al usar una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="9e76a-125">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="9e76a-126">Creación de una aplicación para escalar</span><span class="sxs-lookup"><span data-stu-id="9e76a-126">Create an app to scale</span></span>
<span data-ttu-id="9e76a-127">Para su uso en producción, puede que desee [crear una imagen de máquina virtual personalizada](tutorial-custom-images.md) que incluya la instalación y configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9e76a-127">For production use, you may wish to [Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="9e76a-128">En este tutorial, vamos a personalizar las máquinas virtuales del primer arranque para ver rápidamente un conjunto de escalado en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="9e76a-128">For this tutorial, lets customize the VMs on first boot to quickly see a scale set in action.</span></span>

<span data-ttu-id="9e76a-129">En un tutorial anterior, aprendió [cómo personalizar una máquina virtual Linux en el primer arranque](tutorial-automate-vm-deployment.md) con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="9e76a-129">In a previous tutorial, you learned [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="9e76a-130">Pues bien, el mismo archivo de configuración cloud-init puede usarlo para instalar NGINX y ejecutar una aplicación sencilla Node.js "Hello World".</span><span class="sxs-lookup"><span data-stu-id="9e76a-130">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="9e76a-131">En el shell actual, cree un archivo denominado "*cloud-init.txt*" y pegue la siguiente configuración.</span><span class="sxs-lookup"><span data-stu-id="9e76a-131">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="9e76a-132">Por ejemplo, cree el archivo en Cloud Shell, no en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="9e76a-132">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="9e76a-133">Escriba `sensible-editor cloud-init.txt` para crear el archivo y ver una lista de editores disponibles.</span><span class="sxs-lookup"><span data-stu-id="9e76a-133">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="9e76a-134">Asegúrese de que todo el archivo cloud-init se copia correctamente, especialmente la primera línea:</span><span class="sxs-lookup"><span data-stu-id="9e76a-134">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```


## <a name="create-a-scale-set"></a><span data-ttu-id="9e76a-135">Creación de un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="9e76a-135">Create a scale set</span></span>
<span data-ttu-id="9e76a-136">Antes de poder crear un conjunto de escalado, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9e76a-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9e76a-137">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroupScaleSet* en la ubicación *eastus*:</span><span class="sxs-lookup"><span data-stu-id="9e76a-137">The following example creates a resource group named *myResourceGroupScaleSet* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="9e76a-138">Ahora, cree un conjunto de escalado de máquinas virtuales con [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="9e76a-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="9e76a-139">En el ejemplo siguiente se crea un conjunto de escalado denominado *myScaleSet*, se usa el archivo cloud-init para personalizar la máquina virtual y se generan claves SSH si estas no existen aún:</span><span class="sxs-lookup"><span data-stu-id="9e76a-139">The following example creates a scale set named *myScaleSet*, uses the cloud-init file to customize the VM, and generates SSH keys if they do not exist:</span></span>

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

<span data-ttu-id="9e76a-140">Se tardan unos minutos en crear y configurar todos los recursos de conjunto de escalado y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e76a-140">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span> <span data-ttu-id="9e76a-141">Hay tareas en segundo plano que continúan ejecutándose después de que la CLI de Azure vuelve a abrir el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="9e76a-141">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="9e76a-142">Es posible que tenga que esperar otros dos minutos antes de poder acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9e76a-142">It may be another couple of minutes before you can access the app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="9e76a-143">Permitir tráfico web</span><span class="sxs-lookup"><span data-stu-id="9e76a-143">Allow web traffic</span></span>
<span data-ttu-id="9e76a-144">Se creó automáticamente un equilibrador de carga como parte del conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e76a-144">A load balancer was created automatically as part of the virtual machine scale set.</span></span> <span data-ttu-id="9e76a-145">El equilibrador de carga distribuye el tráfico a través de un conjunto de máquinas virtuales definidas usando reglas de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="9e76a-145">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="9e76a-146">Puede aprender más información sobre los conceptos y la configuración del equilibrador de carga en el siguiente tutorial, [How to load balance virtual machines in Azure](tutorial-load-balancer.md) (Equilibrio de carga en máquinas virtuales de Azure).</span><span class="sxs-lookup"><span data-stu-id="9e76a-146">You can learn more about load balancer concepts and configuration in the next tutorial, [How to load balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="9e76a-147">Para permitir que el tráfico llegue a la aplicación web, cree una regla con [az network lb rule create](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="9e76a-147">To allow traffic to reach the web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="9e76a-148">En el ejemplo siguiente, se crea una regla denominada *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="9e76a-148">The following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a><span data-ttu-id="9e76a-149">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="9e76a-149">Test your app</span></span>
<span data-ttu-id="9e76a-150">Para ver la aplicación de Node.js en la web, obtenga la dirección IP pública del equilibrador de carga con [az network public-ip show](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="9e76a-150">To see your Node.js app on the web, obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="9e76a-151">En el ejemplo siguiente se obtiene la dirección IP de *myLoadBalancerRuleWeb* que se ha creado como parte del conjunto de escalado:</span><span class="sxs-lookup"><span data-stu-id="9e76a-151">The following example obtains the IP address for *myScaleSetLBPublicIP* created as part of the scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="9e76a-152">Escriba la dirección IP pública en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="9e76a-152">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="9e76a-153">Se muestra la aplicación, incluido el nombre de host de la máquina virtual a la que el equilibrador de carga distribuye el tráfico:</span><span class="sxs-lookup"><span data-stu-id="9e76a-153">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Ejecución de la aplicación Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="9e76a-155">Para ver el conjunto de escalado en funcionamiento, realice una actualización forzada del explorador web para ver cómo el equilibrador de carga distribuye el tráfico entre las máquinas virtuales del conjunto de escalado que ejecutan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9e76a-155">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="9e76a-156">Tareas de administración</span><span class="sxs-lookup"><span data-stu-id="9e76a-156">Management tasks</span></span>
<span data-ttu-id="9e76a-157">Durante el ciclo de vida del conjunto de escalado, debe ejecutar una o varias tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="9e76a-157">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="9e76a-158">Además, puede crear scripts para automatizar varias tareas de ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="9e76a-158">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="9e76a-159">La CLI de Azure 2.0 proporciona una forma rápida de realizar esas tareas.</span><span class="sxs-lookup"><span data-stu-id="9e76a-159">The Azure CLI 2.0 provides a quick way to do those tasks.</span></span> <span data-ttu-id="9e76a-160">A continuación, presentamos algunas tareas comunes.</span><span class="sxs-lookup"><span data-stu-id="9e76a-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="9e76a-161">Visualización de máquinas virtuales en un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="9e76a-161">View VMs in a scale set</span></span>
<span data-ttu-id="9e76a-162">Para ver una lista de las máquinas virtuales en ejecución en el conjunto de escalado, use [az vmss list-instances](/cli/azure/vmss#list-instances) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="9e76a-162">To view a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="9e76a-163">La salida es similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9e76a-163">The output is similar to the following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="9e76a-164">Aumento o disminución de instancias de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9e76a-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="9e76a-165">Para ver el número de instancias que tiene actualmente en un conjunto de escalado, use [az vmss show](/cli/azure/vmss#show) y realice consultas a *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="9e76a-165">To see the number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="9e76a-166">A continuación, puede aumentar o reducir manualmente el número de máquinas virtuales del conjunto de escalado con [az vmss scale](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="9e76a-166">You can then manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="9e76a-167">En el ejemplo siguiente se establece el número de máquinas virtuales en el conjunto de escalado en *5*:</span><span class="sxs-lookup"><span data-stu-id="9e76a-167">The following example sets the number of VMs in your scale set to *5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="9e76a-168">Las reglas de escalado automático le permiten definir cómo escalar o reducir verticalmente el número de máquinas virtuales en el conjunto de escalado en respuesta a la demanda, como el tráfico de red o el uso de CPU.</span><span class="sxs-lookup"><span data-stu-id="9e76a-168">Autoscale rules let you define how to scale up or down the number of VMs in your scale set in response to demand such as network traffic or CPU usage.</span></span> <span data-ttu-id="9e76a-169">Actualmente, no se pueden establecer estas reglas en la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="9e76a-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="9e76a-170">Use [Azure Portal](https://portal.azure.com) para configurar el escalado automático.</span><span class="sxs-lookup"><span data-stu-id="9e76a-170">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="9e76a-171">Obtención de información de conexión</span><span class="sxs-lookup"><span data-stu-id="9e76a-171">Get connection info</span></span>
<span data-ttu-id="9e76a-172">Para obtener información de conexión sobre las máquinas virtuales de los conjuntos de escalado, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="9e76a-172">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="9e76a-173">Este comando da como resultado la dirección IP pública y los puertos de cada máquina virtual que le permiten conectarse con SSH:</span><span class="sxs-lookup"><span data-stu-id="9e76a-173">This command outputs the public IP address and port for each VM that allows you to connect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="9e76a-174">Uso de discos de datos con conjuntos de escalado</span><span class="sxs-lookup"><span data-stu-id="9e76a-174">Use data disks with scale sets</span></span>
<span data-ttu-id="9e76a-175">Puede crear y usar discos de datos con conjuntos de escalado.</span><span class="sxs-lookup"><span data-stu-id="9e76a-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="9e76a-176">En un tutorial anterior, ha aprendido cómo [administrar discos de Azure](tutorial-manage-disks.md), donde se describían las prácticas recomendadas y mejoras de rendimiento para la creación de aplicaciones en los discos de datos en lugar de en el disco del SO.</span><span class="sxs-lookup"><span data-stu-id="9e76a-176">In a previous tutorial, you learned how to [Manage Azure disks](tutorial-manage-disks.md) that outlines the best practices and performance improvements for building apps on data disks rather than the OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="9e76a-177">Creación de conjunto de escalado con discos de datos</span><span class="sxs-lookup"><span data-stu-id="9e76a-177">Create scale set with data disks</span></span>
<span data-ttu-id="9e76a-178">Para crear un conjunto de escalado y conectar discos de datos, agregue el parámetro `--data-disk-sizes-gb` al comando [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="9e76a-178">To create a scale set and attach data disks, add the `--data-disk-sizes-gb` parameter to the [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="9e76a-179">En el ejemplo siguiente se crea un conjunto de escalado con discos de datos de *50*Gb conectados a cada instancia:</span><span class="sxs-lookup"><span data-stu-id="9e76a-179">The following example creates a scale set with *50*Gb data disks attached to each instance:</span></span>

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

<span data-ttu-id="9e76a-180">Cuando se quitan las instancias de un conjunto de escalado, también se quitan los discos de datos conectados.</span><span class="sxs-lookup"><span data-stu-id="9e76a-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="9e76a-181">Adición de discos de datos</span><span class="sxs-lookup"><span data-stu-id="9e76a-181">Add data disks</span></span>
<span data-ttu-id="9e76a-182">Para agregar un disco de datos a las instancias en el conjunto de escalado, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="9e76a-182">To add a data disk to instances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="9e76a-183">En el ejemplo siguiente se agrega un disco de *50* Gb a cada instancia:</span><span class="sxs-lookup"><span data-stu-id="9e76a-183">The following example adds a *50*Gb disk to each instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="9e76a-184">Desacoplamiento de discos de datos</span><span class="sxs-lookup"><span data-stu-id="9e76a-184">Detach data disks</span></span>
<span data-ttu-id="9e76a-185">Para quitar un disco de datos a las instancias en el conjunto de escalado, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="9e76a-185">To remove a data disk to instances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="9e76a-186">En el ejemplo siguiente se quita el disco de datos en el LUN *2* de cada instancia:</span><span class="sxs-lookup"><span data-stu-id="9e76a-186">The following example removes the data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="9e76a-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9e76a-187">Next steps</span></span>
<span data-ttu-id="9e76a-188">En este tutorial, ha creado un conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e76a-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="9e76a-189">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="9e76a-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9e76a-190">Usar cloud-init para crear una aplicación para escalar</span><span class="sxs-lookup"><span data-stu-id="9e76a-190">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="9e76a-191">Crear un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9e76a-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="9e76a-192">Aumentar o disminuir el número de instancias en un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="9e76a-192">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="9e76a-193">Ver la información de conexión de las instancias del conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="9e76a-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="9e76a-194">Usar discos de datos con conjuntos de escalado</span><span class="sxs-lookup"><span data-stu-id="9e76a-194">Use data disks in a scale set</span></span>

<span data-ttu-id="9e76a-195">Pase al siguiente tutorial para obtener más información sobre el concepto de equilibrio de carga de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e76a-195">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="9e76a-196">[Load balance virtual machines](tutorial-load-balancer.md) (Equilibrio de carga de máquinas virtuales)</span><span class="sxs-lookup"><span data-stu-id="9e76a-196">[Load balance virtual machines](tutorial-load-balancer.md)</span></span>